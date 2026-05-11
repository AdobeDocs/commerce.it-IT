---
title: Creare e gestire le regole
description: Scopri come creare e gestire le regole di merchandising per le pagine di ricerca, gli elenchi di prodotti predefiniti e le categorie.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: fd4df2b2-83de-4c5c-b18c-e97aa07ef8f6
TQID: https://experienceleague.adobe.com/UOe-TPaF80Wrk-gNuJwLTdndVQMQfbYrbpAfb-r4pJc
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 2760
ht-degree: 0%

---

# Creare e gestire le regole

Per creare una regola, apri l&#39;editor di regole, scegli un **tipo di regola** (condizioni di ricerca, elenco predefinito o pagine di categorie), quindi definisci le condizioni e la classificazione in cui vengono applicate, verifica i risultati e pubblica la regola.

## Creare una regola {#create-a-rule}

1. Nella barra a sinistra, passa a _Merchandising_ > **Regole di merchandising**.
1. (Facoltativo) Utilizza il menu a discesa **Vista catalogo** per selezionare la vista catalogo in cui applicare la regola. La regola creata ha l&#39;ambito della vista selezionata (o di tutte le viste catalogo se è selezionato **Tutte le viste**). Per informazioni sul funzionamento dell&#39;ambito della visualizzazione catalogo, vedere [Selezionare la visualizzazione catalogo](workspace.md#select-catalog-view).

   >[!IMPORTANT]
   >
   >Le visualizzazioni del catalogo sono attualmente in [beta](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta#merchandising-rules-globally-and-per-catalog-view-public-beta). I partecipanti a Beta dovranno ricreare eventuali regole di merchandising esistenti per sfruttare il nuovo ambito di visualizzazione del catalogo.

1. Fare clic su **[!UICONTROL Create rule]** per avviare l&#39;editor di regole.

![Crea regola](../../assets/create-rule.png)

### Tipi di regole

Ogni tipo di regola dispone di un’icona di informazioni nell’editor con una breve spiegazione. Utilizza il tipo di corrispondenza in cui gli acquirenti devono visualizzare la logica di merchandising:

| Tipo di regola | Finalità |
| --- | --- |
| **Regola per tutti i prodotti** | Classificazione e merchandising predefiniti tra gli elenchi di prodotti quando non si applica alcuna regola di ricerca o categoria più specifica. Puoi creare una sola regola di questo tipo, non può contenere condizioni. |
| **Regola categoria** (Beta) | Applica il merchandising e la classificazione a una o più categorie selezionate, controllando l’ordine dei prodotti nelle pagine delle categorie. |
| **Regola di ricerca** | Applica il merchandising e la classificazione quando gli acquirenti eseguono una ricerca che corrisponde alle condizioni di query della regola. |

Nella sezione **Genera la regola**, puoi definire il nome della regola, la pianificazione, se la regola si applica a tutte le inserzioni o a condizioni di ricerca specifiche, e i tipi di classificazione.

1. Nel campo **[!UICONTROL Name]** immettere un nome per la regola. Tutti i nomi delle regole devono essere univoci.
1. Nel campo **[!UICONTROL Description]** immettere una descrizione per la regola.
1. Nel campo **[!UICONTROL Date range]** specificare la data o l&#39;intervallo di date in cui si desidera attivare la regola.
1. Nella sezione **[!UICONTROL Rule applies to]** selezionare il [tipo di regola](#rule-types) che si desidera utilizzare.

>[!BEGINTABS]

>[!TAB Regola di ricerca]

Una regola di ricerca applica la logica di merchandising e classificazione quando gli acquirenti eseguono una ricerca che corrisponde alle condizioni definite.

Le condizioni sono i requisiti per attivare un evento. Una regola può avere fino a dieci condizioni e 25 eventi. Una regola predefinita non può avere condizioni.

![Seleziona condizione regola](../../assets/rule-set-condition.png)

**Condizione singola**

1. In *Genera la regola*, seleziona la **Condizione** da soddisfare e segui le istruzioni per completare l&#39;istruzione.

   - Query di ricerca contiene: immettere la stringa di testo che deve essere inclusa nella query dell&#39;acquirente. L&#39;impostazione Corrispondenza determina il grado di corrispondenza tra la query dell&#39;acquirente e il catalogo. Opzioni:<br /> Qualsiasi - Qualsiasi parte del testo della query dell&#39;acquirente può corrispondere alla condizione.<br />Tutti - Tutte le query dell&#39;acquirente devono corrispondere alla condizione.
   - Query di ricerca: immetti una stringa di testo che corrisponda esattamente alla query dell’acquirente. Ad esempio: &quot;pantaloni da yoga&quot;. Le regole con `Search query is` e la corrispondenza `All` possono avere una sola condizione.
   - La query di ricerca inizia con - Inserisci un carattere o una stringa di testo che deve trovarsi all’inizio della query dell’acquirente.
   - La query di ricerca termina con - Immetti un carattere o una stringa di testo che deve trovarsi alla fine della query dell’acquirente.

   I risultati vengono visualizzati immediatamente nel riquadro *Verifica regola* e sono numerati per priorità. Puoi utilizzare il cursore *Risultati per riga* in alto a destra per modificare il numero di prodotti in ogni riga.

1. Per verificare altre query, modifica il testo della query nella casella di ricerca *Verifica la regola* e premi **Invio**.
Inizialmente, il riquadro dei test esegue il rendering della query dalla casella di ricerca Condizioni. Ma ora sta eseguendo il rendering della query dalla casella di query del test. Nel riquadro dei test viene eseguita una sola query alla volta.
1. Se il risultato ti piace, aggiorna il testo nella casella di ricerca *Condizioni*. Quindi, fai clic in un punto qualsiasi della pagina per aggiornare i risultati nel riquadro del test.
1. Imposta [Classificazione intelligente](#intelligent-ranking) e [Classificazione manuale](#manual-ranking) come descritto nelle sezioni seguenti. Gli stessi controlli si applicano alle pagine delle categorie, con le eventuali differenze indicate.

**Più condizioni**

1. Per creare una regola con più condizioni, fare clic su **Aggiungi condizione**.
Una regola può avere fino a dieci condizioni. L&#39;operatore logico che unisce due condizioni si basa sull&#39;impostazione *Match* corrente. Per impostazione predefinita, *Match* è `All` e l&#39;operatore logico è `AND`.

1. Seleziona la seconda condizione e immetti il testo della query richiesto.

1. Per modificare la logica della regola, modifica l&#39;impostazione **Corrispondenza** per determinare la corrispondenza tra i criteri di ricerca dell&#39;acquirente e la condizione della query. Imposta **Corrispondenza** su uno dei seguenti elementi:

   - Qualsiasi - (impostazione predefinita) Tutti gli operatori logici nella regola sono impostati su `OR` e i risultati vengono visualizzati nel riquadro dei test.
   - Tutti: tutti gli operatori logici nella regola sono impostati su `AND` e i risultati vengono visualizzati nel riquadro dei test.

   Il valore *Match* determina l&#39;operatore logico utilizzato per unire più condizioni. La modifica dell&#39;impostazione *Match* comporta la modifica di tutti gli operatori logici nella regola. Impossibile combinare `AND` e `OR` nella stessa regola.

   In questo esempio, invece di cercare &quot;pantaloni yoga&quot;, ci sono due query separate che cercano &quot;yoga&quot; o &quot;pantaloni&quot;. Questa regola è meno specifica e viene attivata più spesso nella vetrina rispetto alle altre.

1. Per aggiungere un&#39;altra condizione, fare clic su **Aggiungi condizione** e ripetere il processo.
1. Imposta [Classificazione intelligente](#intelligent-ranking) e [Classificazione manuale](#manual-ranking) come descritto nelle sezioni seguenti. Gli stessi controlli si applicano alle pagine delle categorie, con le eventuali differenze indicate.

>[!TAB Regola categoria]

>[!IMPORTANT]
>
>Le regole di categoria sono in versione beta.

Le regole di categoria controllano il modo in cui i prodotti vengono ordinati nelle **pagine di categoria**. È possibile combinare **regole categoria** con **classificazione intelligente** (inclusi i segnali basati sull&#39;intelligenza artificiale) e **azioni manuali** quali pin, boost e bury, in modo da poter curare l&#39;individuazione, eseguire promozioni e allineare le pagine categoria con la strategia senza affidarsi a strumenti esterni.

1. In **Categorie** selezionare la categoria o le categorie a cui applicare la regola. Le categorie selezionate vengono visualizzate sotto il controllo per consentirti di confermare l’ambito.
1. Nell’elenco delle categorie visualizzate, puoi fare clic sui tre punti e selezionare una delle seguenti opzioni:

   - **Elimina** - Rimuove la categoria dalla regola.
   - **Applica a sottocategorie** - Applica la regola alle sottocategorie per le quali non è già stata definita una regola di merchandising attiva.
   - **Anteprima** - Visualizza l&#39;aspetto della pagina della categoria nella vetrina.

1. Imposta [Classificazione intelligente](#intelligent-ranking) e [Classificazione manuale](#manual-ranking) come descritto nelle sezioni seguenti. Gli stessi controlli si applicano alle regole di ricerca, con eventuali differenze richiamate.

>[!ENDTABS]

### Classificazione intelligente {#intelligent-ranking}

Classificazione intelligente ordina i prodotti utilizzando **segnali comportamentali** e, se applicabile, IA. Si applica a **regole di ricerca**, **tutti gli elenchi di prodotti** (regole predefinite) e **regole categoria** (pagine categorie). Per gli acquirenti **ricerche**, la classificazione pesa anche **rilevanza testuale** per la query; **le pagine di categoria** non utilizzano il testo della query allo stesso modo, l&#39;editor si concentra sulle strategie comportamentali.

I proprietari dei negozi possono impostare strategie come le seguenti. Le etichette esatte e le finestre temporali corrispondono all’editor di regole e possono differire leggermente per tipo di regola.

![Classificazioni intelligenti](../../assets/rule-intelligent-ranking.png)

- **Più acquistati** / **Più acquistati** — Classifica per frequenza di acquisto per SKU in una finestra recente (ad esempio, i 7 giorni precedenti per i contesti di ricerca).
- **Più aggiunti al carrello** — Classifica per attività totale aggiunta al carrello in una finestra recente (ad esempio, i 7 giorni precedenti per i contesti di ricerca).
- **Più visualizzati** — classifica per visualizzazioni per SKU in una finestra recente (ad esempio, i 7 giorni precedenti per i contesti di ricerca).
- **Consigliato per te** — Utilizza il segnale `viewed-viewed`: gli acquirenti che hanno visualizzato questo SKU hanno visualizzato anche altri SKU; supporta l&#39;ordinamento personalizzato nelle pagine delle categorie, se disponibile.
- **Di tendenza** — sottolinea la popolarità recente (per la ricerca, visualizzazioni di pagina nelle ultime 72 ore per eventi in background e 24 ore per eventi in primo piano).
- **Nessuno** - Per le ricerche e le inserzioni predefinite, i prodotti sono ordinati per **Rilevanza**. Per **regole categoria**, utilizza l&#39;ordine di merchandising predefinito per la categoria quando non scegli un&#39;altra strategia intelligente.

Seleziona la strategia per la regola. Nel riquadro **Verifica regola** sono visualizzati i risultati previsti per le regole orientate alla ricerca; **regole di categoria** utilizzano l&#39;anteprima delle categorie.

#### Funzionamento del punteggio di classificazione intelligente (ricerca)

Per **risultati di ricerca** (e la query di test nell&#39;editor delle regole), la classificazione intelligente determina l&#39;ordine finale del prodotto combinando due fattori chiave: **rilevanza testuale** e **segnali comportamentali**. Comprendere come questi fattori interagiscono consente di impostare aspettative realistiche per i risultati della ricerca.

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
- Per garantire che la classificazione intelligente funzioni correttamente per **ricerca**, assicurati che il **Peso di ricerca** per tutti gli attributi utilizzati per la ricerca o il filtraggio (facet) sia pari o inferiore a `5`. Questa guida si applica all’indicizzazione delle ricerche e non ai flussi di merchandising di sola categoria.

Per informazioni sull&#39;impostazione dei pesi di ricerca, vedere [API metadati](https://developer.adobe.com/commerce/services/reference/rest/).

### Classificazione manuale {#manual-ranking}

**Classificazione manuale** eventi regola l&#39;ordine dei prodotti per **risultati di ricerca** (quando le condizioni della regola sono soddisfatte), per **elenchi di prodotti predefiniti** e per **elenchi di pagine categorie**. Una singola regola può avere fino a 25 eventi.

- **Incrementa** — sposta un prodotto in alto nell&#39;elenco.
- **Buio** - Sposta uno SKU in basso nell&#39;elenco.
- **Fissa un prodotto** - Corregge un prodotto nella posizione selezionata nell&#39;elenco.
- **Nascondi un prodotto** - Esclude uno SKU dai risultati (orientato alla ricerca; comportamento di conferma per le regole di categoria nell&#39;editor).

Il modo più semplice per fissare un prodotto è tramite trascinamento.

1. Fai clic su un prodotto e trascinalo nel riquadro Test. Trascinalo e rilascialo nella posizione desiderata. I campi Prodotto e Posizione vengono compilati automaticamente nel riquadro Eventi.

Puoi anche fare clic sull’icona a forma di pin per fissare un prodotto alla posizione corrente. Utilizza il menu di scelta rapida con puntini di sospensione per &quot;Fissa in alto&quot; o &quot;Fissa in basso&quot;.

>[!NOTE]
>
>**Regole di ricerca** - È possibile fissare solo i prodotti visualizzati nei risultati della ricerca per le condizioni della regola e della query configurate. I prodotti devono essere indicizzati, visibili, in magazzino e soddisfare tutti i filtri delle regole per essere idonei al fissaggio. Se un prodotto non viene visualizzato nell’anteprima o nei risultati per la regola, l’operazione di fissaggio non ha alcun effetto.
>
>**Ordinamento predefinito**: le posizioni manuali vengono applicate quando l&#39;acquirente utilizza l&#39;ordinamento predefinito: **Ordina per: Più rilevante** per la ricerca o **rilevanza** / **posizione** per gli elenchi di categorie. Se l’acquirente cambia ordinamento; ad esempio per nome, il comportamento bloccato, potenziato, interrato o nascosto potrebbe non corrispondere più all’anteprima.

Gli eventi OR possono essere impostati manualmente:

1. In *Eventi*, scegli l&#39;**Evento** da eseguire quando vengono soddisfatte le condizioni associate.

   Scegliere ad esempio `Hide a product`. Quindi, inserisci il nome del prodotto che desideri nascondere. I prodotti vengono suggeriti durante la digitazione.

1. Per più eventi, scegli qualsiasi altro evento che desideri attivare quando vengono soddisfatte le condizioni.

### Finalizzazione della regola {#finalizing-the-rule}

1. Esaminare i risultati della regola nel riquadro del test.
1. Se la regola dispone di più query, esegui il test di ciascuna che potrebbe essere interessata dalla regola.
1. Al termine, fare clic su **Salva e pubblica**.

   La regola viene aggiunta all&#39;elenco nell&#39;area di lavoro *Rules*.

1. Anche se le regole attive entrano in vigore immediatamente, potrebbe essere necessario attendere fino a 15 minuti prima che i risultati della query memorizzata nella cache vengano aggiornati nella vetrina.

>[!NOTE]
>
>Le regole e i prodotti classificati manualmente vengono applicati ai risultati di **ricerca** quando viene selezionato l&#39;ordinamento predefinito &quot;Ordina per: Più rilevante&quot;. Se un acquirente modifica l’ordinamento in modo da ottenere un ordinamento simile a ordinamento per nome, le regole e le classificazioni manuali non sono più in vigore. Per le **inserzioni categoria**, il comportamento predefinito è descritto in [Classificazione manuale](#manual-ranking).

## Modificare, visualizzare ed eliminare le regole {#edit-view-and-delete-rules}

Segui queste istruzioni per aggiornare le proprietà delle regole esistenti. Non è possibile modificare la vista catalogo (ambito) di una regola dopo averla creata; l&#39;ambito viene impostato al momento della creazione della regola. Vedi [Seleziona visualizzazione catalogo](workspace.md#select-catalog-view).

### Modifica regola

1. Nell&#39;area di lavoro *Regole di merchandising*, individua la regola nella griglia da modificare e fai clic su **Altro** (...) opzioni.
1. Fai clic su **Modifica** per accedere all&#39;editor di regole.
1. Aggiorna condizioni, operatori ed eventi in base alle esigenze.
1. Se necessario, aggiorna i campi nome, data di inizio e di fine e descrizione. Tutti i nomi delle regole devono essere univoci.
1. Verifica la regola.
1. Pubblica le modifiche.
La regola viene aggiunta all&#39;elenco nell&#39;area di lavoro *Rules*. Anche se le regole attive entrano in vigore immediatamente, potrebbero essere necessari fino a 15 minuti perché i risultati delle query memorizzate nella cache vengano aggiornati nella vetrina.

### Visualizza dettagli

Questa opzione consente di visualizzare rapidamente tutti i parametri della regola, mantenendo la tabella *Rules*.

1. Nell&#39;area di lavoro *Regole di merchandising*, individuare la regola nella griglia da modificare e fare clic su **Altro** (...) opzioni.
1. Fai clic su **Visualizza dettagli** per visualizzare i parametri della regola.
1. Scegliere **Modifica** o **Elimina** oppure fare clic sulla X per chiudere il pannello.

### Elimina regola

1. Nell&#39;area di lavoro *Regole*, individuare la regola nella griglia che si desidera modificare e fare clic su **Altro** (...) opzioni.
1. Fare clic su **Elimina**.

## Descrizioni dei campi {#field-descriptions}

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

### Eventi di classificazione manuale

| Evento | Descrizione |
|--- |--- |
| Incrementa | Sposta uno SKU o un intervallo di SKU più in alto nell’elenco (ricerca o categoria). Ognuno di essi è contrassegnato da un badge di anteprima &quot;potenziato&quot; nei risultati del test. |
| Buio | Sposta uno SKU o un intervallo di SKU più in basso nell&#39;elenco. Ognuno di essi è contrassegnato da un badge di anteprima &quot;interrato&quot; nei risultati del test. |
| Fissa un prodotto | Associa un singolo SKU a una posizione specifica nell&#39;elenco. Nei risultati del test, il prodotto è contrassegnato con un badge di anteprima &quot;fissato&quot;. |
| Nascondere un prodotto | Esclude uno SKU, o un intervallo di SKU, dai risultati (orientato alla ricerca; conferma per regole di categoria nell’editor). |

### Dettagli

| Campo | Descrizione |
|--- |--- |
| Nome | Nome della regola. I nomi delle regole devono essere univoci. |
| Tipo di regola | **Predefinito** (tutti gli elenchi prodotti), **Query** (condizioni di ricerca specifiche) o **Categoria** (pagine categorie), a seconda di **La regola si applica a**. |
| Data di inizio | Data di inizio della regola, se pianificata. |
| Data di fine | Data di fine della regola, se pianificata. |
| Descrizione | Breve descrizione della regola. |
