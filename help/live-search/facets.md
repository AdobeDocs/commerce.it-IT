---
title: Facet
description: '[!DNL Live Search] facet utilizzano più dimensioni di valori di attributo come criteri di ricerca.'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
source-git-commit: 86484d49aa4b79bfe64455dba18b84bcd9073736
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# Facet

Faceting è un metodo di filtro ad alte prestazioni che utilizza più dimensioni di valori di attributo come criteri di ricerca. La ricerca con facet è simile, ma considerevolmente &quot;più intelligente&quot; rispetto alla [navigazione a più livelli](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html) standard. L&#39;elenco dei filtri disponibili è determinato dai [attributi filtrabili](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html#filterable-attributes) dei prodotti restituiti nei risultati della ricerca.

[!DNL Live Search] utilizza la query `productSearch`, che restituisce faceting e altri dati specifici di [!DNL Live Search]. Per esempi di codice, fare riferimento a [`productSearch` query](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) nella documentazione per gli sviluppatori.

![Risultati ricerca filtrati](assets/storefront-search-results-run.png)

All’interno di un facet, gli acquirenti possono selezionare più opzioni, ad esempio &quot;Basic&quot; e &quot;Snug&quot; in &quot;Style&quot; e i risultati della ricerca vengono aggiornati per visualizzare solo questi stili. Allo stesso modo, se un acquirente seleziona le opzioni tra i facet, come &quot;Basic&quot; in &quot;Style&quot; e &quot;Indoor&quot; in &quot;Climate&quot;, i risultati della ricerca vengono aggiornati per mostrare lo stile selezionato e il clima selezionato.

Qualsiasi facet definito può essere utilizzato come parametro URL e i risultati verranno filtrati in base ai valori del parametro: `http://yourstore.com?brand=acme&color=red`.

## Requisiti di sfaccettato

I requisiti degli attributi di categoria e prodotto per il faceting sono simili agli attributi filtrabili utilizzati per la navigazione su più livelli. Per ogni proprietà della vetrina di un attributo, il valore &quot;Use in Search Results Layered Navigation&quot; (Usa nei risultati di ricerca a livello di navigazione) deve essere impostato su &quot;Yes&quot; (Sì). È possibile rivedere e aggiornare la configurazione dell&#39;attributo dal menu [!DNL Stores] > [!DNL Attribute] in Amministrazione.

>[!NOTE]
>
>Se si definisce una categoria di prodotto come facet, il facet visualizza il `url_path` della categoria e della sottocategoria.
>
>![Facet categoria](assets/facet-category.png)

Per ulteriori informazioni sui requisiti del facet in [, consulta ](./boundaries-limits.md#facets)limiti e limitazioni[!DNL Live Search].

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
