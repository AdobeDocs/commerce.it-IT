---
title: Visualizzazioni prodotto con AEM Assets
description: Scopri come utilizzare AEM Assets per le immagini di prodotto in [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Visualizzazioni prodotto con AEM Assets

Product Visuals consente ai commercianti di [!DNL Adobe Commerce Optimizer] di gestire le immagini dei prodotti tramite Adobe Experience Manager (AEM) Assets. Questa integrazione fornisce un flusso di lavoro semplice per sincronizzare immagini di prodotto di alta qualità da AEM Assets al catalogo [!DNL Commerce Optimizer] utilizzando i livelli del catalogo.

## Vantaggi chiave

* **Gestione centralizzata delle risorse**: gestisci tutte le immagini dei prodotti in AEM Assets, la soluzione di gestione delle risorse digitali di livello enterprise.
* **Sincronizzazione automatica**: le immagini dei prodotti vengono sincronizzate automaticamente quando le risorse vengono approvate o aggiornate in AEM Assets.
* **Consegna Dynamic Media**: sfrutta Dynamic Media con funzionalità OpenAPI per una consegna delle immagini ottimizzata.
* **Livelli catalogo**: le immagini dei prodotti vengono applicate come livello catalogo, consentendo di sovrapporre le immagini AEM Assets al catalogo di base.

## Come funziona

L’integrazione ha due flussi principali:

* **Da AEM Assets**: quando una risorsa viene approvata, rifiutata o rimossa, l&#39;evento passa attraverso la pipeline di Adobe al servizio di integrazione di Assets. Il servizio associa le risorse ai prodotti utilizzando una strategia di corrispondenza `match-by-SKU` o personalizzata, quindi invia le mappature `product-asset` a [!DNL Commerce Optimizer], dove vengono memorizzate come livelli di prodotto.

* **Da ACO**: quando un prodotto viene aggiornato in [!DNL Commerce Optimizer], l&#39;evento passa attraverso la pipeline di Adobe al servizio di integrazione di Assets. Il servizio sincronizza con ACO eventuali mappature di risorse corrispondenti.

Le immagini aggiornate sono disponibili tramite le API vetrina (Catalog Service, Live Search, Product Recommendations).

### Configurazione di Source e livelli

Le immagini da AEM Assets vengono acquisite come livello di catalogo con la seguente configurazione di origine:

> Esempio di configurazione sorgente

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

Questa configurazione assicura che le immagini AEM Assets vengano applicate come sovrapposizione al catalogo prodotti di base.

## Prerequisiti

Prima di abilitare Product Visuals, assicurati di soddisfare i [prerequisiti per Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md#prerequisites).

## Configurazione

Per abilitare l&#39;integrazione, [crea un ticket di supporto](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) con i tuoi dettagli di [!DNL Commerce Optimizer] e AEM Assets. Il supporto Adobe configura l’integrazione e registra il tenant con il servizio di integrazione Assets.

Per informazioni sull&#39;onboarding, consulta [Configurare AEM Assets per Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md).

### Configurare i metadati di AEM Assets

Per abilitare la corrispondenza automatica dei prodotti, configura le risorse in AEM Assets con i metadati Commerce.

Consulta [Configurare AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets) per i passaggi e i campi di metadati richiesti.

## Utilizzo delle visualizzazioni prodotto

Una volta configurata l’integrazione, gestisci le immagini del prodotto tramite AEM Assets.

### Aggiungere immagini ai prodotti

1. Carica le immagini nel tuo archivio AEM Assets.

1. Aggiungi metadati Commerce alla risorsa. Vedi [Applica metadati alle risorse](../../aem-assets-integration/get-started/configure-aco.md#step-3-apply-metadata-to-assets).

1. Approva la risorsa per la consegna. La risorsa deve essere nello stato **approvato** per attivare la sincronizzazione.

1. L&#39;immagine viene sincronizzata automaticamente con [!DNL Commerce Optimizer].

### Applicare il livello AEM-Assets

Per visualizzare le immagini AEM Assets nella vetrina, [assegna il livello `AEM-Assets` alla vista catalogo](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## Altri argomenti correlati

* [Livelli del catalogo](catalog-layer.md)
* [Visualizzazioni catalogo](catalog-view.md)
* [Guida all’integrazione di AEM Assets](../../aem-assets-integration/overview.md)
