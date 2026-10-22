---
title: Configurazione dei servizi Commerce
description: Scopri come collegare Adobe Commerce ai servizi di merchandising e Magento Open Source ai servizi di pagamento utilizzando il connettore dei servizi di Commerce.
role: Admin, Developer
feature: Integration, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:14:04.410Z'
TQID: 'https://experienceleague.adobe.com/yyUDw1y5CYHxdLlC3bNo0DKK0byamPAKUjK-wwxVEX4'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%
---

# Configurare i servizi Commerce

I progetti Adobe Commerce on cloud infrastructure e on-premise si connettono a servizi come [!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations] e [!DNL Payment Services] tramite Commerce Services Connector. Su [!DNL Adobe Commerce as a Cloud Service], la connessione è configurata automaticamente.

Magento Open Source utilizza Commerce Services Connector per [!DNL Payment Services]. [!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations] richiedono Adobe Commerce e non sono disponibili per Magento Open Source.

>[!NOTE]
>
>Adobe Commerce Optimizer fornisce le funzionalità di cataloghi e merchandising in modo nativo, anziché utilizzare i servizi [!DNL Live Search], [!DNL Catalog Service] e [!DNL Product Recommendations] separati. La sincronizzazione del catalogo non richiede Commerce Services Connector. Altre integrazioni sul backend di Commerce, come [!DNL Payment Services] e [!DNL Data Connection], richiedono ancora il connettore. Vedere [Abilitare Adobe Commerce Optimizer](enable-aco.md) per l&#39;installazione di Optimizer.


## Introduzione

1. Consulta la documentazione di [Commerce Services Connector](/help/landing/saas.md) per ottenere e configurare le chiavi API.

1. Consulta le [Guide dei servizi Adobe Commerce](/help/landing/home.md) per i singoli servizi disponibili tramite il connettore.

## Linee guida correlate

- [Configurare i pagamenti](configure-payments.md)
- [Connettere AEM Assets](connect-aem-assets.md)
- [Integrare con Adobe Experience Platform](integrate-aep.md)
