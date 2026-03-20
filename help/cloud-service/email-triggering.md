---
title: Attivazione delle e-mail tramite REST
description: Scopri come attivare le e-mail transazionali su richiesta utilizzando l’API REST specificando un ID modello, un’e-mail destinatario e variabili modello per  [!DNL Adobe Commerce as a Cloud Service].
role: Admin
level: Experienced
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 9661e368f7a0dc85edcd3e52a67ae2a98355d8b5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Attivazione delle e-mail tramite API REST

In precedenza, era possibile inviare e-mail solo quando venivano attivati gli eventi, ad esempio durante la registrazione del cliente o l’acquisto di un ordine. In [!DNL Adobe Commerce as a Cloud Service] è possibile inviare e-mail tramite l&#39;API REST su richiesta specificando un ID modello, un indirizzo e-mail destinatario e variabili modello.

>[!NOTE]
>
>Al momento, è possibile inviare solo i modelli personalizzati appena creati. I modelli predefiniti e di sistema non sono supportati.

L&#39;endpoint `V1/custom-email/send` consente a **sistemi di terze parti**, quali integrazioni e servizi esterni, di inviare e-mail su richiesta specificando:

- **ID modello** - ID modello e-mail.
- **E-mail destinatario** - Indirizzo e-mail di destinazione per questa richiesta.
- **Variabili** - (Facoltativo) Coppie chiave-valore definite personalizzate da inserire nel modello, ad esempio `customer_name` o `order_id`.

>[!NOTE]
>
>L&#39;e-mail viene inviata in modo sincrono utilizzando l&#39;ambito dell&#39;archivio corrente e l&#39;indirizzo e-mail predefinito **Da** o l&#39;indirizzo e-mail definito per i modelli.

## Contratto REST

La sezione seguente spiega come inviare e-mail transazionali su richiesta utilizzando l’API REST.

### Endpoint

- **URL** - `POST /rest/V1/custom-email/send`
- **Autorizzazione** - È supportata solo **autorizzazione IMS da servizio a servizio**. Il chiamante deve avere accesso alla risorsa **Invia e-mail personalizzata tramite API** (`Magento_CustomEmailSend::send_custom_email`). Per ulteriori informazioni, consultare [autenticazione REST](https://developer.adobe.com/commerce/webapi/rest/authentication/).
- **Utilizzo asincrono** (consigliato) - Sebbene questo endpoint sia implementato in modo sincrono, è consigliabile chiamarlo utilizzando l&#39;**API REST asincrona** in modo che la richiesta venga accodata ed elaborata da un consumer, evitando connessioni HTTP di lunga durata. In [!DNL Adobe Commerce as a Cloud Service] è possibile utilizzare la route con `/async` dopo `V1`, ad esempio: `POST https://<server>.api.commerce.adobe.com/<tenant-id>/V1/async/custom-email/send`.

  Per ulteriori informazioni, fare riferimento a [endpoint Web asincroni (SaaS)](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/).

### Corpo della richiesta

- **templateId** (interger, obbligatorio) - ID modello e-mail come definito nell&#39;amministratore in [!UICONTROL **Marketing**] > [!UICONTROL _Comunicazioni_] > [!UICONTROL **Modelli e-mail**].

- **recipientEmail** (stringa, obbligatorio) - Indirizzo e-mail di destinazione. Deve essere un formato e-mail valido. Valori mancanti o vuoti attivano un errore di convalida.
- **variabili** (oggetto, facoltativo) - Mappa chiave-valore inserita nel modello come `UnstructuredArray`.

  Se non utilizzi le variabili, passa un oggetto vuoto o omettilo. Nel corpo e nell&#39;oggetto del modello e-mail, utilizzare la sintassi della variabile per fare riferimento a una variabile, ad esempio `var order_id`. L&#39;oggetto supporta inoltre le stesse variabili personalizzate e la stessa sintassi descritte in [Scenari modello supportati](#supported-template-scenarios).

### Risposta di successo (HTTP 200)

L’API restituisce HTTP 200 in caso di invio corretto.

### Risposte di errore

- **HTTP 400 - Errore di convalida**

  L&#39;integrazione deve fornire un `templateId` e un `recipientEmail` validi per ogni richiesta.

   - `"message": "Invalid recipient email format"` - indirizzo destinatario non valido o non valido
   - `"message": "Recipient email is required."` - `recipientEmail` mancante o vuoto
   - `"message": "Template ID must be a positive integer."` - mancante, zero o non valido `templateId`

- **HTTP 404 - Modello non trovato**

  Esempio: `"message": "Email template with ID \"999\" does not exist."`

## Scenari di modelli supportati

Le seguenti funzionalità dei modelli sono supportate sia nel **corpo dell&#39;e-mail** che nel **oggetto del modello**:

>[!NOTE]
>
>L’oggetto del modello supporta anche variabili personalizzate. Utilizzare `var variableName` e altra sintassi come descritto nella sezione seguente.

- **Includi direttiva** - per includere altri modelli di progettazione, ad esempio un&#39;intestazione e-mail.

  ```javascript
  {{template config_path="design/email/header_template"}}
  ```

- **Variabili semplici**. Utilizzare `var variableName`, ad esempio `var order_id` o `var g`.

  ```javascript
  {{var order.test}}
  {{var g}}
  {{var order_id}}
  ```

- **Notazione annidata/con punto**: per le chiavi annidate passate nella richiesta `variables`, nelle traduzioni vengono utilizzati nomi con prefisso dollaro, ad esempio `$order_data.customer_name`, `$order.increment_id` o `$order_data.frontend_status_label`.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Traduzione (trans)** - testo con parametri, traduzioni su più righe con più segnaposto e tag HTML.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Output non elaborato**. Utilizzare il filtro `|raw` quando il contenuto tradotto o variabile contiene HTML, ad esempio `<strong>` o `<a>`.

  ```javascript
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Helper URL** - per gli URL dell&#39;archivio nelle traduzioni.

  ```javascript
  {{trans 'You can check the status of your order by [logging into your account](%account_url).' account_url=$this.getUrl($store,'customer/account/',[_nosid:1]) |raw}}
  ```
