---
title: Metriche di successo
description: Le metriche di successo forniscono ad insight le metriche delle prestazioni chiave per il tuo archivio  [!DNL Adobe Commerce Optimizer] .
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: 7202a531-fec3-4698-89b9-6bdbcc37015e
source-git-commit: 4e85d70dc1b099a5b40a807a76ca589aa9a28f07
workflow-type: tm+mt
source-wordcount: '2599'
ht-degree: 0%

---

# Metriche di successo

Questa pagina fornisce una panoramica delle metriche delle prestazioni chiave per l&#39;archivio [!DNL Adobe Commerce Optimizer]. L&#39;obiettivo è quello di comprendere rapidamente i risultati dell&#39;implementazione di [!DNL Adobe Commerce Optimizer], aiutare te e il tuo team a identificare le opportunità di crescita ed evidenziare le aree da ottimizzare.

![Rapporto sulle metriche di successo](../assets/success-metrics.png)

Le metriche nel rapporto vengono estratte dai dati dell’evento vetrina. [Ulteriori informazioni](../setup/events/overview.md) sui dati dell&#39;evento raccolti.

## Informazioni sulle metriche

Il rapporto sulle metriche di successo fornisce informazioni fruibili in cinque aree prestazionali chiave che influiscono direttamente sui risultati aziendali. Ogni metrica rivela i pattern nel comportamento del cliente e archivia le prestazioni che consentono di individuare opportunità e affrontare sfide. Sfrutta queste informazioni per favorire decisioni più intelligenti e ottimizzare la tua esperienza di e-commerce.

**Elementi di rilievo** riepiloga le metriche chiave da ogni area delle prestazioni. Utilizza questa sezione per identificare rapidamente le maggiori opportunità di miglioramento.

Gli indicatori chiave di prestazione sono:

- **Ricavi**—La metrica finanziaria principale che mostra le prestazioni totali delle vendite.
- **Conversione** - Percentuale di visitatori che hanno completato gli acquisti.
- **Coinvolgimento**: il livello di interazione degli utenti con il sito.
- **Acquisizione**: l&#39;efficacia delle attività di acquisizione dei clienti.
- **Percentuale non recapitate**: la percentuale di visitatori che abbandonano dopo aver visualizzato una sola pagina.

### Aggiornamento e precisione dei dati

**Frequenza di aggiornamento:** i dati delle metriche di successo vengono elaborati e aggiornati regolarmente durante la raccolta ed elaborazione degli eventi storefront.

**Quando controllare le metriche:** Per un&#39;analisi delle tendenze più accurata, esaminare le metriche dopo che è trascorso un tempo sufficiente per raccogliere dati significativi. Le fluttuazioni giornaliere sono normali; concentrarsi sulle tendenze settimanali o mensili per le decisioni strategiche.

**Precisione dei dati:** le metriche sono calcolate in base alle interazioni effettive del cliente acquisite tramite eventi storefront. Assicurati che nell&#39;archivio sia configurato correttamente il [tracciamento eventi](../setup/events/overview.md) per la generazione di rapporti accurati.

## Generare un rapporto

1. Dalla barra a sinistra, seleziona **Metriche di successo**.
1. In **Configurazione report** specificare l&#39;**Intervallo date**, l&#39;**Origine catalogo**, in base alle impostazioni internazionali, e la **Valuta**.
1. Fare clic su **[!UICONTROL Apply]**.

   Le **attività principali**, **Ricavi**, **Conversione**, **Coinvolgimento**, **Acquisizione** e **Percentuale non recapitate** sono state tutte aggiornate in base alla configurazione del report.

1. Fare clic su **[!UICONTROL Export]** per salvare il report come PDF.

## Utilizzo congiunto di metriche di successo e Sites Optimizer

Le metriche di successo e Sites Optimizer ([Opportunities](opportunities.md)) sono strumenti complementari progettati per funzionare insieme, che consentono di migliorare le prestazioni del sito di e-commerce. Comprendere la differenza tra queste funzioni ti aiuta a prendere decisioni migliori e a raggiungere risultati misurabili.

### Differenze chiave

| Formato | Metriche di successo | Sites Optimizer (opportunità) |
|---|---|---|
| **Scopo** | Misura prestazioni e risultati | Identifica i problemi e fornisce consigli |
| **Tipo** | Dashboard analitico | Rilevamento proattivo dei problemi |
| **Elementi visualizzati** | Indicatori prestazioni chiave (Ricavi, Conversione, Coinvolgimento, Acquisizione, Percentuale non recapitate) | Raccomandazioni basate sull’intelligenza artificiale per problemi che influiscono sulle prestazioni del sito |
| **Origine dati** | Dati evento vetrina | Cataloghi di prodotti, registri di ricerca, dati dei consigli |
| **Usa quando** | Desideri tenere traccia dei risultati nel tempo | Desideri identificare e risolvere problemi specifici |

### Come utilizzare insieme queste funzioni

L’approccio più efficace combina entrambi gli strumenti in un ciclo di miglioramento continuo:

1. **Misura con metriche di successo**: inizia consultando la dashboard Metriche di successo per comprendere le prestazioni correnti. Identifica i KPI da migliorare (ad esempio, tasso di conversione basso o tasso di mancato recapito elevato).

1. **Esegui diagnosi con opportunità**: passa alla pagina Opportunità per individuare problemi specifici che potrebbero causare prestazioni insoddisfacenti. Sites Optimizer analizza il catalogo dei prodotti, i registri di ricerca e i dati dei consigli per identificare problemi quali dati di prodotto mancanti, scarsa rilevanza della ricerca o problemi di navigazione.

1. **Implementare i consigli**: segui i consigli basati sull&#39;intelligenza artificiale forniti in Opportunità per risolvere i problemi rilevati. Ad esempio, puoi risolvere i problemi relativi alla qualità dei dati dei prodotti, migliorare la SEO (Search Engine Optimization) o ottimizzare la ricerca e il rilevamento.

1. **Miglioramenti del tracciamento**: torna alle metriche di successo per monitorare come le modifiche influiscono sui KPI nel tempo. Utilizza il selettore dell’intervallo di date per confrontare le prestazioni prima e dopo l’implementazione di Recommendations.

1. **Itera e ottimizza**: continua questo ciclo utilizzando le opportunità per identificare nuovi problemi e le metriche di successo per misurare l&#39;impatto delle ottimizzazioni.

### Esempio di flusso di lavoro

Un commerciante nota che il tasso di conversione diminuisce nelle metriche di successo. Di seguito viene illustrato come utilizzare entrambe le funzioni per risolvere il problema:

1. **Identifica il problema**: il dashboard delle metriche di successo mostra un tasso di conversione sceso del 15% nell&#39;ultimo mese.

1. **Ricerca causa**: la pagina Opportunità presenta diversi problemi:
   - In più prodotti mancano gli attributi chiave che influiscono sulla rilevanza della ricerca.
   - Le query di ricerca più comuni restituiscono risultati insoddisfacenti.
   - Tempi di caricamento delle pagine lenti sulle pagine delle categorie.

1. **Azione**: il commerciante assegna priorità alla risoluzione dei problemi di qualità dei dati del prodotto, in quanto Sites Optimizer li classifica come opportunità ad alto impatto che influiscono sulla ricerca e sui consigli.

1. **Risultati delle misurazioni**: dopo aver aggiornato gli attributi del prodotto e implementato le modifiche consigliate, il commerciante monitora settimanalmente le metriche di successo. Nel mese successivo, il tasso di conversione aumenta del 12% e le metriche di coinvolgimento nelle ricerche migliorano in modo significativo.

1. **Continua a ottimizzare**: con il miglioramento del tasso di conversione, il commerciante sposta l&#39;attenzione sulla priorità successiva mostrata in Opportunità, ottimizzando la velocità di caricamento della pagina per ridurre il tasso di mancato recapito.

### Quando utilizzare ogni funzione

**Utilizzare le metriche di successo per:**

- Monitorare le prestazioni aziendali complessive.
- Misura l’impatto delle modifiche nel tempo.
- Identifica le aree della tua azienda che richiedono attenzione.
- Condividere rapporti sulle prestazioni con le parti interessate.
- Comprendere le tendenze del comportamento dei clienti.

**Utilizzare Sites Optimizer (Opportunità) quando si desidera:**

- Scopri problemi specifici che influiscono sulle prestazioni.
- Consigli utili per risolvere i problemi.
- Scopri perché alcune metriche sono in calo.
- Dai priorità alle ottimizzazioni da affrontare per prime.
- Sfrutta l’intelligenza artificiale per identificare i problemi che potresti perdere manualmente.

Insieme, queste funzionalità forniscono una soluzione completa: le metriche di successo indicano *cosa* sta accadendo, mentre Sites Optimizer indica *perché* e *come correggerlo*.

## Passaggi successivi e strategie di ottimizzazione

Utilizza i dati delle metriche di successo per individuare opportunità di miglioramento e implementare strategie di ottimizzazione mirate. Le sezioni seguenti forniscono indicazioni specifiche e fruibili per ogni area metrica.

>[!BEGINTABS]

>[!TAB Ottimizzazione ricavi]

Per i ricavi, l&#39;obiettivo è aumentare le vendite totali e il valore medio dell&#39;ordine.

![Ricavi metriche di successo](../assets/revenue.png)

### Informazioni sulla metrica Ricavi

**Cosa viene misurato:** reddito totale generato dal tuo negozio durante il periodo di tempo selezionato.

**Modalità di calcolo:** I ricavi sono la somma di tutti gli ordini completati (prezzo base × quantità) per tutti i prodotti venduti durante il periodo di reporting. Il calcolo utilizza i dati di `place-order` eventi acquisiti nella vetrina.

>[!IMPORTANT]
>
>I calcoli dei ricavi escludono gli ordini annullati, le restituzioni e gli ordini in cui l&#39;evento `place-order` non è stato acquisito. Gli eventi potrebbero non essere presenti a causa di impostazioni di consenso, problemi del browser (ad blocker, errori di script) o errori di elaborazione tecnica.

**Formula:**

```
Total Revenue = Sum of (Product Base Price × Quantity) for all completed orders
```

**Origine dati:** eventi Storefront (in particolare `place-order` eventi)

**Elementi inclusi:**

- Tutti gli ordini completati durante l’intervallo di date selezionato.
- Prezzi del prodotto di base moltiplicati per le quantità acquistate.
- Ricavi da tutti i canali di vendita registrati da Commerce Optimizer.

**Note importanti:**

- I ricavi vengono calcolati in base ai prezzi base rilevati negli eventi di vetrina.
- Il periodo di reporting è determinato dall’intervallo di date selezionato nella configurazione del rapporto.
- Le metriche dei ricavi vengono aggiornate durante l’elaborazione dei nuovi eventi dell’ordine.

### Strategie

- **Implementa consigli basati sull&#39;intelligenza artificiale**: utilizza il motore di consigli dell&#39;ottimizzatore per rendere visibili prodotti rilevanti che aumentano i tassi di conversione. Distribuisci *I clienti che hanno visualizzato questo hanno visto anche* e *hanno acquistato questo/a tipo/i di consigli* per aumentare le opportunità di cross-selling.

- **Crea regole di merchandising**: incrementa i prodotti con margini elevati nei risultati di ricerca utilizzando [regole di merchandising](../merchandising/rules/overview.md). Aggiungi gli articoli più venduti ai primi risultati di ricerca per le query a traffico elevato.

- **Ottimizza l&#39;individuazione del prodotto**: utilizza [facet intelligenti](../merchandising/facets/overview.md) per aiutare i clienti a trovare i prodotti in modo più efficiente, aumentando i tassi di conversione e i ricavi.

- **Sfrutta le opportunità stagionali**: crea regole di merchandising basate sul tempo per promuovere articoli stagionali o promozionali durante i periodi di picco degli acquisti.

>[!TAB Miglioramento del tasso di conversione]

Per migliorare il tasso di conversione, l’obiettivo è convertire più visitatori in clienti.

![Tasso di conversione delle metriche di successo](../assets/conversion-rate.png)

### Informazioni sulla metrica del tasso di conversione

**Cosa misura:** la percentuale di visitatori che visualizzano i prodotti e poi completano un acquisto, indicando quanto il tuo negozio converte efficacemente i browser in acquirenti.

**Modalità di calcolo:** Il tasso di conversione confronta il numero di visitatori univoci che hanno acquistato prodotti con il numero di visitatori univoci che hanno visualizzato i prodotti.

**Formula:**

```
Conversion Rate = (Total Number of Orders ÷ Total Unique Visitors) × 100
```

**Origine dati:** eventi Storefront.

**Funzionamento:**

- **Le visualizzazioni dei prodotti** vengono tracciate quando i visitatori visualizzano le pagine dei prodotti (utilizzando `product-view` eventi).
- **Gli acquisti** vengono tracciati al completamento degli ordini (utilizzando `place-order` eventi).
- Il calcolo corrisponde agli utenti che hanno visualizzato prodotti specifici con quelli che li hanno acquistati.

**Note importanti:**

- Un visitatore che visualizza più prodotti ma effettua un acquisto conta come una conversione.
- La metrica tiene traccia dei visitatori univoci utilizzando identificatori basati su browser.
- Gli eventi di visualizzazione del prodotto includono sempre un clic, pertanto le visualizzazioni rappresentano un reale interesse dell’utente.

### Strategie

- **Ottimizza la rilevanza della ricerca**: implementa [sinonimi](../merchandising/synonyms/overview.md) per garantire che i clienti trovino ciò che stanno cercando, anche con termini di ricerca diversi. Utilizza il faceting dinamico per fornire opzioni di filtro pertinenti.

- **Posizionamento di consigli strategico**: distribuisci unità di consigli su pagine con traffico elevato, come le pagine dei dettagli del prodotto e le pagine delle categorie. Utilizza i *consigli più visualizzati* e *più acquistati* per creare attendibilità e urgenza.

- **Miglioramento della visibilità dei prodotti**: utilizza le regole di merchandising per garantire che i prodotti più venduti e con elevata conversione vengano visualizzati in primo piano nei risultati di ricerca.

- **Tipi di consigli per test A/B**: prova con diversi tipi di consigli e posizionamenti per trovare ciò che funziona meglio per il tuo pubblico.

>[!TAB Miglioramento del coinvolgimento]

Per migliorare il coinvolgimento, il tuo obiettivo è aumentare l&#39;interazione con il cliente e il tempo a disposizione sul sito.

![Coinvolgimento metriche di successo](../assets/engagement.png)

### Informazioni sulla metrica di coinvolgimento

**Misure:** interazione attiva degli utenti con il tuo archivio, tenendo traccia di azioni significative dalla navigazione iniziale fino al processo di pagamento.

**Modalità di calcolo:** Il coinvolgimento tiene traccia di tutte le interazioni che indicano la partecipazione attiva al tuo negozio, incluse la navigazione dei prodotti, le attività del carrello e le azioni di pagamento.

**Origine dati:** eventi Storefront

**Cosa conta come coinvolgimento:**

Il coinvolgimento include le seguenti categorie di eventi e azioni:

- **Interazioni prodotto:** visualizzazioni prodotto, clic prodotto e confronti prodotti.
- **Attività carrello:** aggiunta di elementi al carrello, aggiornamento delle quantità, rimozione di elementi.
- **Azioni di estrazione:** Avvio dell&#39;estrazione, completamento dei passaggi di estrazione.
- **Navigazione tra categorie:** Visualizzazione delle pagine delle categorie, filtro per facet.
- **Attività elenco desideri:** Aggiunta alla lista desideri, visualizzazione degli elementi della lista desideri.

**Dettagli tracciamento eventi:**

Il sistema tiene traccia del coinvolgimento quando gli eventi hanno:

- Categoria: `product`, `shopper`, `shopping-cart` o `checkout`.
- Proprietà: `Product`, `Checkout`, `Cart`, `Category` o `Wishlist`.

**Note importanti:**

- Un coinvolgimento maggiore è in genere correlato a tassi di conversione più elevati.
- Le metriche di coinvolgimento consentono di identificare gli utenti più attivi nel percorso.
- Utilizza i dati di coinvolgimento per ottimizzare le pagine a traffico elevato e migliorare l’esperienza utente.

### Strategie

- **Diversifica tipi di consigli**: evita di mostrare ripetutamente gli stessi consigli. Utilizza una combinazione di *Consigliati per te*, *Di tendenza* e *Visualizzati di recente* per mantenere il contenuto fresco e coinvolgente.

- **Implementa la ricerca intelligente**: utilizza il faceting dinamico basato sull&#39;intelligenza artificiale e la riclassificazione dei risultati per adattare i risultati della ricerca in tempo reale in base al comportamento dell&#39;acquirente.

- **Creazione di esperienze personalizzate**: distribuisci le unità &quot;Consigliato per te&quot; nella homepage e in tutto il percorso di clienti per fornire suggerimenti di prodotto personalizzati.

- **Ottimizza esperienza di ricerca**: utilizza i sinonimi per migliorare la rilevanza della ricerca e garantire che i clienti trovino rapidamente ciò che stanno cercando.

>[!TAB Crescita acquisizione]

Per acquisire una maggiore crescita, il tuo obiettivo è attrarre nuovi clienti e migliorare l&#39;efficienza di acquisizione.

![Acquisizione delle metriche di successo](../assets/acquisition.png)

### Informazioni sulla metrica di acquisizione

**Informazioni:** il numero di nuovi visitatori univoci che arrivano nel tuo negozio, consentendoti di comprendere l&#39;efficacia delle attività di marketing e acquisizione dei clienti.

**Modalità di calcolo:** l&#39;acquisizione conta i visitatori univoci in base agli identificatori del browser assegnati durante la loro prima visita al tuo store.

**Origine dati:** eventi Storefront.

**Funzionamento:**

- Il browser di ogni visitatore riceve un identificatore univoco (`domain_userid`) tramite un cookie di prime parti.
- I nuovi visitatori vengono identificati quando il loro indice di sessione è uguale a 1 (prima visita).
- Il sistema tiene traccia di questi identificatori per distinguere i nuovi visitatori da quelli di ritorno.

**Note importanti:**

Questo metodo di tracciamento presenta alcune limitazioni note:

- **Utenti multi-dispositivo:** la stessa persona che visita da diversi dispositivi (desktop, dispositivi mobili, tablet) o browser viene conteggiata come più visitatori univoci poiché ogni dispositivo e browser riceve un identificatore diverso.
- **Cancellazione cookie:** Gli utenti che cancellano i cookie del browser ricevono un nuovo identificatore e vengono di nuovo conteggiati come nuovi visitatori.
- **Impostazioni privacy:** Gli utenti con impostazioni di privacy rigide o i cookie bloccanti potrebbero non essere tracciati.

**Ideale per:**

- Tracciamento delle tendenze dei nuovi visitatori nel tempo.
- Analisi dell’efficacia delle campagne di marketing.
- Comprendere i modelli di crescita del traffico.

**Suggerimento per l&#39;interpretazione:** Anche se non perfettamente accurato a causa delle limitazioni di cui sopra, le metriche di acquisizione sono affidabili per identificare le tendenze e confrontare i periodi in cui la maggior parte degli utenti naviga sullo stesso dispositivo e non cancella frequentemente i cookie.

### Strategie

- **Sfrutta i dati sulle prestazioni di ricerca**: utilizza il report [prestazioni di ricerca](../manage-results/search-performance.md) per identificare i prodotti di tendenza e i termini di ricerca più comuni. Crea regole di merchandising per evidenziare questi elementi.

- **Ottimizza prestazioni consigli**: monitora le metriche di [prestazioni consigli](../manage-results/recommendation-performance.md) per identificare i tipi di consigli che generano più traffico e conversioni.

- **Evidenzia articoli nuovi e promozionali**: utilizza le regole di merchandising per promuovere nuovi prodotti o articoli promozionali nei risultati della ricerca per attirare l&#39;attenzione dei nuovi visitatori.

- **Tracciare le origini del traffico**: utilizza i dati dell&#39;evento per capire quali canali generano il traffico più importante e ottimizzare di conseguenza le tue attività di marketing.

>[!TAB Riduzione frequenza di mancato recapito]

Per ridurre il tasso di mancato recapito, l’obiettivo è mantenere i visitatori coinvolti e ridurre le visite a pagina singola.

![Percentuale mancati recapiti delle metriche di successo](../assets/bounce-rate.png)

### Informazioni sulla metrica del tasso di mancato recapito

**Misurazione:** la percentuale di visitatori che abbandonano il sito dopo aver visualizzato una sola pagina, indicando potenziali problemi di esperienza utente, rilevanza della pagina o coinvolgimento nel sito.

**Modalità di calcolo:** La percentuale di mancato recapito confronta le sessioni a pagina singola con il totale delle sessioni per determinare quale percentuale di visitatori lascia senza ulteriore interazione.

**Formula:**

```
Bounce Rate = (Number of Bounced Sessions ÷ Total Sessions) × 100
```

**Origine dati:** eventi Storefront.

**Funzionamento:**

- Una **sessione non recapitata** viene conteggiata quando un visitatore visualizza solo una pagina durante l&#39;intera visita.
- Il sistema tiene traccia delle visualizzazioni di pagina all’interno di ogni sessione per identificare le visite a pagina singola.
- Le sessioni sono determinate dall’attività dell’utente e dal tempo che intercorre tra le interazioni.

**Cause dei mancati recapiti:**

- Visitatori che accedono a pagine irrilevanti (ricerca con targeting o annuncio scarso).
- Tempi di caricamento delle pagine lenti.
- Esperienza utente scadente o navigazione confusa.
- Ricerca rapida delle informazioni senza necessità di ulteriori approfondimenti.
- Problemi tecnici o errori.

**Note importanti:**

- Gli alti tassi di mancato recapito non sono sempre negativi: alcune pagine (come le informazioni di contatto o specifiche di prodotto specifiche) possono naturalmente avere tassi di mancato recapito elevati.
- Confronta le percentuali di mancato recapito tra diversi tipi di pagina e origini di traffico per identificare le aree problematiche.
- Gli aumenti improvvisi del tasso di mancato recapito spesso indicano problemi tecnici o un targeting di campagna inadeguato.

**Qual è il tasso di mancato recapito valido?** Questo varia in base al settore e al tipo di pagina, ma in genere:

- 40-60%: media per i siti di e-commerce.
- Inferiore al 40%: coinvolgimento eccellente.
- Superiore al 70%: può indicare problemi che richiedono un’indagine.

### Strategie

- **Maggiore rilevanza della ricerca**: utilizza sinonimi e faceting intelligente per garantire che i clienti trovino rapidamente i prodotti rilevanti. Risultati di ricerca insoddisfacenti sono la causa principale degli alti tassi di mancato recapito.

- **Implementa unità di consigli**: distribuisci unità di consigli nelle pagine dei risultati delle ricerche e delle categorie per fornire opzioni di prodotto aggiuntive e mantenere il coinvolgimento dei visitatori.

- **Ottimizza individuazione prodotto**: utilizza le regole di merchandising per garantire che i prodotti più rilevanti e popolari vengano visualizzati per primi nei risultati della ricerca.

- **Crea esperienze coinvolgenti nella home page**: utilizza i tipi di consigli &quot;Consigliato per te&quot; e &quot;Di tendenza&quot; nella tua home page per coinvolgere immediatamente i visitatori con contenuti rilevanti.

>[!ENDTABS]

## Risoluzione dei problemi e ottimizzazione

### Quando le metriche sono in declino

**Ricavi in calo**:

- Verifica se le unità di consigli sono ancora attive e se le prestazioni sono buone.
- Rivedi le regole di merchandising per garantire la promozione di prodotti ad alto margine.
- Analizza le prestazioni di ricerca per identificare se i prodotti più popolari sono ancora ben posizionati.

**Diminuzione del tasso di conversione**:

- Verificare che la rilevanza della ricerca sia mantenuta (controllare sinonimi e facet).
- Assicurati che le unità di consigli siano visualizzate correttamente.
- Rivedi le regole di merchandising per eventuali conflitti o problemi.

**Percentuali di mancato recapito elevate**:

- Controlla la rilevanza dei risultati di ricerca e, se necessario, implementa i sinonimi.
- Assicurati che le unità di consigli siano caricate correttamente.
- Verifica la qualità e la disponibilità dei dati del prodotto.

**Basso livello di coinvolgimento**:

- Diversificare i tipi di consigli per evitare l’eccesso di clienti.
- Implementare strategie di consigli più personalizzate.
- Ottimizza l’esperienza di ricerca con facet e sinonimi migliori.

## Descrizioni dei campi

### Configurazione del rapporto

| Campo | Descrizione |
|---|---|
| Intervallo di date | Le opzioni disponibili sono **Ultimi 3 mesi**, **Ultimi 7 giorni**, **Ultimi 30 giorni**, **Ultimi 6 mesi**, **Ultimi 12 mesi** e **Da inizio anno**. Utilizza intervalli più brevi per ottenere informazioni immediate sull’ottimizzazione e intervalli più lunghi per l’analisi delle tendenze. |
| Paese | In base all&#39;origine del catalogo specificata per la [visualizzazione catalogo](../setup/catalog-view.md). Seleziona il mercato appropriato per un’analisi accurata delle prestazioni. |
| Valuta | Valuta specificata per la vista catalogo. Assicurati che questo corrisponda al tuo mercato di destinazione per una segnalazione accurata dei ricavi. |
| Esporta | Salva il report come PDF per la condivisione con le parti interessate o per l&#39;analisi offline. |

## Altri argomenti correlati

- [Prestazioni ricerca](../manage-results/search-performance.md) - Analizza i termini di ricerca e ottimizza la rilevanza della ricerca.
- [Prestazioni consigli](../manage-results/recommendation-performance.md) - Monitora e ottimizza l&#39;efficacia dei consigli.
- [Panoramica dei consigli](../merchandising/recommendations/overview.md) - Scopri i consigli sui prodotti basati sull&#39;intelligenza artificiale.
- [Regole di merchandising](../merchandising/rules/overview.md) - Aumenta, sotterrare, fissare o nascondere i prodotti nei risultati della ricerca.
- [Facet](../merchandising/facets/overview.md) - Migliora la ricerca con un filtro intelligente.
- [Sinonimi](../merchandising/synonyms/overview.md) - Migliora la rilevanza della ricerca e l&#39;esperienza del cliente.
- [Panoramica eventi](../setup/events/overview.md) - Comprendi i dati che alimentano le metriche.
