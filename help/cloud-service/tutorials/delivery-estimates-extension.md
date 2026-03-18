---
title: Esercitazione sull’estensione delle stime di consegna
description: Scopri come creare un’estensione delle stime delle date di consegna per Adobe Commerce as a Cloud Service utilizzando App Builder, Edge Delivery Services e strumenti di sviluppo assistiti da intelligenza artificiale.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3fc8982613df7b1155cdfb08ac4b56de6d1ce4f6
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 0%

---

# Tutorial sull’estensione delle stime di consegna

Questa esercitazione ti guida attraverso la creazione di un&#39;estensione delle stime della data di consegna per [!DNL Adobe Commerce as a Cloud Service] utilizzando [!DNL Adobe App Builder], [!DNL Edge Delivery Services] e strumenti di sviluppo assistiti da IA. L’estensione recupera le stime dei tempi di spedizione e delle date di consegna da un’API esterna e le visualizza nella vetrina.

Vengono create due parti:

- **Estensione App Builder**: azione back-end-for-frontend (BFF) che esegue il wrapping di un&#39;API per la stima della consegna esterna, un webhook che arricchisce i metodi di spedizione con le date di consegna al momento del pagamento e una pagina di configurazione dell&#39;interfaccia utente amministratore per la gestione delle impostazioni senza ridistribuzione.
- **Integrazione Storefront**: le stime delle date di consegna vengono visualizzate nella pagina dei dettagli del prodotto (PDP), nella pagina del carrello e nella pagina di pagamento tramite [!DNL Edge Delivery Services] componenti di rilascio e un modulo client condiviso.

>[!NOTE]
>
>Gli agenti di IA non sono deterministici. I prompt, le domande e gli output di questa esercitazione sono esempi. Il tuo agente può produrre domande, requisiti o proposte di architettura diversi. Utilizza gli esempi in questa esercitazione per indirizzare l’agente verso un risultato simile.

Prima di iniziare, completa i [prerequisiti](./tutorial-prerequisites.md). Questa esercitazione utilizza il **kit di avvio estrazione**. Verificare di averlo già clonato e di aver completato i passaggi di configurazione descritti nella pagina prerequisiti.

## Verificare i prerequisiti

Verifica che siano installati i seguenti prerequisiti:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

Se uno dei comandi precedenti non restituisce i risultati previsti, consultare i [prerequisiti](./tutorial-prerequisites.md).

Inoltre, verifica quanto segue:

- È presente un&#39;istanza [!DNL Adobe Commerce as a Cloud Service] con dati di prodotto. Consulta [Istanze del servizio Commerce Cloud](https://experienceleague.adobe.com/it/docs/commerce/cloud-service/overview){target="_blank"}.
- Si dispone di un progetto vetrina connesso all&#39;istanza [!DNL Commerce]. In caso contrario, seguire i passaggi descritti in [Creare una vetrina](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=it){target="_blank"}.
- CLI `aem` installato:

  ```bash
  npm install -g @adobe/aem-cli
  ```

- Hai un **account acquirente** — un cliente registrato in [!DNL Commerce] con un indirizzo di spedizione predefinito salvato. Le stime delle consegne sulle pagine PDP e Carrello vengono mostrate solo agli acquirenti registrati. Checkout mostra le stime per tutti gli acquirenti indipendentemente dallo stato di autenticazione.

>[!IMPORTANT]
>
>Questa esercitazione utilizza **Checkout Starter Kit** (non Integration Starter Kit). Il Checkout Starter Kit fornisce estensibilità basata su webhook per il pagamento, la spedizione, le imposte e gli eventi. Assicurati di avviare il sistema dal Checkout kit.

## Configurare l’API per la stima di consegna simulata

L’estensione richiama un’API esterna per la stima della consegna per ottenere le stime della data e dell’ora di spedizione. Per questo tutorial, utilizzi un’API fittizia per eseguire il flusso completo senza un account carrier reale. Sono disponibili due opzioni:

- **Opzione A: flusso di lavoro Pipedream** - Livello libero, configurazione rapida, ma con limiti di chiamata mensili.
- **Opzione B: azione App Builder Runtime** - Nessuna dipendenza esterna, creata durante i passaggi di sviluppo back-end.

>[!TIP]
>
>Durante lo sviluppo, è possibile iniziare con Pipedream (Opzione A) e passare a un&#39;azione Runtime (Opzione B) se si raggiunge la quota di chiamate di livello libero. Entrambe le opzioni implementano lo stesso contratto API.

### Specifica API

L’API fittizia accetta una richiesta POST e restituisce stime della data di consegna con vettore, giorni di transito, orario limite e una stima migliore.

**Corpo della richiesta** (tutti i campi sono facoltativi per il modello):

```json
{
  "origin": { "country_code": "US", "postal_code": "90210", "city": "Beverly Hills" },
  "destination": { "country_code": "US", "postal_code": "10001", "city": "New York" },
  "ship_date": "2026-03-10",
  "carriers": ["standard", "express"],
  "service_levels": ["standard", "express"]
}
```

**Risposta (200 OK):**

```json
{
  "estimates": [
    {
      "carrier_code": "standard",
      "service_code": "ground",
      "delivery_date": "2026-03-14",
      "safe_delivery_date": "2026-03-15",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-10T17:00:00.000Z"
    },
    {
      "carrier_code": "express",
      "service_code": "2day",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-12",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-10T12:00:00.000Z"
    }
  ],
  "best_estimation": { "carrier_code": "express", "delivery_date": "2026-03-12", "transit_days": 2 }
}
```

**Risposte di errore:** 401 (chiave API mancante/non valida), 400 (formato `ship_date` non valido), 503 (tempo di inattività simulato).

### Configurare il modello

>[!BEGINTABS]

>[!TAB Flusso di lavoro di reindirizzamento]

L’opzione Pipedream utilizza l’autenticazione del token Bearer e accetta una richiesta POST all’URL dell’attivatore del flusso di lavoro.

| Elemento | Descrizione |
|------|-------------|
| URL di base | L&#39;URL completo del trigger del flusso di lavoro Pipedream (ad esempio `https://<id>.m.pipedream.net`) |
| Auth | `Authorization: Bearer <API_KEY>` |
| Metodo | POST |

{style="table-layout:auto"}

**Crea il flusso di lavoro:**

1. Crea un nuovo flusso di lavoro in [Pipedream](https://pipedream.com){target="_blank"} (**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**).

1. Aggiungi un trigger **HTTP / Webhook** configurato per POST. Pipedream assegna un URL del webhook.

1. Aggiungi un passaggio **Esegui codice Node.js** e incolla il seguente codice del gestore:

   ```javascript
   const DEFAULT_CARRIERS = [
     { carrier_code: "standard", service_code: "ground", transit_days: 4 },
     { carrier_code: "express", service_code: "2day", transit_days: 2 },
     { carrier_code: "priority", service_code: "overnight", transit_days: 1 },
   ];
   
   const ISO_DATE = /^\d{4}-\d{2}-\d{2}$/;
   
   function parseShipDate(shipDate) {
     if (shipDate == null || typeof shipDate !== "string") return null;
     if (!ISO_DATE.test(shipDate)) return null;
     const d = new Date(shipDate + "T12:00:00.000Z");
     if (Number.isNaN(d.getTime())) return null;
     return shipDate;
   }
   
   function addBusinessDays(isoDate, days) {
     const d = new Date(isoDate + "T12:00:00.000Z");
     let added = 0;
     while (added < days) {
       d.setUTCDate(d.getUTCDate() + 1);
       const dow = d.getUTCDay();
       if (dow !== 0 && dow !== 6) added += 1;
     }
     return d.toISOString().slice(0, 10);
   }
   
   function cutoffUtc(isoDate, hour = 17) {
     return `${isoDate}T${String(hour).padStart(2, "0")}:00:00.000Z`;
   }
   
   function getBearerToken(headers) {
     const auth = headers?.Authorization ?? headers?.authorization ?? "";
     if (typeof auth !== "string" || !auth.startsWith("Bearer ")) return null;
     return auth.slice(7).trim() || null;
   }
   
   function handleDeliveryEstimate(body) {
     const shipDate = parseShipDate(body?.ship_date);
     const baseDate = shipDate ?? new Date().toISOString().slice(0, 10);
     let carriers = DEFAULT_CARRIERS;
     if (Array.isArray(body?.carriers) && body.carriers.length > 0) {
       const set = new Set(body.carriers.map((c) => String(c).toLowerCase()));
       carriers = DEFAULT_CARRIERS.filter((c) => set.has(c.carrier_code.toLowerCase()));
     }
     if (Array.isArray(body?.service_levels) && body.service_levels.length > 0) {
       const set = new Set(body.service_levels.map((s) => String(s).toLowerCase()));
       carriers = carriers.filter(
         (c) => set.has(c.service_code.toLowerCase()) || set.has(c.carrier_code.toLowerCase())
       );
     }
     if (carriers.length === 0) {
       return { status: 200, body: { estimates: [], best_estimation: null } };
     }
     const estimates = carriers.map((c) => {
       const delivery_date = addBusinessDays(baseDate, c.transit_days);
       const safe_delivery_date = addBusinessDays(baseDate, c.transit_days + 1);
       const cutoff_datetime_utc = cutoffUtc(baseDate, 17 - c.transit_days);
       return {
         carrier_code: c.carrier_code,
         service_code: c.service_code,
         delivery_date,
         safe_delivery_date,
         transit_days: c.transit_days,
         cutoff_datetime_utc,
       };
     });
     return { status: 200, body: { estimates, best_estimation: estimates[0] } };
   }
   
   export default defineComponent({
     async run({ steps, $ }) {
       const event = steps.trigger?.event ?? steps.trigger ?? {};
       const body = event.body ?? {};
       const headers = event.headers ?? {};
       const auth = getBearerToken(headers);
       const expectedKey =
         (typeof process.env.MOCK_API_KEY === "string" && process.env.MOCK_API_KEY.trim()) || null;
       if (expectedKey && (!auth || auth !== expectedKey)) {
         await $.respond({
           immediate: true,
           status: 401,
           headers: { "Content-Type": "application/json" },
           body: { error: "unauthorized", message: "Missing or invalid API key." },
         });
         return;
       }
       if (body?.ship_date != null && !parseShipDate(body.ship_date)) {
         await $.respond({
           immediate: true,
           status: 400,
           headers: { "Content-Type": "application/json" },
           body: { error: "bad_request", message: "Invalid ship_date; use YYYY-MM-DD." },
         });
         return;
       }
       const { status, body: responseBody } = handleDeliveryEstimate(body);
       await $.respond({
         immediate: true,
         status,
         headers: { "Content-Type": "application/json" },
         body: responseBody,
       });
     },
   });
   ```

1. (Facoltativo) Aggiungi una variabile di ambiente `MOCK_API_KEY` nelle impostazioni del flusso di lavoro per applicare l&#39;autenticazione del token Bearer. Se non viene impostata, viene accettata qualsiasi richiesta.

1. Distribuire il flusso di lavoro.

   L&#39;endpoint è l&#39;URL del trigger del webhook.

**Verifica il modello:**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB Azione App Builder Runtime]

L&#39;opzione di azione App Builder Runtime distribuisce il modello come azione Runtime all&#39;interno dello stesso progetto [!DNL App Builder]. Questo approccio non ha alcuna dipendenza esterna e nessuna quota di richiamo.

Chiedi all&#39;agente di creare l&#39;azione fittizia:

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- Add it to a separate package
- Use the code in docs/pipedream as inspiration
```

L&#39;agente crea `actions/mock-delivery-api/index.js` con lo stesso contratto API dell&#39;opzione Pipedream. Dopo la distribuzione, l’endpoint è:

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

Autenticazione convalidata per una variabile di ambiente `MOCK_API_KEY` in `.env`.

>[!ENDTABS]

## Sviluppo delle estensioni

Questa sezione ti guida attraverso lo sviluppo del backend [!DNL App Builder] per l&#39;estensione delle stime di consegna. Il backend fornisce tre azioni:

| Azione | Tipo | Finalità |
|--------|------|---------|
| `delivery-estimates` | Azione Web autonoma | BFF per vetrina: PDP e carrello chiamano per le date di consegna |
| `shipping-methods` | Azione webhook | Arricchisce le tariffe di spedizione con le date di consegna in `additional_data` al momento del pagamento |
| `delivery-estimates-config` | Azione back-end amministratore | CRUD per la configurazione archiviata in `aio-lib-state` |

{style="table-layout:auto"}

1. Dalle impostazioni MCP degli agenti di codifica, verificare che il set di strumenti `commerce-extensibility` sia abilitato senza errori.

   Ad esempio, in Cursore, vai a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

   Se vengono visualizzati degli errori, disattiva e attiva la serie di strumenti.

   >[!NOTE]
   >
   >Quando si lavora con strumenti di sviluppo assistiti da intelligenza artificiale, è probabile che il codice e le risposte generate dall’agente presentino variazioni naturali.
   >Se riscontri problemi con il codice, chiedi all&#39;agente di aiutarti a eseguirne il debug.

1. Se hai aggiunto della documentazione al contesto del cursore, disattivala.

   Passa a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** ed elimina la documentazione elencata.

### Passaggio 1: fornire il prompt iniziale

Assegna all’agente la specifica API esterna per il contesto e richiedi di iniziare. Dire all&#39;agente di fermarsi e porre domande ti aiuta a gestire l&#39;implementazione in anticipo.

Immetti il seguente prompt nella finestra di chat dell&#39;agente:

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date and time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
Implement this feature by using the skills in this workspace for backend code, and a separate workspace with storefront skills. For this extension, focus on the backend skills and create an API_SPEC to hand work over to the storefront skills.

STOP and ask me clarifying questions about the requirements before you do any work.
```

>[!TIP]
>
>Il riferimento al file delle specifiche API esterne (`@docs/API_SPEC.md`) nel prompt fornisce all&#39;agente un contesto concreto sul contratto API di terze parti. L’agente utilizza questa proprietà per progettare l’azione BFF, il client HTTP condiviso e i campi di configurazione dell’interfaccia utente amministratore. Dire all’agente di INTERROMPERE e porre domande attiva il flusso di lavoro guidato e ti aiuta a gestire l’implementazione in anticipo.

### Passaggio 2: Rispondere alle domande dell&#39;agente

L’agente restituisce una serie di domande chiarificatrici che riguardano argomenti come l’ambiente di destinazione (PaaS vs SaaS), l’ambito (azione BFF autonoma, arricchimento del webhook o entrambi), l’origine dell’indirizzo, la strategia di caching e le preferenze di test. Nell&#39;esempio seguente vengono illustrate domande e risposte tipiche. Il tuo agente può porre domande diverse, ma gli argomenti sono in genere gli stessi.

**Domande dell&#39;agente di esempio:**

1. **Ambiente di destinazione**: stai creando per PaaS (on-premise) o SaaS (Adobe Commerce as a Cloud Service)?
2. **Ambito**: questa deve essere un&#39;azione BFF autonoma (la vetrina la chiama direttamente), un arricchimento del webhook (estendere i metodi di spedizione al momento del pagamento) o entrambi?
3. **Configurabilità amministratore**: le impostazioni quali l&#39;URL API, la chiave API e l&#39;indirizzo di origine devono essere configurabili tramite l&#39;amministratore Commerce o archiviate in `.env`?
4. **Indirizzo di origine** - Da dove proviene l&#39;indirizzo di origine della spedizione (warehouse)? Deve trattarsi di una configurazione statica o risolta in modo dinamico?
5. **Memorizzazione in cache** — Le stime di consegna devono essere memorizzate nella cache lato server per ridurre le chiamate all&#39;API esterna? In caso affermativo, quale TTL?

**Risposte di esempio:**

```shell-session
Clarifications:
1. Let's build for SaaS
2. Let's do this:
(A) Can the PDP/cart call the 3rd party API directly — or are there any benefits of wrapping this call with a runtime action?
(B) Let's use the shipping-methods webhook
3. Let's use a Single-page application (SPA) that uses the Admin UI SDK to integrate with the admin. Since we are adding this config screen, let's make anything else that makes sense configurable to avoid redeployments when changing settings
4. Static configuration — origin address should be configurable in the Admin UI (e.g. warehouse address)
5. Yes, cache on the server side; suggest a TTL (e.g. 30 minutes) and make it configurable in the Admin UI
```

>[!TIP]
>
>Chiedere all’agente se la vetrina deve chiamare direttamente l’API di terze parti o eseguire un’azione di runtime attiva un’utile discussione sull’architettura. L’agente spiega i vantaggi del modello BFF (Backend-for-Frontend): la chiave API rimane lato server, CORS viene gestito, la memorizzazione nella cache è centralizzata e si ottiene l’astrazione del fornitore. Quando si richiede la configurabilità dell&#39;interfaccia utente amministratore, l&#39;agente viene invitato a memorizzare tutte le impostazioni in `aio-lib-state` anziché in `.env`, eliminando le ridistribuzioni durante la modifica delle impostazioni.

>[!NOTE]
>
>Il tuo agente potrebbe porre domande diverse. Utilizzare queste risposte come guida per indirizzare l&#39;agente verso lo stesso risultato funzionale: un&#39;azione BFF per le chiamate di storefront, un webhook dei metodi di spedizione per l&#39;arricchimento dell&#39;estrazione e una pagina di configurazione dell&#39;interfaccia utente amministratore che memorizza le impostazioni in `aio-lib-state`.

### Passaggio 3: verifica dei requisiti e dell’architettura

L&#39;agente genera i requisiti e i documenti dell&#39;architettura da esaminare. Verifica che i requisiti corrispondano alle risposte fornite e che l’architettura copra:

- Azione **BFF** (`delivery-estimates`): azione Web autonoma richiamata dalla vetrina dalle pagine PDP e carrello. Legge la configurazione da `aio-lib-state`, chiama l&#39;API per la stima della consegna esterna e restituisce stime formattate.
- **azione webhook** (`shipping-methods`): durante l&#39;estrazione le tariffe di spedizione vengono arricchite con date di consegna in `additional_data`. Utilizza il metodo webhook `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates`.
- **Azione di configurazione amministratore** (`delivery-estimates-config`): CRUD per la configurazione (URL API, chiave API, indirizzo di origine, gestori, TTL della cache) archiviata in `aio-lib-state`.
- **Librerie condivise**: client HTTP per l&#39;API esterna e modulo di configurazione per la lettura e la scrittura di `aio-lib-state`.

>[!NOTE]
>
>Gli agenti di IA non sono deterministici e i loro comportamenti variano a seconda del modello e dell’IDE. È possibile che vengano visualizzate domande diverse che producono un diverso insieme di requisiti e architettura. In tal caso, prima di procedere, prova a dirigere l’agente in una direzione tale che l’implementazione corrisponda strettamente a quanto illustrato in questa esercitazione.

### Passaggio 4: selezionare un piano di implementazione

L’agente ti offre la possibilità di creare un piano di implementazione dettagliato o di completare un’implementazione diretta.

- Se si desidera un piano revisionabile che può essere eseguito in fasi con maggiore controllo, selezionare la prima opzione.
- Se desideri che l&#39;agente esegua l&#39;implementazione completa con un intervento minimo, seleziona la seconda opzione.

### Passaggio 5: pulire e distribuire

Una volta completata l’implementazione, l’agente procede con la pulizia. Poiché è in uso solo il dominio di spedizione, l’agente rimuove lo scaffolding non utilizzato:

- Azioni di pagamento e configurazione (`validate-payment/`, `filter-payment/`, `payment-methods.yaml`)
- Azioni fiscali e configurazione (`collect-taxes/`, `collect-adjustment-taxes/`, `tax-integrations.yaml`)
- Azioni eventi e configurazione (`commerce-events/`, `3rd-party-events/`, `events.config.yaml`)
- Scaffolding generico (`generic/`)
- Componenti per applicazioni a pagina singola dell’interfaccia di amministrazione da altri domini (ad esempio, pagine e hook relativi alle imposte)
- Script, file di test e variabili di ambiente non utilizzati

>[!TIP]
>
>Chiedi all’agente di controllare anche l’applicazione a pagina singola dell’interfaccia utente amministratore per individuare eventuali elementi rimanenti di altri domini. La pagina Classi imposta e i relativi hook potrebbero essere ancora presenti dallo scaffolding del kit di avvio e devono essere rimossi.

Dopo la pulizia, distribuire utilizzando i passaggi seguenti **in questo ordine**:

```bash
# 1. Copy env template and fill in credentials.
cp env.dist .env

# 2. Select your App Builder workspace.
aio app use --merge

# 3. Sync OAuth credentials from workspace.
npm run sync-oauth-credentials

# 4. Deploy the extension.
aio app deploy

# 5. Register shipping carriers in Commerce.
npm run create-shipping-carriers
```

>[!IMPORTANT]
>
>Non saltare o riordinare i passaggi. I passaggi 1-3 sono prerequisiti per la distribuzione. Il comando `aio app deploy` ha esito negativo se non sono state configurate credenziali.

### Passaggio 6: configurare il webhook e l’interfaccia utente amministratore

Dopo la distribuzione, configura il webhook di spedizione. L&#39;agente può creare uno script per eseguire la sottoscrizione a livello di programmazione:

```bash
npm run subscribe-webhook
```

Con questo comando viene eseguito l&#39;abbonamento al webhook di spedizione con le impostazioni seguenti:

| Campo | Valore |
|-------|-------|
| Webhook, metodo | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Tipo di webhook | `after` |
| Obbligatorio | Facoltativo (consente il fallback alla spedizione predefinita) |
| Timeout | 5000 ms |

{style="table-layout:auto"}

>[!NOTE]
>
>Per SaaS, il nome del metodo webhook elimina `magento.` dal percorso. Il nome del webhook per PaaS è `plugin.magento.out_of_process_shipping_methods...`, mentre il nome del webhook per SaaS è `plugin.out_of_process_shipping_methods...`.

Quindi, configura l’interfaccia utente di amministrazione:

1. Abilita **Interfaccia utente amministratore SDK** (**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL Admin UI SDK]** > **[!UICONTROL Enable]** > **[!UICONTROL Yes]**).

1. Configurare le estensioni selezionando l&#39;area di lavoro e l&#39;estensione [!DNL App Builder].

1. Fare clic su **[!UICONTROL Refresh registrations]**.

1. Passa a **[!UICONTROL Apps]** > **[!UICONTROL Delivery Estimates]** nella barra laterale [!DNL Admin].

1. Completa la configurazione abilitando la funzione e specificando le impostazioni richieste, tra cui l’URL API e la chiave API, l’indirizzo di origine, i gestori predefiniti, il TTL della cache e le mappature del codice del gestore.

### Passaggio 7: testare l’estensione

Testare direttamente l’azione BFF delle stime di consegna:

```bash
curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-runtime-url>/api/v1/web/commerce-checkout-starter-kit/delivery-estimates" | jq .
```

La risposta dovrebbe essere simile a:

```json
{
  "estimates": [
    {
      "carrier": "standard",
      "service_level": "ground",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-13",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-06T18:00:00Z"
    },
    {
      "carrier": "express",
      "service_level": "2day",
      "delivery_date": "2026-03-10",
      "safe_delivery_date": "2026-03-10",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-06T20:00:00Z"
    }
  ],
  "best_estimation": {
    "carrier": "express",
    "delivery_date": "2026-03-10",
    "transit_days": 2
  }
}
```

### Crea il contratto di assistenza

Una volta completato il backend, chiedere all&#39;agente di creare un contratto di assistenza per il lavoro della vetrina:

```shell-session
Produce a spec called STOREFRONT_API_SPEC that I can use in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

L&#39;agente genera `docs/STOREFRONT_API_SPEC.md` con il contratto completo dell&#39;endpoint BFF (formato di richiesta e risposta, payload di esempio, gestione degli errori) e un prompt pronto all&#39;uso per l&#39;area di lavoro vetrina.

Copia questo file nel progetto storefront prima di avviare i passaggi di sviluppo per storefront.

>[!TIP]
>
>Se l&#39;agente genera sia un contratto di assistenza **che**, viene visualizzato un messaggio di richiesta per l&#39;altra area di lavoro, il passaggio tra il team backend e il team storefront (o gli agenti) sarà corretto. L’agente storefront può iniziare a funzionare immediatamente senza dover porre domande sull’API.

## Connetti alla vetrina

Questa sezione ti guida attraverso l&#39;implementazione della parte storefront dell&#39;estensione delle stime di consegna tramite [!DNL Edge Delivery Services] e strumenti di sviluppo assistiti da AI. Puoi aggiungere stime della data di consegna alla pagina PDP, al carrello e alla pagina di pagamento.

>[!NOTE]
>
>I prompt forniti sono punti di partenza. Anche se puoi utilizzarli senza modifiche, puoi considerare di parlare naturalmente con l&#39;agente.
>
>Quando si lavora con strumenti di sviluppo assistiti da intelligenza artificiale, il codice e le risposte generate dall’agente hanno sempre varianti naturali.
>
>Se riscontri problemi con il codice, chiedi all&#39;agente di aiutarti a eseguirne il debug.

### Prerequisiti per la vetrina

Prima di avviare l’integrazione con la vetrina, verifica di disporre dei seguenti elementi:

- Progetto vetrina connesso all&#39;istanza [!DNL Commerce]
- Strumenti di intelligenza artificiale per vetrina Commerce [installati utilizzando CLI](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- Il file `STOREFRONT_API_SPEC.md` copiato nella cartella `docs/` del progetto storefront

### Passaggio 1: Convalidare l’ambiente

Apri il file `config.json` e verifica che i valori per `commerce-core-endpoint` e `commerce-endpoint` puntino all&#39;endpoint GraphQL [!DNL Adobe Commerce as a Cloud Service].

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Passaggio 2: specificare il prompt iniziale

Con il contratto di servizio già presente nel progetto, richiedi all’agente di implementare l’integrazione storefront. Utilizza la modalità **Piano**, se disponibile nell&#39;agente, per impedire che l&#39;agente proceda senza un piano.

```shell-session
I need to implement delivery date estimates on the storefront for an Adobe Commerce (SaaS) store using Edge Delivery Services with storefront drop-ins. The backend is already built and deployed as an App Builder extension.

The full integration contract is in the `docs/STOREFRONT_API_SPEC.md` file— please read it first. It covers two integration points:

PDP and Cart pages — Call the delivery-estimates BFF action (HTTP POST) to fetch estimates for a destination and display the best delivery date.

Checkout shipping step — Delivery dates are already injected into each shipping method's `additional_data` by a webhook. No API call is needed. Just read `additional_data` from the shipping methods and display the delivery date next to each option.

Requirements:
- Show "Get it by [date]" on PDP using best_estimation.delivery_date
- Show a delivery date range on the cart page using delivery_date / safe_delivery_date
- Show delivery dates next to each shipping method at checkout, reading from additional_data
- Show "Order within X hours" countdown using cutoff_datetime_utc where appropriate
- Cache estimates client-side in sessionStorage to avoid redundant calls
- Never block the purchase flow — if estimates are unavailable, hide the UI silently

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>Il prompt è dettagliato perché il contratto API completo è già disponibile dall’agente back-end. Facendo riferimento a `@docs/STOREFRONT_API_SPEC.md`, l&#39;agente conosce l&#39;URL esatto dell&#39;endpoint, il formato di richiesta e risposta e la gestione degli errori. L&#39;elenco dei requisiti espliciti impedisce all&#39;agente di inventare l&#39;ambito. In particolare, la richiesta della modalità di piano attiva il flusso di lavoro graduale che consente di gestire l’implementazione in anticipo.

### Passaggio 3: rispondere alle domande più chiare

L’agente restituisce domande sull’ambito di autenticazione, sull’approccio al pagamento e sullo stile. Nell&#39;esempio seguente vengono illustrate domande e risposte tipiche.

**Domande dell&#39;agente di esempio:**

1. **Utenti anonimi rispetto a quelli connessi**: le stime devono essere visualizzate nelle pagine PDP e Carrello per tutti gli acquirenti o solo per quelli autenticati?
2. **Approccio all&#39;estrazione**: il contenitore a discesa ShippingMethods non espone `additional_data`, pertanto l&#39;agente propone due opzioni:
   - **Opzione A:** Chiamare il file BFF alle date di consegna per l&#39;inserimento del DOM (più semplice, coerente con PDP/Cart)
   - **Opzione B:** Estendere il frammento GraphQL di estrazione tramite `overrideGQLOperations` per includere `additional_data`
3. **Stile**: token di progettazione Emojis e esistenti

**Risposte di esempio:**

```shell-session
1. Only for logged-in users — that way we can use the shopper's default shipping address and avoid a zip code input
2. Let's do Option A if feasible
3. Use anything that matches the current styling
```

>[!TIP]
>
>Mostrare stime solo per gli acquirenti registrati è una scelta pragmatica. L’agente può utilizzare automaticamente l’indirizzo di spedizione predefinito del cliente (tramite GraphQL), pertanto non è necessario inserire alcun codice postale. Gli acquirenti anonimi su PDP e Cart richiederebbero l’immissione di un codice postale, il che aggiunge attrito. Al momento del pagamento, tutti gli acquirenti visualizzano le date di consegna perché l&#39;indirizzo di spedizione è già stato inserito.

>[!NOTE]
>
>Il tuo agente potrebbe porre domande diverse. Utilizza queste risposte come guida:
>
>- Visualizza le stime PDP e Carrello solo per gli acquirenti che hanno effettuato l’accesso (non è necessario alcun input di codice postale).
>- Per il pagamento, utilizza l’opzione A (chiamata BFF + iniezione DOM) per semplicità.
>- Utilizza i token di progettazione esistenti per lo stile.

### Passaggio 4: verifica dei requisiti e dell’architettura

L’agente progetta un’architettura di moduli condivisi. Verifica che copra:

| Componente | Finalità |
|-----------|---------|
| `scripts/delivery-estimates.js` | Modulo condiviso: client BFF, caching (sessionStorage, TTL 30 minuti), formattazione della data, logica di conto alla rovescia, ricerca dell’indirizzo del cliente, mappatura del gestore |
| Integrazione PDP | Visualizza &quot;Ottienila entro [data]&quot; con conto alla rovescia facoltativo tra prezzo e descrizione |
| Integrazione del carrello | Visualizza l’intervallo di date (&quot;Gio, 12 marzo - Ven, 13 marzo&quot;) nella colonna destra sopra il riepilogo dell’ordine |
| Integrazione cassa | Chiama BFF quando il passaggio di spedizione è attivo, DOM inserisce le date di consegna tramite `MutationObserver` |

{style="table-layout:auto"}

Decisioni chiave in materia di progettazione da verificare:

- Tutte le chiamate BFF non sono di blocco: le pagine vengono visualizzate per prime, le stime vengono visualizzate in modo asincrono.
- Tutti gli errori sono invisibili all&#39;utente: solo `console.debug`, nessun errore relativo all&#39;acquirente.
- `CARRIER_MAP` mappa i codici vettore Commerce (DPS, Fedex) ai codici vettore BFF (standard, express).
- `import()` dinamico mantiene il modulo di consegna fuori dal percorso di rendering critico.

>[!NOTE]
>
>Gli agenti di IA non sono deterministici e i loro comportamenti variano a seconda del modello e dell’IDE. È possibile che vengano visualizzate domande diverse che producono un diverso insieme di requisiti e architettura. In tal caso, prima di procedere, prova a dirigere l’agente in una direzione tale che l’implementazione corrisponda strettamente a quanto illustrato in questa esercitazione.

### Passaggio 5: selezionare un piano di implementazione

L’agente ti offre la possibilità di creare un piano di implementazione dettagliato o di completare un’implementazione diretta.

- Se si desidera un piano revisionabile che può essere eseguito in fasi con maggiore controllo, selezionare la prima opzione.
- Se desideri che l&#39;agente esegua l&#39;implementazione completa con un intervento minimo, seleziona la seconda opzione.

Durante l’implementazione, l’agente crea e modifica i seguenti file:

**Nuovo file:**

- `scripts/delivery-estimates.js` — Modulo condiviso con `fetchDeliveryEstimates()`, `getCustomerShippingAddress()`, `formatDeliveryDate()`, `buildCountdownText()`, `findEstimateForCarrier()`

**File modificati:**

- `blocks/product-details/product-details.js` + `.css` — Div della stima di consegna nella colonna di destra, recupero asincrono dopo il rendering principale
- `blocks/commerce-cart/commerce-cart.js` + `.css` — Div stima consegna superiore al riepilogo ordine
- `blocks/commerce-checkout/commerce-checkout.js`, `containers.js`, `.css` — Iniezione DOM basata su `MutationObserver` per le etichette del metodo di spedizione

Guarda il codice generato e fai domande o reindirizza l’agente secondo necessità.

### Passaggio 6: avviare il server e testare

Dopo che l’agente ha completato l’implementazione, avvia il server di sviluppo e verifica le stime di consegna.

1. Avvia il server di sviluppo locale:

   ```bash
   npm run start
   ```

1. In un browser, accedi al tuo account acquirente.

   Le stime di consegna su PDP e Carrello richiedono una sessione autenticata con un indirizzo di spedizione predefinito salvato.

1. Passa a una pagina di prodotto e verifica i seguenti risultati:

   | Pagina | Risultato previsto | Autenticazione richiesta |
   |------|-----------------|---------------|
   | PDP | &quot;Entro giovedì 12 marzo&quot; con conto alla rovescia opzionale | Sì (solo accesso) |
   | Carrello | &quot;Consegna stimata: giovedì 12 marzo - venerdì 13 marzo&quot; | Sì (solo accesso) |
   | Pagamento | &quot;Consegna stimata: giovedì 12 marzo&quot; per metodo di spedizione | No (indirizzo immesso al momento del pagamento) |

   {style="table-layout:auto"}

>[!NOTE]
>
>I metodi di spedizione senza un vettore corrispondente (ad esempio, Tariffa fissa) non mostrano alcuna stima. Questo è per progettazione: solo i gestori mappati in `CARRIER_MAP` ottengono le date di consegna.

Puoi eseguire test manuali o chiedere all’agente di utilizzare le funzionalità del browser per eseguire test per tuo conto:

```shell-session
Run complete browser testing using the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### Passaggio 7: Pulire

Dopo aver saltato o completato il test, l&#39;agente ti chiede di procedere con la pulizia. Una volta confermata, l’agente archivia tutti gli artefatti della documentazione prodotti durante l’implementazione.

## Risoluzione dei problemi

Se riscontri dei problemi durante l’esercitazione, utilizza i seguenti suggerimenti.

### Back-end (App Builder)

| Sintomo | Causa | Correzione |
|---------|-------|-----|
| L&#39;azione di configurazione dell&#39;interfaccia utente di amministrazione restituisce `400 Bad Request` con &quot;La richiesta definisce parametri non consentiti (proprietà riservate)&quot; | L&#39;hook front-end invia `__ow_method` nel corpo della richiesta. Le proprietà con prefisso `__ow_` sono riservate da OpenWhisk e rifiutate quando l&#39;azione ha `final: true`. | Invia una proprietà `method` personalizzata invece di `__ow_method`. L&#39;azione di backend legge prima `params.method`, quindi torna a `params.__ow_method` (fornito automaticamente da Runtime). |
| `aio app deploy` ha esito negativo con &quot;maxVersion è obbligatorio in productDependencies&quot; | La convalida CLI richiede sia `minVersion` che `maxVersion` in `app.config.yaml` dipendenze prodotto. | Aggiungere un valore `maxVersion` a ogni voce `productDependencies` in `app.config.yaml`. |
| Comando di distribuzione non riuscito | Credenziali non configurate prima della distribuzione. `.env`, la selezione dell&#39;area di lavoro e la sincronizzazione OAuth devono essere eseguite per prime. | Segui l&#39;ordine corretto: `cp env.dist .env` > `aio app use --merge` > `npm run sync-oauth-credentials` > `aio app deploy`. |

{style="table-layout:auto"}

### Vetrina (Edge Delivery Services)

| Sintomo | Causa | Correzione |
|---------|-------|-----|
| La stima della consegna PDP non viene visualizzata per gli acquirenti connessi | Il blocco PDP non inizializza l&#39;eliminazione di `account`, pertanto `getCustomerAddress()` non riesce in modo invisibile all&#39;utente e non viene recuperata alcuna stima. | Utilizza `CORE_FETCH_GRAPHQL.fetchGraphQl()` direttamente per eseguire query sugli indirizzi dell&#39;acquirente invece di affidarti all&#39;API di rilascio dell&#39;account. Funziona su qualsiasi pagina. |
| Il PDP non viene ancora visualizzato dopo la correzione di GraphQL | È stato utilizzato un errore di battitura nel nome del metodo: `CORE_FETCH_GRAPHQL.fetch()` invece di `CORE_FETCH_GRAPHQL.fetchGraphQl()`. | Utilizzare il nome di metodo corretto: `fetchGraphQl` (Q maiuscola, l minuscola). |
| Le date di consegna del pagamento non vengono visualizzate al primo caricamento | Il listener di eventi `checkout/updated` è stato registrato dopo l&#39;attivazione di `checkout/initialized`, quindi i dati iniziali non sono stati rilevati. | Aggiungere un listener `checkout/initialized` con `{ eager: true }` per rilevare gli eventi emessi prima della registrazione. Mantieni il listener `checkout/updated` per le modifiche successive. |
| La stima della consegna al carrello non viene visualizzata | `block.appendChild(fragment)` sposta tutti gli elementi secondari fuori dal frammento, quindi `fragment.querySelector('.cart__delivery-estimate')` restituisce null. | Query da `block` anziché `fragment` dopo l&#39;operazione di accodamento. |
| La spedizione con tariffa fissa non mostra alcuna data di consegna al momento del pagamento | Per progettazione: `CARRIER_MAP` associa solo DPS a standard e Fedex a express. La tariffa fissa non ha un gestore corrispondente nell’API esterna. | Non è un bug. Per aggiungere stime per altri gestori, estendere `CARRIER_MAP` in `scripts/delivery-estimates.js` e configurare il gestore nell&#39;estensione back-end. |

{style="table-layout:auto"}

### Sandbox SaaS Commerce

| Sintomo | Causa | Correzione |
|---------|-------|-----|
| Webhook restituisce `429 Too Many Requests` | L&#39;area di lavoro [!DNL App Builder] è in modalità di debug, con limiti di frequenza al minuto rigidi. [!DNL Commerce] ricalcola frequentemente le tariffe di spedizione durante il pagamento, esaurendo la quota. | Distribuire in un&#39;area di lavoro di produzione (`aio app use` per passare, quindi `aio app deploy`). Le aree di lavoro di produzione non dispongono di limiti di velocità di debug. |
| Avviso di timeout soft di Webhook (>1000 ms) | L&#39;azione del webhook dei metodi di spedizione ha richiesto più tempo del timeout soft di [!DNL Commerce] 1000 ms. | Abilitare il caching lato server in `aio-lib-state` in modo più aggressivo o aumentare il timeout del webhook in [!DNL Commerce Admin] (configurazione dei webhook Commerce). |

{style="table-layout:auto"}

## Riepilogo esercitazione

Di seguito è riportato un riepilogo degli argomenti trattati in questa esercitazione:

- **Configurazione API fittizia:** Creazione di un&#39;API simulazione per la stima di consegna tramite Pipedream o un&#39;azione di runtime [!DNL App Builder].
- **Modello BFF:** creazione di un&#39;azione back-end-for-frontend che racchiude l&#39;API esterna, mantiene le credenziali lato server e centralizza la memorizzazione nella cache.
- **Arricchimento webhook:** estensione del webhook dei metodi di spedizione per inserire le date di consegna in ogni opzione di spedizione al momento del pagamento.
- **Configurabilità interfaccia utente amministratore:** Aggiunta di una pagina di configurazione utilizzando [!DNL Admin UI SDK] per consentire ai commercianti di gestire le impostazioni API, l&#39;indirizzo di origine e le mappature dei gestori senza ridistribuzione.
- **Contratti di servizio:** creazione di contratti API che collegano estensioni back-end e implementazioni storefront.
- **Integrazione con Storefront:** visualizzazione delle stime di consegna in PDP (&quot;Ottienila entro&quot;), carrello (intervallo di date) e pagamento (per metodo di spedizione) tramite un modulo client condiviso.
- **UX non bloccante:** assicurandosi che le stime di consegna non blocchino mai il flusso di acquisto. Le pagine vengono visualizzate per prime e le stime vengono visualizzate in modo asincrono.

## Passaggi successivi

Utilizza i seguenti suggerimenti per estendere il servizio di stime della consegna:

- **Connetti un&#39;API vettore reale:** Sostituisci il simulatore con un&#39;API di spedizione live come UPS, FedEx o USPS modificando l&#39;URL del servizio e la chiave API in [!DNL Admin UI].
- **Supporta acquirenti anonimi:** Aggiungi un codice postale inserito nelle pagine PDP e cart in modo che anche gli acquirenti non connessi possano vedere le stime di consegna.
- **Estendi mappature vettore:** Aggiungi altri codici vettore a `CARRIER_MAP` per visualizzare le date di consegna per metodi di spedizione aggiuntivi.
- **Aggiungi caching lato server:** Implementa il caching `aio-lib-state` nell&#39;azione BFF per ridurre le chiamate all&#39;API esterna per coppie di origine e destinazione ripetute.
- **Mostra le stime nella conferma dell&#39;ordine:** Visualizza la data di consegna stimata nella pagina di conferma dell&#39;ordine e nelle e-mail transazionali.
