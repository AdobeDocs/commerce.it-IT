---
title: Governance del Centro informazioni Commerce
description: Scopri il modello di governance interna per il Centro informazioni di Commerce. Non pubblicato in Experience League.
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%
---

# Governance del Centro informazioni Commerce

Questo riferimento interno per il team di documentazione non è elencato in `TOC.md`, pertanto non è pubblicato in Adobe Experience League.

## Proprietà

Il team di documentazione di Adobe Commerce è il proprietario del Centro informazioni. È stato creato in `Adobe-Enterprise-Docs/commerce.en`, il repository elencato come `git-repo` in `metadata.md`.

Non è di proprietà di un singolo team di prodotto, in quanto è tra prodotti diversi. Inoltra le correzioni specifiche per il prodotto al contatto della documentazione del team di prodotto proprietario invece di correggerle qui.

## Contenuto del Centro informazioni

| Appartiene qui | Appartiene all’archivio del prodotto |
| --- | --- |
| Contenuti che riguardano più di un prodotto o servizio, ad esempio indicazioni sulla selezione dei prodotti, percorsi di implementazione per più prodotti, modelli di architettura e white paper | Contenuto per singolo prodotto, ad esempio configurazione dettagliata, riferimento API/CLI/config e risoluzione dei problemi |
| Pagine brevi per la cura dei contenuti che rimandano a documenti di prodotto autorevoli | |

- Se una pagina accumula dettagli su un singolo prodotto, spostala nella guida del prodotto e collegala.
- Il Centro informazioni non consolida né esegue la migrazione della documentazione del prodotto e non documenta le singole caratteristiche del prodotto. Collega a contenuti autorevoli esistenti prima di scrivere qualcosa di nuovo.

## Aggiunta di nuovi contenuti

### Articoli in una sezione esistente

1. Aggiungi il file alla cartella che corrisponde alla sezione.
1. Aggiungi una voce a `TOC.md` in quella sezione.

Non è richiesta alcuna approvazione oltre alla normale revisione PR.

| Sezione sommario | Cartella |
| --- | --- |
| Esplorare piattaforme e servizi Commerce | `portfolio/`, `storefronts/`, `aem-assets/`, `apis/` |
| Introduzione per ruolo | `get-started/` |
| Approfondimenti e guida | `guidance-and-insights/` |
| Architettura | `architecture-options/` |
| Migrazione e adozione | `migration-adoption/` |
| Guide all’implementazione | `implementation-guides/` |

### Articoli di approfondimento e guida

1. Copia `whitepaper-template.md` o `security-guidance-template.md` da `guidance-and-insights/templates/` in `guidance-and-insights/`. I modelli non vengono pubblicati. Per informazioni sull&#39;intero processo di authoring, incluso il ticket di acquisizione COMDOX, vedere [readme.md](guidance-and-insights/readme.md).
1. Elimina i commenti dei segnaposto del modello.
1. Aggiungi una voce `TOC.md` in Approfondimenti e linee guida quando il contenuto è pronto per la pubblicazione.

### Sezioni di primo livello

Un nuovo gruppo di primo livello in `TOC.md` modifica la navigazione della guida, pertanto richiede una revisione IA. Contattare il proprietario di Commerce IA review. Riutilizzare prima una sezione esistente, ad esempio Introduzione al ruolo per contenuto partner o di abilitazione.

### URL pubblicati

Gli URL sono generati dall&#39;ID guida, dagli ID sezione in `TOC.md` (ad esempio, `{#insights-and-guidance}`) e dal nome file. I nomi delle cartelle non vengono visualizzati nell’URL. Assegna un ID univoco a ciascuna sezione e accertati che non vi siano due articoli che risolvono lo stesso URL.

## Frequenza di revisione

- **Basato su eventi**: esaminare le sezioni Esplora piattaforme e servizi Commerce, Introduzione a ruolo, Architettura, Migrazione e adozione e Guide all&#39;implementazione quando un prodotto Commerce viene rinominato, avviato o dichiarato obsoleto o quando cambia la disponibilità. Ad esempio, puoi consultarli se Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer ottengono un’integrazione. Prima queste pagine diventano obsolete.
- **Pianificato**: per rilevare la terminologia obsoleta, il branding o le imprecisioni tecniche, eseguire un controllo automatico del contenuto e rivederlo ogni sei mesi.

## Relazione con la guida/l&#39;atterraggio/

`help/landing/` (&quot;Adobe Commerce Services Guides&quot;) è una guida separata che non fa parte del Centro informazioni. Si concentra su servizi Commerce come Catalog Service, Live Search, Product Recommendations e Payment Services, e il Centro informazioni vi si collega per ulteriori dettagli. Ricompilare o consolidare i due elementi è una decisione di follow-up che questa guida non risolve.
