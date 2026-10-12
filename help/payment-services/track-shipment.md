---
title: Tracciamento delle spedizioni in [!DNL Payment Services]
description: Personalizza [!DNL Payment Services] spedizioni e informazioni di registrazione visualizzate nel dashboard di Paypal Merchant.
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%
---
# Tracciamento delle spedizioni in [!DNL Payment Services]

[!DNL Payment Services] consente ai commercianti di visualizzare le informazioni di tracciamento per una spedizione nel dashboard PayPal del commerciante.

Per ulteriori informazioni sulla griglia delle spedizioni per Adobe Commerce, vedere l&#39;argomento [spedizioni](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank}.

## Come funziona la spedizione

Questa funzionalità dipende dal fatto che l&#39;ordine sia stato fatturato, poiché PayPal deve ricevere `capture_id` per elaborare le informazioni di tracciamento. Se un commerciante spedisce i suoi prodotti prima di catturarli, le informazioni di tracciamento non vengono inviate a PayPal.

>[!NOTE]
>
> Si consiglia di creare una spedizione per numero di registrazione, associando gli articoli corretti alla spedizione.

## Aggiunta del numero di tracciamento

Le seguenti istruzioni ti guideranno nel processo di creazione di una spedizione in Adobe Commerce con [!DNL Payment Services]:

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.

1. Nella colonna **[!UICONTROL Action]** dell&#39;ordine selezionato, fare clic su **[!UICONTROL View]**.

1. Fare clic su **[!UICONTROL Ship]**.

1. Scorri verso il basso fino al blocco **[!UICONTROL Payment & Shipping Method]** e fai clic su **[!UICONTROL Add Tracking Number]** in **[!UICONTROL Shipping Information]**.

1. Imposta **[!UICONTROL Carrier]**.

1. Per tenere traccia della spedizione, immettere **[!UICONTROL Title]** e **[!UICONTROL Number]**.

1. Fare clic su **[!UICONTROL Submit Shipment]**.

>[!NOTE]
>
> In alternativa, è possibile utilizzare un modulo di spedizione per inserire le informazioni relative al numero di registrazione. Verificare che il modulo di spedizione stia salvando le informazioni sul numero di registrazione nel campo `tracking_number`.

### Compatibilità con terzi

Qualsiasi estensione di terze parti è compatibile con la funzionalità quando viene creata un&#39;entità di spedizione tramite [API Commerce](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}.
