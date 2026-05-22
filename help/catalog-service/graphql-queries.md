---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Utilizza le query GraphQL per recuperare i dati del catalogo e potenziare le esperienze Commerce.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
TQID: https://experienceleague.adobe.com/ahutwotbB6Dxg7Tc3WMFd7S-WBMALvOYIUTmB5JKmyM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: d842311424e76b83a131ada7a2db6e3fb868acd8
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# Recuperare i dati del catalogo con GraphQL {#graphql-queries}

Utilizza le query GraphQL per recuperare i dati di prodotti, prezzi e altri dati di catalogo dallo spazio dati [!DNL Catalog Service] ed eseguire il rendering di [!DNL Adobe Commerce] esperienze di vetrina più rapidamente rispetto alle query di prodotti native.

{{aco-merchandising-services}}

[!DNL Catalog Service] fornisce le query seguenti:

| Query | Descrizione | Utilizzo | Limiti |
| --- | --- | --- | --- |
| `categories` | Restituisce i dati della categoria. Se si specifica l&#39;oggetto di input `subtree`, la query restituirà dettagli sulle sottocategorie. | Utile per il rendering delle pagine di navigazione e categoria della vetrina. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/){target="_blank"} | — |
| `products` | Restituisce i dettagli sugli SKU specificati come input. | Utilizzato principalmente per riprodurre il contenuto sulle pagine di dettaglio e confronto dei prodotti. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} | 100 SKU per richiesta |
| `productSearch` | Restituisce un elenco di prodotti che corrispondono ai criteri di ricerca. | Utile per il rendering dei risultati di ricerca e delle pagine di elenco prodotti in base all’input di ricerca. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/){target="_blank"} | 100 SKU per richiesta |
| `refineProduct` | Limita i risultati della query `products` per un prodotto complesso per restituire informazioni specifiche su una variante di prodotto. | Utile per il rendering delle pagine dei dettagli del prodotto aggiornate quando gli acquirenti selezionano un’opzione di prodotto. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/){target="_blank"} | 100 SKU per richiesta |
| `variants` | Restituisce i dettagli di tutte le varianti di un prodotto. | Utile per mostrare immagini di varianti sui dettagli del prodotto o per elencare le pagine senza inviare più richieste API. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/){target="_blank"} | 100 SKU per richiesta |

{style="table-layout:auto"}

Per ulteriori informazioni sull&#39;utilizzo di queste query, vedere [Servizi Storefront GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/){target="_blank"}.
