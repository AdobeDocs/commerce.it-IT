---
title: GraphQL
description: L'area di lavoro di  [!DNL Live Search] GraphQL ti consente di creare query con i tuoi dati live.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

L&#39;area di lavoro *GraphQL* consente agli amministratori di generare e testare le query GraphQL utilizzando i propri dati.

Questa area di lavoro supporta le query [`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/) e [`attributeMetadata`](https://developer.adobe.com/commerce/services/graphql/live-search/attribute-metadata/).

![Area di lavoro GraphQL](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
		name
      }
    }
    facets {
      title
    }
  }
}
```

Variabili:

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```

