---
title: Configurare l’integrazione
description: Scopri come collegare il progetto Adobe Commerce e i progetti Experience Manager Assets per abilitare la sincronizzazione delle risorse tra questi due sistemi.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
TQID: 'https://experienceleague.adobe.com/MM-neGrH-N8xBcCwLgnsaIrIjhbX6uYL5kS41QdV79I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 5e9c42e5c93ac81604aa38bf3e55c5df729650a0
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 1%
---
# Configurare l’integrazione

Configura l’integrazione connettendo Commerce all’istanza di AEM Assets e selezionando la strategia di corrispondenza per la sincronizzazione delle risorse.

Dopo aver identificato il progetto AEM Assets, seleziona la regola corrispondente per la sincronizzazione delle risorse tra Adobe Commerce e AEM Assets.

* **[!UICONTROL Match by product SKU]**—Regola predefinita che corrisponde allo SKU nei metadati della risorsa con [SKU prodotto Commerce](https://experienceleague.adobe.com/it/docs/commerce-operations/implementation-playbook/glossary#sku) per garantire che le risorse siano associate ai prodotti corretti.

* **[!UICONTROL Custom match]** - Regola di corrispondenza per scenari più complessi o requisiti aziendali specifici che richiedono una logica di corrispondenza personalizzata. L’implementazione della corrispondenza personalizzata richiede lo sviluppo di codice personalizzato in Adobe Developer App Builder per definire il modo in cui le risorse vengono associate ai prodotti. Vedi [Corrispondenza automatica personalizzata](../synchronize/custom-match.md).

Per la configurazione iniziale, utilizzare la regola predefinita **[!UICONTROL Match by product SKU]**.

## Requisiti

Prima di configurare l’integrazione di AEM Assets, verifica di aver completato i seguenti passaggi:

* [Configurare il progetto AEM Assets](configure-aem.md)

* [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} [Installa i pacchetti Adobe Commerce](configure-commerce.md) per aggiungere l&#39;estensione e generare le credenziali e le connessioni necessarie per utilizzare l&#39;estensione.

* [Autorizzazioni utente e IMS](permissions.md): configura le autorizzazioni richieste per il selettore risorse, la selezione dell&#39;ambiente AEM e il mapping dei domini.

## Configurare la connessione

![Configurazione dell&#39;integrazione AEM Assets con valori di ambiente e dominio di esempio](../assets/aem-assets-view.png){width="900" zoomable="yes"}

1. Dall&#39;amministratore di Commerce, passa a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

>[!INFO]
>
> L’integrazione di AEM Assets supporta solo la configurazione nell’ambito globale (predefinito). La configurazione a livello di sito web non è supportata. Quando tenti di configurare l’integrazione a livello di sito web, il sistema ignora le impostazioni a livello di sito web e utilizza invece i valori di configurazione globale.

1. [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Inserisci **[!UICONTROL Asset Selector IMS Client ID]**.

   Questo ID è necessario per abilitare il Selettore risorse. Per ottenere questo ID, consulta [Autorizzazioni utente e IMS](permissions.md). Per informazioni dettagliate sul selettore risorse, vedere [Selezione manuale delle risorse](../synchronize/asset-selector-integration.md).

1. Da **[!UICONTROL AEM Environment]**, selezionare l&#39;ambiente configurato in [Configura il progetto AEM Assets](configure-aem.md).

   L’elenco include gli ambienti AEM per i quali l’utente dispone di un profilo di prodotto Author o Delivery. Se manca l&#39;ambiente previsto, esaminare [Autorizzazioni utente e IMS](permissions.md).

   Se nella configurazione vengono visualizzati campi **[!UICONTROL Program ID]** e **[!UICONTROL Environment ID]** separati, specificare gli identificatori per l&#39;ambiente. Per l&#39;immissione manuale, copiarli da AEM Cloud Manager o derivarli dall&#39;URL dell&#39;autore: `https://author-p<ProgramID>-e<EnvironmentID>.adobeaemcloud.com/`. Immettere solo gli identificatori numerici, senza i prefissi `p` e `e`.

   Per i campi con una casella di controllo **[!UICONTROL Use system value]**, deselezionarla prima di sostituire il valore predefinito.

1. Seleziona **[!UICONTROL AEM Domain Mapping]**. I domini disponibili vengono caricati automaticamente in base all’ambiente AEM selezionato. Se il progetto utilizza un dominio di consegna risorse personalizzato, segui [Configurare l&#39;URL del dominio personalizzato](#optional-configure-the-custom-domain-url).

1. [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Seleziona [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) per autenticare le richieste tra Commerce e il servizio di corrispondenza risorse.

1. Impostare **[!UICONTROL Synchronization enabled]** su `Yes` per consentire a Commerce di accettare gli aggiornamenti in arrivo da AEM Assets.

   Dopo aver abilitato l’integrazione, sono disponibili opzioni di configurazione aggiuntive per specificare i criteri di corrispondenza delle risorse.

1. Selezionare una delle regole di corrispondenza risorse per la sincronizzazione risorse dal menu a discesa **[!UICONTROL Asset matching rule]**.

   * Selezionare **[!UICONTROL Match by product SKU]** per [corrispondenza automatica predefinita](../synchronize/default-match.md).
   * Selezionare **[!UICONTROL Custom match]** per [corrispondenza automatica personalizzata](../synchronize/custom-match.md). Questa opzione richiede [Adobe Developer App Builder](https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder).

1. Per **[!UICONTROL Match by product SKU]**, immettere il nome della proprietà dei metadati [AEM Assets](../metadata.md) nel campo **[!UICONTROL Match by product SKU attribute name]**. Il valore predefinito è `commerce:skus`.

   Inserisci il nome della proprietà, non un valore SKU del prodotto. Aggiungi gli SKU del prodotto effettivi ai metadati **[!UICONTROL Product Data]** di ciascuna risorsa in AEM Assets, come descritto in [Corrispondenza automatica predefinita](../synchronize/default-match.md).

1. Rivedi l&#39;impostazione [Proprietario visualizzazione](#configure-the-visualization-owner). Durante la migrazione, mantieni la proprietà di **Adobe Commerce** fino al completamento della sincronizzazione delle risorse.

1. Selezionare **[!UICONTROL Save Config]** per applicare gli aggiornamenti e avviare la sincronizzazione delle risorse.

   L’aggiornamento della configurazione attiva il processo di sincronizzazione iniziale, consentendo a Commerce di accettare gli aggiornamenti in arrivo da AEM Assets. Il tempo necessario per la sincronizzazione dipende dal volume delle risorse e da configurazioni specifiche. L’integrazione sfrutta i processi automatizzati per ridurre al minimo il tempo necessario per la sincronizzazione.

### Sincronizzazione SLA

Service level agreement (SLA) per l’integrazione garantisce i seguenti livelli di prestazioni di sincronizzazione:

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

Questo livello di servizio assicura che le pagine dei prodotti visualizzino sempre le immagini più aggiornate, mantenendo contenuti precisi e accattivanti dal punto di vista visivo.

## Sincronizza testo alternativo localizzato

Il testo alternativo localizzato utilizza il processo di sincronizzazione risorse esistente. Non è necessario un nuovo tipo di evento o una configurazione di sincronizzazione separata.

1. Aggiungi una o più righe di testo alternativo per la visualizzazione store nella scheda **[!UICONTROL Commerce]** della risorsa AEM.

1. Associa la risorsa allo SKU del prodotto Commerce.

1. Approva la risorsa in AEM Assets.

1. Attendi il completamento dell’evento risorsa e del processo di sincronizzazione.

1. Verifica il valore localizzato in Commerce Admin e nella risposta della vetrina.

Per i nomi dei campi, le regole di convalida e i risultati di Commerce, vedi [Metadati Commerce in AEM Assets](../metadata.md).

## Configurare il proprietario della visualizzazione

L&#39;impostazione **Proprietario visualizzazione** determina quale sistema fornisce le immagini del prodotto nell&#39;integrazione:

* Adobe Commerce: usa immagini in hosting in Commerce.

* AEM Assets: usa immagini sincronizzate da AEM.

L&#39;amministratore visualizza le immagini disponibili per il proprietario, mentre le altre immagini sono disattivate e visualizzate con l&#39;etichetta **hidden**.

Per informazioni sul comportamento di visualizzazione delle immagini, vedere l&#39;argomento [Imposta dettagli immagine](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank}.

>[!TIP]
>
> Durante una migrazione da Commerce ad AEM Assets, imposta **Proprietario visualizzazione** su Commerce per evitare collegamenti immagine interrotti. Dopo che tutti i prodotti sono stati sincronizzati con AEM Assets, passa al proprietario di AEM Assets per completare la transizione. Ciò garantisce la disponibilità continua delle immagini durante l&#39;intero processo.

1. Passa a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![Proprietario visualizzazione impostato su AEM Assets](../assets/visualization-owner-detail.png){width="700" zoomable="yes"}

1. Seleziona l&#39;origine **Proprietario visualizzazione** per visualizzare le immagini.

1. Fare clic su **[!UICONTROL Save Config]** per applicare gli aggiornamenti.

   Prima di passare a **AEM Assets**, [verifica che le risorse siano associate ai prodotti previsti](#verify-the-integration). Quindi [configura la vetrina](configure-storefront.md) per visualizzare le immagini dei prodotti AEM Assets.

## Facoltativo. Configurare l’URL del dominio personalizzato

Se il progetto AEM Assets as a Cloud Service è stato configurato con un [nome di dominio personalizzato](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}, è necessario aggiungere il nome di dominio alla configurazione dell&#39;archivio Commerce in modo che l&#39;integrazione AEM Assets per Commerce possa utilizzarlo.

Ottieni l’URL di dominio personalizzato configurato per la consegna delle risorse dall’amministratore AEM. Questa impostazione sostituisce l’URL di consegna di AEM; non è l’URL di authoring di AEM utilizzato per identificare l’ID del programma e l’ID dell’ambiente. Se il progetto non utilizza un dominio personalizzato, lascia invariato il mapping del dominio.

>[!NOTE]
>
>La configurazione di un URL di dominio personalizzato non aggiorna gli URL delle risorse sincronizzate in precedenza. Queste risorse mantengono gli URL precedenti fino a quando non vengono [rielaborate in AEM Assets](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/manage/reprocessing){target=_blank}. Dopo aver salvato la configurazione del dominio personalizzato, rielabora queste risorse per aggiornare i loro URL in modo da utilizzare il dominio personalizzato.

1. Passa a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Conferma **[!UICONTROL AEM Environment]** selezionato, quindi seleziona il dominio personalizzato configurato da **[!UICONTROL AEM Domain Mapping]**. I domini disponibili vengono caricati automaticamente per l’ambiente selezionato.

![Selettori di ambienti e domini AEM con valori di esempio](../assets/aem-assets-environment-domain.png){width="700" zoomable="yes"}

    Per le configurazioni che visualizzano un campo di testo **[!UICONTROL Asset Custom Domain]**, immettere l&#39;URL del dominio personalizzato nel campo.

1. Fare clic su **[!UICONTROL Save Config]** per applicare gli aggiornamenti.

## Verificare l’integrazione

>[!NOTE]
>
>Stato di sincronizzazione non disponibile per Adobe Commerce Optimizer. Segui il [flusso di lavoro di verifica di Commerce Optimizer](configure-aco.md#match-by-sku-workflow-example) invece dei controlli di amministrazione di Commerce riportati di seguito.

1. Scegli un prodotto Commerce esistente e annota il relativo SKU.

1. In AEM Assets, contrassegna una risorsa di prova come **[!UICONTROL Eligible for Commerce]**, associala allo SKU del prodotto e impostane il ruolo e la posizione. Approva la risorsa. Vedi [Corrispondenza automatica predefinita](../synchronize/default-match.md) oppure utilizza la [regola di corrispondenza personalizzata](../synchronize/custom-match.md) configurata.

1. Al termine della sincronizzazione, apri il prodotto in Commerce Admin e controlla la sezione **[!UICONTROL Images And Videos]** per la risorsa, il ruolo e la posizione associati. Vedi [Gestione risorse](../manage-assets.md).

1. Rivedi [Stato sincronizzazione](sync-status.md) per il risultato della sincronizzazione della risorsa. Se la sincronizzazione non riesce, esaminare la colonna **[!UICONTROL Error]**.

1. Dopo aver selezionato **AEM Assets** come proprietario della visualizzazione e aver completato la [configurazione della vetrina](configure-storefront.md), apri il prodotto nella vetrina e conferma che venga visualizzata l&#39;immagine prevista.

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Per ulteriori informazioni sulla risoluzione dei problemi di sincronizzazione, esaminare i [registri di integrazione](logs.md).

## Passaggio successivo

* [Configura Commerce Storefront](configure-storefront.md) per visualizzare le immagini dei prodotti AEM Assets con Edge Delivery Services.

* Imposta [regole corrispondenti](../synchronize/default-match.md) tra Adobe Commerce e l&#39;integrazione AEM Assets.

* [Gestione risorse Commerce](../manage-assets.md).
