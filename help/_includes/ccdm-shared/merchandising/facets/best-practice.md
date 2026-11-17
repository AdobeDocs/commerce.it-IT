---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.it-IT/blob/main/help/_includes/ccdm-shared/merchandising/facets/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Best practice per i facet

La funzionalità di filtro e sfaccettatura è un componente fondamentale delle esperienze Commerce, progettata per migliorare l’esperienza dell’acquirente consentendo a quest’ultimo di limitare i risultati della ricerca e trovare i prodotti in modo più efficiente. Questa funzionalità consente agli acquirenti di ordinare all’interno di vasti cataloghi di articoli applicando criteri specifici, rendendo il processo di acquisto più veloce, semplice e soddisfacente. Implementando filtri e facet efficaci e facet facet facet, puoi aiutare i clienti a trovare esattamente ciò di cui hanno bisogno in modo rapido ed efficiente, aumentando in ultima analisi i tassi di soddisfazione e di conversione.

## Suggerimenti per ottimizzare i facet

- Determinare gli attributi di prodotto rilevanti, ad esempio titolo, categoria, marchio, fascia di prezzo, colore e dimensione, e impostarli come [facet dinamici](type.md). 
- Imposta e ordina gli attributi del prodotto che sono coerenti all’interno del catalogo e altamente rilevanti per i tuoi prodotti, in modo da migliorare la rilevanza e le funzionalità di filtro per gli acquirenti.
- Assicurati che le etichette dei facet siano facili da comprendere e denominate in modo coerente all’interno del sito. Utilizzare ad esempio `Price Range` anziché `Cost`.
- Evita di sopraffare gli acquirenti limitando il numero di sfaccettature a quelle più importanti. Troppe opzioni possono causare affaticamento decisionale. La configurazione facet supporta fino a 100 attributi configurati come facet e fino a 100 valori per facet. Ulteriori informazioni sulle [limitazioni del facet](/help/optimizer/boundaries-limits.md#product-discovery).
- Consenti agli acquirenti di selezionare più criteri di filtro contemporaneamente per perfezionare i risultati. Ad esempio, consentendo agli acquirenti di selezionare sia il rosso che il blu.
- Visualizza il numero di prodotti disponibili accanto a ogni opzione di sfaccettatura per dare agli acquirenti un&#39;idea dei risultati di ricerca che possono aspettarsi.
- Per mantenere pulita e gestibile l’interfaccia, in particolare sui dispositivi mobili, implementa sezioni facet comprimibili.
- Consenti agli acquirenti di reimpostare i singoli facet o tutti i filtri selezionati per avviare facilmente una nuova ricerca.
- Se disponi di un numero elevato di attributi, puoi combinarli in un singolo meta-attributo. Ad esempio, le scarpe hanno dimensioni numeriche, mentre le magliette hanno generalmente le dimensioni &quot;S/M/L/XL&quot;. Questi due tipi di dimensioni possono essere combinati in un unico attributo ricercabile.
