---
title: Best practice per [!DNL Live Search]
description: Scopri le best practice per l'implementazione di [!DNL Live Search] nel tuo store.
role: Admin, Developer
exl-id: f7700339-fb13-42fe-a249-17cd4ba36e1b
source-git-commit: a22a57f52503811a3a3e9294174a6626c5630b79
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 0%

---

# Best practice

Questo articolo aiuta i commercianti a migliorare la funzionalità di ricerca sul sito, garantendo un’esperienza di acquisto fluida ed efficiente che massimizza i tassi di conversione. Seguendo le strategie descritte, imparerai a implementare funzionalità di ricerca avanzate e a perfezionare continuamente lo strumento di ricerca per ottenere prestazioni ottimali con Adobe Commerce [!DNL Live Search].

Esistono diversi fattori chiave che determinano la rilevanza e l’efficacia dei risultati della ricerca:

- Dati di prodotto ben strutturati garantiscono che gli algoritmi di ricerca possano far corrispondere efficacemente i prodotti alle query. La bassa qualità dei dati sui prodotti porta a risultati di ricerca poco rilevanti. Per avere un impatto diretto sul successo della strategia di merchandising:
   - Imposta gli attributi corretti come ricercabili con il loro peso corrispondente.
   - Assicurati che i dati all’interno di tali attributi siano pertinenti.
- Un’esperienza di ricerca ben progettata crea fiducia nei clienti e infonde fiducia nel fatto che troveranno ciò di cui hanno bisogno.
- Le regole di ricerca sono fondamentali in quanto possono aumentare la visibilità di alcuni prodotti in base alla popolarità, ai nuovi arrivi, ai criteri promozionali o a qualsiasi altra strategia di merchandising per soddisfare le esigenze aziendali.
- La navigazione a facet consente ai clienti di perfezionare le ricerche e ottenere rapidamente risultati rilevanti.

Per gestire [!DNL Live Search], vai a **Marketing** > *SEO &amp; Search* > **[!DNL Live Search]** nell&#39;amministratore Adobe [!DNL Commerce]. 

## Ottimizzazione della funzionalità di ricerca

In questa sezione imparerai a ottimizzare le funzionalità di ricerca utilizzando funzionalità quali il completamento automatico per fornire suggerimenti in tempo reale come il tipo di acquirente, i sinonimi e gli ortografi per garantire che gli acquirenti trovino i prodotti anche se utilizzano parole diverse, e i facet per consentire agli acquirenti di limitare i risultati della ricerca.

### Completamento automatico

Il completamento automatico, noto anche come completamento automatico o suggerimento automatico, è una funzione di ricerca interattiva che visualizza dinamicamente i suggerimenti agli acquirenti man mano che immettono i termini di ricerca. In questo modo i clienti possono trovare i prodotti in modo rapido e semplice, offrendo suggerimenti in tempo reale in base alle loro esigenze.

Il widget [!DNL Live Search] [[!DNL popover]](storefront-popover.md) abilita le opzioni di ricerca di completamento automatico per suggerire i prodotti più comuni. Con ogni carattere digitato dal cliente, il popover si aggiorna con i prodotti suggeriti e le miniature dei risultati di ricerca principali.

[!DNL Live Search] inizia a restituire risultati quando l&#39;utente ha digitato due caratteri. Per una corrispondenza parziale, il numero massimo di caratteri per parola è 20. Il numero di caratteri in una query di ricerca durante la digitazione non è configurabile.

Ulteriori informazioni sul widget [popover](storefront-popover.md).

### Sinonimi e errori di ortografia

Per impostazione predefinita, Live Search gestisce gli errori di ortografia. È possibile impostare sinonimi per includere parole che gli acquirenti potrebbero utilizzare, diverse dalle parole specificate nel catalogo. Non si vuole perdere una vendita perché qualcuno sta cercando un &quot;divano&quot;, mentre il vostro prodotto è elencato come un &quot;divano&quot;. È possibile acquisire un&#39;ampia gamma di termini di ricerca immettendo tutte le possibili parole che i clienti potrebbero utilizzare per trovare i prodotti. È possibile [impostare i sinonimi in un modo o in due](synonyms-add.md#step-2-define-the-synonym-by-type) per migliorare i risultati.

#### Suggerimenti per ottimizzare i sinonimi

- Mappa i nomi dei marchi e le abbreviazioni ai loro nomi completi, ad esempio &quot;HP&quot; in &quot;Hewlett-Packard&quot; e i soprannomi di prodotto comuni, ad esempio &quot;iPhone&quot; in &quot;Apple iPhone&quot;.
- Includere un gergo specifico per il settore e termini che gli acquirenti potrebbero utilizzare in modo intercambiabile, ad esempio &quot;scarpe da ginnastica&quot; e &quot;scarpe da corsa&quot;.
- Aggiorna regolarmente l’elenco dei sinonimi in base alle nuove tendenze di ricerca, alle aggiunte di prodotti e al comportamento degli acquirenti.
- Verifica l’efficacia delle mappature dei sinonimi analizzando i risultati della ricerca e il feedback degli acquirenti. Affina le mappature per migliorare precisione e rilevanza.

Ulteriori informazioni sui sinonimi:

- [Tipi di sinonimi](synonyms-type.md)
- [Creare sinonimi](synonyms-add.md)
- [Gestire i sinonimi](synonyms-manage.md)
- [Supporto linguistico](settings.md#language)

### Facet

Le funzionalità di filtro e facet sono un componente fondamentale del sito [!DNL Commerce], progettato per migliorare l&#39;esperienza dell&#39;acquirente consentendo agli acquirenti di limitare i risultati di ricerca e trovare i prodotti in modo più efficiente. Questa funzionalità consente agli acquirenti di ordinare all’interno di vasti cataloghi di articoli applicando criteri specifici, rendendo il processo di acquisto più veloce, semplice e soddisfacente. Implementando filtri e facet efficaci e facet facet facet, puoi aiutare i clienti a trovare esattamente ciò di cui hanno bisogno in modo rapido ed efficiente, aumentando in ultima analisi i tassi di soddisfazione e di conversione.

Per impostare un attributo di prodotto come facet, è necessario che siano impostate le seguenti [proprietà](facets-add.md#step-1-add-a-facet):

- **[!UICONTROL Use in Search]** -  `Yes`
- **[!UICONTROL Use in Layered Navigation]** -  `Filterable (with results)`
- **[!UICONTROL Use in Search Results Layered Navigation]** -  `Yes`

#### Suggerimenti per ottimizzare i facet

- Determina gli attributi più rilevanti e utili per i tuoi prodotti, ad esempio titolo, categoria, marchio, fascia di prezzo, colore e dimensione e impostali come [facet dinamici](facets-type.md). 
- Imposta e ordina gli attributi del prodotto che sono coerenti all’interno del catalogo e altamente rilevanti per i tuoi prodotti, in modo da migliorare la rilevanza e le funzionalità di filtro per gli acquirenti.
- Assicurati che le etichette dei facet siano facili da comprendere e denominate in modo coerente all’interno del sito. Ad esempio, utilizza &quot;Fascia di prezzo&quot; invece di &quot;Costo&quot;.
- Evita di sopraffare gli acquirenti limitando il numero di sfaccettature a quelle più importanti. Troppe opzioni possono causare affaticamento decisionale. Per impostazione predefinita, [!DNL Live Search] è limitato a un massimo di 100 attributi configurati come facet e 30 bucket restituiti all&#39;interno di ogni facet. Ulteriori informazioni sulle [limitazioni del facet](boundaries-limits.md#facets). 
- Consenti agli acquirenti di selezionare più criteri di filtro contemporaneamente per perfezionare i risultati. Ad esempio, consentendo agli acquirenti di selezionare sia il rosso che il blu.
- Visualizza il numero di prodotti disponibili accanto a ogni opzione di sfaccettatura per dare agli acquirenti un&#39;idea dei risultati di ricerca che possono aspettarsi.
- Implementa sezioni facet comprimibili per mantenere l’interfaccia pulita e gestibile, soprattutto sui dispositivi mobili.
- Consenti agli acquirenti di reimpostare facilmente singoli facet o tutti i filtri selezionati per avviare una nuova ricerca.

Ulteriori informazioni sui facet:

- [Tipi di facet](facets-type.md)
- [Aggiungi facet](facets-add.md)
- [Gestione facet](facets-manage.md) (modifica, fissaggio di un facet, eliminazione, pubblicazione)
- [Fatturazione del prezzo](settings.md#price-faceting)

## Migliorare la rilevanza dei risultati di ricerca

Questa sezione illustra come migliorare la rilevanza dei risultati di ricerca implementando regole di ricerca efficaci e utilizzando i metadati del prodotto per garantire che sia possibile eseguire ricerche in attributi precisi e dettagliati.

### Immagini

Assicurati che i prodotti secondari dei prodotti configurabili dispongano di immagini con i ruoli corretti. Se si dispone di prodotti principali o secondari, il risultato della ricerca potrebbe non contenere immagini.

>[!NOTE]
>
>Le immagini nei risultati di ricerca possono essere diverse a seconda del termine di ricerca. Se il termine di ricerca determina che un prodotto secondario è più rilevante, verranno utilizzate le immagini del prodotto secondario anziché le immagini del prodotto principale.

### Cerca regole

Per ottimizzare il tasso di conversione e i ricavi, devi implementare regole di ricerca efficaci. Regola le classificazioni dei prodotti in base ai dati di vendita, ai livelli di magazzino e alle promozioni con [Ricerca merchandising](rules.md).

È fondamentale stabilire una regola di ricerca predefinita ben ponderata. La [regola predefinita](rules.md#default-rule) determina il modo in cui i risultati della ricerca vengono inizialmente ordinati e visualizzati agli acquirenti, migliorando la loro esperienza complessiva e aumentando la probabilità di acquisto. Il monitoraggio regolare e l&#39;adeguamento di questa regola garantiscono che continui a soddisfare le esigenze dei clienti e gli obiettivi aziendali in modo efficace.

#### Suggerimenti per ottimizzare le regole di ricerca

- Aggiungi o incrementa prodotti con elevati volumi di vendita o attività di vendita recenti.
- Dai priorità ai prodotti con valutazioni elevate e recensioni positive.
- Assicurati che gli articoli in magazzino abbiano una classificazione più alta.
- Dare leggermente priorità ai prodotti con margini di profitto più elevati senza compromettere la rilevanza.
- Evidenzia i prodotti in vendita o inclusi nelle promozioni speciali.
- Impostare automaticamente le regole di ricerca durante i periodi di promozione o di vendita utilizzando l&#39;intervallo di date durante il periodo di promozione.
- Personalizza i risultati della ricerca in base al comportamento dei singoli acquirenti utilizzando [classificazione intelligente](rules-add.md#intelligent-ranking), ad esempio &quot;consigliato per te&quot;, &quot;più visualizzato&quot; e così via. Per personalizzare il comportamento dell’acquirente, devi assicurarti che l’evento sia implementato correttamente. Per i commercianti Luma, l’evento è disponibile come strumento predefinito. Per le implementazioni headless o personalizzate, devi [implementare eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/) in base alle tue esigenze specifiche.

Ulteriori informazioni sulle regole di ricerca:

- [Area di lavoro merchandising](rules-workspace.md#set-the-scope)
- [Requisiti](rules.md#requirements)
- [Regola di ricerca predefinita](rules.md#default-rule)
- Gestire le regole di ricerca
   - [Crea](rules-add.md)
   - [Modifica, visualizza, elimina](rules-manage.md)
- Raccolta dati
   - [[!DNL Live Search] eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)
   - [Agente di raccolta eventi Adobe Commerce](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)
   - [Eventi Commerce GitHub](https://github.com/adobe/commerce-events/tree/main/examples) 

### Sfruttare i metadati del prodotto

Assicurati che gli attributi di prodotto precisi e dettagliati siano [configurati come ricercabili](workspace.md#set-attributes-as-searchable). Tieni presente che gli attributi SKU, nome e categoria sono ricercabili per impostazione predefinita e non possono essere esclusi dalla ricerca. Per ottenere risultati ottimali, non utilizzare spazi negli SKU.

Per aumentare la rilevanza della ricerca, assegnare un peso a ogni attributo ricercabile. Gli attributi con un peso maggiore dovrebbero apparire più in alto nei risultati della ricerca. L’ordinamento in base alla rilevanza è influenzato da più criteri, ad esempio il peso della ricerca. Ciò significa che a volte gli attributi con un peso di ricerca inferiore possono comunque avere maggiore rilevanza degli attributi con un peso di ricerca maggiore. Altri criteri possono includere il numero di corrispondenze in un dato attributo, la posizione del termine di ricerca trovato e la struttura generale del testo prima e dopo un termine di ricerca.

Assicurati che ogni prodotto abbia contenuti rilevanti all’interno di ogni attributo ricercabile. Si sconsiglia di impostare un attributo come ricercabile se contiene grandi quantità di contenuto, in quanto ciò può ridurre la rilevanza dei risultati di ricerca.

Ulteriori informazioni sugli attributi del prodotto per la ricerca:

- [Imposta attributi come ricercabili](workspace.md#set-attributes-as-searchable)
- [Assegna peso agli attributi](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results#weighted-search)

## Monitoraggio dei risultati di ricerca

Per ottimizzare i risultati della ricerca con [!DNL Live Search], monitorare gli indicatori di prestazioni chiave (KPI, Key Performance Indicators) pertinenti, ad esempio query univoche, posizione media dei clic, tassi di click-through, tasso di conversione e tasso di risultati zero, per capire come gli acquirenti interagiscono con la funzionalità di ricerca. Questi dati ti aiutano ad aggiornare e perfezionare regolarmente le regole di ricerca.

È possibile monitorare questi KPI all&#39;interno dell&#39;[!DNL Live Search] [Area di lavoro prestazioni](performance.md) in cui sono disponibili le metriche seguenti: 

- **Ricerche univoche** - Numero di query di ricerca distinte eseguite sul sito [!DNL Commerce]. Ogni ricerca univoca viene conteggiata una sola volta, anche se viene ripetuta più volte dallo stesso acquirente o da acquirenti diversi. Questa metrica ti aiuta a comprendere la diversità dei termini di ricerca utilizzati dai clienti e fornisce informazioni approfondite sui prodotti o sulle informazioni che gli acquirenti stanno cercando. Il tracciamento delle ricerche univoche consente di:

   - Identifica le tendenze di ricerca più comuni e gli elementi cercati di frequente.
   - Rileva potenziali lacune nel catalogo dei prodotti o nel contenuto.
   - Ottimizza la funzionalità di ricerca aggiungendo [sinonimi](synonyms.md), creando o aggiornando le regole di ricerca.

- **Posizione media clic** - Indica che la posizione media dei risultati della ricerca su cui gli acquirenti hanno fatto clic dopo aver eseguito una query di ricerca sul sito. Questa metrica fornisce informazioni sulla rilevanza e l’efficacia dei risultati della ricerca.

  Una posizione di clic media più bassa (più vicina a 1) suggerisce che gli acquirenti trovano rapidamente i risultati rilevanti, indicando che la tua strategia di ricerca è efficace. Ti aiuta a capire il comportamento degli acquirenti e fino a che punto sono disposti a scorrere per trovare il prodotto desiderato. Se la posizione di clic media è alta, potrebbe indicare che i risultati più rilevanti non vengono visualizzati nella parte superiore, il che richiede una revisione e un’ottimizzazione della strategia di ricerca.

- **Tasso di click-through (CTR)** - Misura la percentuale di acquirenti che fanno clic su un risultato di ricerca dopo aver eseguito una query di ricerca. Un CTR elevato indica che i risultati della ricerca sono pertinenti e attraenti per gli acquirenti, mentre stanno cliccando sui risultati che trovano. Il monitoraggio del CTR può aiutare a identificare le aree da migliorare. Un CTR basso può suggerire che i risultati della ricerca non corrispondono all&#39;intento dell&#39;acquirente, rendendo necessario perfezionare le regole di ricerca, migliorare i dati dei prodotti o migliorare la presentazione dei risultati.

- **Tasso di conversione**: indica l&#39;efficacia della funzionalità di ricerca nel promuovere le vendite e raggiungere gli obiettivi aziendali. Riflette l&#39;efficacia complessiva della funzionalità di ricerca nel soddisfare le esigenze dei clienti e facilitare un&#39;esperienza di acquisto fluida. Un alto tasso di conversione indica che i risultati della ricerca sono altamente pertinenti e persuasivi, portando gli acquirenti a completare gli acquisti. Se il tasso di conversione è basso, può suggerire problemi relativi alla rilevanza della ricerca, alla disponibilità del prodotto o al percorso complessivo di acquirenti dalla ricerca all’acquisto.

- **Nessun risultato** - Misura la percentuale di query di ricerca sul sito [!DNL Commerce] che non restituiscono alcun risultato. Questa metrica è fondamentale per comprendere quanto spesso le ricerche degli acquirenti non hanno esito positivo e può fornire informazioni su potenziali lacune nel catalogo dei prodotti o nella configurazione della ricerca. Un elevato tasso di zero risultati può frustrare gli acquirenti, portando a una scarsa esperienza di acquisto e a una potenziale perdita di clienti. Può indicare prodotti o categorie mancanti nel catalogo che gli acquirenti stanno cercando, guidando le decisioni sull’inventario e sull’elenco dei prodotti.

  Per ridurre la percentuale di risultati pari a zero, puoi effettuare le seguenti operazioni:

   - Offri termini di ricerca alternativi o correlati, ad esempio [sinonimi](synonyms.md) quando non vengono trovate corrispondenze esatte.
   - Esamina regolarmente le query senza risultati per identificare i pattern e apportare le modifiche necessarie al catalogo dei prodotti e alle impostazioni di ricerca.

- **Risultati popolari**: possono migliorare in modo significativo i risultati della ricerca allineandoli alle preferenze e ai comportamenti degli acquirenti.

Puoi utilizzare questi dati di metrica per ottimizzare la funzionalità di ricerca nei seguenti modi:

- Implementa le regole per classificare automaticamente i prodotti più popolari più in alto nei risultati di ricerca. Ai prodotti su cui si fa clic frequentemente o acquistati può essere data priorità per essere visualizzati nella parte superiore. Cura manualmente gli elenchi dei prodotti più popolari per specifiche query di ricerca e assicurati che questi elementi siano visualizzati in modo evidente.
- Evidenzia i prodotti attualmente in tendenza o che hanno recentemente registrato un picco di popolarità. Questo può essere particolarmente efficace durante gli eventi stagionali, le vacanze o i periodi promozionali. A questo scopo, utilizza la classificazione intelligente che si adatta meglio al tuo caso d’uso e alle tue esigenze aziendali durante la configurazione di una regola di ricerca.
- Evidenzia i filtri o i facet più comuni, se gli acquirenti spesso filtrano in base a determinati marchi o gamme di prezzo, rendi tali opzioni più evidenti fissando i facet e ordinandoli di conseguenza.
- Quando una ricerca restituisce zero risultati, utilizza i dati dei risultati più comuni per suggerire prodotti alternativi o categorie correlate che hanno un elevato coinvolgimento degli acquirenti.
- Analizza i termini di ricerca più diffusi e i dati di prodotto per identificare importanti parole chiave. Ottimizza gli attributi ricercabili del prodotto con queste parole chiave per migliorare la rilevanza della ricerca.
- Analizza regolarmente i dati dei risultati per comprendere le tendenze in evoluzione, le preferenze e i comportamenti degli acquirenti, identificare i termini di ricerca principali e rilevare eventuali problemi. Utilizza questo ciclo di feedback per perfezionare e migliorare continuamente le regole di ricerca e le offerte di prodotti

Per ottenere i dati corretti all&#39;interno del report [!DNL Live Search], è necessario assicurarsi che l&#39;evento sia implementato correttamente. Per i commercianti Luma, l’evento è disponibile come strumento predefinito. Per le implementazioni headless o personalizzate, devi [implementare eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/) in base alle tue esigenze specifiche.
