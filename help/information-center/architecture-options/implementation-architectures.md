---
title: Opzioni dell'architettura di implementazione
description: Confronta le architetture Adobe Commerce, tra cui Commerce Foundation, Adobe Commerce as a Cloud Service, Optimizer Connector e Standalone Optimizer.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:39:51.406Z'
TQID: 'https://experienceleague.adobe.com/tYkxRAfJWOY7C0OEqYxEb4onwvnnL9wEofEG2e6qnKA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%
---

# Opzioni dell’architettura di implementazione

Le architetture di implementazione di Adobe Commerce combinano tre livelli: un back-end di e-commerce ([!DNL Adobe Commerce] o [!DNL Adobe Commerce Optimizer]), una vetrina e un set di servizi e integrazioni connessi. Confrontare le seguenti opzioni per identificare il sistema proprietario di cataloghi, prezzi, carrello, pagamento, ordini e transazioni cliente in ogni architettura.

## Riepilogo opzioni architettura

Confronta le opzioni in base alla proprietà della transazione e all’esperienza della vetrina.

### Piattaforma Commerce e transazioni

| Opzione | Sistema di registrazione | Percorso transazione | Adatta |
| --- | --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]con Commerce Foundation** | Commerce Foundation gestito da Adobe | Managed Commerce Foundation e servizi Commerce connessi | Clienti che desiderano un Commerce SaaS (Software as a Service) gestito da Adobe con una riduzione della proprietà dell&#39;infrastruttura |
| **[!DNL Adobe Commerce]nel cloud o nei locali con[!DNL Adobe Commerce Optimizer Connector]** | Commerce Foundation esistente, per dati e transazioni Commerce | API di Commerce Foundation e servizi di transazione connessi esistenti | Clienti che desiderano aggiungere funzionalità di rilevamento e merchandising di Optimizer a una distribuzione [!DNL Adobe Commerce] esistente |
| **[!DNL Adobe Commerce Optimizer] autonomo con back-end di e-commerce esterno** | Piattaforma commerciale esistente o di terze parti. I dati di catalogo e prezzo vengono aggiunti a Optimizer da un’origine esterna | API Mesh, App Builder o integrazioni dirette collegano la vetrina a servizi di terze parti quali carrello, pagamento, cliente, ordine, pagamento, imposta, spedizione e adempimento | Clienti che desiderano le funzionalità di Optimizer mantenendo una piattaforma di e-commerce transazionale esistente o di terze parti |
| **[!DNL Adobe Commerce]nel cloud o in locale con Commerce Foundation** | Commerce Foundation | API di Commerce Foundation e integrazioni configurate per pagamenti, imposte, spedizione, inventario e evasione | Clienti che necessitano della piattaforma [!DNL Adobe Commerce] completa con controllo della distribuzione su infrastruttura cloud o locale |

### Esperienza vetrina

Gli storefront si connettono alle API di Commerce Foundation, ai servizi Storefront ([!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations]) o ai servizi di merchandising [!DNL Adobe Commerce Optimizer].

| Opzione | Esperienza vetrina | Percorso dati Storefront |
| --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]con Commerce Foundation** | Commerce Storefront con tecnologia Edge Delivery Services o altra esperienza headless supportata | Servizi Storefront, più API di Commerce Foundation per i dati della piattaforma di base |
| **[!DNL Adobe Commerce]nel cloud o nei locali con[!DNL Adobe Commerce Optimizer Connector]** | Edge Delivery Services o vetrina headless personalizzata con esperienze Optimizer | API GraphQL di Commerce Optimizer Merchandising Services per i dati di catalogo e merchandising gestiti da Optimizer |
| **[!DNL Adobe Commerce Optimizer] autonomo con back-end di e-commerce esterno** | Commerce Storefront con tecnologia Edge Delivery Services o una vetrina headless personalizzata | API GraphQL di Commerce Optimizer Merchandising Services per i dati di catalogo e merchandising |
| **[!DNL Adobe Commerce]nel cloud o in locale con Commerce Foundation** | Edge Delivery Services, Luma, PWA o vetrina headless personalizzata | API di Commerce Foundation e servizi Storefront, se configurati |

## Adobe Commerce as a Cloud Service

![Diagramma dell&#39;architettura di Adobe Commerce as a Cloud Service con Commerce Foundation gestito e i servizi Storefront che alimentano uno store di Commerce](../assets/architecture/commerce-cloud-service-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Limite chiave**: Adobe gestisce la piattaforma Commerce Foundation. L&#39;architettura utilizza i servizi Storefront, inclusi [!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations], per le esperienze storefront. [!DNL Product Visuals] con tecnologia AEM Assets è un&#39;integrazione SaaS opzionale. Consulta [Integrazione AEM Assets per Commerce](../aem-assets/aem-assets-integration.md).

**Riferimenti:**

- [Panoramica di [!DNL Adobe Commerce as a Cloud Service]](/help/cloud-service/overview.md)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [Schema GraphQL dei servizi Storefront](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)

## Adobe Commerce con Commerce Foundation

![Diagramma dell&#39;architettura di Adobe Commerce nel cloud o sul posto con i servizi Storefront e le API Commerce Foundation che alimentano uno store Commerce](../assets/architecture/commerce-paas-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Limite chiave**: Commerce Foundation è proprietaria della piattaforma Commerce e dei flussi di transazioni. [!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations] forniscono l&#39;accesso ottimizzato in vetrina a catalogo, ricerca e consigli, se configurati. L’integrazione di AEM Assets è facoltativa. Consulta [Integrazione AEM Assets per Commerce](../aem-assets/aem-assets-integration.md).

**Riferimenti:**

- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [API GRAPHQL COMMERCE](https://developer.adobe.com/commerce/webapi/graphql/)
- [Schema GraphQL dei servizi Storefront](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)


## Adobe Commerce con il connettore Optimizer

![Diagramma dell&#39;architettura di Adobe Commerce Optimizer Connector che sincronizza i dati di catalogo e prezzo da Adobe Commerce a Adobe Commerce Optimizer, alimentando una vetrina Commerce tramite le API di Merchandising Services](../assets/architecture/adobe-commerce-optimizer-architecture.drawio.png){width="600" zoomable="yes"}

**Limite chiave** - Il connettore sincronizza i dati di catalogo e prezzo da [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer]. [!DNL Adobe Commerce] rimane il sistema di transazioni, mentre Optimizer fornisce esperienze di individuazione e merchandising tramite le API di Merchandising Services.

**Riferimenti:**

- [Integrazioni Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md)
- [Servizi di merchandising Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [API GRAPHQL COMMERCE](https://developer.adobe.com/commerce/webapi/graphql/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Commerce Optimizer indipendente con back-end di terze parti

![Diagramma dell&#39;architettura dei sistemi di origine di proprietà del cliente che invia i dati di catalogo e prezzo tramite l&#39;acquisizione dei dati a un Adobe Commerce Optimizer autonomo, fornendo un Commerce Storefront connesso a un back-end di e-commerce di terze parti](../assets/architecture/adobe-commerce-optimizer-standalone-detailed.drawio.png){width="800" zoomable="yes"}

**Limite chiave**: [!DNL Adobe Commerce Optimizer] è il proprietario autonomo delle esperienze di individuazione catalogo e merchandising, ma non il back-end Commerce transazionale. I dati di catalogo e prezzo vengono inseriti tramite l’API REST di acquisizione dati. La vetrina Edge Delivery Services utilizza le API GraphQL di Merchandising Services per le esperienze dei prodotti e si connette al backend di terze parti per il carrello e il pagamento.

**Riferimenti:**

- [Cos’è Adobe Commerce Optimizer?](/help/optimizer/overview.md)
- [Acquisizione dei dati Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- [Servizi di merchandising Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Riferimento rapido terminologia

| Termine preferito | Significato | Evita di utilizzare come etichetta di architettura corrente |
| --- | --- | --- |
| **Commerce Foundation** | Funzionalità di base di commerce e transazionali | Core Commerce, livello base PHP |
| **Servizi Storefront** | API orientate allo store per Catalog Service, Live Search e Product Recommendations | Etichetta limitata a una sola piattaforma Commerce |
| **Servizi di merchandising Commerce Optimizer** | API di ottimizzazione per l’individuazione dei cataloghi e le esperienze di merchandising | API di Commerce Foundation |
| **Commerce Storefront con tecnologia Edge Delivery Services** | Implementazione della vetrina rivolta al cliente | Una famiglia API |

## Linee guida correlate

- [Architetture di riferimento](reference-architectures.md)
- [Scegli un&#39;opzione Commerce](../portfolio/choose-commerce-option.md)
- [Storefront](../storefronts/overview.md)
- [API](../apis/commerce-apis.md)
