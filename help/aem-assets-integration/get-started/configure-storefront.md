---
title: Configurare Storefront
description: Scopri come collegare la vetrina Edge Delivery Services all’integrazione AEM Assets.
feature: CMS, Media, Integration
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '127'
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

Per ulteriori informazioni su come utilizzare AEM Assets con Commerce Storefront con tecnologia Edge Delivery Services, completa la configurazione della vetrina descritta nell&#39;argomento [Integrazione AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=it) nella documentazione di *Adobe Commerce Storefront*.
