---
title: Moduli esportazione dati SaaS
description: Scopri i pacchetti del modulo Magento inclusi in [!DNL SaaS Data Export] e i relativi ruoli nella raccolta dati, nella trasformazione e nell’invio ai servizi SaaS di Adobe.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 8%
---

# Moduli esportazione dati SaaS

[!DNL SaaS Data Export] è costituito da due gruppi di moduli: il primo per la raccolta e l&#39;indicizzazione dei dati e il secondo per il trasporto e l&#39;invio HTTP.

Questi moduli gestiscono il rilevamento delle modifiche delle entità, l’indicizzazione dei feed, l’estrazione dei dati e la definizione dello schema.
La tabella seguente fornisce solo moduli a livello di framework; l’elenco completo dei moduli disponibili dipende dai pacchetti installati.

| Modulo | Finalità | Classi chiave |
| --- | --- |--- |
| `DataExporter` | Framework di base: indicizzatore, tabella dei feed, hash, nuovo tentativo, blocco | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager` |
| `QueryXml` | Query DSL basata su XML per la raccolta dati | `QueryFactory`, `QueryProcessor`, `SelectBuilder` |
| `SaaSCommon` | Trasporto HTTP condiviso, nuovo tentativo, CLI (`saas:resync`), orchestrazione di risincronizzazione | `ExportFeed`, `SubmitFeed`, `ResyncManager`, `ResyncManagerPool`, `ProgressBarManager` |

Per informazioni sull&#39;interazione di questi moduli durante la sincronizzazione, vedere [Pipeline di esportazione dati SaaS](../sync-overview.md).

>[!MORELIKETHIS]
>
>- [Funzionamento della sincronizzazione](../sync-overview.md)
>- [Schema tabella feed](feed-table-reference.md)
>- [Gestire l&#39;estensione per l&#39;esportazione dei dati SaaS](../manage-extension.md)
