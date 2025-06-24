---
title: Configurare la vetrina
description: Scopri come eseguire lo strumento di scaffolding per configurare la vetrina  [!DNL Adobe Commerce as a Cloud Service] .
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: c608d9e82a892e40d362065c229b8d451ed3dbfb
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Configurare la vetrina

Nei passaggi seguenti viene illustrato come configurare rapidamente la vetrina Adobe Commerce con tecnologia Edge Delivery utilizzando il comando `aio commerce init`. Questo processo imposta quanto segue:

* [Commerce Storefront con tecnologia Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=it): una vetrina performante, scalabile e sicura basata su Edge Delivery Services di Adobe.
* [Mesh API per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/mesh/): piattaforma API che consente agli sviluppatori di combinare più origini dati in un unico endpoint GraphQL. API Mesh orchestra API di terze parti con API Adobe tramite un singolo gateway. Una query al singolo endpoint GraphQL può restituire risultati da più origini.
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) - Raccolta di strumenti per sviluppatori con accesso a API, eventi, funzioni di runtime e plug-in, che è possibile utilizzare per creare progetti per le applicazioni Adobe.
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) - Un motore senza server per la distribuzione di codice personalizzato che risponde agli eventi ed esegue funzioni nel cloud.

## Prerequisiti

Prima di eseguire il comando `aio commerce init`, è necessario completare i seguenti prerequisiti:

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

1. Installare [Adobe I/O Runtime CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Installa il plug-in Mesh API di Adobe I/O.

   ```bash
   aio plugins:install @adobe/aio-cli-plugin-api-mesh
   ```

1. Installa il plug-in Commerce di Adobe I/O.

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. Aggiorna eventuali plug-in esistenti.

   ```bash
   aio plugins:update
   ```

1. Accedi al tuo account Adobe Experience Cloud.

   ```bash
   aio login
   ```

   Se il comando `aio login` non avvia una finestra del browser, consultare la sezione [Risoluzione dei problemi](#troubleshooting).

1. Seleziona l’organizzazione IMS, il progetto e l’area di lavoro. Utilizza i tasti freccia e premi **Invio** per effettuare la selezione. Per ulteriori informazioni sui comandi `aio`, consulta la [documentazione CLI di Adobe I/O](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands).

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

1. Se non lo hai già fatto, accetta le Condizioni d&#39;uso per sviluppatori nella console Adobe Developer accedendo a https://developer.adobe.com/console/home e facendo clic su **Accetta e continua**.

## Esegui il comando `aio commerce init`

L’esecuzione del comando seguente creerà uno scaffolding per la vetrina Commerce. Questo scaffolding offre un ottimo punto di partenza per la creazione e la comprensione della vetrina. Per ulteriori informazioni sull&#39;utilizzo della vetrina, consulta la [documentazione di Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=it).


1. Esegui il comando `init`:

   ```bash
   aio commerce init
   ```

1. Se hai già effettuato l&#39;accesso a GitHub, immetti `Y` per creare l&#39;archivio con il tuo nome utente.

1. Immettere il nome dell&#39;archivio che si desidera creare.

1. Selezionare una delle opzioni seguenti:

   * **Utilizza il tenant demo di Adobe Commerce**. Utilizza un tenant demo.
      * Se selezioni questa opzione, ti viene richiesto di installare il bot AEM Code Sync in una finestra del browser. È necessario specificare l’archivio creato e autorizzare il bot. Tornare a CLI e immettere `y` per confermare l&#39;installazione bot di AEM Code Sync.
   * **Scegli un tenant Adobe Commerce disponibile**. Seleziona un tenant Commerce esistente nell&#39;organizzazione selezionata.
      * Se selezionate questa opzione, dovete selezionare il progetto e l&#39;area di lavoro in cui creare una mesh.
   * **Fornisci il tuo URL API tenant Adobe Commerce**. Seleziona questa opzione se sei un partecipante al programma di accesso anticipato. Immetti l’URL API fornito nell’e-mail di onboarding di Adobe.

   >[!NOTE]
   >
   >Se si seleziona l&#39;opzione `Pick an available API (Mesh -> SaaS)`, è necessario disporre di un progetto e di un Workspace esistenti in Adobe Developer Console. [Se si crea un progetto basato su modelli](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/) e si seleziona App Builder, verranno create automaticamente le aree di lavoro necessarie.

1. Al termine del processo, puoi personalizzare la vetrina utilizzando i seguenti metodi:

   * Personalizzare il codice: `https://github.com/<username or org>/<repo name>`
   * Modifica il contenuto: `https://da.live/#/<username or org>/<repo name>`
   * Gestisci configurazione: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * Anteprima vetrina: `https://main--<repo name>--<username or org>.aem.page/`
   * Esecuzione locale: `aio commerce:dev`

Per personalizzare la vetrina, consulta la [documentazione di Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=it).

## Risoluzione dei problemi

In caso di problemi con il comando `aio login`, Adobe consiglia di disconnettersi completamente da CLI e dal browser e quindi di effettuare di nuovo l&#39;accesso.

1. Per disconnettersi da CLI, eseguire:

   ```bash
   aio logout
   ```

1. Nel browser, passa a [Adobe Developer Console](https://developer.adobe.com/console), fai clic sull&#39;icona del tuo profilo in alto a destra e seleziona **Esci**.

1. Tornare a CLI ed eseguire di nuovo il comando `aio login`, che dovrebbe avviare una finestra del browser per l&#39;accesso. Puoi quindi procedere con la selezione dell’organizzazione, del progetto e dell’area di lavoro.

   ```bash
   aio console org select
   ```

   ```bash
   aio console workspace select
   ```

   ```bash
   aio console project select
   ```
