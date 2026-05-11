---
title: Onboarding
description: Scopri i requisiti e le piattaforme supportate in [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
TQID: https://experienceleague.adobe.com/FLrOFe-Lwe7i3dOwCISflVGEv2MIkXmmE-NqTvpaY-0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 418
ht-degree: 0%

---

# Onboarding

>[!IMPORTANT]
>
>**Product Recommendations non è un servizio compatibile con HIPAA.** Non abilitare o utilizzare la funzione Consigli di prodotto in alcuna implementazione di Adobe Commerce che utilizzi un’offerta compatibile con HIPAA o che elabori in altro modo informazioni protette sulla salute (PHI). Product Recommendations fa parte dei servizi SaaS di Commerce attualmente classificati come non conformi HIPAA.
>
>Per informazioni dettagliate sulle funzionalità di Adobe Commerce pronte per HIPAA e sui servizi che non devono essere utilizzati con PHI, vedere [Preparazione HIPAA in Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) e [Operazioni](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services).

Il processo di onboarding per [!DNL Product Recommendations] richiede l&#39;accesso alla riga di comando del server ed è costituito dai passaggi seguenti. Se non hai familiarità con l’utilizzo della riga di comando, chiedi aiuto a uno sviluppatore o a un integratore di sistemi.

- [Flusso di lavoro di implementazione](implementation-workflow.md)
- [Installazione e configurazione](install-configure.md)
- [Impostazioni](settings.md)
- [Verifica](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)
- [Ambiente di staging](staging-environment.md)

## Requisiti

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3 o 8.4
- Compositore 2

### Piattaforme supportate

- Adobe Commerce on-premise (EE) : 2.4.4+
- Adobe Commerce on Cloud (ECE) : 2.4.4+

## Endpoint

[!DNL Product Recommendations] comunica attraverso l&#39;endpoint in `https://catalog-service.adobe.io/graphql`.

### Supporto di Page Builder

[!DNL Product Recommendations] può essere aggiunto a una pagina come tipo di contenuto Page Builder. Per aggiungere il supporto di Page Builder ai consigli di prodotto, fare riferimento a [Installazione e configurazione](install-configure.md).

Per istruzioni su come aggiungere [!DNL Product Recommendations] al contenuto di [!DNL Page Builder], vedere [[!DNL Page Builder] Integrazione](page-builder.md).

### Indicizzazione dei prezzi SaaS

I clienti di Product Recommendation possono utilizzare l&#39;[indicizzazione dei prezzi SaaS](../price-index/price-indexing.md), che fornisce aggiornamenti più veloci sulle modifiche dei prezzi e tempi di sincronizzazione.

### Supporto B2B {#b2bsupport}

I punti vendita B2B spesso richiedono una logica complessa che determina la visibilità dei prodotti e i prezzi per ogni acquirente o gruppo di clienti. [!DNL Product Recommendations] ora [supporta](release-notes.md) questa funzionalità rispettando [le autorizzazioni categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html), [i cataloghi condivisi](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) e [i prezzi specifici del gruppo di clienti](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html). Ad esempio, se hai nascosto alcune categorie dal segmento dei clienti al dettaglio, a un acquirente in quel segmento non verranno mostrati i consigli per i prodotti in quelle categorie. Inoltre, quando definisci un catalogo condiviso per gruppi di clienti e aziende specifici, questi acquirenti visualizzano i consigli solo per i prodotti a cui possono accedere. Tutti i prodotti consigliati riflettono il prezzo corretto specifico per il gruppo di clienti in base al gruppo di clienti di ciascun acquirente.

>[!NOTE]
>
>I commercianti possono personalizzare ed estendere widget o elementi della vetrina utilizzando l&#39;API [Catalog Service](../catalog-service/overview.md) della vetrina, ma qualsiasi personalizzazione esula dall&#39;ambito del team di supporto di Adobe.
