---
title: Facet
description: '[!DNL Live Search] facet utilizzano più dimensioni di valori di attributo come criteri di ricerca.'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---

# Facet

Faceting è un metodo di filtro ad alte prestazioni che utilizza più dimensioni di valori di attributo come criteri di ricerca. La ricerca con facet è simile, ma considerevolmente &quot;più intelligente&quot; rispetto alla [navigazione a più livelli](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html) standard. L&#39;elenco dei filtri disponibili è determinato dai [attributi filtrabili](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html#filterable-attributes) dei prodotti restituiti nei risultati della ricerca.

[!DNL Live Search] utilizza la query `productSearch`, che restituisce faceting e altri dati specifici di [!DNL Live Search]. Per esempi di codice, fare riferimento a [`productSearch` query](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) nella documentazione per gli sviluppatori.

![Risultati ricerca filtrati](assets/storefront-search-results-run.png)

All’interno di un facet, gli acquirenti possono selezionare più opzioni, ad esempio &quot;Basic&quot; e &quot;Snug&quot; in &quot;Style&quot; e i risultati della ricerca vengono aggiornati per visualizzare solo questi stili. Allo stesso modo, se un acquirente seleziona le opzioni tra i facet, come &quot;Basic&quot; in &quot;Style&quot; e &quot;Indoor&quot; in &quot;Climate&quot;, i risultati della ricerca vengono aggiornati per mostrare lo stile selezionato e il clima selezionato.

Qualsiasi facet definito può essere utilizzato come parametro URL e i risultati verranno filtrati in base ai valori del parametro: `http://yourstore.com?brand=acme&color=red`.

## Requisiti di sfaccettato

I requisiti degli attributi di categoria e prodotto per il faceting sono simili agli attributi filtrabili utilizzati per la navigazione su più livelli. Per ogni proprietà della vetrina di un attributo, il valore &quot;Use in Search Results Layered Navigation&quot; (Usa nei risultati di ricerca a livello di navigazione) deve essere impostato su &quot;Yes&quot; (Sì).

[!DNL Live Search] supporta fino a:

* 100 attributi configurati come facet
* 50 attributi ordinabili
* 200 attributi filtrabili
* 200 attributi ricercabili

>[!NOTE]
>
> Se sono definiti più di 200 attributi filtrabili, non è deterministico quali 200 saranno effettivamente indicizzati.

Se hai a che fare con un numero elevato di attributi, puoi combinarli in un singolo &quot;meta-attribute&quot;. Ad esempio, le scarpe hanno generalmente dimensioni numeriche, mentre le magliette hanno generalmente le dimensioni &quot;S/M/L/XL&quot;. Questi due tipi di dimensioni possono essere combinati in un unico attributo ricercabile.

| Impostazione | Descrizione |
|--- |--- |
| [Impostazioni visualizzazione categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-display-settings.html) | Ancoraggio - `Yes` |
| [Proprietà attributo](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html) | [Tipo di input catalogo](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/attributes-input-types.html) - `Yes/No`, `Dropdown`, `Multiple Select`, `Price`, `Visual swatch` (solo widget), `Text swatch` (solo widget) |
| Proprietà vetrina attributo | Utilizzo in navigazione a livelli dei risultati di ricerca - `Yes` |

## Aggregazione facet

L&#39;aggregazione sfaccettatura viene eseguita come segue: se la vetrina ha tre sfaccettature (categorie, colore e prezzo) e i filtri acquirente su tutte e tre (colore = blu, prezzo = $ 10.00-50,00, categorie = `promotions`).

* Aggregazione `categories`: aggrega `categories`, quindi applica i filtri `color` e `price`, ma non il filtro `categories`.
* Aggregazione `color`: aggrega `color`, quindi applica i filtri `price` e `categories`, ma non il filtro `color`.
* Aggregazione `price`: aggrega `price`, quindi applica i filtri `color` e `categories`, ma non il filtro `price`.

## Valori attributi predefiniti

I seguenti attributi di prodotto hanno [proprietà storefront](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) utilizzate da [!DNL Live Search] e abilitate per impostazione predefinita.

| Proprietà | Storefront, proprietà | Attributo |
|---|---|---|
| Ordinabile | Utilizzato per l’ordinamento nell’elenco prodotti | `price` |
| Ricercabile | Uso nella ricerca | `price` <br />`sku`<br />`name` |
| FilterableInSearch | Uso in navigazione a livelli - Filtrabile (con risultati) | `price`<br />`visibility`<br />`category_name` |

## Proprietà attributi non di sistema predefinite

La tabella seguente mostra le proprietà predefinite di ricerca e filtrabili degli attributi non di sistema, inclusi quelli specifici dei dati di esempio Luma. Se si imposta la proprietà dell&#39;attributo *Use in Search* su `Yes`, sarà possibile eseguire ricerche sia in [!DNL Live Search] che in Adobe Commerce nativo.

| Codice attributo | Ricercabile | Uso in navigazione a livelli |
|--- |--- |--- |
| attività | Sì | Filtrabile (con risultati) |
| attributes_brand | Sì | No |
| brand | Sì | No |
| clima | Sì | Filtrabile (con risultati) |
| collare | Sì | Filtrabile (con risultati) |
| colore | Sì | Filtrabile (con risultati) |
| costo | Sì | No |
| eco_collection | Sì | Filtrabile (con risultati) |
| genere | Sì | Filtrabile (con risultati) |
| produttore | Sì | Filtrabile (con risultati) |
| materiale | Sì | Filtrabile (con risultati) |
| scopo | Sì | Filtrabile (con risultati) |
| strap_bag | Sì | Filtrabile (con risultati) |
| style_general | Sì | Filtrabile (con risultati) |

## Proprietà attributi di sistema predefiniti

Nella tabella seguente vengono illustrate le proprietà predefinite di ricerca e filtrabili degli attributi di sistema.

| Codice attributo | Ricercabile | Uso in navigazione a livelli |
|--- |--- |--- |
| allow_open_amount | Sì | Filtrabile (con risultati) |
| descrizione | Sì | No |
| name | Sì | No |
| prezzo | Sì | Filtrabile (con risultati) |
| short_description | Sì | No |
| sku | Sì | No |
| stato | Sì | No |
| tax_class_id | Sì | No |
| url_key | Sì | No |
| peso | Sì | No |
