---
title: Configurare la vetrina
description: Scopri come configurare la vetrina  [!DNL Adobe Commerce Optimizer] .
role: Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Configurare la vetrina

Questo tutorial illustra come configurare e utilizzare [Adobe Commerce Storefront con tecnologia Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) per creare una vetrina Commerce performante, scalabile e sicura basata sui dati dell&#39;istanza [!DNL Adobe Commerce Optimizer].


## Prerequisiti

- Assicurati di disporre di un account GitHub (github.com) in grado di creare archivi e configurato per lo sviluppo locale.

- Scopri i concetti e il flusso di lavoro per sviluppare vetrine di Commerce su Adobe Edge Delivery Services consultando la [Panoramica](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) nella documentazione di Adobe Commerce Storefront.
- Configurare l’ambiente di sviluppo


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

   - **Modello repository**—`hlxsites/aem-boilerplate-commerce` (impostazione predefinita).
   - **Includi tutti i rami**—Selezionare l&#39;opzione per includere tutti i rami.
   - **Proprietario**—La tua organizzazione o il tuo account (obbligatorio).
   - **Nome archivio**: un nome univoco per il nuovo archivio (obbligatorio).
   - **Descrizione**: breve descrizione dell&#39;archivio (facoltativo).
   - **Pubblico o Privato**. Adobe consiglia Pubblico (impostazione predefinita).

1. Selezionare **Crea repository**.

   Dopo alcuni minuti, viene aperto il nuovo archivio.

   Ignora le notifiche di richiesta pull visualizzate nell’interfaccia utente di GitHub.

### Passaggio 2: aggiornare la piastra di cottura della vetrina

Per aggiornare il codice boilerplate della vetrina sono necessarie le seguenti informazioni:

- **URL archivio GitHub dal passaggio 2**— `github.com/{ORG}/{SITE}`
   - `{ORG}` è il nome dell&#39;organizzazione o il nome utente per l&#39;archivio
   - `{SITE}` è il nome del repository
- **URL cartella contenuto dal passaggio 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`
   - `{YOUR_FOLDER_ID}` è l&#39;ID della cartella creata con i dati del contenuto di esempio.

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

   - Sostituire la stringa `{ORG}` con l&#39;organizzazione o il nome utente del repository.

   - Sostituisci la stringa `{SITE}` con il nome dell&#39;archivio

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
