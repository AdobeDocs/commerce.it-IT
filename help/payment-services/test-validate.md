---
title: Test e convalida
description: I test e la convalida garantiscono che  [!DNL Payment Services]  funzioni funzionino come previsto e forniscono le migliori opzioni di pagamento per i clienti
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: 91a4b8fa7228fb91c8ee0bf0a1623d104f061894
workflow-type: tm+mt
source-wordcount: '0'
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

### Test sugli ambienti di sviluppo locali

Il test dei metodi di pagamento PayPal, PayLater e Venmo negli ambienti di sviluppo locali richiede che l&#39;ambiente sia accessibile da Internet. Questi metodi di pagamento utilizzano un [callback di spedizione lato server](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/) che richiede a PayPal di comunicare con l&#39;istanza di Commerce per recuperare le opzioni di spedizione e calcolare i totali.

>[!INFO]
>
>Senza un URL accessibile a Internet, il callback di spedizione non può funzionare, il che si traduce in un flusso di pagamento diverso rispetto alla produzione. Esegui sempre il test con un URL accessibile per garantire risultati accurati.

Per esporre l’ambiente locale:

1. Utilizza un servizio di tunneling come [ngrok](https://ngrok.com/) per creare un URL accessibile al pubblico per l&#39;ambiente locale.

1. Aggiorna la configurazione dell’URL di base di Commerce in modo che corrisponda all’URL non elaborato:

   ```bash
   bin/magento config:set web/unsecure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento config:set web/secure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento cache:flush
   ```

1. Completa i test con i metodi di pagamento PayPal, PayLater o Venmo.

1. Ripristina la configurazione dell’URL di base originale al termine del test.

Se il tempo di risposta dell&#39;endpoint è inferiore a 5 secondi, PayPal visualizza un messaggio di errore nel pop-up.

#### Sviluppo locale Apple Pay

Apple Pay richiede una configurazione aggiuntiva per lo sviluppo locale. Apple Pay utilizza la registrazione del dominio per verificare che il tuo sito sia autorizzato ad accettare pagamenti Apple Pay. Apple deve quindi essere in grado di raggiungere il dominio per convalidare un file di verifica del dominio in `/.well-known/apple-developer-merchantid-domain-association`.

Per lo sviluppo locale, l’ambiente deve soddisfare i seguenti requisiti:

* **Accessibile al pubblico**, Apple deve essere in grado di raggiungere il dominio da Internet.
* **Protocollo HTTPS**, Apple Pay funziona solo su connessioni sicure.

L&#39;utilizzo di un servizio di tunneling come [ngrok](https://ngrok.com/) soddisfa entrambi i requisiti. Dopo aver configurato ngrok come descritto in precedenza, [registra il dominio sandbox](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains) con PayPal utilizzando l&#39;URL **ngrok**.

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

### Test di Apple Pay in produzione

Per testare Apple Pay in modalità di produzione, devi [registrare i domini di produzione](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).
