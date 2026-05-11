---
title: Selezione manuale delle risorse
description: Scopri in che modo il Selettore risorse di AEM integrato nell’amministratore di Commerce consente agli addetti al marketing e ai merchandising di aggiungere facilmente immagini da AEM Assets ad Adobe Commerce, semplificando la gestione delle risorse.
feature: CMS, Media, Integration
exl-id: 3c1f906f-3ec3-4eac-a47e-b21792767359
TQID: https://experienceleague.adobe.com/3fYabUvRiY8KTxQX1YiTBbLxABpQqfZLu0a6IBDsM3E
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 396
ht-degree: 0%

---

# Selezione manuale delle risorse

**Selettore risorse AEM** consente agli addetti al marketing e ai merchandising di aggiungere facilmente immagini da AEM Assets ad Adobe Commerce, semplificando il processo di gestione delle risorse. Questo metodo garantisce la coerenza del marchio e la conformità limitando la selezione delle risorse a quelle esaminate e approvate in [!DNL DAM (Digital Asset Management system)].

Il **selettore risorse AEM** è disponibile quando l&#39;ID client IMS per il progetto AEM Assets è stato configurato nell&#39;amministratore di Commerce e gli utenti dispongono delle [autorizzazioni e dell&#39;autenticazione IMS necessarie](../get-started/permissions.md). Consulta [Configurare AEM Asset Selector](#configure-the-aem-asset-selector-in-adobe-commerce).

Quando l&#39;integrazione **AEM Asset Selector** è configurata, gli addetti al marketing e i merchandiser possono:

* Gestisci le immagini delle categorie in modo semplice, garantendone l’allineamento con le linee guida del marchio e della campagna.
* [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Assegna risorse direttamente in Page Builder per contenuti visivamente avanzati.
* [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} Assegna Assets direttamente in Commerce Storefront con tecnologia Edge Delivery Services per contenuti arricchiti visivamente.

>[!NOTE]
>
> AEM Asset Selector è un componente front-end di AEM Assets che consente di integrare AEM Assets con le applicazioni di authoring. Per ulteriori informazioni su questo componente, vedi [Selettore risorse micro-front](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector){target=_blank} nella *Guida utente di AEM as a Cloud Service*.

## Vantaggi principali

L’incorporazione di AEM Asset Selector nel pannello di amministrazione di Adobe Commerce offre diversi vantaggi chiave:

* **Coerenza marchio**-Visualizza solo le risorse approvate, riducendo al minimo il rischio di immagini obsolete o non conformi sullo storefront.

* **Efficienza**-Consente agli addetti al marketing e ai merchandising di assegnare rapidamente le risorse senza passare da una piattaforma all&#39;altra.

* **Collaboration** semplificato semplifica il lavoro di squadra consentendo la selezione diretta delle immagini da DAM, eliminando i download e i caricamenti manuali.

* **Qualità dei contenuti migliorata**-Assicura l&#39;utilizzo di immagini ottimizzate ad alta risoluzione tra pagine di prodotti, categorie e Page Builder.

![Selettore risorse](../assets/asset-selector.png){width="600" zoomable="yes"}

## Configurare il selettore delle risorse di AEM in Adobe Commerce

1. Dall&#39;amministratore di Commerce, passare a **[!UICONTROL Store]** > Configurazione > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Compila il campo **[!UICONTROL IMS Client ID]**. Per informazioni sulle autorizzazioni richieste e su come ottenere questo ID, consulta [Autorizzazioni utente e IMS](../get-started/permissions.md).

1. **Salva** la configurazione.

## Passaggi successivi

* [Gestire le immagini delle categorie con il selettore risorse](../manage-assets.md#category-images)
* [Gestire le immagini nel contenuto di Page Builder](../manage-assets.md#using-aem-asset-selector-in-page-builder)
