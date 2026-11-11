---
title: Modelli di dati di catalogo componibili e servizi di merchandising
description: Scopri in che modo il modello dati del catalogo componibile cambia la consegna del catalogo in [!DNL Adobe Commerce as a Cloud Service] e cosa devono sapere i commercianti e i team di vetrina.
feature: Catalog Management, Personalization, Saas
role: Leader
level: Beginner
autotag-review: '2026-11-09T05:07:21.124Z'
TQID: 'https://experienceleague.adobe.com/5Aaumfx9-lOBMDOg59rr-MMl-0sgFLSVUzngkdzfyR0'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: 0bda134570bb3bf2f43da545917dedc95394df5e
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%
---

# Servizi di merchandising

Adobe Commerce as a Cloud Service ora supporta il modello dati di catalogo componibile (CCDM) tramite Merchandising Services. Adobe Commerce Optimizer ha introdotto questo modello dati e il CCDM fornisce a entrambi i prodotti una base comune per fornire funzionalità di navigazione e merchandising dei cataloghi in vetrina, mentre Commerce Foundation continua a gestire prodotti, prezzi e transazioni.

In questo argomento vengono illustrate le modifiche apportate al modello CCDM, le funzionalità che continuano e le conseguenze per commercianti, partner e sviluppatori di vetrine.

## Quali modifiche introduce il CCDM?

Il modello di catalogo originale utilizza Catalog Service per fornire i dati dei prodotti agli store, con le funzionalità di ricerca, merchandising e consigli di Live Search e Product Recommendations. In questo modello, Commerce esegue la sincronizzazione utilizzando [Esportazione dati SaaS](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview).

Con CCDM, queste funzionalità funzionano sulla stessa base di catalogo che alimenta Adobe Commerce Optimizer. [Visualizzazioni catalogo](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/setup/catalog-view) e [Criteri](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/setup/policies) definiscono il contesto del catalogo disponibile per una vetrina. I criteri determinano l’assortimento di prodotti e le regole di merchandising possono essere applicate a tutte le visualizzazioni di catalogo o essere personalizzate per una visualizzazione specifica.

Questo cambia la modalità di configurazione, accesso e merchandised del catalogo. CCDM si basa sulle funzionalità di ricerca, consigli e merchandising del catalogo Commerce originale e introduce controlli a livello di visualizzazione del catalogo. Di seguito sono descritte ulteriori funzionalità di gestione e reporting.

Commerce Foundation rimane la fonte canonica per prodotti e prezzi. I dati relativi a prodotti e prezzi si sincronizzano in un solo modo con il CCDM attraverso un’integrazione nativa di Adobe Commerce as a Cloud Service. La configurazione della visualizzazione del sito web, dello store e dello store rimane in Commerce, insieme ai flussi di lavoro esistenti per carrello, pagamento e gestione degli ordini.

## Licenze e provisioning

I servizi di merchandising sono inclusi nello SKU Adobe Commerce as a Cloud Service esistente. Non si tratta di un secondo prodotto o abbonamento e non richiede un acquisto Adobe Commerce Optimizer separato, adesione o tenant.

## Panoramica dell’architettura

[!DNL Commerce Foundation] rimane il record principale per prodotti e prezzi e continua a gestire le transazioni. L&#39;integrazione nativa sincronizza i dati di prodotto e prezzo in un modo unico da [!DNL Commerce] a CCDM. Non installare un connettore separato o un&#39;app [!DNL App Builder] per questa sincronizzazione.

Gli store front utilizzano i servizi di merchandising basati su CCDM per recuperare i dati e il contesto del catalogo per la navigazione, la ricerca, i consigli e il merchandising. Le richieste utilizzano il contesto del catalogo per recuperare prodotti e prezzi per il pubblico previsto. Si continua a gestire la configurazione di siti Web, store e store-view in [!DNL Commerce].

Il diagramma seguente mostra la posizione dei servizi di merchandising nell’architettura Adobe Commerce as a Cloud Service più ampia.

![Architettura di Commerce che mostra il flusso di dati del catalogo in Merchandising Services](./assets/data-flow-ccdm.png){zoomable="yes"}

## Novità per i commercianti

Il nuovo modello consente di estendere le regole di merchandising esistenti a tutte le viste di catalogo o a una vista specifica. Questo consente di applicare il merchandising a ogni pubblico della vetrina. Scopri come [estendere una regola di merchandising alle viste catalogo](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/merchandising/rules/add).

In Amministrazione è possibile configurare il contesto del catalogo con [!UICONTROL Catalog Views] e [!UICONTROL Policies]. È inoltre possibile utilizzare [!UICONTROL Success Metrics] per esaminare i ricavi, la conversione, il coinvolgimento, l&#39;acquisizione e il tasso di mancato recapito. Per informazioni dettagliate, consulta [Metriche di successo](https://experienceleague.adobe.com/en/docs/commerce-admin/merchandising-with-ccdm/manage-results/success-metrics).

## Considerazioni prima dell’adozione

Prima di adottare i servizi di merchandising, controlla in che modo il modello CCDM influisce sui flussi di lavoro relativi a licenze, integrazioni di cataloghi, vetrina e amministrazione.

### Gestione del catalogo e integrazioni

Continua a gestire prodotti e prezzi in [!DNL Commerce Foundation]. L’integrazione nativa li sincronizza con il CCDM. Non creare un secondo catalogo di prodotti per Merchandising Services.

### Implementazione storefront

Il modo in cui la vetrina recupera i dati del catalogo dipende dall’implementazione:

- **[!DNL Adobe Commerce Storefront]** elenchi a discesa: questi ultimi gestiscono la transizione. Non sono richieste modifiche al codice. Consulta la [documentazione di configurazione della vetrina](https://experienceleague.adobe.com/en/tools/commerce-storefront/).
- **Storefront personalizzati o di altro tipo** - Aggiorna le intestazioni di richiesta del catalogo come descritto nel [riferimento alla configurazione dell&#39;intestazione](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

Esamina le query di catalogo e le intestazioni di richiesta per il modello basato su CCDM. Non presumere che le query o le intestazioni esistenti rimangano invariate. Le query GraphQL di merchandising sono diverse dalle query utilizzate nel modello originale di catalog-services. Altre query supportano CCDM. Utilizza il [riferimento API GraphQL per merchandising](https://developer.adobe.com/commerce/services/reference/graphql/) e verifica il contesto del catalogo richiesto in base al [riferimento intestazione storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

### App ed estensioni di terze parti

Rivedi le app e le estensioni di terze parti che leggono i dati del catalogo o utilizzano eventi del catalogo con il loro provider. La compatibilità dipende dal modo in cui ogni app o estensione utilizza tali interfacce.

### Esperienza di amministrazione

Adobe Commerce as a Cloud Service con CCDM utilizza [[!DNL Adobe Unified Experience]](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/admin-unified-experience) (Unified Shell). Adobe ha rilasciato Unified Shell separatamente da CCDM. Le istanze esistenti nel modello Catalog-Services originale mantengono l&#39;accesso sia a Classic che a Unified Shell.

### Limiti

Il modello CCDM non modifica i limiti di Adobe Commerce as a Cloud Service. La condivisione di una base di catalogo con Optimizer non significa che Commerce erediti la capacità o i limiti di Optimizer.

## Disponibilità e migrazione

Le organizzazioni che iniziano con Adobe Commerce as a Cloud Service dopo questa versione ricevono i servizi di merchandising per impostazione predefinita. Se l’organizzazione richiede il modello dati del catalogo originale, contatta il team dell’account Adobe per valutare se è disponibile un’eccezione.

Le organizzazioni che disponevano di Adobe Commerce as a Cloud Service prima di questa versione possono scegliere uno dei modelli di catalogo quando [eseguono il provisioning di una nuova istanza](./getting-started.md#create-an-instance). Per impostazione predefinita, il commutatore [!UICONTROL Enable CCDM] è disabilitato. Una volta attivato, il CCDM non può essere disattivato.

Le istanze esistenti non vengono modificate automaticamente. Con la disponibilità generale (GA, General Availability) non è possibile eseguire la migrazione di un&#39;istanza Catalog-Services originale esistente a Merchandising Services.
