---
title: API di Commerce
description: Confronta le famiglie di API di Adobe Commerce, tra cui Commerce Foundation, Storefront Services, Commerce Optimizer Merchandising Services e Data Ingestion.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:36:11.529Z'
TQID: 'https://experienceleague.adobe.com/JBpnpCy9QITdcYtKnL2btd9grmgIk1prYaCNasgWkok'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
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
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%
---

# API

| Famiglia API | Scopo principale | Utilizzato da |
| --- | --- | --- |
| **API GraphQL di Commerce Foundation** | Funzionalità commerciali e transazionali di base come operazioni di catalogo, carrello, pagamento, clienti e ordini | [!DNL Adobe Commerce] nel cloud, [!DNL Adobe Commerce] nei locali e [!DNL Adobe Commerce as a Cloud Service] |
| **API GraphQL di Storefront Services** | Esperienze di catalogo, ricerca e consigli orientate agli store tramite [!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations] | [!DNL Adobe Commerce] nel cloud o in locale con servizi configurati e [!DNL Adobe Commerce as a Cloud Service] |
| **API GraphQL di Commerce Optimizer Merchandising Services** | Recupera i risultati di cataloghi, visualizzazioni di cataloghi, contesti di prezzo, ricerche, consigli e merchandising gestiti da Optimizer | [!DNL Adobe Commerce] nel cloud o in locale con il connettore Optimizer e [!DNL Adobe Commerce Optimizer] autonomo |
| **API REST per l&#39;acquisizione dei dati Commerce Optimizer** | Aggiungere dati di catalogo e prezzo a un&#39;implementazione autonoma di [!DNL Adobe Commerce Optimizer] | [!DNL Adobe Commerce Optimizer] autonomo connesso a un&#39;origine dati esterna |

## API GraphQL di Commerce Foundation

Funzionalità di base di commerce, tra cui catalogo, carrello, pagamento, clienti e ordini. Utilizzato da [!DNL Adobe Commerce] nel cloud, [!DNL Adobe Commerce] nei locali e [!DNL Adobe Commerce as a Cloud Service]. Consulta [API GraphQL di Commerce](https://developer.adobe.com/commerce/webapi/graphql/).

## API GraphQL di Storefront Services

Esperienze di catalogo, ricerca e consigli orientate agli store tramite [!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations]. Utilizzato da [!DNL Adobe Commerce] su Cloud, locale e [!DNL Adobe Commerce as a Cloud Service]. Vedere lo schema di GraphQL di [Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## API GraphQL di Commerce Optimizer Merchandising Services

Recupera i risultati di cataloghi, visualizzazioni di cataloghi, contesti di prezzo, ricerche, consigli e merchandising gestiti da Optimizer. Utilizzato da [!DNL Adobe Commerce] su Cloud, on-premise con [!DNL Adobe Commerce Optimizer Connector] e autonomo [!DNL Adobe Commerce Optimizer]. Consulta [Servizi di merchandising Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/).

## API REST per l’acquisizione dei dati Commerce Optimizer

Aggiungere dati di catalogo e prezzo a un&#39;implementazione autonoma di [!DNL Adobe Commerce Optimizer] da un&#39;origine dati esterna. Consulta [Acquisizione dati Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).

## Integrazioni Commerce Optimizer

[!DNL Adobe Commerce Optimizer] si connette ad altri sistemi attraverso diversi percorsi di integrazione, a seconda che sia abbinato a [!DNL Adobe Commerce] o a un back-end di terze parti.

### Connettore Adobe Commerce Optimizer

Sincronizza i dati di catalogo e prezzo da [!DNL Adobe Commerce] nel cloud o on-premise a [!DNL Adobe Commerce Optimizer], mantenendo [!DNL Adobe Commerce] come sistema di transazioni mentre Optimizer fornisce individuazione e merchandising. Consulta [Integrazioni Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md).

### Integrazioni con soluzioni commerce di terze parti

Acquisisce i dati di catalogo e prezzo da una piattaforma di e-commerce di terze parti, PIM, ERP o un&#39;altra origine in [!DNL Adobe Commerce Optimizer] autonomo tramite l&#39;API REST di acquisizione dati, mentre la piattaforma di terze parti rimane il sistema transazionale di record.

### Mesh API e App Builder

Utilizza API Mesh per orchestrare le API di Adobe Commerce con API private o di terze parti. Utilizza Adobe Developer App Builder per creare applicazioni e integrazioni personalizzate. Per informazioni sull&#39;estensibilità di Commerce correlate, vedere [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) e [Adobe Commerce extensibility](https://developer.adobe.com/commerce/extensibility/).

Per le integrazioni basate su eventi specifiche, vedere [Adobe I/O Events per Adobe Commerce](https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events).


### Carrello e pagamento

Per [!DNL Adobe Commerce Optimizer] autonomi con un backend esterno, la vetrina utilizza le API GraphQL di Merchandising Services per le esperienze dei prodotti, quindi consegna al backend tramite Mesh API, App Builder o integrazione diretta.

### AEM Assets

AEM Assets è un’integrazione opzionale e trasversale per la gestione delle risorse digitali che può essere aggiunta a qualsiasi architettura Commerce o Optimizer anziché a un percorso di integrazione separato. Consulta [Integrazione AEM Assets per Commerce](../aem-assets/aem-assets-integration.md).

## Linee guida correlate

- [Panoramica dell’architettura](../architecture-options/overview.md)
- [Storefront](../storefronts/overview.md)
- [Integrazione di AEM Assets per Commerce](../aem-assets/aem-assets-integration.md)
