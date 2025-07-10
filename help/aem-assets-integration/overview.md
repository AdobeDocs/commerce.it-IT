---
title: Integrazione di AEM Assets per Commerce
description: Scopri come integrare Adobe Experience Manager Assets con l'istanza  [!DNL Commerce]  per creare e gestire i file multimediali per la vetrina Commerce.
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
source-git-commit: 9e6f8ae86b28577e2b2c675dbf274c762abe9f3f
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Integrazione di AEM Assets per Commerce

La domanda di contenuti personalizzati sta rapidamente aumentando mentre i budget per il marketing sono sotto pressione. Rivenditori e marchi hanno difficoltà a tenere il passo con la crescente necessità di varianti di immagini di prodotto, dettate da requisiti regionali, stagionali e specifici del segmento.

Prendi in considerazione un retailer con 1.000 prodotti. Anche prima di prendere in considerazione le varianti di attributi, il numero di risorse digitali richieste si espande in modo significativo se si considerano diverse aree geografiche, segmenti di clienti e attività di personalizzazione. Questo può portare a un numero enorme di variazioni di risorse, che possono raggiungere i milioni.

![panoramica](assets/product-visuals-example.png){width="700" zoomable="yes"}

L’integrazione di AEM Assets affronta questa sfida automatizzando i flussi di lavoro per la gestione delle risorse. L’integrazione assicura che le risorse digitali, come immagini di prodotti e contenuti di marketing, siano collegate in modo dinamico alle entità di merchandising appropriate, inclusi prodotti e categorie in Adobe Commerce, in base allo SKU o ad altri attributi chiave. Questo processo semplifica le operazioni e migliora l&#39;efficienza consentendo:

* **Installazione e configurazione senza problemi**- I team di merchandising e gli sviluppatori possono configurare rapidamente l&#39;integrazione utilizzando gli strumenti e i flussi di lavoro di Adobe familiari.

* **Aggiornamenti risorse dinamiche** - Le immagini di prodotto e le risorse di marketing riflettono automaticamente le ultime modifiche in AEM Assets, mantenendo gli store front precisi e rilevanti.

* **Gestione semplificata del catalogo**: automatizza l&#39;aggiornamento e la pulizia delle risorse, riducendo al minimo gli sforzi manuali e garantendo un catalogo dei prodotti coerente e ben gestito.

## Requisiti per l’utilizzo dell’integrazione

Per sfruttare questa integrazione con Product Visuals o AEM Assets, le aziende devono soddisfare i seguenti requisiti:

>[!BEGINTABS]

>[!TAB Visualizzazioni prodotto]

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} Licenze attive per Adobe Commerce, Visuali prodotto con tecnologia AEM Assets e [AEM Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media) (queste licenze sono disponibili come standard con [!DNL Adobe Commerce as a Cloud Service] e [!DNL Adobe Commerce Optimizer]).

>[!TAB AEM Assets]

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} Licenze attive per Adobe Commerce, Adobe Experience Manager Assets e [AEM Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media).

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Adobe Commerce 2.4.5+

* PHP 8.1, 8.2, 8.3 e 8.4

* Compositore 2.x

Per [!BADGE solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} è stato eseguito il provisioning di Adobe Experience Manager con [Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/overview)

>[!ENDTABS]

L&#39;utente di Adobe Commerce che configura l&#39;integrazione deve avere accesso all&#39;organizzazione [IMS](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) in cui è stato eseguito il provisioning del progetto AEM Assets.

>[!BEGINSHADEBOX]

## Vantaggi principali per il business

![check](assets/icon-check.png) **Nessun costo aggiuntivo**-Questa integrazione viene fornita gratuitamente ai commercianti che soddisfano i requisiti di licenza.

![verifica](assets/icon-check.png) **Soluzione Adobe ufficiale** sviluppata, mantenuta e completamente supportata da Adobe, per garantire stabilità e allineamento con i futuri miglioramenti della piattaforma.

![verifica](assets/icon-check.png) **Adobe Managed Support Model**-L&#39;assistenza e la risoluzione dei problemi vengono gestite direttamente da Adobe, garantendo la massima tranquillità e la risoluzione semplificata dei problemi.

![verifica](assets/icon-check.png) **Funzionalità di Adobe Storefront Builder**-La soluzione di gestione delle risorse digitali (DAM) consente l&#39;utilizzo di risorse quali immagini, video e altri supporti nel [Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/#userlabs-commerce-genai-product-visuals).

>[!ENDSHADEBOX]

Guarda questo video per scoprire come Adobe Commerce e AEM Assets collaborano per semplificare i flussi di lavoro dei contenuti:

>[!VIDEO](https://video.tv.adobe.com/v/3447837)

## Passaggi successivi

L’abilitazione dell’integrazione di Commerce con Experience Manager Assets è un processo in tre fasi:

1. [Configura il progetto AEM Assets per supportare i metadati di Commerce](get-started/configure-aem.md).

1. [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} [Installa pacchetti Adobe Commerce](get-started/configure-commerce.md).

1. [Configura l&#39;integrazione](get-started/setup-synchronization.md).

## Supporto

Se hai bisogno di informazioni o se hai domande non trattate in questa guida, contatta il tuo rappresentante commerciale per l&#39;integrazione di AEM Assets o crea un [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) per ricevere ulteriore assistenza.
