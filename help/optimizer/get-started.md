---
title: Introduzione a  [!DNL Adobe Commerce Optimizer]
description: Scopri come iniziare a utilizzare  [!DNL Adobe Commerce Optimizer].
hide: true
recommendations: noCatalog
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 9c3f5d1d5e7fd57d2306502d654a854bc5c66c71
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Introduzione

>[!NOTE]
>
>Questa documentazione descrive un prodotto in fase di sviluppo con accesso anticipato e non riflette tutte le funzionalità previste per la disponibilità generale.

Questa guida illustra come creare e utilizzare un&#39;istanza di [!DNL Adobe Commerce Optimizer].

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/webapi/rest/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## Provisioning

Quando le istanze di [!DNL Adobe Commerce Optimizer] sono pronte, il team di provisioning di [!DNL Adobe Commerce Optimizer] fornisce i seguenti endpoint:

| Elemento | URL di esempio | Finalità |
|---|---|---|
| [!DNL Adobe Commerce Optimizer] UI | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | Accedi all&#39;interfaccia utente di Commerce Optimizer per la gestione del catalogo in:<br>1. Regole di merchandising (individuazione prodotto, consigli prodotto).<br>2. Gestione del catalogo (creazione di canali e criteri).<br>3. Approfondimenti dati (visualizza lo stato di inserimento dei dati nel catalogo). |
| API Storefront | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | Accedi alle API necessarie per configurare la vetrina Commerce con tecnologia Edge Delivery Services. |
| API per l’acquisizione di dati catalogo | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | Accedi alle API necessarie per acquisire i dati del catalogo. |

>[!NOTE]
>
>Per ulteriori informazioni sulle API necessarie per la configurazione della vetrina e l&#39;inserimento del catalogo, consulta la [documentazione per sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

In qualità di partecipante con accesso anticipato, riceverai un&#39;e-mail con un collegamento sicuro che, insieme al token IMS, ti consente di accedere a [!DNL Adobe Commerce Optimizer] o effettuare chiamate API.

## Configurare la vetrina

Ora che disponi di un&#39;istanza [!DNL Adobe Commerce Optimizer], sei pronto per procedere con la [configurazione](./storefront.md) della tua vetrina Commerce con tecnologia Edge Delivery Services.

## Dati di catalogo disponibili per i partecipanti con accesso anticipato

In qualità di partecipante ad accesso anticipato, l&#39;istanza [!DNL Adobe Commerce Optimizer] contiene dati di catalogo fittizi basati sul [caso d&#39;uso Carvelo](./use-case/admin-use-case.md). I dati fittizi, insieme ad alcuni canali e criteri preconfigurati, consentono di acquisire familiarità con l&#39;interfaccia utente di [!DNL Adobe Commerce Optimizer].

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
