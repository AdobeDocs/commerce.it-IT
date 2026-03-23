---
title: Accedi come cliente con codici occasionali
description: Scopri come utilizzare la funzione Login as Customer OTC per generare codici una tantum per l'autenticazione del cliente in [!DNL Adobe Commerce as a Cloud Service].
role: Admin
level: Intermediate
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 2de1006ad3cee936d114bcf1b9a98b43a54d8c76
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Accedi come cliente

{{accs-sandbox-experimental}}

La funzione Login as Customer OTC (One-Time Code) consente agli utenti amministratori di generare per un cliente un codice monouso di breve durata. Questo codice può essere scambiato con un token di accesso del cliente tramite GraphQL, abilitando flussi di lavoro senza password **Accedi come cliente** per scenari di acquisto assistito dal venditore.

L’accesso come cliente è costituito dai seguenti componenti:

* **Interfaccia utente amministratore** - Nella pagina di modifica del cliente, gli amministratori possono richiedere un codice monouso (OTC) invece di accedere direttamente come cliente.
* **REST API** - Endpoint programmatico per la generazione OTC, utile per script di amministrazione e integrazioni di terze parti.
* **API GraphQL** - Mutazioni che scambiano un OTC con un token di accesso del cliente per flussi commerciali storefront o headless.

## Generare un codice monouso dall’amministratore

L&#39;OTC Accedi come cliente sostituisce il pulsante standard Accedi come cliente nella pagina di modifica del cliente con un pulsante [!UICONTROL **Ottieni OTC di accesso cliente**]. Il codice una tantum generato può quindi essere utilizzato con la vetrina o con il GraphQL per gli acquisti assistiti dal venditore.

>[!NOTE]
>
>Il pulsante **Accedi come cliente** non è disponibile nelle pagine Ordine, Fattura, Spedizione e Nota di credito.

### Prerequisiti

Prima di utilizzare la funzione di accesso come cliente, è necessario soddisfare i seguenti requisiti:

* **Autorizzazione amministratore** - L&#39;utente amministratore deve avere l&#39;autorizzazione `Magento_LoginAsCustomer::login` per l&#39;elenco di controllo di accesso (ACL) abilitata nel proprio ruolo di amministratore per accedere come cliente.

* **Consenso cliente** - L&#39;attributo dell&#39;estensione `login_as_customer_assistance_allowed` deve essere impostato su **2**. Questa può essere configurata nella pagina **Modifica cliente** dell&#39;amministratore o tramite GraphQL durante la creazione o la modifica di un cliente.

  ![Configurazione dell&#39;attributo di estensione del consenso del cliente nella pagina Modifica cliente](./assets/customer-consent-attribute.png){width="600" zoomable="yes"}

* **Estensione Accedi come cliente abilitata** - La funzionalità Accedi come cliente non è disponibile quando l&#39;estensione Accedi come cliente è disabilitata. Per verificare che l&#39;estensione sia abilitata, passa a [!UICONTROL **Archivi**] > [!UICONTROL **Configurazione**] > [!UICONTROL **Clienti**] > [!UICONTROL **Accedi come cliente**] > [!UICONTROL **Abilita estensione**].

### Richiedi codice monouso (OTC)

1. Passa a [!UICONTROL **Clienti**] e seleziona un cliente per aprire la pagina di modifica.

1. Nella pagina Modifica cliente fare clic su [!UICONTROL **Ottieni l&#39;accesso del cliente OTC**].

   ![Pulsante Ottieni OTC accesso cliente nella pagina Modifica cliente](./assets/get-customer-login-otc-button.png){width="600" zoomable="yes"}

1. Immetti un [!UICONTROL **motivo**] (obbligatorio) e fai clic su [!UICONTROL **Richiesta**].

   ![Richiesta OTC modale con campo Motivo](./assets/otc-reason-modal.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Il campo **Reason** è obbligatorio. Viene passato al flusso di generazione OTP ed è riservato per l’utilizzo nelle prossime funzioni di controllo e registrazione degli eventi.

1. L’OTC generato viene visualizzato nel modale. Usa questo codice con la mutazione GraphQL `generateCustomerToken` o `exchangeOtpForCustomerToken` per l&#39;autorizzazione del cliente.

   ![OTC generato visualizzato nel modale](./assets/otc-generated-code.png){width="300" zoomable="yes"}

>[!IMPORTANT]
>
>L’OTC del codice monouso generato è valido per 30 secondi per impostazione predefinita e viene invalidato dopo un singolo utilizzo. Il TTL può essere configurato inviando un [ticket di supporto](https://experienceleague.adobe.com/home?lang=it&support-tab=home#support).

Dopo aver generato il codice una tantum, puoi utilizzarlo accedendo alla vetrina e accedendo utilizzando le seguenti credenziali:

* **E-mail**: indirizzo e-mail del cliente
* **Password**: codice monouso (OTC) generato

## Generare un codice una tantum utilizzando l’API REST

L&#39;endpoint POST `V1/customer/:customerId/otp` fornisce un modo programmatico per generare un OTC per un cliente. Questa funzione è utile per le interfacce utente dell’amministratore, gli script o le integrazioni di terze parti che devono attivare in modo coerente il rilascio OTC.

### Contratto REST

| Elemento | Valore |
|---|---|
| **Metodo** | POST |
| **URL** | `/rest/V1/customer/:customerId/otp` |
| **Autenticazione** | Token amministratore (Bearer). ACL richiesto: `Magento_LoginAsCustomer::login`. |
| **Corpo della richiesta** | JSON con campo `reason` facoltativo. Utilizzato per il controllo e la registrazione. |
| **Risposta di successo** | HTTP 200, JSON con `otp` (stringa esadecimale di 32 caratteri). |
| **Risposte di errore** | Errori API Web standard (ad esempio, 401, 403). Se l’assistenza clienti Login as è disabilitata per il cliente, potrebbe essere visibile la dicitura 500 o un’eccezione mappata. |

### Esempio di richiesta

```text
POST /rest/V1/customer/:customerId/otp
Content-Type: application/json
```

```json
{"reason": "Support session"}
```

### Esempio di risposta

```json
{"otp": "a1b2c3d4e5f6789012345678abcdef01"}
```

## Scambia un codice una tantum con un token cliente tramite GraphQL

Dopo aver generato un OTC (dall’interfaccia utente di Admin o dall’API REST), utilizza una delle seguenti mutazioni GraphQL per scambiarlo con un token di accesso del cliente.

### `generateCustomerToken` mutazione

La mutazione `generateCustomerToken(email, password)` restituisce un token cliente. L&#39;argomento `password` viene valutato nell&#39;ordine seguente:

1. **Password cliente (predefinita)** - Password dell&#39;account del cliente.
1. **Token password reimpostazione cliente (uso una tantum)** - Token valido da **Password dimenticata** (ad esempio, la mutazione `requestPasswordResetEmail`). Consumato al primo utilizzo.
1. **Codice OTC (one-time code) generato dall&#39;amministratore** - Codice generato da un amministratore per il cliente tramite l&#39;API REST o l&#39;interfaccia utente dell&#39;amministratore. Uso una tantum, di breve durata (30 secondi per impostazione predefinita).

**Schema:**

```graphql
type Mutation {
  generateCustomerToken(email: String!, password: String!): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**Esempio: accesso con OTC amministratore**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

Variabili (utilizzare OTC come `password`):

```json
{
  "email": "customer@example.com",
  "password": "<admin-generated-OTC>"
}
```

**Esempio: accesso con password**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

Variabili:

```json
{
  "email": "customer@example.com",
  "password": "CustomerPassword123"
}
```

**Esempio: accesso con token di reimpostazione password**

Dopo che il cliente ha richiesto la reimpostazione della password (ad esempio, `requestPasswordResetEmail`), il token di reimpostazione ricevuto tramite il collegamento e-mail può essere utilizzato come `password` in `generateCustomerToken` (utilizzo una tantum).

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

Variabili (utilizzare il token di ripristino come `password`):

```json
{
  "email": "customer@example.com",
  "password": "<reset-password-token-from-email-link>"
}
```

**Risposta di esempio:**

```json
{
  "data": {
    "generateCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### `exchangeOtpForCustomerToken` mutazione

La mutazione `exchangeOtpForCustomerToken` scambia un token di reimpostazione della password o un OTP generato da un amministratore per un token di accesso del cliente. L’OTP viene invalidato dopo il corretto scambio (utilizzo una tantum). Questo endpoint rispetta la configurazione reCAPTCHA.

**Schema:**

```graphql
type Mutation {
  exchangeOtpForCustomerToken(
    email: String!
    otp: String!
  ): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**Richiesta di esempio:**

```graphql
mutation ExchangeOtpForCustomerToken($email: String!, $otp: String!) {
  exchangeOtpForCustomerToken(email: $email, otp: $otp) {
    token
  }
}
```

Variabili:

```json
{
  "email": "customer@example.com",
  "otp": "<one-time-password>"
}
```

**Risposta di esempio:**

```json
{
  "data": {
    "exchangeOtpForCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### Riepilogo mutazione

| Mutazione | Caso d’uso |
|---|---|
| `generateCustomerToken(email, password)` | Singolo punto di ingresso: password del cliente, token di reimpostazione password, OTC amministratore o OTP (provato dopo la reimpostazione della password). |
| `exchangeOtpForCustomerToken(email, otp)` | Scambio token password OTP o reimpostazione. Il token OTP (o il token di reimpostazione password) viene utilizzato dopo l’uso. |

Il token di reimpostazione password e l&#39;OTC amministratore vengono entrambi passati come argomento `password` a `generateCustomerToken`. Il Risolutore rileva il tipo di token e lo convalida di conseguenza.
