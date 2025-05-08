---
title: Rimborsi
description: Crea rimborsi per  [!DNL Payment Services]  ordini nell'amministratore come parte del processo della nota di credito.
exl-id: 2b3721a1-9c9d-4e3f-ab7d-5bd61573dcb4
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Rimborsi

I rimborsi per [!DNL Payment Services] ordini vengono creati nell&#39;amministratore come parte del processo della nota di credito. Una nota di credito è un documento che mostra l&#39;importo dovuto al cliente, per un rimborso completo o parziale, che può essere applicato a un acquisto o rimborsato direttamente al cliente. Le note di accredito possono essere emesse solo per gli ordini [fatturati](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}.

Consulta [Note di credito](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"} nella nostra guida utente di base per ulteriori informazioni e per scoprire come emettere e stampare note di credito.

Per gli ordini elaborati con PayPal o con una carta di credito puoi:

* Rimborsare l&#39;intero importo dell&#39;ordine
* Rimborsare un importo parziale di un ordine (o più importi parziali)
* Rimborso di un importo inferiore al valore di un articolo dell&#39;ordine specifico

Per ulteriori informazioni, consulta [Emissione di una nota di credito](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"} nella guida utente di base.

>[!NOTE]
>
>Si verifica un errore per gli ordini PayPal o elaborati con carta di credito se si tenta di rimborsare parzialmente un ordine per un importo superiore all&#39;importo restante (importo originale meno il totale dei rimborsi esistenti) o se si emette un rimborso per un importo superiore all&#39;intero importo dell&#39;ordine.

L&#39;impostazione [!UICONTROL Payment Action] nella configurazione [!UICONTROL Payment Settings], `Authorize` o `Authorize and Capture`, determina il [flusso di lavoro di rimborso di base](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"} per gli ordini.

Per ulteriori informazioni, vedere la sezione [Impostazione delle azioni di pagamento](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"} di _Emissione di una nota di credito_.
