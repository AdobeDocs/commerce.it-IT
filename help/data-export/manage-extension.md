---
title: '[!DNL Manage the Data Export extension]'
description: Scopri come aggiornare l'estensione  [!DNL Data Export]  e rimuovere o disabilitare i servizi di esportazione dati non richiesti.
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
source-git-commit: ea722d5e427e5bf536b9f2d2322f0dabb2981c77
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Gestire l’estensione di esportazione dei dati SaaS

L&#39;[[!DNL data export] estensione](https://github.com/magento/commerce-data-export) per i servizi SaaS è una raccolta di moduli che consentono la raccolta e la sincronizzazione dei dati tra Adobe Commerce e i servizi Commerce connessi.

Moduli specifici sono inclusi nei metapacchetti per le estensioni di Adobe Commerce Services, ad esempio
come [Live Search](/help/live-search/overview.md), [Product Recommendations](/help/product-recommendations/overview.md) e [Catalog Service](/help/catalog-service/overview.md). Se utilizzi questi servizi, non è necessaria alcuna installazione separata per abilitare l’estensione Esportazione dati.

## Rimuovere o disabilitare le funzioni di esportazione dei dati di Commerce

Se non è necessario uno dei moduli di esportazione dei dati di commerce installati, utilizzare il comando CLI `magento:module:disable` per disabilitarlo.

Esiste ad esempio un&#39;API [Categories](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) che utilizza internamente i dati del feed di autorizzazioni delle categorie. Se non utilizzi questa API, puoi disabilitare l’esportazione dei dati per il feed di autorizzazioni per le categorie.

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### Aggiornare un modulo a una versione specifica

Puoi aggiornare uno qualsiasi dei moduli di esportazione dei dati di e-commerce installati utilizzando Composer. Ad esempio, puoi aggiornare un modulo a una versione specificata e anche aggiornare eventuali dipendenze richieste.

1. Accedere al server applicazioni Commerce.

1. Dalla riga di comando, aggiorna il modulo utilizzando Compositore:

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

Se l’istanza Commerce è distribuita nell’infrastruttura cloud, aggiorna l’estensione dalla directory del progetto cloud. Consulta [Aggiornare un&#39;estensione](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension) nella _Guida di Adobe Commerce sull&#39;infrastruttura cloud_.
