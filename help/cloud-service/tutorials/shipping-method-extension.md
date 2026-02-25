---
title: Esercitazione sull’estensione del metodo di spedizione
description: Scopri come creare un’estensione del metodo di spedizione configurabile per Adobe Commerce as a Cloud Service utilizzando App Builder, il kit di avvio per il pagamento e strumenti di sviluppo assistiti da AI.
feature: App Builder, Cloud
role: Developer
level: Intermediate
source-git-commit: e55bc4db196d3d973b981bb2484be950dcd6b7c3
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 0%

---

# Esercitazione sull’estensione del metodo di spedizione

Questa esercitazione ti guida attraverso la creazione di un&#39;estensione del metodo di spedizione per [!DNL Adobe Commerce as a Cloud Service] utilizzando [!DNL Adobe App Builder], il [kit di avvio per l&#39;estrazione](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} e strumenti di sviluppo assistiti da IA.

L&#39;estensione aggiunge un metodo di spedizione configurabile al momento del pagamento, in cui le tariffe provengono da un servizio di tariffe di spedizione fittizie esterno. Gli esercenti configurano l’URL del servizio, la chiave API e l’indirizzo del magazzino (di partenza) nell’interfaccia utente di amministrazione, al momento del pagamento della tariffa per le richieste di estensione da parte del servizio e visualizzano al cliente le opzioni restituite.

Prima di iniziare, completa i [prerequisiti](./tutorial-prerequisites.md).

## Verificare i prerequisiti {#tutorial-verify-prerequisites}

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

## Creare l’API delle tariffe di spedizione fittizie

Dopo aver completato i [prerequisiti](./tutorial-prerequisites.md), crea l&#39;API delle tariffe di spedizione fittizie in modo da disporre dell&#39;URL del servizio e della chiave API quando configuri l&#39;estensione in [!DNL Commerce Admin]. L’estensione richiama un’API per le tariffe di spedizione esterne. Per questo tutorial utilizzi una finta API che ti consente di eseguire il flusso senza un account di gestore reale. Creerai l&#39;API fittizia utilizzando [Pipedream](https://pipedream.com) (è richiesto un account gratuito). L’API fittizia utilizza un contratto di richiesta/risposta simile alle normali API delle tariffe di spedizione reali, pertanto collegare questa estensione a un fornitore reale in un secondo momento dovrebbe essere semplice.

Per creare l&#39;API fittizia, scarica il file delle specifiche API delle [tariffe fittizie](../assets/mock-rates-api-spec.zip), aprilo e aggiungi il file `.md` al progetto (ad esempio `docs/mock-rates-api-spec.md`).

**Tempo:** La creazione dell&#39;API fittizia dovrebbe richiedere circa **5-10 minuti**.

### Creare un flusso di lavoro e un trigger HTTP

1. Vai a [pipedream.com](https://pipedream.com) e accedi.
1. Fai clic su **Nuovo flusso di lavoro** (o **Aggiungi flusso di lavoro**).
1. Per il trigger, selezionare **HTTP / Webhook**.
1. Nella configurazione del trigger, imposta **Risposta HTTP** su **Restituire una risposta personalizzata dal flusso di lavoro**. Questo consente al passaggio Codice di inviare la risposta JSON fittizia.
1. Pipedream visualizza un **URL endpoint HTTP** univoco, ad esempio `https://123456.m.pipedream.net`.
1. **Copia questo URL** e utilizzalo come **URL servizio** durante la configurazione dell&#39;estensione in Amministrazione Commerce.

   ![Flusso di lavoro Pipedream con trigger HTTP/Webhook e URL endpoint visibile](../assets/mock-api-trigger.png){width="600" zoomable="yes"}

Non è necessario configurare **Authorization** sul trigger; l&#39;API fittizia convalida l&#39;intestazione `API-Key` nel passaggio del codice.

### Aggiungi il passaggio Codice

1. Fai clic sull&#39;icona **+** per aggiungere un passaggio.
1. Scegli **Esegui codice Node.js** (passaggio codice).
1. **Sostituisci** il codice predefinito con il seguente JavaScript.

   ```javascript
   export default defineComponent({
   async run({ steps, $ }) {
      const event = steps.trigger.event;
      const body = event.body ?? {};
      const headers = event.headers ?? {};
      const apiKey = headers["api-key"] ?? body.api_key ?? "";
   
      if (!apiKey || String(apiKey).trim() === "") {
         await $.respond({
         immediate: true,
         status: 401,
         headers: { "Content-Type": "application/json" },
         body: { error: "Missing or invalid API-Key header" },
         });
         return;
      }
   
      const shipment = body.shipment;
      if (!shipment || typeof shipment !== "object") {
         await $.respond({
         immediate: true,
         status: 400,
         headers: { "Content-Type": "application/json" },
         body: { error: "Missing or invalid shipment" },
         });
         return;
      }
   
      const rates = [
         {
         service_code: "mock_standard",
         service_name: "Mock Standard",
         carrier_friendly_name: "Mock Carrier",
         shipping_amount: { amount: 5.99 },
         shipment_cost: 5.99,
         cost: 5.99,
         },
         {
         service_code: "mock_express",
         service_name: "Mock Express",
         carrier_friendly_name: "Mock Carrier",
         shipping_amount: { amount: 12.99 },
         shipment_cost: 12.99,
         cost: 12.99,
         },
      ];
   
      await $.respond({
         immediate: true,
         status: 200,
         headers: { "Content-Type": "application/json" },
         body: { rates },
      });
   },
   });
   ```

1. Fare clic su **Distribuisci**.

   ![Passaggio del codice Pipedream con script fittizio per le tariffe di spedizione](../assets/mock-api-code-step.png){width="600" zoomable="yes"}

Il modello restituisce due opzioni di tasso (Mock Standard e Mock Express) per qualsiasi richiesta valida che includa un&#39;intestazione `API-Key` non vuota e un oggetto `shipment`. La chiave API verrà configurata in [!DNL Commerce Admin] più avanti in questa esercitazione. Puoi anche specificare l’URL del flusso di lavoro Pipedream nella stessa schermata di configurazione, quindi prendi nota.

## Sviluppo delle estensioni

Questa sezione descrive come sviluppare un&#39;estensione del metodo di spedizione per [!DNL Adobe Commerce as a Cloud Service] utilizzando [il kit di avvio per l&#39;estrazione](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} e gli strumenti di sviluppo assistiti da IA.

1. Passa alle impostazioni MCP nell’agente di codifica. Ad esempio, in Cursore, vai a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**. Verificare che il set di strumenti `commerce-extensibility` sia abilitato senza errori. Se vengono visualizzati degli errori, disattiva e attiva la serie di strumenti.

   ![Impostazioni IDE cursore che mostrano il set di strumenti di estendibilità e commerce MCP abilitato](../assets/cursor-settings-shipping.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Quando si lavora con strumenti di sviluppo assistiti da intelligenza artificiale, è probabile che il codice e le risposte generate dall’agente presentino variazioni naturali.
   >
   >In caso di problemi con il codice, puoi sempre chiedere all&#39;agente di aiutarti a eseguire il debug.

1. Se hai aggiunto della documentazione al contesto del cursore, disattivala. Passa a [!UICONTROL **Cursore**] > [!UICONTROL **Impostazioni**] > [!UICONTROL **Impostazioni cursore**] > [!UICONTROL **Indicizzazione e documenti**] ed elimina la documentazione elencata.

   ![L&#39;indicizzazione del cursore e le impostazioni dei documenti con l&#39;elenco della documentazione sono vuoti](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Concedi all’agente l’accesso alle specifiche API delle tariffe fittizie in modo che possa implementare correttamente il client. Se non lo hai già fatto, scarica il file delle specifiche API delle [tariffe fittizie](../assets/mock-rates-api-spec.zip), aprilo e aggiungi il file `.md` al progetto (ad esempio `docs/mock-rates-api-spec.md`), quindi fai riferimento a tale file nel prompt.

1. Genera l&#39;estensione del metodo di spedizione:

   - Dalla finestra di chat dell&#39;agente, selezionare la modalità **Piano**, se disponibile. Questo impedisce all&#39;agente di procedere senza un piano.
   - Immetti il seguente prompt:

   ```shell-session
   Build an Adobe Commerce extension that adds a shipping method at checkout. The rates come from an external mock shipping rates service: the merchant configures the service's URL and API key in Admin, and at checkout the extension asks that service for rates and shows the returned options to the customer.
   
   External service (mock shipping rates API):
   - The service endpoint URL is configurable by the merchant (for example https://123456.m.pipedream.net).
   - The API is specified in ./docs/mock-rates-api-spec.md.
   
   The merchant must be able to configure the following in the Adobe Commerce Admin UI. Use the Adobe Commerce Admin UI SDK (or equivalent App Builder extensibility options for the Admin) to add a configuration screen where the merchant can set:
   - The service URL (where the extension sends rate requests).
   - An API key the service expects (any non-empty value for the mock). The API key is sensitive data: it must be stored securely and must never appear in logs, error messages, or in the UI in full (e.g. mask in the UI).
   - The warehouse (ship-from) address: name, phone, street, city, state, postal code, country. This is the origin used when requesting rates.
   ```

   >[!NOTE]
   >
   >Se l’agente richiede di cercare nella documentazione, consenti.

   ![Finestra di chat del cursore in modalità agente con richiesta di estensione di spedizione immessa](../assets/enter-prompt-shipping.png){width="600" zoomable="yes"}

1. Rispondi alle domande dell&#39;agente esattamente per aiutarlo a generare il codice migliore. Se l&#39;agente richiede quale kit o modello utilizzare, indirizzarlo al [kit di avvio per l&#39;estrazione](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} con il dominio di spedizione e l&#39;estensione SDK dell&#39;interfaccia utente amministratore in modo che sia il webhook di spedizione che la schermata di configurazione del commerciante siano implementati.

   L&#39;agente può creare un file `requirements.md` (o equivalente) che funge da fonte di verità per l&#39;implementazione.

1. Esaminare il file `requirements.md` (o equivalente) e verificare il piano. Se tutto sembra corretto, indicare all&#39;agente di passare alla pianificazione dell&#39;architettura (o **Fase 2**). Conferma che:

   - Un&#39;azione **shipping-methods** (o equivalente) gestisce il webhook Commerce e chiama l&#39;API delle tariffe esterne.
   - Un&#39;azione **shipping-config** (o equivalente) supporta GET (read config, API key masked) e SET (save service URL, API key, warehouse address), con la configurazione archiviata in modo sicuro, ad esempio nello stato di runtime.
   - L&#39;interfaccia utente amministratore include una scheda **Spedizione fittizia** (o simile) con campi per URL servizio, chiave API (password/mascherata) e indirizzo warehouse.

   ![File dei requisiti creato dall&#39;agente di IA con i dettagli di implementazione dell&#39;estensione di spedizione](../assets/requirements-file-shipping.png){width="600" zoomable="yes"}

1. Rivedi il piano dell’architettura quando l’agente lo fornisce.

   ![Piano di implementazione dell&#39;agente AI per l&#39;estensione delle tariffe di spedizione fittizie](../assets/implementation-plan-shipping.png){width="600" zoomable="yes"}

1. Indica all&#39;agente di procedere con la generazione del codice. L&#39;agente deve aggiungere un gestore **fittizio** alla configurazione dei gestori di spedizione che consenta a Commerce di accettare i metodi restituiti e utilizzare il metodo webhook `plugin.magento.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` (tipo webhook **dopo**, richiesto **facoltativo**).

   L’agente genera il codice necessario e fornisce un riepilogo dettagliato dei passaggi successivi (tra cui l’installazione delle dipendenze, la registrazione del vettore fittizio, la configurazione del webhook di Commerce e la distribuzione).

   ![Riepilogo del codice generato e dell&#39;implementazione per l&#39;estensione di spedizione](../assets/code-generation-summary-shipping.png){width="600" zoomable="yes"}

   ![Passaggi successivi dell&#39;agente AI per l&#39;installazione, la configurazione del webhook e la distribuzione dell&#39;estensione di spedizione](../assets/next-steps-shipping.png){width="600" zoomable="yes"}

### Pulizia prima della distribuzione

Prima della distribuzione, rimuovi il codice non necessario per l’applicazione. Il kit di avvio per il pagamento può includere domini non utilizzati (ad esempio pagamenti, imposte o eventi) e scaffolding. Chiedi all&#39;agente di rimuoverli e di mantenere solo la spedizione e [!DNL Admin UI] parti utilizzando un prompt come:

```shell-session
Proceed with Phase 5 cleanup.
```

L&#39;agente genera un rapporto di pulizia, rimuove le azioni, la configurazione e gli script inutilizzati e aggiorna il progetto. Completa questo passaggio prima della distribuzione.

![Il report di pulizia di fase 5 dell&#39;agente IA mostra i componenti rimossi e mantenuti](../assets/cleanup-report-shipping.png){width="600" zoomable="yes"}

### Distribuire l’estensione

1. Dopo aver verificato il codice generato, distribuisci l’estensione utilizzando il seguente prompt:

   ```shell-session
   Deploy the app.
   ```

   L&#39;agente esegue una valutazione di fattibilità pre-distribuzione (ad esempio, controllando `.env` per `COMMERCE_WEBHOOKS_PUBLIC_KEY`, `COMMERCE_BASE_URL` e variabili OAuth/IMS se viene utilizzata l&#39;interfaccia utente di amministrazione o l&#39;API Commerce).

   ![Preparazione per la predistribuzione dell&#39;agente AI e passaggi di distribuzione per l&#39;estensione Mock Shipping](../assets/pre-deployment-assessment-shipping.png){width="600" zoomable="yes"}

1. Quando sei sicuro dei risultati della valutazione, indica all’agente di procedere con la distribuzione. L’agente utilizza il toolkit MCP per verificare, generare e distribuire automaticamente.

   ![Output di distribuzione del toolkit MCP con pacchetti distribuiti e URL del webhook per l&#39;estensione di spedizione](../assets/deployment-process-shipping.png){width="600" zoomable="yes"}

### Post-distribuzione

Dopo la distribuzione, completa i passaggi seguenti per registrare il gestore fittizio, configurare il webhook e [!DNL Admin UI] e verificare l&#39;estensione al momento del pagamento.

1. **Registra il vettore fittizio in Commerce** (eseguito una volta dopo la distribuzione):

   ```bash
   npm run create-shipping-carriers
   ```

   Verificare che `.env` disponga di `COMMERCE_BASE_URL` e di credenziali OAuth/IMS valide, in modo che lo script possa registrare il gestore.

1. **Configura il webhook di spedizione in [!DNL Commerce Admin]:**

   - Vai a **Archivi** > Impostazioni > **Configurazione** > **Servizi Adobe** > **Webhook Commerce**.
   - Aggiungi un webhook:
      - **Metodo webhook:** `plugin.magento.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates`
      - **Tipo webhook:** **dopo**
      - **URL:** l&#39;URL dell&#39;azione Web **shipping-methods** distribuito (dall&#39;output di distribuzione o da [!DNL Adobe Developer Console]).
      - **Obbligatorio:** **Facoltativo** - Questo consente il funzionamento dell&#39;estrazione se l&#39;API esterna non restituisce tariffe.

   ![Configurazione del webhook di amministrazione di Commerce per le tariffe di spedizione fittizie](../assets/admin-webhook-shipping.png){width="600" zoomable="yes"}

1. **Configura l&#39;estensione [!DNL Admin UI SDK]:**

   - In [!DNL Commerce Admin], vai a **Archivi** > Impostazioni > **Configurazione**.
   - Apri **Adobe Services** > **Interfaccia utente amministratore SDK**.
   - Imposta **Abilita SDK** dell&#39;interfaccia utente amministratore su **Sì** e fai clic su **Salva configurazione** se non è già abilitata.
   - Fai clic su **Configura estensioni**, scegli l&#39;area di lavoro a cui è distribuita l&#39;app, quindi fai clic su **Applica**. È inoltre possibile selezionare l&#39;opzione **Personalizzato** e immettere il nome dell&#39;area di lavoro.
   - Seleziona l&#39;app [!DNL App Builder] nell&#39;elenco e salva. Se l&#39;app non viene visualizzata, fare clic su **Aggiorna registrazioni** e riprovare.

   ![Interfaccia utente amministratore SDK Configurare le estensioni modali con l&#39;area di lavoro e la selezione dell&#39;estensione](../assets/admin-ui-configure-extensions.png){width="600" zoomable="yes"}

1. **Configurare il metodo di spedizione fittizio nell&#39;interfaccia utente di amministrazione di Adobe Commerce:**
   - Apri **App** e seleziona la tua app.
   - Apri la scheda **Spedizione fittizia** (o equivalente).
   - Immetti i seguenti dettagli:
      - **URL servizio:** l&#39;URL del flusso di lavoro Pipedream copiato, ad esempio `https://123456.m.pipedream.net`.
      - **Chiave API:** qualsiasi valore non vuoto per il modello, ad esempio `tutorial-key`.
      - **Indirizzo del magazzino (origine spedizione):** nome, telefono, via, città, stato, codice postale, paese.
   - Fai clic su **Salva**. La configurazione viene archiviata nello stato Runtime e utilizzata dall&#39;azione metodi di spedizione.

   ![Modulo di configurazione per spedizione fittizia con URL del servizio, chiave API e indirizzo warehouse](../assets/admin-ui-mock-shipping.png){width="600" zoomable="yes"}

1. **Verifica al momento dell&#39;estrazione:** Aggiungere un prodotto al carrello, passare all&#39;estrazione e immettere un indirizzo di spedizione. Dovresti visualizzare le opzioni di spedizione fittizie, ad esempio **Mock Standard** e **Mock Express**.

   ![Pagina di pagamento che mostra le opzioni di spedizione fittizia dall&#39;API delle tariffe esterne](../assets/checkout-mock-shipping.png){width="600" zoomable="yes"}

### Risoluzione dei problemi

- **Configurazione non salvata nell&#39;interfaccia utente di amministrazione:** Se viene visualizzato &quot;Risposta non valida &#39;message/http&#39;&quot; o i valori non vengono aggiornati dopo il salvataggio, controllare i registri di attivazione runtime per l&#39;azione di configurazione, utilizzando un comando simile al seguente:

  ```bash
  aio app logs --action CustomMenu/shipping-config --limit 20
  ```

  Le cause comuni includono il gateway che prevede un formato di risposta specifico (ad esempio un corpo stringa e `Content-Type: application/json`) o la libreria di stato che richiede valori stringa. Assicurarsi che l&#39;azione memorizzi la configurazione come stringa e la analizzi durante la lettura e che l&#39;azione metodi di spedizione utilizzi lo stesso metodo di analisi. Controlla la chat o i registri dell’agente per la causa esatta e correggi.

- **&quot;La risposta deve contenere almeno un&#39;operazione&quot;** (nei registri del webhook): Commerce richiede che il webhook di spedizione restituisca almeno un&#39;operazione. Chiedi all’agente di garantire che l’azione metodi di spedizione non restituisca mai un array di operazioni vuoto (ad esempio restituendo una percentuale di fallback quando l’API esterna non restituisce alcuna percentuale).

- **Nessuna tariffa di spedizione al momento del pagamento:** Verificare che l&#39;URL e il metodo del webhook siano corretti, che il vettore fittizio sia registrato (`npm run create-shipping-carriers`) e che la configurazione della spedizione fittizia sia impostata in [!DNL Admin UI]. Controllare i registri di runtime per l&#39;azione dei metodi di spedizione per gli errori di API o di convalida. Verificare che l&#39;azione restituisca almeno un&#39;operazione, pertanto [!DNL Commerce] non mostra &quot;La risposta deve contenere almeno un&#39;operazione&quot;.

### Riepilogo esercitazione

Di seguito è riportato un riepilogo degli argomenti trattati in questa esercitazione:

- **Prerequisiti e configurazione:** verifica degli strumenti e creazione dell&#39;API per le tariffe di spedizione fittizie.
- **Sviluppo basato su agenti:** utilizzo del set di strumenti di estendibilità per commerce per generare requisiti, un piano di implementazione e il codice per il webhook di spedizione e l&#39;interfaccia utente amministratore.
- **Pulizia fase 5:** rimozione dei domini e dello scaffolding del kit di avvio dell&#39;estrazione inutilizzati prima della distribuzione.
- **Distribuzione:** valutazione pre-distribuzione e distribuzione del toolkit MCP.
- **Configurazione post-distribuzione:** Registrazione del vettore fittizio, configurazione del webhook [!DNL Commerce], abilitazione dell&#39;estensione [!DNL Admin UI SDK] e impostazione di Mock Shipping (URL servizio, chiave API, warehouse) in [!DNL Admin UI].
- **Verifica:** le opzioni di spedizione fittizie vengono visualizzate al momento dell&#39;estrazione.

### Passaggi successivi

Per ulteriori sperimentazioni con questa esercitazione, considera quanto segue:

- Automatizza la configurazione post-distribuzione con un hook che registra il vettore fittizio in [!DNL Commerce] e configura il webhook di spedizione dopo ogni distribuzione.
- Puntare l&#39;estensione a un&#39;API delle tariffe di spedizione reali modificando l&#39;URL del servizio e la chiave API in [!DNL Admin UI].
- Estendere [!DNL Admin UI] per mostrare lo stato del vettore o verificare la connettività al servizio tariffe.
