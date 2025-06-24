---
title: Best practice per i facet
description: Scopri le best practice per l’implementazione dei facet nel tuo store.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Best practice per i facet

Le funzionalità di filtro e facet sono un componente fondamentale del sito [!DNL Adobe Commerce Optimizer], progettato per migliorare l&#39;esperienza dell&#39;acquirente consentendo agli acquirenti di limitare i risultati di ricerca e trovare i prodotti in modo più efficiente. Questa funzionalità consente agli acquirenti di ordinare all’interno di vasti cataloghi di articoli applicando criteri specifici, rendendo il processo di acquisto più veloce, semplice e soddisfacente. Implementando filtri e facet efficaci e facet facet facet, puoi aiutare i clienti a trovare esattamente ciò di cui hanno bisogno in modo rapido ed efficiente, aumentando in ultima analisi i tassi di soddisfazione e di conversione.

## Suggerimenti per ottimizzare i facet

- Determina gli attributi più rilevanti e utili per i tuoi prodotti, ad esempio titolo, categoria, marchio, fascia di prezzo, colore e dimensione e impostali come [facet dinamici](type.md). 
- Imposta e ordina gli attributi del prodotto che sono coerenti all’interno del catalogo e altamente rilevanti per i tuoi prodotti, in modo da migliorare la rilevanza e le funzionalità di filtro per gli acquirenti.
- Assicurati che le etichette dei facet siano facili da comprendere e denominate in modo coerente all’interno del sito. Ad esempio, utilizza &quot;Fascia di prezzo&quot; invece di &quot;Costo&quot;.
- Evita di sopraffare gli acquirenti limitando il numero di sfaccettature a quelle più importanti. Troppe opzioni possono causare affaticamento decisionale. Per impostazione predefinita, [!DNL Adobe Commerce Optimizer] è limitato a un massimo di 100 attributi configurati come facet e 30 bucket restituiti all&#39;interno di ogni facet. Ulteriori informazioni sulle [limitazioni del facet](../../boundaries-limits.md#catalog-views-and-policies). 
- Consenti agli acquirenti di selezionare più criteri di filtro contemporaneamente per perfezionare i risultati. Ad esempio, consentendo agli acquirenti di selezionare sia il rosso che il blu.
- Visualizza il numero di prodotti disponibili accanto a ogni opzione di sfaccettatura per dare agli acquirenti un&#39;idea dei risultati di ricerca che possono aspettarsi.
- Implementa sezioni facet comprimibili per mantenere l’interfaccia pulita e gestibile, soprattutto sui dispositivi mobili.
- Consenti agli acquirenti di reimpostare facilmente singoli facet o tutti i filtri selezionati per avviare una nuova ricerca.
- Se hai a che fare con un numero elevato di attributi, puoi combinarli in un singolo &quot;meta-attribute&quot;. Ad esempio, le scarpe hanno generalmente dimensioni numeriche, mentre le magliette hanno generalmente le dimensioni &quot;S/M/L/XL&quot;. Questi due tipi di dimensioni possono essere combinati in un unico attributo ricercabile.
