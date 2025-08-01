---
title: Prestazioni di ricerca
description: La pagina Prestazioni di ricerca fornisce ad insight i termini di ricerca utilizzati dagli acquirenti.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: 75b43c6f-d876-4379-ad70-5c2a2f29a5ac
source-git-commit: b8b7af1119163589b7d83654b13edae656fea339
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 0%

---

# Prestazioni di ricerca

La pagina *Prestazioni di ricerca* fornisce ad insight i termini di ricerca utilizzati dagli acquirenti. Le informazioni possono essere utilizzate per identificare le tendenze, aumentare il click-through e migliorare il tasso di conversione. La pagina Prestazioni di ricerca fornisce un’istantanea delle metriche di ricerca per un intervallo di date specifico e include i seguenti rapporti:

- Ricerche univoche
- Posizione media clic
- Percentuale di click-through
- Tasso di conversione
- Percentuale risultati zero

![Prestazioni ricerca](../assets/search-performance.png){zoomable="yes"}

>[!IMPORTANT]
>
>Se non trovi alcuna metrica delle prestazioni di ricerca, assicurati che i dati dell&#39;evento di ricerca siano [raccolti](../setup/events/overview.md).

## Scegli la **visualizzazione catalogo**

Seleziona la [vista catalogo](../setup/catalog-view.md) per visualizzare risultati specifici delle prestazioni di ricerca.

![Visualizzazione catalogo](../assets/catalog-view.png)

## Visualizzare un rapporto

Fare clic sul calendario ed eseguire una delle operazioni seguenti:

- Per specificare una singola data, fare doppio clic sulla data nel calendario.
- Per specificare un intervallo di date, fare clic sulla prima e sull&#39;ultima data del calendario.

>[!NOTE]
>
>L’intervallo di date non può superare un anno.

Fai clic su **[!UICONTROL Export to CSV]** per generare un file CSV delle prestazioni di ricerca.

## Come migliorare le prestazioni di ricerca

La sezione seguente fornisce le strategie da utilizzare per migliorare la funzionalità di ricerca del sito, garantendo un&#39;esperienza di acquisto fluida ed efficiente che massimizza i tassi di conversione.

Esistono diversi fattori chiave che determinano la rilevanza e l’efficacia dei risultati della ricerca:

- Dati di prodotto ben strutturati garantiscono che gli algoritmi di ricerca possano far corrispondere efficacemente i prodotti alle query. I dati sui prodotti di bassa qualità portano a risultati di ricerca meno rilevanti. Per avere un impatto diretto sul successo della strategia di merchandising:
   - Imposta gli [attributi corretti come ricercabili](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata) con il relativo peso.
   - Assicurati che i dati all’interno di tali attributi siano pertinenti.
- Un’esperienza di ricerca ben progettata crea fiducia nei clienti e infonde fiducia nel fatto che troveranno ciò di cui hanno bisogno.
- Le regole di ricerca sono fondamentali in quanto possono aumentare la visibilità di alcuni prodotti in base alla popolarità, ai nuovi arrivi, ai criteri promozionali o a qualsiasi altra strategia di merchandising per soddisfare le esigenze aziendali.
- La navigazione a facet consente ai clienti di perfezionare le ricerche e ottenere rapidamente risultati rilevanti.

### Monitoraggio dei risultati di ricerca

Per ottimizzare i risultati della ricerca con [!DNL Adobe Commerce Optimizer], monitorare gli indicatori di prestazioni chiave (KPI, Key Performance Indicators) pertinenti, ad esempio query univoche, posizione media dei clic, tassi di click-through, tasso di conversione e tasso di risultati zero, per capire come gli acquirenti interagiscono con la funzionalità di ricerca. Questi dati ti aiutano ad aggiornare e perfezionare regolarmente le regole di ricerca.

- **Ricerche univoche** - Numero di query di ricerca distinte eseguite sul sito [!DNL Adobe Commerce Optimizer]. Ogni ricerca univoca viene conteggiata una sola volta, anche se viene ripetuta più volte dallo stesso acquirente o da acquirenti diversi. Questa metrica ti aiuta a comprendere la diversità dei termini di ricerca utilizzati dai clienti e fornisce informazioni approfondite sui prodotti o sulle informazioni che gli acquirenti stanno cercando. Il tracciamento delle ricerche univoche consente di:

   - Identifica le tendenze di ricerca più comuni e gli elementi cercati di frequente.
   - Rileva potenziali lacune nel catalogo dei prodotti o nel contenuto.
   - Ottimizza la funzionalità di ricerca aggiungendo [sinonimi](../merchandising/synonyms/overview.md), creando o aggiornando [regole di ricerca](../merchandising/rules/overview.md).

- **Posizione media clic** - Indica che la posizione media dei risultati della ricerca su cui gli acquirenti hanno fatto clic dopo aver eseguito una query di ricerca sul sito. Questa metrica fornisce informazioni sulla rilevanza e l’efficacia dei risultati della ricerca.

  Una posizione di clic media più bassa (più vicina a 1) suggerisce che gli acquirenti trovano rapidamente i risultati rilevanti, indicando che la tua strategia di ricerca è efficace. Ti aiuta a capire il comportamento degli acquirenti e fino a che punto sono disposti a scorrere per trovare il prodotto desiderato. Se la posizione di clic media è alta, potrebbe indicare che i risultati più rilevanti non vengono visualizzati nella parte superiore, il che richiede una revisione e un’ottimizzazione della strategia di ricerca.

- **Tasso di click-through (CTR)** - Misura la percentuale di acquirenti che fanno clic su un risultato di ricerca dopo aver eseguito una query di ricerca. Un CTR elevato indica che i risultati della ricerca sono pertinenti e attraenti per gli acquirenti, mentre stanno cliccando sui risultati che trovano. Il monitoraggio del CTR può aiutare a identificare le aree da migliorare. Un CTR basso può suggerire che i risultati della ricerca non corrispondono all&#39;intento dell&#39;acquirente, rendendo necessario perfezionare le regole di ricerca, migliorare i dati dei prodotti o migliorare la presentazione dei risultati.

- **Tasso di conversione**: indica l&#39;efficacia della funzionalità di ricerca nel promuovere le vendite e raggiungere gli obiettivi aziendali. Riflette l&#39;efficacia complessiva della funzionalità di ricerca nel soddisfare le esigenze dei clienti e facilitare un&#39;esperienza di acquisto fluida. Un alto tasso di conversione indica che i risultati della ricerca sono altamente pertinenti e persuasivi, portando gli acquirenti a completare gli acquisti. Se il tasso di conversione è basso, può suggerire problemi relativi alla rilevanza della ricerca, alla disponibilità del prodotto o al percorso complessivo di acquirenti dalla ricerca all’acquisto.

- **Percentuale zero risultati** - Misura la percentuale di query di ricerca sul sito [!DNL Adobe Commerce Optimizer] che non restituiscono risultati. Questa metrica è fondamentale per comprendere quanto spesso le ricerche degli acquirenti non hanno esito positivo e può fornire informazioni su potenziali lacune nel catalogo dei prodotti o nella configurazione della ricerca. Un elevato tasso di zero risultati può frustrare gli acquirenti, portando a una scarsa esperienza di acquisto e a una potenziale perdita di clienti. Può indicare prodotti o categorie mancanti nel catalogo che gli acquirenti stanno cercando, guidando le decisioni sull’inventario e sull’elenco dei prodotti.

  Per ridurre la percentuale di risultati pari a zero, puoi effettuare le seguenti operazioni:

   - Offri termini di ricerca alternativi o correlati, ad esempio [sinonimi](../merchandising/synonyms/overview.md) quando non vengono trovate corrispondenze esatte.
   - Esamina regolarmente le query senza risultati per identificare i pattern e apportare le modifiche necessarie al catalogo dei prodotti e alle impostazioni di ricerca.

Puoi utilizzare questi dati di metrica per ottimizzare la funzionalità di ricerca nei seguenti modi:

- Implementa le regole per classificare automaticamente i prodotti più popolari più in alto nei risultati di ricerca. Ai prodotti su cui si fa clic frequentemente o acquistati può essere data priorità per essere visualizzati nella parte superiore. Cura manualmente gli elenchi dei prodotti più popolari per specifiche query di ricerca e assicurati che questi elementi siano visualizzati in modo evidente.
- Evidenzia i prodotti attualmente in tendenza o che hanno recentemente registrato un picco di popolarità. Questo può essere particolarmente efficace durante gli eventi stagionali, le vacanze o i periodi promozionali. A questo scopo, utilizza la classificazione intelligente che si adatta meglio al tuo caso d’uso e alle tue esigenze aziendali durante la configurazione di una regola di ricerca.
- Evidenzia i filtri o i facet più comuni, se gli acquirenti spesso filtrano in base a determinati marchi o gamme di prezzo, rendi tali opzioni più evidenti fissando i facet e ordinandoli di conseguenza.
- Quando una ricerca restituisce zero risultati, utilizza i dati dei risultati più comuni per suggerire prodotti alternativi o categorie correlate che hanno un elevato coinvolgimento degli acquirenti.
- Analizza i termini di ricerca più diffusi e i dati di prodotto per identificare importanti parole chiave. Ottimizza gli attributi ricercabili del prodotto con queste parole chiave per migliorare la rilevanza della ricerca.
- Analizza regolarmente i dati dei risultati per comprendere le tendenze in evoluzione, le preferenze e i comportamenti degli acquirenti, identificare i termini di ricerca principali e rilevare eventuali problemi. Utilizza questo ciclo di feedback per perfezionare e migliorare continuamente le regole di ricerca e le offerte di prodotti

## Ottimizzazione della funzionalità di ricerca

Per ottimizzare la funzionalità di ricerca, utilizza [sinonimi e ortografia](../merchandising/synonyms/overview.md) per garantire che gli acquirenti trovino i prodotti anche se utilizzano parole diverse e [facet](../merchandising/facets/overview.md) per consentire agli acquirenti di limitare i risultati della ricerca.

## Migliorare la rilevanza dei risultati di ricerca

Per migliorare la pertinenza dei risultati della ricerca, implementa [regole di ricerca](../merchandising/rules/overview.md) efficaci e utilizza i metadati del prodotto per garantire che gli [attributi siano precisi e dettagliati](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata).

### Immagini

Assicurati che i prodotti secondari dei prodotti configurabili dispongano di immagini con i ruoli corretti. Se si dispone di prodotti principali o secondari, il risultato della ricerca potrebbe non contenere immagini.

>[!NOTE]
>
>Le immagini nei risultati di ricerca possono essere diverse a seconda del termine di ricerca. Se il termine di ricerca determina che un prodotto secondario è più rilevante, verranno utilizzate le immagini del prodotto secondario anziché le immagini del prodotto principale.

### Sfruttare i metadati del prodotto

Assicurati che gli attributi del prodotto [ precisi e dettagliati siano impostati come ricercabili](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata). Tieni presente che gli attributi SKU, nome e categoria sono ricercabili per impostazione predefinita e non possono essere esclusi dalla ricerca. Per ottenere risultati ottimali, non utilizzare spazi negli SKU.

Per aumentare la rilevanza della ricerca, assegnare un peso a ogni attributo ricercabile. Gli attributi con un peso maggiore dovrebbero apparire più in alto nei risultati della ricerca. L’ordinamento in base alla rilevanza è influenzato da più criteri, ad esempio il peso della ricerca. Ciò significa che a volte gli attributi con un peso di ricerca inferiore possono comunque avere maggiore rilevanza degli attributi con un peso di ricerca maggiore. Altri criteri possono includere il numero di corrispondenze in un dato attributo, la posizione del termine di ricerca trovato e la struttura generale del testo prima e dopo un termine di ricerca.

Assicurati che ogni prodotto abbia contenuti rilevanti all’interno di ogni attributo ricercabile. Si sconsiglia di impostare un attributo come ricercabile se contiene grandi quantità di contenuto, in quanto ciò può ridurre la rilevanza dei risultati di ricerca.

Ulteriori informazioni sugli attributi del prodotto per la ricerca:

- [Imposta gli attributi come ricercabili](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)
- [Assegna peso agli attributi](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)

## Descrizioni dei campi

| Dati snapshot | Descrizione |
|--- |--- |
| Ricerche univoche | Numero totale di ricerche univoche per l’intervallo di date specificato. Le ricerche multiple dello stesso acquirente, anche se per la stessa query, sono considerate univoche se inviate a più di un&#39;ora di distanza. |
| Percentuale di click-through | La percentuale di ricerche che si concludono con il cliente che fa clic su un prodotto. Ad esempio, il tasso di click-through è del 50% se l’acquirente cerca &quot;pantaloni&quot; e &quot;camicia&quot; e poi fa clic su un risultato nella ricerca &quot;camicia&quot;. |
| Tasso di conversione | La percentuale di prodotti acquistati dal cliente rispetto al numero di prodotti su cui il cliente fa clic per l’intervallo di date specificato. Ad esempio, il tasso di conversione dell’interazione è del 100% se l’acquirente visualizza sei prodotti nella finestra a comparsa, fa clic su uno e effettua un acquisto. <br /><br />Il tasso di conversione non è influenzato dal numero di visualizzazioni di un determinato prodotto. Ad esempio, il tasso di conversione rimane lo stesso se l’acquirente utilizza la ricerca, ma non fa clic su alcun prodotto. |
| Percentuale risultati zero | Percentuale di ricerche univoche che non restituisce alcun risultato per l’intervallo di date specificato. Ad esempio, il tasso di risultati zero è 66,67% se il cliente cerca &quot;fjjajfjfjf&quot; due volte (senza risultati) e &quot;pantaloni&quot; una volta (con risultati). |
| Media posizione clic | Posizione relativa del tasso medio di click-through basato su ricerche univoche per l’intervallo di date specificato. |

| Rapporti | Descrizione |
|--- |--- |
| Nessun risultato | Elenca le query di ricerca che non restituiscono risultati e il numero di volte in cui vengono utilizzate durante l’intervallo di date specificato. Limite rapporto: primi 500 termini |
| Risultati comuni | Elenca i nomi dei prodotti che hanno ricevuto il maggior numero di visualizzazioni durante l’intervallo di date specificato. I risultati più comuni vengono calcolati solo in base alle impression e non sono influenzati dal numero di clic o ricavi generati. Limite rapporto: primi 500 termini |
| Ricerche univoche | Elenca le query di ricerca univoche utilizzate durante l’intervallo di date specificato. I dati del report vengono calcolati nello stesso modo dei dati univoci dello snapshot di ricerca. Se un acquirente digita la stessa query di ricerca due volte, ma a più di un’ora di distanza, la ricerca viene considerata come due ricerche univoche. Limite rapporto: primi 500 termini |
