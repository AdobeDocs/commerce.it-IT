---
title: Esercitazione sull’estensione delle valutazioni
description: Scopri come creare un’estensione di valutazione del prodotto per Adobe Commerce as a Cloud Service utilizzando App Builder e strumenti di sviluppo assistiti da AI.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 453b21f89d2024a8d6927fa082affdd5abb6e5cd
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Adobe Developers Live - Cartella di lavoro di Adobe Commerce lab

Questa esercitazione ti guida attraverso la creazione di un&#39;estensione di valutazione del prodotto per [!DNL Adobe Commerce as a Cloud Service] utilizzando [!DNL Adobe App Builder] e strumenti di sviluppo assistiti da IA.

## Verificare i prerequisiti

Verifica che siano installati i seguenti prerequisiti:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git
git --version

# Check Bash
bash --version
```

## Accedi a Adobe Developer Console

1. Passa a [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Se hai già effettuato l&#39;accesso, fai clic sull&#39;icona del tuo profilo in alto a destra, quindi fai clic sul pulsante **Disconnetti**.
1. Accedi utilizzando l&#39;ID e-mail e la password forniti per il tuo posto.
1. Se viene richiesto di aggiungere un indirizzo e-mail o un numero di telefono secondario, fare clic su **Non adesso**.
1. Quando ti viene richiesto di selezionare un profilo organizzazione, seleziona **Adobe Commerce Labs**.

   ![select-organization](./assets/select-org.png){width="600" zoomable="yes"}

1. Se ti viene richiesto di accettare i termini e le condizioni, fai clic sul collegamento per leggerli, quindi fai clic su **Accetta e continua**.

   ![accept-terms](./assets/accept-terms.png){width="600" zoomable="yes"}

## Eseguire lo script di installazione

Se sono installati i [prerequisiti](#verify-prerequisites) e hai effettuato l&#39;accesso a Adobe Developer Console, scarica ed esegui lo script di installazione. In alternativa, puoi impostare manualmente lo script seguendo i [prerequisiti lab](workbook-prerequisites.md).

1. Clona l’archivio che contiene lo script di installazione:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-adl-2025.git
   ```

   >[!NOTE]
   >
   >Se lo script non riesce, fare riferimento ai [prerequisiti](workbook-prerequisites.md) e continuare quando lo script ha rilevato un errore.

1. Accedi al repository:

   ```bash
   cd commerce-adl-2025
   ```

1. Esegui lo script di installazione:

   ```bash
   bash adl-setup.sh
   ```

   Mentre lo script è in esecuzione, verrà richiesto di immettere il nome utente e la password, che verranno forniti durante l&#39;esercitazione. Il nome utente rifletterà la posizione e il numero di posto. Ad esempio, se ti trovi a San Jose, CA, postazione 123, il tuo nome utente sarà `sjc-adl-123@adobeeventlab.com`.

   È inoltre necessario selezionare il progetto che corrisponde al numero di postazione e all&#39;area di lavoro **stage**. Il nome del progetto corrisponderà alla posizione e al numero di posto. Ad esempio, se ti trovi a San Jose, CA, sede 123, il nome del progetto sarà `SJC ADL 123`.

## Sviluppo delle estensioni

Questa sezione ti guida attraverso lo sviluppo di un’estensione di valutazione per Adobe Commerce as a Cloud Service utilizzando strumenti di sviluppo assistiti da intelligenza artificiale.

### Installare gli strumenti di IA per l’estensibilità

Configurare gli strumenti di sviluppo assistito da IA nella cartella `extension`:

```bash
cd extension
```

```bash
aio commerce extensibility tools-setup
```

![Installare gli strumenti di IA](./assets/install-ai-tools.png){width="600" zoomable="yes"}

### Apri cursore

>[!NOTE]
>
>Quando si lavora con strumenti di sviluppo assistiti da intelligenza artificiale, il codice e le risposte generate dall’agente presenteranno varianti naturali.
>In caso di problemi con il codice, puoi sempre chiedere all&#39;agente di aiutarti a eseguire il debug.

Apri l&#39;applicazione [!DNL Cursor] e passa alla cartella `extension` oppure, se hai installato [CLI cursore](https://cursor.com/docs/configuration/shell#installing-cli-commands), immetti il comando seguente nel terminale:

```bash
cursor .
```

![Apri cursore](./assets/open-cursor.png){width="600" zoomable="yes"}

A questo punto, tutte le regole [!DNL Cursor] sono installate nella cartella `.cursor/rules`. Puoi trovare gli strumenti MCP nelle **Impostazioni MCP** in [!DNL Cursor]. Verificare che il set di strumenti `commerce-extensibility` sia abilitato senza errori. Se vengono visualizzati degli errori, disattiva e attiva la serie di strumenti.

![Impostazioni cursore](./assets/cursor-settings.png){width="600" zoomable="yes"}

Se hai aggiunto della documentazione al contesto del cursore, dovrai disattivarla. Passa a [!UICONTROL **Cursore**] > [!UICONTROL **Impostazioni**] > [!UICONTROL **Impostazioni cursore**] > [!UICONTROL **Indicizzazione e documenti**] ed elimina la documentazione elencata.

![Disabilita documentazione](./assets/disable-documentation.png){width="600" zoomable="yes"}

### Generazione del codice

Questa sezione illustra come utilizzare strumenti basati sull’intelligenza artificiale per generare il codice per un’estensione di valutazione del prodotto.

#### Definire i requisiti

Implementerai un’estensione che fornisce le valutazioni del prodotto come API. L&#39;estensione [!DNL App Builder] risponde con i dettagli di valutazione per uno SKU specifico.

**Richiesta iniziale:**

Utilizzare il seguente prompt in [!DNL Cursor]:

1. Apri la finestra di chat in Cursore.
1. Selezionare la modalità **Agente**.
1. Immetti il seguente prompt:

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   Implement a REST API to handle GET ratings requests.
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

1. Se l’agente richiede di cercare nella documentazione, consenti.

![Immetti il prompt nel cursore](./assets/enter-prompt.png){width="600" zoomable="yes"}

L’agente analizza i requisiti e pone domande chiarificatrici. Rispondi alle domande dell&#39;agente esattamente per aiutarlo a generare il codice migliore.

![L&#39;agente pone domande chiarificatrici](./assets/agent-questions.png){width="600" zoomable="yes"}

**Richiesta di risposta:**

Utilizza la seguente risposta per rispondere alle domande dell&#39;agente:

```text
Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
This extension will be called directly from the storefront,
no async invocation, such as events or webhooks, is required.
Let's start with just the GET API for now,
we will implement other CRUD operations at a later time.
We do not need a DB or storage mechanism right now,
just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
The API should only return the average rating for the product and the total number of ratings.
We do not need to add tests right now.
```

L&#39;agente crea un file `requirements.md` che funge da origine di verità per l&#39;implementazione.

![File dei requisiti creato](./assets/requirements-file.png){width="600" zoomable="yes"}

#### Verifica dei requisiti e dell’architettura del piano

1. Esaminare il file `requirements.md`.
1. Se tutto sembra corretto, indicare all&#39;agente di passare alla **Fase 2 - Pianificazione architettura**.
1. Rivedi il piano dell’architettura.
1. Indica all&#39;agente di procedere con la generazione del codice.

![Pianificazione architettura](./assets/architecture-planning.png){width="600" zoomable="yes"}

#### Genera codice

L&#39;agente genera il codice necessario e fornisce un riepilogo dettagliato con i passaggi successivi.

![Riepilogo generazione codice](./assets/code-generation-summary.png){width="600" zoomable="yes"}

![Passaggi successivi](./assets/next-steps.png){width="600" zoomable="yes"}

### Test locale

Chiedi all&#39;agente di aiutarti a testare il codice localmente.

```text
Test the ratings API locally on a dev server using cURL.
```

Segui le istruzioni dell’agente e verifica che l’API funzioni localmente.

![Test locale](./assets/local-testing.png){width="600" zoomable="yes"}

![Risultati test locali](./assets/local-testing-1.png){width="600" zoomable="yes"}

### Distribuire l’estensione

Dopo aver verificato il codice generato, sei pronto per distribuire l’estensione utilizzando il seguente prompt:

```text
Deploy the ratings API.
```

#### Valutazione pre-installazione

Prima della distribuzione, l&#39;agente esegue una valutazione di fattibilità pre-distribuzione.

![Valutazione pre-distribuzione](./assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

#### Distribuisci

Quando sei sicuro dei risultati della valutazione, indica all’agente di procedere con la distribuzione. L’agente utilizza il toolkit MCP per verificare, generare e distribuire automaticamente.

![Distribuzione](./assets/deployment-process.png){width="600" zoomable="yes"}

### Testare l’API

Puoi testare l’API prima di integrarla nella vetrina.

L’agente fornisce la posizione della nuova azione e una strategia di test.

![Strategia di test](./assets/testing-strategy.png){width="600" zoomable="yes"}

#### Test manuale con cURL

Verifica manualmente l’API utilizzando cURL in un terminale:

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![test cURL](./assets/curl-test.png){width="600" zoomable="yes"}

### Integrare con Edge Delivery Services

Per integrare l&#39;API di valutazione con una vetrina [!DNL Adobe Commerce] con tecnologia [!DNL Edge Delivery Services], chiedere all&#39;agente di creare un contratto di servizio con i requisiti per l&#39;API di valutazione:

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![Contratto di assistenza](./assets/create-contract.png){width="600" zoomable="yes"}

![Dettagli contratto di assistenza](./assets/contract.png){width="600" zoomable="yes"}

Tornare al terminale ed eseguire il comando seguente nella cartella `extension` per copiare il file nella cartella `storefront`:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## Connetti alla vetrina

Questa sezione ti aiuterà a implementare funzionalità vere e proprie della vetrina, mostrando come comunicare in modo efficace con gli agenti AI quando lavori con [!DNL Adobe Commerce] dropin e [!DNL Edge Delivery Services].

>[!NOTE]
>
>I prompt forniti sono punti di partenza, dovresti sentirti libero di parlare naturalmente con l&#39;agente. Quando si lavora con strumenti di sviluppo assistiti da intelligenza artificiale, il codice e le risposte generate dall’agente presenteranno varianti naturali.
>
>In caso di problemi con il codice, puoi sempre chiedere all&#39;agente di aiutarti a eseguire il debug.

### Implementare le stelle di valutazione e il conteggio delle recensioni

1. Passare alla cartella `storefront`:

   ```bash
   cd storefront
   ```

1. Aprire la cartella vetrina in una nuova finestra Cursore. Se è installato [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands), immettere il comando seguente nel terminale:

   ```bash
   cursor .
   ```

1. Avvia il server di sviluppo locale:

   ```bash
   npm run start
   ```

1. In un browser, passa alla pagina Abbigliamento:

   ```text
   http://localhost:3000/apparel
   ```

1. Osserva il layout standard dell’interfaccia utente della vetrina.

1. Chiedi all&#39;agente di effettuare le seguenti operazioni:

   ```text
   Implement product ratings to the storefront.
   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.
   Use the dropin slot system where available.
   
   Use the @RATINGS_API_CONTRACT.md to understand how to use the ratings api.
   ```

   >[!NOTE]
   >
   >Se viene richiesto di avviare il server di sviluppo locale, informare l&#39;agente che è già in esecuzione.

1. Osserva le modifiche nella base di codice e guarda la pagina Abbigliamento per gli aggiornamenti.

**Risultato previsto:**

* Viene creata automaticamente una valutazione del prodotto &quot;component&quot;.
* Il componente è integrato nei blocchi product-details, product-list-page e product-recommendations utilizzando gli slot.
* Le stelle vengono visualizzate con proporzioni di riempimento appropriate in base a valori di valutazione fittizi.

![Implementazione valutazioni prodotto](./assets/product-ratings-implementation.png){width="600" zoomable="yes"}

### Cambia i colori delle stelle

Chiedi all&#39;agente quanto segue:

```text
Change the star fill color to red.
```

**Risultato previsto:**

Le stelle sono cambiate in rosso.

![Colori Stella Rossa](./assets/red-star-colors.png){width="600" zoomable="yes"}

## Riepilogo vetrina

Nel corso di questa esercitazione, sono stati trattati i seguenti argomenti:

* **Implementazione delle funzionalità**: come descrivere le nuove funzionalità per un agente di intelligenza artificiale.
* **Modifiche iterative**: modifica rapida del codice esistente.
* **Componenti dell&#39;interfaccia utente complessi**: creazione di funzionalità interattive con riferimenti visivi.
* **Integrazione Dropin**: utilizzo di [!DNL Adobe Commerce] contenitori e slot di eliminazione.
* **Riutilizzabilità dei componenti**: creazione di componenti condivisi utilizzati in più blocchi.

## Passaggi successivi

Se il tempo lo consente, puoi personalizzare ulteriormente l’estensione delle classificazioni aggiungendo le seguenti funzionalità:

### Aggiungi distribuzione valutazione modale (facoltativo)

I passaggi seguenti mostrano come l’agente gestisce funzioni complesse dell’interfaccia utente con riferimenti visivi.

1. **Prima di iniziare:** Salva la seguente immagine fittizia e incollala nella chat con il tuo agente storefront.

   ![Mockup distribuzione valutazione](./assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Utilizza i seguenti passaggi per aiutarti a creare la distribuzione modale delle valutazioni in base all’immagine di riferimento:

   * Aggiorna l’API per restituire dati aggiuntivi che rappresentano la distribuzione delle valutazioni.
   * Aggiorna il contratto API.
   * Aggiorna il contatto nella base di codice della vetrina.
   * Chiedi all’agente vetrina di utilizzare l’immagine di riferimento e il contratto API aggiornato per aggiungere la distribuzione delle valutazioni alla pagina PDP.

1. Osserva le seguenti modifiche nella base di codice e guarda la pagina Abbigliamento per aggiornamenti:

   * Come l’agente interpreta il modello visivo
   * Indica se viene utilizzata la struttura HTML appropriata per l&#39;accessibilità
   * Come gestisce gli stati di posizionamento e interazione

**Risoluzione dei problemi:**

* Se il modale non viene visualizzato, controlla la console del browser per verificare la presenza di errori.
* Se il posizionamento è disattivato, puoi chiedere all’agente di:

  ```text
  adjust the modal position to be...
  ```

![Distribuzione valutazione modale](./assets/rating-distribution-modal.png){width="600" zoomable="yes"}
