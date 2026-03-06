---
title: Prerequisiti del tutorial
description: Scopri i prerequisiti e i passaggi di configurazione per le esercitazioni di Adobe Commerce as a Cloud Service, inclusi gli strumenti di sviluppo per estensioni e vetrine.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
source-git-commit: 1848c9dda4a1976e1bccb4d1f9d5a2e21540fc0b
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 0%

---

# Prerequisiti del tutorial

In questa pagina sono elencati i prerequisiti e i passaggi di configurazione per le esercitazioni di [!DNL Adobe Commerce as a Cloud Service], ad esempio l&#39;esercitazione sull&#39;estensione delle [classificazioni](./ratings-extension.md) e l&#39;esercitazione sull&#39;estensione del [metodo di spedizione](./shipping-method-extension.md).

## Prerequisiti generali

In questo tutorial sono necessari i seguenti strumenti per lo sviluppo sia di estensioni che di vetrine.

* [!DNL Node.js] (versione `22.x.x`) e npm (`9.0.0` o successiva): Verificare l&#39;installazione utilizzando il comando seguente:

  ```bash
  node --version
  npm --version
  ```

* Installa [Git](https://git-scm.com). Verificare l&#39;installazione:

  ```bash
  git --version
  ```

* Guscio Bash
   * macOS/Linux: nessuna installazione richiesta
   * Windows: utilizzare [Git Bash](https://git-scm.com/install) o [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* Scarica un IDE basato su IA, ad esempio [Cursore](https://cursor.com/download) (consigliato). Sono supportati anche altri IDE, come Claude Code, Gemini CLI o Copilot, ma potrebbero richiedere modifiche ai prompt e ad altri passaggi dell’esercitazione.

## [!DNL Adobe Commerce as a Cloud Service] prerequisiti

* Installa [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Installa i plug-in [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce), [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime) e [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev):

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

### Prerequisiti di Adobe Developer Console

Configura un progetto in Adobe Developer Console con le API e le credenziali richieste.

1. Passa a [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Accedi utilizzando l’e-mail e la password.

#### Crea un nuovo progetto

Crea un progetto App Builder in Adobe Developer Console per ospitare la tua estensione.

1. Passa a [Adobe Developer Console](https://developer.adobe.com/).
1. Fare clic su **[!UICONTROL Create project from a template]**.
1. Selezionare il modello **[!UICONTROL App Builder]**.
1. Immettere **[!UICONTROL Project Title]** e **[!UICONTROL App Name]**.
1. Verificare che la casella di controllo **[!UICONTROL Include Runtime]** sia contrassegnata.

   ![Creazione di un progetto Adobe Developer Console con modello App Builder selezionato](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Fare clic su **[!UICONTROL Save]**.

#### Aggiungere API all’area di lavoro

Aggiungi le API richieste all’area di lavoro di Stage per la gestione degli eventi e l’integrazione con Commerce.

1. Fare clic sull&#39;area di lavoro **[!UICONTROL Stage]** e quindi ripetere i passaggi seguenti per ogni API.

   ![Area di lavoro di staging con opzione Aggiungi servizio per API](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Fare clic su **[!UICONTROL Add Service]** e selezionare **[!UICONTROL API]**.

1. Seleziona una delle seguenti API. Ripeti questo processo per ogni API elencata di seguito:

   * Filtro **[!UICONTROL Adobe Services]**:
      * **[!UICONTROL I/O Management API]**
      * API **[!UICONTROL I/O Events]**
   * Filtro **[!UICONTROL Experience Cloud]**:
      * API **[!UICONTROL Adobe I/O Events for Adobe Commerce]**

1. Fare clic su **[!UICONTROL Next]**.

1. Fare clic su **[!UICONTROL Save configured API]**.

1. Ripeti i passaggi precedenti fino a aggiungere tutte le API all’area di lavoro.

   ![Workspace con tutte le API richieste aggiunte](../assets/apis-added.png){width="600" zoomable="yes"}

### Configurare Adobe I/O CLI

Connetti [!DNL Adobe I/O CLI] all&#39;organizzazione, al progetto e all&#39;area di lavoro.

1. Cancella eventuali configurazioni esistenti:

   ```bash
   aio config clear
   ```

1. Accedi utilizzando [!DNL Adobe I/O CLI]:

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

```bash
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

Copiare questi valori dalla pagina **[!UICONTROL Credential details]** in [Developer Console](https://developer.adobe.com/) facendo clic sulla scheda **[!UICONTROL OAuth Server-to-Server]** nell&#39;area di lavoro.

![Pagina credenziali server-to-server OAuth in Adobe Developer Console](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Aggiungere la configurazione Commerce

Aggiungi i seguenti dettagli dell&#39;istanza di Commerce al file `.env`:

```bash
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

Per trovare questi valori:

1. Passa a [istanze del servizio Commerce Cloud](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Fai clic sull’icona delle informazioni accanto all’istanza.
1. Copiare l&#39;endpoint REST come `COMMERCE_BASE_URL`.
1. Copiare l&#39;endpoint GraphQL come `COMMERCE_GRAPHQL_ENDPOINT`.

#### Impostare il prefisso dell’evento

Imposta un valore temporaneo per il prefisso dell&#39;evento:

```bash
EVENT_PREFIX=test
```

### Scarica la configurazione dell’area di lavoro

Esegui il comando seguente per scaricare il file di configurazione dell’area di lavoro:

```bash
aio console workspace download workspace.json
```

Copiare il file di configurazione dell&#39;area di lavoro nella directory `scripts`:

```bash
cp workspace.json scripts/
```

### Connetti l&#39;area di lavoro locale all&#39;area di lavoro remota

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

### Installare gli strumenti di extensibility AI

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

## Prerequisiti per la vetrina

I seguenti elementi sono necessari per completare la sezione [storefront](./ratings-extension.md#connect-to-the-storefront) del [tutorial sull&#39;estensione delle valutazioni](./ratings-extension.md) e visualizzare le valutazioni del prodotto nel tuo store.

* [Google Chrome](https://www.google.com/chrome/) - Necessario per testare la vetrina

* Progetto vetrina connesso all&#39;istanza [!DNL Commerce]. Se non disponi di un progetto storefront, segui i passaggi descritti in [Creare una vetrina](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=it){target="_blank"}, inclusa la sezione [Collegare l&#39;archivio ai dati di e-commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=it#link-repo-to-commerce-data){target="_blank"}.

### Clona l’archivio della vetrina

Apri il terminale e clona l’archivio:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

### Installare le dipendenze

Installare le dipendenze del progetto:

```bash
npm install
```

### Installare gli strumenti di IA per la vetrina

Configurare gli strumenti di sviluppo assistiti da IA nella cartella `storefront`. Esegui il seguente comando dalla directory principale del progetto boilerplate:

```bash
aio commerce extensibility tools-setup
```

Il comando illustra due prompt:

1. **Selezionare un kit di avvio**. Scegliere **AEM Boilerplate Commerce**.

1. **Selezionare l&#39;agente di codifica** — Scegliere l&#39;agente dall&#39;elenco degli agenti supportati.

Il comando installa il pacchetto `@adobe-commerce/commerce-extensibility-tools` come dipendenza di sviluppo, copia i file delle abilità nella directory delle abilità dell&#39;agente e configura MCP (Model Context Protocol) in modo che l&#39;agente possa accedere agli strumenti di ricerca della documentazione di Commerce.