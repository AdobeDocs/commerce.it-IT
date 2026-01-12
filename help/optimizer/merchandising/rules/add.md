---
title: Creare e gestire le regole
description: Scopri come creare e gestire le regole di merchandising.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: fd4df2b2-83de-4c5c-b18c-e97aa07ef8f6
source-git-commit: bd54ff7afb0b6a5d78098225a8f98f81f96a7923
workflow-type: tm+mt
source-wordcount: '2146'
ht-degree: 0%

---

# Creare e gestire le regole

Per creare una regola, il primo passaggio consiste nell’utilizzare l’editor di regole per definire, nel testo della query dell’acquirente, le condizioni che attivano gli eventi associati. Quindi, completa i dettagli della regola, verifica i risultati e pubblica la regola.

## Creare una regola

1. Nella barra a sinistra, passa a _Merchandising_ > **Regole di merchandising**.
1. Fai clic su **Crea regola** per avviare l&#39;editor di regole.

![Crea regola](../../assets/create-rule.png)

Nella sezione **Generare la regola** è possibile definire criteri di ricerca, condizioni e tipi di classificazione specifici.

1. Nel campo **[!UICONTROL Name]** immettere un nome per la regola. Tutti i nomi delle regole devono essere univoci.
1. Nel campo **[!UICONTROL Description]** immettere una descrizione per la regola.
1. Nel campo **[!UICONTROL Date range]** specificare la data o l&#39;intervallo di date in cui si desidera attivare la regola.
1. Nella sezione **[!UICONTROL Rule applies to]** sono disponibili due opzioni: **[!UICONTROL All product listings]** o **[!UICONTROL Specific conditions]**.

   - **Tutti gli elenchi di prodotti** - Si tratta essenzialmente della regola predefinita e viene applicata a tutte le query di ricerca, a meno che non venga definita una query di ricerca più specifica. È possibile creare una sola regola predefinita che non può contenere condizioni. Scegli il tipo di classificazione intelligente ed eventuali classificazioni manuali da applicare a tutte le ricerche predefinite.
   - **Condizioni specifiche** - Consulta la sezione successiva per informazioni sui tipi di condizioni che puoi impostare per la regola.

### Condizioni

Le condizioni sono i requisiti per attivare un evento. Una regola può avere fino a dieci condizioni e 25 eventi. Una regola predefinita non può avere condizioni.

![Seleziona condizione regola](../../assets/rule-set-condition.png)

#### Condizione singola

1. In *Genera la regola*, seleziona la **Condizione** da soddisfare e segui le istruzioni per completare l&#39;istruzione.

   - Query di ricerca contiene: immettere la stringa di testo che deve essere inclusa nella query dell&#39;acquirente. L&#39;impostazione Corrispondenza determina il grado di corrispondenza tra la query dell&#39;acquirente e il catalogo. Opzioni:<br /> Qualsiasi - Qualsiasi parte del testo della query dell&#39;acquirente può corrispondere alla condizione.<br />Tutti - Tutte le query dell&#39;acquirente devono corrispondere alla condizione.
   - Query di ricerca: immetti una stringa di testo che corrisponda esattamente alla query dell’acquirente. Ad esempio: &quot;pantaloni da yoga&quot;. Le regole con `Search query is` e la corrispondenza `All` possono avere una sola condizione.
   - La query di ricerca inizia con - Inserisci un carattere o una stringa di testo che deve trovarsi all’inizio della query dell’acquirente.
   - La query di ricerca termina con - Immetti un carattere o una stringa di testo che deve trovarsi alla fine della query dell’acquirente.

   I risultati vengono visualizzati immediatamente nel riquadro *Verifica regola* e sono numerati per priorità. Puoi utilizzare il cursore *Risultati per riga* in alto a destra per modificare il numero di prodotti in ogni riga.

1. Per verificare altre query, modifica il testo della query nella casella di ricerca *Verifica la regola* e premi **Invio**.
Inizialmente, il riquadro dei test esegue il rendering della query dalla casella di ricerca Condizioni. Ma ora sta eseguendo il rendering della query dalla casella di query del test. Nel riquadro dei test viene eseguita una sola query alla volta.
1. Se il risultato ti piace, aggiorna il testo nella casella di ricerca *Condizioni*. Quindi, fai clic in un punto qualsiasi della pagina per aggiornare i risultati nel riquadro del test.

#### Condizioni multiple

1. Per creare una regola con più condizioni, fare clic su **Aggiungi condizione**.
Una regola può avere fino a dieci condizioni. L&#39;operatore logico che unisce due condizioni si basa sull&#39;impostazione *Match* corrente. Per impostazione predefinita, *Match* è `All` e l&#39;operatore logico è `AND`.

1. Seleziona la seconda condizione e immetti il testo della query richiesto.

1. Per modificare la logica della regola, modifica l&#39;impostazione **Corrispondenza** per determinare la corrispondenza tra i criteri di ricerca dell&#39;acquirente e la condizione della query. Imposta **Corrispondenza** su uno dei seguenti elementi:

   - Qualsiasi - (impostazione predefinita) Tutti gli operatori logici nella regola sono impostati su `OR` e i risultati vengono visualizzati nel riquadro dei test.
   - Tutti: tutti gli operatori logici nella regola sono impostati su `AND` e i risultati vengono visualizzati nel riquadro dei test.

   Il valore *Match* determina l&#39;operatore logico utilizzato per unire più condizioni. La modifica dell&#39;impostazione *Match* comporta la modifica di tutti gli operatori logici nella regola. Impossibile combinare `AND` e `OR` nella stessa regola.

   In questo esempio, invece di cercare &quot;pantaloni yoga&quot;, ci sono due query separate che cercano &quot;yoga&quot; o &quot;pantaloni&quot;. Questa regola è meno specifica e viene attivata più spesso nella vetrina rispetto alle altre.

1. Per aggiungere un&#39;altra condizione, fare clic su **Aggiungi condizione** e ripetere il processo.

### Classificazione intelligente

La classificazione intelligente combina i comportamenti degli utenti e le statistiche del sito per determinare la classificazione del prodotto.
I proprietari dei negozi possono impostare i seguenti tipi di strategie di classificazione:

![Classificazioni intelligenti](../../assets/rule-intelligent-ranking.png)

- Più acquistati: classifica i prodotti in base agli acquisti totali per SKU nei 7 giorni precedenti.
- La maggior parte è stata aggiunta al carrello, in ordine di attività totali &quot;Aggiungi al carrello&quot; nei 7 giorni precedenti.
- Più visualizzati: classifica le visualizzazioni totali per SKU nei 7 giorni precedenti.
- Consigliato per te - Utilizza il punto dati `viewed-viewed` - Gli acquirenti che hanno visualizzato questo SKU hanno esaminato anche questi altri SKU.
- Tendenza: considera gli eventi di visualizzazione della pagina delle ultime 72 ore per gli eventi in background e 24 ore per gli eventi in primo piano.
- Nessuno: i prodotti vengono ordinati in base alla rilevanza.

Selezionare il tipo di strategia per la regola. Nella finestra **Verifica regola** vengono visualizzati i risultati previsti.

#### Come funziona il punteggio di classificazione intelligente

La classificazione intelligente determina l&#39;ordine finale del prodotto combinando due fattori chiave: **rilevanza testuale** e **segnali comportamentali**. Comprendere come questi fattori interagiscono consente di impostare aspettative realistiche per i risultati della ricerca.

**Componenti punteggio:**

- **Rilevanza testuale**: il fattore dominante nel punteggio. Questo misura se il nome, la descrizione e gli attributi di un prodotto corrispondono alla query di ricerca. Il punteggio di rilevanza del testo è illimitato (non ha un limite superiore specifico) ed è influenzato da fattori come:

   - Frequenza di occorrenza delle parole corrispondenti.
   - Lunghezza (in lettere) dei nomi/delle descrizioni dei prodotti.

- **Segnali comportamentali**: aumento limitato applicato al punteggio di rilevanza del testo. Quando selezioni una strategia di classificazione intelligente come &quot;Più visualizzati&quot; o &quot;Più acquistati&quot;, i prodotti con segnali comportamentali più elevati ricevono un incremento fisso dei punteggi. Tuttavia, questo incremento ha un limite definito.

**Perché il prodotto più visualizzato potrebbe non essere visualizzato per primo:**

La rilevanza testuale in genere domina la classificazione perché il suo punteggio è illimitato, mentre gli aumenti comportamentali sono fissi. Di conseguenza, i prodotti con corrispondenze testuali forti spesso superano quelli con segnali di coinvolgimento più elevati. Gli aumenti comportamentali da soli possono non compensare le grandi lacune nella rilevanza del testo. La classificazione intelligente affronta questo problema prendendo in considerazione sia la qualità della corrispondenza che l’interazione con l’acquirente, migliorando la rilevanza complessiva. Tuttavia, la qualità della corrispondenza del testo rimane il principale driver di classificazione.

**Esempio:**

Un commerciante utilizza la strategia di classificazione intelligente &quot;Più visualizzato&quot; e cerca &quot;candela&quot;. Si aspettano che lo SKU del prodotto YAN-K-E-512 appaia all’inizio dei risultati perché ha il conteggio di visualizzazioni più alto. Tuttavia, altri prodotti sono classificati più in alto:

- **Candela Texas** (prima posizione): ha un nome di prodotto più breve e più chiaro che crea un punteggio di rilevanza del testo molto elevato. Anche se ha meno visualizzazioni di YAN-K-E-512, la sua corrispondenza testuale superiore supera l&#39;incremento comportamentale.

- **YAN-K-E-512** (posizione più bassa): nonostante il percentile di visualizzazione più alto nei dati comportamentali &quot;Più visualizzati&quot;, il nome complesso basato su SKU genera un punteggio di rilevanza del testo più basso. L’impulso comportamentale fisso non è sufficiente per superare questo vuoto di rilevanza del testo.

Consulta [regole di ricerca](./best-practice.md#tips-to-optimize-search-rules) per scoprire come migliorare la reperibilità dei prodotti utilizzando le regole.

#### Avvertenze

- Gli apostrofi e le citazioni nelle interrogazioni possono portare ad alcuni problemi minori di classificazione e rilevanza in alcune lingue.
- Per garantire il corretto funzionamento della classificazione intelligente, assicurati che il **Peso di ricerca** per tutti gli attributi utilizzati per la ricerca o il filtraggio (facet) sia pari o inferiore a `5`.

Per informazioni sull&#39;impostazione dei pesi di ricerca, vedere [API metadati](https://developer.adobe.com/commerce/services/reference/rest/).

### Classificazione manuale

**Classificazione manuale** sono azioni che modificano i risultati della ricerca quando vengono soddisfatte le condizioni definite. Una singola regola può avere fino a 25 eventi.

- Incrementa: sposta un prodotto più in alto nei risultati di ricerca.
- Intervallo: sposta una SKU in basso nei risultati di ricerca.
- Fissa un prodotto: il prodotto viene visualizzato nella posizione selezionata sulla pagina.
- Nascondi un prodotto: esclude uno SKU dai risultati della ricerca.

Il modo più semplice per fissare un prodotto è tramite trascinamento.

1. Fai clic su un prodotto e trascinalo nel riquadro Test. Trascinalo e rilascialo nella posizione desiderata. I campi Prodotto e Posizione vengono compilati automaticamente nel riquadro Eventi.

Puoi anche fare clic sull’icona a forma di pin per fissare un prodotto alla posizione corrente. Utilizza il menu di scelta rapida con puntini di sospensione per &quot;Fissa in alto&quot; o &quot;Fissa in basso&quot;.

>[!NOTE]
>
>Puoi fissare solo i prodotti visualizzati nei risultati della ricerca per le condizioni della query e della regola configurate.
>
>I prodotti devono essere indicizzati, visibili, in magazzino e soddisfare tutti i filtri delle regole per essere idonei al fissaggio. Se un prodotto non viene visualizzato nell’anteprima o nei risultati per la regola, l’operazione di fissaggio non ha alcun effetto.

Gli eventi OR possono essere impostati manualmente:

1. In *Eventi*, scegli l&#39;**Evento** da eseguire quando vengono soddisfatte le condizioni associate.

   Scegliere ad esempio `Hide a product`. Quindi, inserisci il nome del prodotto che desideri nascondere. I prodotti vengono suggeriti durante la digitazione.

1. Per più eventi, scegli qualsiasi altro evento che desideri attivare quando vengono soddisfatte le condizioni.

### Finalizzazione della regola

1. Esaminare i risultati della regola nel riquadro del test.
1. Se la regola dispone di più query, esegui il test di ciascuna che potrebbe essere interessata dalla regola.
1. Al termine, fare clic su **Salva e pubblica**.

   La regola viene aggiunta all&#39;elenco nell&#39;area di lavoro *Rules*.

1. Anche se le regole attive entrano in vigore immediatamente, potrebbe essere necessario attendere fino a 15 minuti prima che i risultati della query memorizzata nella cache vengano aggiornati nella vetrina.

>[!NOTE]
>
>Le regole e i prodotti classificati manualmente vengono applicati ai risultati della ricerca quando viene selezionato il criterio di ordinamento predefinito &quot;Ordina per: Più rilevante&quot;. Se un acquirente modifica il criterio di ordinamento in modo da definirlo in base al nome o al prezzo, le regole e le classificazioni manuali non sono più attive.

## Modificare, visualizzare ed eliminare le regole

Segui queste istruzioni per aggiornare le proprietà delle regole esistenti.

### Modifica regola

1. Nell&#39;area di lavoro *Regole di merchandising*, individua la regola nella griglia che desideri modificare e fai clic su **Altre** (...) opzioni.
1. Fai clic su **Modifica** per accedere all&#39;editor di regole.
1. Aggiorna condizioni, operatori ed eventi in base alle esigenze.
1. Se necessario, aggiorna i campi nome, data di inizio e di fine e descrizione. Tutti i nomi delle regole devono essere univoci.
1. Verifica la regola.
1. Pubblica le modifiche.
La regola viene aggiunta all&#39;elenco nell&#39;area di lavoro *Rules*. Anche se le regole attive entrano in vigore immediatamente, potrebbero essere necessari fino a 15 minuti perché i risultati delle query memorizzate nella cache vengano aggiornati nella vetrina.

### Visualizza dettagli

Questa opzione consente di visualizzare rapidamente tutti i parametri della regola, mantenendo la tabella *Rules*.

1. Nell&#39;area di lavoro *Regole di merchandising*, individuare la regola nella griglia che si desidera modificare e fare clic su **Altre** (...) opzioni.
1. Fai clic su **Visualizza dettagli** per visualizzare i parametri della regola.
1. Scegliere **Modifica** o **Elimina** oppure fare clic sulla X per chiudere il pannello.

### Elimina regola

1. Nell&#39;area di lavoro *Regole*, individuare la regola nella griglia che si desidera modificare e fare clic su **Altre** (...) opzioni.
1. Fare clic su **Elimina**.

## Descrizioni dei campi

### Condizioni (if)

| Condizione | Descrizione |
|--- |--- |
| La query di ricerca contiene | Carattere o stringa di testo inclusa nella query dell&#39;acquirente. Per soddisfare questa condizione, la query dell’acquirente deve corrispondere a un solo carattere. |
| Query di ricerca: | Carattere o stringa di testo che corrisponde esattamente alla query dell&#39;acquirente. Non è possibile comporre query complesse con più condizioni quando si utilizza questa condizione. |
| La query di ricerca inizia con | La query del cliente inizia con questo carattere o stringa di testo. |
| La ricerca termina con | La query del cliente termina con questo carattere o stringa di testo. |

### Operatori logici

| Operatore | Descrizione |
|--- |--- |
| OPPURE | Impostazione predefinita. L&#39;operatore logico `OR` confronta due condizioni e soddisfa i requisiti per attivare un evento se almeno una condizione è vera. |
| E | L&#39;operatore logico `AND` confronta due condizioni e soddisfa i requisiti per attivare un evento se entrambe le condizioni sono vere. |

### Operatori di corrispondenza

| Operatore | Descrizione |
|--- |--- |
| Qualsiasi | Modifica tutti gli operatori logici nella regola in `OR` e restituisce il set di prodotti corrispondenti. |
| Tutti | Modifica tutti gli operatori logici nella regola in `AND` e restituisce il set di prodotti corrispondenti. |

### Classificazione manuale

| Evento | Descrizione |
|--- |--- |
| Incrementa | Sposta uno SKU o un intervallo di SKU più in alto nei risultati di ricerca. Ognuno di essi è contrassegnato da un badge di anteprima &quot;potenziato&quot; nei risultati della ricerca di test. |
| Buio | Sposta uno SKU o un intervallo di SKU in un livello inferiore nei risultati di ricerca. Ognuno di essi è contrassegnato da un badge di anteprima &quot;interrato&quot; nei risultati della ricerca di test. |
| Fissa un prodotto | Associa un singolo SKU a una posizione specifica nei risultati della ricerca. Il prodotto è contrassegnato con un badge di anteprima &quot;fissato&quot; nei risultati della ricerca di test. |
| Nascondere un prodotto | Esclude uno SKU, o intervallo di SKU, dai risultati della ricerca. |

### Dettagli

| Campo | Descrizione |
|--- |--- |
| Nome | Nome della regola. I nomi delle regole devono essere univoci. |
| Tipo di regola | Predefinito o Query. Il valore predefinito viene applicato a tutte le regole, a meno che non sia definita una regola di query più specifica. |
| Data di inizio | Data di inizio della regola, se pianificata. |
| Data di fine | Data di fine della regola, se pianificata. |
| Descrizione | Breve descrizione della regola. |
