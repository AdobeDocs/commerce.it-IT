---
title: Vuoti
description: I vuoti consentono di liberare i fondi in un conto della carta di credito o di debito che sono bloccati o detenuti da un'autorizzazione per l'importo di un acquisto.
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Vuoti

Con [!DNL Payment Services] è possibile utilizzare le funzionalità esistenti di Commerce per annullare le transazioni. I vuoti consentono di liberare i fondi in un conto della carta di credito o di debito che sono bloccati o detenuti da un&#39;autorizzazione per l&#39;importo di un acquisto.

>[!NOTE]
>
>Puoi annullare una transazione solo se il pagamento non è ancora stato acquisito.

Se il tuo negozio è [configurato](https://experienceleague.adobe.com/it/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} per autorizzare solo i fondi (non acquisirli) presso il punto vendita, un acquisto dal tuo negozio determina un ordine con stato `Processing` nell&#39;amministratore di Commerce.

È inoltre possibile [annullare un ordine](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} non fatturato. Anche eventuali autorizzazioni non acquisite vengono annullate nell’ambito di tale processo di annullamento.

>[!NOTE]
>
>L’annullamento di un ordine genera anche un annullamento, ma l’annullamento di un ordine non attiva l’annullamento.

Per ulteriori informazioni sui passaggi di base di un ordine, consulta l&#39;argomento [Flusso di lavoro dell&#39;ordine](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} nella guida utente di base.

Per informazioni sulla funzionalità di annullamento e su come annullare una transazione ordine, vedere [Elaborazione di un ordine](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} nella guida utente di base.
