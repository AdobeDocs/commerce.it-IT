---
title: Configurare l’integrazione
description: Scopri come collegare il progetto Adobe Commerce e i progetti Experience Manager Assets per abilitare la sincronizzazione delle risorse tra questi due sistemi.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
source-git-commit: 86e8876af21da3df0ec5e940113f19593b2f6d0a
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Configurare l’integrazione

Configura l’integrazione connettendo Commerce all’istanza di AEM Assets e selezionando la strategia di corrispondenza per la sincronizzazione delle risorse.

Dopo aver identificato il progetto AEM Assets, seleziona la regola corrispondente per la sincronizzazione delle risorse tra Adobe Commerce e AEM Assets.

* **[!UICONTROL Match by product SKU]**—Regola predefinita che corrisponde allo SKU nei metadati della risorsa con [SKU prodotto Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#sku) per garantire che le risorse siano associate ai prodotti corretti.

* **[!UICONTROL Custom match]** - Regola di corrispondenza per scenari più complessi o requisiti aziendali specifici che richiedono una logica di corrispondenza personalizzata. L’implementazione della corrispondenza personalizzata richiede lo sviluppo di codice personalizzato in Adobe Developer App Builder per definire il modo in cui le risorse vengono associate ai prodotti. Ulteriori dettagli disponibili a breve...

Per la configurazione iniziale, utilizza la regola predefinita *Corrispondenza per SKU prodotto*.

## Prerequisiti

* [Configurare il progetto AEM Assets](configure-aem.md)

* [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} [Installa i pacchetti Adobe Commerce](configure-commerce.md) per aggiungere l&#39;estensione e generare le credenziali e le connessioni necessarie per utilizzare l&#39;estensione.

* Segui i passaggi descritti nell&#39;argomento [abilita Dynamic Media Open API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis). Includi le seguenti informazioni per il team di supporto:

   * **[!UICONTROL AEM Program ID]**
   * **[!UICONTROL Adobe Commerce URL]**
   * **[!UICONTROL AEM Environment ID]**,
   * **[!UICONTROL IMS Org ID]** per l&#39;ambiente di authoring AEM Assets che si desidera connettere a Commerce.

## Configurare la connessione

1. Ottieni l&#39;ID del progetto e dell&#39;ambiente [AEM Assets Authoring Environment](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/quick-start).

   1. Apri AEM Cloud Manager e seleziona **[!UICONTROL Assets]**.

   1. Copia e salva gli ID di progetto e ambiente dall&#39;URL:<br>`https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`

1. Dall’amministratore di Commerce, apri la configurazione dell’integrazione di AEM Assets.

   1. Vai a **[!UICONTROL Store]** > Configurazione > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

      ![L&#39;integrazione di AEM Assets abilita l&#39;integrazione](../assets/aem-assets-view.png){width="600" zoomable="yes"}

1. Immettere l&#39;ambiente AEM Assets **[!UICONTROL Program ID]** e **[!UICONTROL Environment ID]**.

   Modificare i valori di configurazione rimuovendo la selezione da *[!UICONTROL Use system value]*.

1. Immettere **[!UICONTROL Asset Selector IMS Client ID]**.

   Per informazioni dettagliate sul selettore risorse, vedi [Selezione manuale delle risorse](../synchronize/asset-selector-integration.md)

1. [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Seleziona [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) per autenticare le richieste tra Commerce e il servizio di corrispondenza risorse.

1. Imposta **[!UICONTROL Commerce integration]** su `assets-integration` per selezionare l&#39;integrazione di Commerce da utilizzare con AEM Assets.

1. Impostare **[!UICONTROL Synchronization enabled]** su `Yes` per consentire a Commerce di accettare gli aggiornamenti in arrivo da AEM Assets.

   Dopo aver abilitato l’integrazione, sono disponibili opzioni di configurazione aggiuntive per specificare i criteri di corrispondenza delle risorse.

1. Selezionare una delle regole di corrispondenza risorse per la sincronizzazione risorse dal menu a discesa **[!UICONTROL Asset matching rule]**.

   * Seleziona **[!UICONTROL Match by SKU]** per [corrispondenza automatica predefinita](../synchronize/default-match.md),
   * Seleziona **[!UICONTROL Custom match]** per [corrispondenza automatica personalizzata](../synchronize/custom-match.md) (richiede [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder).)

1. Aggiungi il nome del campo di metadati [AEM Assets](configure-aem.md#configure-metadata) definito per gli SKU dei prodotti Commerce nel campo **[!UICONTROL Match by product SKU attribute name]**, `commerce:skus` per impostazione predefinita.

1. Selezionare **[!UICONTROL Save Config]** per applicare gli aggiornamenti e avviare la sincronizzazione delle risorse.

   L’aggiornamento della configurazione attiva il processo di sincronizzazione iniziale, consentendo a Commerce di accettare gli aggiornamenti in arrivo da AEM Assets. Il tempo necessario per la sincronizzazione dipende dal volume delle risorse e da configurazioni specifiche. L’integrazione sfrutta i processi automatizzati per ridurre al minimo il tempo necessario per la sincronizzazione.

### Sincronizzazione SLA

L’integrazione garantisce i seguenti livelli di prestazioni di sincronizzazione:

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

In questo modo le pagine dei prodotti visualizzano sempre le immagini più aggiornate, mantenendo accurati e accattivanti i contenuti della vetrina.

### Configurare il proprietario della visualizzazione

L&#39;impostazione **Proprietario visualizzazione** determina quale sistema fornisce le immagini del prodotto nell&#39;integrazione:

* Adobe Commerce: usa immagini in hosting in Commerce.
* AEM Assets: usa immagini sincronizzate da AEM.

L&#39;amministratore visualizza le immagini disponibili per il proprietario, mentre le altre immagini sono disattivate e visualizzate con l&#39;etichetta **hidden**.

Per informazioni sul comportamento di visualizzazione delle immagini, vedere l&#39;argomento [Imposta dettagli immagine](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank}.

>[!TIP]
>
> Durante una migrazione da Commerce ad AEM Assets, imposta **Proprietario visualizzazione** su Commerce per evitare collegamenti immagine interrotti. Dopo che tutti i prodotti sono stati sincronizzati con AEM Assets, passa al proprietario di AEM Assets per completare la transizione. Ciò garantisce la disponibilità continua delle immagini durante l&#39;intero processo.

1. Passa a **[!UICONTROL Store]** > Configurazione > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![Funzionalità proprietario visualizzazione integrazione AEM Assets](../assets/visualization-owner-detail.png){width="400" zoomable="yes"}

1. Seleziona l&#39;origine **Proprietario visualizzazione** per visualizzare le immagini.

1. Fare clic su **[!UICONTROL Save Config]** per applicare gli aggiornamenti e avviare la sincronizzazione delle risorse.

### Facoltativo. Configurare l’URL del dominio personalizzato

Se il progetto AEM Assets as a Cloud Service è stato configurato con un [nome di dominio personalizzato](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}, è necessario aggiungere il nome di dominio alla configurazione dell&#39;archivio Commerce in modo che l&#39;integrazione AEM Assets per Commerce possa utilizzarlo.

1. Passa a **[!UICONTROL Store]** > Configurazione > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![L&#39;integrazione di AEM Assets abilita l&#39;integrazione](../assets/aem-assets-view.png){width="700" zoomable="yes"}

1. Aggiungi l&#39;**URL dominio personalizzato** al campo **[!UICONTROL Asset Custom Domain]**.

1. Fare clic su **[!UICONTROL Save Config]** per applicare gli aggiornamenti e avviare la sincronizzazione delle risorse.

## Passaggio successivo

[Gestire le risorse Commerce](../manage-assets.md)
