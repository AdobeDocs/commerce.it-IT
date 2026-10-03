---
title: Monitorare la sincronizzazione della visualizzazione catalogo per i cataloghi condivisi B2B
last-update: 2026-09-03
description: Utilizzare la pagina Stato di sincronizzazione della visualizzazione del catalogo per monitorare e riconciliare i dati di visualizzazione del catalogo, i criteri, il riferimento al listino prezzi e i dati di configurazione chiave sincronizzati con Adobe Commerce Optimizer.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: 1fd5e3d84d5249ce96014cae46e045528d2790d0
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%
---

# Monitorare la sincronizzazione della visualizzazione catalogo per i cataloghi condivisi B2B

Tracciare la sincronizzazione della vista del catalogo B2B da [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer] utilizzando il dashboard [!UICONTROL Catalog View Sync Status] nell&#39;amministrazione di Commerce.

[!UICONTROL Catalog View Sync Status] verifica che le configurazioni della vista catalogo, del criterio, del riferimento del listino prezzi e della chiave di accesso con restrizioni per ogni catalogo condiviso B2B siano presenti in [!DNL Adobe Commerce Optimizer] e corrispondano alla configurazione [!DNL Adobe Commerce]. Per tenere traccia della sincronizzazione di prodotti, prezzi e feed di categoria, vedere [Gestire la sincronizzazione dei dati](data-sync-status.md#verify-that-the-data-sync-is-working).

## Accedere alla pagina dello stato di sincronizzazione {#access-the-sync-status-page}

Dall&#39;amministratore di Commerce, passa a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Catalog View Sync Status]**.

![Pagina Stato sincronizzazione visualizzazione catalogo per monitorare lo stato di sincronizzazione della visualizzazione del catalogo, dei criteri, del listino prezzi dedicato e delle configurazioni delle chiavi di accesso in Adobe Commerce Optimizer](assets/catalog-view-sync-status.png){width="600" zoomable="yes"}

La pagina contiene tre schede: [!UICONTROL Catalog Views], [!UICONTROL Orphaned in ACO] e [!UICONTROL Deleted].

## Interpretare lo stato di sincronizzazione per i cataloghi condivisi {#interpret-sync-status}

Nella scheda [!UICONTROL Catalog View] ogni riga rappresenta una visualizzazione di catalogo condiviso personalizzata proiettata da una combinazione di visualizzazione catalogo e visualizzazione archivio condivisa. La proiezione è costituita dalla vista catalogo, dai criteri, dal riferimento del listino prezzi e dai dati di configurazione con chiave di accesso limitato che [!DNL Commerce Optimizer Connector] esporta in [!DNL Adobe Commerce Optimizer] per il catalogo condiviso. Utilizza le informazioni sullo stato per determinare se i dati inviati all’esperienza di vetrina dell’azienda sono completi e corretti. Nella tabella seguente sono riepilogati i valori di stato più comuni e il loro significato per il catalogo condiviso:

| Stato | Che cosa significa per il catalogo condiviso |
| --- | --- |
| **Danneggiato** | Qualcosa è stato cambiato direttamente in [!DNL Adobe Commerce Optimizer], ad esempio il criterio o il listino prezzi collegato. L&#39;azienda potrebbe vedere l&#39;assortimento o i prezzi errati fino a quando non risolvi il problema. Questo può accadere anche se la chiave di accesso, il nome della visualizzazione o l’origine vengono modificati in Commerce Optimizer. |
| **Non riuscito** | La visualizzazione del catalogo non esiste in [!DNL Adobe Commerce Optimizer] o se il periodo di tolleranza scade prima che venga effettuata la prima proiezione. (Vedi [Configurare le impostazioni di sincronizzazione della vista catalogo ACO](#configure-aco-catalog-view-sync-settings)). Se lo stato di sincronizzazione di un catalogo è `Failed`, la società non può accedere all&#39;esperienza di vetrina del catalogo condiviso. |
| **Ritiro** | Hai eliminato il catalogo condiviso in [!DNL Adobe Commerce]. La vista catalogo è ancora accessibile fino alla scadenza del periodo di tolleranza per l’eliminazione. Il periodo di tolleranza predefinito è di sette giorni. È possibile modificare il valore predefinito aggiornando le [impostazioni di sincronizzazione della visualizzazione catalogo](#configure-aco-catalog-view-sync-settings). |
| **Orfano** | La visualizzazione o la chiave del catalogo è stata creata direttamente in [!DNL Adobe Commerce Optimizer] Studio, non dal connettore. Vedi [Rivedi voci orfane ed eliminate](#review-orphaned-and-deleted-entries). |

[!UICONTROL Healthy], [!UICONTROL Pending] e [!UICONTROL Deleted] sono stati informativi che non richiedono alcun intervento. Per l&#39;elenco completo, vedere [Sincronizzare i valori di stato](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/catalog-view-sync-status#sync-status-values){target="_blank"} nella *Guida dell&#39;amministratore di Commerce*.

### Configura le impostazioni di sincronizzazione della vista catalogo ACO {#configure-aco-catalog-view-sync-settings}

Dall&#39;amministratore [!DNL Adobe Commerce] (non da [!DNL Adobe Commerce Optimizer] Studio), passa a **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Catalog View Sync]** per controllare in che modo il connettore esegue le eliminazioni e le creazioni e se ripara automaticamente la deriva.

![Pagina di configurazione della sincronizzazione della visualizzazione del catalogo ACO che mostra le sezioni Eliminazione, Creazione e Riconciliatore di deriva](assets/aco-catalog-view-sync-configuration.png){width="600" zoomable="yes"}

- **[!UICONTROL Deletion Grace Period (days)]** - Numero di giorni in cui la visualizzazione del catalogo condiviso eliminato, il criterio e i metadati vengono conservati in [!DNL Adobe Commerce Optimizer] prima di essere rimossi. Predefinito su sette giorni. Impostare su `0` per rimuovere immediatamente la proiezione, senza periodo di tolleranza.

- **[!UICONTROL Creation Grace Period (days)]** - Numero di giorni in cui una visualizzazione catalogo appena registrata può attendere che la prima proiezione sia [!DNL Adobe Commerce Optimizer] se segnalata come [!UICONTROL Pending]. Se il periodo di tolleranza scade senza una proiezione, lo stato diventa [!UICONTROL Failed]. Impostazione predefinita: 1.

- **[!UICONTROL Enabled]** (Riconciliatore di deriva): esegue il riconciliatore di deriva pianificato che confronta [!DNL Adobe Commerce Optimizer] con lo stato di proiezione [!DNL Adobe Commerce] e corregge o segnala una divergenza.

- **[!UICONTROL Automatically Repair Drift]** - Se impostata su **[!UICONTROL Yes]**, l&#39;esecuzione pianificata converge [!DNL Adobe Commerce Optimizer] in [!DNL Adobe Commerce] per la deriva riparabile. Se impostata su **[!UICONTROL No]**, l&#39;esecuzione pianificata rileva solo la deriva dei registri e rileva la deriva; le voci orfane vengono sempre segnalate, mai rimosse automaticamente. Questa impostazione ha effetto solo sul riconciliatore pianificato. L&#39;azione **[!UICONTROL Reconcile & Repair]** in questa pagina corregge sempre la deriva. Vedere [Scegliere monitoraggio o ripristino](#choose-monitoring-or-repair).

Per informazioni dettagliate su ciascuna impostazione, vedere [Configurazione sincronizzazione visualizzazione catalogo ACO](https://experienceleague.adobe.com/en/docs/commerce-admin/configuration-reference/services/aco-catalog-view-sync.md) nella *[!DNL Commerce Admin]Guida*.

## Scegli monitoraggio o riparazione {#choose-monitoring-or-repair}

[!DNL Adobe Commerce] è sempre la fonte di verità per la vista catalogo, i criteri, il listino prezzi e le configurazioni chiave per i cataloghi condivisi B2B. Se l&#39;utente o un altro amministratore ha modificato un criterio, un listino prezzi o un&#39;impostazione di configurazione delle chiavi direttamente in [!DNL Adobe Commerce Optimizer] Studio, la riconciliazione segnala le differenze di configurazione come deviazione.

- Selezionare **[!UICONTROL Reconcile]** per verificare la deriva senza modificare nulla, in modo da poter esaminare le differenze prima di agire.
- Selezionare **[!UICONTROL Reconcile & Repair]** per ripristinare la configurazione prevista per qualsiasi deriva riparabile.

Per esaminare cosa è cambiato e perché, apri la pagina dei dettagli di una visualizzazione catalogo e controlla la cronologia delle modifiche apportate.

## Rivedi voci orfane ed eliminate {#review-orphaned-and-deleted-entries}

Le schede **[!UICONTROL Orphaned in ACO]** e **[!UICONTROL Deleted]** coprono due casi che il connettore non può risolvere automaticamente perché non è presente alcun catalogo condiviso di [!DNL Adobe Commerce] su cui eseguire la riconciliazione:

- **[!UICONTROL Orphaned in ACO]** - Il connettore segnala le entità orfane nello stato di sincronizzazione e durante la riconciliazione della deriva. Non le adotta o le elimina automaticamente anche se la riconciliazione viene eseguita con il ripristino abilitato.

  Un&#39;entità è orfana quando esiste in [!DNL Adobe Commerce Optimizer] ma il connettore non la tiene traccia né la associa a una visualizzazione di catalogo tracciata. Ciò può verificarsi quando un’entità viene creata manualmente, da un’altra integrazione o lasciata indietro dopo un’operazione del connettore interrotta.

  - **Visualizzazioni catalogo** - Il connettore non tiene traccia della visualizzazione. Selezionare il collegamento della visualizzazione catalogo per aprire la pagina dei dettagli della visualizzazione catalogo in [!DNL Adobe Commerce Optimizer] Studio. Se la vista catalogo non è più necessaria, rimuoverla.

  - **Chiavi di accesso limitate**—Nessuna vista di catalogo live fa riferimento alla chiave. Selezionare il collegamento della visualizzazione catalogo per aprire la pagina dei dettagli della visualizzazione catalogo in [!DNL Adobe Commerce Optimizer] Studio. Rivedi la chiave di accesso configurata e rimuovila se non è più necessaria.

  - **Criteri** - Il connettore non tiene traccia del criterio e non vi fa riferimento alcuna visualizzazione di catalogo live. Selezionare il collegamento al criterio per aprirlo in [!DNL Adobe Commerce Optimizer] Studio.  Rivederlo e rimuoverlo se non è più necessario.

- **[!UICONTROL Deleted]** - È stato eliminato un catalogo condiviso in [!DNL Adobe Commerce] e la relativa proiezione della vista catalogo è stata successivamente rimossa. Queste righe vengono conservate per 90 giorni come registrazione di ciò che è stato rimosso.

>[!MORELIKETHIS]
>
> - [Monitoraggio dello stato di sincronizzazione della visualizzazione del catalogo](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/catalog-view-sync-status.md){target="_blank"} — Riferimento completo alla documentazione per la pagina Stato di sincronizzazione della visualizzazione del catalogo nella *Guida per l&#39;amministratore di Commerce* —>
> - [Gestire la sincronizzazione dei dati](data-sync-status.md): verificare la sincronizzazione di prodotti, prezzi e feed di categoria
> - [Visualizzazioni catalogo privato](/help/optimizer/setup/private-catalog-view.md) — Scopri cos’è una visualizzazione catalogo privato gestita dal connettore
> - [Chiavi di accesso con restrizioni](/help/optimizer/setup/restricted-access-keys.md) - Informazioni sul funzionamento delle chiavi gestite dal connettore
> - [Monitorare le modifiche al catalogo condiviso B2B](get-started-b2b-shared-catalogs.md#monitor-b2b-shared-catalog-changes) — Scopri cosa automatizza il connettore per i cataloghi condivisi B2B
