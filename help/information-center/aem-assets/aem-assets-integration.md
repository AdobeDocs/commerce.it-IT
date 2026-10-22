---
title: Integrazione di AEM Assets per Commerce
description: Scopri come integrare AEM Assets con Adobe Commerce, Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer per gestire centralmente immagini e contenuti multimediali dei prodotti.
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:34:13.564Z'
TQID: 'https://experienceleague.adobe.com/v15DE37DoqpstrsWqnwd6DYpa5moT-BhQ80zDq2KP6I'
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
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%
---

# Integrazione di AEM Assets per Commerce

L’integrazione di AEM Assets abilita le funzionalità di visualizzazione dei prodotti in Adobe Commerce, in modo da poter gestire centralmente immagini di prodotti, video e altri supporti in AEM Assets. Si tratta di un componente aggiuntivo opzionale che funziona con qualsiasi opzione dell’architettura Commerce, non con una piattaforma Commerce separata.

## Percorsi di integrazione per architettura

Esistono due percorsi di integrazione. Il percorso dipende dall’architettura di Commerce.

| Architettura Commerce | Percorso di integrazione AEM Assets | Ulteriori informazioni |
| --- | --- | --- |
| [!DNL Adobe Commerce] su Cloud o locale | Integrazione di [!DNL AEM Assets] per Commerce. Utilizza il pacchetto di integrazione di Commerce per sincronizzare e gestire immagini di prodotti, video e altri supporti tra [!DNL Adobe Commerce] e [!DNL AEM Assets]. | Integrazione di [AEM Assets per Commerce](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | [!DNL Product Visuals] con tecnologia [!DNL AEM Assets] | [Configurazione integrazione AEM Assets](/help/aem-assets-integration/overview.md#next-steps) |
| [!DNL Adobe Commerce Optimizer] autonomo | [!DNL Product Visuals] con tecnologia [!DNL AEM Assets]. I dati del catalogo di base e del prezzo arrivano tramite l&#39;API [Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/). | [Visualizzazioni prodotto con AEM Assets](/help/optimizer/setup/product-visuals.md) |
| [!DNL Adobe Commerce] con [!DNL Adobe Commerce Optimizer Connector] | [!DNL Product Visuals] con tecnologia [!DNL AEM Assets]. I dati di catalogo e prezzo sono sincronizzati da [!DNL Adobe Commerce] dal connettore. | [Integrazioni Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals] è il percorso di integrazione per Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer. Sincronizza le immagini dei prodotti gestiti da AEM con il livello di catalogo Commerce e le distribuisce alle esperienze vetrina tramite API storefront.

## Prima di scegliere

- I requisiti di configurazione e licenze sono diversi tra il percorso Commerce sul cloud o locale e il percorso Commerce as a Cloud Service o Adobe Optimizer [!DNL Product Visuals]. Rivedi prima i requisiti specifici della distribuzione.
- [!DNL AEM Assets] gestisce le risorse digitali. Non sostituisce il catalogo Commerce, i prezzi, il carrello, il pagamento o il sistema di ordini.
- Le risorse di prodotto vengono associate ai prodotti Commerce utilizzando SKU (Stock Keeping Unit) o altri metadati corrispondenti documentati.
- Se i team di marketing e merchandising necessitano di immagini di prodotto centralizzate e flussi di lavoro delle risorse, scegli il percorso che corrisponde alla tua architettura Commerce.

## Informazioni correlate

- [Documentazione di Adobe Experience Manager Assets](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/overview)
- [Panoramica dell’architettura](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
