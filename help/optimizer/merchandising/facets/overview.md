---
title: Panoramica dei facet
description: Scopri i facet in [!DNL Adobe Commerce Optimizer] e come migliorano i risultati della ricerca.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: b786a8675625dc969b9542b4b4f716de5342c1af
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 0%

---

# Facet

Facet è un metodo di filtro ad alte prestazioni che utilizza più dimensioni di valori di attributo come criteri di ricerca.

![Risultati ricerca filtrati](../../assets/storefront-search-results-run.png)

All’interno di un facet, gli acquirenti possono selezionare più opzioni, ad esempio &quot;Basic&quot; e &quot;Snug&quot; in &quot;Style&quot; e i risultati della ricerca vengono aggiornati per visualizzare solo questi stili. Allo stesso modo, se un acquirente seleziona le opzioni tra i facet, come &quot;Basic&quot; in &quot;Style&quot; e &quot;Indoor&quot; in &quot;Climate&quot;, i risultati della ricerca vengono aggiornati per mostrare lo stile selezionato e il clima selezionato.

Qualsiasi facet definito può essere utilizzato come parametro URL e i risultati verranno filtrati in base ai valori del parametro: `http://yourstore.com?brand=acme&color=red`.

## Aggregazione facet

L&#39;aggregazione sfaccettatura viene eseguita come segue: se la vetrina ha tre sfaccettature (categorie, colore e prezzo) e i filtri acquirente su tutte e tre (colore = blu, prezzo = $ 10.00-50,00, categorie = `promotions`).

- Aggregazione `categories`: aggrega `categories`, quindi applica i filtri `color` e `price`, ma non il filtro `categories`.
- Aggregazione `color`: aggrega `color`, quindi applica i filtri `price` e `categories`, ma non il filtro `color`.
- Aggregazione `price`: aggrega `price`, quindi applica i filtri `color` e `categories`, ma non il filtro `price`.

## Valori attributi predefiniti

I seguenti attributi di prodotto sono utilizzati da [!DNL Adobe Commerce Optimizer] e abilitati per impostazione predefinita.

| Proprietà | Descrizione | Attributo |
|---|---|---|
| Ordinabile | Utilizzato per l’ordinamento nell’elenco prodotti | `price` |
| Ricercabile | Uso nella ricerca | `price` <br />`sku`<br />`name` |

Per ulteriori informazioni sugli attributi del prodotto e sulle relative proprietà, consulta l&#39;[API dei metadati per l&#39;acquisizione dei dati](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata).

## Ricerca su più livelli ed espansione dei tipi di ricerca

La ricerca a livelli, o ricerca all’interno di una ricerca, è un sistema di filtro basato su attributi che estende la funzionalità di ricerca tradizionale per includere parametri di ricerca aggiuntivi. Questi parametri di ricerca aggiuntivi consentono un rilevamento del prodotto più preciso e flessibile.

La ricerca su più livelli consente di:

- Consenti agli acquirenti di eseguire ricerche all&#39;interno dei risultati di ricerca.
- Utilizza l&#39;indicizzazione della ricerca `startsWith` e `contains` nel secondo livello della ricerca a livelli per perfezionare ulteriormente i risultati.

Le funzionalità di ricerca avanzata sono implementate tramite il parametro `filter` nella query [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) utilizzando operatori specifici:

- **Ricerca a livelli** - Ricerca in un altro contesto di ricerca - Con questa funzionalità è possibile eseguire fino a due livelli di ricerca per le query di ricerca. Ad esempio:

   - **Ricerca livello 1** - Ricerca &quot;motore&quot; in `product_attribute_1`.
   - **Ricerca livello 2** - Ricerca &quot;numero parte 123&quot; in `product_attribute_2`. In questo esempio viene cercata la voce &quot;part number 123&quot; all&#39;interno dei risultati per &quot;motor&quot;.

  La ricerca con livelli è disponibile sia per l&#39;indicizzazione di ricerca `startsWith` che per l&#39;indicizzazione di ricerca `contains` nel secondo livello della ricerca con livelli, come descritto di seguito:

- **startsWith indicizzazione ricerca** - Effettua la ricerca utilizzando l&#39;indicizzazione `startsWith`. Questa funzionalità consente di:

   - Ricerca di prodotti in cui il valore dell&#39;attributo inizia con una stringa specificata.
   - La configurazione di una ricerca &quot;termina con&quot; consente agli acquirenti di cercare prodotti in cui il valore dell’attributo termina con una stringa specifica.
      - Per abilitare una ricerca &quot;termina con&quot;, l’attributo del prodotto deve essere acquisito in ordine inverso e anche la chiamata API deve essere una stringa inversa. Ad esempio, se desideri cercare un nome di prodotto che termina con &quot;pantaloni&quot;, devi inviarlo come &quot;stnap&quot; (bloccaggio).

- **contiene l&#39;indicizzazione della ricerca** - Effettuare la ricerca di un attributo utilizzando l&#39;indicizzazione contains. Questa nuova funzionalità consente di:

   - Ricerca di una query all&#39;interno di una stringa più grande. Ad esempio, se un acquirente cerca il numero di prodotto &quot;PE-123&quot; nella stringa &quot;HAPE-123&quot;.

      - Nota: questo tipo di ricerca è diverso dalla [ricerca frase](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase) esistente, che esegue una ricerca di completamento automatico. Ad esempio, se il valore dell’attributo del prodotto è &quot;pantaloni da esterni&quot;, la ricerca di una frase restituisce una risposta per &quot;out pan&quot;, ma non restituisce una risposta per &quot;o formiche&quot;. Una ricerca contiene, tuttavia, restituisce una risposta per &quot;o formiche&quot;.

Queste nuove condizioni migliorano il meccanismo di filtro delle query di ricerca per perfezionare i risultati della ricerca. Queste nuove condizioni non influiscono sulla query di ricerca principale.

### Implementazione

1. [Impostare gli attributi come ricercabili](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata).

1. Specificare la funzionalità di ricerca per l&#39;attributo, ad esempio **Contains** (impostazione predefinita) o **Starts with**. È possibile specificare un massimo di sei attributi da abilitare per **Contains** e sei attributi da abilitare per **Starts with**. Inoltre, per l&#39;indicizzazione **Contains**, la lunghezza della stringa non può superare i 50 caratteri.

1. Consulta la [documentazione per gli sviluppatori](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) per esempi su come aggiornare le chiamate API [!DNL Commerce Optimizer] utilizzando le nuove funzionalità di ricerca di `contains` e `startsWith`.

   Puoi implementare queste nuove condizioni nella pagina dei risultati della ricerca. Ad esempio, puoi aggiungere una nuova sezione nella pagina in cui l’acquirente può perfezionare ulteriormente i risultati della ricerca. È possibile consentire agli acquirenti di selezionare attributi di prodotto specifici, ad esempio &quot;Produttore&quot;, &quot;Numero parte&quot; e &quot;Descrizione&quot;. Da lì, eseguono ricerche all&#39;interno di tali attributi utilizzando le condizioni `contains` o `startsWith`.

### Quando utilizzare la ricerca a livelli anziché i facet

La ricerca su più livelli e i facet hanno scopi diversi nell’individuazione del prodotto e la scelta tra di essi dipende dal caso d’uso specifico:

**Usa ricerca su più livelli per:**

- Ricerca nei risultati di ricerca utilizzando più criteri
- Utilizzare numeri di parte, SKU o specifiche tecniche in cui gli utenti conoscono informazioni parziali
- Consenti agli acquirenti di limitare i risultati passo dopo passo con i criteri nidificati
- Ridurre il numero di chiamate API combinando più criteri di ricerca in una singola query
- Implementare modelli di ricerca specifici per l’azienda che vanno oltre la navigazione con facet standard

**Usa facet per:**

- Fornisci un filtro tipico per categoria, prezzo, marchio e attributi
- Offri opzioni di filtro intuitive che gli utenti possono facilmente comprendere e selezionare
- Mostra le opzioni disponibili in base ai risultati di ricerca correnti
- Visualizza i conteggi dei filtri e gli intervalli che consentono agli utenti di comprendere le opzioni disponibili
- Lavorare con caratteristiche di prodotto comuni come colore, dimensioni, materiale e così via

**Best practice:** utilizza la ricerca su più livelli per ricerche tecniche complesse in cui gli utenti hanno criteri specifici e utilizza facet per il filtro standard dell&#39;e-commerce in cui gli utenti desiderano esplorare e perfezionare le opzioni visivamente.
