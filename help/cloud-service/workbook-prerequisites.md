---
title: Prerequisiti per il laboratorio di ADL Commerce
description: Scopri i prerequisiti per il laboratorio di estensione delle valutazioni.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ba4d096bcb99420c029d0b0674fc00f1f1445cea
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Adobe Developers Live - Prerequisiti per il laboratorio Adobe Commerce

In questa pagina sono elencati i prerequisiti e gli altri passaggi di configurazione manuale per il [laboratorio di estensioni delle classificazioni](./workbook.md). Il laboratorio contiene anche uno script che automatizza la maggior parte di questi passaggi.

## Prerequisiti per l’estensione

Prima di iniziare, completa i seguenti prerequisiti:

* Installa [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Installare il plug-in Commerce

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* È inoltre possibile scaricare un IDE basato sull&#39;intelligenza artificiale, ad esempio [Cursor](https://cursor.com/download) (scelta consigliata), altri IDE, ad esempio Claude Code, Gemini CLI o Copilot, ma potrebbe essere necessario apportare modifiche ai prompt e ad altri passaggi di questa esercitazione.
<!-- 
### Create a new project on Adobe Developer Console

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Create project with App Builder template](./assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click **Save**.

### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![APIs added to workspace](./assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select the [!UICONTROL **Adobe Services**] filter and select one of the following APIs:

   * [!UICONTROL **I/O Management API**]
   * [!UICONTROL **I/O Events**]

1. Select the [!UICONTROL **Experience Cloud**] filter and select one of the following APIs:

   * [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![APIs added to workspace](./assets/apis-added.png){width="600" zoomable="yes"} -->

### Configurare la CLI AIO

1. Cancella la configurazione esistente:

   ```bash
   aio config clear
   ```

   Effettuate il login utilizzando la CLI AIO:

   ```bash
   aio auth login -f
   ```

1. Seleziona l’organizzazione, il progetto e l’area di lavoro utilizzando ciascuno dei seguenti comandi:

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![Configurazione CLI](./assets/cli-configuration.png){width="600" zoomable="yes"}

### Kit di avvio per l’integrazione dei cloni

Clona l’archivio del kit di avvio dell’integrazione di Commerce e prepara il progetto:

```bash
git clone --branch adl https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Kit di avvio clone](./assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Creare il file .env

Creare il file di configurazione dell’ambiente:

```bash
cp env.dist .env
```

<!-- Open the `.env` file in a text editor and add the following OAuth credentials:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth credentials](./assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Go to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your assigned seat.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL Endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```text
EVENT_PREFIX=test
```
 -->

### Scarica configurazione area di lavoro

Esegui il comando seguente per scaricare il file di configurazione dell’area di lavoro:

```bash
aio console workspace download workspace.json
```

### Connetti area di lavoro locale a area di lavoro remota

Collega il progetto locale all’area di lavoro remota:

```bash
aio app use workspace.json -m
```

![Connetti all&#39;area di lavoro](./assets/connect-workspace.png){width="600" zoomable="yes"}

## Prerequisiti per la vetrina

I seguenti elementi sono necessari per completare la sezione [storefront](#connect-to-the-storefront) di questo tutorial e visualizzare le valutazioni del prodotto nel tuo archivio.
<!-- 
* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com) (Optional) - Required only if [cloning the repository directly](#option-a-clone-the-repository-recommended)(recommended), not needed if you [download the zip file](#option-b-download-the-zip-file). Verify your installation:

  ```bash
  git --version
  ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront -->

### Ottieni i file di progetto

È possibile ottenere i file di progetto in uno dei due modi seguenti:

<!-- 
#### Option A: Clone the repository (recommended) -->

Se hai installato [!DNL Git], apri il terminale e clona l&#39;archivio:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

<!-- #### Option B: Download the zip file

If you don't have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ``` -->

### Installare le dipendenze radice

Installa le dipendenze principali del progetto:

```bash
npm install
```

Verranno installati tutti i pacchetti necessari per l&#39;applicazione storefront.

### Installare le dipendenze del server MCP

Passa alla directory del server MCP e installane le dipendenze:

```bash
cd mcp-server
npm install
cd ..
```

<!-- ### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create a `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values (we'll provide the actual URL during the lab):

```env
RAG_MODE=worker
WORKER_RAG_URL=<provided-during-lab>
```

>[!NOTE]
>
>The actual value for `WORKER_RAG_URL` will be provided by the lab facilitator at the start of the session. -->

### Abilita MCP nel cursore

Il server MCP (Model Context Protocol) fornisce agli agenti IA l&#39;accesso alla documentazione Storefront [!DNL Adobe Commerce].

#### Apri impostazioni MCP cursore

![Apri impostazioni MCP cursore](./assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Apri [!DNL Cursor]
1. Vai a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**

#### Abilitare e configurare le funzioni MCP

Il progetto include un file di configurazione MCP in `.cursor/mcp.json`. Questo file deve essere già configurato per l&#39;utilizzo del server MCP locale.

Verifica la configurazione MCP:

1. Verificare che il server &quot;commerce-documentation-rag&quot; sia elencato e abilitato

La configurazione deve essere simile alla seguente:

![Configurazione MCP](./assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Lo script `start-mcp.sh` carica automaticamente le variabili di ambiente dal file `.env` nella directory `mcp-server`.

#### Riavvia cursore

Dopo aver abilitato MCP e configurato il server:

1. Esci completamente da [!DNL Cursor]
1. Riaprire [!DNL Cursor] e aprire il progetto `aem-boilerplate-commerce`

#### Verifica connessione MCP

Verifica che il server MCP funzioni correttamente:

1. Apri una nuova chat in [!DNL Cursor]
1. Cerca un indicatore che mostra che il server MCP è connesso (di solito nell’interfaccia di chat)
1. Prova a porre una domanda del tipo: &quot;Cerca nei documenti della vetrina informazioni sugli slot&quot;

Se il server MCP funziona, dovresti vedere i risultati della documentazione pertinenti.

![Connessione MCP verificata](./assets/mcp-connection-verified.png){width="600" zoomable="yes"}

### Avviare il server di sviluppo

Avvia il server di sviluppo locale:

```bash
npm run start
```

Il server di sviluppo verrà avviato alle `http://localhost:3000`.

Passare alla pagina Abbigliamento in `http://localhost:3000/apparel`.

![Server di sviluppo in esecuzione](./assets/development-server-running.png){width="600" zoomable="yes"}
