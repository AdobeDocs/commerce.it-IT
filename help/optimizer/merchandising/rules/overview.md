---
title: Regole di merchandising
description: '[!DNL Adobe Commerce Optimizer] le regole di merchandising combinano la logica con le azioni per modellare i risultati della ricerca, gli elenchi di prodotti predefiniti e le pagine delle categorie.'
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: f2a9b5e8-d23d-4855-b424-ca6b40e057df
TQID: https://experienceleague.adobe.com/1lpaqHx0SaVYLXcTSOToxvbpKzhPJKmhfxjlCvNQLkU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 838
ht-degree: 0%

---

# Regole di merchandising

Le regole di merchandising combinano la logica con le azioni per modellare l&#39;aspetto dei prodotti in **risultati di ricerca**, in **elenchi di prodotti predefiniti** (**tutti gli elenchi di prodotti**) e in **pagine di categorie** ([regole di categoria](#category-rules) sono in versione beta). Puoi aumentare, seppellire, fissare o nascondere i prodotti e applicare **classificazione intelligente** in modo che le inserzioni riflettano i tuoi obiettivi aziendali.

Ogni **regola di ricerca** ha tre componenti principali:

- **Condizioni** - Requisiti basati su query che attivano un&#39;azione quando la ricerca dell&#39;acquirente corrisponde.
- **Eventi** - Azioni che vengono eseguite quando vengono soddisfatte le condizioni (classificazione manuale ed eventi correlati).
- **Dettagli** - Nome della regola, intervallo di tempo e descrizione facoltativi.

**Le regole di categoria** utilizzano la **selezione di categorie** invece delle condizioni di query di ricerca. La classificazione intelligente e la classificazione manuale funzionano allo stesso modo della ricerca, con differenze richiamate in [Crea e gestisci regole](add.md).

È possibile combinare più condizioni e azioni per le regole di ricerca e pianificare l&#39;attivazione di qualsiasi regola per un periodo. È inoltre possibile impostare una **regola predefinita** (**Tutti gli elenchi di prodotti**) che viene applicata quando non viene applicata alcuna regola di ricerca o categoria specifica.

## Regole di categoria {#category-rules}

>[!IMPORTANT]
>
>Le regole di categoria sono in versione beta.

**Regole categoria** controlla l&#39;ordine dei prodotti in **pagine categoria**. Seleziona una o più categorie, quindi applica la classificazione intelligente (ad esempio, più visualizzati, di tendenza) e le azioni manuali come pin, boost e bury. Non utilizzano le condizioni di query di ricerca. Per i passaggi di configurazione, i tipi di regole e il modo in cui viene applicata la classificazione alla categoria rispetto alla ricerca, vedere [Creare e gestire regole](add.md).

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

È possibile impostare una regola predefinita (**Tutti gli elenchi di prodotti**) che viene applicata quando non viene specificato alcun termine di ricerca o non è possibile applicare altre regole di ricerca. Se si imposta la regola predefinita su &quot;Most Purchased&quot; (Più acquistati), le query vengono impostate per default su tale tipo di classificazione, a meno che non vengano sostituite da un termine di ricerca più specifico. Nessun termine di ricerca può essere impostato per la regola predefinita. **Le regole di categoria** sono separate: si applicano solo alle categorie selezionate e non sostituiscono la regola di elenco predefinita.

## Ordine di precedenza con più regole

Quanto segue si applica alle **regole di ricerca** e al modo in cui interagiscono per una determinata ricerca. **Le regole di categoria** si applicano per categoria; consulta [Creare e gestire regole](add.md) per informazioni su come si adattano alle regole di ricerca e alle regole predefinite.

A un termine di ricerca viene applicata una sola regola di ricerca alla volta.
Se a una frase di ricerca sono applicabili più regole, vengono applicate tutte queste regole. Se si verifica una collisione tra due regole, `rule 1`, che aumenta lo SKU1 ma `rule 2` nasconde lo stesso SKU, la regola applicata più di recente (`rule 2`) ha la precedenza.

- Le regole vengono ordinate in base alla marca temporale &quot;Ultima modifica&quot;. La regola modificata più di recente viene applicata per prima, e le regole precedenti vengono applicate in seguito, in ordine di marca temporale.
- La condizione `query is` ha la precedenza rispetto ad altre condizioni. Se una regola più recente contiene una condizione `query contains`, ma una regola precedente ha una condizione `query is`, la regola `query is` viene applicata.

### Richieste Storefront

Se una regola attiva contenente una condizione `query is` corrisponde alla frase di ricerca, viene applicata. Se esistono più regole corrispondenti con una condizione `query is`, viene applicata la regola attiva aggiornata più di recente.
In caso contrario, viene applicata la regola attiva aggiornata più di recente.

### Anteprima richieste

La richiesta effettuata in [!DNL Adobe Commerce Optimizer] funziona in modo leggermente diverso. Durante l&#39;anteprima di [!DNL Adobe Commerce Optimizer], vengono applicate tutte le regole, incluse quelle scadute e pianificate.

- Se la regola visualizzata in anteprima ha una condizione `query is`, viene applicata.
- Se la regola visualizzata in anteprima non ha una condizione `query is` e viene trovata una regola successiva attiva con una condizione `query is`, la regola `query is` viene applicata.
- Se la regola visualizzata in anteprima non ha una condizione `query is` e non viene trovata alcuna altra regola con una condizione `query is`, la regola visualizzata in anteprima viene applicata.
