---
title: Migrazione e adozione
description: Scopri i percorsi per l’adozione di Adobe Commerce Optimizer, la modernizzazione di una vetrina esistente o la migrazione completa ad Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/2iEJ6fA-wLr18bi9C8l-w3srx1AWlAtiGt1cG9RPv0Q'
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
  - id: 1783ae9f-7157-5aeb-a915-91e260301e46
    internal-label: Routes
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%
---

# Migrazione e adozione

Non è necessario che l’adozione avvenga tramite un’unica modifica della piattaforma all-at-once. Seleziona un percorso a seconda che l’obiettivo immediato sia la modernizzazione della vetrina, il miglioramento del merchandising, la modernizzazione del back-end o il passaggio completo al software gestito come servizio (SaaS).

## Percorsi di adozione

### Modernizzare l’implementazione Adobe Commerce esistente

- Mantieni Commerce Foundation esistente come back-end transazionale.
- Adottare Commerce Storefront con tecnologia [!DNL Edge Delivery Services].
- Utilizza i servizi Storefront, App Builder, API Mesh e un’integrazione AEM Assets opzionale.

### Utilizzare Commerce Optimizer come bridge

- Connetti [!DNL Adobe Commerce] cloud o locale utilizzando [!DNL Adobe Commerce Optimizer Connector].
- Adottare servizi di merchandising, individuazione, consigli e una vetrina Edge Delivery Services.
- Mantieni [!DNL Adobe Commerce] come sistema di registrazione principale per prodotti, prezzi, struttura del catalogo, carrello, pagamento, clienti e ordini.
- Utilizza questa architettura come possibile transizione verso [!DNL Adobe Commerce as a Cloud Service].

### Migrazione completa ad Adobe Commerce as a Cloud Service

- Valuta l’applicazione corrente, le personalizzazioni, le integrazioni, la vetrina e i dati.
- Modernizzare le personalizzazioni utilizzando modelli di estensibilità compatibili con SaaS.
- Rigenera o adatta la vetrina e le integrazioni.
- Migra e convalida catalogo, clienti, ordini, configurazione e dati personalizzati supportati.
- Test, suddivisione e funzionamento del nuovo ambiente SaaS.

### Adottare Adobe Commerce Optimizer autonomo

- Acquisire dati su catalogo e prezzi da una piattaforma Commerce di terze parti, da PIM, ERP o da un&#39;altra origine.
- Utilizza i servizi di merchandising [!DNL Adobe Commerce Optimizer] per il recupero, l&#39;individuazione, i consigli e il merchandising dei cataloghi.
- Utilizza Commerce Storefront con tecnologia [!DNL Edge Delivery Services].
- Conserva carrello, pagamento, clienti, ordini, pagamenti, imposte, spedizione ed evasione nei sistemi di terze parti collegati.

## Sequenza consigliata

1. Valutare lo stato corrente e definire la proprietà del sistema.
1. Stabilisci i limiti dell’integrazione API-first.
1. Modernizza la vetrina e il livello esperienza.
1. Adottare in parallelo i servizi di merchandising e AEM Assets.
1. Esegui la migrazione di Commerce Foundation quando necessario.
1. Convalida, taglia, monitora e ottimizza.

## Linee guida correlate

- [Scegli un&#39;opzione Commerce](../portfolio/choose-commerce-option.md)
- [Opzioni dell&#39;architettura](../architecture-options/overview.md)
- [Modernizzare una vetrina esistente](../implementation-guides/modernize-storefront.md)
- [Abilita Adobe Commerce Optimizer](../implementation-guides/enable-aco.md)
