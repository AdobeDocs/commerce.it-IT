---
title: Installazione e configurazione
description: Scopri come installare, aggiornare e disinstallare [!DNL Product Recommendations].
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Installazione e configurazione

La distribuzione [!DNL Product Recommendations] nel tuo negozio e nell&#39;amministratore richiede l&#39;installazione del modulo e la configurazione del [connettore](../landing/saas.md) di Commerce Services. Man mano che vengono rilasciati gli aggiornamenti, è possibile aggiornare facilmente l&#39;installazione con la versione più recente.

- [Installare](#install)
- [Configura](#configure)
- [Aggiorna](#update)
- [Disinstallazione](#uninstall)

## Installare [!DNL Product Recommendations] {#install}

Poiché il [!DNL Product Recommendations] modulo è un metapacchetto autonomo, gli aggiornamenti vengono rilasciati più frequentemente rispetto a Adobe Systems Commerce. Per essere sicuri di essere aggiornati con le correzioni di bug e le funzionalità più recenti, fare riferimento alla [note sulla versione](release-notes.md).

>[!IMPORTANT]
>
>Assicurati di[&#128279;](../landing/saas.md#credentials) disporre delle adesioni corrette per utilizzare Product Raccomandazioni.

Installare il `magento/product-recommendations` modulo con Composer:

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

1. Per garantire che l&#39;esportazione del catalogo possa essere eseguita correttamente, verificate che i [cron](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) job e gli [indicizzatori](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/manage-indexers) siano in esecuzione e che l&#39;indicizzatore `Product Feed` sia impostato su `Update by Schedule`.

Dopo aver correttamente collegare Commerce applicazione a Commerce Services e specificato lo [spazio](../landing/saas.md#saas-configuration) dati SaaS, inizia il Sincronizzazione catalogo. Puoi quindi [verificare](verify.md) che i dati comportamentali vengano inviati al tuo negozio.

## Monitoraggio e risoluzione dei problemi di sincronizzazione dei dati

Dall&#39;amministratore Commerce, è possibile monitorare il processo di sincronizzazione utilizzando il dashboard[&#128279;](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-dashboard) di [gestione dei dati. Utilizza l&#39;interfaccia della riga](../data-export/data-export-cli-commands.md#troubleshooting) di comando e i registri di Commerce per gestire e risolvere i problemi del processo.

Puoi quindi [verificare](verify.md) che i dati comportamentali vengano inviati al tuo negozio.

## Aggiorna la tua [!DNL Product Recommendations] installazione {#update}

Come tutto Adobe Systems Commerce, [!DNL Product Recommendations] utilizza Composer per l&#39;installazione e gli aggiornamenti. Per aggiornare il `magento/product-recommendations` modulo, esegui quanto segue:

```bash
composer update magento/product-recommendations --with-dependencies
```

Per eseguire l&#39;aggiornamento a una versione principale, ad esempio dalla 5.0 alla 6.0, è necessario modificare il file radice `composer.json` del progetto. Per informazioni sulla versione più recente, vedere la [note sulla versione](release-notes.md) . Ad esempio, apriamo il file principale `composer.json` e ricerca per il `magento/product-recommendations` modulo:

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

Sbattiamo la versione principale da `5.0` a `6.0`:

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

## Disinstallazione [!DNL Product Recommendations] {#uninstall}

Se necessario, è possibile [disinstallare](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) il modulo product-recommendations.
