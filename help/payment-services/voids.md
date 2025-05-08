---
title: Vuoti
description: I vuoti consentono di liberare i fondi in un conto della carta di credito o di debito che sono bloccati o detenuti da un'autorizzazione per l'importo di un acquisto.
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Vuoti

[!DNL Payment Services] supporta la funzionalità esistente di Commerce per la cancellazione delle transazioni. Un void rilascia fondi in un conto della carta di credito o di debito che sono detenuti da un&#39;autorizzazione per l&#39;importo dell&#39;acquisto. Le transazioni possono essere annullate solo se il pagamento non è stato ancora acquisito.

* Se il tuo Negozio è [configurato](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} per autorizzare solo (non acquisire) i fondi presso il punto vendita, un acquisto dal tuo Negozio determina un ordine con stato `Processing` nell&#39;Amministratore di Commerce.

* È inoltre possibile [annullare un ordine](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} non fatturato. Anche eventuali autorizzazioni non acquisite vengono annullate nell’ambito di tale processo di annullamento.

>[!NOTE]
>
>L’annullamento di un ordine genera anche un annullamento, ma l’annullamento di un ordine non attiva l’annullamento.

Per ulteriori informazioni sui passaggi di base di un ordine, consulta l&#39;argomento [Flusso di lavoro dell&#39;ordine](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} nella guida utente di base.

Per informazioni sulla funzionalità di annullamento e su come annullare una transazione dell&#39;ordine, vedere [Elaborazione di un ordine](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} nella guida utente di base.
