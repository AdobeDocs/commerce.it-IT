---
title: Mappatura campi per  [!DNL Adobe Commerce Optimizer Connector] feed
description: Scopri [!DNL Adobe Commerce Optimizer Connector] la mappatura dei campi da [!DNL Adobe Commerce] dati catalogo a [!DNL Adobe Commerce Optimizer] formati API di acquisizione per tutti i feed.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 665
ht-degree: 0%

---


# Mappatura dei campi per i feed del connettore

In questa pagina viene illustrato come [!DNL Adobe Commerce Optimizer Connector] trasforma i campi del catalogo [!DNL Adobe Commerce] nel formato richiesto da [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]. Per un elenco dei feed supportati e dei relativi endpoint API, consulta il [riferimento connettore](connector-reference.md#supported-feeds).

## Prodotti

Il feed `products` invia dati all&#39;endpoint [Products](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}.

| Campo [!DNL Adobe Commerce] | Campo API [!DNL Commerce Optimizer] | Note |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin` risolto in `"AdobeCommerce"` |
| `status` | `status` | In maiuscolo; impostato su `DISABLED` per i prodotti compositi a cui non sono assegnati elementi figlio |
| `description` | `description` | |
| `shortDescription` | `shortDescription` | |
| `visibility` | `visibleIn` | Valore separato da virgole diviso e mappato: `Catalog`→`CATALOG`, `Search`→`SEARCH`; valori non mappati eliminati |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | Stringa delimitata da nuova riga divisa in matrice |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | Oggetto con codifica JSON `{inStock, lowStock, weight, weightType}`; sempre presente come prima voce di attributo |
| `attributes[]` | `attributes[]` | Ogni voce mappata a `{code, values[], variantReferenceId}`; `inStock`, `lowStock`, `weight`, `weightType` sono esclusi (entrano in `aco_ac_attributes`) |
| `images[]` | `images[]` | `url`, `label`; ruoli standard mappati: `image`→`BASE`, `small_image`→`SMALL`, `thumbnail`→`THUMBNAIL`, `swatch_image`→`SWATCH`; ruoli non standard vanno a `customRoles[]` |
| `categoryData[].categoryPath` | `routes[].path` | |
| `categoryData[].productPosition` | `routes[].position` | |
| `links[].type` + `links[].sku` | `links[]` | `type` in maiuscolo; voci senza `sku` eliminate |
| `parents[].productType` + `parents[].sku` | `links[]` | Tipo mappato: `configurable`→`VARIANT_OF`, `bundle`/`bundle_fixed`→`IN_BUNDLE` |
| `configurable options` | `configurations[]` | `id`→`attributeCode`, `label`; tipo di opzione `SWATCH` quando è impostato `swatchType`, altrimenti `CONFIGURABLE`; variante predefinita da `isDefault`; valori inclusi `variantReferenceId`, `label`, `colorHex`, `imageUrl` |
| `bundle options` | `bundles[]` | `label`→`group`; `required`; `renderType` `checkbox`/`multi`→`multiSelect: true`; SKU predefinite da `isDefault`; elementi inclusi `sku`, `qty`, `userDefinedQty` (`qtyMutability`) |

## Metadati degli attributi del prodotto

Il feed `productAttributes` invia dati all&#39;endpoint [metadati](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}.


| Campo [!DNL Adobe Commerce] | Campo API [!DNL Commerce Optimizer] | Note |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | Vedi la tabella di conversione seguente |
| `visible` | `visibleIn: "PRODUCT_DETAIL"` | Aggiunto all&#39;array quando `true` |
| `visibleInSearch` | `visibleIn: "SEARCH_RESULTS"` | Aggiunto all&#39;array quando `true` |
| `visibleInListing` | `visibleIn: "PRODUCT_LISTING"` | Aggiunto all&#39;array quando `true` |
| `visibleInCompareList` | `visibleIn: "PRODUCT_COMPARE"` | Aggiunto all&#39;array quando `true` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### Conversione del tipo di dati

Il connettore deriva l&#39;API `dataType` dai campi Commerce `dataType` e `frontendInput` nella tabella di mappatura precedente. Nella tabella seguente sono illustrate le regole di conversione applicate dal connettore.

| [!DNL Adobe Commerce] `dataType` | [!DNL Adobe Commerce] `frontendInput` | API [!DNL Commerce Optimizer] `dataType` |
| -------------------- | -------------------------- | ------------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` o `select` | `TEXT` |
| `int` | qualsiasi altro | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| qualsiasi altro | - | `TEXT` |

>[!NOTE]
>
>Quando `dataType` per un attributo è impostato su `OBJECT`, l&#39;API [products](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} tratta il valore dell&#39;attributo come un oggetto strutturato anziché come una stringa semplice. In fase di query, l’API tenta di analizzare il valore memorizzato come JSON. Se l&#39;analisi ha esito positivo, il risultato viene restituito come oggetto nidificato nella risposta. **Questo comportamento è particolarmente utile** quando si forniscono attributi personalizzati in modo dinamico, ad esempio per inserire dati strutturati o a più campi che non possono essere rappresentati come valori scalari. Per istruzioni, consulta [Aggiungere dinamicamente gli attributi del prodotto](../../data-export/add-attribute-dynamically.md).

## Listino prezzi

Il feed `priceBooks` invia dati all&#39;endpoint [Listini prezzi](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}.

A differenza degli altri feed del connettore, il feed `priceBooks` non viene raccolto da un indicizzatore [!DNL SaaS Data Export] in [!DNL Adobe Commerce]. Il connettore genera questo feed dal sito web e dalla configurazione del gruppo di clienti in Admin.

Viene creato un **listino prezzi di base** per sito Web, più un **listino prezzi figlio** per coppia sito-gruppo clienti.

**Formula ID registro prezzi:**

- **Base** (prezzi regolari): `priceBookId = websiteCode`
- **Secondario** (gruppo clienti o catalogo condiviso): `priceBookId = websiteCode::sha1(customerGroupId)` dove `sha1(customerGroupId)` è il digest esadecimale SHA-1 dell&#39;ID intero del gruppo clienti

Il feed dei prezzi utilizza la stessa formula per la risoluzione del listino prezzi a cui appartiene una voce di prezzo. Per informazioni sulla risoluzione di `priceBookId` per una sessione del cliente, vedere [Integrazione della vetrina headless](../headless-storefront.md#graphql-commerceoptimizer-query).

| Campo generato | Campo API [!DNL Commerce Optimizer] | Note |
| ---------------- | -------------- | ------- |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| Nome del sito web | `name` | Listino prezzi base: nome del sito Web. Figlio: `"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | Presente solo sui libri prezzi per bambini; punta al listino prezzi base |
| Valuta di base sito Web | `currency` | Presente solo sui libri di prezzi base; ereditato dai figli |

## Prezzi

Il feed `prices` invia i dati all&#39;endpoint [Price](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}.

| Campo [!DNL Adobe Commerce] | Campo API [!DNL Commerce Optimizer] | Note |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| `regular` | `regular` | |
| `discounts[]` | `discounts[]` | esempio di sconti: prezzo speciale, prezzo regola catalogo, prezzo catalogo condiviso |
| `tierPrices[]` | `tierPrices[]` | |

## Categorie

Il feed `categories` invia dati all&#39;endpoint [Categories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}.

Gli elementi con un `urlPath` vuoto (categorie radice logiche) vengono ignorati e non vengono mai inviati.

| Campo [!DNL Adobe Commerce] | Campo API [!DNL Commerce Optimizer] | Note |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | Stringa delimitata da nuova riga divisa in matrice |
| `image` | `images[].url` | Matrice a elemento singolo; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` quando `true`, `[]` altrimenti |

>[!MORELIKETHIS]
>
> - [Acquisire dati su prodotti e prezzi con l&#39;API Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}: scopri il modello dati del catalogo per metadati, prodotti, categorie, listini prezzi e prezzi
> - [Riferimento API REST per l&#39;acquisizione dei dati del catalogo](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — Rivedi gli schemi di richiesta e risposta per ogni endpoint di feed
> - [Funzionamento di  [!DNL Commerce Optimizer Connector] con [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce): scopri come le visualizzazioni dello store, i siti Web e i gruppi di clienti si associano alle origini del catalogo e ai listini prezzi
> - [Listini prezzi in [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md): gestisci listini prezzi creati dall&#39;esportazione del connettore
> - [Integrazione headless storefront](../headless-storefront.md#graphql-commerceoptimizer-query) — Risolvi `priceBookId` per le sessioni dei clienti
