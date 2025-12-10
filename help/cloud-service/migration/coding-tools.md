---
title: Strumenti di codifica IA per le estensioni
description: Scopri come utilizzare gli strumenti di intelligenza artificiale per creare estensioni Commerce App Builder.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 8f7b5536388e8f4cb1e763b430bdca8644d1da5c
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 0%

---

# Strumenti di codifica IA per le estensioni

Durante la migrazione a [!DNL Adobe Commerce as a Cloud Service], è possibile utilizzare gli strumenti di codifica AI per convertire le estensioni PHP [!DNL Adobe Commerce] esistenti in estensioni [!DNL Adobe Developer App Builder]. Può essere utilizzato anche per creare nuove estensioni [!DNL App Builder].

L’utilizzo degli strumenti di codifica AI offre i seguenti vantaggi:

* **Flusso di lavoro di sviluppo avanzato**: strumenti di sviluppo Adobe Commerce integrati.
* **Assistenza basata su IA**: generazione e debug del codice in base al contesto.
* **Funzioni specifiche di Commerce**: strumenti specializzati per lo sviluppo Adobe Commerce App Builder.
* **Flussi di lavoro automatizzati**: processi di sviluppo e distribuzione semplificati.

## Prerequisiti

* Uno dei seguenti agenti di codifica:
   * [Cursore](https://cursor.com/download) (consigliato)
   * [Copilota Github](https://github.com/features/copilot)
   * [CLI Gemini Google](https://github.com/google-gemini/gemini-cli)
   * [Codice Claude](https://www.claude.com/product/claude-code)
* [Node.js](https://nodejs.org/en/download): versione LTS
* Gestione pacchetti: [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) o [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git): per la clonazione dell&#39;archivio e il controllo della versione

## Installazione

1. Installa la [Adobe I/O CLI](https://github.com/adobe/aio-cli) più recente a livello globale:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Installa i seguenti plug-in:

   * [Commerce Adobe I/O CLI](https://github.com/adobe-commerce/aio-cli-plugin-commerce)
   * [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime)
   * [CLI di App Builder](https://github.com/adobe/aio-cli-plugin-app-dev)

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
   ```

1. Clona il [kit di avvio per l&#39;integrazione di Commerce](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration):

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. Passare alla directory del kit di avvio:

   ```bash
   cd commerce-integration-starter-kit
   ```

1. Installare gli strumenti di estensibilità di Commerce AI eseguendo il comando di installazione interattivo:

   ```bash
   aio commerce extensibility tools-setup
   ```

Il processo di configurazione richiede di specificare le opzioni di configurazione. Per il percorso di installazione, scegliere &quot;Directory corrente&quot; per installare gli strumenti nell&#39;area di lavoro corrente:

```terminal
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

Quando si seleziona l&#39;agente di codifica, Adobe consiglia di selezionare `Cursor` per la migliore esperienza di sviluppo:

```terminal
? Which coding agent would you like to use?
❯ Cursor
  Copilot
  Gemini CLI
  Claude Code
```

Quando si seleziona Gestione pacchetti, Adobe consiglia di utilizzare `npm` per coerenza:

```terminal
? Which package manager would you like to use?
❯ npm
  yarn
```

1. Dopo aver installato correttamente gli strumenti di codifica, il processo di installazione configura:

   * Integrazione del server MCP per lo sviluppo Adobe Commerce
   * Regole IDE del cursore per un’esperienza di sviluppo avanzata
   * Strumenti di sviluppo e flussi di lavoro specifici per Commerce

   I seguenti file vengono aggiunti all&#39;area di lavoro:

   **Cursore**

   * Configurazione MCP: `.cursor/mcp.json`
   * Directory regole: `.cursor/rules/`

   **Copilota**

   * Configurazione MCP: `.vscode/mcp.json`
   * Directory regole: `.github/copilot-instructions.md`

>[!NOTE]
>
>Prima di distribuire il progetto, è necessario completare le seguenti attività di configurazione:
>
>* Accedi a [Adobe Developer Console](https://developer.adobe.com/console) utilizzando Adobe I/O CLI.
>* Crea un progetto App Builder (vedi [Configurazione del progetto](https://developer.adobe.com/commerce/extensibility/events/project-setup)).
>* Configurare le variabili di ambiente in un file `.env`.
>
>Puoi completare questi passaggi di configurazione manualmente o sfruttare gli strumenti di codifica IA per guidarti nel processo. Per istruzioni di configurazione dettagliate, consulta [Creare un&#39;integrazione](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/).

## Configurazione post-installazione

### Accedi a [!DNL Adobe I/O CLI]

Dopo aver installato [!DNL Adobe I/O CLI], è necessario accedere in qualsiasi momento per utilizzare il server MCP.

```bash
aio auth login
```

Per verificare di aver eseguito l&#39;accesso, eseguire il comando seguente:

```bash
aio where
```

In caso di problemi, disconnettersi e accedere nuovamente:

```bash
aio auth logout
aio auth login
```

>[!NOTE]
>
>Alcune funzionalità del server MCP funzioneranno senza effettuare l’accesso, ma il servizio RAG (Retrieval-Augmented Generation) non funzionerà. Il servizio RAG fornisce all’agente di codifica AI l’accesso in tempo reale al set completo della documentazione di Adobe Commerce, consentendogli di rispondere alle domande e generare il codice in base alle procedure di sviluppo Commerce, alle API e ai pattern architetturali correnti.
>
>In una versione futura, il servizio RAG sarà accessibile in modo indipendente senza la necessità di installare altri strumenti.

### Cursore

1. Riavvia l’IDE cursore per caricare i nuovi strumenti e la nuova configurazione MCP.

1. Verificare l&#39;installazione confermando che le regole sono presenti nella cartella `.cursor/rules/`.

1. Attiva il server MCP:

   * Apri le impostazioni MCP del cursore utilizzando **Cmd+Maiusc+P** (macOS) o **Ctrl+Maiusc+P** (Windows e Linux).
   * Tipo **Visualizza: apri impostazioni MCP**
   * Individua **Commerce-Extensibility MCP Server** nell&#39;elenco
   * Attiva/disattiva il server **ON** per abilitare gli strumenti di codifica

1. Verifica dello stato del server: il server MCP di estensibilità di Commerce deve essere visualizzato come:

   ```terminal
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

1. Utilizza il seguente prompt per verificare se l’agente utilizza il server MCP. In caso contrario, chiedi esplicitamente all’agente di utilizzare gli strumenti MCP disponibili.

```terminal
What are the differences between Adobe Commerce PaaS and Adobe Commerce as a Cloud Service when configuring a webhook that activates an App Builder runtime action?
```

### Copilota

1. Riavviare Visual Studio Code per caricare i nuovi strumenti e la nuova configurazione MCP.

1. Verificare l&#39;installazione confermando che il file `copilot-instructions.md` esiste nella cartella `.github`.

1. Attiva il server MCP:

   * Apri il pannello Estensioni facendo clic sull&#39;icona **Estensioni** nella barra attività a sinistra oppure utilizzando **Cmd+Maiusc+X** (macOs) o **Ctrl+Maiusc+X** (Windows e Linux).
   * Fare clic su **SERVER MCP - INSTALLATI**.
   * Fare clic sull&#39;icona a forma di ingranaggio accanto a **Commerce-extensibility MCP Server** e selezionare **Avvia server**, se il server è arrestato.
   * Fare di nuovo clic sull&#39;icona a forma di ingranaggio e selezionare **Mostra output**.

1. Verificare lo stato del server. L&#39;output `MCP:commerce-extensibility` deve corrispondere al seguente:

   ```terminal
   2025-11-13 12:58:50.652 [info] Starting server commerce-extensibility
   2025-11-13 12:58:50.652 [info] Connection state: Starting
   2025-11-13 12:58:50.652 [info] Starting server from LocalProcess extension host
   2025-11-13 12:58:50.657 [info] Connection state: Starting
   2025-11-13 12:58:50.657 [info] Connection state: Running
   
   (...)
   
   2025-11-13 12:58:50.753 [info] Discovered 10 tools
   ```

1. Utilizza il seguente prompt per verificare se l’agente utilizza il server MCP. In caso contrario, chiedi esplicitamente all’agente di utilizzare gli strumenti MCP disponibili.

   ```terminal
   What are the differences between Adobe Commerce PaaS and SaaS when configuring a webhook that activates an App Builder runtime action?
   ```

## Richiesta di esempio

Il seguente prompt di esempio crea un’estensione per inviare notifiche quando viene effettuato un ordine.

```terminal
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## Comandi Prompt

Oltre a richiedere conferma, è possibile utilizzare il comando `/search-commerce-docs` per eseguire ricerche nella documentazione nelle conversazioni con l&#39;agente. Ad esempio:

```text
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Best practice

Adobe consiglia di seguire le seguenti best practice durante l’utilizzo degli strumenti di codifica IA:

### Elenco di controllo

Prima di iniziare una sessione di sviluppo:

* Controlla `REQUIREMENTS.md`
* Verificare che gli strumenti MCP funzionino
* Rivedi la fase corrente e gli obiettivi
* Inizia con codice di esempio o progetti su scaffolding

Durante lo sviluppo:

* Considera attendibile il [protocollo](#protocol) in quattro fasi
* Richiedi piani di implementazione per lo sviluppo complesso
* Utilizzare gli strumenti MCP quando disponibili
* Test di ogni funzione dopo l’implementazione
* Esegui prima il test in locale, quindi distribuiscilo e ripetilo
* Utilizzo degli strumenti di codifica per testare il supporto
* Mettere in dubbio la complessità inutile
* Implementazione incrementale per uno sviluppo più rapido

All&#39;avvio di una nuova chat:

* Fornire un handoff di sessione corretto
* Fai riferimento ai file chiave con `@`
* Imposta obiettivi chiari per la sessione
* Usa limiti basati su fasi

### Flusso di lavoro

Durante lo sviluppo con gli strumenti di codifica AI, inizia con un codice di esempio o progetti su scaffolding. Questo approccio ti assicura di basarti su basi solide anziché partire dal nulla, ottimizzando al contempo il flusso di lavoro di sviluppo dell’intelligenza artificiale.

Questo consente anche di sfruttare i modelli di Adobe e di basarsi su modelli e architetture collaudate, mantenendo al contempo strutture e convenzioni di directory consolidate.

Consulta le seguenti risorse per iniziare:

* [Kit di avvio dell&#39;integrazione](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [Modelli di kit di avvio Adobe Commerce](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Modelli di avvio Adobe I/O Events](https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [Applicazioni di esempio App Builder](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### Perché utilizzare queste risorse

* **Modelli comprovati**: i kit di avvio incorporano le best practice e le decisioni di architettura di Adobe
* **Sviluppo più rapido**: riduce il tempo impiegato per il boilerplate e la configurazione
* **Coerenza**: assicura che l&#39;estensione segua le convenzioni stabilite
* **Manutenzione**: più semplice da mantenere e aggiornare con i seguenti modelli standard
* **Documentazione**: gli starter kit includono esempi e documentazione
* **Supporto community**: è più semplice ottenere assistenza quando si utilizzano approcci standard
* **Efficienza del contesto AI**: utilizza modelli e strutture familiari con cui lavorare, riducendo la necessità di spiegazioni approfondite e migliorando la precisione della generazione del codice
* **Utilizzo token ridotto**: fai riferimento a modelli esistenti invece di generare tutto da zero, per conversazioni più efficienti e meno riepiloghi di contesto

### Protocollo

Il seguente protocollo in quattro fasi viene applicato automaticamente dal sistema di regole. Gli strumenti devono seguire automaticamente questo protocollo durante lo sviluppo di estensioni:

* Fase 1: analisi dei requisiti e chiarimento
   * Quando ti vengono poste domande chiarificatrici, fornisci risposte complete.
* Fase 2: pianificazione architetturale e approvazione degli utenti
   * Quando viene presentato un piano, rivederlo attentamente prima di approvarlo.
* Fase 3: Generazione e implementazione del codice
* Fase 4: Documentazione e convalida

### Richiedi piani di implementazione per lo sviluppo complesso

Per uno sviluppo complesso che coinvolge più azioni di runtime, punti di contatto o integrazioni, richiedi esplicitamente che gli strumenti di intelligenza artificiale creino un piano di implementazione dettagliato. Quando in [Fase 2](#protocol) viene visualizzato un piano di alto livello che coinvolge più componenti, richiedere un piano di implementazione dettagliato per suddividerlo in attività gestibili:

```terminal
Create a detailed implementation plan for this complex development.
```

Le estensioni Adobe Commerce complesse spesso richiedono:

* Più azioni di runtime
* Configurazione dell’evento in più punti di contatto
* Integrazione con sistemi esterni
* Requisiti di gestione dello stato
* Test su più componenti

### Utilizzare gli strumenti MCP

>[!NOTE]
>
>Prima di utilizzare gli strumenti MCP, assicurati di aver [effettuato l&#39;accesso a Adobe I/O CLI](#log-in-to-the-adobe-io-cli).

Per impostazione predefinita, gli strumenti sono strumenti MCP, ma in determinate circostanze possono essere utilizzati i comandi CLI. Se desideri garantire l’utilizzo dello strumento MCP, richiedilo esplicitamente nel prompt.

Se sono presenti comandi CLI in uso e si desidera utilizzare gli strumenti MCP, utilizzare il seguente prompt:

```terminal
Use only MCP tools and not CLI commands
```

* Strumenti MCP: aio-app-deploy, aio-app-dev, aio-dev-invoke
* Comandi CLI: distribuzione app aio, sviluppo app aio

I comandi CLI possono essere utilizzati per i seguenti scenari:

* Scenari di distribuzione complessi
* Problemi specifici di debug
* Quando gli strumenti MCP hanno limitazioni
* Operazioni una tantum che non beneficiano dell&#39;integrazione MCP

### Sviluppo

È importante mettere in discussione la complessità non necessaria creata dagli strumenti di intelligenza artificiale.

Quando si aggiungono file non necessari (`validator.js`, `transformer.js`, `sender.js`) per endpoint di sola lettura semplici, utilizzare i prompt seguenti:

```terminal
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### Test

Utilizza le seguenti best practice durante il test:

#### Test di ogni funzione dopo l’implementazione

Dopo aver completato lo sviluppo di una funzione nel piano di implementazione, testala immediatamente. I test preliminari evitano i problemi composti e semplificano il debug.

* Non attendere il completamento di tutte le funzionalità
* Esegui il test in modo incrementale per rilevare i problemi in anticipo
* Convalida la funzionalità prima di passare alla funzionalità successiva

#### Esegui prima il test locale

Eseguire sempre il test prima localmente utilizzando lo strumento `aio-app-dev`. Questo offre un feedback immediato e consente cicli di iterazione più rapidi, debug più semplice e nessun sovraccarico di distribuzione.

1. Avvia server di sviluppo locale:

   ```bash
   aio-app-dev
   ```

1. Test delle azioni in locale:

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### Distribuisci e verifica di nuovo

Una volta che il test locale ha avuto esito positivo, distribuisci e verifica nell’ambiente di runtime. Gli ambienti di runtime possono avere un comportamento diverso rispetto allo sviluppo locale.

1. Distribuisci in fase di esecuzione:

   ```bash
   aio-app-deploy
   ```

1. Test delle azioni distribuite

1. Utilizzare il browser web o le richieste HTTP dirette

1. Controlla i registri di attivazione per il debug

#### Utilizzo degli strumenti di codifica per testare il supporto

Chiedi assistenza per i test. Gli strumenti possono essere utili per il debug, l’analisi dei registri e la creazione di dati di test appropriati per azioni di runtime specifiche.

**Azioni runtime di test**:

```terminal
Help me test the customer-created runtime action running locally
```

**Errori di debug**:

```terminal
Why did the subscription-updated runtime action activation fail?
```

**Registri di controllo**:

```terminal
Help me check the logs for the last stock-monitoring runtime action invocation
```

**Crea payload di test**:

```terminal
Generate test data for this Commerce event
```

```terminal
Create a test payload for the customer_save_after event
```

**Trova endpoint di runtime**:

```terminal
What's the URL for this deployed action?
```

**Gestisci autenticazione**:

```terminal
How do I authenticate with this external API?
```

**Risoluzione dei problemi**:

```terminal
Help me debug why this action is returning 500 errors
```

### Debug

Fermatevi e valutate quando le cose vanno male. In caso di problemi:

* Interrompi e valuta - Non continuare in uno stato interrotto
* Registri di controllo: utilizza i registri di attivazione per identificare i problemi
* Semplificare: rimuovere la complessità per isolare i problemi
* Test incrementale: correggi un problema alla volta
* Convalida: verifica di ogni correzione prima di procedere

### Distribuzione

Utilizza le seguenti best practice durante la distribuzione:

#### Implementare in modo incrementale

Distribuisci solo le azioni modificate per accelerare lo sviluppo. Questo ridurrà il rischio di interrompere le funzionalità esistenti e fornirà un feedback più rapido sulle modifiche. Riduce inoltre il rischio di interrompere le funzionalità esistenti.

* Utilizzare gli strumenti MCP per distribuire azioni specifiche

  ```bash
  aio-app-deploy --actions action-name
  ```

* Distribuire singole azioni dopo il test locale
* Distribuzione incrementale ed evitare l&#39;installazione completa delle applicazioni durante lo sviluppo

#### Pulizia runtime

Dopo modifiche importanti, utilizza gli strumenti per pulire le azioni orfane. Lasciare che gli strumenti di intelligenza artificiale gestiscano il processo di pulizia in modo sistematico, può identificare in modo efficiente le azioni orfane, verificarne lo stato e rimuoverle in modo sicuro senza intervento manuale.

```terminal
Help me identify and clean up orphaned runtime actions
```

Richiedi agli strumenti di intelligenza artificiale di elencare le azioni distribuite e identificare quelle non utilizzate

```terminal
List all deployed actions and identify which ones are no longer needed
```

Richiedere agli strumenti di intelligenza artificiale di rimuovere le azioni orfane utilizzando i comandi appropriati

```terminal
Remove the orphaned actions that are no longer part of the current implementation
```

### Monitorare

Utilizza le seguenti best practice per monitorare l’applicazione:

#### Controlla gli indicatori di qualità del contesto

* **Buon contesto**: IA ricorda le decisioni recenti e fa riferimento a file corretti
* **Contesto non valido**: l&#39;IA richiede le informazioni fornite in precedenza e ripete i problemi risolti

#### Tracciare la velocità di sviluppo

* **Alta velocità**: chiaro progresso, è necessaria una chiarificazione minima
* **Bassa velocità**: spiegazioni ripetute, confusione IA, avanzamento lento

#### Monitorare l&#39;efficienza dei costi

Tracciare i pattern di utilizzo dei token:

* **Efficiente**: utilizzo dei token ridotto, pochi riepiloghi di contesto
* **Inefficiente**: utilizzo token elevato, più riepiloghi, lavoro ripetuto

## Cosa evitare

Quando utilizzi gli strumenti di codifica AI, evita i seguenti pattern di protezione:

* **Non saltare la fase di chiarificazione**. Assicurarsi sempre che la fase 1 sia completata prima dell&#39;implementazione.
* **Non saltare i test dopo ogni funzionalità**. Esegui il test in modo incrementale, non attendere il completamento di tutto.
* **Non aggiungere complessità senza l&#39;analisi della causa principale**. Contattare i file aggiunti non necessari e richiedere indagini appropriate.
* **Non dichiarare l&#39;esito positivo senza test dei dati reali** - Verifica sempre con i dati effettivi, non solo con i casi limite.
* **Non dimenticare la pulizia in fase di esecuzione**. Eliminare sempre le azioni orfane dopo modifiche importanti.
