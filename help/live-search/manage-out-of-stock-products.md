---
title: Gestisci prodotti esauriti in [!DNL Live Search]
description: Scopri come gestire i prodotti esauriti in [!DNL Live Search] per Adobe Commerce. Configura la visualizzazione dell’inventario, il filtro in Stock e il filtro API GraphQL.
feature: Services, Search
role: Admin, Developer
level: Intermediate
source-git-commit: bc8f35434c9f01f1a920745fe42617df2003ca60
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Gestire i prodotti esauriti

È possibile controllare la modalità di visualizzazione dei prodotti esauriti nei risultati di ricerca e categoria di [!DNL Live Search] utilizzando la configurazione dell&#39;inventario, i filtri di query e i flag di funzionalità di back-end facoltativi. Queste opzioni hanno dei limiti importanti, come viene spiegato in questo argomento.

## Filtri di stato del magazzino

L&#39;attributo di Adobe Commerce Stock `quantity_and_stock_status` non è supportato come facet e non viene visualizzato nella finestra di dialogo **[!UICONTROL Add Facet]**. Tuttavia, [!DNL Live Search] espone un campo `inStock` che è possibile utilizzare come filtro in fase di query.

## Nascondi prodotti esauriti

Utilizza uno dei seguenti approcci per nascondere i prodotti esauriti.

### Configurazione Commerce

1.Da *Amministratore*, passare a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Catalog]**>**[!UICONTROL Inventory]**.

1.Impostare **[!UICONTROL Display Out of Stock Products]** su **[!UICONTROL No]**.

1. Fare clic su **[!UICONTROL Save Config]**.

Quando **[!UICONTROL Display Out of Stock Products]** è impostato su `No`, [!DNL Live Search] aggiunge `inStock = 'no` alle query storefront tramite il widget PLP, pertanto i prodotti esauriti non vengono restituiti.

### Filtro API

Quando chiami direttamente l&#39;API [!DNL Live Search] (GraphQL o REST), filtra esplicitamente i prodotti esauriti, ad esempio:

```graphql
query productSearchInStockOnly {
  productSearch(
    phrase: ""
    filter: [
      { attribute: "inStock", eq: "true" }
    ]
  ) {
    total_count
    items {
      productView {
        sku
        name
        inStock
      }
    }
  }
}
```

Utilizzare questo approccio quando non si instrada la richiesta tramite il [widget PLP di Live Search](plp-styling.md).

### Mostra risultati esauriti dopo i risultati in magazzino

Per mantenere i prodotti esauriti nel set di risultati ma sempre dopo i prodotti in magazzino quando si ordina per rilevanza, Adobe può abilitare un flag di funzione interno per il tuo ambiente.

- Questo flag di funzione non è esposto nell&#39;interfaccia utente di amministrazione di [!DNL Live Search].
- Per richiederlo, [contatta il supporto Adobe](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"} e fai riferimento alla funzionalità per spostare i prodotti esauriti alla fine dei risultati della ricerca.

>[!NOTE]
>
>Dopo l&#39;attivazione del flag, tutti i prodotti esauriti rimanenti nel set di risultati vengono spostati in fondo all&#39;ordinamento in base a *Rilevanza*. Altri tipi di ordinamento (ad esempio, *Prezzo* o *Nome prodotto*) non sono interessati.

### Cerca regole e azioni di merchandising

Le regole di ricerca di merchandising sono basate su query e si rivolgono a singoli prodotti, non a gruppi interi in base allo stato azionario o al valore di facet:

- Le condizioni delle regole dipendono solo dalla frase di ricerca dell&#39;acquirente (`Query is`, `Query contains`, `Query starts with`, `Query ends with`).
- Gli eventi di regola (Incremento, Interruzione, Fissa, Nascondi) si applicano a un SKU per evento.

A causa di questi vincoli:

- Non è possibile creare una regola che nasconda o nasconda tutti i prodotti esauriti solo in base allo stato delle scorte.
- Puoi nascondere o nascondere manualmente gli SKU specifici aggiunti come eventi in una regola (entro il limite di 50 regole e 25 eventi per regola).

Per nascondere o rimuovere la priorità dei prodotti esauriti nel catalogo, utilizza la configurazione dell’inventario e il filtro `inStock` (e il flag di funzione opzionale) descritti in questo argomento anziché cercare le regole di merchandising.

>[!MORELIKETHIS]
>
> - [Cerca regole di merchandising](rules.md)
> - [Configurare le opzioni globali di Inventory management](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/configuration/configuration)
