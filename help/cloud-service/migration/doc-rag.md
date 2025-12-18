---
title: Servizio RAG documentazione
description: Scopri come utilizzare il servizio di ricerca della documentazione basato sull’intelligenza artificiale per lo sviluppo di Adobe Commerce.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 28396828516645abec3b42a2c6874afe9134dfb8
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Servizio RAG documentazione (Beta)

>[!NOTE]
>
>Il servizio di documentazione RAG è attualmente disponibile in Beta e l’esperienza è soggetta a modifiche.

Il servizio di documentazione RAG (Retrieval-Augmented Generation) fornisce funzionalità di ricerca semantica basate sull’intelligenza artificiale nella documentazione pertinente di Adobe Commerce e App Builder.

Questo RAG fornisce un’interfaccia IDE per porre domande su Adobe Commerce e può consigliarti sulle best practice per lo sviluppo di applicazioni e altre attività di migrazione.

Il servizio RAG fa parte del server [Commerce extensibility tools](./coding-tools.md) MCP (Model Context Protocol), che si integra con Cursor e altri assistenti di IA compatibili con MCP.

## Documentazione disponibile

Nella tabella seguente viene descritta la documentazione attualmente indicizzata dal servizio RAG e le parole chiave che è possibile utilizzare per attivare la ricerca nell&#39;indice associato. La documentazione inclusa continuerà a crescere man mano che svilupperemo il servizio RAG.

| Categoria | Indice | Contenuto incluso | Parole chiave |
|-------|---------|---------|------------------------|
| [Vetrina](https://experienceleague.adobe.com/developer/commerce/storefront/) | commerce-storefront-docs | Edge Delivery Services, drop-in, componenti storefront | vetrina, consegna, EDS, elenco prodotti, pagamento |
| [Estensibilità](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhook, eventi, estensioni, integrazioni | webhook, evento, estensione, mesh API, GraphQL |
| [Commerce](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview) | commerce-core-docs | Commerce core (catalogo, clienti, ordini) | catalogo, prodotto, cliente, ordine, inventario |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder, azioni di runtime, estensioni dell’interfaccia utente | app builder, azione runtime, React Spectrum |

Per ulteriori informazioni sulla selezione dell&#39;indice, consultare [Selezione automatica dell&#39;indice](#automatic-index-selection-recommended) e [Selezione esplicita dell&#39;indice](#explicit-index-selection).

Per informazioni dettagliate sulla documentazione inclusa in ogni indice, consulta l&#39;[elenco di origini acquisite](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md).

## Sicurezza e privacy

* **Autenticazione IMS** - Tutte le chiamate API utilizzano token Adobe IMS OAuth2.
* **Archiviazione dati assente** - Il server MCP non memorizza credenziali o dati.
* **Esecuzione locale** - Tutti gli strumenti vengono eseguiti localmente nel computer.
* **Comunicazione sicura** - La ricerca nella documentazione utilizza HTTPS con convalida del token.

L&#39;endpoint di produzione è protetto da [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview), che include le seguenti protezioni:

* Firewall applicazione Web (WAF) con set di regole predefinito di Microsoft 2.1 e set di regole di gestione bot 1.0
* Blocco geografico per le regioni soggette a embargo da parte degli Stati Uniti (Cuba, Iran, Corea del Nord, Siria, Crimea, Luhansk, Donetsk)
* Protezione DDoS ai margini
* Il backend di gestione API è bloccato per accettare solo il traffico da Front Door

Per diversi requisiti di sicurezza, puoi utilizzare un endpoint personalizzato. Per ulteriori informazioni, vedere [Endpoint Front Door personalizzato](#custom-front-door-endpoint).

## Prerequisiti

Prima dell’installazione, assicurati di disporre di:

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+ (consigliato)
* [IDE cursore](https://cursor.com/download){target="_blank"} (consigliato) o un altro IDE compatibile con MCP

  >[!NOTE]
  >
  >Sono supportati altri IDE compatibili con MCP, tuttavia l’IDE consigliato è Cursor. Se utilizzi un altro IDE, dovrai modificare i prompt e gli altri passaggi della documentazione per utilizzare l’IDE selezionato.

## Installazione

1. Installa [Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) a livello globale:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Autenticazione con Adobe IMS:

   ```bash
   aio auth login
   ```

1. Clonare il repository degli strumenti di estensibilità di Commerce e passare alla directory:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. Installare le dipendenze:

   ```bash
   npm install
   ```

1. Crea o aggiorna `.cursor/mcp.json` nella directory del progetto Commerce (non globalmente) per includere il server MCP `commerce-extensibility-tools`:

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   Assicurarsi di sostituire `<your-project-directory>` con il percorso effettivo in cui è stato clonato l&#39;archivio.

   >[!NOTE]
   >
   >In Windows, in caso di problemi con la fornitura del percorso alla directory del progetto, consulta [Risoluzione dei problemi del percorso](#path-issues-windows).

1. Riavvia IDE cursore per caricare il server MCP.

1. Verifica l’installazione chiedendo all’assistente AI:

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## Utilizzo

Una volta installato, è possibile chiamare gli indici [automaticamente](#automatic-index-selection-recommended) o [in modo esplicito](#explicit-index-selection). È inoltre possibile utilizzare il comando [`/search-commerce-docs`](#command-based-search).

>[!NOTE]
>
>Il servizio RAG restituisce i primi 5 risultati più rilevanti.

### Selezione automatica indice (scelta consigliata)

Facendo domande in linguaggio naturale sul progetto Commerce, lo strumento cercherà automaticamente l’indice della documentazione appropriato e fornirà informazioni pertinenti:

>[!BEGINSHADEBOX]

Il seguente prompt seleziona automaticamente l&#39;indice `commerce-storefront-docs`:

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

Il seguente prompt seleziona automaticamente l&#39;indice `commerce-extensibility-docs`:

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

Il seguente prompt seleziona automaticamente l&#39;indice `commerce-core-docs`:

```shell-session
"How to configure product catalog settings?"
```

Il seguente prompt seleziona automaticamente l&#39;indice `app-builder-docs`:

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### Selezione esplicita dell&#39;indice

In alternativa, è possibile specificare l&#39;indice da utilizzare nel prompt.

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### Ricerca basata su comandi

Se si desidera assicurarsi che venga utilizzato il servizio RAG, è possibile richiamare manualmente il comando Cursore `/search-commerce-docs` per eseguire ricerche nella documentazione al prompt:

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Endpoint personalizzato porta anteriore

Per impostazione predefinita, la ricerca nella documentazione utilizza l&#39;endpoint di produzione [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) con protezione WAF. A scopo di test o sviluppo, è possibile eseguire l&#39;override con la variabile di ambiente `FRONT_DOOR_URL`.

Per utilizzare un endpoint personalizzato, aggiungilo alla configurazione MCP cursore:

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>La maggior parte degli sviluppatori deve utilizzare l&#39;endpoint di produzione predefinito e non è necessario impostare la variabile `FRONT_DOOR_URL`.

## Risoluzione dei problemi

Nelle sezioni seguenti vengono forniti suggerimenti per la risoluzione dei problemi comuni che possono verificarsi quando si utilizza il servizio RAG della documentazione.

### Errori di autenticazione

Lo strumento di ricerca della documentazione richiede l’autenticazione Adobe IMS. Se riscontri errori di autenticazione, procedi come segue per risolvere il problema e risolverlo.

1. Verifica di aver effettuato l’accesso:

   ```bash
   aio where
   ```

1. Verifica di poter visualizzare il token IMS:

   ```bash
   aio auth login --bare
   ```

1. Se gli errori di autenticazione persistono, disconnettersi e accedere di nuovo:

   ```bash
   aio auth logout
   aio auth login
   ```

### Impossibile caricare il server MCP

Se il server MCP non si connette o l&#39;agente comunica che non è in grado di connettersi a RAG, attenersi alla procedura seguente per risolvere il problema.

1. Apri Impostazioni cursore tramite **Cmd ,** (macOS) o **Ctrl ,** (Windows e Linux).

1. Cercare &quot;MCP&quot; e verificare che `commerce-extensibility-tools` sia elencato e abilitato.

1. Verifica la presenza di messaggi di errore nel pannello delle impostazioni MCP.

1. Verificare che il file `mcp.json` esista nel progetto:

   ```bash
   cat .cursor/mcp.json
   ```

1. Verifica che il percorso sia corretto e assoluto:

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### Strumento non trovato

1. Chiudere Cursore e riaprirlo.

1. Controlla i registri del server MCP nella console per sviluppatori del cursore utilizzando **Cmd+Shift+P** (macOS) o **Ctrl+Shift+P** (Windows/Linux) e cercando &quot;Sviluppatore: Apri cartella dei registri&quot;.

1. Verificare l&#39;installazione:

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   Il server deve avviarsi senza errori.

### Problemi di percorso (Windows)

In Windows, utilizzare le barre `/` o le barre rovesciate con escape `\\`:

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## Risorse aggiuntive

* [Documentazione per gli sviluppatori di Adobe Commerce](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [Documentazione di App Builder](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [Protocollo contesto modello](https://modelcontextprotocol.io/){target="_blank"}
* [IDE cursore](https://cursor.sh/docs){target="_blank"}
