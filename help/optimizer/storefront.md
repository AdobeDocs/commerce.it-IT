---
title: Configurare la vetrina
description: Scopri come configurare la vetrina  [!DNL Adobe Commerce Optimizer] .
role: Developer
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 785bc4e71431a4e62df2ef7b0b75d66f8bf34579
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 0%

---

# Configurare la vetrina

>[!NOTE]
>
>Questa documentazione descrive un prodotto in fase di sviluppo con accesso anticipato e non riflette tutte le funzionalità previste per la disponibilità generale.

Questo tutorial illustra come configurare e utilizzare [Adobe Commerce Storefront con tecnologia Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) per creare una vetrina Commerce performante, scalabile e sicura basata sui dati dell&#39;istanza [!DNL Adobe Commerce Optimizer].


## Prerequisiti

* Assicurati di disporre di un account GitHub (github.com) in grado di creare archivi e configurato per lo sviluppo locale.

* Scopri i concetti e il flusso di lavoro per sviluppare vetrine di Commerce su Adobe Edge Delivery Services consultando la [Panoramica](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) nella documentazione di Adobe Commerce Storefront.
* Configurare l’ambiente di sviluppo


### Configurare l’ambiente di sviluppo

Installa Node.js e l&#39;estensione del browser Sidekick necessaria per sviluppare e testare la vetrina [!DNL Adobe Commerce Optimizer] su Edge Delivery Services.

#### Installare Node.js

Installare Node Version Manager (NVM) e la versione di Node.js richiesta (22.13.1 LTS).

1. Installazione di Node Version Manager (NVM).

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. Installare Node.js e NPM. Per ulteriori informazioni, vedere [Node.js](https://nodejs.org/en/).

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. Verificare l&#39;installazione.

   ```bash
   npm -v
   ```

>[!TIP]
>
>Risorse aggiuntive per l&#39;estensione e la personalizzazione della soluzione [!DNL Adobe Commerce Optimizer] sono disponibili tramite [App Builder per Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) e [API Mesh per Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Per informazioni su accesso e utilizzo, contatta il rappresentante del tuo account Adobe.

#### Installare Sidekick

Installa l’estensione del browser Sidekick per modificare, visualizzare in anteprima e pubblicare contenuti nella vetrina. Consulta le [istruzioni di installazione di Sidekick](https://www.aem.live/docs/sidekick#installation).

## Crea la vetrina

La vetrina creata per il progetto [!DNL Adobe Commerce Optimizer] utilizza una versione personalizzata di Adobe Commerce su Edge Delivery Services Storefront. La boilerplate è un insieme di file e cartelle che forniscono un punto di partenza per lo sviluppo della vetrina. Questo processo di installazione è diverso da quello standard per un [Adobe Commerce su Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

>[!NOTE]
>
>Questa esercitazione utilizza macOS, Chrome e Visual Studio Code come ambiente di sviluppo. La schermata acquisisce e le istruzioni riflettono tale configurazione. Puoi utilizzare un sistema operativo, un browser e un editor di codice diversi, ma l’interfaccia utente visualizzata e i passaggi da eseguire variano di conseguenza.

### Panoramica del flusso di lavoro

Segui questi passaggi per configurare una vetrina da usare con [!DNL Adobe Commerce Optimizer].

1. **[Creare un archivio del codice](#step-1-create-site-code-repository)**-Creare un archivio GitHub dal modello standard Adobe Commerce + Edge Delivery Services. Includi tutti i rami dall’archivio di origine.
1. **[Aggiorna il boilerplate della vetrina](#step-2-update-the-storefront-boilerplate)**-Aggiorna il modello boilerplate personalizzato nel ramo `aco` per collegare la cartella dei contenuti alla vetrina.
1. **[Distribuisci modifiche](#step-3-deploy-changes)**-Sovrascrivi il codice nel ramo `main` con il codice aggiornato dal ramo `aco`.
1. **[Aggiungi l&#39;app CodeSync](#step-5-add-the-aem-code-sync-app)**-Connetti l&#39;archivio al servizio Edge Delivery. Non connettere l&#39;app di sincronizzazione codice finché non hai completato la personalizzazione del codice sorgente e il codice è stato inviato al ramo `main`.
1. **[Aggiungi contenuto](#step-6-add-content)**-Utilizza lo strumento di clonazione dei contenuti demo per creare e inizializzare il contenuto della vetrina nell&#39;ambiente di authoring dei documenti ospitato su `https://da.live`.
1. **[Anteprima sito demo](#step-7-preview-demo-site)**-Connettersi al sito storefront per visualizzare il contenuto e i dati di esempio dall&#39;istanza demo [!DNL Adobe Commerce Optimizer].
1. **[Sviluppa nell&#39;ambiente locale](#step-8-develop-in-your-local-environment)**-Installa le dipendenze richieste. Avviare il server di sviluppo locale e aggiornare la configurazione della vetrina per connettersi all&#39;istanza [!DNL Adobe Commerce Optimizer] fornita da Adobe.
1. **[Passaggi successivi](#next-steps)**-Ulteriori informazioni sulla gestione e la visualizzazione di contenuti e dati nella vetrina.


### Passaggio 1: creare l’archivio del codice del sito

Crea un archivio GitHub per il codice boilerplate del sito per la vetrina utilizzando il modello Boilerplate di Edge Delivery Services + Adobe Commerce.

1. Accedi al tuo account GitHub.

1. Passa all’archivio GitHub [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce).

1. Selezionare **Usa questo modello**, quindi selezionare **Crea nuovo repository** dal menu a discesa.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   Viene visualizzata la pagina di configurazione del repository.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Completa il modulo di configurazione con i seguenti dettagli:

   * **Modello repository**—`hlxsites/aem-boilerplate-commerce` (impostazione predefinita).
   * **Includi tutti i rami**—Selezionare l&#39;opzione per includere tutti i rami.
   * **Proprietario**—La tua organizzazione o il tuo account (obbligatorio).
   * **Nome archivio**: un nome univoco per il nuovo archivio (obbligatorio).
   * **Descrizione**: breve descrizione dell&#39;archivio (facoltativo).
   * **Pubblico o Privato**. Adobe consiglia Pubblico (impostazione predefinita).

1. Selezionare **Crea repository**.

   Dopo alcuni minuti, viene aperto il nuovo archivio.

   Ignora le notifiche di richiesta pull visualizzate nell’interfaccia utente di GitHub.

### Passaggio 2: aggiornare la piastra di cottura della vetrina

Per aggiornare il codice boilerplate della vetrina sono necessarie le seguenti informazioni:

* **URL archivio GitHub dal passaggio 2**— `github.com/{ORG}/{SITE}`

   * `{ORG}` è il nome dell&#39;organizzazione o il nome utente per l&#39;archivio

   * `{SITE}` è il nome del repository

* **URL cartella contenuto dal passaggio 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` è l&#39;ID della cartella creata con i dati del contenuto di esempio.

#### Collegare l’archivio all’ambiente di authoring dei documenti

1. Clona l’archivio nel computer locale.

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   Se rilevi errori durante la clonazione dell&#39;archivio, consulta [Risoluzione dei problemi di clonazione](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) nella documentazione di GitHub.

1. Apri l’archivio nel terminale o nell’IDE.

1. Controlla il ramo `aco`

   ```bash
   git checkout aco
   ```

1. Creare il file di configurazione copiando il file `default-fstab.yaml` in `fstab.yaml`.

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. Aggiorna il punto di montaggio nel file di configurazione della vetrina in modo che punti all&#39;URL del contenuto.

   1. Apri il file di configurazione [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary).

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup
      
      folders:
       /products/: /products/default
      ```

   1. Sostituisci le stringhe `{ORG}` e `{SITE}` con i valori per l&#39;archivio GitHub creato per il codice standard.

      Ad esempio, il codice aggiornato dovrebbe essere simile al seguente.

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. Salva il file.

#### Configurare l&#39;estensione Sidekick

1. Aggiungi la configurazione del progetto per l’estensione Sidekick. Questa configurazione assicura la disponibilità di Sidekick per la gestione dei contenuti per il progetto storefront.

>[!NOTE]
>
>Verifica di aver installato l&#39;estensione [Sidekick](https://www.aem.live/docs/sidekick#installation) nel browser.

1. Aprire il file `tools/sidekick/config.json`.

   +++File di configurazione Sidekick

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   Per ulteriori informazioni, consulta la [documentazione della libreria Sidekick](https://www.aem.live/docs/sidekick-library).

+++

1. Aggiorna i valori chiave `url` con i valori per l&#39;archivio GitHub.

   * Sostituire la stringa `{ORG}` con l&#39;organizzazione o il nome utente del repository.

   * Sostituisci la stringa `{SITE}` con il nome dell&#39;archivio

   +++Esempio di file di configurazione aggiornato

   Se l&#39;archivio GitHub è denominato `aco-storefront` e l&#39;organizzazione è `early-adopter`, l&#39;URL aggiornato dovrebbe essere simile al seguente:

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

+++

1. Salva il file.

### Passaggio 3: distribuire le modifiche

Per utilizzare il codice boilerplate personalizzato della vetrina, sovrascrivi il codice nel ramo `main` con i tuoi aggiornamenti.

1. Dall’editor o dall’IDE, esegui il commit e salva i file aggiornati.

   ```bash
   git add .
   ```

1. Verifica di eseguire il commit dei due file aggiornati.

   ```bash
   git status
   On branch aco
   Your branch is up to date with 'origin/aco'.
   
   Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        new file:   fstab1.yaml
        modified:   tools/sidekick/config.json
   ```

1. Eseguire il commit delle modifiche nel ramo `aco`.

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Sovrascrivere la boilerplate nel ramo `main` con le modifiche nel ramo `aco`.

   ```bash
   git push origin aco:main -f
   ```

### Passaggio 5: aggiungere l’app AEM Code Sync

Connetti l’archivio al servizio Edge Delivery aggiungendo all’archivio l’app AEM Code Sync GitHub.

>[!IMPORTANT]
>
>Non connettere l’app di sincronizzazione codice finché non hai caricato il codice standard aggiornato nel ramo principale dell’archivio GitHub.

1. Apri la pagina di configurazione dell&#39;app [AEM Code Sync](https://github.com/apps/aem-code-sync).

1. Seleziona **Configura**, quindi esegui l&#39;autenticazione con l&#39;**organizzazione** o l&#39;**account** che contiene l&#39;archivio creato.

1. Dal modulo, scegliere **Seleziona solo archivi**, quindi selezionare il repository creato.

1. Seleziona **Installa** per aggiungere l&#39;app AEM Code Sync all&#39;archivio.

   Dovresti visualizzare un messaggio che informa che l’app è stata installata correttamente.

### Passaggio 6: aggiungere contenuti

Crea e inizializza il contenuto della vetrina nell&#39;ambiente di authoring dei documenti ospitato su `https://da.live` utilizzando lo strumento di clonazione del sito demo. Questo strumento importa il contenuto di esempio nell’ambiente di authoring dei documenti e completa il processo di anteprima e pubblicazione dei contenuti per tutti i documenti contenuti nel contenuto di esempio. Il contenuto di esempio include i layout di pagina, i banner, le etichette e altri elementi per popolare la vetrina.

1. Apri lo strumento [clone di contenuti demo](https://da.live/app/hlxsites/aem-boilerplate-commerce/tools/site-creator/site-creator).

   ![[!DNL AEM demo content clone tool]](./assets/storefront-demo-content-clone-tool.png){width="700" zoomable="yes"}

1. Incolla l&#39;URL GitHub per il progetto boilerplate della vetrina nel campo [!UICONTROL **URL GitHub del progetto**].


1. Importare, visualizzare in anteprima e pubblicare il contenuto nell&#39;ambiente di authoring dei documenti selezionando **Crea sito**.

   ![[!DNL AEM demo content clone tool]](./assets/storefront-edit-initial-content.png){width="700" zoomable="yes"}

   Dopo la creazione del sito, è possibile utilizzare i collegamenti nelle sezioni [!UICONTROL Edit content] e [!UICONTROL View Site] per esplorare la vetrina demo.

   I collegamenti principali al contenuto e al sito seguono questi formati:

   * **Cartella contenuto principale**— `https://da.live/#/{ORG}/{SITE}`
   * **Anteprima sito**—   `https://main--{SITE}--{ORG}.aem.page/`
   * **Produzione del sito:**— `https:/main--{SITE}--{ORG}.ae.live/`

1. Apri il collegamento alla cartella principale dei contenuti per visualizzarne il contenuto.

   ![[!DNL Storefront Document Author environment]](./assets/storefront-document-author-environment.png){width="700" zoomable="yes"}

   >[!TIP]
   >
   >Nella navigazione laterale, utilizza i collegamenti [!UICONTROL **Scopri**] e [!UICONTROL **Scopri**] per accedere alle risorse di apprendimento per la gestione del sito e del relativo contenuto.

### Passaggio 7: anteprima del sito demo

Verifica che sia il contenuto di esempio che i dati dell’istanza demo di Adobe Commerce Optimizer siano visualizzati correttamente.

* **Il contenuto di esempio** viene distribuito dalla cartella dei contenuti nell&#39;ambiente di authoring dei documenti. Include i layout di pagina, i banner e le etichette del sito.
* **I dati di esempio** sono forniti dall&#39;istanza demo [!DNL Adobe Commerce Optimizer]. I dati includono i dati di prodotto con attributi di prodotto, immagini, descrizioni dei prodotti e prezzi compilati in base ai valori di intestazione specificati nel file di configurazione della vetrina, `config.json`.

#### Connettiti al sito per visualizzare contenuti e dati di esempio

1. Visualizzare il sito passando a `https://main--{SITE}--{ORG}.aem.live`.

   Sostituisci `{ORG}` e `{SITE}` con l&#39;organizzazione e il nome per l&#39;archivio predefinito.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Se la pagina restituisce un 404, verifica quanto segue:

   * [Il punto di montaggio nel file `fstab.yaml` punta all&#39;URL di contenuto corretto](#link-the-repository-to-the-document-author-environment): `https://content.da.live/{ORG}/{SITE}/`
   * [Hai configurato l&#39;app di sincronizzazione codice per la connessione all&#39;archivio GitHub](#step-5%3A-add-the-aem-code-sync-app).
   * [Il contenuto è stato pubblicato nell&#39;ambiente di authoring dei documenti mediante lo strumento di clonazione dei contenuti demo](#step-6%3A-add-content-documents-for-your-storefront).


1. Visualizza i dati del catalogo di esempio provenienti dall’istanza predefinita di Commerce Optimizer.

   1. Nell&#39;intestazione della vetrina, fare clic sulla lente di ingrandimento per cercare `tires`.

      ![[!DNL View product list page]](./assets/storefront-site-with-aco-data.png){width="675" zoomable="yes"}

   1. Premi **Invio** per visualizzare la pagina dei risultati della ricerca.

      ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

      I componenti della pagina dei risultati di ricerca sono definiti dal documento di contenuto `search`. I dati dei risultati della ricerca vengono compilati in base alla configurazione della vetrina in `config.json`.

   1. Per visualizzare la pagina dei dettagli del prodotto, seleziona uno dei pneumatici presenti nella pagina.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

      I componenti della pagina dei dettagli del prodotto sono definiti dal documento di contenuto `default` nella cartella `product`.

### Passaggio 8: sviluppare nell’ambiente locale

In questa sezione aggiorni la configurazione della vetrina dall’ambiente di sviluppo locale.

* Aggiornare la configurazione storefront per connettersi all&#39;endpoint GraphQL per l&#39;istanza [!DNL Adobe Commerce Optimizer] fornita da Adobe.
* Aggiorna i valori dell’intestazione per recuperare i dati dall’istanza.

#### Avvia sviluppo locale

1. Nell’IDE, estrai il ramo principale e ripristinalo all’ultimo commit sul ramo remoto.

   ```bash
   git checkout main
   git reset --hard origin/main
   ```

1. Installa le dipendenze richieste.

   ```bash
   npm install
   ```

1. Avvia il server di sviluppo locale.

   ```bash
   npm start
   ```

   La prima pagina della vetrina dovrebbe essere visibile nel browser all&#39;indirizzo `http://localhost:3000`.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### Aggiornare la configurazione della vetrina

Aggiorna il file di configurazione della vetrina e visualizza in anteprima le modifiche nell&#39;ambiente di sviluppo locale.

1. Nell&#39;IDE, aggiornare la configurazione della vetrina per connettersi all&#39;istanza [!DNL Adobe Commerce Optimizer] fornita da Adobe.

   1. Aprire il file `config.json`.

   1. Aggiorna i seguenti valori utilizzando l&#39;endpoint per l&#39;istanza [!DNL Adobe Commerce Optimizer]:

      * **`commerce-endpoint`**-Sostituisci il valore esistente con l&#39;URL dell&#39;endpoint.

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql"
        ```

      * **`ac-environment-id`** - Sostituisci il valore esistente con l&#39;ID tenant dell&#39;URL dell&#39;endpoint.

        ```json
        "ac-environment-id": "{tenantId}"
        ```

   1. Salva il file.

      Se l&#39;anteprima locale funziona correttamente, gli aggiornamenti vengono applicati alla vetrina locale.

1. Controlla il sito per visualizzare i risultati della modifica della configurazione.

   1. Nel browser passare a `http://localhost:3000` e aggiornare la pagina.

   1. Nell&#39;intestazione della vetrina, fare clic sulla lente di ingrandimento per cercare `tires`.

      ![Cerca pneumatici](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

   1. Premere **Invio** per visualizzare la pagina Risultati ricerca.

      ![Risultati di ricerca vuoti con valori di intestazione non validi](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      La ricerca non restituisce alcun risultato perché i valori di intestazione nel file di configurazione della vetrina sono basati sull’istanza predefinita. Ora che la configurazione punta all&#39;istanza [!DNL Adobe Commerce Optimizer] fornita, tali valori non sono validi.

### Passaggi successivi

Per ulteriori informazioni sulla gestione e la visualizzazione di contenuti e dati nella vetrina, consulta il [caso d&#39;uso end-to-end dell&#39;amministratore di store e catalogo](./use-case/admin-use-case.md).

>[!MORELIKETHIS]
>
> Per ulteriori informazioni sull&#39;aggiornamento del contenuto del sito e sull&#39;integrazione con i componenti front-end e i dati back-end di Commerce, consulta la [documentazione di Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).
