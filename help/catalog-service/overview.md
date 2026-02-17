---
title: '[!DNL Catalog Service]'
description: 'Accelera la tua vetrina Adobe Commerce con [!DNL Catalog Service] : un''API GraphQL ad alte prestazioni che riduce i tempi di caricamento delle pagine per pagine di prodotti, pagine di categorie e risultati di ricerca.'
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: 4f3f8accd653dbee6fec45c065f55ff04b17bd2d
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 0%

---

# [!DNL Catalog Service] per Adobe Commerce

[!DNL Catalog Service] per l&#39;estensione Adobe Commerce migliora i tempi di caricamento della vetrina fornendo dati di catalogo ottimizzati e di sola lettura tramite un&#39;API GraphQL dedicata. Questo servizio è progettato specificamente per migliorare le esperienze di pagina relative al prodotto, velocizzando il caricamento delle pagine e migliorando i tassi di conversione.

I dati rich view-model forniti da [!DNL Catalog Service] includono dettagli di prodotto, attributi, inventario e prezzi, consentendo il rendering rapido delle esperienze di vetrina relative al prodotto, ad esempio:

- Pagine dettagli prodotto
- Pagine di elenco prodotti e categorie
- Pagine dei risultati di ricerca
- Caroselli di prodotti
- Pagine di confronto dei prodotti
- Qualsiasi altra pagina che riproduce i dati di prodotto, come le pagine del carrello, dell’ordine e dell’elenco dei desideri


## Vantaggi e caratteristiche principali

- **Caricamenti di pagina più veloci**: query ottimizzate per un recupero dei dati del catalogo fino a 10 volte più veloce rispetto al sistema GraphQL di base
- **Tassi di conversione migliorati**: i tempi di caricamento più rapidi consentono una migliore esperienza utente
- **Tipi di prodotto semplificati**: lo schema unificato basato su tipi di prodotto semplici e complessi riduce la complessità per gli sviluppatori
- **Migliore precisione del prezzo**: supporto per valori a 16 cifre con 4 cifre decimali
- **Architettura separata**: un sistema GraphQL separato per i dati del catalogo garantisce prestazioni elevate senza influire sulle operazioni principali di Commerce
- **Sincronizzazione dei dati in tempo reale**: Catalog Service viene mantenuto sincronizzato con l&#39;applicazione Adobe Commerce tramite l&#39;estensione SaaS Data Export, garantendo che le query restituiscano i dati del catalogo più aggiornati
- **Dashboard di gestione dati**: monitora e gestisci le operazioni di sincronizzazione dei dati dall&#39;interfaccia di amministrazione di Adobe Commerce
- **Integrazione Mesh API**: è possibile eseguire l&#39;integrazione con [Mesh API per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) per combinare i sistemi Adobe Commerce GraphQL con altre API interne e di terze parti per estendere lo schema GraphQL di Catalog Service e aggiungere dati o funzionalità personalizzate


## Panoramica dell’architettura

>[!NOTE]
>
>Se implementi il catalogo utilizzando il catalogo componibile con Adobe Commerce Optimizer o Adobe Commerce Optimizer Connector, consulta la [Guida di Adobe Commerce Optimizer](../optimizer/overview.md#architecture) e Guida per gli sviluppatori di Merchandising Services.

[!DNL Catalog Service] utilizza [GraphQL](https://graphql.org/) per richiedere e ricevere i dati del catalogo, inclusi prodotti, attributi di prodotto, inventario e prezzi. GraphQL è un linguaggio di query che un client front-end utilizza per comunicare con l’API (Application Programming Interface) definita su un back-end come Adobe Commerce. GraphQL è un metodo di comunicazione diffuso perché è leggero e consente a un integratore di sistemi di specificare il contenuto e l’ordine di ciascuna risposta.

Adobe Commerce fornisce due sistemi GraphQL con scopi diversi:

### Sistema core GraphQL

- **Scopo**: API completa per tutte le operazioni di Commerce
- **Funzionalità**: query (lettura) e mutazioni (scrittura) per prodotti, clienti, carrello, pagamento e altro ancora
- **Limitazione**: le query di prodotto non sono ottimizzate per la velocità
- **Caso d&#39;uso**: operazioni generali di Commerce e operazioni di scrittura

### Sistema GraphQL di Catalog Service

- **Scopo**: solo query del catalogo prodotti ad alte prestazioni
- **Funzionalità**: query di sola lettura per prodotti, attributi, inventario e prezzi
- **Vantaggio**: notevolmente più veloce del sistema di base per i dati di prodotto
- **Caso d&#39;uso**: esperienze di prodotto in vetrina in cui la velocità è un fattore critico

I dati disponibili per Catalog Service vengono forniti dall’estensione SaaS Data Export. Questa estensione sincronizza i dati tra l’applicazione Commerce e i servizi Commerce connessi per garantire che le query sugli endpoint API di GraphQL Services restituiscano i dati del catalogo più recenti. Per informazioni sulla gestione e la risoluzione dei problemi relativi alle operazioni di esportazione dei dati SaaS, vedere la [Guida all&#39;esportazione dei dati SaaS](../data-export/overview.md).

I clienti [!DNL Catalog Service] possono utilizzare l&#39;[Indicizzatore prezzi SaaS](../price-index/price-indexing.md), che fornisce aggiornamenti dei prezzi e tempi di sincronizzazione più rapidi.

## Dettagli dell’architettura

Il diagramma seguente illustra le differenze a livello di architettura tra il sistema GraphQL di base e il sistema GraphQL di Catalog Service, illustrando come questi sistemi collaborino per ottimizzare le prestazioni della vetrina:

![Diagramma dell&#39;architettura del catalogo](assets/catalog-service-architecture.png)

### Funzionamento dei sistemi

**Sistema GraphQL di base (approccio tradizionale):**
L’app web progressiva (PWA) invia le richieste direttamente all’applicazione Commerce, che elabora ogni richiesta tramite più sottosistemi prima di restituire una risposta. Questo percorso di andata e ritorno in più passaggi può causare tempi di caricamento delle pagine lenti, che potrebbero comportare tassi di conversione più bassi.

**Servizio catalogo (approccio ottimizzato):**
Catalog Service funge da gateway dei servizi di Storefront che accede a un database dedicato e ottimizzato contenente dettagli dei prodotti, attributi, varianti, prezzi e categorie. Il servizio mantiene la sincronizzazione con Adobe Commerce tramite l’indicizzazione automatizzata, aggirando il tradizionale ciclo di richiesta-risposta per ridurre notevolmente la latenza.

I sistemi GraphQL di base e di servizio non comunicano direttamente tra loro. Puoi accedere a ogni sistema da un URL diverso e le chiamate richiedono informazioni di intestazione diverse. I due sistemi GraphQL sono progettati per essere utilizzati insieme. Il sistema GraphQL [!DNL Catalog Service] potenzia il sistema di base per rendere più veloci le esperienze di presentazione dei prodotti.

Facoltativamente, puoi implementare [Mesh API per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) per integrare i due sistemi Adobe Commerce GraphQL con API private e di terze parti e altre interfacce software tramite Adobe Developer. La mesh può essere configurata in modo da garantire che le chiamate instradate a ciascun endpoint contengano le informazioni di autorizzazione corrette nelle intestazioni.

## Dettagli architetturali

Le sezioni seguenti descrivono alcune delle differenze tra i due sistemi GraphQL.

### Gestione schema

Poiché Catalog Service funziona come un servizio, gli integratori non devono preoccuparsi della versione sottostante di Commerce. La sintassi delle query è la stessa per tutte le versioni. Inoltre, lo schema è coerente per tutti i commercianti. Questa coerenza semplifica la definizione delle best practice e aumenta in modo significativo il riutilizzo dei widget della vetrina.

### Semplificazione dei tipi di prodotto

Lo schema riduce la diversità dei tipi di prodotto a due casi d’uso:

- **Prodotti semplici**: Catalog Service mappa i tipi di prodotti Adobe Commerce semplici, virtuali, scaricabili e gift card su `simpleProductViews`. Questo tipo dispone di:
   - Un unico prezzo fisso e quantità
   - Un prezzo regolare (prima degli sconti) e il prezzo finale (dopo gli sconti)
   - Supporto per attributi di prodotto come colore, dimensione e altre caratteristiche

- **Prodotti complessi**: Catalog Service mappa i tipi di prodotto configurabili, raggruppati e raggruppati di Adobe Commerce su `complexProductViews`. I prodotti complessi sono raccolte di più prodotti semplici che possono essere configurati o raggruppati insieme.
   - Ogni componente prodotto semplice può avere il proprio prezzo.
   - Gli acquirenti possono specificare le quantità dei singoli componenti.
   - Le opzioni di prodotto (come dimensioni, colore, materiale) sono unificate e funzionano allo stesso modo indipendentemente dal tipo di prodotto. Ogni selezione di opzioni punta a un prodotto semplice specifico con i propri attributi e prezzo. Il prodotto finale rimane indefinito fino a quando l&#39;acquirente non seleziona tutte le opzioni richieste.

#### Attributi di visualizzazione del prodotto

Sia i prodotti semplici che quelli complessi dispongono di attributi definiti dal cliente che possono essere visualizzati nella vetrina. Questi attributi vengono restituiti come [ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type). In Adobe Commerce, gli attributi disponibili vengono definiti al momento della creazione del prodotto. Puoi aggiungere attributi aggiuntivi dal backend di Adobe Commerce o a livello di programmazione. Vedi [Estendere e personalizzare i dati del feed di esportazione dei dati SaaS](../data-export/extensibility-and-customizations.md).

>[!TIP]
>
>Anziché aggiungere tipi di dati al backend di Commerce, è possibile utilizzare [Mesh API con Catalog Service](mesh.md) per estendere lo schema GraphQL di Catalog Service per aggiungere dati o configurare dati di catalogo esistenti per abilitare nuove funzionalità.

### Prezzi

I prodotti semplici rappresentano l&#39;unità di vendita di base che ha un prezzo. [!DNL Catalog Service] calcola il prezzo regolare prima degli sconti e il prezzo finale dopo gli sconti. I calcoli dei prezzi possono includere imposte sui prodotti fisse. Escludono le promozioni personalizzate.

Un prodotto complesso non ha un prezzo stabilito. Catalog Service restituisce invece i prezzi dei semplici collegati. Ad esempio, un esercente può inizialmente assegnare gli stessi prezzi a tutte le varianti di un prodotto configurabile. Se determinate dimensioni o colori sono impopolari, il commerciante può ridurre i prezzi di tali varianti. Pertanto, il prezzo del prodotto complesso (configurabile) presenta inizialmente una fascia di prezzo, che riflette il prezzo sia delle varianti standard che di quelle impopolari. Dopo che l&#39;acquirente ha selezionato un valore per tutte le opzioni disponibili, la vetrina visualizza un solo prezzo.

Catalog Service assicura aggiornamenti e calcoli accurati dei prezzi grazie al supporto di prezzi con valori elevati (fino a 16 cifre) e alta precisione decimale (fino a 4 cifre decimali).

>[!NOTE]
>
> I clienti Commerce con [!DNL Catalog Service] possono sfruttare gli aggiornamenti più rapidi delle modifiche dei prezzi e i tempi di sincronizzazione sui loro siti Web con l&#39;[indicizzatore dei prezzi SaaS](../price-index/price-indexing.md).

## Implementazione

Il processo di attuazione prevede:

1. [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."} **[Installa e configura Catalog Service](installation.md)**. Installa e configura l&#39;estensione Catalog Service e configura la connessione SaaS utilizzando [!DNL Commerce Services Connector].
2. **Aggiorna codice vetrina**: integra le query GraphQL di Catalog Service nel tuo front-end.
3. **Instrada query**: tutte le query di Catalog Service passano attraverso il gateway GraphQL (URL fornito durante l&#39;onboarding)
4. **Monitoraggio e risoluzione dei problemi relativi alla sincronizzazione dei dati**: verificare prestazioni migliorate e monitorare i risultati


