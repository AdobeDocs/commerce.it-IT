---
title: Ricerca semantica
description: Abilita la ricerca semantica AI in [!DNL Adobe Commerce Optimizer] da Impostazioni. Non è richiesta alcuna modifica alla configurazione degli attributi o alla vetrina.
role: Admin, User
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# Ricerca semantica

La ricerca semantica utilizza l&#39;intelligenza artificiale per capire cosa significano gli acquirenti, non solo le parole esatte che digitano. Query come &quot;abito per un matrimonio in spiaggia&quot; o &quot;scarpe comode per stare in piedi tutto il giorno&quot; possono restituire prodotti rilevanti anche quando il catalogo non utilizza quelle frasi esatte.

[!DNL Adobe Commerce Optimizer] combina la corrispondenza delle parole chiave e la corrispondenza semantica in un&#39;unica esperienza di ricerca. Non è possibile gestire modalità separate per parole chiave e semantiche nella vetrina. In Amministrazione, passare all&#39;area di lavoro [Impostazioni](../settings.md#advanced-search) per gestire la ricerca semantica e, facoltativamente, ottimizzare i controlli avanzati nella scheda **[!UICONTROL Advanced search]**.

## Vantaggi

- **Meno pagine di ricerca vuote** — Gli acquirenti trovano i prodotti quando il testo non corrisponde esattamente al testo del catalogo.
- **Corrispondenza intento migliore** - Le query naturali e descrittive restituiscono risultati utili.
- **Meno manutenzione sinonimi** — Varianti comuni delle parole (ad esempio, divano e divano) vengono spesso gestite senza elenchi di sinonimi manuali.
- **Nessuna vetrina o lavoro per sviluppatori**. La ricerca semantica è abilitata per impostazione predefinita e non richiede modifiche al codice del tema, all&#39;elenco a discesa o all&#39;API.

## Come funziona

Quando la ricerca semantica è abilitata, [!DNL Adobe Commerce Optimizer] utilizza attributi di catalogo predefiniti scelti dal sistema (ad esempio il nome e la descrizione del prodotto) per interpretare il significato della query insieme alla ricerca tradizionale per parole chiave. Non selezionare o assegnare la priorità agli attributi nell’amministratore.

Ad esempio:

- Una ricerca per &quot;divano in pelle&quot; può restituire prodotti etichettati &quot;divano in pelle&quot;.
- &quot;Spring dress&quot; può far emergere gli abiti stagionali anche quando &quot;spring&quot; non è nel nome del prodotto.
- &quot;Scarpe da corsa&quot; può abbinare prodotti descritti come calzature da fuoristrada o da trekking.

## Cosa succede quando si abilita la ricerca semantica

La ricerca semantica funziona insieme alla configurazione di ricerca [!DNL Adobe Commerce Optimizer] esistente. Non si sostituisce la ricerca per parola chiave né si riconfigura la vetrina.

Quando la ricerca semantica è attiva:

- Le [regole di merchandising](../merchandising/rules/overview.md), [sinonimi](../merchandising/synonyms/overview.md), [facet](../merchandising/facets/overview.md), aumenti e filtri esistenti continuano ad essere applicati.
- La ricerca semantica aggiunge una comprensione basata sull’intelligenza artificiale dell’intento del cliente di migliorare la rilevanza dei risultati insieme alla corrispondenza delle parole chiave.
- Gli attributi predefiniti del catalogo vengono indicizzati automaticamente. Non selezionare attributi né pubblicare una configurazione separata.

## Gestire la ricerca semantica nell’amministratore

La ricerca semantica è **abilitata per impostazione predefinita** per i cataloghi inglesi idonei. Vai a **[!UICONTROL Settings]** > **[!UICONTROL Advanced search]** per confermare o modificare l&#39;impostazione:

1. In Admin, vai a **[!UICONTROL Settings]**.
1. Nella scheda **[!UICONTROL Advanced search]**, rivedi **[!UICONTROL Enable semantic search]**.

   Se abilitata, la ricerca associa i prodotti in base al significato e al contesto, producendo risultati più rilevanti, meno pagine di ricerca vuote e una conversione migliore.

1. Fare clic su **[!UICONTROL Save]** se si modificano i controlli di attivazione/disattivazione.

   I risultati della ricerca vengono aggiornati al termine dell’indicizzazione. Per un catalogo di medie dimensioni, l’indicizzazione può richiedere fino a mezz’ora. Per cataloghi di grandi dimensioni con milioni di prodotti, può richiedere alcune ore.

>[!NOTE]
>
> La ricerca semantica è disponibile solo per **cataloghi inglesi**. Se si modifica **[!UICONTROL Language]** in un catalogo non inglese, **[!UICONTROL Enable semantic search]** viene disabilitato automaticamente.

Non è necessario pubblicare una configurazione separata o modificare le impostazioni della vetrina dopo il salvataggio.

## Convalida dopo l’abilitazione

Al termine dell’indicizzazione e dopo l’attivazione della ricerca semantica, Adobe consiglia di convalidare le prestazioni della ricerca. Utilizza la pagina [Prestazioni di ricerca](../manage-results/search-performance.md) per rivedere le metriche e testare le query importanti per la tua azienda.

1. Controlla i termini più cercati nel rapporto **Ricerche univoche**.
1. Verifica le query a zero risultati cronologiche dal report **Zero results** nella vetrina.
1. Confronta i risultati della ricerca per le stesse query prima e dopo l’abilitazione.
1. Monitora la conversione della ricerca e le metriche di coinvolgimento, tra cui il tasso di click-through, il tasso di conversione e il tasso di zero risultati.

## Sintonizzazione opzionale

Nella scheda **[!UICONTROL Advanced search]** è possibile modificare il funzionamento della ricerca dopo l&#39;attivazione della ricerca semantica:

- **[!UICONTROL Semantic boost]** - Aumenta o diminuisce il livello di influenza delle corrispondenze basate sul significato sulla classificazione. Ad esempio, supponiamo che una corrispondenza del prodotto recuperata tramite la ricerca semantica venga visualizzata alla fine del risultato. L’aggiunta di una spinta la porta più in alto nel risultato.
- **[!UICONTROL Similarity threshold]** — Impostare la distanza di una corrispondenza prima che venga visualizzato un prodotto. I valori più bassi mostrano più risultati; i valori più alti mostrano meno corrispondenze.
- **[!UICONTROL Fuzzy search]** e **[!UICONTROL Fuzzy search similarity threshold]** - Aiutano gli acquirenti a trovare i prodotti quando le query includono piccole differenze ortografiche.

Consulta [Ricerca avanzata](../settings.md#advanced-search) per le descrizioni dei controlli e le istruzioni dettagliate.

## Best practice

- Utilizza nomi e descrizioni di prodotti chiari e descrittivi (idealmente 50-100 parole) in modo che sia la corrispondenza semantica che quella delle parole chiave abbiano un testo di catalogo forte con cui lavorare.
- Inizia con l&#39;impostazione predefinita **[!UICONTROL Enable semantic search]**, quindi regola **[!UICONTROL Semantic boost]** o **[!UICONTROL Similarity threshold]** solo se i risultati si sentono troppo ampi o troppo stretti.
- Mantieni [sinonimi](../merchandising/synonyms/overview.md) specifici del brand o altamente tecnici, in cui la ricerca semantica potrebbe non includere termini specializzati.

## Risoluzione dei problemi

| Problema | Cosa fare |
| --- | --- |
| Nessuna modifica nella vetrina subito dopo il salvataggio | Attendere il completamento dell&#39;indicizzazione. I cataloghi di grandi dimensioni possono richiedere più tempo. |
| I risultati sono troppo ampi | Alzare **[!UICONTROL Similarity threshold]** o **[!UICONTROL Semantic boost]** nella scheda **[!UICONTROL Advanced search]**. |
| I risultati sembrano troppo stretti | Abbassa **[!UICONTROL Similarity threshold]** o aumenta **[!UICONTROL Semantic boost]**. |
| Ricerca semantica non disponibile | Conferma **[!UICONTROL Language]** è impostato su **Inglese**. |

## Limitazioni {#semantic-search-limitations}

- **Lingua del catalogo:** La ricerca semantica è disponibile solo per **cataloghi in lingua inglese**.

## Ulteriori informazioni su questo argomento

- [Ricerca avanzata](../settings.md#advanced-search)
- [Sinonimi](../merchandising/synonyms/overview.md)
- [Prestazioni di ricerca](../manage-results/search-performance.md)
