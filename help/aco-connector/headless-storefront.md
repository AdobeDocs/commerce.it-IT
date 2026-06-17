---
title: Integrazione con [!DNL Adobe Commerce Optimizer Connector] Headless Storefront
description: Scopri come integrare i punti vendita headless con l’API di  [!DNL Adobe Commerce Optimizer Connector] GraphQL, gli ID del listino prezzi dedicato e la codifica bundle add-to-cart.
feature: Storefront, Integration, GraphQL
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T16:27:30.102Z'
TQID: 'https://experienceleague.adobe.com/Orif1rROglTQ-3ZkRj5LMF90Y-AdpfTnOgPmJXQjYgc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 0%

---

# Integrazione con la vetrina headless

Il modulo `CommerceAdapter` estende [!DNL Adobe Commerce] per colmare il gap tra una vetrina headless e [!DNL Adobe Commerce Optimizer]. Fornisce una query GraphQL per la risoluzione del contesto del listino prezzi cliente e applica la codifica del prodotto bundle prevista dall&#39;API GraphQL [!DNL Adobe Commerce Optimizer].

Per le istruzioni di configurazione della vetrina di alto livello, vedere [Configurare merchandising e vetrine](./overview.md#merchandising-storefronts) nella panoramica di [!DNL Adobe Commerce Optimizer Connector].

## GraphQL: query `commerceOptimizer` {#graphql-commerceoptimizer-query}

Gli storefront headless chiamano la query GraphQL `commerceOptimizer` per recuperare `priceBookId` per la sessione cliente corrente. Trasferisci questo valore all&#39;[[!DNL Adobe Commerce Optimizer] API GraphQL](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api){target="_blank"} durante il recupero dei prezzi.

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

Esempio di risposta:

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

Risoluzione di `priceBookId`:

| Stato sessione | `priceBookId` |
|-----------------------|---------------------------------------------------------------------|
| Guest (non connesso) | `websiteCode::sha1(0)`, dove `0` è l&#39;ID gruppo clienti guest |
| Cliente connesso | `websiteCode::sha1(customerGroupId)` |

L&#39;intestazione della richiesta `Store` determina l&#39;ambito del sito Web e quindi il componente `websiteCode`. Il componente `sha1(customerGroupId)` corrisponde alla formula ID listino prezzi utilizzata durante la sincronizzazione dei dati. Consulta [Listino prezzi](reference/field-mapping.md#price-books).

## Prodotti bundle: formato add-to-cart {#bundle-products-add-to-cart-format}

Consenti agli acquirenti di aggiungere prodotti bundle al carrello da una vetrina headless con solo `SKU` e `qty` per ogni opzione bundle selezionata.

Ogni valore di opzione selezionato o immesso deve essere codificato in base64 nel formato seguente:

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

Lo stesso SKU figlio può essere visualizzato una sola volta in tutte le opzioni.

Esempio ([!DNL JavaScript]):

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
