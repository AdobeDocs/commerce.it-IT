---
title: Risoluzione dei problemi relativi a  [!DNL SaaS Data Export]
description: Scopri come diagnosticare e risolvere comportamenti di sincronizzazione imprevisti [!DNL SaaS Data Export] causati da configurazione errata, impostazioni di indicizzazione o interpretazione errata dei risultati di sincronizzazione.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 991
ht-degree: 0%

---


# Risoluzione dei problemi relativi a [!DNL SaaS Data Export]

In questa pagina sono descritti i comportamenti che è possibile osservare durante l&#39;utilizzo di [!DNL SaaS Data Export] che sono in genere causati da una configurazione errata o da un&#39;interpretazione errata dei risultati di sincronizzazione. Utilizza le descrizioni di seguito per identificare la causa principale e applicare la risoluzione appropriata.

## Prodotto configurabile o in bundle mancante nei servizi Commerce {#configurable-bundle-missing}

**Problema:** un prodotto configurabile o bundle ha lo stato *Enabled* in [!DNL Adobe Commerce] ma non è restituito nella vetrina o viene visualizzato con lo stato *Disabled* nei servizi SaaS di Commerce.

**Causa:** lo stato effettivo dei prodotti compositi dipende dallo stato dei prodotti secondari e non solo dallo stato del prodotto principale. I servizi SaaS di Commerce riflettono questo stato calcolato:

- **Prodotti configurabili** - almeno una variante di prodotto deve essere abilitata.
- **Prodotti bundle** - almeno un prodotto deve essere abilitato per ogni opzione di bundle richiesta.

Se queste condizioni non vengono soddisfatte, il prodotto padre viene considerato disabilitato anche se il suo stato è impostato su *Abilitato*.

**Soluzione:**

- Per i prodotti configurabili, verifica che almeno una variante di prodotto semplice associata sia abilitata e assegnata alla visualizzazione corretta del sito web e dello store.
- Per i prodotti bundle, verifica che per ogni opzione di bundle richiesta sia abilitato almeno un prodotto secondario. Un’opzione obbligatoria con tutti gli elementi secondari disabilitati fa sì che l’intero bundle venga trattato come disabilitato.
- Dopo aver abilitato i prodotti secondari appropriati, attiva una risincronizzazione o attendi la successiva sincronizzazione pianificata, quindi conferma lo stato aggiornato nei servizi SaaS di Commerce.

## Prezzi non aggiornati dopo l&#39;attivazione della regola prezzo catalogo {#prices-not-updated}

**Problema:** dopo l&#39;attivazione di una regola dei prezzi di catalogo tramite la funzione Aggiornamento pianificato, i prezzi non vengono aggiornati. `commerce-data-export.log` mostra `synced: 0` per il feed `prices` dopo l&#39;applicazione degli aggiornamenti pianificati.

**Causa:** una situazione di tipo &quot;race condition&quot; può verificarsi tra gruppi cron quando si utilizzano gli aggiornamenti pianificati per le regole dei prezzi di catalogo. È possibile che l&#39;indicizzatore `catalog_data_exporter_product_prices` venga eseguito prima che la relativa dipendenza, l&#39;indice `catalogrule_product`, abbia completato la ricostruzione. Di conseguenza, l’esportatore di prezzi legge i dati non aggiornati e non esporta modifiche.

**Soluzione:**

La correzione immediata per questo problema è una soluzione alternativa: configurare entrambi i gruppi cron in modo che vengano eseguiti in sequenza per eliminare la race condition:

1. Vai a **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Cron (Scheduled Tasks)]**.
1. Imposta **[!UICONTROL Use Separate Process]** su **[!UICONTROL No]** per entrambi:
   - Opzioni di configurazione per il gruppo: **[!UICONTROL index]**
   - Opzioni di configurazione per il gruppo: **[!UICONTROL staging]**
1. Svuota la cache di configurazione dopo il salvataggio.

>[!NOTE]
>
>Con entrambi i gruppi in esecuzione in-process e in sequenza, una reindicizzazione completa lenta blocca l’esecuzione dello staging fino al suo completamento. Nei cataloghi di grandi dimensioni, questo potrebbe ritardare gli aggiornamenti di staging.

## Discrepanza dei dati del catalogo tra [!DNL Adobe Commerce] e i servizi connessi {#catalog-data-discrepancy}

**Problema:** i dati di prodotto visualizzati nei servizi Commerce connessi (ad esempio [!DNL Live Search] o [!DNL Product Recommendations]) non corrispondono ai dati del catalogo in [!DNL Adobe Commerce]. Ad esempio, il nome, il prezzo o la descrizione di un prodotto appaiono obsoleti o errati nella vetrina.

**Causa:** dopo l&#39;attivazione di una risincronizzazione, l&#39;aggiornamento dei dati può richiedere fino a un&#39;ora e può essere riflesso nei componenti dell&#39;interfaccia utente. Se la discrepanza persiste oltre tale finestra, è possibile che l&#39;elemento non sia stato acquisito dall&#39;ultima sincronizzazione o che la sincronizzazione non abbia rilevato una modifica perché i dati del feed sono già contrassegnati come aggiornati.

**Soluzione:**

1. Dalla vetrina Commerce, apri i risultati della ricerca. Quindi, seleziona il prodotto in questione per aprirne la vista dettagliata.
1. Copiare l&#39;output JSON e verificare che corrisponda a quello presente nel catalogo [!DNL Commerce].
1. Se il contenuto non corrisponde, apporta una modifica minore al prodotto nel catalogo, ad esempio aggiungendo uno spazio o un punto, per forzare il rilevamento della modifica.
1. Attendere la risincronizzazione o attivare una risincronizzazione manuale dalla CLI o dalla pagina [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) nell&#39;amministratore.

Per ulteriori informazioni sulla risoluzione dei problemi relativi ai dati del catalogo in [!DNL Product Recommendations], vedere [Risoluzione dei problemi relativi al modulo Consigli di prodotto](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce) nella Knowledge Base di Commerce.

## Sincronizzazione dati non in esecuzione secondo pianificazione {#sync-not-on-schedule}

**Problema:** la sincronizzazione dei dati non viene eseguita secondo la pianificazione oppure non viene sincronizzato alcun elemento nonostante le modifiche apportate al prodotto in [!DNL Adobe Commerce].

**Causa:** Le cause più comuni sono processi cron non in esecuzione o indicizzatori non configurati in modalità **[!UICONTROL Update by Schedule]**.

**Soluzione:**

- [Verificare che i processi cron siano in esecuzione](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Verificare che gli indicizzatori per i feed seguenti siano impostati su **[!UICONTROL Update by Schedule]**: Attributi catalogo, Prodotto, Sostituzioni prodotto e Variante prodotto. Controllare da [[!UICONTROL Index Management]](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/tools/index-management) nell&#39;amministratore di Commerce o utilizzare CLI: `bin/magento indexer:show-mode | grep -i feed`.

## Stato della sincronizzazione del catalogo non riuscito {#catalog-sync-failed}

**Problema:** la sincronizzazione del catalogo mostra uno stato **Non riuscito** nella pagina **[!UICONTROL Data Feed Sync Status]**.

**Causa:** Si è verificato un errore irreversibile durante la fase di raccolta o invio dei dati. Le cause più comuni includono problemi di autenticazione API, errori di rete o errori di convalida dei dati.

**Soluzione:**

1. Per informazioni dettagliate sull’errore, consulta i registri degli errori di esportazione dei dati. Consulta [Esaminare i registri e risolvere i problemi](logging.md) per il formato del registro e le opzioni di registrazione estese:
   - `var/log/commerce-data-export-errors.log` per errori durante la raccolta dati.
   - `var/log/saas-export-errors.log` per gli errori durante l&#39;invio dei dati.
1. Se l&#39;errore non è correlato alla configurazione o a un&#39;estensione di terze parti, [invia un ticket di supporto](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) con le voci di registro pertinenti.

## Il registro mostra i messaggi &quot;operazione ignorata - elaborazione bloccata&quot; {#process-locked}

**Problema:** Il file `commerce-data-export.log` contiene voci simili alle seguenti:

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

**Causa:** Questo è un comportamento previsto, non un errore. Il messaggio viene visualizzato quando si tenta di eseguire una sincronizzazione parziale attivata da cron mentre è già in corso una reindicizzazione completa o `saas:resync`. L&#39;estensione [!DNL SaaS Data Export] utilizza un meccanismo di blocco del feed per impedire operazioni di sincronizzazione simultanee in conflitto.

**Soluzione:**

Non è richiesta alcuna azione. Una volta che il processo in esecuzione completa e rilascia il blocco, l’esecuzione successiva del cron rileva e sincronizza eventuali modifiche in sospeso. Per informazioni dettagliate sul funzionamento del meccanismo di blocco, vedere [Meccanismo di blocco del feed per l&#39;esportazione dei dati SaaS](../feed-lock-mechanism.md).

>[!MORELIKETHIS]
>
> - [Esaminare i registri e risolvere i problemi](logging.md)
> - [Riferimento codici di registro](log-codes-reference.md)
> - [Meccanismo di blocco del feed per l&#39;esportazione dei dati SaaS](../feed-lock-mechanism.md)
