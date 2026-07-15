---
title: Integrazione di AEM Assets per Commerce
description: Scopri come integrare Adobe Experience Manager Assets con l'istanza  [!DNL Commerce]  per creare e gestire i file multimediali per la vetrina Commerce.
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
TQID: https://experienceleague.adobe.com/CTDmM7Ox2rQ-55F1BVTg-C8DPBEuEpzFxXGtWpnjXKs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 1081
ht-degree: 1%

---

# Integrazione di AEM Assets per Commerce

La domanda di contenuti personalizzati sta rapidamente aumentando mentre i budget per il marketing sono sotto pressione. Rivenditori e marchi hanno difficoltà a tenere il passo con la crescente necessità di varianti di immagini di prodotto, dettate da requisiti regionali, stagionali e specifici del segmento.

Prendi in considerazione un retailer con 1.000 prodotti. Il numero di risorse digitali richieste si espande in modo significativo se si considerano diverse aree geografiche, segmenti di clienti e attività di personalizzazione. Questa situazione può portare a un numero enorme di variazioni di attività, che possono raggiungere i milioni.

![panoramica](assets/product-visuals-example.png){width="700" zoomable="yes"}

L’integrazione di AEM Assets affronta questa sfida automatizzando i flussi di lavoro per la gestione delle risorse. L’integrazione collega dinamicamente le risorse digitali ai prodotti e alle categorie di Adobe Commerce appropriati in base allo SKU o ad altri attributi chiave. Questo processo semplifica le operazioni e migliora l&#39;efficienza consentendo:

* **Installazione e configurazione senza problemi**- I team di merchandising e gli sviluppatori possono configurare rapidamente l&#39;integrazione utilizzando gli strumenti e i flussi di lavoro di Adobe familiari.

* **Aggiornamenti risorse dinamiche** - Le immagini di prodotto e le risorse di marketing riflettono automaticamente le ultime modifiche in AEM Assets, mantenendo gli store front precisi e rilevanti.

* **Gestione semplificata del catalogo**: automatizza l&#39;aggiornamento e la pulizia delle risorse, riducendo al minimo gli sforzi manuali e garantendo un catalogo dei prodotti coerente e ben gestito.

## Requisiti per l’utilizzo dell’integrazione

Per sfruttare questa integrazione con [Product Visuals o AEM Assets](https://experienceleague.adobe.com/it/docs/commerce/cloud-service/overview#product-visuals-powered-by-aem-assets), le aziende devono soddisfare i seguenti requisiti:

>[!BEGINTABS]

>[!TAB Visualizzazioni prodotto]

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} Licenze attive per Adobe Commerce, Visuali prodotto con tecnologia AEM Assets e [AEM Dynamic Media](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media) (queste licenze sono disponibili come standard con [!DNL Adobe Commerce as a Cloud Service] e [!DNL Adobe Commerce Optimizer]).

>[!TAB AEM Assets]

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} Licenze attive per Adobe Commerce, Adobe Experience Manager Assets e [AEM Dynamic Media](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media).

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Adobe Commerce 2.4.5+

* PHP 8.1, 8.2, 8.3 e 8.4

* Compositore 2.x

Per [!BADGE solo SaaS]{type=Positive url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} è stato eseguito il provisioning di Adobe Experience Manager con [Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/overview)

>[!ENDTABS]

L&#39;utente di Adobe Commerce che configura l&#39;integrazione deve avere accesso all&#39;organizzazione [IMS](https://experienceleague.adobe.com/it/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) in cui è stato eseguito il provisioning del progetto AEM Assets.

>[!BEGINSHADEBOX]

## Vantaggi principali per il business

![check](assets/icon-check.png) **Nessun costo aggiuntivo** - Questa integrazione viene fornita gratuitamente ai commercianti che soddisfano i requisiti di licenza.

![verifica](assets/icon-check.png) **Soluzione Adobe ufficiale** - Sviluppata, mantenuta e completamente supportata da Adobe, per garantire stabilità e allineamento con i futuri miglioramenti della piattaforma.

![verifica](assets/icon-check.png) **Adobe Managed Support Model** - Adobe gestisce direttamente l&#39;assistenza e la risoluzione dei problemi, fornendo un supporto affidabile e una risoluzione dei problemi semplificata.

![verifica](assets/icon-check.png) **Funzionalità di Adobe Storefront Builder** - La soluzione di gestione delle risorse digitali (DAM) consente l&#39;utilizzo di risorse quali immagini, video e altri supporti nel [Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=it#userlabs-commerce-genai-product-visuals).

>[!ENDSHADEBOX]

## Esercitazione

Per scoprire come impostare e utilizzare l’integrazione di AEM Assets con Adobe Commerce, guarda questi video.

>[!BEGINTABS]

>[!TAB Esercitazione Adobe Commerce su cloud o locale]

Per scoprire come Adobe Commerce e AEM Assets collaborano per semplificare i flussi di lavoro dei contenuti, guarda questo video:

>[!VIDEO](https://video.tv.adobe.com/v/3447893?captions=ita)

>[!TAB Esercitazione su Adobe Commerce as a Cloud Service]

Scopri come utilizzare Adobe Commerce as a Cloud Service con l’integrazione AEM Assets.

>[!VIDEO](https://video.tv.adobe.com/v/3478140?quality=12&learn=on)

>[!ENDTABS]

## Passaggi successivi

Il processo di installazione e configurazione dell’integrazione di AEM Assets dipende dalla distribuzione di Adobe Commerce. In tutti i casi, devi prima configurare AEM Assets, quindi collegare Commerce.

Per comprendere lo spazio dei nomi, lo schema dei metadati e la scheda **[!UICONTROL Commerce]** aggiunti dall&#39;integrazione all&#39;ambiente AEM Assets, controlla [metadati Commerce in AEM Assets](metadata.md) prima di iniziare.

Seleziona la distribuzione per seguire i passaggi richiesti nell’ordine:

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE Solo SaaS]{type=Positive tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service (infrastruttura SaaS gestita da Adobe)."}

1. Per supportare i metadati di Commerce, [configura il progetto AEM Assets](get-started/configure-aem.md). In AEM versione `2026.5.26309` e successive, utilizzare l&#39;[onboarding self-service](get-started/configure-aem.md#enable-aem-commerce-self-service); nelle versioni precedenti, installare manualmente il pacchetto `assets-commerce`.

1. [Configura le autorizzazioni utente IMS](get-started/permissions.md) in modo che siano disponibili i campi Selettore risorse e **[!UICONTROL Program ID]** e **[!UICONTROL Environment ID]** compilati automaticamente.

1. [Configurare l&#39;integrazione nell&#39;amministratore di Commerce](get-started/setup-synchronization.md).

1. Facoltativo. [Abilita la visualizzazione dell&#39;immagine del prodotto](get-started/configure-storefront.md#enable-product-images) in modo che una vetrina basata su Edge Delivery Services esegua il rendering delle immagini dei prodotti gestiti da AEM.

>[!TAB Adobe Commerce su cloud (PaaS)]

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."}

1. Per supportare i metadati di Commerce, [configura il progetto AEM Assets](get-started/configure-aem.md). In AEM versione `2026.5.26309` e successive, utilizzare l&#39;[onboarding self-service](get-started/configure-aem.md#enable-aem-commerce-self-service); nelle versioni precedenti, installare manualmente il pacchetto `assets-commerce`.

1. [Installa i pacchetti Adobe Commerce](get-started/configure-commerce.md) per aggiungere l&#39;estensione e generare le credenziali e le connessioni richieste.

1. [Configura le autorizzazioni utente IMS](get-started/permissions.md) in modo che siano disponibili i campi Selettore risorse e **[!UICONTROL Program ID]** e **[!UICONTROL Environment ID]** compilati automaticamente.

1. [Configurare l&#39;integrazione nell&#39;amministratore di Commerce](get-started/setup-synchronization.md).

1. Facoltativo. [Abilita la visualizzazione dell&#39;immagine del prodotto](get-started/configure-storefront.md#enable-product-images) in modo che una vetrina basata su Edge Delivery Services esegua il rendering delle immagini dei prodotti gestiti da AEM.

>[!TAB Adobe Commerce Optimizer]

[!BADGE Solo SaaS]{type=Positive tooltip="Applicabile solo ai progetti Adobe Commerce Optimizer."}

[!DNL Adobe Commerce Optimizer] Non dispone di un&#39;interfaccia utente di configurazione amministratore. Il supporto Adobe configura l’integrazione dal ticket di onboarding, quindi prepara prima AEM Assets.

1. Per supportare i metadati di Commerce, [configura il progetto AEM Assets](get-started/configure-aem.md). In AEM versione `2026.5.26309` e successive, utilizzare l&#39;[onboarding self-service](get-started/configure-aem.md#enable-aem-commerce-self-service); nelle versioni precedenti, installare manualmente il pacchetto `assets-commerce`.

1. [Invia il ticket di supporto all&#39;onboarding](get-started/configure-aco.md#onboarding) con il tuo ID tenant, l&#39;ID programma AEM, l&#39;ID ambiente AEM, la regola, il livello e le impostazioni locali corrispondenti.

1. [Configura la vista catalogo](get-started/configure-aco.md#onboarding) con le stesse impostazioni locali e lo stesso livello registrati nel ticket.

1. Facoltativo. [Abilita la visualizzazione dell&#39;immagine del prodotto](get-started/configure-storefront.md#enable-product-images) in modo che una vetrina basata su Edge Delivery Services esegua il rendering delle immagini dei prodotti gestiti da AEM.

   Per informazioni dettagliate su procedure, limitazioni e livelli, vedere [Configurare AEM Assets per Commerce Optimizer](get-started/configure-aco.md).

>[!ENDTABS]

## Supporto

Se hai bisogno di informazioni o se hai domande non trattate in questa guida, contatta il tuo rappresentante commerciale per l&#39;integrazione di AEM Assets o crea un [ticket di supporto](https://experienceleague.adobe.com/it/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case) per ricevere ulteriore assistenza.
