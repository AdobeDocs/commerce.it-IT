---
title: Test e convalida
description: I test e la convalida garantiscono che  [!DNL Payment Services]  funzioni funzionino come previsto e forniscono le migliori opzioni di pagamento per i clienti
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Test e convalida

Prima di esporre [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] agli acquirenti, è consigliabile eseguire il test nell&#39;ambiente sandbox _e_ in produzione. I test e la convalida garantiscono che le funzioni di [!DNL Payment Services] funzionino come previsto e forniscono le migliori opzioni di pagamento per il tuo negozio e i tuoi clienti.

## Test in ambiente sandbox

Il test di [!DNL Payment Services] in un ambiente sandbox è un passaggio importante di convalida, anche se si tratta di un ambiente simulato connesso solo alla sandbox PayPal, non a banche e commercianti reali.

1. Completa l&#39;estrazione dal tuo Negozio con [Campi carta di credito](payments-options.md#credit-card-fields) o con uno dei [pulsanti di pagamento PayPal](payments-options.md#paypal-smart-buttons). Per ulteriori informazioni sull&#39;utilizzo di carte di credito false per i test, vedere [Verifica delle credenziali](#testing-credentials).
1. Acquisisci (quando l&#39;azione di pagamento è [impostata su `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)), [rimborsi](refunds.md) o [annulli](voids.md) l&#39;ordine appena completato. Puoi anche semplicemente [creare una fattura](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"} per un ordine, se l&#39;azione di pagamento è impostata su `Authorize` invece di `Authorize and Capture`.
1. Entro 24-48 ore, visualizzare la transazione e altre informazioni nel [report Pagamenti](payouts.md).
1. Vedi i dettagli dell&#39;ordine nel [report sullo stato del pagamento dell&#39;ordine](order-payment-status.md).

### Verifica delle credenziali

Durante il test e la convalida della sandbox è necessario utilizzare numeri di carta di credito falsi, in modo da non creare spese effettive per un account di carta di credito esistente.

Utilizza il generatore di carte di credito di PayPal per [generare informazioni casuali sulla carta di credito](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157) per il test.

Per testare Apple Pay in modalità sandbox:

* Crea un account [Apple sandbox tester](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account), completo di informazioni false sulla carta di credito e sulla fatturazione.
* [Registra i domini sandbox](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains).

>[!NOTE]
>
>A volte l&#39;elaborazione dei pagamenti sandbox di PayPal è lenta e il servizio può occasionalmente andare in tilt. Questa situazione non è un&#39;indicazione della velocità e dell&#39;efficienza del processo di pagamento dei prodotti vivi.

## Test in produzione

Si consiglia vivamente di testare [!DNL Payment Services] in produzione, con carte di credito e banche reali, prima di esporre questa funzionalità agli acquirenti. Anche se il test di [!DNL Payment Services] in sandbox è importante, il test in produzione è il metodo più stupido per garantire che [!DNL Payment Services] funzioni come previsto.

È possibile eseguire il test di [!DNL Payment Services] in produzione in uno dei due modi seguenti:

* Scegli un momento in cui sai che nessun ordine verrà effettuato dagli acquirenti.
* Utilizza un archivio Web temporaneamente inaccessibile agli acquirenti, ma che è accessibile per i test.

Completa i test di produzione con carte di credito reali e account PayPal, testando l&#39;intero ciclo di vita di un pagamento, inclusa l&#39;acquisizione e il rimborso. Il completamento dell&#39;intero flusso di pagamento e di pagamento durante il test offre un&#39;immagine chiara del funzionamento della funzionalità [!DNL Payment Services] quando gli acquirenti in tempo reale la utilizzano.

È inoltre necessario verificare che le informazioni visualizzate nei rendiconti bancari per i metodi di pagamento utilizzati nei test di produzione siano corrette e previste (inclusa la descrizione della propria attività).

Per testare Apple Pay in modalità di produzione, devi [registrare i domini di produzione](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).
