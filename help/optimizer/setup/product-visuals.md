---
title: Visualizzazioni prodotto con AEM Assets
description: Scopri come utilizzare AEM Assets per le immagini di prodotto in [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 264658bee09a22cfd55828c6960153cc1239d3fb
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Visualizzazioni prodotto con AEM Assets

Product Visuals consente ai commercianti di [!DNL Adobe Commerce Optimizer] di gestire le immagini dei prodotti tramite Adobe Experience Manager (AEM) Assets. Questa integrazione fornisce un flusso di lavoro semplice per sincronizzare immagini di prodotto di alta qualità da AEM Assets al catalogo [!DNL Commerce Optimizer] utilizzando i livelli del catalogo.

>[!NOTE]
>
>**Elementi visivi prodotto** è il nome del bundle fornito con [!DNL Adobe Commerce as a Cloud Service] e [!DNL Adobe Commerce Optimizer]. Combina [Dynamic Media con funzionalità OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) e [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime).
>
>I clienti con una licenza AEM Assets diversa (ad esempio, **AEM Assets Ultimate**) possono utilizzare la stessa integrazione; solo la versione di AEM influisce sui passaggi di onboarding, non sul tipo di licenza.

## Vantaggi chiave

* **Gestione centralizzata delle risorse**: gestisci tutte le immagini dei prodotti in AEM Assets, la soluzione di gestione delle risorse digitali di livello enterprise.
* **Sincronizzazione automatica**: le immagini dei prodotti vengono sincronizzate automaticamente quando le risorse vengono approvate o aggiornate in AEM Assets.
* **Consegna Dynamic Media**: sfrutta Dynamic Media con funzionalità OpenAPI per una consegna delle immagini ottimizzata.
* **Livelli catalogo**: le immagini dei prodotti vengono applicate come livello catalogo, consentendo di sovrapporre le immagini AEM Assets al catalogo di base.

## Come funziona

L’integrazione dispone di due flussi di eventi indipendenti. Entrambi utilizzano [Adobe I/O Events](https://developer.adobe.com/events/docs/) per trasferire gli eventi al servizio di integrazione Assets, ma ogni direzione utilizza il proprio provider di eventi:

* **Da AEM Assets al servizio di integrazione di Assets**: quando una risorsa viene approvata, rifiutata o rimossa, l&#39;evento viene inviato al servizio di integrazione di Assets. Il servizio associa le risorse ai prodotti utilizzando una strategia di corrispondenza `match-by-SKU` o personalizzata, quindi invia le mappature `product-asset` a [!DNL Commerce Optimizer], dove vengono memorizzate come livelli di prodotto.

* **Da [!DNL Commerce Optimizer] a Assets Integration Service**: quando un prodotto viene aggiornato in [!DNL Commerce Optimizer], l&#39;evento viene consegnato a Assets Integration Service. Il servizio sincronizza eventuali mapping di risorse corrispondenti in [!DNL Commerce Optimizer].

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

Per abilitare l&#39;integrazione, [crea un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/help-and-support/create-a-support-ticket) con i tuoi dettagli di [!DNL Commerce Optimizer] e AEM Assets. Il supporto Adobe configura l’integrazione e registra il tenant con il servizio di integrazione Assets.

Per informazioni sull&#39;onboarding, consulta [Configurare AEM Assets per Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md).

### Configurare i metadati di AEM Assets

Per abilitare la corrispondenza automatica dei prodotti, configura le risorse in AEM Assets con i metadati Commerce.

Consulta [Configurare AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets-first) per i passaggi e i campi di metadati richiesti.

## Limitazioni

Prima di utilizzare i visualizzatori di prodotto, controlla le [limitazioni dell&#39;integrazione](../../aem-assets-integration/get-started/configure-aco.md#limitations), ovvero i vincoli relativi ai livelli che influiscono sul modo in cui i dati di AEM Assets vengono uniti al catalogo di base.

Per le allocazioni di capacità e utilizzo (archiviazione delle risorse, operazioni Dynamic Media, licenze utente), consulta [Limiti dei visualizzatori di prodotto](../boundaries-limits.md#product-visuals-limits) nella _Guida limiti e limiti_.

## Utilizzo delle visualizzazioni prodotto

Una volta configurata l’integrazione, gestisci le immagini del prodotto tramite AEM Assets.

### Aggiungere immagini ai prodotti

1. Carica le immagini nel tuo archivio AEM Assets.

1. Aggiungi metadati Commerce alla risorsa.

   Vedi [Corrispondenza automatica predefinita](../../aem-assets-integration/synchronize/default-match.md) e [Corrispondenza automatica personalizzata](../../aem-assets-integration/synchronize/custom-match.md).

1. Approva la risorsa per la consegna. La risorsa deve essere nello stato **approvato** per attivare la sincronizzazione.

1. L&#39;immagine viene sincronizzata automaticamente con [!DNL Commerce Optimizer].

### Applicare il livello AEM-Assets

Per visualizzare le immagini AEM Assets nella vetrina, [assegna il livello `AEM-Assets` alla vista catalogo](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## Altri argomenti correlati

* [Livelli del catalogo](catalog-layer.md)
* [Visualizzazioni catalogo](catalog-view.md)
* [Guida all’integrazione di AEM Assets](../../aem-assets-integration/overview.md)
