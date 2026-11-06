---
title: Integrazioni Commerce Optimizer
description: Scopri le integrazioni Adobe Commerce Optimizer per la sincronizzazione dei cataloghi, la gestione delle risorse, l’ottimizzazione della vetrina e la connettività Salesforce Commerce Cloud.
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo a [!DNL Adobe Commerce Optimizer] progetti (infrastruttura SaaS gestita da Adobe)."
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 9b3448a40c2e829e09de5e394b0972c527ee0e9b
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%
---

# [!DNL Adobe Commerce Optimizer] integrazioni

[!DNL Adobe Commerce Optimizer] include integrazioni che consentono di sincronizzare dati da Adobe Commerce su cloud o on-premise, gestire risorse, migliorare esperienze di vetrina e collegare sistemi esterni. Le sezioni seguenti descrivono il funzionamento di ogni integrazione con [!DNL Adobe Commerce Optimizer]. Segui i collegamenti per la configurazione e l’utilizzo quotidiano.

{{aco-integration-environment-alignment}}

## Visualizzazioni prodotto con AEM Assets {#product-visuals}

Product Visuals consente di gestire le immagini dei prodotti tramite Adobe Experience Manager (AEM) Assets. Configura AEM Assets per Commerce Optimizer per abilitare i Visualizzatori di prodotto. Al termine della configurazione, utilizzi AEM Assets come soluzione centralizzata per la gestione delle risorse digitali per le immagini dei prodotti, con flussi di lavoro automatizzati per la revisione e la gestione delle risorse che mantengono le immagini sincronizzate con il catalogo Commerce Optimizer. L’integrazione associa le risorse ai prodotti per SKU. Gli aggiornamenti passano attraverso i servizi di integrazione di Adobe, in modo che le vetrine riflettano i file multimediali più recenti senza ricaricamenti manuali.

- [Visualizzazioni prodotto con AEM Assets](../setup/product-visuals.md)

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

Adobe Experience Manager Sites Optimizer analizza i siti Web Commerce e migliora le prestazioni presentando **[!UICONTROL Opportunities]** basato sull&#39;intelligenza artificiale: consigli che consentono di migliorare l&#39;individuazione, il coinvolgimento e le conversioni.

>[!AVAILABILITY]
>
>Questa funzionalità richiede la licenza **Ultima** Adobe Sites Optimizer. È possibile richiedere una licenza tramite il proprio consulente tecnico clienti Adobe. Una volta eseguito il provisioning del tuo account, la funzione Opportunità è disponibile nell&#39;interfaccia [!DNL Adobe Commerce Optimizer] e puoi iniziare a utilizzare informazioni basate sull&#39;intelligenza artificiale per ottimizzare le strategie di storefront e merchandising.

- [Opportunità](../manage-results/opportunities.md)

## Connettore Adobe Commerce Optimizer {#aco-connector}

Il connettore Adobe Commerce Optimizer è il bridge che sincronizza i dati di catalogo e determinazione prezzi tra Adobe Commerce (cloud o locale) e [!DNL Adobe Commerce Optimizer]. Quando abiliti il connettore, Commerce rimane il sistema di registrazione per i dati dei prodotti, mentre [!DNL Adobe Commerce Optimizer] potenzia l&#39;individuazione dei prodotti, i consigli, le regole di merchandising, le analisi e le esperienze di vetrina headless. Per limitare gli utenti che possono eseguire query su una visualizzazione catalogo sincronizzata, vedere [Visualizzazioni catalogo privato](../setup/private-catalog-view.md).

- [Panoramica del connettore Adobe Commerce Optimizer](../../aco-connector/overview.md){target="_blank"}
- [Introduzione al connettore](../../aco-connector/get-started.md){target="_blank"}

## Integrazione di carrello e pagamento di terze parti

Adobe Commerce Optimizer può potenziare l’individuazione dei prodotti e il merchandising per una vetrina che utilizza una piattaforma di e-commerce separata per le transazioni. La vetrina utilizza le API di Commerce Optimizer Merchandising Services per dati di prodotto, ricerche, consigli e merchandising. La piattaforma di e-commerce dell’host rimane responsabile degli account cliente, del carrello, del pagamento e dell’elaborazione degli ordini. L’integrazione con la piattaforma host è un’implementazione personalizzata che utilizza API Mesh, App Builder, API dirette o una combinazione di questi strumenti.

Per Salesforce Commerce Cloud (SFCC), il [Adobe Commerce Optimizer SFCC Checkout Starter Kit](https://github.com/adobe-commerce/aco-sfcc-checkout-starter-kit) fornisce esempi di blocchi e script Edge Delivery Services per la connessione di una vetrina Adobe Commerce Optimizer a una funzionalità SFCC shopper, cart e checkout. Utilizzala come implementazione di riferimento e adattala alla vetrina; non è un connettore predefinito generico. È disponibile anche un esempio di [vetrina headless per Next.js](https://github.com/adobe-commerce/aco-sfcc-storefront-next){target="_blank"}.


## Connettore Salesforce Commerce {#commerce-salesforce-connector}

Il connettore Salesforce di Commerce (basato su Adobe App Builder) sincronizza i dati di catalogo e prezzo da Salesforce Commerce Cloud B2C in [!DNL Adobe Commerce Optimizer] in modo da poter utilizzare le funzionalità di vetrina e merchandising di Adobe senza dover riorganizzare il back-end di Salesforce commerce. Puoi pianificare le sincronizzazioni, eseguire aggiornamenti su richiesta ed estendere l’integrazione utilizzando le API di Salesforce Commerce.

- [Connettore Commerce Salesforce](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Documentazione tecnica di Adobe Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [Introduzione a Adobe Commerce Optimizer](../get-started.md)
