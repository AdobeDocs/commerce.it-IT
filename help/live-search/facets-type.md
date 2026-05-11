---
title: Tipi di facet
description: '[!DNL Live Search] facet sono dinamici e vengono visualizzati nell''elenco Filtri quando necessario.'
exl-id: cd05c0c5-1028-4d66-951d-0b61c1ecc440
TQID: https://experienceleague.adobe.com/8cO5HLAkJLHHqyL-cYb3USCk4E9q1KSRJQ1fOGK0HB4
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 428
ht-degree: 0%

---

# Tipi di facet

[!DNL Live Search] utilizza diversi tipi di facet e vengono visualizzati nell&#39;elenco *Filtri* solo se pertinenti. L’elenco dei facet disponibili cambia in base ai prodotti restituiti. Le seguenti caratteristiche influiscono sulla loro presentazione e sul loro comportamento:

* Facet bloccati: i facet più comunemente utilizzati possono essere bloccati in alto nell’elenco. I facet rimanenti sono elencati nell&#39;ordine *Tipo di ordinamento* dopo i facet bloccati.
* Facet dinamici - Attributi del prodotto trovati più rilevanti per un set di prodotti e una query da [Adobe AI](https://business.adobe.com/ai.html). Il calcolo prende in considerazione i metadati dell’attributo dell’intero catalogo e determina in fase di query i facet più rilevanti per la query.

  >[!NOTE]
  >
  >Se dopo la creazione dei facet dinamici nella risposta alla query di GraphQL vengono visualizzati degli errori di timeout, modifica tutti i facet in modo che siano bloccati per vedere se i problemi di prestazioni vengono risolti.

* Facet popolari: attributi di prodotto più spesso presenti nei risultati di ricerca.
* Facet di prezzo - Restituisci i prodotti per fascia di prezzo. È possibile specificare il numero di selezioni e l&#39;intervallo di prezzi nell&#39;area di lavoro [*Impostazioni*](settings.md).

Al momento della query, [!DNL Live Search] genera i risultati della ricerca in gruppi di facet dinamici e popolari.

![Facet - Prezzo](assets/storefront-search-results-run-price.png)

## Opzioni vetrina e headless

I facet di cui viene eseguito il rendering per la vetrina [!DNL Commerce] vengono elaborati dall&#39;adattatore di ricerca, che indirizza le richieste ed esegue il rendering dei risultati nella vetrina. Tutti i facet [!DNL Commerce] della vetrina sono ordinati alfabeticamente con opzioni di selezione singola, indipendentemente dal tipo di input assegnato all&#39;attributo corrispondente. I facet disponibili nella vetrina vengono riprodotti in base al tema corrente e riflettono eventuali personalizzazioni apportate alla presentazione della navigazione a livelli.

Al contrario, [implementazioni headless](https://developer.adobe.com/commerce/php/architecture/technical-vision/web-api/) vengono elaborate dall&#39;API e supportano opzioni aggiuntive. I facet headless possono essere ordinati alfabeticamente o per conteggio e possono avere opzioni a selezione singola o multipla.

### Etichette facet

Per [!DNL Commerce] storefronts, l&#39;etichetta del facet è determinata dalle [*Proprietà attributo*](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html). Per gli archivi con più visualizzazioni, è possibile definire etichette aggiuntive in *Gestisci etichette*. Per le implementazioni headless, le etichette vengono modificate dall&#39;[area di lavoro faceting](faceting-workspace.md).

### Tipo di ordinamento

Tutti i facet di cui è stato eseguito il rendering per la vetrina sono ordinati alfabeticamente. Per le implementazioni headless, i facet possono essere ordinati alfabeticamente o per conteggio.

| Tipo di ordinamento | Descrizione |
|--- |--- |
| Alfabetico | Nell&#39;elenco *Filtri* della vetrina, i facet sono ordinati alfabeticamente. |
| Conteggio | (Solo headless) Per le implementazioni headless, i facet possono essere ordinati anche in base al numero di valori trovati per facet nel set corrente di prodotti restituiti. |
