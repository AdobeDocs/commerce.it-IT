---
title: Connettore Adobe Commerce Optimizer
description: Scopri come collegare i dati dal cloud Commerce o dal progetto on-premise a Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 380d2c91a17a3e6b84d435774de1b05ada7d3a52
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# Connettore Adobe Commerce Optimizer

Il connettore Adobe Commerce Optimizer è il bridge di integrazione che sincronizza i dati di catalogo e determinazione prezzi tra un&#39;infrastruttura cloud Adobe Commerce o un&#39;implementazione locale e [!DNL Adobe Commerce Optimizer]. La sincronizzazione dei dati con Adobe Commerce Optimizer consente di utilizzare funzioni quali Ricerche IA dinamiche, consigli, vetrine con caricamento rapido headless, incluse vetrine Adobe Commerce su Edge Delivery Services, e analisi delle prestazioni in tempo reale.

## Architettura ed esperienza

Il connettore Adobe Commerce Optimizer funziona mappando i siti web Commerce e memorizzando le viste su un progetto Commerce Optimizer come mostrato nella figura seguente:

![Mappatura dei dati di Commerce a Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.svg){width="600" zoomable="yes"}

Quando i dati vengono esportati da Commerce a Commerce Optimizer:

* Le visualizzazioni dello store di Commerce sono mappate alle origini del catalogo
* I siti Web sono mappati su listini prezzi

I dati di catalogo e prezzo associati vengono esportati e successivamente utilizzati per creare visualizzazioni di catalogo e, facoltativamente, definire un criterio per filtrare i dati di catalogo e prezzo per casi d’uso aziendali specifici.

Invece di configurare e gestire i servizi Commerce (Live Search e Product Recommendations) dall&#39;amministratore di Commerce, puoi utilizzare [[!DNL Adobe Commerce Optimizer] strumenti di merchandising](../optimizer/merchandising/overview.md) per gestire l&#39;individuazione dei prodotti (Live Search) e la configurazione delle regole di consigli (Product Recommendations). L’istanza di Adobe Commerce diventa l’origine dati per i dati di catalogo e prezzo. Quando i dati vengono aggiornati in Commerce, gli aggiornamenti vengono sincronizzati nell&#39;istanza [!DNL Adobe Commerce Optimizer].

## Flussi di lavoro

Il connettore consente diversi flussi di lavoro chiave:

* **Esporta dati catalogo Commerce in[!DNL Adobe Commerce Optimizer]**. I dati relativi al listino prezzi e al listino prezzi vengono esportati a livello di sito Web e di gruppo di clienti. I dati degli attributi del prodotto e del prodotto vengono esportati al livello `store view`. Per impostazione predefinita, la sincronizzazione dei dati del catalogo è abilitata per tutti gli ambiti di Commerce (siti Web e visualizzazioni dello store).

  Per abilitare questo flusso di lavoro, installare l&#39;estensione PHP `adobe-commerce/commerce-data-export-aco-adapter`, rivedere la configurazione di esportazione e quindi abilitare l&#39;integrazione tra Commerce e Commerce Optimizer dall&#39;amministratore di Commerce. Per istruzioni dettagliate, vedere [Introduzione](#get-started).

* **Mappa il sito Web Commerce e archivia i dati della visualizzazione da esportare in[!DNL Adobe Commerce Optimizer]**

  Se necessario, personalizzare le impostazioni di esportazione per sincronizzare i dati solo per siti Web specifici o per visualizzazioni dello store. Ad esempio, puoi scegliere di esportare i dati del catalogo per una sola visualizzazione store da utilizzare per un caso d’uso specifico, ad esempio ottimizzando l’esperienza di ricerca e rilevamento per un mercato o un’area geografica specifica.

* **Configurazione e gestione regole merchandising**

  Quando il connettore è abilitato, le regole di merchandising per l&#39;individuazione dei prodotti e i consigli vengono definite e gestite dall&#39;interfaccia utente [!DNL Adobe Commerce Optimizer], non dalle pagine [!UICONTROL Live Search] e [!UICONTROL Product Recommendations] nell&#39;amministrazione di Commerce.

* **Distribuisci Commerce Storefront su Edge Delivery Services**

  Dopo aver configurato l&#39;integrazione con [!DNL Adobe Commerce Optimizer], è possibile configurare e implementare uno storefront Commerce su Edge Delivery Services per fornire prestazioni, scalabilità, authoring di contenuti ottimizzato, personalizzazione integrata e costi operativi ridotti utilizzando l&#39;architettura componibile basata su API e i componenti modulari disponibili con [!DNL Adobe Commerce Optimizer].

Per informazioni dettagliate su come impostare l&#39;integrazione e abilitare questi flussi di lavoro, vedere [Introduzione](get-started.md).
