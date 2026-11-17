---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.it-IT/blob/main/help/_includes/ccdm-shared/merchandising/overview.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Adobe Merchandising

Scopri come creare esperienze personalizzate per gli acquirenti attraverso l’individuazione dei prodotti e la generazione di consigli.

Questi servizi Adobe Merchandising sono basati sul modello dati del catalogo componibile (CCDM), che separa *dati prodotto* dal *contesto prodotto*. I dati dei prodotti includono SKU, attributi, metadati, risorse e prezzi. Il contesto di prodotto definisce il modo in cui vengono consegnati i dati, incluse [visualizzazioni catalogo](/help/optimizer/setup/catalog-view.md), [criteri di accesso ai dati](/help/optimizer/setup/policies.md) e [origini catalogo](/help/optimizer/setup/catalog-sources.md) (impostazioni internazionali). Poiché le visualizzazioni e i criteri del catalogo controllano i dati della vetrina, puoi comporre cataloghi personalizzati per modelli B2B, B2C e D2C e personalizzare le esperienze di acquisto senza duplicare i dati di base.

- **Individuazione del prodotto**: offre ai commercianti strumenti potenti per curare e ottimizzare l&#39;esperienza di acquisto, garantendo che i clienti trovino rapidamente i prodotti giusti al momento giusto. Regolando il comportamento di ricerca, puoi influenzare direttamente la visibilità, la rilevanza e la conversione dei prodotti.

  Con l’individuazione dei prodotti, puoi indirizzare gli acquirenti verso i prodotti più rilevanti con il minimo attrito configurando:

  - [**Regole di merchandising**](rules/overview.md): incrementa, sotterrare, fissare o filtrare i prodotti nei risultati di ricerca, negli elenchi di prodotti predefiniti e nelle pagine delle categorie.
  - [**Facet**](facets/overview.md) - Configura i filtri utilizzati dagli acquirenti per limitare i risultati di ricerca e categoria.
  - [**Sinonimi**](synonyms/overview.md): mappa termini equivalenti in modo che parole di ricerca diverse restituiscano gli stessi prodotti.

  La ricerca semantica, attivata per impostazione predefinita in [Impostazioni](../settings.md), migliora la rilevanza per le query basate su linguaggio naturale e intento. In Impostazioni puoi anche configurare i facet di prezzo, la lingua del catalogo e le opzioni di ricerca semantica e sfocata avanzate.

- [**Consigli**](recommendations/overview.md): utilizza algoritmi di intelligenza artificiale e machine learning per analizzare il comportamento aggregato dei visitatori e le interazioni dei prodotti nella vetrina. Insieme al tuo catalogo, questi dati offrono esperienze altamente coinvolgenti, pertinenti e personalizzate. I consigli vengono visualizzati nella vetrina come unità con etichette, ad esempio &quot;Hanno visto anche i clienti che hanno visualizzato questo prodotto&quot;. Puoi creare, gestire e distribuire i consigli direttamente dall’area di lavoro Consigli e distribuirli in tutto il percorso per supportare obiettivi promozionali, strategie di cross-selling ed esperienze personalizzate.
