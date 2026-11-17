---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/facets/type.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Tipi di facet

I facet sono disponibili in diversi tipi e vengono visualizzati nell&#39;elenco *Filtri* solo se pertinenti. L’elenco dei facet disponibili cambia in base ai prodotti restituiti. Le seguenti caratteristiche influiscono sulla loro presentazione e sul loro comportamento:

- Facet bloccati (Pinned Facets) - I facet più comunemente utilizzati possono essere bloccati nella parte superiore dell&#39;elenco. I facet rimanenti sono elencati nell&#39;ordine *Tipo di ordinamento* dopo i facet bloccati.
- Facet dinamici: attributi di prodotto trovati più rilevanti per un set di prodotti e una query da [Adobe AI](https://business.adobe.com/ai.html). Il calcolo prende in considerazione i metadati dell’attributo dell’intero catalogo e determina in fase di query i facet più rilevanti per la query.
- Facet di prezzo: restituisce i prodotti in base alla fascia di prezzo. È possibile specificare il numero di selezioni e l&#39;intervallo di prezzi nell&#39;area di lavoro [*Impostazioni*](https://experienceleague.adobe.com/en/docs/commerce/optimizer/settings).

## Etichette facet

È possibile modificare le etichette dei facet dall&#39;[area di lavoro facet](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/facets/workspace).

## Tipo di ordinamento

Tutti i facet di cui è stato eseguito il rendering per la vetrina sono ordinati alfabeticamente o per conteggio.

| Tipo di ordinamento | Descrizione |
|--- |--- |
| Alfabetico | Nell&#39;elenco *Filtri* della vetrina, i facet sono ordinati alfabeticamente. |
| Conteggio | I facet possono anche essere ordinati in base al numero di valori trovati per facet nel set corrente di prodotti restituiti. |
