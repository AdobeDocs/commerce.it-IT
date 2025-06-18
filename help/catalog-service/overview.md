---
title: '[!DNL Catalog Service]'
description: '[!DNL Catalog Service] per Adobe Commerce consente di recuperare i contenuti delle pagine di visualizzazione dei prodotti e delle pagine dell''elenco dei prodotti in modo molto più rapido rispetto alle query native di Adobe Commerce GraphQL.'
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 0%

---

# [!DNL Catalog Service] per Adobe Commerce

L&#39;estensione [!DNL Catalog Service] per Adobe Commerce fornisce dati di catalogo avanzati per modelli di visualizzazione (sola lettura) per riprodurre in modo rapido e completo le esperienze della vetrina relative ai prodotti, tra cui:

* Pagine dettagli prodotto
* Pagine di elenco prodotti e categorie
* Pagine dei risultati di ricerca
* Caroselli di prodotti
* Pagine di confronto dei prodotti
* Qualsiasi altra pagina che riproduce i dati di prodotto, come le pagine del carrello, dell’ordine e dell’elenco dei desideri

[!DNL Catalog Service] utilizza [GraphQL](https://graphql.org/) per richiedere e ricevere i dati del catalogo, inclusi prodotti, attributi di prodotto, inventario e prezzi. GraphQL è un linguaggio di query che un client front-end utilizza per comunicare con l’API (Application Programming Interface) definita su un back-end come Adobe Commerce. GraphQL è un metodo di comunicazione diffuso perché è leggero e consente a un integratore di sistemi di specificare il contenuto e l’ordine di ciascuna risposta.

Adobe Commerce dispone di due sistemi GraphQL. Il sistema GraphQL di base fornisce un’ampia gamma di query (operazioni di lettura) e mutazioni (operazioni di scrittura) che consentono a un acquirente di interagire con molti tipi di pagine, tra cui prodotto, account cliente, carrello, pagamento e altro ancora. Tuttavia, le query che restituiscono le informazioni sul prodotto non sono ottimizzate per la velocità. Il sistema GraphQL dei servizi può eseguire query solo sui prodotti e sulle informazioni correlate. Queste query sono più performanti di query di base simili.

I dati disponibili per Catalog Service vengono forniti dall’estensione SaaS Data Export. Questa estensione sincronizza i dati tra l’applicazione Commerce e i servizi Commerce connessi per garantire che le query sugli endpoint API di GraphQL Services restituiscano i dati del catalogo più recenti. Per informazioni sulla gestione e la risoluzione dei problemi relativi alle operazioni di esportazione dei dati SaaS, vedere la [Guida all&#39;esportazione dei dati SaaS](../data-export/overview.md).

I clienti [!DNL Catalog Service] possono utilizzare l&#39;[Indicizzatore prezzi SaaS](../price-index/price-indexing.md), che fornisce aggiornamenti dei prezzi e tempi di sincronizzazione più rapidi.

## Architettura

Il diagramma seguente mostra i due sistemi GraphQL:

![Diagramma dell&#39;architettura del catalogo](assets/catalog-service-architecture.png)

Nel sistema GraphQL di base, PWA invia una richiesta all’applicazione Commerce, che riceve ogni richiesta, la elabora, eventualmente inviando una richiesta tramite più sottosistemi, quindi restituisce una risposta alla vetrina. Questo round trip può causare rallentamenti nei tempi di caricamento delle pagine, con possibili tassi di conversione più bassi.

[!DNL Catalog Service] è un gateway di servizi Storefront. Il servizio accede a un database separato contenente i dettagli del prodotto e le informazioni correlate, ad esempio attributi del prodotto, varianti, prezzi e categorie. Il servizio mantiene il database sincronizzato con Adobe Commerce tramite l’indicizzazione.
Poiché il servizio ignora la comunicazione diretta con l’applicazione, è in grado di ridurre la latenza del ciclo di richiesta e risposta.

I sistemi GraphQL di base e di servizio non comunicano direttamente tra loro. Puoi accedere a ogni sistema da un URL diverso e le chiamate richiedono informazioni di intestazione diverse. I due sistemi GraphQL sono progettati per essere utilizzati insieme. Il sistema GraphQL [!DNL Catalog Service] potenzia il sistema di base per rendere più veloci le esperienze di presentazione dei prodotti.

Facoltativamente, puoi implementare [Mesh API per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) per integrare i due sistemi Adobe Commerce GraphQL con API private e di terze parti e altre interfacce software tramite Adobe Developer. La mesh può essere configurata in modo da garantire che le chiamate instradate a ciascun endpoint contengano le informazioni di autorizzazione corrette nelle intestazioni.

## Dettagli architetturali

Le sezioni seguenti descrivono alcune delle differenze tra i due sistemi GraphQL.

### Gestione schema

Poiché Catalog Service funziona come un servizio, gli integratori non devono preoccuparsi della versione sottostante di Commerce. La sintassi delle query è la stessa per tutte le versioni. Inoltre, lo schema è coerente per tutti i commercianti. Questa coerenza semplifica la definizione delle best practice e aumenta in modo significativo il riutilizzo dei widget della vetrina.

### Semplificazione dei tipi di prodotto

Lo schema riduce la diversità dei tipi di prodotto a due casi d’uso:

* I prodotti semplici sono prodotti definiti con un unico prezzo e quantità. Catalog Service esegue il mapping dei tipi di prodotto semplici, virtuali, scaricabili e gift card su `simpleProductViews`.

* I prodotti complessi sono costituiti da più prodotti semplici. Il componente prodotti semplici può avere prezzi diversi. Un prodotto complesso può anche essere definito in modo che l&#39;acquirente possa specificare la quantità di componenti semplici prodotti. Catalog Service mappa i tipi di prodotto configurabili, raggruppati e raggruppati su `complexProductViews`.

Le opzioni di prodotto complesse sono unificate e si distinguono per il loro comportamento, non per il tipo. Ogni valore di opzione rappresenta un prodotto semplice. Questo valore di opzione ha accesso agli attributi di prodotto semplici, incluso il prezzo. Quando l’acquirente seleziona tutte le opzioni per un prodotto complesso, la combinazione di opzioni selezionate punta a un prodotto semplice specifico. Il prodotto semplice rimane ambiguo finché l’acquirente non seleziona un valore per tutte le opzioni disponibili.

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

[!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."}

Il processo di installazione richiede la configurazione di [Commerce Services Connector](../landing/saas.md). Al termine, il passaggio successivo consiste nell&#39;aggiornamento del codice della vetrina da parte di un integratore di sistemi per incorporare le query [!DNL Catalog Service]. Tutte le query [!DNL Catalog Service] vengono instradate al gateway GraphQL. L’URL viene fornito durante il processo di onboarding.
