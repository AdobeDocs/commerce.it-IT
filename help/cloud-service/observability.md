---
title: Osservabilità per  [!DNL Adobe Commerce as a Cloud Service]
description: Scopri gli strumenti di osservabilità e le funzionalità di telemetria disponibili per  [!DNL Adobe Commerce as a Cloud Service], tra cui metriche, registrazione e analisi.
feature: Cloud, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
autotag-review: '2026-06-09T15:41:54.613Z'
TQID: 'https://experienceleague.adobe.com/jTPNVSy6cP8v-pV-3pyqgJX-PAzFFhOUf9SjQIMeBns'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: ef32511703a96b5f4db32d54229e9a7cbe961f12
workflow-type: tm+mt
source-wordcount: 607
ht-degree: 0%

---

# Osservabilità

L&#39;osservabilità è un aspetto critico del funzionamento di [!DNL Adobe Commerce as a Cloud Service]. Include la raccolta, l&#39;elaborazione e la visualizzazione dei dati di telemetria, incluse metriche, registrazione e tracciamento, per consentire il monitoraggio dello stato delle applicazioni, la diagnosi dei problemi di prestazioni e l&#39;ottimizzazione dell&#39;affidabilità della piattaforma commerce e delle relative integrazioni.

## [!DNL Adobe Commerce as a Cloud Service]

### Panoramica sull’osservabilità

L’osservabilità offre visibilità sullo stato e sulle prestazioni della vetrina Adobe Commerce e di tutte le applicazioni App Builder connesse. Raccogliendo i dati di telemetria nell&#39;ecosistema commerce, è possibile:

* **Tieni traccia delle metriche**, ad esempio i tempi di risposta delle API, le percentuali di richieste ed errori e l&#39;utilizzo delle risorse per monitorare le prestazioni in tempo reale e le tendenze spot.
* **Centralizza i registri** dall&#39;applicazione, dall&#39;infrastruttura, dalla rete CDN e dalle integrazioni in un&#39;unica vista per una risoluzione più rapida dei problemi.
* **Richieste di trace** end-to-end durante il flusso dal front-end attraverso Commerce e le app connesse, per individuare i colli di bottiglia e gli errori prima che influiscano sui clienti.

Queste funzionalità consentono di identificare e risolvere rapidamente i problemi, ottimizzare le prestazioni e garantire un&#39;esperienza affidabile per i clienti. La [panoramica sull&#39;osservabilità](https://developer.adobe.com/commerce/extensibility/observability/) spiega come [!DNL Adobe Commerce as a Cloud Service] utilizza OpenTelemetry per unificare questa raccolta di telemetria tra eventi, webhook e applicazioni App Builder.

![Architettura di osservabilità](./assets/observability.png){width="600" zoomable="yes"}

Adobe Commerce supporta i seguenti strumenti di osservabilità tramite OpenTelemetry:

* Elasticsearch
* Grafana
* Jaeger
* New Relic
* Prometeo
* Splunk
* Zipkin

### Configurare le sottoscrizioni

[Configurare le sottoscrizioni di osservabilità](https://developer.adobe.com/commerce/extensibility/observability/configuration/) in [!UICONTROL Admin] o tramite l&#39;API REST per instradare registri, metriche o tracce a qualsiasi endpoint compatibile con OpenTelemetry. Ogni sottoscrizione esegue il targeting di componenti specifici (webhook, eventi o [!UICONTROL Admin UI SDK]).

### API REST di osservabilità

L&#39;[API REST di osservabilità](https://developer.adobe.com/commerce/extensibility/observability/api/) fornisce endpoint che creano, recuperano, aggiornano ed eliminano sottoscrizioni di osservabilità a livello di programmazione. Utilizza questi endpoint per automatizzare la configurazione tra le istanze.

## Adobe Developer App Builder

### Strumentazione App Builder

[Implementa l&#39;osservabilità in [!DNL App Builder]](https://developer.adobe.com/commerce/extensibility/observability/app-builder/) per propagare il contesto di traccia da Commerce nelle azioni [!DNL App Builder] in modo che i registri e le tracce di entrambi i sistemi siano correlati nella piattaforma di osservabilità. Include la strumentazione per integrazioni basate su webhook e su eventi.

[!DNL App Builder] fornisce inoltre strumenti incorporati per [gestire i registri delle applicazioni](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/application_logging/logging), incluso l&#39;accesso a CLI e Developer Console, e l&#39;inoltro dei registri a soluzioni esterne quali Splunk, Azure e New Relic.

### Libreria di telemetria

La libreria [`@adobe/aio-lib-telemetry`](https://github.com/adobe/aio-lib-telemetry/blob/main/docs/usage.md) è ciò che le azioni App Builder utilizzano per emettere log e tracce compatibili con OpenTelemetry. Include l&#39;installazione, la configurazione e la configurazione di esportazione.

### Sviluppo e test locali

[Verifica localmente la configurazione dell&#39;osservabilità](https://developer.adobe.com/commerce/extensibility/observability/local-development/) prima della distribuzione. Utilizzare [!DNL Grafana] per la visualizzazione e l&#39;inoltro tunnel (ad esempio, [!DNL Ngrok]) per ricevere la telemetria da un&#39;istanza remota di Commerce nel computer di sviluppo.

## [!DNL API Mesh]

### Registrazione Mesh API

[Registrazione Mesh API](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/logging/) consente di monitorare ed eseguire il debug delle richieste che scorrono nella rete utilizzando gli ID di ray. Esportare i registri in blocco o inoltrarli a piattaforme come [!DNL New Relic] per l&#39;analisi centralizzata.

## Vetrina

### Monitoraggio CDN e Real User

[Raccolta di dati Proxy Real User Monitoring (RUM)](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/#proxy-rum-through-the-origin-to-avoid-a-tls-handshake) tramite l&#39;origine CDN per eliminare un handshake TLS aggiuntivo e migliorare la misurazione delle prestazioni front-end.

## Video di osservabilità

I video seguenti forniscono una panoramica di alto livello delle offerte di osservabilità in [!DNL Adobe Commerce as a Cloud Service]:

* [Video sull’osservabilità di App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/observability/overview){target="_blank"}
* [Video Mesh API](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/api-mesh/getting-started-api-mesh){target="_blank"}
