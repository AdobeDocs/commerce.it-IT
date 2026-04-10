---
title: Note sulla versione
description: Informazioni aggiornate sulla versione per  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
source-git-commit: d0967674d05018f13dc6c8a562005d65d44e42ab
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# Note sulla versione

Le seguenti note sulla versione contengono aggiornamenti a [!DNL Adobe Commerce Optimizer].

## Aprile 2026

**Data di rilascio**: 7 aprile 2026

>[!BEGINSHADEBOX]

### Regole del catalogo

Le regole di merchandising ora includono [regole di categoria](./merchandising/rules/add.md), quindi puoi eseguire il targeting di una o più categorie e controllare l&#39;ordine dei prodotti sulle pagine delle categorie utilizzando la stessa classificazione intelligente e le stesse azioni manuali (pin, boost, bury) di quelle per la ricerca.

### Filtro prezzi

I filtri per consigli ora supportano un [filtro prezzo](./merchandising/recommendations/filters.md#price) che è possibile utilizzare per impostare un intervallo di prezzo minimo e massimo per i prodotti.

### Note aggiuntive sulla versione

[!DNL Adobe Commerce Optimizer] funziona con le ultime versioni dell&#39;integrazione AEM Assets, il connettore Commerce Optimizer e [!DNL Adobe Commerce Storefront]. Utilizza i seguenti collegamenti per visualizzare le note sulla versione per ogni area:

| Estensibilità | Vetrina |
| --- | --- |
| [Integrazione AEM Assets](../aem-assets-integration/release-notes.md)<br>[Connettore Commerce Optimizer](../aco-connector/release-notes.md) | [Informazioni sulla versione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=it)<br>[Storefront changelog](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=it) |

>[!ENDSHADEBOX]

## Febbraio 2026

**Data di rilascio**: 19 febbraio 2026

>[!BEGINSHADEBOX]

È stata aggiunta la possibilità di specificare una visualizzazione del catalogo quando [crei unità di consigli](./merchandising/recommendations/create.md) o [regole di merchandising](./merchandising/rules/add.md).

### Note aggiuntive sulla versione

[!DNL Adobe Commerce Optimizer] funziona con le ultime versioni dell&#39;integrazione AEM Assets, il connettore Commerce Optimizer e [!DNL Adobe Commerce Storefront]. Utilizza i seguenti collegamenti per visualizzare le note sulla versione per ogni area:

| Estensibilità | Vetrina |
| --- | --- |
| [Integrazione AEM Assets](../aem-assets-integration/release-notes.md)<br>[Connettore Commerce Optimizer](../aco-connector/release-notes.md) | [Informazioni sulla versione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=it)<br>[Storefront changelog](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=it) |

>[!ENDSHADEBOX]

## Dicembre 2025

**Data di rilascio**: 10 dicembre 2025

>[!BEGINSHADEBOX]

### Opportunità

I consigli per l&#39;ottimizzazione del sito basati sull&#39;intelligenza artificiale sono ora disponibili tramite l&#39;[integrazione Adobe Sites Optimizer](./manage-results/opportunities.md). Questa funzione consente ai commercianti di identificare e risolvere i problemi che influiscono sulle prestazioni del sito commerce tramite rilevamento automatico e consigli intelligenti.

### Livelli del catalogo

Sono stati aggiunti [livelli catalogo](./setup/catalog-layer.md) per consentire la modifica dei dati di prodotto senza modificare i dati di origine, incluse la gestione della priorità dei livelli e l&#39;integrazione con le funzioni di correzione automatica di Adobe Sites Optimizer.

### Note aggiuntive sulla versione

[!DNL Adobe Commerce Optimizer] funziona con le ultime versioni dell&#39;integrazione AEM Assets, il connettore Commerce Optimizer e [!DNL Adobe Commerce Storefront]. Utilizza i seguenti collegamenti per visualizzare le note sulla versione per ogni area:

| Estensibilità | Vetrina |
| --- | --- |
| [Integrazione AEM Assets](../aem-assets-integration/release-notes.md)<br>[Connettore Commerce Optimizer](../aco-connector/release-notes.md) | [Informazioni sulla versione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=it)<br>[Storefront changelog](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=it) |

>[!ENDSHADEBOX]

## Ottobre 2025

**Data di rilascio**: 14 ottobre 2025

>[!BEGINSHADEBOX]

### Connettore Commerce Salesforce Commerce Optimizer

[!DNL Commerce Optimizer Salesforce Commerce Connector] è un nuovo kit di avvio per l&#39;integrazione di App Builder che consente agli amministratori e agli sviluppatori di Commerce di collegare facilmente i dati del catalogo Salesforce B2C Commerce con [!DNL Commerce Optimizer].<!--COMOPT-536-->

**Per gli amministratori:**

* Gli aggiornamenti del catalogo in Salesforce (prodotti, prezzi, metadati, listini prezzi) vengono sincronizzati automaticamente con Commerce Optimizer, senza richiedere alcun intervento manuale.
* L’integrazione opera in modo indipendente da Adobe Commerce, riducendo la complessità e i potenziali punti di errore.
* Gli amministratori possono fare affidamento sugli aggiornamenti pianificati regolarmente per garantire dati di catalogo accurati in Commerce Optimizer, migliorando il merchandising e i consigli sui prodotti.

**Per sviluppatori:**

* Il kit di avvio fornisce un framework semplificato ed estensibile per l’acquisizione dei dati del catalogo Salesforce in SaaS Merchandising Services.
* Sono disponibili implementazioni di riferimento, documentazione di progettazione ed esempi di codice per accelerare le integrazioni personalizzate o la risoluzione dei problemi.<!--COMOPT-536-->

### Ricerca con livelli

* Versione GA per le seguenti funzionalità di ricerca avanzate: ricerca a livelli con `startsWith` e `contains`. [Ulteriori informazioni](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### API per categorie

È ora disponibile una nuova API REST per le categorie, che consente agli amministratori e agli sviluppatori di creare, aggiornare e gestire in modo programmatico più strutture di categoria per la navigazione e il raggruppamento dei prodotti. L’API supporta configurazioni globali e specifiche per canale ed è progettata per un’elevata scalabilità, supporta fino a 10.000 alberi di categorie e 500 categorie per albero. Per informazioni dettagliate, vedere [Categorie](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#categories) nella _Guida per gli sviluppatori di servizi di merchandising_.<!--DCAT-2649-->

### Note aggiuntive sulla versione

[!DNL Adobe Commerce Optimizer] funziona con le ultime versioni dell&#39;integrazione AEM Assets, il connettore Commerce Optimizer e [!DNL Adobe Commerce Storefront]. Utilizza i seguenti collegamenti per visualizzare le note sulla versione per ogni area:

| Estensibilità | Vetrina |
| --- | --- |
| [Integrazione AEM Assets](../aem-assets-integration/release-notes.md)<br>[Connettore Commerce Optimizer](../aco-connector/release-notes.md) | [Informazioni sulla versione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=it)<br>[Storefront changelog](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=it) |

>[!ENDSHADEBOX]

## Agosto 2025

**Data di rilascio**: 28 agosto 2025

>[!BEGINSHADEBOX]

### Area geografica UE ora disponibile

È ora disponibile il supporto per le organizzazioni IMS dei clienti nella regione dell’Unione europea (eu1). È ora possibile selezionare **Unione europea** come **Area geografica** quando [aggiungi un&#39;istanza di Commerce Optimizer](./get-started.md#step-1-create-an-instance) in Cloud Manager. L&#39;area dell&#39;Unione Europea è disponibile solo per gli ambienti di produzione.

Gli URL di produzione di base per la regione dell’Unione Europea sono:

* Amministratore: `https://eu1.admin.commerce.adobe.com`
* REST e GraphQL: `https://eu1.api.commerce.adobe.com`

![crea istanza](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

### Note aggiuntive sulla versione

[!DNL Adobe Commerce Optimizer] funziona con le ultime versioni dell&#39;integrazione AEM Assets, il connettore Commerce Optimizer e [!DNL Adobe Commerce Storefront]. Utilizza i seguenti collegamenti per visualizzare le note sulla versione per ogni area:

| Estensibilità | Vetrina |
| --- | --- |
| [Integrazione AEM Assets](../aem-assets-integration/release-notes.md)<br>[Connettore Commerce Optimizer](../aco-connector/release-notes.md) | [Informazioni sulla versione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=it)<br>[Storefront changelog](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=it) |

>[!ENDSHADEBOX]
