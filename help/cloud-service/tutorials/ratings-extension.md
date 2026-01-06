---
title: Esercitazione sull’estensione delle valutazioni
description: Scopri come creare un’estensione di valutazione del prodotto per Adobe Commerce as a Cloud Service utilizzando App Builder e strumenti di sviluppo assistiti da AI.
feature: App Builder, Cloud
role: Developer
level: Intermediate
hide: true
hidefromtoc: true
source-git-commit: 4ca909c2f8f95fbc404ce6a745d769958b2c01f4
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# Tutorial sull’estensione delle valutazioni (Beta)

>[!NOTE]
>
>Lo strumento di intelligenza artificiale utilizzato in questo tutorial è attualmente in Beta e potrebbe includere bug o altri problemi.

Questa esercitazione ti guida attraverso la creazione di un&#39;estensione di valutazione del prodotto per [!DNL Adobe Commerce as a Cloud Service] utilizzando [!DNL Adobe App Builder] e strumenti di sviluppo assistiti da IA.

Prima di iniziare, completa i [prerequisiti](./tutorial-prerequisites.md).

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

Se uno dei comandi precedenti non restituisce i risultati previsti, consultare i [prerequisiti](tutorial-prerequisites.md).

## Sviluppo delle estensioni

Questa sezione ti guida attraverso lo sviluppo di un’estensione di valutazione per Adobe Commerce as a Cloud Service utilizzando strumenti di sviluppo assistiti da intelligenza artificiale.

1. Passare a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]** e verificare che il set di strumenti `commerce-extensibility` sia abilitato senza errori. Se vengono visualizzati degli errori, disattiva e attiva la serie di strumenti.

   ![Impostazioni IDE cursore che mostrano il set di strumenti di estendibilità e commerce MCP abilitato](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Quando si lavora con strumenti di sviluppo assistiti da intelligenza artificiale, è probabile che il codice e le risposte generate dall’agente presentino variazioni naturali.
   >In caso di problemi con il codice, puoi sempre chiedere all&#39;agente di aiutarti a eseguire il debug.

1. Se hai aggiunto della documentazione al contesto del cursore, disattivala:

   - Passa a [!UICONTROL **Cursore**] > [!UICONTROL **Impostazioni**] > [!UICONTROL **Impostazioni cursore**] > [!UICONTROL **Indicizzazione e documenti**] ed elimina la documentazione elencata.

   ![L&#39;indicizzazione del cursore e le impostazioni dei documenti con l&#39;elenco della documentazione sono vuoti](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Genera il codice per un’estensione di valutazione del prodotto:
   - Dalla finestra di chat del cursore, selezionare la modalità [!UICONTROL **Agente**].
   - Immetti il seguente prompt:

   ```shell-session
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >Se l’agente richiede di cercare nella documentazione, consenti.

1. Rispondi alle domande dell&#39;agente esattamente per aiutarlo a generare il codice migliore.

   ![Finestra di chat del cursore in modalità agente con richiesta di estensione immessa](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![Agente di IA che pone domande chiarificatrici sui requisiti dell&#39;estensione](../assets/agent-questions.png){width="600" zoomable="yes"}

1. Utilizza il testo di esempio seguente per rispondere alle domande dell’agente per impostare dati di valutazione randomizzati:

   ```shell-session
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension is called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   L&#39;agente crea un file `requirements.md` che funge da origine di verità per l&#39;implementazione.

   ![File Requirements.md creato dall&#39;agente di IA con dettagli di implementazione](../assets/requirements-file.png){width="600" zoomable="yes"}

1. Esaminare il file `requirements.md` e verificare il piano.

   Se tutto sembra corretto, indicare all&#39;agente di passare alla **Fase 2 - Pianificazione architettura**.
1. Rivedi il piano dell’architettura.
1. Indica all&#39;agente di procedere con la generazione del codice.

   L&#39;agente genera il codice necessario e fornisce un riepilogo dettagliato con i passaggi successivi.

   ![Piano dell&#39;architettura dell&#39;agente di IA di fase 2 per l&#39;API di valutazione](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![Riepilogo dei file di codice e della struttura generati](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![Agente di IA che fornisce i passaggi successivi per il test e la distribuzione](../assets/next-steps.png){width="600" zoomable="yes"}

### Test locale

1. Chiedi all&#39;agente di aiutarti a testare il codice localmente.

   ```shell-session
   Test the ratings API locally on a dev server using cURL.
   ```

1. Segui le istruzioni dell’agente e verifica che l’API funzioni localmente.

   ![Istruzioni agente IA per test API locali](../assets/local-testing.png){width="600" zoomable="yes"}

   ![Terminale che mostra i risultati dei test API locali con cURL](../assets/local-testing-1.png){width="600" zoomable="yes"}

### Distribuire l’estensione

1. Dopo aver verificato il codice generato, distribuisci l’estensione utilizzando il seguente prompt:

   ```shell-session
   Deploy the ratings API.
   ```

   Prima della distribuzione, l&#39;agente esegue una valutazione di fattibilità pre-distribuzione.

   ![Elenco di controllo per la valutazione dell&#39;idoneità dell&#39;agente di IA pre-distribuzione](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. Quando sei sicuro dei risultati della valutazione, indica all’agente di procedere con la distribuzione.

   L’agente utilizza il toolkit MCP per verificare, generare e distribuire automaticamente.

   ![Processo di compilazione e distribuzione del toolkit MCP](../assets/deployment-process.png){width="600" zoomable="yes"}

### Post-distribuzione

Puoi testare l’API prima di integrarla nella vetrina. L’agente deve fornire la posizione della nuova azione e una strategia di test.

![Strategia di test dell&#39;agente di IA con URL azione distribuito e comandi di test](../assets/testing-strategy.png){width="600" zoomable="yes"}

Puoi anche testare manualmente l’API utilizzando cURL in un terminale:

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![Terminale che mostra il test cURL dell&#39;API di classificazione distribuita](../assets/curl-test.png){width="600" zoomable="yes"} riuscito

### Integrare con Edge Delivery Services

Per integrare l&#39;API di valutazione con una vetrina [!DNL Adobe Commerce] con tecnologia [!DNL Edge Delivery Services], chiedere all&#39;agente di creare un contratto di servizio con i requisiti per l&#39;API di valutazione:

```shell-session
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![Agente di IA che crea il file del contratto di servizio per l&#39;integrazione storefront](../assets/create-contract.png){width="600" zoomable="yes"}

![File markdown del contratto API delle valutazioni con dettagli dell&#39;endpoint e della risposta](../assets/contract.png){width="600" zoomable="yes"}
<!-- 
Return to the terminal and run the following command in the `extension` folder to copy the file to the `storefront` folder:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
``` -->

### Passaggi successivi

Ora che hai il contratto API di valutazione, puoi iniziare a creare la porzione vetrina (front-end) dell’estensione di valutazione.

<!-- 
## Connect to the storefront

This section teaches you how to implement real storefront features and communicate effectively with AI agents when working with [!DNL Adobe Commerce] dropins and [!DNL Edge Delivery Services].

>[!NOTE]
>
>The prompts provided are starting points. Although you can use them without modification, consider having a natural conversation with the agent.
>
>When working with AI-assisted development tools, there are always natural variations in the code and responses generated by the agent.
>
>If you encounter any issues with your code, ask the agent to help you debug it.

### Ratings stars and review count implementation

1. Navigate to the `storefront` folder:

   ```bash
   cd storefront
   ```

1. Open the storefront folder in a new Cursor window.

    Alternatively, if you have the [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) installed, open the window by using the following command in your terminal:

   ```bash
   cursor .
   ```

1. Start the local development server:

   ```bash
   npm run start
   ```

1. In a browser, navigate to the Apparel page:

   ```shell-session
   http://localhost:3000/apparel
   ```

1. Observe the boilerplate storefront UI layout and note the lack of visual product ratings.

1. Use the following prompt with your agent:

   ```shell-session
   Implement product ratings in the storefront.

   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.

   Use the dropin slot system where available.

   Use @RATINGS_API_CONTRACT.md to understand how to use the ratings API.
   ```

1. Observe the changes in the codebase, and watch the Apparel page for updates.

   You should see the following changes in your development environment and browser:

   * A product rating "component" is automatically created.
   * The component is integrated into product-details, product-list-page, and product-recommendations blocks using [dropin slots](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots).
   * Stars display with proper fill proportions based on mock rating values.

![Product Ratings Implementation](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Tutorial recap

Here is a summary of the topics covered in this tutorial:

* **Feature implementation**: How to describe new functionality to an AI agent.
* **Iterative changes**: Making quick modifications to existing code.
* **Complex UI components**: Building interactive features with visual references.
* **Dropin integration**: Working with [!DNL Adobe Commerce] dropin containers and slots.
* **Component reusability**: Creating shared components used across multiple blocks.

## Next steps

For further experimentation with this tutorial, use the following suggestions to further customize your ratings extension, or create your own modifications:

### Change the star colors

Use the following prompt to your agent:

```shell-session
Change the star fill color to red.
```

**Expected outcome:**

The stars are changed to red.

![Red Star Colors](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Add rating distribution modal

The following steps show how the agent handles complex UI features with visual references.

1. **Before starting:** Save the following mock image and paste it into the chat with your storefront agent.

   ![Rating Distribution Mockup](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Follow these steps to create the ratings distribution modal using the reference image as a guide:

   * Update the API to return additional data representing the ratings distribution.
   * Update the API Contract.
   * Update the contact in the storefront codebase.
   * Ask the storefront agent to use the reference image and updated API Contract to add the ratings distribution to the PDP page.

1. Observe the following changes in the codebase, and watch the Apparel page for updates:

   * How the agent interprets the visual mockup
   * Whether it uses appropriate HTML structure for accessibility
   * How it handles the positioning and interaction states

#### Troubleshooting

* If the modal does not appear, check the browser console for errors.
* If positioning is off, ask the agent to fix it using the following format:

   ```shell-session
   adjust the modal position to be...
   ```

![Rating Distribution Modal](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
 -->
