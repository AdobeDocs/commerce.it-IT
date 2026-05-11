---
title: Configurare Storefront
description: Scopri come collegare la vetrina Edge Delivery Services all’integrazione AEM Assets.
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 137
ht-degree: 0%

---

# Configurare Storefront

L’integrazione di AEM Assets mostra le immagini del prodotto gestite in AEM Assets invece di utilizzare le immagini in hosting in Adobe Commerce. L’integrazione consente funzionalità avanzate di gestione delle immagini, tra cui ottimizzazione avanzata, ritaglio e distribuzione tramite la rete CDN (Content Delivery Network) di Adobe.

Per abilitare l&#39;integrazione in vetrine di Commerce con tecnologia Edge Delivery Services, aggiornare il file di configurazione della vetrina (`config.json`) per aggiungere il parametro `"commerce-assets-enabled": true`.

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

I menu a discesa di Commerce rilevano automaticamente la configurazione `commerce-assets-enabled` e regolano di conseguenza la gestione delle immagini.

Per ulteriori informazioni su come utilizzare AEM Assets con Commerce Storefront con tecnologia Edge Delivery Services, completa la configurazione della vetrina descritta nell&#39;argomento [Integrazione AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) nella documentazione di *Adobe Commerce Storefront*.
