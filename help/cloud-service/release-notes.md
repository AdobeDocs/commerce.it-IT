---
title: Note sulla versione di [!DNL Adobe Commerce as a Cloud Service]
description: Scopri le funzionalità e i miglioramenti più recenti in [!DNL Adobe Commerce as a Cloud Service].
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
TQID: https://experienceleague.adobe.com/MmwdYWe5Et9m0BvtrVYNK2jiJ3fZBnUe2K6xMdIbMUk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 3633
ht-degree: 0%

---

# Note sulla versione

Le seguenti note sulla versione contengono aggiornamenti a [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Se utilizzi Adobe Commerce on-premise o Adobe Commerce sull&#39;infrastruttura cloud, consulta le [note sulla versione di Adobe Commerce](https://experienceleague.adobe.com/it/docs/commerce-operations/release/notes/overview).

## Maggio 2026 - #1 sulla versione {#latest}

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

I seguenti elementi sono stati rilasciati negli ambienti di produzione il 7 maggio 2026.

>[!BEGINSHADEBOX]

### Ignora reCAPTCHA per l’autenticazione OTP programmatica

Una nuova opzione di configurazione consente di ignorare la convalida reCAPTCHA per la mutazione GraphQL [`exchangeOtpForCustomerToken`](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/). Questo abilita i flussi di lavoro di punchout B2B in cui lo scambio di password monouso (OTP) viene avviato a livello di programmazione senza una voce di modulo, rendendo superflua la convalida reCAPTCHA. Questa funzionalità si basa sulla funzionalità [accesso al codice una tantum](https://experienceleague.adobe.com/it/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer){target="_blank"} introdotta nella versione di marzo 2026. La mutazione `exchangeOtpForCustomerToken` continua a richiedere reCAPTCHA per impostazione predefinita quando reCAPTCHA è abilitato per l&#39;accesso del cliente. Contatta il tuo Customer Success Manager Adobe Commerce per abilitare questa opzione. <!-- ACCS-850 -->

### Modifica ordini parzialmente fatturati

Il pulsante [!UICONTROL **Modifica**] è ora disponibile nella schermata [!UICONTROL **Visualizzazione ordine**] per gli ordini parzialmente fatturati, offrendo agli esercenti maggiore flessibilità per modificare gli ordini ancora in corso. In precedenza, non era possibile modificare gli ordini con fatture, anche quando rimanevano articoli non fatturati. L&#39;ordine può essere modificato se è ancora possibile fatturare qualsiasi articolo nell&#39;ordine. I commercianti con integrazioni personalizzate basate sulla precedente restrizione di modifica devono rivedere i propri flussi di lavoro. <!-- ACCS-849 -->

### Miglioramenti e correzioni di bug

In questa versione sono inclusi i miglioramenti, le ottimizzazioni e le correzioni di bug seguenti:

* È stato risolto un problema che impediva la restituzione dell&#39;attributo di estensione `stock_item` sull&#39;endpoint dell&#39;elenco REST API `GET /V1/products`. La risposta ora corrisponde al contratto API documentato. <!-- ACCS-819 -->

* È stato risolto un problema a causa del quale i collegamenti per la reimpostazione della password nelle e-mail restituivano un errore 404. <!-- ACCS-797 -->

* Sono state migliorate le prestazioni delle query sulla cronologia degli ordini per le aziende che utilizzano filtri per intervalli di date. <!-- ACCS-859 -->

* È stato risolto un problema a causa del quale gli utenti della società B2B potevano visualizzare gli ordini dei colleghi prima che un utente entrasse a far parte della società. <!-- ACCS-859 -->

* Sono stati risolti i problemi di timeout dell&#39;estrazione che potevano influire sulle prestazioni dell&#39;API REST durante il caricamento delle virgolette con `trigger_recollect` abilitato. <!-- CCSAAS-4904 -->

* Sono stati risolti dei problemi di caricamento delle pagine che potevano verificarsi dopo l&#39;invio di un ordine in [!DNL Commerce Admin]. <!-- CCSAAS-4413 -->

* È stato risolto un problema a causa del quale gli ordini con la stessa marca temporale potevano visualizzare informazioni obsolete sullo stato degli ordini nella griglia degli ordini di vendita. <!-- CCSAAS-4890 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Aprile 2026 - #3 sulla versione

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

I seguenti elementi sono stati rilasciati negli ambienti di produzione il 27 aprile 2026.

>[!BEGINSHADEBOX]

### Miglioramenti e correzioni di bug

In questa versione sono inclusi i miglioramenti, le ottimizzazioni e le correzioni di bug seguenti:

* È stato aggiunto l&#39;endpoint REST API `GET /V1/order-statuses` per recuperare tutti gli stati dell&#39;ordine configurati con le relative assegnazioni di stato. <!-- CEXT-6100 -->

* È stato risolto un problema che impediva la visualizzazione di `custom_attributes` nello schema REST per entità quali Ordine, Carrello, Fattura, Nota di credito e Società. <!-- CCSAAS-4818 -->

* Risoluzione degli errori di elaborazione dei messaggi duplicati (`MessageLockException`) nel consumer API bulk asincrono. <!-- CCSAAS-4805 -->

* Numero di attributi di prodotto ora eseguono il rendering come da/a filtri intervallo nella griglia di prodotto [!DNL Commerce Admin] quando l&#39;attributo è abilitato per le opzioni di filtro. <!-- ACCS-761 -->

* È stato risolto un problema che impediva la visualizzazione delle immagini del prodotto nelle e-mail di promemoria per l&#39;abbandono del carrello quando si utilizzava [!DNL AEM Assets]. <!-- ACCS-798 -->

* È stato risolto un problema che causava la visualizzazione di un falso errore di &quot;dimensione massima caricamento&quot; durante l’aggiunta di file, esempi o collegamenti a prodotti scaricabili. <!-- ACCS-813 -->

* È stato risolto un problema che poteva causare un errore durante il salvataggio di un prodotto assegnato a più cataloghi condivisi. <!-- ACCS-788 -->

* È stato risolto un problema a causa del quale la query della cronologia degli ordini poteva essere lenta e causare errori di memoria esaurita nel database per le aziende con molti ordini. <!-- ACCS-808 -->

* È stato risolto un problema che poteva impedire la convalida del file di importazione. <!-- CCSAAS-4364 -->

* La configurazione **[!UICONTROL Recently Viewed/Compared Products]** è stata rimossa dalla sezione **[!UICONTROL Catalog]** in **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**, poiché non è supportata nell&#39;amministratore [!DNL Adobe Commerce as a Cloud Service]. <!-- ACCS-793 -->

>[!ENDSHADEBOX]

## Aprile 2026 - #2 sulla versione

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

I seguenti elementi sono stati rilasciati negli ambienti di produzione il 16 aprile 2026.

>[!BEGINSHADEBOX]

### Implementare i totali delle virgolette personalizzate con i webhook

Il `plugin.magento.out_of_process_totals_collector.api.get_total_modifications.execute` [webhook](https://developer.adobe.com/commerce/extensibility/webhooks/) è ora disponibile in [!DNL Adobe Commerce as a Cloud Service]. Utilizzala per implementare modifiche ai totali delle offerte personalizzate tramite l’estensibilità fuori processo. <!-- CEXT-5896 -->

### Regole promemoria e-mail riutilizzabili (sperimentali)

>[!IMPORTANT]
>
>Questa funzione è sperimentale e deve essere abilitata contattando il Customer Success Manager di Adobe Commerce o creando un ticket di supporto.

[Le regole di promemoria e-mail](https://experienceleague.adobe.com/it/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules#rule-repeatability) ora supportano un&#39;impostazione facoltativa di riutilizzabilità delle regole che consente di applicare nuovamente la stessa regola a un cliente dopo la cessazione della condizione di attivazione originale.

Ad esempio, se un cliente abbandona un carrello, completa l’acquisto e successivamente abbandona un nuovo carrello, la regola può essere nuovamente attivata. Senza questa impostazione, un cliente che cancella il trigger originale viene escluso in modo permanente dalle corrispondenze future della stessa regola.

### Visualizzare il report Transazioni di servizi di pagamento

Se hai abilitato [[!DNL Payment Services]](https://experienceleague.adobe.com/it/docs/commerce/payment-services/get-started/production), la [Interfaccia utente dashboard](../payment-services/payments-home.md) è ora disponibile in [!DNL Commerce Admin], fornendo l&#39;accesso al report [Transazioni](../payment-services/reporting.md#transactions-report-view) per la visualizzazione e la gestione delle transazioni di pagamento. <!-- PAY-6510 -->

### Miglioramenti e correzioni di bug

In questa versione sono inclusi i miglioramenti, le ottimizzazioni e le correzioni di bug seguenti:

* È stato corretto un errore 500 nella pagina Società di assegnazione catalogo condiviso che poteva verificarsi quando si utilizzavano cataloghi condivisi di grandi dimensioni con il SDK dell&#39;interfaccia utente amministratore. <!-- CCSAAS-4783 -->

* È stato risolto un problema che impediva ai clienti della società di visualizzare i propri ordini se questi erano stati effettuati prima che il cliente fosse assegnato alla società. <!-- ACCS-746 -->

>[!ENDSHADEBOX]

## Aprile 2026

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

I seguenti elementi sono stati rilasciati negli ambienti di produzione il 1° aprile 2026.

>[!BEGINSHADEBOX]

### Aggiungere file ai prodotti

[!DNL Adobe Commerce as a Cloud Service] ora supporta [l&#39;aggiunta di file ai prodotti](./product-files.md) utilizzando attributi di prodotto di tipo file. È possibile caricare i file manualmente nella pagina di modifica del prodotto, a livello di programmazione tramite l&#39;API REST o in blocco fornendo URL esterni in CSV. <!-- ACCS-535, ACCS-565 -->

### Verifica lo stato di sottoscrizione dell&#39;avviso di prezzo e azioni tramite GraphQL

Le nuove query GraphQL, [`isSubscribedProductAlertStock`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-stock/){target="_blank"} e [`isSubscribedProductAlertPrice`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-price/){target="_blank"}, consentono alle vetrine di determinare se un acquirente è già abbonato agli avvisi sulle azioni o sui prezzi per un prodotto. <!-- ACCS-334 -->

### Creare attributi di prodotto numerici che supportano valori negativi

Un nuovo tipo di input dell&#39;attributo di prodotto `numeric` [&#128279;](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/attributes-input-types) consente ai commercianti di creare attributi decimali che supportano valori negativi. <!-- ACCS-600 -->

### Eseguire una query sulla configurazione reCAPTCHA per più moduli in una richiesta GraphQL

La query [`recaptchaFormConfigs`](https://developer.adobe.com/commerce/webapi/graphql/schema/store/queries/recaptcha-form-configs/) può restituire dettagli di configurazione per più tipi di modulo in una singola richiesta. <!-- ACCS-628 -->

### Visualizza tutti gli ordini aziendali con una nuova autorizzazione B2B

Un nuovo `view_all_company_orders` [ruolo aziendale](https://developer.adobe.com/commerce/webapi/rest/b2b/roles/) consente ai clienti della società B2B di visualizzare tutti gli ordini all&#39;interno della società, inclusi gli ordini storici creati dagli utenti amministratori. <!-- ACCS-675 -->

### Miglioramenti e correzioni di bug

In questa versione sono inclusi i miglioramenti, le ottimizzazioni e le correzioni di bug seguenti:

* Ora puoi filtrare i risultati dell’API REST per ordini e società utilizzando gli attributi personalizzati applicabili, supportando scenari come le ricerche di ordini nell’ambito della società. <!-- ACCS-633 -->

* È stato risolto un errore che poteva comparire nella console di sviluppo del browser. <!-- CCSAAS-4650 -->

* È stato corretto un errore che poteva verificarsi durante l’annullamento di un ordine guest con commenti sull’ordine. <!-- ACCS-674 -->

* È stato corretto un errore che poteva verificarsi durante l’aggiunta di un prodotto raggruppato con molti articoli associati a un elenco di richieste di acquisto. <!-- ACCS-627 -->

>[!ENDSHADEBOX]

## Marzo 2026 - #2 sulla versione

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

I seguenti elementi sono stati rilasciati negli ambienti di produzione il 24 marzo 2026.

>[!BEGINSHADEBOX]

### Accedi come cliente utilizzando codici occasionali

Gli amministratori ora possono generare [codici occasionali](https://experienceleague.adobe.com/it/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer) per la rappresentazione del cliente tramite l&#39;API [!DNL Commerce Admin] e REST. Il codice una tantum può essere scambiato con un token di accesso del cliente tramite le mutazioni GraphQL `generateCustomerToken` o `exchangeOtpForCustomerToken`, abilitando flussi &quot;Accedi come cliente&quot; senza password per scenari di acquisto assistito dal venditore. <!-- ACCS-404 -->

Per istruzioni sull&#39;implementazione di questa funzionalità tramite API, consulta la documentazione [REST API](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/) e [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/).

### Gestire gli account gift card tramite l’API REST

È ora possibile creare, aggiornare, eliminare e interrogare [account gift card](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/) tramite l&#39;API REST. Inoltre, il supporto per l&#39;importazione in blocco JSON è disponibile tramite l&#39;endpoint `/V1/import/json`, consentendo alle integrazioni di terze parti di sincronizzare in modo programmatico le gift card. <!-- ACCS-476 -->

### Attivare le e-mail transazionali tramite l’API REST

Un nuovo endpoint REST API (`POST /V1/custom-email/send`) consente di [attivare le e-mail transazionali](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/) su richiesta specificando un ID modello e-mail, un indirizzo e-mail del destinatario e variabili modello. L’API supporta array nidificati come variabili modello per contenuti e-mail complessi. <!-- ACCS-325, ACCS-481 -->

### Iscriviti al webhook di recupero tariffe spedizione fuori processo

Il webhook `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` è ora disponibile nell&#39;elenco dei webhook di amministrazione in [!DNL Adobe Commerce as a Cloud Service]. Utilizzala per implementare [metodi di spedizione personalizzati](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods). <!-- ACCS-478 -->

### Caricare PDF e altri file tramite gli attributi del prodotto

Un nuovo &quot;file&quot; [Tipo di input attributo](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/attributes-input-types) consente di creare set di attributi in cui è possibile caricare file, ad esempio PDF, in singoli prodotti. Puoi configurare le estensioni di file consentite e la dimensione massima del file passando a [!UICONTROL **Archivi**] > [!UICONTROL **Configurazione**] > [!UICONTROL _Catalogo_] > [!UICONTROL **Attributi del file di prodotto**]. <!-- ACCS-535, ACCS-565 -->

### Configurare gli attributi personalizzati della società

Gli amministratori ora possono gestire gli attributi personalizzati della società nella pagina di modifica della società in [!DNL Commerce Admin]. Gli attributi personalizzati possono essere configurati, salvati e convalidati dall&#39;interfaccia utente di amministrazione per [!DNL Adobe Commerce as a Cloud Service].

Per configurare gli attributi personalizzati della società, passa a [!UICONTROL **Clienti**] > [!UICONTROL **Società**] e seleziona una società per aprire la pagina di modifica. Quindi seleziona la scheda [!UICONTROL **Attributi personalizzati**] per aggiungere nuovi attributi.
<!-- ACCS-294 -->

### Iscriviti agli avvisi su prezzi e azioni tramite GraphQL

Gli storefront EDS ora funzionano con [avvisi di prezzo e scorte](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup). <!-- ACCS-334 -->

Inoltre, esistono diverse nuove mutazioni di GraphQL per abbonarsi e annullare l’abbonamento agli avvisi sui prezzi e sulle azioni:

+++Nuove mutazioni GraphQL

```graphql
mutation {
  subscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStockAll {
    success
    message
  }
}
```

```graphql
mutation {
  subscribeProductAlertPrice(input: { sku: "ADB112" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPrice(input: { sku: "ADB115" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPriceAll {
    success
    message
  }
}
```

+++

### Miglioramenti e correzioni di bug

In questa versione sono inclusi i miglioramenti, le ottimizzazioni e le correzioni di bug seguenti:

* Il ruolo aziendale [!UICONTROL Sales] > [!UICONTROL View Orders] ora funziona come previsto. <!-- ACCS-604 -->

* L&#39;attributo di estensione del cliente `last_login_at` è ora disponibile tramite l&#39;API REST, consentendo alle integrazioni di recuperare la data di accesso più recente per ogni cliente. <!-- ACCS-555 -->

* È stato risolto un problema relativo ai suggerimenti del modulo di integrazione [!DNL AEM Assets]. <!-- ACCS-209 -->

* È stato risolto un problema che causava un errore in seguito alle azioni di assegnazione e annullamento dell’assegnazione di società in blocco sulla griglia del catalogo condiviso. <!-- CCSAAS-4614 -->

* È stato risolto un problema a causa del quale la determinazione del prezzo del carrello personalizzato veniva sovrascritta quando lo stesso prodotto veniva aggiunto nuovamente al carrello con una quantità o un prezzo personalizzato diverso. <!-- ACCS-529 -->

* Gli UID delle voci dell’elenco richieste di acquisto ora sono coerenti con gli UID del carrello e delle voci dell’elenco dei desideri. <!-- ACCS-349 -->

* È stato corretto un timeout della pagina di modifica del prodotto che poteva verificarsi con cataloghi condivisi di grandi dimensioni. <!-- CCSAAS-4657 -->

* Riabilitazione degli endpoint REST API per GET `/V1/directory/countries` e GET `/V1/directory/countries/:countryId` per le integrazioni amministratore, consentendo ai client di cercare dati validi per paese e area geografica. <!-- ACCS-518 -->

* È stato risolto un problema di timeout che poteva verificarsi nell’API REST quando un utente disponeva di un catalogo condiviso di grandi dimensioni. <!-- ACCS-4657 -->

* È stato risolto un problema a causa del quale le aziende B2B bloccate potevano comunque aggiungere prodotti al carrello. <!-- ACCS-552 -->

* Se si dispone di una grande quantità di dati sulle griglie Cliente o Società, i pulsanti di esportazione non sono più disponibili per evitare errori. <!-- ACCS-320 -->

* È stato risolto un problema che impediva la corretta visualizzazione delle dimensioni dei file allegati. <!-- ACCS-566 -->

* È stato risolto un problema relativo alla creazione e all&#39;eliminazione dei tipi di attributi &quot;File&quot; in [!DNL Commerce Admin]. <!-- ACCS-605, ACCS-606 -->

>[!ENDSHADEBOX]


## Marzo 2026 - #1 sulla versione

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

I seguenti elementi sono stati rilasciati negli ambienti di produzione di [!DNL Adobe Commerce as a Cloud Service] il 9 marzo 2026.

>[!BEGINSHADEBOX]

### Strumenti e tutorial di codifica di IA per App Builder

È ora possibile utilizzare gli strumenti per sviluppatori di codifica [AI](https://developer.adobe.com/commerce/extensibility/developer-agent/){target="_blank"} per creare nuove applicazioni [!DNL App Builder] e convertire le estensioni PHP [!DNL Adobe Commerce] esistenti in applicazioni [!DNL App Builder]. Sono disponibili i seguenti tutorial per dimostrare come utilizzare gli strumenti:

* [Prerequisiti del tutorial](./tutorials/tutorial-prerequisites.md)
* [Esercitazione sull’estensione delle valutazioni](./tutorials/ratings-extension.md)
* [Esercitazione sull’estensione del metodo di spedizione](./tutorials/shipping-method-extension.md)

### Accedere alla gestione delle app App Builder tramite l’amministratore

[!DNL Commerce Admin] ora include una voce di menu che si collega a [Gestione app](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}, una shell unificata per la gestione di [!DNL App Builder] app associate all&#39;istanza di Commerce. Questa aggiunta è basata sull’ultimo aggiornamento SDK dell’interfaccia utente di amministrazione. <!-- CEXT-5755 -->

### Richiedi modifica limite creazione entità

In precedenza, il limite del numero di siti web, store e visualizzazioni dello store era limitato a 50. È ora possibile inviare una [richiesta di supporto](https://experienceleague.adobe.com/home?lang=it&support-tab=home#support) per modificare questi limiti, se necessario. <!-- ACCS-398 -->

### Personalizzare i messaggi di autenticazione della vetrina con codici di errore strutturati

La mutazione di GraphQL [`generateCustomerToken`](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"} ora restituisce codici di errore digitati insieme ai messaggi di errore, consentendo a storefront di visualizzare messaggi di interfaccia utente specifici per motivo dell&#39;errore. I codici di errore disponibili includono: `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED` e `CUSTOMER_GENERIC_ERROR`. <!-- ACCS-301 -->

### Inviare promemoria e-mail automatizzati per l’inattività del carrello e della lista dei desideri

Il modulo [Promemoria e-mail](https://experienceleague.adobe.com/it/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`) è ora attivo in [!DNL Adobe Commerce as a Cloud Service], consentendo agli esercenti di creare regole di promemoria automatizzate che attivano le e-mail ai clienti in base all&#39;inattività del carrello e della lista dei desideri. <!-- CCSAAS-4597 -->

### Webhook eventi di eliminazione categoria per iscrizione

Il webhook `observer.catalog_category_delete_before` è ora disponibile in [!DNL Adobe Commerce as a Cloud Service]. Utilizzalo per eseguire la logica prima che una categoria venga eliminata. <!-- CEXT-5862 -->

### Tracciare gli ordini degli ospiti inviati tramite e-mail registrata

Una nuova configurazione facoltativa a livello di negozio consente ai clienti di [tenere traccia degli ordini dei clienti](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails) effettuati, se l&#39;ordine è stato effettuato utilizzando un indirizzo e-mail corrispondente a un account cliente registrato. <!-- ACCS-289 -->

### Miglioramenti e correzioni di bug

In questa versione sono inclusi i miglioramenti, le ottimizzazioni e le correzioni di bug seguenti:

* È stato risolto un problema che impediva ad alcuni amministratori dell’organizzazione di accedere in modo errato alle istanze del tenant senza diritti per tenant. <!-- ACCS-335 -->

* È stato risolto un problema che poteva provocare la disconnessione di un utente da [!DNL Commerce Admin] quando apportava modifiche a un catalogo condiviso. <!-- ACCS-318 -->

* È stato risolto un problema che causava la visualizzazione errata di alcuni campi webhook nell&#39;interfaccia utente [!DNL Commerce Admin]. <!-- CEXT-5874 -->

>[!ENDSHADEBOX]

## Febbraio 2026 - #2 sulla versione

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

I seguenti elementi sono stati rilasciati negli ambienti di produzione di [!DNL Adobe Commerce as a Cloud Service] il 24 febbraio 2026.

>[!BEGINSHADEBOX]

### Inviare campi di contesto con eventi commerciali

[!DNL Adobe Commerce as a Cloud Service] ora supporta [campi di contesto](https://developer.adobe.com/commerce/extensibility/events/context-fields/) nei payload dell&#39;evento, consentendo di includere dati che non fanno parte dell&#39;evento per impostazione predefinita. <!-- CEXT-5713 -->

### Iscriviti agli eventi di salvataggio degli elementi del preventivo utilizzando un nuovo webhook

Il webhook `observer.sales_quote_item_save_before` è ora disponibile in [!DNL Adobe Commerce as a Cloud Service]. Utilizzarlo per eseguire la logica prima del salvataggio di un preventivo. <!-- ACCS-346 -->

### Miglioramenti e correzioni di bug

In questa versione sono inclusi i miglioramenti, le ottimizzazioni e le correzioni di bug seguenti:

* È stato corretto un errore che poteva causare problemi di visualizzazione nell&#39;elenco prodotti [!DNL Commerce Admin]. L’elenco dei prodotti ora limita il numero di cataloghi condivisi visualizzati per migliorare le prestazioni. <!-- CCSAAS-1242 -->

* È stato corretto un errore di GraphQL che poteva impedire l’aggiunta di gift card personalizzabili al carrello. <!-- ACCS-313 -->

>[!ENDSHADEBOX]

## Febbraio 2026 - #1 sulla versione

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

I seguenti elementi sono stati rilasciati negli ambienti di produzione di [!DNL Adobe Commerce as a Cloud Service] il 10 febbraio 2026.

>[!BEGINSHADEBOX]

### Personalizza i metodi di spedizione e visualizza i rapporti dell’amministratore

Sono stati apportati i seguenti miglioramenti a [!DNL Commerce Admin]:

* Sono stati migliorati [i payload del webhook di spedizione](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload) out-of-process per includere gli attributi personalizzati dell&#39;indirizzo di spedizione. Questa modifica consente ai commercianti di implementare metodi di spedizione personalizzati. <!-- ACCS-235 -->

* È stato aggiunto l&#39;accesso ai report dell&#39;amministratore, inclusi i report per [Clienti](https://experienceleague.adobe.com/it/docs/commerce-admin/start/reporting/customer-reports), [Marketing](https://experienceleague.adobe.com/it/docs/commerce-admin/start/reporting/marketing-reports), [Prodotti](https://experienceleague.adobe.com/it/docs/commerce-admin/start/reporting/product-reports) e [Vendite](https://experienceleague.adobe.com/it/docs/commerce-admin/start/reporting/sales-reports). <!-- CCSAAS-3085 -->

>[!NOTE]
>
>I report non disponibili in [!DNL Adobe Commerce as a Cloud Service] sono etichettati solo come PaaS ([!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."}).

### Acquisire gli importi delle fatture personalizzate tramite API REST

L&#39;API Fattura ora supporta [importi di acquisizione personalizzati](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) utilizzando gli attributi di estensione. <!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>A causa di restrizioni legali, l&#39;importo di cattura personalizzato è disponibile solo nell&#39;area Nord America (NA) e in altre aree geografiche in cui è consentita la sovrascrittura dei pagamenti.

### Miglioramenti e correzioni di bug

In questa versione sono inclusi i miglioramenti, le ottimizzazioni e le correzioni di bug seguenti:

* È stato corretto il filtro Griglia coupon per visualizzare tutti i coupon personalizzati creati tramite l’API o l’importazione. <!-- CCSAAS-4509 -->

* È stato risolto un problema in [!DNL Storefront Compatibility B2B Package] a causa del quale la mutazione `setNegotiableQuoteShippingAddress` non salvava gli indirizzi immessi manualmente nella rubrica del cliente, anche quando `save_in_address_book` era impostato su `true`. <!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* È stato risolto un problema che impediva la corretta visualizzazione delle immagini del prodotto in [!DNL Edge Delivery Services] a causa di valori `no_selection` danneggiati negli attributi personalizzati relativi ai ruoli delle risorse. <!-- ACAP-1206 -->

* È stato risolto un problema che impediva agli account utente federati con valori di nome o cognome null di accedere all’amministratore di Commerce. <!-- ACCS-200 -->

* La configurazione di Asset Selector è stata semplificata fornendo automaticamente gli ID client IMS specifici per regione. I commercianti non dovranno più inviare ticket di supporto per configurare Asset Selector per la mappatura delle immagini delle categorie di prodotti con le risorse. Il sistema ora utilizza automaticamente gli ID client IMS dedicati basati sull’area geografica di Commerce. <!-- ACCS-175 -->

* Vari miglioramenti a livello di prestazioni e ottimizzazione. <!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

>[!ENDSHADEBOX]

## Gennaio 2026

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

I seguenti elementi sono stati rilasciati negli ambienti di produzione di [!DNL Adobe Commerce as a Cloud Service] il 20 gennaio 2026.

>[!BEGINSHADEBOX]

### Eliminazioni B2B

Sono state apportate le seguenti modifiche ai componenti di rilascio B2B:

* [!DNL Commerce Storefront on Edge Delivery Services] ora include [componenti di eliminazione B2B](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=it). Sono ora disponibili i seguenti menu a discesa B2B:

   * **[Gestione società](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/?lang=it)** - Abilita la gestione del profilo società e le autorizzazioni basate sui ruoli per le vetrine di Adobe Commerce.
   * **[Commutatore società](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/?lang=it)** - Fornisce un componente dell&#39;interfaccia utente che consente agli utenti di passare da un&#39;azienda all&#39;altra a cui sono associati.
   * **[Ordini di acquisto](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/?lang=it)** - Gestisce i flussi di lavoro degli ordini di acquisto, le regole di approvazione e la cronologia degli ordini di acquisto per le transazioni B2B.
   * **[Gestione dei preventivi](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/?lang=it)** - Abilita i preventivi negoziabili per i clienti B2B con flussi di lavoro di richiesta, negoziazione e approvazione.
   * **[Elenchi di richieste](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/?lang=it)** - Fornisce gli strumenti per la creazione e la gestione degli elenchi di richieste per acquisti ripetuti e ordini in blocco.

* È stato rilasciato il pacchetto di compatibilità per la vetrina B2B. Questo pacchetto migliora lo schema GraphQL B2B di [!DNL Adobe Commerce] per migliorare lo sviluppo dei sistemi B2B.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=it). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/?lang=it). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. 
-->

### Collegamenti cliccabili ai tracker di spedizione esterni

Trasforma i numeri di tracciamento della spedizione inclusi nelle e-mail dei clienti da testo normale in collegamenti cliccabili [abilitando gli URL di tracciamento personalizzati](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Questa funzionalità è supportata per USPS, UPS, FedEx e DHL. <!-- See PR #716 in commerce-admin -->

### Supporto di Google reCAPTCHA Enterprise

[!DNL Adobe Commerce as a Cloud Service] storefront ora supportano [reCAPTCHA Enterprise](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Questa funzione offre una protezione avanzata dei bot utilizzando l’analisi adattiva dei rischi e l’apprendimento automatico per distinguere con precisione gli utenti umani dai bot automatizzati. Rafforza la sicurezza del sito, impedisce le attività fraudolente e riduce lo spam e gli abusi per mantenere un’esperienza di acquisto affidabile. <!-- CCSAAS-4242 -->

### Accesso amministratore specifico per istanza

Ora puoi [assegnare agli utenti l&#39;accesso](./user-management.md#add-users) alle singole [!DNL Adobe Commerce as a Cloud Service] istanze in Admin Console. <!-- CCSAAS-4337 -->
<!-- See PR #332 -->

### Osservabilità

Utilizzando [!DNL App Builder], è possibile ottenere una visibilità più approfondita nell&#39;istanza [!DNL Adobe Commerce as a Cloud Service] con [osservabilità OpenTelemetry](https://developer.adobe.com/commerce/extensibility/observability/), ora disponibile automaticamente. OpenTelemetry fornisce metriche, registri e tracce che consentono di monitorare le prestazioni, risolvere più rapidamente i problemi e ottimizzare la vetrina. Questa funzionalità consente di ottenere informazioni proattive sullo stato del sistema e migliora l’affidabilità per i clienti.

>[!NOTE]
>
>L&#39;osservabilità OpenTelemetry richiede l&#39;utilizzo di [!DNL App Builder] o altre offerte di estendibilità fuori processo (OOPE).

### Determinazione prezzi a livello per le regole di prezzo catalogo

È ora possibile combinare gli sconti per prezzi su più livelli con gli sconti delle regole di catalogo utilizzando [regole di prezzo catalogo](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). Questo miglioramento consente di creare strategie di prezzo più dinamiche e competitive, premiando gli acquisti in blocco e applicando contemporaneamente sconti promozionali. Il risultato è una maggiore flessibilità per attrarre clienti, aumentare il valore dell&#39;ordine e favorire le conversioni.<!-- See PR #708 in commerce-admin -->

### Miglioramenti e correzioni di bug

I miglioramenti, le ottimizzazioni e le correzioni di bug seguenti inclusi in questa versione:

* È stato risolto un errore che poteva verificarsi durante il caricamento di un file in S3. <!-- CCSAAS-4189 -->

* È stato risolto un errore `User is not entitled to access this instance` che poteva verificarsi quando si accedeva all&#39;amministrazione di Commerce o all&#39;API REST. <!-- CCSAAS-4324 -->

* È stato corretto un errore che si verificava durante l’anteprima o l’accodamento di una newsletter dalla griglia del modello della newsletter. <!-- CCSAAS-4398 -->

* È stato corretto un errore `404` che si verificava facendo clic sul pulsante [!UICONTROL **Ricarica dati**] nel dashboard di amministrazione. <!-- CCSAAS-4468 -->

* È stato risolto un problema che impediva l&#39;aggiornamento degli attributi personalizzati del prodotto tramite l&#39;API REST quando [!DNL AEM Assets integration] era abilitato e il prodotto conteneva immagini. <!-- ACAP-1178 -->

* Vari miglioramenti a livello di prestazioni e ottimizzazione.
<!-- CCSAAS-4255 -->
<!-- CCSAAS-4233 -->
<!-- CCSAAS-4220 -->
<!-- CCSAAS-4252 -->
<!-- CCSAAS-4330 -->
<!-- CCSAAS-3669 -->
<!-- CCSAAS-4462 -->

>[!ENDSHADEBOX]

## Novembre 2025

>[!BEGINSHADEBOX]

### Miglioramenti

* [Gestione utenti](./user-management.md) - È stato modificato il ruolo **Amministratore prodotti** in Admin Console per aggiornare automaticamente l&#39;accesso degli utenti all&#39;Amministratore Commerce. <!-- CCSAAS-3012 -->

* È stata aggiunta la possibilità di caricare e recuperare in Amazon S3 allegati di preventivi negoziabili nonché file e immagini associati a clienti e indirizzi dei clienti utilizzando URL prefirmati in [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) e [REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads). Con REST è possibile caricare anche immagini di categorie. <!-- CCSAAS-3250 -->

* Sono stati aggiunti gli endpoint `POST /V1/customers` e `PUT /V1/customers/{customerId}` all&#39;[API REST](https://developer.adobe.com/commerce/webapi/rest/reference/) per creare e aggiornare i clienti. Questi endpoint richiedono l’autorizzazione IMS. <!-- CCSAAS-3112 -->

* È stata aggiunta la mutazione [`exchangeOtpForCustomerToken`](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), che richiede l&#39;indirizzo e-mail di un acquirente e una password monouso (OTP) e riceve in cambio un token cliente. Questa mutazione viene generalmente utilizzata in scenari in cui un cliente deve eseguire l’autenticazione utilizzando un OTP inviato alla propria e-mail o al proprio telefono.

* Se un indirizzo definito nella schermata di configurazione [!UICONTROL **Archivia indirizzi e-mail**] nell&#39;amministratore contiene un valore che termina con `example.com`, Commerce non invia e-mail a questo indirizzo. Il sistema invece registra che l’e-mail non è stata inviata.  <!-- CCSAAS-3533 -->

#### Attributi ordine personalizzati

* Gli utenti amministratori ora possono visualizzare e modificare [attributi dell&#39;ordine personalizzati](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) direttamente dalle schermate Visualizzazione ordine, Modifica e Crea nel pannello Amministratore. Questo miglioramento migliora la gestione dei dati degli ordini personalizzati creati tramite GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
