---
title: Storefront
description: Scopri le opzioni della vetrina Adobe Commerce, incluso Commerce Storefront con tecnologia Edge Delivery Services e le implementazioni headless personalizzate.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:22.967Z'
TQID: 'https://experienceleague.adobe.com/1mQm2s3UGzr7S4j9RMZAaRoUVtzu93N1IFbOypR8vkA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%
---

# Storefront

La vetrina è separata dal backend Commerce e dai livelli API. A seconda dell&#39;architettura selezionata, una vetrina può recuperare dati dalle API di Commerce Foundation, dalle API di Storefront Services, dalle API di [!DNL Adobe Commerce Optimizer] Merchandising Services o dai sistemi connessi tramite API Mesh, App Builder o altri meccanismi di integrazione. Consulta [Opzioni di architettura](../architecture-options/overview.md) per vedere come ogni vetrina si abbina a un backend Commerce.

## Commerce Storefront con tecnologia Edge Delivery Services

Commerce Storefront con tecnologia [!DNL Edge Delivery Services] è un&#39;opzione di vetrina per il cliente basata sulla piattaforma standard Adobe Commerce, che utilizza componenti e blocchi di contenuto di rilascio. È compatibile con qualsiasi [panoramica dell&#39;architettura](../architecture-options/overview.md), connessione a Commerce Foundation, Storefront Services o [!DNL Adobe Commerce Optimizer] servizi di merchandising a seconda del back-end. Consulta la [panoramica su Adobe Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

## Servizi Storefront

[!DNL Storefront Services] sono servizi orientati alla vetrina utilizzati con [!DNL Adobe Commerce]. Le API del servizio forniscono un accesso ottimizzato a funzionalità quali:

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

Sia [!DNL Adobe Commerce] nel cloud o on-premise (se configurato) che [!DNL Adobe Commerce as a Cloud Service] utilizzano i servizi Storefront. Non sono esclusivi di [!DNL Adobe Commerce as a Cloud Service] e non devono essere utilizzati come etichetta distintiva tra le due opzioni della piattaforma [!DNL Adobe Commerce]. Vedere lo schema di GraphQL di [Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## Vetrine di negozi headless personalizzate

Le opzioni di Storefront oltre a Commerce Storefront con tecnologia [!DNL Edge Delivery Services] includono [!DNL Luma], [!DNL PWA Studio] o una vetrina headless personalizzata, a seconda dei requisiti di implementazione e supporto della piattaforma. Una vetrina headless personalizzata si connette alle stesse famiglie di API di qualsiasi altra opzione di vetrina, Commerce Foundation, Storefront Services o Commerce Optimizer Merchandising Services, in base all&#39;[opzione di architettura](../architecture-options/overview.md) selezionata.

## Integrazione carrello e pagamento

La gestione delle transazioni di carrello e pagamento dipende dal back-end di Commerce, non dalla tecnologia di vetrina:

- Quando [!DNL Adobe Commerce] Commerce Foundation è il backend, la vetrina utilizza le API di Commerce Foundation per le operazioni di carrello, pagamento, cliente e ordine, oltre a integrazioni configurate di pagamento, imposta, spedizione ed evasione.
- Quando una piattaforma di e-commerce di terze parti è il back-end, come nel caso di [!DNL Adobe Commerce Optimizer] autonomo, la vetrina si connette ai servizi relativi a carrello, pagamento, cliente, ordine, pagamento, imposte, spedizione e evasione della piattaforma tramite API Mesh, App Builder o un&#39;integrazione diretta.

## Linee guida correlate

- [Panoramica dell’architettura](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
