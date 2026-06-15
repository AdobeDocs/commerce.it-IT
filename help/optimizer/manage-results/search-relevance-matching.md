---
title: Ricerca corrispondenza e classificazione
description: Scopri come [!DNL Adobe Commerce Optimizer] assegna priorità alle corrispondenze esatte e vicine, alle corrispondenze nello stesso campo e alle corrispondenze tra campi, e come la classificazione interagisce con i pesi di ricerca, la classificazione intelligente e le regole di merchandising.
role: Admin, Leader, User
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
hide: true
autotag-review: '2026-06-12T19:49:25.241Z'
TQID: 'https://experienceleague.adobe.com/GBfssL1pTVx4FKjsi45mDsTx2XyCr0aViexH3OpPjVo'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
subfeature_v2: id: faf75e43-5608-48b8-8169-3f8a9b8a5caf
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 717ecbc9c6aa41f8a504579de8ce55f514cc4307
workflow-type: tm+mt
source-wordcount: 946
ht-degree: 0%

---

# Ricerca corrispondenza e classificazione

>[!IMPORTANT]
>
>La funzionalità seguente è in [versione beta privata](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta).

[!DNL Adobe Commerce Optimizer] classifica i risultati in modo che gli acquirenti possano vedere per primi i prodotti più rilevanti. Il servizio fornisce l&#39;impulso più forte ai prodotti il cui testo del catalogo **corrisponde** a quello che l&#39;acquirente digita, quindi favorisce le corrispondenze in cui i termini di query appaiono insieme in modo significativo e infine include corrispondenze più ampie (compreso il comportamento che supporta la corrispondenza in stile di completamento automatico).

## Priorità delle corrispondenze

A un livello elevato, la rilevanza utilizza tre livelli di forza di corrispondenza (oltre ad altri fattori di punteggio descritti di seguito):

1. **Corrispondenza frase esatta e vicina**: la frase di ricerca completa corrisponde al testo del catalogo o a una corrispondenza vicina dopo la normalizzazione, ad esempio la stemming (i moduli singolari e plurali, ad esempio, si risolvono nella stessa radice). Queste partite ricevono il massimo incremento di rilevanza.

1. **Tutte le parole nello stesso campo**. Ogni parola nella query viene visualizzata in un unico attributo ricercabile, ad esempio `red` e `pants` nel prodotto **name**. Questo livello riceve l&#39;incremento successivo più elevato.

1. **Parole in campi diversi** — I termini di query vengono visualizzati in attributi diversi ricercabili (ad esempio, `red` in **color** e `pants` in **name**). Si tratta del livello di corrispondenza più ampio e riceve l’incremento di rilevanza più basso. Può inoltre corrispondere a query parziali utilizzate dal completamento automatico, ad esempio quando un acquirente digita `red pan` prima di terminare `pants`. Per i cataloghi tedeschi, vedere [Decomposizione (tedesco)](#decompounding-german).

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

La decomposizione è basata su regole e può aggiungere casi limite a questo livello. Se manca una parola secondaria nel dizionario, la tokenizzazione può essere incompleta e restituire corrispondenze più ampie di quanto previsto. Ad esempio, **gas** mancante da **gaszähler** potrebbe emettere solo **zahl** o **stat** mancante da **termostato**. Lo stemmer può anche produrre radici impreviste (ad esempio, **schrauber** che deriva da **schraub** o **schelle** a **schell**). Adobe aggiorna il dizionario e le sostituzioni di origine per i casi noti, man mano che vengono identificati dei problemi.

## Cos’altro influisce sulla classificazione

La rilevanza non è determinata solo dalla corrispondenza delle frasi. Diversi segnali interagiscono:

- Incrementa da **esatta / vicino** corrispondenza frase
- Incrementa quando **tutti i termini di query** vengono visualizzati nel campo **same**
- **Classificazione intelligente** (se abilitata), che combina rilevanza testuale e segnali comportamentali. Vedere [Funzionamento del punteggio di classificazione intelligente](../merchandising/rules/add.md#how-intelligent-ranking-scoring-works-search)
- **[Peso della ricerca](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)** per ogni attributo e altri fattori di rilevanza testuali (ad esempio, la frequenza con cui si verificano i termini e la lunghezza del nome o della descrizione). In *Impostazioni*, configura gli attributi che partecipano alla ricerca per parole chiave e i relativi **[pesi di ricerca per parole chiave](../settings.md)**.
- **[Regole di merchandising](../merchandising/rules/overview.md)** come pin, boost e bury

Poiché questi segnali interagiscono, un prodotto che corrisponde solo al livello più ampio può talvolta essere classificato al di sopra di una corrispondenza di frase più stretta, ad esempio quando **i pesi di ricerca** o la frequenza del termine in un campo di peso elevato superano una corrispondenza di frase più debole in un altro punto.

**Esempio:** se **pantaloni rossi** compare come frase in **descrizione** con **peso ricerca = 1**, ma **rosso** e **pantaloni** compaiono separatamente in **nome** e **colore** con **peso ricerca = 10**, la corrispondenza della frase in **descrizione** potrebbe non essere superiore alla corrispondenza di divisione, a seconda del punteggio complessivo.

Le regole manuali **pin** e **bury** rimangono valide; le regole **boost** potrebbero richiedere l&#39;ottimizzazione per superare le nuove estensioni di frasi e campi uguali. Convalida le query importanti dopo la modifica dei pesi o delle regole.

### Peso di ricerca 1 e indicizzazione combinata

Gli attributi configurati con il **peso minimo di ricerca** (peso **1**) e **non** configurati per modalità di corrispondenza speciali (come contains o starts-with) possono essere combinati nell&#39;indice di ricerca in un singolo campo interno (`defaultSearchField`) per ridurre il sovraccarico di mappatura dei campi. Considera questa come un&#39;unica superficie ricercabile per la corrispondenza **same-field**: i token che arrivano solo in quei campi a basso peso combinati vengono valutati insieme anziché come campi per attributo separati. Adobe può perfezionare questa ottimizzazione nel tempo man mano che la corrispondenza si evolve.

## Argomenti correlati

- [Impostazioni](../settings.md)
- [Prestazioni di ricerca](search-performance.md)
- [Panoramica sulle regole di merchandising](../merchandising/rules/overview.md)
- [Aggiungi regole di ricerca](../merchandising/rules/add.md)
- [Panoramica dei sinonimi](../merchandising/synonyms/overview.md)
