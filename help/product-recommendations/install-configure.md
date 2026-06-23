---
title: Installazione e configurazione
description: Scopri come installare, aggiornare e disinstallare [!DNL Product Recommendations].
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
TQID: https://experienceleague.adobe.com/z-ue-sojw9Iewuz-ZToCzkumP3qN-TCWWF3UWdpdIL0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10a91a91337778648e99078bcbf0c9ef25a49f86
workflow-type: tm+mt
source-wordcount: 578
ht-degree: 0%

---

# Installazione e configurazione

La distribuzione di [!DNL Product Recommendations] nella vetrina e nell&#39;amministratore richiede l&#39;installazione del modulo e la configurazione di [Commerce Services Connector](../landing/saas.md). Man mano che gli aggiornamenti vengono rilasciati, è possibile aggiornare facilmente l’installazione con la versione più recente.

- [Installa](#install)
- [Configura](#configure)
- [Aggiorna](#update)
- [Disinstalla](#uninstall)

## Installa [!DNL Product Recommendations] {#install}

Poiché il modulo [!DNL Product Recommendations] è un metapacchetto autonomo, gli aggiornamenti vengono rilasciati più frequentemente rispetto ad Adobe Commerce. Per essere certi di essere aggiornati sulle ultime correzioni di bug e funzionalità, consulta le [note sulla versione](release-notes.md).

>[!IMPORTANT]
>
>Assicurati di disporre dei [diritti](../landing/saas.md#credentials) corretti per utilizzare i consigli sui prodotti.

Installa il modulo `magento/product-recommendations` con Composer:

```bash
composer require magento/product-recommendations
```

### Supporto per Aggiungi Page Builder {#pbsupport}

[!DNL Product Recommendations] per Page Builder è un modulo facoltativo e viene installato separatamente. Per utilizzare [!DNL Product Recommendations] con Page Builder, installare il modulo eseguendo il comando seguente:

```bash
composer require magento/module-page-builder-product-recommendations
```

Attivando [!DNL Product Recommendations] in Page Builder, è possibile aggiungere una [unità di consigli](https://experienceleague.adobe.com/it/docs/commerce-admin/page-builder/add-content/recommendations) attiva a qualsiasi contenuto creato in Page Builder, ad esempio pagine, blocchi e blocchi dinamici.

Per ulteriori istruzioni, vedi [Utilizzo di [!DNL Product Recommendations] con contenuto Page Builder](page-builder.md).

### Aggiungi tipo di consiglio per somiglianza visiva {#vissimsupport}

Il tipo di consiglio _Somiglianza visiva_ ti consente di distribuire un&#39;unità di consigli nella pagina dei dettagli del prodotto che mostra prodotti [visivamente simili](type.md#visualsim) al prodotto visualizzato. Questo tipo di consigli è più utile quando le immagini e gli aspetti visivi dei prodotti sono parti importanti dell’esperienza di acquisto. Installa il tipo di consiglio _Somiglianza visiva_ eseguendo il comando seguente:

```bash
composer require magento/module-visual-product-recommendations
```

## Configura [!DNL Product Recommendations] {#configure}

1. Dopo aver installato il modulo `magento/product-recommendations`, configurare [Commerce Services Connector](../landing/saas.md) specificando le chiavi API e selezionando uno spazio dati SaaS.

   La configurazione di questa connessione consente la sincronizzazione dei dati e la comunicazione tra l’istanza di Commerce, Catalog Service e altri servizi di supporto. La sincronizzazione dei dati è gestita dall&#39;estensione [SaaS Data Export](../data-export/overview.md).

1. Per garantire la corretta esecuzione dell&#39;esportazione del catalogo, verificare che i processi [cron](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) e [indexers](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/manage-indexers) siano in esecuzione e che l&#39;indicizzatore `Product Feed` sia impostato su `Update by Schedule`.

Dopo aver collegato correttamente l&#39;applicazione Commerce a Commerce Services e aver specificato [Spazio dati SaaS](../landing/saas.md#saas-configuration), la sincronizzazione del catalogo inizia. Puoi quindi [verificare](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) che i dati comportamentali vengano inviati alla vetrina.

## Monitoraggio e risoluzione dei problemi di sincronizzazione dei dati

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

{{install-data-sync-feed-status}}

## Aggiorna l&#39;installazione di [!DNL Product Recommendations] {#update}

Come tutti gli altri componenti di Adobe Commerce, [!DNL Product Recommendations] utilizza Composer per l&#39;installazione e gli aggiornamenti. Per aggiornare il modulo `magento/product-recommendations`, eseguire le operazioni seguenti:

```bash
composer update magento/product-recommendations --with-dependencies
```

Per eseguire l&#39;aggiornamento a una versione principale, ad esempio da 5.0 a 6.0, è necessario modificare il file radice `composer.json` del progetto. Per informazioni sull&#39;ultima versione, vedere le [note sulla versione](release-notes.md). Ad esempio, apriamo il file `composer.json` principale e cerchiamo il modulo `magento/product-recommendations`:

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

Saltiamo la versione principale da `5.0` a `6.0`:

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

Salva il file `composer.json` ed esegui:

```bash
composer update magento/product-recommendations --with-dependencies
```

Oppure se hai installato i moduli `magento/module-visual-product-recommendations` e `magento/module-page-builder-product-recommendations`:

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> Nelle versioni 3.x.x di Product Recommendations, era necessaria una sola chiave API. Nelle versioni 4.x.x e successive devi fornire chiavi API pubbliche e private sia per l’ambiente sandbox che per quello di produzione. Se non fornisci entrambe le coppie di chiavi API, non puoi accedere alla funzione Consigli di prodotto in Amministrazione. Tuttavia, la raccolta dei dati continua nella vetrina e i consigli esistenti continuano a essere visualizzati agli acquirenti.

## Firewall

Per consentire ai consigli di prodotto di passare attraverso un firewall, aggiungi `commerce.adobe.io` all&#39;elenco consentiti.

## Disinstalla [!DNL Product Recommendations] {#uninstall}

Se necessario, puoi [disinstallare](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) il modulo product-recommendations.
