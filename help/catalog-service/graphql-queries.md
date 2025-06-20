---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Utilizza le query GraphQL per recuperare i dati del catalogo e potenziare le esperienze Commerce.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Recuperare i dati del catalogo con GraphQL {#graphql-queries}

Utilizza le query GraphQL per recuperare prodotti, prezzi e altri dati dallo spazio dati SaaS del catalogo Adobe Commerce e utilizzalo per riprodurre le esperienze Commerce in modo più rapido rispetto alle query GraphQL native di Adobe Commerce.

Catalog Service fornisce le seguenti query:

| Query | Descrizione | Utilizzo |
|-------|-------------|-------|
| `categories` | Restituisce i dati della categoria. Se viene specificato l&#39;oggetto di input della sottostruttura, la query restituisce i dettagli relativi alle sottocategorie. | Utile per il rendering delle pagine di navigazione e categoria della vetrina. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | Restituisce i dettagli sugli SKU specificati come input. | Utilizzato principalmente per riprodurre il contenuto sulle pagine di dettaglio e confronto dei prodotti. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | Restituisce un elenco di prodotti che corrispondono ai criteri di ricerca. | Utile per il rendering dei risultati di ricerca e delle pagine di elenco prodotti in base all’input di ricerca. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | Limita i risultati di una query di prodotti eseguita su un prodotto complesso per restituire informazioni specifiche su una variante di prodotto. | Utile per il rendering delle pagine dei dettagli del prodotto aggiornate quando gli acquirenti selezionano un’opzione di prodotto. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | Restituisce i dettagli di tutte le varianti di un prodotto. | Utile per mostrare immagini di varianti sui dettagli del prodotto o per elencare le pagine senza inviare più richieste API. [Vedi esempio.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

Per ulteriori informazioni sull&#39;utilizzo di queste query, vedere la [Guida API di Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
