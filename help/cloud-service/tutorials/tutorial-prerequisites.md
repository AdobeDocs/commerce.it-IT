---
title: Prerequisiti del tutorial
description: Scopri i prerequisiti per il laboratorio di estensione delle valutazioni.
feature: App Builder, Cloud
role: Developer
level: Intermediate
source-git-commit: 68e34cecbc1b16194ccc2e0296c2d66f37855b7c
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Prerequisiti del tutorial

In questa pagina sono elencati i prerequisiti e i passaggi di configurazione per le esercitazioni di [!DNL Adobe Commerce as a Cloud Service], ad esempio l&#39;esercitazione sull&#39;estensione delle [classificazioni](./ratings-extension.md) e l&#39;esercitazione sull&#39;estensione del [metodo di spedizione](./shipping-method-extension.md).

## Prerequisiti per Adobe Commerce as a Cloud Service

* Installa [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Installa i plug-in [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce), [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime) e [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev):

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

* Scaricare un IDE basato sull&#39;intelligenza artificiale, ad esempio [Cursor](https://cursor.com/download) (scelta consigliata), sono supportati anche altri IDE, come Claude Code, Gemini CLI o Copilot, ma potrebbero essere necessarie modifiche ai prompt e ad altri passaggi dell&#39;esercitazione.

### Prerequisiti di Adobe Developer Console

1. Passa a [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Accedi utilizzando l’e-mail e la password.

#### Crea un nuovo progetto

1. Passa a [Adobe Developer Console](https://developer.adobe.com/).
1. Fai clic su [!UICONTROL **Crea progetto da un modello**].
1. Seleziona il modello [!UICONTROL **App Builder**].
1. Immetti un [!UICONTROL **Titolo progetto**] e un [!UICONTROL **Nome app**].
1. Verificare che la casella di controllo **[!UICONTROL Include Runtime]** sia contrassegnata.

   ![Creazione di un progetto Adobe Developer Console con modello App Builder selezionato](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Fai clic su [!UICONTROL **Salva**].

#### Aggiungere API all’area di lavoro

1. Fare clic sull&#39;area di lavoro [!UICONTROL **Stage**] e quindi ripetere i passaggi seguenti per ogni API.

   ![Area di lavoro di staging con opzione Aggiungi servizio per API](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Fai clic su [!UICONTROL **Aggiungi servizio**] e seleziona [!UICONTROL **API**].

1. Seleziona una delle seguenti API. Dovrai ripetere questo processo per ogni API elencata di seguito:

   * [!UICONTROL **Filtro Adobe Services**]:
      * [!UICONTROL **API di gestione I/O**]
      * [!UICONTROL **Eventi I/O**] API
   * [!UICONTROL **Filtro Experience Cloud**]:
      * API [!UICONTROL **Adobe I/O Events per Adobe Commerce**]

1. Fai clic su [!UICONTROL **Avanti**].

1. Fai clic su [!UICONTROL **Salva API configurata**].

1. Ripeti i passaggi precedenti fino a quando tutte le API non vengono aggiunte all’area di lavoro.

   ![Workspace con tutte le API richieste aggiunte](../assets/apis-added.png){width="600" zoomable="yes"}

### Configurare Adobe I/O CLI

1. Cancella eventuali configurazioni esistenti:

   ```bash
   aio config clear
   ```

   Accedi utilizzando [!DNL Adobe I/O CLI]:

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

   ![Terminale che mostra la selezione del progetto e dell&#39;area di lavoro dell&#39;organizzazione CLI di Adobe I/O](../assets/cli-configuration.png){width="600" zoomable="yes"}

### Clonare i kit di avvio

Clona uno dei seguenti archivi di Commerce Starter Kit per l’estensione che stai creando e prepara il progetto:

Kit di avvio dell’integrazione:

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

Kit di avvio per il pagamento:

```bash
git clone https://github.com/adobe/commerce-checkout-starter-kit.git extension
cd extension
```

>[!BEGINTABS]

>[!TAB Kit di avvio dell&#39;integrazione]

### Creare un file .env

Creare il file di configurazione dell’ambiente:

```bash
cp env.dist .env
```

Apri il file `.env` in un editor di testo e aggiungi le seguenti credenziali OAuth:

```shell-session
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

È possibile copiare questi valori dalla pagina **[!UICONTROL Credential details]** in [Developer Console](https://developer.adobe.com/) facendo clic sulla scheda **[!UICONTROL OAuth Server-to-Server]** nell&#39;area di lavoro.

![Pagina credenziali server-to-server OAuth in Adobe Developer Console](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Aggiungere la configurazione Commerce

Aggiungi i seguenti dettagli dell&#39;istanza di Commerce al file `.env`:

```shell-session
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

Per trovare questi valori:

1. Passa a [istanze del servizio Commerce Cloud](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Fai clic sull’icona delle informazioni accanto all’istanza.
1. Copiare l&#39;endpoint REST come `COMMERCE_BASE_URL`.
1. Copiare l&#39;endpoint GraphQL come `COMMERCE_GRAPHQL_ENDPOINT`.

#### Imposta prefisso evento

Imposta un valore temporaneo per il prefisso dell&#39;evento:

```shell-session
EVENT_PREFIX=test
```

### Scarica configurazione area di lavoro

Esegui il comando seguente per scaricare il file di configurazione dell’area di lavoro:

```bash
aio console workspace download workspace.json
```

Copiare il file di configurazione dell&#39;area di lavoro nella directory `scripts`:

```bash
cp workspace.json scripts/
```

### Connetti area di lavoro locale a area di lavoro remota

Collega il progetto locale all’area di lavoro remota:

```bash
aio app use workspace.json -m
```

![Terminale che mostra la connessione all&#39;area di lavoro riuscita con il comando aio app use](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!TAB Kit di avvio estrazione]

### Connetti area di lavoro locale a area di lavoro remota

Collega il progetto locale all’area di lavoro remota. Dalla directory principale del progetto (la cartella `extension`), eseguire:

```bash
aio app use --merge
```

Quando richiesto, scegli l’opzione che utilizza l’organizzazione, il progetto e l’area di lavoro selezionati durante la configurazione di Adobe I/O CLI. In questo modo la configurazione dell’area di lavoro viene scritta nell’app in modo che l’area di lavoro venga utilizzata sia per la distribuzione che per lo sviluppo locale.

![Terminale che mostra la connessione all&#39;area di lavoro riuscita con il comando aio app use](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!ENDTABS]

### Installare gli strumenti di IA per l’estensibilità

Questo processo crea la configurazione MCP (`.<agent>/mcp.json`), la directory delle abilità (`.<agent>/skills/`) e aggiunge `AGENTS.md` alla directory principale del progetto. Verrà richiesto di scegliere un kit di avvio, un agente di codifica e un gestore di pacchetti.


1. Impostare gli strumenti di sviluppo assistito da IA nella cartella `extension` utilizzando i seguenti comandi:

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![Terminale che mostra l&#39;output del comando di installazione degli strumenti di estensibilità AI](../assets/install-ai-tools.png){width="600" zoomable="yes"}

1. Al termine dell’installazione, riavvia l’agente di codifica per consentirgli di caricare i nuovi strumenti e le nuove competenze MCP. Gli strumenti Commerce App Builder sono ora disponibili nel tuo ambiente.

   >[!NOTE]
   >
   >Se viene visualizzato un avviso che indica che non sono state trovate abilità per il kit di avvio, si è verificato un errore, spesso perché la configurazione veniva eseguita in una cartella diversa da quella in cui è stato clonato il kit di avvio. Eseguire `aio commerce extensibility tools-setup` dalla cartella `extension` (radice del progetto del kit di avvio) e selezionare il kit di avvio appropriato quando richiesto.

   ![Terminale che mostra la configurazione degli strumenti di estensibilità AI con il kit di avvio selezionato](../assets/tools-setup-checkout.png){width="600" zoomable="yes"}

<!--
## Storefront prerequisites

The following items are required to complete the [storefront](./ratings-extension.md#connect-to-the-storefront) section of [this tutorial](./ratings-extension.md) and see the product ratings in your store.

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
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront

### Get the project files

You can obtain the project files using one of the following methods:

#### Option A: Clone the repository (recommended)

If you have [!DNL Git] installed, open your terminal and clone the repository:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

#### Option B: Download the zip file

If you do not have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ```

### Install root dependencies

Install the main project dependencies:

```bash
npm install
```

This will install all the necessary packages for the storefront application.

### Install MCP server dependencies

Navigate to the MCP server directory and install its dependencies:

```bash
cd mcp-server
npm install
cd ..
```

### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create an `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values:

```env
RAG_MODE=worker
WORKER_RAG_URL=
```

### Enable MCP in Cursor

The Model Context Protocol (MCP) server provides AI agents with access to [!DNL Adobe Commerce] Storefront documentation.

#### Open Cursor MCP settings

![Open Cursor MCP Settings](../assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Open [!DNL Cursor].
1. Navigate to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

#### Enable and configure MCP features

The project includes an MCP configuration file at `.cursor/mcp.json`. This file should already be configured to use the local MCP server.

Verify the MCP configuration:

1. Ensure the "commerce-documentation-rag" server is listed and enabled

The configuration should look similar to this:

![MCP Configuration](../assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>The `start-mcp.sh` script will automatically load the environment variables from your `.env` file in the `mcp-server` directory.

#### Restart Cursor

After enabling MCP and configuring the server:

1. Quit [!DNL Cursor] completely.
1. Reopen [!DNL Cursor] and open the `aem-boilerplate-commerce` project.

#### Verify MCP connection

Check that the MCP server is running correctly:

1. Open a new chat in [!DNL Cursor].
1. Look for an indicator showing the MCP server is connected. This indicator is typically located in the chat interface.
1. Try entering a prompt like the following:

   ```shell-session
   Search the storefront docs for information about slots
   ```

If the MCP server is working, you should see relevant documentation results.

![MCP Connection Verified](../assets/mcp-connection-verified.png){width="600" zoomable="yes"}

If this works, you are ready to continue with the [tutorial](./ratings-extension.md).
 -->
