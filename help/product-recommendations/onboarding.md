---
title: Onboarding
description: Scopri i requisiti e le piattaforme supportate in [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Onboarding

Il processo di onboarding per [!DNL Product Recommendations] richiede l&#39;accesso alla riga di comando del server ed è costituito dai passaggi seguenti. Se non hai familiarità con l’utilizzo della riga di comando, chiedi aiuto a uno sviluppatore o a un integratore di sistemi.

- [Flusso di lavoro di implementazione](implementation-workflow.md)
- [Installazione e configurazione](install-configure.md)
- [Impostazioni](settings.md)
- [Verifica](verify.md)
- [Ambiente di staging](staging-environment.md)

## Requisiti

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
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

I punti vendita B2B spesso richiedono una logica complessa che determina la visibilità dei prodotti e i prezzi per ogni acquirente o gruppo di clienti. [!DNL Product Recommendations] ora [supporta](release-notes.md) questa funzionalità rispettando [le autorizzazioni categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=it), [i cataloghi condivisi](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html?lang=it) e [i prezzi specifici del gruppo di clienti](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=it). Ad esempio, se hai nascosto alcune categorie dal segmento dei clienti al dettaglio, a un acquirente in quel segmento non verranno mostrati i consigli per i prodotti in quelle categorie. Inoltre, quando definisci un catalogo condiviso per gruppi di clienti e aziende specifici, questi acquirenti visualizzano i consigli solo per i prodotti a cui possono accedere. Tutti i prodotti consigliati riflettono il prezzo corretto specifico per il gruppo di clienti in base al gruppo di clienti di ciascun acquirente.

>[!NOTE]
>
>I commercianti possono personalizzare ed estendere widget o elementi della vetrina utilizzando l&#39;API [Catalog Service](../catalog-service/overview.md) della vetrina, ma qualsiasi personalizzazione esula dall&#39;ambito del team di supporto di Adobe.
