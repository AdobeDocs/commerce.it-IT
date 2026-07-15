---
title: Configurare AEM Assets per Commerce Optimizer
description: Scopri come configurare l'integrazione di AEM Assets per  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---


# Configura AEM Assets per [!DNL Adobe Commerce Optimizer]

[!BADGE Solo SaaS]{type=Positive tooltip="Applicabile solo ai progetti Adobe Commerce Optimizer."}

L&#39;integrazione di AEM Assets per [!DNL Adobe Commerce Optimizer] consente ai commercianti di utilizzare AEM Assets come soluzione centralizzata per la gestione delle risorse digitali per le immagini dei prodotti. Questa guida descrive la configurazione specifica di [!DNL Commerce Optimizer].

Il diagramma seguente offre una panoramica della sincronizzazione dei prodotti tra [!DNL Adobe Commerce Optimizer] e l&#39;integrazione di AEM Assets.

![Flusso da AEM Assets a [!DNL Commerce Optimizer]](../assets/aco-asset-sync-architecture.png){width="700"}

Questa integrazione dispone di due flussi di eventi indipendenti. Entrambi utilizzano [Adobe I/O Events](https://developer.adobe.com/events/docs/) per trasferire gli eventi a Assets Integration Service, ma ogni direzione utilizza il proprio provider di eventi:

* **Da AEM Assets ad Assets Integration Service**: quando una risorsa viene approvata, rifiutata o rimossa, l&#39;evento viene consegnato ad Assets Integration Service. Il servizio associa le risorse ai prodotti utilizzando `match-by-SKU` (basato su metadati) o un [programma di corrispondenza personalizzato (App Builder)](../synchronize/custom-match.md){target=_blank}, quindi invia i mapping `product-asset` a [!DNL Commerce Optimizer], dove vengono memorizzati come livelli di prodotto.

  >[!NOTE]
  >
  >Il livello di catalogo `AEM-Assets` utilizzato dall&#39;integrazione viene creato automaticamente durante l&#39;onboarding. Non è necessario crearlo in anticipo. Per informazioni generali sul funzionamento dei livelli del catalogo e sul comportamento del livello AEM-Assets, vedi [Livello AEM-Assets](../../optimizer/setup/catalog-layer.md#aem-assets-layer).

* **Da [!DNL Adobe Commerce Optimizer] a Assets Integration Service**: quando un prodotto viene aggiornato in [!DNL Commerce Optimizer], l&#39;evento viene consegnato a Assets Integration Service. Il servizio sincronizza eventuali mapping di risorse corrispondenti in [!DNL Commerce Optimizer].

## Limitazioni

L&#39;integrazione di [!DNL Commerce Optimizer] presenta le seguenti limitazioni:

### Vincoli relativi ai livelli

* Utilizza un livello dedicato per i contenuti AEM Assets.

  I payload inviati da AEM Assets popolano un livello di catalogo Commerce Optimizer. I valori in tale livello sovrascrivono gli attributi del catalogo di base in cui vengono forniti i campi. Quando l’integrazione omette un campo nel payload, i valori corrispondenti in quel livello possono essere sovrascritti con valori vuoti. La condivisione di un livello con flussi di lavoro Commerce non correlati, o il riutilizzo di un livello che già memorizza dati di prodotto non AEM-Assets, può causare **perdita di dati non intenzionale** o sovrascritture confuse. Riserva il nome del livello (ad esempio il **`AEM-Assets`** predefinito) principalmente per la sincronizzazione delle immagini del prodotto basata su AEM.

* L’integrazione supporta un’origine catalogo per tenant: una singola lingua e un livello denominato. Al momento, la configurazione di più livelli AEM-Assets o di più impostazioni locali per lo stesso tenant non è supportata.

* Il riutilizzo di un livello esistente o la condivisione di un livello con flussi di lavoro non correlati è una causa frequente di casi di supporto prevenibili.

### Altri vincoli

* **Solo immagini**: l&#39;integrazione non supporta video o altri tipi di file multimediali in questa fase.
* **Nessuna immagine categoria**: la sincronizzazione immagine categoria non è disponibile. Le immagini delle categorie da AEM Assets per il selettore Assets (inserimento nell’interfaccia utente) non sono supportate.
* **Nessuna distinzione tra più siti**: l&#39;integrazione non gestisce più siti. Un&#39;immagine associata a un prodotto viene visualizzata allo stesso modo su tutti i canali e i criteri.
* **Posizione/ordinamento immagine**: la posizione e l&#39;ordinamento delle immagini non sono supportati.
* **Il prodotto deve esistere**: se il prodotto non esiste in [!DNL Commerce Optimizer], il livello non viene creato per la mappatura prodotto-risorsa.

## Prerequisiti

Prima di configurare l’integrazione, assicurati di disporre di:

* Un&#39;istanza [!DNL Adobe Commerce Optimizer] attiva con adesione **Product Visuals** (bundle Dynamic Media con funzionalità OpenAPI + [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime)) o una licenza AEM Assets fornita dal cliente (ad esempio, **AEM Assets Ultimate**) con Dynamic Media abilitato.
* Accesso a un ambiente AEM Assets as a Cloud Service.
* Sia [!DNL Commerce Optimizer] che AEM Assets nella stessa organizzazione Adobe IMS.
* Dynamic Media con OpenAPI abilitato nell&#39;ambiente AEM Assets (consulta [Configurare il progetto AEM Assets](configure-aem.md#prerequisites) per i passaggi di abilitazione).

### Configurare prima AEM Assets

Per supportare l&#39;integrazione, configurare il progetto AEM Assets e gli ambienti prima di iniziare il processo per integrare AEM Assets con [!DNL Commerce Optimizer]. Ciò include l’abilitazione di Dynamic Media con funzionalità OpenAPI e la disponibilità di schemi di metadati, eventi e interfaccia utente di Commerce nel progetto AEM.

* [!BADGE Consigliato]{type=Positive} In AEM versione `2026.5.26309` e successive, abilita l&#39;integrazione da Cloud Manager senza distribuzione del codice. Segui [Abilitare l&#39;integrazione Commerce (self-service)](configure-aem.md#enable-aem-commerce-self-service).

* Nelle versioni precedenti di AEM, distribuire manualmente il pacchetto `assets-commerce`.
Segui [Installare manualmente il pacchetto assets-commerce](configure-aem.md#install-the-assets-commerce-package-manually).

>[!TIP]
>
> Puoi controllare la versione corrente di AEM dal menu in alto a destra: **[!UICONTROL Help]** > **[!UICONTROL About AEM]**.

## Onboarding

>[!IMPORTANT]
>
>Prima di inviare un ticket di supporto per abilitare l&#39;integrazione con [!DNL Commerce Optimizer], completare il processo per [Configurare AEM Assets](#configure-aem-assets-first). Il supporto richiede la configurazione degli ambienti e del progetto AEM Assets per supportare l&#39;integrazione AEM Commerce, inclusa la distribuzione del pacchetto `assets-commerce` (o equivalente self-service) per metadati ed eventi. L’apertura di un ticket prima che AEM sia configurato può ritardare l’onboarding.

Per integrare AEM Assets con [!DNL Commerce Optimizer], il supporto Adobe deve registrare l&#39;istanza Adobe Commerce Optimizer con Assets Integration Service e sottoscriverla a:

* Eventi AEM Assets (risorsa approvata, aggiornata, rimossa)
* [!DNL Commerce Optimizer] eventi catalogo (prodotto creato, aggiornato)

Per avviare il processo, [creare un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) che includa le seguenti informazioni:

* **[!DNL Adobe Commerce Optimizer]ID tenant** (ID istanza) trovato nell&#39;URL [!DNL Commerce Optimizer] o nell&#39;interfaccia utente di Commerce Cloud Manager.
* **ID programma AEM e ID ambiente** che hai configurato quando [hai configurato AEM Assets](#configure-aem-assets-first) per l&#39;integrazione.
* **Regola corrispondente**: corrisponde per SKU o [corrispondenza esterna (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Livello**: il nome del livello del catalogo con cui registrare il tenant (vedi **Vincoli relativi ai livelli**). Specificare un nome personalizzato solo se intenzionale. In caso contrario, verrà utilizzato il nome predefinito **`AEM-Assets`**.
* **Impostazioni locali**: le impostazioni locali di origine del catalogo con cui registrare il tenant (ad esempio, `en-US`). Queste impostazioni locali devono corrispondere a quelle utilizzate nella vista catalogo e nei dati del catalogo prodotti.

### Configurare la vista catalogo

Dopo la registrazione del tenant [!DNL Commerce Optimizer], configura la vista catalogo in modo che la vetrina e le API facciano emergere i dati immagine basati su AEM:

* **Selezionare l&#39;origine del catalogo (impostazioni locali)** — Selezionare le stesse impostazioni locali specificate nel ticket di supporto (ad esempio **`en-US`**). L’integrazione registra una lingua per tenant; una mancata corrispondenza impedisce la visualizzazione delle immagini sincronizzate nella vista catalogo prevista.
* **Assegna il livello Catalogo** — Assegna il livello **`AEM-Assets`** (o il nome del livello personalizzato dal ticket) a tale vista catalogo.

Se le impostazioni locali o il livello non sono assegnati correttamente, i dati immagine **non vengono visualizzati** o si comportano in modo imprevisto, anche se la sincronizzazione è stata eseguita a monte.

## Ssincronizzazione

Una volta configurata, l&#39;integrazione sincronizza automaticamente `product-asset` mappature.

Per ulteriori informazioni, vedere [Corrispondenza automatica personalizzata](../synchronize/custom-match.md).

### Esempio di flusso di lavoro Corrispondenza per SKU

Un flusso tipico quando si aggiunge una risorsa esistente a un nuovo prodotto:

1. Crea il prodotto in [!DNL Commerce Optimizer] (tramite API o acquisizione dati). Il prodotto può esistere inizialmente senza immagini.

1. In AEM Assets, apri la risorsa da mappare sul prodotto.

1. Aggiungi lo SKU del prodotto ai metadati **commerce:skus** e assegna i ruoli immagine (ad esempio, `thumbnail`, `image`).

1. Approva la risorsa per la consegna. Questo attiva l’evento elaborato dal servizio di integrazione Assets.

1. Il servizio di integrazione di Assets invia la mappatura prodotto-immagine a [!DNL Commerce Optimizer]. Il prodotto in [!DNL Commerce Optimizer] è stato aggiornato con le immagini della risorsa.

1. Verifica che l’immagine sia visibile. Attendere alcuni minuti per il completamento della sincronizzazione, quindi controllare il prodotto nell&#39;interfaccia utente [!DNL Commerce Optimizer] o eseguire una query sulle API storefront per confermare che l&#39;immagine sia stata restituita.

## Gestione ruolo immagine

Quando un prodotto dispone di più risorse che utilizzano lo stesso ruolo immagine (ad esempio, due risorse con il ruolo `thumbnail`), l&#39;integrazione assicura che solo una risorsa mantenga tale ruolo per evitare ruoli duplicati nel livello [!DNL Commerce Optimizer] e comportamenti imprevisti nella vetrina.

**Comportamento:** Quando viene inviato un aggiornamento da AEM Assets, la risorsa aggiornata più di recente riceve il ruolo immagine (ad esempio, `thumbnail`) e il ruolo viene rimosso dalla risorsa precedente che lo aveva. Questo impedisce la visualizzazione di ruoli immagine duplicati nella vetrina.

## Altri argomenti correlati

* [Visualizzazioni prodotto](../../optimizer/setup/product-visuals.md)
* [Configurare il progetto AEM Assets](configure-aem.md)
* [Corrispondenza automatica personalizzata](../synchronize/custom-match.md)
* [Panoramica dell’integrazione di AEM Assets](../overview.md)
