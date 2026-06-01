---
title: Integrazioni Commerce Optimizer
description: Scopri le integrazioni Adobe Commerce Optimizer per la sincronizzazione dei cataloghi, la gestione delle risorse, l’ottimizzazione della vetrina e la connettività Salesforce Commerce Cloud.
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo a  [!DNL Adobe Commerce Optimizer]  progetti (infrastruttura SaaS gestita da Adobe)."
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
source-git-commit: a404c2ff7cec5e72ce65d3670330b1f3f3c4702d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer] integrazioni

[!DNL Adobe Commerce Optimizer] include integrazioni che consentono di sincronizzare dati da Adobe Commerce su cloud o on-premise, gestire risorse, migliorare esperienze di vetrina e collegare sistemi esterni. Le sezioni seguenti descrivono il funzionamento di ogni integrazione con [!DNL Adobe Commerce Optimizer]. Segui i collegamenti per la configurazione e l’utilizzo quotidiano.

{{aco-integration-environment-alignment}}

## Connettore Adobe Commerce Optimizer {#aco-connector}

Il connettore Adobe Commerce Optimizer è il bridge che sincronizza i dati di catalogo e determinazione prezzi tra Adobe Commerce (cloud o locale) e [!DNL Adobe Commerce Optimizer]. Quando abiliti il connettore, Commerce rimane il sistema di registrazione per i dati dei prodotti, mentre [!DNL Adobe Commerce Optimizer] potenzia l&#39;individuazione dei prodotti, i consigli, le regole di merchandising, le analisi e le esperienze di vetrina headless.

- [Panoramica del connettore Adobe Commerce Optimizer](../../aco-connector/overview.md){target="_blank"}
- [Introduzione al connettore](../../aco-connector/get-started.md){target="_blank"}

## Visualizzazioni prodotto con AEM Assets {#product-visuals}

Product Visuals consente di gestire le immagini dei prodotti tramite Adobe Experience Manager (AEM) Assets. Configura AEM Assets per Commerce Optimizer per abilitare i Visualizzatori di prodotto. Al termine della configurazione, utilizzi AEM Assets come soluzione centralizzata per la gestione delle risorse digitali per le immagini dei prodotti, con flussi di lavoro automatizzati per la revisione e la gestione delle risorse che mantengono le immagini sincronizzate con il catalogo Commerce Optimizer. L’integrazione associa le risorse ai prodotti per SKU. Gli aggiornamenti passano attraverso i servizi di integrazione di Adobe, in modo che le vetrine riflettano i file multimediali più recenti senza ricaricamenti manuali.

- [Visualizzazioni prodotto con AEM Assets](../setup/product-visuals.md)
- [Configurare AEM Assets per Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md){target="_blank"}

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

Adobe Experience Manager Sites Optimizer analizza i siti Web Commerce e migliora le prestazioni presentando **[!UICONTROL Opportunities]** basato sull&#39;intelligenza artificiale: consigli che consentono di migliorare l&#39;individuazione, il coinvolgimento e le conversioni.

>[!AVAILABILITY]
>
>Questa funzionalità richiede la licenza **Ultima** Adobe Sites Optimizer. È possibile richiedere una licenza tramite il proprio consulente tecnico clienti Adobe. Una volta eseguito il provisioning del tuo account, la funzione Opportunità è disponibile nell&#39;interfaccia [!DNL Adobe Commerce Optimizer] e puoi iniziare a utilizzare informazioni basate sull&#39;intelligenza artificiale per ottimizzare le strategie di storefront e merchandising.

- [Opportunità](../manage-results/opportunities.md)

## Connettore Salesforce Commerce {#commerce-salesforce-connector}

Il connettore Salesforce di Commerce (basato su Adobe App Builder) sincronizza i dati di catalogo e prezzo da Salesforce Commerce Cloud B2C in [!DNL Adobe Commerce Optimizer] in modo da poter utilizzare le funzionalità di vetrina e merchandising di Adobe senza dover riorganizzare il back-end di Salesforce commerce. Puoi pianificare le sincronizzazioni, eseguire aggiornamenti su richiesta ed estendere l’integrazione utilizzando le API di Salesforce Commerce.

- [Connettore Commerce Salesforce](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Documentazione tecnica di Adobe Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [Introduzione a Adobe Commerce Optimizer](../get-started.md)
