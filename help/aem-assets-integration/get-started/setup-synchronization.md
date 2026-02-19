---
title: Configurare l’integrazione
description: Scopri come collegare il progetto Adobe Commerce e i progetti Experience Manager Assets per abilitare la sincronizzazione delle risorse tra questi due sistemi.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
source-git-commit: d59c9d179018318d7a0ab1685d8e9e172eefa3ed
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 0%

---

# Configurare l’integrazione

Configura l’integrazione connettendo Commerce all’istanza di AEM Assets e selezionando la strategia di corrispondenza per la sincronizzazione delle risorse.

Dopo aver identificato il progetto AEM Assets, seleziona la regola corrispondente per la sincronizzazione delle risorse tra Adobe Commerce e AEM Assets.

* **[!UICONTROL Match by product SKU]**—Regola predefinita che corrisponde allo SKU nei metadati della risorsa con [SKU prodotto Commerce](https://experienceleague.adobe.com/it/docs/commerce-operations/implementation-playbook/glossary#sku) per garantire che le risorse siano associate ai prodotti corretti.

* **[!UICONTROL Custom match]** - Regola di corrispondenza per scenari più complessi o requisiti aziendali specifici che richiedono una logica di corrispondenza personalizzata. L’implementazione della corrispondenza personalizzata richiede lo sviluppo di codice personalizzato in Adobe Developer App Builder per definire il modo in cui le risorse vengono associate ai prodotti. Ulteriori dettagli disponibili a breve...

Per la configurazione iniziale, utilizza la regola predefinita *Corrispondenza per SKU prodotto*.

## Requisiti

Prima di configurare l’integrazione di AEM Assets, verifica di aver completato i seguenti passaggi:

* [Configurare il progetto AEM Assets](configure-aem.md)

* [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} [Installa i pacchetti Adobe Commerce](configure-commerce.md) per aggiungere l&#39;estensione e generare le credenziali e le connessioni necessarie per utilizzare l&#39;estensione.

### Autorizzazioni IMS e utente

Per utilizzare il Selettore risorse e fornire una configurazione più fluida in Commerce, sono necessarie le seguenti autorizzazioni:

>[!BEGINTABS]

>[!TAB ACCS]

[!BADGE Solo SaaS]{type=Positive tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."}

L’autenticazione IMS è attivata per impostazione predefinita. Aggiungi l&#39;utente al profilo di prodotto **Utenti OpenAPI di AEM Assets DM - delivery** in [Adobe Admin Console](https://adminconsole.adobe.com/) per concedere l&#39;accesso al livello di consegna di AEM Assets.

![Profilo prodotto Admin Console per la consegna AEM Assets](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB PaaS]

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."}

1. [Abilitare Adobe IMS per Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=it){target=_blank} seguendo le istruzioni contenute nella *Guida per l&#39;amministratore di Commerce*.

1. [Apri un ticket di supporto](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) per richiedere un ID client IMS personalizzato per il selettore risorse.

1. Aggiungi l&#39;utente al profilo di prodotto **Utenti OpenAPI di AEM Assets DM - delivery** in [Adobe Admin Console](https://adminconsole.adobe.com/) per concedere l&#39;accesso al livello di consegna di AEM Assets.

>[!ENDTABS]

## Configurare la connessione

1. Dall’amministratore di Commerce, apri la configurazione dell’integrazione di AEM Assets.

   1. Vai a **[!UICONTROL Store]** > Configurazione > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

      ![L&#39;integrazione di AEM Assets abilita l&#39;integrazione](../assets/aem-assets-view.png){width="600" zoomable="yes"}

>[!INFO]
>
> L’integrazione di AEM Assets supporta solo la configurazione nell’ambito globale (predefinito). La configurazione a livello di sito web non è supportata. Quando tenti di configurare l’integrazione a livello di sito web, il sistema ignora le impostazioni a livello di sito web e utilizza invece i valori di configurazione globale.

1. [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Inserisci **[!UICONTROL Asset Selector IMS Client ID]**.

   Questo ID è necessario per abilitare il Selettore risorse e la funzione di compilazione automatica per i campi ID programma e ID ambiente. Per ottenere questo ID, consulta [IMS e autorizzazioni utente](#ims-and-user-permissions). Per informazioni dettagliate sul selettore risorse, vedere [Selezione manuale delle risorse](../synchronize/asset-selector-integration.md).

1. Selezionare l&#39;ambiente AEM Assets **[!UICONTROL Program ID]** e **[!UICONTROL Environment ID]** dai menu a discesa.

   I menu a discesa si compilano automaticamente in base alla sessione IMS dell’utente. Per utilizzare questa funzione, assicurati di disporre delle [autorizzazioni IMS e dell&#39;autorizzazione utente](#ims-and-user-permissions) corrette.

   Se i menu a discesa non sono disponibili, puoi immettere manualmente gli ID dall&#39;URL di AEM Cloud Manager: `https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`

   Modificare i valori di configurazione rimuovendo la selezione da *[!UICONTROL Use system value]*.

1. [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Seleziona [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) per autenticare le richieste tra Commerce e il servizio di corrispondenza risorse.

1. Impostare **[!UICONTROL Synchronization enabled]** su `Yes` per consentire a Commerce di accettare gli aggiornamenti in arrivo da AEM Assets.

   Dopo aver abilitato l’integrazione, sono disponibili opzioni di configurazione aggiuntive per specificare i criteri di corrispondenza delle risorse.

1. Selezionare una delle regole di corrispondenza risorse per la sincronizzazione risorse dal menu a discesa **[!UICONTROL Asset matching rule]**.

   * Seleziona **[!UICONTROL Match by SKU]** per [corrispondenza automatica predefinita](../synchronize/default-match.md),
   * Seleziona **[!UICONTROL Custom match]** per [corrispondenza automatica personalizzata](../synchronize/custom-match.md) (richiede [Adobe Developer App Builder](https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder).)

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

Per informazioni sul comportamento di visualizzazione delle immagini, vedere l&#39;argomento [Imposta dettagli immagine](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank}.

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

* **Configura Commerce Storefront**. Per utilizzare AEM Assets con Commerce Storefront con tecnologia Edge Delivery Services, completa la configurazione della vetrina descritta nell&#39;argomento [Integrazione AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=it) nella *documentazione Adobe Commerce Storefront*.

* Imposta [regole corrispondenti](../synchronize/default-match.md) tra Adobe Commerce e l&#39;integrazione AEM Assets.

* [Gestione risorse Commerce](../manage-assets.md).
