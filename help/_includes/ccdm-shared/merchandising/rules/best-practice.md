---
source-git-commit: e3be9274ca8db80d3559b24a5c8be36f5d61b2ba
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/rules/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Best practice per le regole di merchandising

Per ottimizzare la conversione e i ricavi, implementa **regole di ricerca** efficaci, una **regola di elenco predefinita** forte e **[regole di categoria](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types)**. Regola le classificazioni utilizzando dati di vendita, azioni, promozioni e [classificazione intelligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking).

Utilizza [regole di soppressione della ricerca](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#search-suppression-rules) solo quando le query corrispondenti devono restituire zero prodotti, non quando i prodotti richiedono una classificazione diversa.

È fondamentale stabilire una regola **predefinita** ben ponderata. La [regola predefinita](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#default-rule) determina il modo in cui i risultati della ricerca vengono inizialmente ordinati quando non si applica alcuna regola di ricerca più specifica, migliorando così l&#39;individuazione e la probabilità di acquisto. Esamina regolarmente in modo da tenere il passo con le esigenze e le campagne dei clienti.

## Suggerimenti per ottimizzare le regole di ricerca

- Aggiungi o incrementa prodotti con elevati volumi di vendita o attività di vendita recenti.
- Dai priorità ai prodotti con valutazioni elevate e recensioni positive.
- Assicurati che gli articoli in magazzino abbiano una classificazione più alta.
- Dare leggermente priorità ai prodotti con margini di profitto più elevati senza compromettere la rilevanza.
- Evidenzia i prodotti in vendita o inclusi nelle promozioni speciali.
- Impostare automaticamente le regole di ricerca durante i periodi di promozione o di vendita utilizzando l&#39;intervallo di date durante il periodo di promozione.
- Personalizza i risultati della ricerca in base al comportamento dei singoli acquirenti utilizzando [classificazione intelligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking), ad esempio &quot;consigliato per te&quot;, &quot;più visualizzato&quot; e così via.
- Quando è selezionata una strategia intelligente diversa da **Nessuno**, sintonizza **[Aumento classificazione intelligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** per regola e convalida in **Verifica la regola** prima di pubblicare.
- Utilizza sempre il pannello &quot;Test della regola&quot; per visualizzare in anteprima come la tua strategia di classificazione intelligente influisce sui risultati effettivi della ricerca per query diverse.

## Suggerimenti per le regole di categoria

- Utilizza [regole di categoria](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types) nelle **pagine di categoria** con traffico elevato o margine elevato in cui l&#39;ordine curato è importante quanto la ricerca, ad esempio raccolte stagionali o reparti in primo piano.
- Allinea **classificazione intelligente** (ad esempio, di tendenza, più visualizzato) al modo in cui gli acquirenti sfogliano tale categoria; le pagine delle categorie non utilizzano il testo delle query di ricerca come fanno le regole di ricerca. Vedi [Classificazione intelligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking). Per i metodi intelligenti diversi da **Nessuno**, utilizza **[Aumento classificazione intelligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** e l&#39;anteprima delle categorie per ottimizzare la forza comportamentale per la regola di categoria.
- Applica **pin**, **boost** e **bury** in modo coerente con il piano della campagna; ricorda che le posizioni manuali di solito si applicano solo quando l&#39;acquirente utilizza l&#39;**ordinamento predefinito** per l&#39;inserzione. Vedi [Classificazione manuale](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#manual-ranking).
- Anteprima nel flusso di regole **categoria** nell&#39;editor e convalida nella vetrina dopo la pubblicazione, stessa disciplina utilizzata per il pannello &quot;Test della regola&quot; durante la ricerca.

## Best practice e casi d’uso per l’eliminazione della ricerca {#search-suppression-best-practices}

Una regola di soppressione della ricerca blocca i risultati per le query che corrispondono alle relative condizioni, pertanto la vetrina visualizza una pagina di risultati di ricerca con zero prodotti. L’editor di regole non fornisce un’anteprima per le regole di soppressione. Utilizza la condizione più stretta che soddisfa la restrizione, quindi segui [Crea e gestisci regole di soppressione della ricerca](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules). Quando la regola diventa attiva, verifica le ricerche corrispondenti e non corrispondenti nella vetrina. Controlla l’effettiva presentazione senza risultati della vetrina.

| Caso d’uso | Configurazione suggerita | Cosa controllare |
| --- | --- | --- |
| Conformità alle normative per la ricerca | Esegui la valutazione della regola nella vista catalogo interessata e utilizza i termini di ricerca limitati. | Conferma i termini con il tuo team di conformità. La soppressione della ricerca da sola non impedisce l’accesso tramite la navigazione tra categorie, pagine di merchandising, consigli o URL di prodotti diretti. |
| Restrizioni di branding | Usa **La query contiene** quando un nome di marchio con restrizioni deve essere bloccato all&#39;interno di query più lunghe. | Dopo che la regola diventa attiva, seleziona le query non correlate in vetrina che contengono testo simile per evitare di eliminare le ricerche legittime. |
| Impedisci a un termine di ricerca specifico di restituire risultati | Utilizza **Query is** per una frase esatta che non deve restituire alcun prodotto. | Controllare le frasi correlate separatamente. Una condizione di corrispondenza esatta non blocca ogni query contenente tale frase. |
| Restrizioni sui prefissi o suffissi di query | Utilizza **La query inizia con** o **La query termina con** quando la posizione del testo con restrizioni è importante. | Dopo che la regola diventa attiva, controlla le query della vetrina con il testo all’inizio, al centro e alla fine per confermare l’ambito previsto. |
| Limitazioni di ricerca temporanee | Imposta una data di inizio e una data di fine per una restrizione limitata nel tempo. | Conferma la pianificazione e lo stato abilitato e controlla se la regola è ancora necessaria al termine della restrizione. |

- Assegna un nome descrittivo a ogni regola e registra il motivo della restrizione nella relativa descrizione.
- Rivedi le condizioni della query prima di pubblicare le modifiche. Dopo che la regola diventa attiva, controlla le query vetrina che devono essere bloccate e le query che devono ancora restituire prodotti. L’aggiornamento dei risultati delle query memorizzate nella cache può richiedere fino a 15 minuti.
- Esamina lo stato senza risultati della vetrina e assicurati che gli acquirenti abbiano un modo utile per continuare a navigare, ad esempio rivedere la query o passare a una categoria, se supportato dalla vetrina.
- Non utilizzare l’eliminazione delle query in sostituzione delle esclusioni a livello di prodotto. Per escludere i prodotti dai risultati della ricerca, dai suggerimenti di ricerca e dal completamento automatico, utilizza esclusioni manuali o **Eventi di merchandising basati su attributi** con un&#39;azione **Nascondi** nella **regola di ricerca predefinita**.
- Rivedi regolarmente le regole di soppressione attive. Disattiva le regole non più necessarie oppure modificale e pubblicale quando cambiano le restrizioni.
