---
title: Supporto per tipi di prodotto personalizzati nell’esportazione di dati del catalogo SaaS
description: Scopri in che modo il modulo di abilitazione del catalogo MCP di Commerce Storefront consente l’esportazione di dati SaaS di rappresentare tipi di prodotti di terze parti personalizzati e non riconosciuti come prodotti semplici nei dati di catalogo inviati a Live Search e Catalog Service.
role: Admin, Developer
hide: true
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
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
source-git-commit: fd87417a494987f33009d386019d870b306dcf73
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%
---
# Supporto per tipi di prodotto personalizzati nell’esportazione di dati di catalogo SaaS

>[!IMPORTANT]
>
>Il supporto per i tipi di prodotto personalizzati è attualmente in **Accesso anticipato** come parte di [!DNL Commerce Storefront MCP]. Questo modulo è supportato in Adobe Commerce versione 2.4.4 e successive. I requisiti di disponibilità, packaging e installazione sono soggetti a modifiche prima della disponibilità generale. Per richiedere un invito a questo **Accesso anticipato**, invia un&#39;e-mail a [commerceeap@adobe.com](mailto:commerceeap@adobe.com). Il team Adobe risponderà con i passaggi successivi e i requisiti di idoneità.

## Panoramica

[!DNL SaaS Data Export] riconosce i tipi di prodotto standard di Adobe Commerce (semplice, configurabile, bundle e così via) quando prepara i dati del catalogo per i servizi Commerce connessi, ad esempio [Live Search](../live-search/overview.md) e [Catalog Service](../catalog-service/overview.md). Le estensioni di terze parti possono introdurre **tipi di prodotto personalizzati** che [!DNL SaaS Data Export] non riconosce in modo nativo.

Il modulo di abilitazione del catalogo MCP di Commerce Storefront consente a [!DNL SaaS Data Export] di rappresentare questi tipi di prodotti personalizzati non riconosciuti come **prodotti semplici** nel payload del catalogo in uscita, in modo che gli acquirenti che utilizzano [!DNL Commerce Storefront MCP] possano individuarli tramite i servizi basati su catalogo.

## Ambito del comportamento

- Il modulo di abilitazione del catalogo MCP di Commerce Storefront non modifica il tipo di prodotto memorizzato in Adobe Commerce. La rappresentazione di un tipo di prodotto personalizzato come prodotto semplice si applica solo ai dati del catalogo inviati a [!DNL Live Search] e [!DNL Catalog Service].
- Non è richiesta alcuna impostazione di amministrazione o configurazione runtime. I tipi di prodotto standard continuano ad esportare normalmente.
- Il modulo è destinato a tipi di prodotto personalizzati introdotti da estensioni di terze parti, non ai tipi di prodotto Commerce standard.

## Installare il modulo

Per abilitare il modulo di abilitazione del catalogo MCP di Commerce Storefront, eseguire quanto segue dalla riga di comando:

```bash
composer require magento/module-storefront-mcp-enablement --no-update
composer update magento/module-storefront-mcp-enablement --with-dependencies
bin/magento setup:upgrade
```

## Risincronizza dati catalogo

L’installazione del modulo non modifica i dati del prodotto sottostante in Adobe Commerce, pertanto gli elementi dei tipi di prodotto personalizzati esistenti non vengono riesportati automaticamente. Per applicare la nuova rappresentazione di prodotto semplice ai dati del catalogo già sincronizzati prima dell’installazione del modulo, risincronizza manualmente i dati del catalogo. Vedi [Risincronizzazione manuale dei dati](data-sync-manage.md#manually-resync-data).
