---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---
La ricerca semantica utilizza l&#39;intelligenza artificiale per capire cosa significano gli acquirenti, non solo le parole esatte che digitano. Query come &quot;abito per un matrimonio in spiaggia&quot; o &quot;scarpe comode per stare in piedi tutto il giorno&quot; possono restituire prodotti rilevanti anche quando il catalogo non utilizza quelle frasi esatte.

Il sistema di individuazione dei prodotti combina la corrispondenza delle parole chiave e la corrispondenza semantica in un’unica esperienza di ricerca. Non è possibile gestire modalità separate per parole chiave e semantiche nella vetrina.

## Configurare la ricerca semantica

La ricerca semantica è **abilitata per impostazione predefinita** per i cataloghi inglesi idonei. Puoi gestirlo nella scheda **[!UICONTROL Advanced search]** dell&#39;area di lavoro [Impostazioni](../settings.md#advanced-search), in cui puoi confermare o modificare l&#39;impostazione e, facoltativamente, regolare l&#39;incremento semantico, la soglia di somiglianza e la ricerca fuzzy. Consulta [Impostazioni](../settings.md#access-the-settings-workspace) per informazioni su come aprire l&#39;area di lavoro.

Non è necessario pubblicare una configurazione separata o modificare le impostazioni della vetrina dopo il salvataggio.

## Vantaggi

- **Meno pagine di ricerca vuote** - Gli acquirenti trovano i prodotti quando il testo non corrisponde esattamente al testo del catalogo.
- **Corrispondenza intento migliore**: le query naturali e descrittive restituiscono risultati utili.
- **Meno manutenzione sinonimi**—Varianti comuni delle parole (ad esempio, divano e divano) vengono spesso gestite senza elenchi di sinonimi manuali.
- **Nessuna vetrina o lavoro per sviluppatori**. La ricerca semantica è abilitata per impostazione predefinita e non richiede modifiche al codice del tema, all&#39;elenco a discesa o all&#39;API.

## Come funziona

Quando la ricerca semantica è abilitata, il sistema utilizza attributi di catalogo predefiniti (come il nome e la descrizione del prodotto) per interpretare il significato della query insieme alla ricerca tradizionale per parole chiave. Non selezioni o stabilisci la priorità degli attributi nelle Impostazioni.

Ad esempio:

- Una ricerca per &quot;divano in pelle&quot; può restituire prodotti etichettati &quot;divano in pelle&quot;.
- &quot;Spring dress&quot; può far emergere gli abiti stagionali anche quando &quot;spring&quot; non è nel nome del prodotto.
- &quot;Scarpe da corsa&quot; può abbinare prodotti descritti come calzature da fuoristrada o da trekking.

## Cosa succede quando si abilita la ricerca semantica

La ricerca semantica funziona insieme alla configurazione di ricerca esistente. Non si sostituisce la ricerca per parola chiave né si riconfigura la vetrina.

Quando la ricerca semantica è attiva:

- Le [regole di merchandising](../merchandising/rules/overview.md), [sinonimi](../merchandising/synonyms/overview.md), [facet](../merchandising/facets/overview.md), aumenti e filtri esistenti continuano ad essere applicati.
- La ricerca semantica aggiunge una comprensione basata sull’intelligenza artificiale dell’intento del cliente di migliorare la rilevanza dei risultati insieme alla corrispondenza delle parole chiave.
- Gli attributi predefiniti del catalogo vengono indicizzati automaticamente. Non selezionare attributi né pubblicare una configurazione separata.

## Convalida dopo l’abilitazione

Al termine dell’indicizzazione e dopo l’attivazione della ricerca semantica, Adobe consiglia di convalidare le prestazioni della ricerca. Utilizza la pagina [Prestazioni di ricerca](../manage-results/search-performance.md) per rivedere le metriche e testare le query importanti per la tua azienda.

1. Controlla i termini più cercati nel rapporto **Ricerche univoche**.
1. Verifica le query a zero risultati cronologiche dal report **Zero results** nella vetrina.
1. Confronta i risultati della ricerca per le stesse query prima e dopo l’abilitazione.
1. Monitora la conversione della ricerca e le metriche di coinvolgimento, tra cui il tasso di click-through, il tasso di conversione e il tasso di zero risultati.

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
