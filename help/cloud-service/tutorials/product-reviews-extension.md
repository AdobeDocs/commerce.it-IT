---
title: Esercitazione sull’estensione per recensioni di prodotti
description: Scopri come creare un’estensione Q&A per Adobe Commerce as a Cloud Service con strumenti di sviluppo assistiti da intelligenza artificiale, App Builder e Edge Delivery Services.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 9c76bae29c05909406a40ca03a2b3d242db05f3f
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---

# Esercitazione sull’estensione delle recensioni dei prodotti

Questa esercitazione ti guida attraverso la creazione di un&#39;estensione che consente ai clienti di inviare contenuti di revisione dei prodotti e domande e risposte (Q&amp;A) per le vetrine con un back-end [!DNL Adobe Commerce as a Cloud Service] utilizzando [!DNL Adobe App Builder] e strumenti di sviluppo assistiti da IA. L’estensione fornisce endpoint REST API per consentire agli acquirenti di visualizzare e inviare contenuti di revisione e domanda e risposta del prodotto (Q&amp;A) e visualizzarli nella pagina dei dettagli del prodotto (PDP).

Vengono create due parti:

- **Estensione App Builder**: API REST con operazioni GET e POST per creare e visualizzare contenuti di revisione e domande e risposte dei prodotti con convalida, impaginazione e persistenza in `aio-lib-state`.
- **Integrazione con Storefront**: blocco di revisione dei prodotti nel PDP che visualizza le recensioni e le domande e risposte, con moduli che consentono agli acquirenti di inviare recensioni, domande e risposte.

>[!NOTE]
>
>Gli agenti di IA non sono deterministici. I prompt, le domande e gli output di questa esercitazione sono esempi. Il tuo agente può produrre domande, requisiti o proposte di architettura diversi. Utilizza gli esempi in questa esercitazione per indirizzare l’agente verso un risultato simile.

Prima di iniziare, completa i [prerequisiti](./tutorial-prerequisites.md). Questa esercitazione utilizza il **kit di avvio dell&#39;integrazione**. Verificare di averlo già clonato e di aver completato i passaggi di configurazione descritti nella pagina prerequisiti.

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

Se uno dei comandi precedenti non restituisce i risultati previsti, vedere i [prerequisiti](./tutorial-prerequisites.md).

Inoltre, verifica quanto segue:

- È presente un&#39;istanza [!DNL Adobe Commerce as a Cloud Service] con dati di prodotto. Consulta [Istanze del servizio Commerce Cloud](https://experienceleague.adobe.com/it/docs/commerce/cloud-service/overview){target="_blank"}.
- Si dispone di un progetto vetrina connesso all&#39;istanza [!DNL Commerce]. In caso contrario, seguire i passaggi descritti in [Creare una vetrina](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=it){target="_blank"}.
- CLI `aem` installato:

  ```bash
  npm install -g @adobe/aem-cli
  ```

## Sviluppo delle estensioni

Questa sezione ti guida attraverso lo sviluppo di un&#39;estensione per inviare e visualizzare la revisione del prodotto e i contenuti Q&amp;A per l&#39;estensione per gli store front con un backend [!DNL Adobe Commerce as a Cloud Service] utilizzando strumenti di sviluppo assistiti da intelligenza artificiale. L’estensione fornisce un’API REST per inviare e visualizzare la revisione del prodotto e i contenuti di domande e risposte e per visualizzarli sul PDP.

1. Passa alle impostazioni MCP nell’agente di codifica. Ad esempio, in Cursore, vai a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**. Verificare che il set di strumenti `commerce-extensibility` sia abilitato senza errori. Se vengono visualizzati degli errori, disattiva e attiva la serie di strumenti.

   >[!NOTE]
   >
   >Quando si lavora con strumenti di sviluppo assistiti da intelligenza artificiale, è probabile che il codice e le risposte generate dall’agente presentino variazioni naturali.
   >Se riscontri problemi con il codice, chiedi all&#39;agente di aiutarti a eseguirne il debug.

1. Se hai aggiunto della documentazione al contesto del cursore, disattivala.

   Passa a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** ed elimina la documentazione elencata.

### Passaggio 1: fornire il prompt iniziale

Richiedi all’agente di intelligenza artificiale di iniziare l’implementazione. Dire all&#39;agente di fermarsi e porre domande ti aiuta a gestire l&#39;implementazione in anticipo.

Immetti il seguente prompt nella finestra di chat dell&#39;agente:

```shell-session
I want to build an Adobe Commerce as a Cloud Service extension that allows shoppers to submit and view product review and question and answer (Q&A) content that displays on product detail pages (PDP).

## Product Reviews
The application has REST API endpoints that can be called by a storefront to retrieve and submit product reviews for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch reviews for
- limit (integer, optional): The maximum number of reviews to return (default: 10)
- offset (integer, optional): The number of reviews to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a review for
- rating (integer, required): The rating for the product (1-5)
- review (string, optional): The text of the review
- user (string, optional): The name of the user submitting the review

The POST endpoint validates the input and returns appropriate error responses for invalid data. The reviews are stored and associated with the corresponding product SKU.

## Questions and Answers
The application has REST API endpoints that can be called by a storefront to retrieve and submit questions and answers for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch questions and answers for
- limit (integer, optional): The maximum number of questions and answers to return (default: 10)
- offset (integer, optional): The number of questions and answers to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a question or answer for
- type (string, required): The type of submission ("question" or "answer")
- questionId (string, required if type is "answer"): The ID of the question being answered
- content (string, required): The text of the question or answer
- user (string, optional): The name of the user submitting the question or answer

The POST endpoint validates the input and returns appropriate error responses for invalid data. The questions and answers are stored and associated with the corresponding product SKU. Answers are also associated with the corresponding question.

Do not require Adobe IMS authentication for these endpoints. They will be called directly from the storefront.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>Dire all&#39;agente di INTERROMPERE e porre domande prima di procedere ti aiuta a gestire l&#39;implementazione nelle prime fasi del processo. In questo modo, i presupposti chiave e i requisiti mancanti vengono identificati in anticipo ed è necessario per avviare il flusso di lavoro guidato in questa esercitazione.

### Passaggio 2: Rispondere alle domande dell&#39;agente

L&#39;agente restituisce una serie di domande a cui deve rispondere prima di poter iniziare a creare una soluzione. Nell&#39;esempio seguente vengono illustrate domande e risposte tipiche. Il tuo agente può porre domande diverse, ma gli argomenti sono in genere gli stessi.

**Domande dell&#39;agente di esempio:**

1. **API REST — host e consumatori** — L&#39;API REST CRUD deve far parte di questa app App Builder (azioni web su Adobe I/O Runtime) che le vetrine chiamano? Chi lo chiamerà (EDS Storefront, custom/headless storefront, o entrambi)? Hai bisogno di un accesso CORS o pubblico (non autenticato) oppure i chiamanti useranno le chiavi API o OAuth?
1. **Modello dati** — Cosa deve rappresentare una &quot;revisione&quot; o una &quot;domanda&quot;? Identificatore cliente (solo e-mail o anche ID cliente)? Identificatore del prodotto (solo SKU o SKU + visualizzazione punto vendita)? Lo stesso cliente può inviare più recensioni per la stessa SKU?
1. **Persistenza** - `aio-lib-state` è il posto giusto per mantenere le recensioni e le domande e risposte oppure si dispone di un archivio esterno? Il progetto deve presupporre più tenant o tenant singolo?
1. **Semantica di impaginazione**: per Q&amp;A GET, `limit` è applicabile solo alle domande (con risposte nidificate) o al conteggio totale di domande più risposte?

**Risposte di esempio:**

```shell-session
1. The REST API should be part of this App Builder app. It will be called by the EDS Storefront. No authentication — public access for both GET and POST.
2. For reviews: sku, rating (1-5), optional review text, optional user name. For Q&A: sku, type (question or answer), content, optional user. Answers linked to questions via questionId. Allow multiple reviews per SKU from the same user.
3. Use aio-lib-state. Single tenant for now.
4. Pagination by question — limit and offset apply to questions; each question includes its nested answers.
```

>[!NOTE]
>
>Il tuo agente potrebbe porre domande diverse. Utilizza queste risposte come guida per indirizzare l’agente verso lo stesso risultato funzionale: un’API REST pubblica con recensioni e domande e risposte, persistenza di `aio-lib-state` e nessuna autenticazione.

### Passaggio 3: verifica dei requisiti e dell’architettura

L&#39;agente genera i requisiti e i documenti dell&#39;architettura da esaminare. Verifica che i requisiti corrispondano alle risposte fornite e che l’architettura copra:

- Quattro azioni Web: `reviews-get`, `reviews-post`, `qa-get`, `qa-post`
- Persistenza nell&#39;utilizzo di `aio-lib-state` con chiavi conformi al pattern consentito (`[a-zA-Z0-9-_.]` — nessun due punti)
- Valori di stato memorizzati come stringhe JSON (non oggetti o array non elaborati)
- Pacchetto autonomo: codice condiviso (utilità, costanti) all&#39;interno del pacchetto `product-reviews`, non tramite `../../` percorsi che eseguono l&#39;escape del bundle

>[!NOTE]
>
>Gli agenti di IA non sono deterministici e i loro comportamenti variano a seconda del modello e dell’IDE. È possibile che vengano visualizzate domande diverse che producono un diverso insieme di requisiti e architettura. In tal caso, prima di procedere, prova a dirigere l’agente nella direzione in modo che l’implementazione corrisponda strettamente a quanto illustrato in questa esercitazione.

### Passaggio 4: selezionare un piano di implementazione

L’agente ti offre la possibilità di creare un piano di implementazione dettagliato o di completare un’implementazione diretta.

- Se si desidera un piano revisionabile che può essere eseguito in fasi con maggiore controllo, selezionare la prima opzione.
- Se desideri che l&#39;agente esegua l&#39;implementazione completa con un intervento minimo, seleziona la seconda opzione.

### Passaggio 5: distribuire l’estensione

Dopo che l&#39;agente ha completato l&#39;implementazione, distribuisci l&#39;estensione:

```bash
aio app deploy
```

Se l&#39;agente ha aggiunto `require-adobe-auth: true` alle azioni, chiedergli di rimuovere l&#39;autenticazione in modo che gli endpoint possano essere chiamati direttamente dalla vetrina:

```shell-session
Remove the requirement to provide a valid Adobe IMS access token from all product-reviews actions.
```

Quindi ridistribuisci:

```bash
aio app deploy
```

### Passaggio 6: creare dati fittizi e precompilare per il test

Crea un file di dati fittizio e utilizza curl per precompilare l’API in modo da disporre di contenuti di revisione e domande e risposte di esempio per i test in CLI e storefront.

1. Creare un file `docs/mock-product-reviews-data.json` (o simile) con dati di esempio. Ad esempio:

   ```json
   {
     "reviews": [
       { "sku": "ADB153", "rating": 5, "review": "Great product, highly recommend!", "user": "shopper@example.com" },
       { "sku": "ADB153", "rating": 4, "review": "Good value for money.", "user": "buyer@example.com" }
     ],
     "questions": [
       { "sku": "ADB153", "type": "question", "content": "Does this come in other colors?", "user": "curious@example.com" }
     ]
   }
   ```

1. Utilizza curl per pubblicare i dati nell’API implementata.

   Sostituisci `<your-runtime-url>` con l&#39;URL di runtime effettivo di App Builder (ad esempio, `https://1172492-prodreviewqa135-stage.adobeioruntime.net`):

   ```bash
   API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
   
   # Submit reviews
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":5,"review":"Great product, highly recommend!","user":"shopper@example.com"}'
   
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":4,"review":"Good value for money.","user":"buyer@example.com"}'
   
   # Submit a question (save the returned id for the answer)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"question","content":"Does this come in other colors?","user":"curious@example.com"}'
   
   # Submit an answer (replace <QUESTION-UUID> with the id from the question response)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it comes in blue and red.","user":"seller@example.com"}'
   ```

1. Verifica i dati con le richieste di GET:

   ```bash
   curl -s "$API_URL/reviews-get?sku=ADB153"
   curl -s "$API_URL/qa-get?sku=ADB153"
   ```

>[!TIP]
>
>Utilizzare SKU `ADB153` per un prodotto con contenuti di revisione e domande e risposte e `ADB152` per un prodotto senza revisioni. Questa configurazione di dati consente di testare sia gli stati popolati che quelli vuoti nella vetrina.

### Passaggio 7: testare l’estensione

Chiedi all&#39;agente di fornire i passaggi di test o utilizza gli esempi curl del passaggio precedente. Negli esempi seguenti vengono illustrati i comandi di test tipici.

**Invia una recensione:**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
curl -s -X POST "$API_URL/reviews-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","rating":5,"review":"Excellent!","user":"test@example.com"}'
```

**Elenco recensioni:**

```bash
curl -s "$API_URL/reviews-get?sku=ADB153"
```

**Invia una domanda:**

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"question","content":"Is this dishwasher safe?","user":"test@example.com"}'
```

**Invia una risposta** (utilizza `id` dalla risposta alla domanda come `questionId`):

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it is.","user":"support@example.com"}'
```

### Crea il contratto di assistenza

Una volta completata l&#39;implementazione del servizio, chiedere all&#39;agente di creare un contratto di assistenza per il lavoro della vetrina:

```shell-session
Create a service contract for the Product Review and Q&A application that defines the API endpoints, request and response formats, and any necessary data models. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront integration without needing to ask additional questions about the API. Name this file PRODUCT_REVIEW_QA_CONTRACT.md
```

Copia questo file nel progetto storefront in modo che l&#39;agente storefront possa farvi riferimento.

## Connetti alla vetrina

Questa sezione ti guida attraverso l&#39;implementazione della sezione vetrina delle recensioni dei prodotti e dell&#39;estensione Q&amp;A tramite [!DNL Edge Delivery Services] e strumenti di sviluppo assistiti da AI. Aggiungi al PDP un blocco di recensione del prodotto che visualizza sia il contenuto di revisione che quello di domanda e risposta e che consente agli acquirenti di inviare nuovi contenuti.

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
- Il file `PRODUCT_REVIEW_QA_CONTRACT.md` copiato nel tuo progetto storefront

### Passaggio 1: Convalidare l’ambiente

Apri il file `config.json` e verifica che i valori per `commerce-core-endpoint` e `commerce-endpoint` puntino all&#39;endpoint GraphQL [!DNL Adobe Commerce as a Cloud Service].

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Passaggio 2: specificare il prompt iniziale

Se il contratto di assistenza è già presente nel progetto, richiedere all&#39;agente di implementare il blocco di revisione del prodotto. Utilizza la modalità **Piano**, se disponibile nell&#39;agente, per impedire che l&#39;agente proceda senza un piano.

```shell-session
Analyze @PRODUCT_REVIEW_QA_CONTRACT.md and build a product review block using the API specified in the contract. The block displays both reviews and Q&A content on the product detail page, with forms for shoppers to submit reviews, questions, and answers. Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>La richiesta specifica di utilizzare l’abilità di project manager attiva il flusso di lavoro graduale che consente di gestire l’implementazione. Ciò assicura che le ipotesi chiave e i requisiti mancanti siano identificati nelle prime fasi del processo.

### Passaggio 3: rispondere alle domande più chiare

L&#39;agente restituisce una serie di domande a cui deve rispondere prima di poter iniziare a creare una soluzione. Nell&#39;esempio seguente vengono illustrate domande e risposte tipiche. Il tuo agente può porre domande diverse, ma gli argomenti sono in genere gli stessi.

**Domande dell&#39;agente di esempio:**

1. **URL di base API** — In che modo lo storefront deve ottenere l&#39;URL di base API per le recensioni dei prodotti? Le opzioni possono includere un blocco di configurazione (ad esempio, una tabella con `apiBaseUrl`), segnaposto globali o un altro approccio.
1. **Origine SKU**: il blocco deve leggere lo SKU dal contesto PDP (prodotto corrente) o dalla configurazione del blocco?
1. **Comportamento modulo** - Dopo un invio corretto, il modulo deve essere nascosto, mostrare un messaggio di operazione riuscita o rimanere visibile ma disabilitato?

**Risposte di esempio:**

```shell-session
1. Block table config with apiBaseUrl (required). Each block instance can point to its own deployment.
2. From block table if set; otherwise use getProductSku() so it works on PDP without authoring a SKU.
3. Show a success message above the form; keep the form visible but disabled.
```

>[!NOTE]
>
>Sostituisci il segnaposto nella configurazione del blocco con l&#39;URL di runtime effettivo di App Builder (ad esempio, `https://1172492-prodreviewqa135-stage.adobeioruntime.net`).
>
>Il tuo agente potrebbe porre domande diverse. Utilizza queste risposte come guida:
>
>- L’URL di base dell’API deve provenire dalla tabella dei blocchi in modo da poter essere modificato senza modifiche al codice.
>- SKU dalla tabella dei blocchi se impostata; in caso contrario dal prodotto corrente sulla PDP.
>- Dopo l’invio corretto, mostra un messaggio di successo e disattiva il modulo.

### Passaggio 4: verifica dei requisiti e dell’architettura

L&#39;agente aggiorna il documento sui requisiti che è possibile esaminare. Verifica che:

- Il blocco esegue il rendering di recensioni (con valutazione, utente, data, testo) e domande e risposte (domande con risposte nidificate).
- Forms è in grado di inviare recensioni, domande e risposte.
- L’impaginazione è supportata sia per i contenuti di revisione che per quelli di domande e risposte.
- L’integrazione API utilizza l’URL di base della tabella dei blocchi.
- Gli stati di successo e di errore vengono gestiti in base al contratto.

>[!NOTE]
>
>Gli agenti di IA non sono deterministici e i loro comportamenti variano a seconda del modello e dell’IDE. È possibile che vengano visualizzate domande diverse che producono un diverso insieme di requisiti e architettura. In tal caso, prima di procedere, prova a dirigere l’agente nella direzione in modo che l’implementazione corrisponda strettamente a quanto illustrato in questa esercitazione.

### Passaggio 5: selezionare un piano di implementazione

L’agente ti offre la possibilità di creare un piano di implementazione dettagliato o di completare un’implementazione diretta.

- Se si desidera un piano revisionabile che può essere eseguito in fasi con maggiore controllo, selezionare la prima opzione.
- Se desideri che l&#39;agente esegua l&#39;implementazione completa con un intervento minimo, seleziona la seconda opzione.

Durante l’implementazione, l’agente crea e modifica i file di blocco. Guarda il codice generato e fai domande o reindirizza l’agente secondo necessità. Se non viene eseguito il rendering del blocco, chiedere all&#39;agente di analizzare la decorazione di sezione e il pattern di individuazione del blocco. L&#39;elemento del blocco deve essere un figlio diretto della sezione in modo che il framework possa trovarlo.

### Passaggio 6: aggiungere il blocco alla pagina del prodotto in Authoring dei documenti

Aggiungi il blocco di recensione prodotto al modello della pagina di prodotto in modo che venga visualizzato su tutti i PDP. Utilizza il servizio di authoring dei documenti (da.live) per aggiungere e configurare il blocco.

1. Apri il servizio di authoring dei documenti, ad esempio [da.live](https://da.live/)

1. Fai clic sullo spazio del progetto, apri la cartella **products** e seleziona **default** (`products/default`).

1. Aggiungi una nuova sezione blocco.

   Nella tabella dei blocchi, aggiungi una riga con il nome del blocco **product-review** (o il nome del blocco creato dall&#39;agente).

1. Configura il blocco con le impostazioni richieste:
   - **apiBaseUrl** — L&#39;URL di runtime di App Builder (ad esempio, `https://<namespace>-<app-name>-stage.adobeioruntime.net`).
   - **sku** — Lasciare vuoto per usare lo SKU del prodotto corrente nel PDP o immettere uno SKU specifico per visualizzare solo le recensioni per quel prodotto.

1. Fai clic su **[!UICONTROL Publish]** per pubblicare le modifiche.

### Passaggio 7: avviare il server e testare

Dopo aver aggiunto il blocco alla pagina del prodotto in Document Authoring, avvia il server di sviluppo e verifica il blocco.

1. Avvia il server di sviluppo locale:

   ```bash
   npm run start
   ```

1. In un browser, accedi a una pagina di prodotto con contenuti di domande e risposte precompilati. Ad esempio:

   ```shell-session
   http://localhost:3000/products/<product-slug>/ADB153
   ```

1. Verifica che nel blocco di recensione del prodotto siano visualizzati le recensioni e il contenuto delle domande e risposte e che i moduli di invio funzionino.

Puoi eseguire test manuali o chiedere all’agente di utilizzare le funzionalità del browser per eseguire test per tuo conto:

```shell-session
Run complete browser testing. Use the following product page 'http://localhost:3000/products/<product-slug>/ADB153'
```

### Passaggio 8: Pulire

Dopo aver saltato o completato il test, l&#39;agente ti chiede di procedere alla fase finale di **pulizia**. Una volta confermata, l’agente archivia tutti gli artefatti della documentazione creati durante l’implementazione.

## Risoluzione dei problemi

Se riscontri dei problemi durante l’esercitazione, utilizza i seguenti suggerimenti.

### Back-end (App Builder)

| Sintomo | Causa | Correzione |
|---------|-------|-----|
| GET o POST restituisce 500 &quot;Impossibile trovare il modulo&quot; | Le azioni di revisione dei prodotti utilizzano `require("../../utils")` o `require("../../constants")`, che determinano l&#39;escape del bundle del pacchetto. Tali file non vengono inclusi durante la distribuzione del pacchetto. | Rendi il pacchetto di recensioni dei prodotti autonomo. Aggiungi `actions/product-reviews/lib/constants.js` e `actions/product-reviews/lib/utils.js` e aggiorna tutte e quattro le azioni da richiedere a `../lib/...` invece di `../../`. |
| GET restituisce 500 con &quot;la chiave deve corrispondere al pattern&quot; | Le chiavi di stato utilizzano i due punti (ad esempio, `reviews:ADB153`). `aio-lib-state` consente solo `[a-zA-Z0-9-_.]`. | Modificare i prefissi da `reviews:` e `qa:` in `reviews.` e `qa.`. Aggiungi un helper `stateKey(prefix, sku)` che bonifica lo SKU (sostituisci caratteri non validi con `_`). |
| POST restituisce 500 con &quot;il valore deve essere una stringa&quot; | `aio-lib-state` accetta solo valori stringa. Il codice passa array o oggetti a `state.put()`. | Serializzare con `JSON.stringify()` durante la scrittura e `JSON.parse()` durante la lettura. Aggiorna tutte e quattro le azioni. |

{style="table-layout:auto"}

### Vetrina (Edge Delivery Services)

| Sintomo | Causa | Correzione |
|---------|-------|-----|
| Il blocco non viene riprodotto nella pagina di prova | L&#39;elemento del blocco è nidificato all&#39;interno di un `div` aggiuntivo, quindi dopo `decorateSections` il selettore del blocco (`div.section > div > div`) non corrisponde. | Rendi il blocco un figlio diretto della sezione. Struttura: `section > div.product-review` (o classe di blocco equivalente). Evita `section > div > div.product-review`. |
| Token CSS non validi | Il blocco utilizza token di progettazione che non esistono in `styles/styles.css` (ad esempio, `--color-error-100`, `--type-detail-font-size`). | Chiedere all&#39;agente di convalidare i token rispetto al progetto `styles/styles.css` e sostituire i token non validi con quelli esistenti (ad esempio, `--color-alert-*`, `--type-details-caption-*`). |

{style="table-layout:auto"}

## Riepilogo esercitazione

Di seguito è riportato un riepilogo degli argomenti trattati in questa esercitazione:

- **Sviluppo delle estensioni:** descrizione della funzionalità di creazione e visualizzazione di contenuti di recensione prodotti e domande e risposte in una vetrina con un back-end Adobe Commerce as a Cloud Service in un agente di intelligenza artificiale e di implementazione di questa funzionalità mediante la generazione di un&#39;API REST funzionante con quattro endpoint utilizzando [!DNL App Builder].
- **Persistenza:** utilizzo di `aio-lib-state` con il formato di chiave e i valori serializzati JSON corretti.
- **Dati fittizi e pre-popolamento:** Creazione di un file di dati fittizio e utilizzo di curl per prepopolare l&#39;API per il test di CLI e storefront.
- **Contratti di servizio:** creazione di contratti API che collegano estensioni back-end e implementazioni storefront.
- **Integrazione graduale della vetrina:** Utilizzo di requisiti, architettura e implementazione tramite competenze basate sull&#39;intelligenza artificiale.
- **Blocco PDP:** aggiunta al PDP di un blocco di revisione del prodotto che visualizza revisioni e domande e risposte con moduli di invio e impaginazione.

## Passaggi successivi

Utilizza i seguenti suggerimenti per estendere il servizio di recensioni dei prodotti:

- **Aggiungi moderazione:** Implementa un flusso di lavoro di moderazione per la revisione e contenuti di domande e risposte prima della pubblicazione.
- **Aggiungi autenticazione:** Richiedi agli acquirenti di accedere per inviare recensioni o contenuti di domande e risposte e di associare gli invii agli account dei clienti.
- **Aggiungi una pagina di gestione degli abbonamenti:** Crea una pagina di vetrina in cui gli acquirenti possono visualizzare e modificare le loro recensioni.
- **Supporto di distribuzioni multi-tenant:** Estendere la gestione dello stato per supportare più tenant Commerce in una singola app App Builder.
- **Aggiungi limite di velocità:** Implementa limiti di velocità nell&#39;API per evitare abusi.
