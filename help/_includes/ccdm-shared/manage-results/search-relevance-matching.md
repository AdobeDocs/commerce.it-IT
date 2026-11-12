---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%
---
>[!IMPORTANT]
>
>La funzionalità seguente è in [versione beta privata](https://experienceleague.adobe.com/it/docs/commerce-operations/release/beta).

I servizi di merchandising con il modello di dati a catalogo componibile (CCDM) classificano i risultati in modo che gli acquirenti possano vedere prima i prodotti più rilevanti. Il servizio incrementa i prodotti il cui testo del catalogo **corrisponde** alla query dell&#39;acquirente, quindi favorisce le corrispondenze in cui i termini vengono visualizzati insieme e infine include corrispondenze più ampie.

## Priorità delle corrispondenze

La rilevanza utilizza tre livelli di forza di corrispondenza (oltre ad altri fattori di valutazione descritti di seguito):

1. **Corrispondenza frase esatta e vicina**: la frase di ricerca completa corrisponde al testo del catalogo o a una corrispondenza vicina dopo la normalizzazione, ad esempio la stemming (i moduli singolari e plurali, ad esempio, si risolvono nella stessa radice). Queste partite ricevono il massimo incremento di rilevanza.

1. **Tutte le parole nello stesso campo**. Ogni parola di query viene visualizzata in un attributo ricercabile, ad esempio `red` e `pants` nel prodotto **name**. Questo livello riceve l&#39;incremento successivo più elevato.

1. **Parole in campi diversi** — I termini di query vengono visualizzati in attributi diversi ricercabili (ad esempio, `red` in **color** e `pants` in **name**). Questo livello di corrispondenza è il più ampio e riceve l’incremento di rilevanza più basso. Può inoltre corrispondere a query parziali utilizzate dal completamento automatico, ad esempio quando un acquirente digita `red pan` prima di terminare `pants`. Per i cataloghi tedeschi, vedere [Decomposizione (tedesco)](#decompounding-german).

### Esempio

Per una query come `red pants`:

- Prodotti con la frase esatta **pantaloni rossi** (o una variante vicina) sono classificati **primi**.
- I prodotti in cui **red** e **pantaloni** compaiono nel **stesso campo** (ad esempio, **name**) sono classificati accanto.
- Seguono i prodotti in cui i termini vengono visualizzati in **campi diversi** (ad esempio, **colore** e **nome**).

### Decomposizione (tedesco) {#decompounding-german}

I cataloghi tedeschi usano molte parole composte. Ad esempio, **spülbecken** e **spül becken** possono decomporsi in token come **spul** e **beck** (dopo la stemming) in modo che un acquirente che cerca **spul becken** possa ancora trovare **Spülbecken**. A questo livello, le parole secondarie decomposte da un termine composto devono comparire nello stesso campo. Altri termini di query possono corrispondere in campi diversi.

Questo requisito **AND** filtra corrispondenze irrilevanti in cui è presente una sola parola secondaria. Ad esempio, la ricerca di **Brauseschlauch** non restituisce più **Schlauchstück** quando solo una parte del composto corrisponde. Una ricerca per **spülbecken** può comunque corrispondere a **spülbeckventil** perché la parola più lunga contiene tutti i token previsti.

>[!NOTE]
>
>La corrispondenza esatta e vicina alle frasi e la corrispondenza dello stesso campo utilizzano le regole descritte sopra senza scomporre.

#### Esempio

Per una frase di ricerca come `Brauseschlauch chrom`:

- **Corrispondenza frase esatta e vicina** - Cerca la frase completa **brauseschlauch chrom** digitata, senza decomporre (la stemming è ancora valida).
- **Tutte le parole nello stesso campo** - Cerca **brauseschlauch** e **chrom** nell&#39;attributo **same** ricercabile, ancora senza decomposizione (ad esempio, entrambi in **name**).
- **Parole in campi diversi** — Decompone **Brauseschlauch** in **brause** e **schlauch**. Tali token devono essere visualizzati nel campo **same** (non necessariamente come frase adiacente). **chrom** può corrispondere in un campo **differente** (ad esempio, **brause** e **schlauch** in **name**, **chrom** in **color**).

Imposta **Lingua** su **Tedesco** nella scheda [Lingua](../settings.md#language) in [Impostazioni](../settings.md) in modo che vengano applicate le regole di decomposizione. Convalida le query tedesche di alto valore in una vetrina prima di abilitare le modifiche nella produzione.

La decomposizione è basata su regole e può aggiungere casi limite a questo livello. Se manca una parola secondaria nel dizionario, la tokenizzazione è incompleta e restituisce corrispondenze più ampie del previsto, ad esempio **gas** mancante da **gaszähler** emette solo **zahl** o **stat** mancante da **thermostat**. Lo stemmer può anche produrre radici impreviste (ad esempio, **schrauber** che deriva da **schraub** o **schelle** a **schell**). Adobe aggiorna il dizionario e le sostituzioni di origine per i casi noti, man mano che vengono identificati dei problemi.

## Cos’altro influisce sulla classificazione

La corrispondenza delle frasi da sola non determina la rilevanza. Diversi segnali interagiscono:

- Incrementa da **esatta / vicino** corrispondenza frase
- Incrementa quando **tutti i termini di query** vengono visualizzati nel campo **same**
- **Classificazione intelligente** (se abilitata), che combina rilevanza testuale e segnali comportamentali. Vedere [Funzionamento del punteggio di classificazione intelligente](../merchandising/rules/add.md#how-intelligent-ranking-scoring-works-search)
- **[Peso della ricerca](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/catalog/search/search-results)** per ogni attributo e altri fattori di rilevanza testuali (ad esempio, la frequenza con cui si verificano i termini nella lunghezza del nome o della descrizione). In *Impostazioni*, configura gli attributi che partecipano alla ricerca per parole chiave e i relativi **[pesi di ricerca per parole chiave](../settings.md)**.
- **[Regole di merchandising](../merchandising/rules/overview.md)** come pin, boost e bury

Poiché i segnali interagiscono, a volte una corrispondenza ampia viene posizionata al di sopra di una corrispondenza di frase più stretta quando **i pesi di ricerca** o la frequenza dei termini superano una corrispondenza di frase più debole.

**Esempio:** se **pantaloni rossi** compaiono in **descrizione** con **peso ricerca = 1**, ma **pantaloni rossi** e **pantaloni** compaiono separatamente in **nome** e **colore** con **peso ricerca = 10**, la corrispondenza divisa supera la corrispondenza della frase.

Le regole manuali **pin** e **bury** rimangono valide; le regole **boost** potrebbero richiedere l&#39;ottimizzazione per superare le nuove estensioni di frasi e campi uguali. Convalida le query importanti dopo la modifica dei pesi o delle regole.

### Peso di ricerca 1 e indicizzazione combinata

Attributi con **peso minimo di ricerca** (peso **1**) e nessuna modalità di corrispondenza speciale si combinano in un unico campo interno (`defaultSearchField`) per ridurre il sovraccarico di mappatura. Considera questa come un&#39;unica superficie ricercabile per la corrispondenza **same-field**: i token che arrivano solo in quei campi a basso peso combinati vengono valutati insieme anziché come campi per attributo separati. Adobe può perfezionare questa ottimizzazione nel tempo man mano che la corrispondenza si evolve.

## Argomenti correlati

- [Impostazioni](../settings.md)
- [Prestazioni di ricerca](search-performance.md)
- [Panoramica sulle regole di merchandising](../merchandising/rules/overview.md)
- [Aggiungi regole di ricerca](../merchandising/rules/add.md)
- [Panoramica dei sinonimi](../merchandising/synonyms/overview.md)
