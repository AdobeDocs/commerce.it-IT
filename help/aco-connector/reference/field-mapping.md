---
title: Mappatura campi per [!DNL Adobe Commerce Optimizer Connector] feed
description: Scopri come mappare il campo [!DNL Adobe Commerce Optimizer Connector] dai dati del catalogo [!DNL Adobe Commerce] ai formati API di acquisizione [!DNL Adobe Commerce Optimizer] per tutti i feed.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
source-git-commit: 1e34df4f07f9043675104fce55c58e0617463b33
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 2%
---

# Mappatura dei campi per i feed del connettore

In questa pagina viene illustrato come [!DNL Adobe Commerce Optimizer Connector] trasforma i campi del catalogo [!DNL Adobe Commerce] nel formato richiesto da [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]. Per un elenco dei feed supportati e dei relativi endpoint API, consulta il [riferimento connettore](connector-reference.md#supported-feeds).

## Prodotti

Il feed `products` invia dati all&#39;endpoint [Products](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}.

| Campo [!DNL Adobe Commerce] | Campo API [!DNL Commerce Optimizer] | Dettagli mappatura |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | Imposta `origin` su `"AdobeCommerce"` |
| `status` | `status` | Converte lo stato in maiuscolo. Usa `DISABLED` se lo stato è mancante o se un prodotto configurabile o bundle non ha valori di opzione. |
| `description` | `description` | Se manca la descrizione, utilizza una stringa vuota. |
| `shortDescription` | `shortDescription` | Se manca la descrizione breve, utilizza una stringa vuota. |
| `visibility` | `visibleIn` | Divide il valore separato da virgole e mappa `Catalog` in `CATALOG` e `Search` in `SEARCH`. Elimina altri valori. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | Divide le parole chiave separate da una nuova riga in un array e taglia gli spazi vuoti. |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | Aggiunge sempre una voce `aco_ac_attributes` come primo attributo. Il valore JSON include `inStock` e `lowStock` come stringhe. Include `weight` e `weightType` quando tali valori sono disponibili. |
| `attributes[]` | `attributes[]` | Mappa ciascuna voce al relativo codice attributo, ai valori stringa e all’ID di riferimento della variante corrispondente, se disponibile. Ignora `inStock`, `lowStock`, `categories`, `weight` e `weightType`. I valori relativi all&#39;inventario sono inclusi in `aco_ac_attributes`. Le categorie vengono esportate come cicli di lavorazione. |
| `images[]` | `images[]` | Ignora le immagini senza un URL.<br>Esporta `url`, `label` (vuoto se mancante) e `sortOrder` (numero intero, predefinito `0`).<br>Ordina le immagini per `sortOrder` in ordine crescente.<br>Esegue il mapping dei ruoli standard: `image` a `BASE`, `small_image` a `SMALL`, `thumbnail` a `THUMBNAIL` e `swatch_image` a `SWATCH`. Esporta altri ruoli come `customRoles[]`. |
| `categoryData[].categoryPath` | `routes[].path` | Ignora le voci con un percorso di categoria vuoto. |
| `categoryData[].productPosition` | `routes[].position` | Usa `0` se manca la posizione del prodotto. |
| `links[].type` + `links[].sku` | `links[]` | `type` in maiuscolo; voci senza `sku` eliminate |
| `parents[].productType` + `parents[].sku` | `links[]` | Esegue il mapping di `configurable` a `VARIANT_OF` e di `bundle` o `bundle_fixed` a `IN_BUNDLE`. Converte altri tipi di prodotto in maiuscolo. Ignora i genitori senza SKU. |
| `configurable options` | `configurations[]` | Esporta le opzioni che hanno un ID e almeno un valore.<br>Associa `id` a `attributeCode`. Imposta `type` su `SWATCH` quando `swatchType` è presente, e su `CONFIGURABLE` in caso contrario.<br>Utilizza l&#39;ID del valore predefinito come `defaultVariantReferenceId`.<br>Mappa ogni valore su `variantReferenceId`, `label`, `colorHex` e `imageUrl`. |
| `bundle options` | `bundles[]` | Esporta le opzioni che contengono almeno un elemento.<br>Utilizza l&#39;etichetta dell&#39;opzione come `group` oppure `Bundle group` se l&#39;etichetta è vuota. Copia `required` nell&#39;output.<br>Imposta `multiSelect` su `true` per i tipi di rendering `checkbox` e `multi`.<br>Elenca gli SKU predefiniti in `defaultItemSkus`. Ogni elemento include `sku`, `qty` (impostazione predefinita: `0`) e `userDefinedQty` (da `qtyMutability`, impostazione predefinita: `false`). |

## Metadati degli attributi del prodotto

Il feed `productAttributes` invia dati all&#39;endpoint [metadati](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}.

| Campo [!DNL Adobe Commerce] | Campo API [!DNL Commerce Optimizer] | Dettagli mappatura |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | Vedi la tabella di conversione seguente |
| `dataType` e `frontendInput` | `dataType` | Utilizza le regole di conversione seguenti. |
| `visible`, `visibleInSearch`, `visibleInListing`, `visibleInCompareList` | `visibleIn[]` | Quando un flag è `true`, aggiunge il valore corrispondente:<br>`visible` → `PRODUCT_DETAIL`<br>`visibleInSearch` → `SEARCH_RESULTS`<br>`visibleInListing` → `PRODUCT_LISTING`<br>`visibleInCompareList` → `PRODUCT_COMPARE` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### Conversione del tipo di dati

Quando `dataType` è `int`, il connettore controlla `frontendInput`. Per altri tipi di dati, `frontendInput` non influisce sulla conversione.

| Input `dataType` | Input `frontendInput` | Output `dataType` |
| ---------------- | --------------------- | ----------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` o `select` | `TEXT` |
| `int` | Qualsiasi altro valore, incluso un valore mancante | `INTEGER` |
| `decimal` | Non utilizzato | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | Non utilizzato | `TEXT` |
| `OBJECT` | Non utilizzato | `OBJECT` |
| Qualsiasi altro valore | Non utilizzato | `TEXT` |

>[!NOTE]
>
>Quando un attributo utilizza il tipo di dati `OBJECT`, l&#39;API [Products](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} tenta di analizzare il valore memorizzato come JSON. Se l’analisi riesce, l’API restituisce il valore come oggetto nidificato. Utilizzare `OBJECT` per dati di attributi strutturati che non possono essere rappresentati come un singolo valore. Per istruzioni, consulta [Aggiungere dinamicamente gli attributi del prodotto](../../data-export/add-attribute-dynamically.md).

## Listino prezzi

Il feed `priceBooks` invia dati all&#39;endpoint [Listini prezzi](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}.

A differenza degli altri feed del connettore, il feed `priceBooks` non viene raccolto da un indicizzatore [!DNL SaaS Data Export] in [!DNL Adobe Commerce]. Il connettore genera questo feed dal sito web e dalla configurazione del gruppo di clienti in Admin.

Per ogni sito web, il connettore crea un listino prezzi base e un listino prezzi dedicato figlio per ogni gruppo di clienti.

Usa queste formule per `priceBookId`:

- Libretti prezzi base per prezzi regolari: `priceBookId = websiteCode`.
- Listini prezzi figlio per gruppi di clienti: `priceBookId = websiteCode::sha1(customerGroupId)`, dove `sha1(customerGroupId)` è il digest esadecimale SHA-1 dell&#39;ID intero del gruppo di clienti.

Il feed prezzi utilizza la stessa formula per assegnare ogni voce di prezzo a un listino prezzi dedicato. Per informazioni sulla risoluzione di `priceBookId` da parte di una vetrina per una sessione del cliente, vedi [Integrazione della vetrina headless](../headless-storefront.md#graphql-commerceoptimizer-query).


| Campo o valore Source | Campo API [!DNL Commerce Optimizer] | Dettagli mappatura |
| ---------------- | -------------- | ------- |
| `websiteCode` | `parentId` | Aggiunge questo campo ai listini prezzi figlio. Il valore identifica il listino prezzi base. |
| Nome del sito web | `name` | Utilizza il nome del sito Web per i listini prezzi base. Usa `Customer group name (Website name)` per i listini prezzi figli. |
| `websiteCode` | `parentId` | Presente solo sui libri prezzi per bambini; punta al listino prezzi base |
| Valuta di base sito Web | `currency` | Include questo campo solo nei listini prezzi base. I libri dei prezzi per bambini lo omettono. |

## Prezzi

Il feed `prices` invia [!DNL Adobe Commerce] dati all&#39;endpoint [Price](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}.

| Campo di input feed | Campo API [!DNL Commerce Optimizer] | Dettagli mappatura |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | Passa lo SKU senza modificarlo. |
| `websiteCode`, `customerGroupCode` | `priceBookId` | Combina `websiteCode` con l&#39;hash SHA-1 dell&#39;ID gruppo cliente in `customerGroupCode`. Se `customerGroupCode` è `0`, usa solo `websiteCode`. |
| `regular` | `regular` | Trasmette il prezzo regolare senza modifiche. |
| `discounts[]` | `discounts[]` | Se il valore di origine è `null`, esporta un array vuoto.<br>Per le voci con `code` impostato su `special_price` e un `percentage`, imposta `percentage` su `100 - percentage` quando il valore è compreso tra `0` e `100`. Imposta su `0` all&#39;interno o all&#39;esterno dell&#39;intervallo.<br>Le altre voci, inclusi i prezzi speciali basati sui prezzi, vengono passate senza modifiche. |
| `tierPrices[]` | `tierPrices[]` | Utilizza un array vuoto se manca il valore di origine o `null`. |

## Categorie

Il feed `categories` invia [!DNL Adobe Commerce] dati all&#39;endpoint [Categories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}.

Gli elementi con un `urlPath` vuoto (categorie radice logiche) vengono ignorati e non vengono mai inviati.

| Campo [!DNL Adobe Commerce] | Campo API [!DNL Commerce Optimizer] | Dettagli mappatura |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `position` | `position` | Esporta la posizione della categoria quando presente. Omette il campo quando manca. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | Stringa delimitata da nuova riga divisa in matrice |
| `image` | `images[].url` | Matrice a elemento singolo; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` quando `true`, `[]` altrimenti |

| `metaKeywords` | `metaTags/keywords` | Divide le parole chiave delimitate da una nuova riga in un array e taglia gli spazi vuoti. |
| `image` | `images[].url` | Se è presente `image`, esporta un&#39;immagine con la mansione `BASE`. Esporta una matrice vuota quando l&#39;immagine è vuota o mancante. |
| `isActive` + `includeInMenu` | `families` | Aggiunge `top_menu` solo quando entrambi i valori sono `true`. In caso contrario, esporta un array vuoto. |
| `attributes[]` | `attributes[]` | Esporta le voci con `attributeCode` non vuoto come `{code, values[]}`. Converte i valori in stringhe. Omette `attributes` quando non esistono voci idonee. |

>[!MORELIKETHIS]
>
> - [Acquisire dati su prodotti e prezzi con l&#39;API Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}: scopri il modello dati del catalogo per metadati, prodotti, categorie, listini prezzi e prezzi
> - [Riferimento API REST per l&#39;acquisizione dei dati del catalogo](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — Rivedi gli schemi di richiesta e risposta per ogni endpoint di feed
> - [Funzionamento di  [!DNL Commerce Optimizer Connector] con [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce): scopri come le visualizzazioni dello store, i siti Web e i gruppi di clienti si associano alle origini del catalogo e ai listini prezzi
> - [Listini prezzi in [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md): gestisci listini prezzi creati dall&#39;esportazione del connettore
> - [Integrazione headless storefront](../headless-storefront.md#graphql-commerceoptimizer-query) — Risolvi `priceBookId` per le sessioni dei clienti
