---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%
---
Le regole di merchandising combinano la logica con le azioni per modellare l&#39;aspetto dei prodotti in **risultati di ricerca**, in **elenchi di prodotti predefiniti** tramite la **regola di ricerca predefinita** e in **pagine di categorie**. Puoi aumentare, seppellire, fissare o nascondere i prodotti e applicare **classificazione intelligente** in modo che le inserzioni riflettano i tuoi obiettivi aziendali.

Ogni **regola di ricerca** ha tre componenti principali:

- **Condizioni** - Requisiti basati su query che attivano un&#39;azione quando la ricerca dell&#39;acquirente corrisponde.
- **Eventi** - Azioni che vengono eseguite quando vengono soddisfatte le condizioni (classificazione manuale ed eventi correlati).
- **Dettagli** - Nome della regola, intervallo di tempo e descrizione facoltativi.

**Le regole di categoria** utilizzano la **selezione di categorie** invece delle condizioni di query di ricerca. La classificazione intelligente e la classificazione manuale funzionano allo stesso modo della ricerca, con differenze richiamate in [Crea e gestisci regole](https://experienceleague.adobe.com/it/docs/commerce/optimizer/merchandising/rules/add).

È possibile combinare più condizioni e azioni per le regole di ricerca e pianificare l&#39;attivazione di qualsiasi regola per un periodo. È inoltre possibile impostare una **regola di ricerca predefinita** da applicare quando non è disponibile alcuna regola di ricerca o categoria specifica.

## Regole di categoria {#category-rules}

**Regole categoria** controlla l&#39;ordine dei prodotti in **pagine categoria**. Seleziona una o più categorie, quindi applica la classificazione intelligente (ad esempio, più visualizzati, di tendenza) e le azioni manuali come pin, boost e bury. Non utilizzano le condizioni di query di ricerca. Per i passaggi di configurazione, i tipi di regole e il modo in cui viene applicata la classificazione alla categoria rispetto alla ricerca, vedere [Creare e gestire regole](https://experienceleague.adobe.com/it/docs/commerce/optimizer/merchandising/rules/add).

## Requisiti

Una **regola di ricerca** semplice può avere una singola condizione e un singolo evento, mentre una regola complessa può avere fino a dieci condizioni che attivano fino a 25 eventi. **Le regole di categoria** seguono gli stessi limiti di eventi per la classificazione manuale; non utilizzano condizioni di query.

Le regole possono avere:

- Fino a dieci **condizioni** (solo regole di ricerca)
- Fino a 25 **eventi**

Il testo della query può contenere:

- Caratteri alfanumerici (lettere e numeri)
- Caratteri maiuscoli o minuscoli. L&#39;iniziale maiuscola viene ignorata.

## Operatori logici

Gli operatori logici `AND` e `OR` si uniscono a due condizioni e restituiscono risultati diversi. Tutti gli operatori logici utilizzati in una regola con più condizioni sono gli stessi. Impossibile utilizzare `AND` e `OR` nella stessa regola.

### Operatori di corrispondenza

Gli operatori Match `All` e `Any` determinano l&#39;operatore logico utilizzato per unire più condizioni nella regola e possono essere utilizzati per modificare l&#39;operatore esistente.

- `All` - Utilizza l&#39;operatore logico `AND` per unire più condizioni. Una regola che utilizza l&#39;operatore di corrispondenza `All` può avere una sola condizione `Search query is`.
- `Any` - Utilizza l&#39;operatore logico `OR` per unire più condizioni.

Durante la composizione di una regola complessa, può essere utile scriverla con un rientro per descrivere le condizioni, gli eventi associati e i nomi dei prodotti o gli SKU necessari per restituire i risultati desiderati. Quindi, crea la regola e verifica il risultato.

## Regola predefinita

È possibile impostare una **regola di ricerca predefinita** da applicare quando non viene specificato alcun termine di ricerca o non è possibile applicare altre regole di ricerca. Se si imposta la regola predefinita su &quot;Most Purchased&quot; (Più acquistati), le query vengono impostate per default su tale tipo di classificazione, a meno che non vengano sostituite da un termine di ricerca più specifico. Nessun termine di ricerca può essere impostato per la regola predefinita. **Le regole di categoria** sono separate: si applicano solo alle categorie selezionate e non sostituiscono la regola di elenco predefinita.

## Ordine di precedenza con più regole

Quanto segue si applica alle **regole di ricerca** e al modo in cui interagiscono per una determinata ricerca. **Le regole di categoria** si applicano per categoria; consulta [Creare e gestire regole](https://experienceleague.adobe.com/it/docs/commerce/optimizer/merchandising/rules/add) per informazioni su come si adattano alle regole di ricerca e alle regole predefinite.

A un termine di ricerca viene applicata una sola regola di ricerca alla volta.
Se a una frase di ricerca sono applicabili più regole, vengono applicate tutte queste regole. Se si verifica una collisione tra due regole, `rule 1`, che aumenta lo SKU1 ma `rule 2` nasconde lo stesso SKU, la regola applicata più di recente (`rule 2`) ha la precedenza.

- Le regole vengono ordinate in base alla marca temporale &quot;Ultima modifica&quot;. La regola modificata più di recente viene applicata per prima, e le regole precedenti vengono applicate in seguito, in ordine di marca temporale.
- La condizione `query is` ha la precedenza rispetto ad altre condizioni. Se una regola più recente contiene una condizione `query contains`, ma una regola precedente ha una condizione `query is`, la regola `query is` viene applicata.

### Richieste Storefront

Se una regola attiva contenente una condizione `query is` corrisponde alla frase di ricerca, viene applicata. Se esistono più regole corrispondenti con una condizione `query is`, viene applicata la regola attiva aggiornata più di recente.
In caso contrario, viene applicata la regola attiva aggiornata più di recente.

### Anteprima richieste

Le richieste effettuate in anteprima funzionano in modo leggermente diverso. Durante la visualizzazione in anteprima, vengono applicate tutte le regole, incluse quelle scadute e pianificate.

- Se la regola visualizzata in anteprima ha una condizione `query is`, viene applicata.
- Se la regola visualizzata in anteprima non ha una condizione `query is` e viene trovata una regola successiva attiva con una condizione `query is`, la regola `query is` viene applicata.
- Se la regola visualizzata in anteprima non ha una condizione `query is` e non viene trovata alcuna altra regola con una condizione `query is`, la regola visualizzata in anteprima viene applicata.
