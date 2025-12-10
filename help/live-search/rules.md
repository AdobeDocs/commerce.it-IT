---
title: Cerca nel merchandising
description: '[!DNL Live Search] regole di merchandising combinano logica e azioni per modellare l''esperienza di acquisto.'
exl-id: 9894bf2b-8556-4057-aa23-ebdcb1599914
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---

# Cerca nel merchandising

Per &quot;Search Merchandising&quot; si intende un insieme di regole che combinano logica e azioni per dare forma all’esperienza di ricerca di un acquirente nel tuo negozio. Puoi utilizzare le regole di merchandising per promuovere, seppellire, fissare o nascondere i prodotti per calibrare i risultati della ricerca in tempo reale per supportare gli obiettivi aziendali.

Ogni regola ha tre componenti principali:

* Condizioni: le condizioni che attivano un’azione.
* Eventi: le azioni che hanno luogo quando vengono soddisfatte le condizioni.
* Dettagli: il nome della regola, l’intervallo di tempo facoltativo e la descrizione.

È possibile combinare più condizioni e azioni e pianificare una regola affinché sia attiva per un periodo. Puoi anche impostare una regola predefinita che viene applicata anche quando non è impostato alcun termine di ricerca.

## Requisiti

Una regola di ricerca semplice può avere una singola condizione e un singolo evento, mentre una regola complessa può avere fino a dieci condizioni che attivano fino a 25 eventi.
Le regole possono avere:

* Fino a dieci condizioni
* Fino a 25 eventi

Il testo della query può contenere:

* Caratteri alfanumerici (lettere e numeri)
* Caratteri maiuscoli o minuscoli. L&#39;iniziale maiuscola viene ignorata.

## Operatori logici

Gli operatori logici `AND` e `OR` si uniscono a due condizioni e restituiscono risultati diversi. Tutti gli operatori logici utilizzati in una regola con più condizioni sono gli stessi. Impossibile utilizzare `AND` e `OR` nella stessa regola.

### Operatori di corrispondenza

Gli operatori Match `All` e `Any` determinano l&#39;operatore logico utilizzato per unire più condizioni nella regola e possono essere utilizzati per modificare l&#39;operatore esistente.

* `All` - Utilizza l&#39;operatore logico `AND` per unire più condizioni. Una regola che utilizza l&#39;operatore di corrispondenza `All` può avere una sola condizione `Search query is`.
* `Any` - Utilizza l&#39;operatore logico `OR` per unire più condizioni.

Durante la composizione di una regola complessa, può essere utile scriverla con un rientro per descrivere le condizioni, gli eventi associati e i nomi dei prodotti o gli SKU necessari per restituire i risultati desiderati. Quindi, crea la regola e verifica il risultato.

## Regola predefinita

È possibile impostare una regola predefinita che viene applicata quando non viene fornito alcun termine di ricerca o non è possibile applicare altre regole di ricerca. Se imposti la regola predefinita su &quot;Più acquistati&quot;, tutte le query assumeranno per impostazione predefinita tale tipo di classificazione, a meno che non vengano precedute da un termine di ricerca più specifico. Nessun termine di ricerca può essere impostato per la regola predefinita.

## Ordine di precedenza con più regole

A un termine di ricerca viene applicata una sola regola di ricerca alla volta.
Se a una frase di ricerca sono applicabili più regole, vengono applicate tutte queste regole. Se si verifica una collisione tra due regole, `rule 1`, che aumenta lo SKU1 ma `rule 2` nasconde lo stesso SKU, la regola applicata più di recente (`rule 2`) ha la precedenza.

* Le regole vengono ordinate in base alla marca temporale &quot;Ultima modifica&quot;. La regola modificata più di recente viene applicata per prima, e le regole precedenti vengono applicate in seguito, in ordine di marca temporale.
* La condizione `query is` ha la precedenza rispetto ad altre condizioni. Se una regola più recente contiene una condizione `query contains`, ma una regola precedente ha una condizione `query is`, la regola `query is` viene applicata.

### Richieste Storefront

Se una regola attiva contenente una condizione `query is` corrisponde alla frase di ricerca, viene applicata. Se esistono più regole corrispondenti con una condizione `query is`, viene applicata la regola attiva aggiornata più di recente.
In caso contrario, viene applicata la regola attiva aggiornata più di recente.

### Anteprima richieste

La richiesta effettuata nell’amministratore funziona in modo leggermente diverso. Quando visualizzi l’anteprima in Amministrazione, vengono applicate tutte le regole, incluse quelle scadute e pianificate.

* Se la regola visualizzata in anteprima ha una condizione `query is`, viene applicata.
* Se la regola visualizzata in anteprima non ha una condizione `query is` e viene trovata una regola successiva attiva con una condizione `query is`, la regola `query is` viene applicata.
* Se la regola visualizzata in anteprima non ha una condizione `query is` e non viene trovata alcuna altra regola con una condizione `query is`, la regola visualizzata in anteprima viene applicata.

## Assegnazioni di prodotti di categoria e merchandising categorie

[!DNL Live Search] consente di filtrare per categorie. Per ulteriori informazioni, consulta [merchandising per categorie](category-merch.md).
Tuttavia, in Adobe Commerce puoi creare una categoria virtuale con [Assegnazioni prodotti categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/products-in-category/categories-product-assignments.html?lang=it). Questo tipo di categoria viene creato in fase di esecuzione e non esiste nel database delle categorie. [!DNL Live Search] non è pertanto in grado di leggere o utilizzare questo tipo di categoria.
