---
title: Panoramica dell’architettura di Commerce
description: Scopri il modello di prodotto Adobe Commerce e dove trovare opzioni di architettura dettagliate, vetrina e linee guida API.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T10:11:03.706Z'
TQID: 'https://experienceleague.adobe.com/V9Zp0eS8b45xYEay4EK91tPVnKhRdkWGDj4Vv7hB79U'
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
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%
---

# Panoramica dell’architettura di Commerce

Le architetture Adobe Commerce in genere combinano tre livelli: un back-end di e-commerce ([!DNL Adobe Commerce] o [!DNL Adobe Commerce Optimizer]), una vetrina e un set di servizi e integrazioni connessi. In questa sezione viene illustrato il modello di prodotto e vengono illustrati dettagliatamente confronti, diagrammi e riferimenti API contenuti in ogni pagina dedicata.

## Introduzione

| Sezione | Utilizzala per |
| ------- | --------- |
| [Piattaforme e servizi](../portfolio/platform-and-services.md) | Comprendi cosa sono i singoli prodotti Commerce: Adobe Commerce, Commerce Foundation, Adobe Commerce Optimizer e Adobe Commerce as a Cloud Service. |
| [Scegliere un&#39;opzione di Commerce](../portfolio/choose-commerce-option.md) | Confronta le opzioni di Commerce in base alla proprietà della transazione, al modello di distribuzione e alle esigenze di merchandising. |
| [Opzioni architettura](../architecture-options/implementation-architectures.md) | Confrontare in dettaglio le quattro architetture supportate, inclusi i diagrammi di sistema e i collegamenti di riferimento. |
| [Storefronts](../storefronts/overview.md) | Comprendi le opzioni della vetrina e come si connettono a ciascuna architettura. |
| [API](../apis/commerce-apis.md) | Confronta le famiglie di API utilizzate in Commerce Foundation, Storefront Services e Commerce Optimizer. |
| Integrazione di [AEM Assets per Commerce](../aem-assets/aem-assets-integration.md) | Aggiungi la gestione centralizzata delle risorse digitali a qualsiasi architettura Commerce o Optimizer. |
| [Migrazione e adozione](../migration-adoption/overview.md) | Pianifica un passaggio tra architetture diverse o un&#39;adozione graduale di Adobe Commerce Optimizer. |

## Riferimento rapido terminologia

| Termine preferito | Significato | Evita di utilizzare come etichetta di architettura corrente |
| --- | --- | --- |
| **Commerce Foundation** | Funzionalità di base di commerce e transazionali | Livello base Commerce core e PHP |
| **Servizi Storefront** | API orientate allo store per Catalog Service, Live Search e Product Recommendations | Etichetta limitata a una sola piattaforma Commerce |
| **Servizi di merchandising Commerce Optimizer** | API di ottimizzazione per l’individuazione dei cataloghi e le esperienze di merchandising | API di Commerce Foundation |
| **Commerce Storefront con tecnologia Edge Delivery Services** | Implementazione della vetrina rivolta al cliente | Una famiglia API |

## Linee guida correlate

- [Architetture di implementazione](implementation-architectures.md)
- [Architetture di riferimento](reference-architectures.md)
- [Crea una nuova vetrina](../implementation-guides/build-new-storefront.md)
