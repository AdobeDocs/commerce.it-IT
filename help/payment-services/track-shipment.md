---
title: Tracciamento delle spedizioni in [!DNL Payment Services]
description: Personalizza [!DNL Payment Services] le spedizioni e le informazioni di registrazione visualizzate nel dashboard di Paypal Merchant.
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '211'
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
