---
title: Sviluppo per amministratori di Product Recommendations
description: Panoramica dell’architettura e delle funzioni di sviluppo di Product Recommendations.
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
TQID: https://experienceleague.adobe.com/DtPYY7DaB-A7-VyTeXkjL9Y2My-WOQx-9CD-TgrcTmk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 319
ht-degree: 0%

---

# Sviluppo per amministratori di Product Recommendations

I consigli di prodotto sono un potente strumento di marketing che puoi utilizzare per aumentare le conversioni, incrementare i ricavi e stimolare il coinvolgimento degli acquirenti. I consigli di prodotto vengono visualizzati nella vetrina sotto forma di unità quali &quot;Hanno visualizzato anche i clienti che hanno acquistato questo prodotto&quot;, &quot;Hanno acquistato anche questo prodotto&quot;, &quot;Sono consigliati per te&quot; e così via. I consigli di prodotto di Adobe Commerce sono basati su [Adobe AI](https://business.adobe.com/ai.html), che utilizza algoritmi di intelligenza artificiale e machine learning per eseguire un&#39;analisi approfondita dei dati aggregati degli acquirenti. Quando vengono combinati con il catalogo Commerce, questi dati offrono esperienze altamente coinvolgenti, pertinenti e personalizzate per l’acquirente.

>[!NOTE]
>
>Se la vetrina è implementata tramite PWA Studio, consulta la [documentazione di PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se utilizzi una tecnologia front-end personalizzata come React o Vue JS, consulta la guida utente per scoprire come integrare Consigli di prodotto in un ambiente [headless](headless.md). Le istanze headless devono implementare l’evento per alimentare l’area di lavoro Product Recommendation.

## Panoramica dell’architettura

Ad alto livello, i consigli di prodotto Commerce vengono distribuiti come SaaS. Il lato Commerce include la vetrina, che contiene l’agente di raccolta eventi e il modello di layout dei consigli, e il back-end, che include i servizi dati, il modulo Esportazione SaaS e l’interfaccia utente amministratore. I servizi di intelligence di Adobe AI sono utilizzati lato SaaS.

![Diagramma dell&#39;architettura dei consigli di prodotto](assets/arch-diag-sensei.svg)

Una volta installati e configurati i moduli di consigli, la vetrina inizierà a raccogliere i dati comportamentali. Adobe AI elabora questi dati comportamentali insieme ai dati del catalogo e calcola le associazioni di prodotti utilizzate dal servizio Recommendations. A questo punto, il commerciante può creare, gestire e distribuire unità di consigli di prodotto nella vetrina direttamente dall’interfaccia utente di amministrazione.

## Passaggi successivi

Leggi i seguenti argomenti per iniziare a utilizzare i consigli di prodotto:

- [Come implementare la funzione Consigli di prodotto](implementation-workflow.md)

- [Installare e configurare Product Recommendations](install-configure.md)

- [Creare consigli di prodotto](create.md)
