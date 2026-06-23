---
title: '[!DNL Adobe Commerce Optimizer Connector] moduli ed endpoint di feed'
description: Scopri  [!DNL Adobe Commerce Optimizer Connector]  moduli, endpoint API per feed catalogo, limiti batch e percorsi di configurazione core_config_data per  [!DNL Adobe Commerce].
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T15:48:19.494Z'
TQID: 'https://experienceleague.adobe.com/UM6Y-xoQpUDzWpaMe1GRPp4XoAtHBLBsHw388kumN8g'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 301
ht-degree: 1%

---

# Moduli di connettore ed endpoint di feed per il connettore Adobe Commerce Optimizer

Questo riferimento elenca i pacchetti del modulo [!DNL Adobe Commerce Optimizer Connector], gli endpoint API di feed supportati e i percorsi chiave di configurazione archiviati in `core_config_data`. Per informazioni sull&#39;interazione di questi componenti durante la sincronizzazione, vedere [Pipeline di sincronizzazione del connettore](../connector-sync-pipeline.md).

## Moduli

Il connettore include più moduli Magento che raccolgono dati di catalogo, mappano i dati di feed nel formato supportato dall&#39;API [!DNL Commerce Optimizer] e gestiscono l&#39;invio e il controllo dell&#39;ambito. La tabella seguente riepiloga ogni modulo e il relativo ruolo.

| Modulo | Ruolo |
| ------ | ---- |
| `DataExporterAdapter` | Mappa i feed [!DNL Adobe Commerce] al formato richiesto dall&#39;API [!DNL Adobe Commerce Optimizer]. Sostituisce la configurazione del pool di feed e dello schema. |
| `SaasExportAdapter` | Instrada i feed [!DNL Commerce Optimizer] all&#39;API di acquisizione e blocca l&#39;invio di feed non supportati. |
| `CommerceAcoExporter` | Gestisce le credenziali [!DNL Commerce Optimizer] e fornisce i comandi di installazione CLI |
| `CommerceAdapter` | Livello di compatibilità API [!DNL Commerce Optimizer] (GraphQL, componente aggiuntivo bundle per il carrello, interfaccia utente di configurazione) |
| `PriceBookDataExporter` | Feed del listino prezzi indicizzato per sito Web e gruppo di clienti |
| `SaasPriceBook` | Infrastruttura SaaS per la presentazione del listino prezzi dedicato |
| `CommerceOptimizerScopeMapper` | Abilitazione della sincronizzazione per sito web e per visualizzazione store |

## Feed supportati

Il connettore invia più tipi di feed a [!DNL Commerce Optimizer] [[!DNL Catalog Data Ingestion API]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}. Nella tabella seguente sono elencati tutti i feed con il relativo endpoint, limite batch, nome indicizzatore e tabella feed in [!DNL Adobe Commerce].

| Feed | Endpoint API [!DNL Commerce Optimizer] | Limite batch | Nome indice AC | Tabella feed |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

I feed `products`, `productAttributes`, `categories` e `prices` riutilizzano i dati raccolti dagli indicizzatori [!DNL SaaS Data Export]. Il connettore genera il feed `priceBooks` dalla configurazione del sito Web e del gruppo di clienti e non si basa su un indicizzatore [!DNL SaaS Data Export].

Per i dettagli di mappatura a livello di campo per ciascun feed, vedi [Mappatura campo per [!DNL Commerce Optimizer Connector] feed](field-mapping.md).
Per stimare la durata di una sincronizzazione in base alle dimensioni del catalogo, vedere [Stima del volume dei dati e del tempo di sincronizzazione](estimate-data-volume-sync-time.md).

## Percorsi di configurazione

Le credenziali di [!DNL Commerce Optimizer Connector] e gli URL del servizio sono archiviati in `core_config_data` nel prefisso del percorso `aco_exporter/general/`. Eseguire `bin/magento aco:config:show` per rivedere i valori correnti. Il comando non visualizza il segreto client.

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
