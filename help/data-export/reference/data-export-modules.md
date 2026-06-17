---
title: Moduli esportazione dati SaaS
description: Scopri i pacchetti del modulo Magento inclusi in [!DNL SaaS Data Export] e i relativi ruoli in raccolta dati, trasformazione e invio ai servizi SaaS di Adobe.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 0%

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
