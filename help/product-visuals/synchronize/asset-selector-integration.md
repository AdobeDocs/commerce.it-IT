---
title: Selezione manuale delle risorse
description: Scopri in che modo il Selettore risorse di AEM integrato nell’amministratore di Commerce consente agli addetti al marketing e ai merchandising di aggiungere facilmente immagini da AEM Assets ad Adobe Commerce, semplificando la gestione delle risorse.
feature: CMS, Media, Integration
source-git-commit: d362e6e821e81f6da99c420881e1e1b1058bbd45
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Selezione manuale delle risorse

**Selettore risorse AEM** consente agli addetti al marketing e ai merchandising di aggiungere facilmente immagini da AEM Assets ad Adobe Commerce, semplificando il processo di gestione delle risorse. Questo metodo garantisce la coerenza del marchio e la conformità limitando la selezione delle risorse a quelle esaminate e approvate in [!DNL DAM (Digital Asset Management system)].

Il **selettore risorse AEM** è disponibile quando l&#39;ID client IMS per il progetto AEM Assets è stato configurato in Amministrazione Commerce. Consulta [Configurare AEM Asset Selector]&#x200B;(#configure-the-aem-asset-selector-in-adobe-commerce.

Quando l&#39;integrazione **AEM Asset Selector** è configurata, gli addetti al marketing e i merchandiser possono:

* Gestisci le immagini delle categorie in modo semplice, garantendone l’allineamento con le linee guida del marchio e della campagna.
* [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Assegna risorse direttamente in Page Builder per contenuti visivamente avanzati.

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

1. Compila il campo **[!UICONTROL IMS Client ID]**.

1. **Salva** la configurazione.

## Passaggi successivi

* [Gestire le immagini delle categorie con il selettore risorse](../manage-assets.md#category-images)
* [Gestire le immagini nel contenuto di Page Builder](../manage-assets.md#using-aem-asset-selector-in-page-builder)
