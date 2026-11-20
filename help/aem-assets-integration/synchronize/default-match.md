---
title: Corrispondenza automatica predefinita
description: Scopri in che modo la regola di corrispondenza automatica predefinita consente una sincronizzazione perfetta tra Adobe Commerce e l’integrazione AEM Assets, garantendo che le risorse siano collegate automaticamente alle entità di merchandising corrette.
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
TQID: 'https://experienceleague.adobe.com/z7vpuhsVJnKohiU-bKNrcGnoIQ5WAwcwiccYlvawN0U'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 5e9c42e5c93ac81604aa38bf3e55c5df729650a0
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%
---
# Corrispondenza automatica predefinita

L&#39;integrazione AEM Assets per Commerce fornisce un meccanismo di corrispondenza automatica predefinito (**[!UICONTROL Match by product SKU]**) basato sulla configurazione dei metadati **AEM Assets**. Questa regola abilita la sincronizzazione perfetta tra **Adobe Commerce** e **AEM Assets**, garantendo che le risorse siano collegate automaticamente alle entità di merchandising corrette.

## Configurare il meccanismo di corrispondenza automatica

1. Dall&#39;amministratore di Commerce, passare a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Specificare **[!UICONTROL Match by product SKU]** come regola corrispondente.

   ![Corrispondenza per regola SKU prodotto e nome proprietà metadati](../assets/ootb-matching-rule.png){width="700" zoomable="yes"}

1. In **[!UICONTROL Match by product SKU attribute name]**, immetti il nome [della proprietà metadati](../metadata.md) che memorizza gli SKU dei prodotti in AEM Assets, non un valore SKU effettivo.

   >[!NOTE]
   >
   > Se è stato seguito il processo di onboarding standard, questo valore deve essere impostato su `commerce:skus`.

## Funzionamento del meccanismo di abbinamento automatico

Quando la regola di corrispondenza **[!UICONTROL Match by product SKU]** è configurata in Commerce Admin, i file di risorse Commerce vengono sincronizzati automaticamente da AEM Assets al progetto Commerce in base ai metadati delle risorse configurati per ciascun file. Puoi configurare i metadati dalla scheda AEM **Commerce** nell&#39;ambiente **AEM Assets author**:

1. Apri l’istanza di authoring di AEM Assets (l’URL viene fornito per il progetto nella stessa organizzazione IMS di Adobe Commerce).

1. Dalla schermata di navigazione principale, fai clic su **Assets** per accedere all&#39;interfaccia di Digital Asset Management (DAM).

1. In AEM Assets, aggiornare i metadati dell&#39;immagine per aggiungere l&#39;associazione Adobe Commerce impostando il campo `Eligible for Commerce` su `Yes`.

   ![Esempio di metadati](../assets/metadata-commerce-yes.png){width="600" zoomable="yes"}

1. Configurare i metadati ([!UICONTROL SKU], [!UICONTROL position] e [!UICONTROL role]) che collegano la risorsa allo SKU del prodotto associato.

   I quattro ruoli standard sono `image`, `small_image`, `thumbnail` e `swatch_image`. Con l&#39;estensione AEM Assets Integration versione 1.4.6 e successive, è inoltre possibile immettere un ruolo immagine personalizzato, ad esempio `hero` o `custom_role_1`. Vedi [Corrispondenza automatica personalizzata](custom-match.md) per i dettagli.

   >[!NOTE]
   >
   > Se una risorsa viene utilizzata per più prodotti, configura i metadati per ogni SKU associata.

1. Nella scheda `Basic`, impostare il valore predefinito per il campo _[!UICONTROL Review Status]_&#x200B;su `approved`.

   ![Esempio di metadati](../assets/metadata-review-status.png){width="600" zoomable="yes"}

Dopo aver approvato la risorsa, [verifica l&#39;associazione del prodotto, il risultato della sincronizzazione e la visualizzazione della vetrina](../get-started/setup-synchronization.md#verify-the-integration). Se la risorsa non viene visualizzata, controlla [Stato sincronizzazione](../get-started/sync-status.md). Per Adobe Commerce Optimizer, utilizzare invece il flusso di lavoro di verifica dell&#39;optimizer [&#128279;](../get-started/configure-aco.md#match-by-sku-workflow-example). Stato sincronizzazione non disponibile.

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Per ulteriori informazioni sulla risoluzione dei problemi di sincronizzazione, esaminare i [registri di integrazione](../get-started/logs.md).
