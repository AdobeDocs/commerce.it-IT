---
title: Panoramica dei facet
description: Scopri i facet in [!DNL Adobe Commerce Optimizer] e come migliorano i risultati della ricerca.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: cf16626e-8f85-47ca-b973-891b16c31fe3
source-git-commit: ad8fb7d1d7e1ad124647ba84377079dcfbd46a3c
workflow-type: tm+mt
source-wordcount: '338'
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

## Proprietà attributi non di sistema predefinite

Nella tabella seguente sono illustrate le proprietà predefinite di ricerca e filtrabili degli attributi non di sistema. L&#39;impostazione della proprietà dell&#39;attributo *Use in Search* su `Yes` rende l&#39;attributo ricercabile in [!DNL Adobe Commerce Optimizer].

| Codice attributo | Ricercabile |
|--- |--- |
| attività | Sì |
| attributes_brand | Sì |
| brand | Sì |
| clima | Sì |
| collare | Sì |
| colore | Sì |
| costo | Sì |
| eco_collection |
| genere | Sì |
| produttore | Sì |
| materiale | Sì |
| scopo | Sì |
| strap_bag | Sì |
| style_general | Sì |

## Proprietà attributi di sistema predefiniti

Nella tabella seguente vengono illustrate le proprietà predefinite di ricerca e filtrabili degli attributi di sistema.

| Codice attributo | Ricercabile |
|--- |--- |
| allow_open_amount | Sì |
| descrizione | Sì |
| name | Sì |
| prezzo | Sì |
| short_description | Sì |
| sku | Sì |
| stato | Sì |
| tax_class_id | Sì |
| url_key | Sì |
| peso | Sì |
