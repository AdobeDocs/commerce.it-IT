---
title: Vista catalogo
description: Scopri come creare e gestire le visualizzazioni catalogo in [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 0%

---

# Crea vista catalogo

[Visualizzazioni catalogo](#catalog-views) ti aiutano a definire la tua struttura di vendita al dettaglio in business group significativi. Una vista catalogo influisce sulla visibilità dei prodotti applicando criteri e filtri specifici che determinano quali prodotti vengono visualizzati in una vetrina. Questi criteri possono includere attributi come marchio, modello o categoria di parte, garantendo che solo i prodotti rilevanti siano visibili agli acquirenti in base alla configurazione della vista catalogo. Inoltre, le visualizzazioni catalogo possono utilizzare listini prezzi per visualizzare i prezzi specifici del cliente, adattando ulteriormente l’esperienza di acquisto. [Ulteriori informazioni](#catalog-views) sulle visualizzazioni del catalogo.

In questa sezione, puoi creare una visualizzazione catalogo, selezionare un [criterio](policies.md) e un [listino prezzi dedicato](pricebooks.md).

1. Nel menu a sinistra, vai a _Configurazione archivio_ e fai clic su **[!UICONTROL Catalog views]**.

1. Fare clic su **[!UICONTROL Create catalog view]**. &#x200B;

1. Aggiungi i dettagli di visualizzazione del catalogo:

   - **Nome** - Immettere il nome della visualizzazione del catalogo. Ad esempio, &quot;Celport&quot;. &#x200B;
   - **Origini del catalogo** - Aggiungi l&#39;origine del catalogo (impostazioni locali). Ad esempio, &quot;en-US&quot;. Premere il tasto **Invio**.
   - **Criteri**: utilizzare il menu a discesa per selezionare i criteri rilevanti. Ad esempio, &quot;Marchio&quot;, &quot;Modello&quot;. &#x200B;Assicurarsi di avere già [creato un criterio](policies.md).

1. Selezionare il listino prezzi che si desidera collegare alla visualizzazione del catalogo. Ulteriori informazioni su [listini prezzi](pricebooks.md).

1. Fare clic su **[!UICONTROL Add]** per creare la visualizzazione catalogo con il listino prezzi dedicato e i criteri collegati.

   Se il pulsante **[!UICONTROL Add]** non è attivo, assicurati che l&#39;origine del catalogo sia aggiunta correttamente posizionando il cursore nel campo Origini del catalogo e premendo **Invio**. &#x200B;

La pagina Visualizzazioni catalogo viene aggiornata per visualizzare la nuova visualizzazione del catalogo.&#x200B;

Dopo aver completato questi passaggi, la nuova vista catalogo viene configurata per visualizzare prodotti e prezzi in base alle origini e ai criteri di catalogo selezionati.

## Visualizzazioni catalogo

Un catalogo di prodotti è essenziale per le esperienze di acquisto online, consentendo ai clienti di sfogliare, cercare e fare acquisti. Per l&#39;efficienza operativa, un catalogo di prodotti deve rispecchiare fedelmente la struttura aziendale dell&#39;azienda. Le aziende spesso devono vendere i prodotti a prezzi diversi in base al mercato geografico, alla visualizzazione del catalogo di distribuzione, al segmento di clienti e ad altre variabili. Per soddisfare questo requisito, una piattaforma di e-commerce deve offrire un modello dati di catalogo flessibile che consenta alle aziende di produrre varianti del proprio catalogo su misura per questi scenari. Adobe soddisfa queste esigenze offrendo servizi di merchandising basati su visualizzazioni e criteri del catalogo. I servizi di merchandising forniscono elementi di base che i commercianti possono utilizzare per creare e gestire cataloghi su larga scala. Questo consente alle aziende di configurare cataloghi in linea con la propria struttura aziendale e con le strategie di go-to-market.

Ad alto livello, con i servizi di merchandising è possibile:

- Utilizza un singolo catalogo di base per tutte le tue esigenze aziendali. Scalabilità rapida del catalogo per nuovi marchi, mercati, business unit, visualizzazioni di cataloghi go-to-market e segmenti di clienti senza la necessità di una riarchitettura completa. Questo elimina la duplicazione dei dati e imposta la piattaforma di e-commerce per un&#39;elevata efficienza operativa.
- Sblocca la distribuzione del catalogo e fornisci i contenuti giusti progettando il catalogo dei prodotti in modo che rifletta la tua attività, inclusi prodotti, clienti, prezzi e distribuzione.
- Acquisisci e aggiorna rapidamente i dati del catalogo e distribuisci rapidamente gli aggiornamenti allo storefront in base alle tue esigenze di promozioni e campagne.
- Ottieni punteggi perfetti con componenti dell’interfaccia utente pronti all’uso e veloci grazie a Edge Delivery Services, per una navigazione fluida dei prodotti e consigli.
- Adottare un&#39;architettura componibile moderna utilizzando l&#39;architettura di estensibilità di Adobe ([App Builder](https://experienceleague.adobe.com/it/playlists/commerce-get-started-app-builder-development)) per importare i dati dei prodotti e alimentare le vetrine commerciali headless utilizzando la [Mesh API](https://experienceleague.adobe.com/it/playlists/commerce-get-started-app-builder-and-api-mesh) di Adobe.

>[!INFO]
>
>Per informazioni sulle API disponibili in Merchandising Services basate su visualizzazioni e criteri del catalogo, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog).

## Architettura

I servizi di merchandising basati su visualizzazioni e criteri del catalogo sono un modello di dati del catalogo altamente scalabile e flessibile che consente di sbloccare con facilità casi d’uso multi-brand, multi-business unit e multilingue. Questo modello sostituisce l’utilizzo delle origini del catalogo prodotti di Adobe Commerce (sito web, store, storeview) con le nuove origini del catalogo prodotti di Merchandising Services (vista catalogo, criteri e impostazioni internazionali).

Il diagramma seguente fornisce una panoramica di alto livello del framework Merchandising.

Architettura ![[!DNL Merchandising Services]](../assets/merchandising-svcs-architecture.png)

Nella parte superiore di questo diagramma, i dati del catalogo (PIM, ERP e così via) vengono acquisiti nel framework dei servizi di merchandising. Questi dati del catalogo contengono SKU. Ogni SKU contiene i dettagli dell&#39;origine del catalogo (impostazioni internazionali) e gli attributi dei prodotti, che vengono mappati alle nuove origini del catalogo dei prodotti di Merchandising Services (visualizzazioni del catalogo, criteri e impostazioni internazionali).

Quando tutti questi dati vengono acquisiti nel framework Merchandising, il risultato è un nuovo catalogo di base unificato disponibile nella pipeline di dati di Catalog Service. Nella parte successiva del diagramma sono presenti più visualizzazioni di catalogo. Ogni vista catalogo rappresenta una Business Unit. Ad esempio, *Vendita al dettaglio in Texas*, *Vendita al dettaglio in Texas stagionale* e così via. Come si può vedere dal diagramma, le impostazioni internazionali, le policy e i listini prezzi possono essere condivisi tra le diverse visualizzazioni del catalogo&#x200B;

Infine, il diagramma mostra come questi dati distinti del catalogo possano essere visualizzati in varie posizioni, ad esempio in una vetrina Edge Delivery Services, in un marketplace, in una visualizzazione del catalogo di annunci pubblicitari, in una vetrina micro personalizzata e così via.

Per informazioni su come acquisire i dati del catalogo in Merchandising utilizzando l&#39;API di acquisizione dati del catalogo e su come impostare le impostazioni internazionali, le policy e i listini prezzi utilizzando l&#39;API gestione catalogo e regole, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Per ulteriori informazioni sui concetti che compongono Merchandising Services, consulta le sezioni seguenti.

## Gestione catalogo prodotti

La gestione del catalogo dei prodotti comprende due aspetti distinti: i dati dei prodotti e il contesto dei prodotti. I servizi di merchandising rispettano la separazione di questi compiti, offrendo una gestione indipendente per ciascuno di essi.

- **Dati prodotto** - Quale prodotto è in vendita e a quale prezzo?
- **Contesto del prodotto** - Chi vende a chi e dove?

![[!DNL Merchandising Services] aspetti](../assets/merchandising-svcs-parts.png)

### Dati prodotto

I dati di prodotto includono i seguenti tipi:

- **Prodotti** - Singoli SKU o raccolte di SKU che rappresentano beni fisici o servizi immateriali con attributi che rappresentano il prodotto, tra cui descrizione, peso, dimensioni e molto altro. Gli attributi specificano anche le origini del catalogo della vista catalogo e del catalogo dei criteri per uno SKU. I prodotti possono essere raggruppati in vari tipi di prodotti, ad esempio semplici, configurabili, bundle, bundle di bundle, abbonamenti e altro ancora.
- **Metadati** - I metadati dell&#39;attributo del prodotto definiscono e gestiscono la modalità di visualizzazione degli attributi del prodotto nella vetrina in elenchi di prodotti, pagine di dettaglio, risultati di ricerca e così via. I metadati definiscono inoltre il modo in cui gli attributi del prodotto vengono utilizzati nella ricerca: ordinamento, filtro, ponderazione della ricerca e così via.
- **Listini prezzi e listini prezzi** - Determina i prezzi di vendita dei prodotti. In Merchandising Services, uno SKU di prodotto e un prezzo sono separati, pertanto hai il potere di definire più listini prezzi per una singola SKU. Separando i prezzi dallo SKU, puoi sbloccare i prezzi specifici dell’origine del catalogo per diversi livelli cliente, business unit e aree geografiche. Puoi definire prezzi regolari e scontati e gestire tutto questo su larga scala.
- **Assets** - Artefatti associati a prodotti quali immagini, video, PDF o altri tipi di file (roadmap futura).

### Gestione del contesto del prodotto

La gestione del contesto del prodotto riguarda i seguenti aspetti:

- **vista catalogo** - La vista catalogo di distribuzione definisce il percorso attraverso cui un&#39;azienda desidera vendere i prodotti. Una vista catalogo è l’astrazione di livello più alto che racchiude le impostazioni internazionali e i criteri.
   - Esempio: rivenditori per l&#39;industria automobilistica. Filiali di conglomerati multimarca. Ubicazione di produzione per i fornitori.
- **Criterio** - Filtro di accesso ai dati che ti consente di inviare il contenuto corretto alla destinazione giusta. Questo concetto abilita le funzionalità di distribuzione del catalogo.
   - Esempio: punti vendita negozi fisici, mercati, pipeline pubblicitarie (Google, Facebook, Instagram)
- **origine catalogo** - Rappresenta la lingua (lingua) per i cataloghi, ad esempio `en-US`. l’origine del catalogo è impostata a livello di SKU durante l’inserimento dei dati nel catalogo.

Durante l’inserimento e l’aggiornamento dei dati del prodotto, uno SKU contiene i dettagli delle origini e degli attributi del catalogo (gli attributi vengono mappati alle viste e ai criteri del catalogo). Questi definiscono gli identificatori del contesto del prodotto a cui appartiene una SKU:

![[!DNL Merchandising Services] identificatori contesto prodotto](../assets/merchandising-svcs-product-id.png)

Nell’immagine precedente, ogni SKU fornisce:

- identificatori di origine del catalogo&#x200B;
   - Lingua: obbligatoria&#x200B;
- Attributi del prodotto
   - Gli attributi di prodotto vengono utilizzati per la mappatura alle visualizzazioni di catalogo e ai criteri pertinenti&#x200B;
   - Esempio: in qualità di produttore di automobili, puoi scegliere di creare una visualizzazione di catalogo e una combinazione di criteri per gli attributi del prodotto: (1) Rivenditori (2) Marchi di automobili.&#x200B;
- Prezzi e listini prezzi assegnati
   - Ogni SKU può avere più prezzi definiti utilizzando più listini prezzi.
   - Esempio: Offri ai dipendenti un prezzo regolare ridotto sui pezzi di ricambio con uno sconto aggiuntivo del 25%. Offri ai clienti VIP un prezzo più alto a tariffa regolare con uno sconto del 10%. Le informazioni sul prezzo SKU del prodotto garantiscono che venga visualizzato il prezzo corretto per ogni segmento di cliente.

La vista catalogo e le definizioni dei criteri vengono create utilizzando API dedicate:

![[!DNL Merchandising Services] mapping di visualizzazione catalogo, criteri e origine catalogo](../assets/merchandising-svcs-scope-map.png)

- **origine catalogo** (impostazioni locali): impostata a livello SKU durante l&#39;acquisizione dei dati del prodotto.&#x200B;
- **vista catalogo** - Definizione creata utilizzando API dedicate. &#x200B;
- **Criterio** - Definizione creata utilizzando API dedicate.

## Funzioni principali

| Funzioni principali | Beneficio |
|---|---|
| **Acquisizione diretta dei dati del catalogo nella pipeline dei servizi di vetrina**: acquisisci i dati del catalogo direttamente nella pipeline del servizio di catalogo per il ciclo di vita di ricerca e navigazione di vetrina (pagina di visualizzazione del prodotto, pagina dell&#39;elenco dei prodotti, pagina dei risultati di ricerca e così via). | <ul><li>Acquisisci direttamente i dati del catalogo nella pipeline del servizio di vetrina che alimenta: Catalog Service, l’individuazione del prodotto e la funzione Consigli. Con questo, puoi distribuire aggiornamenti del catalogo su larga scala per milioni di SKU. Questo consente di gestire le promozioni su larga scala in base al tempo. </li></ul> |
| **Nuove origini catalogo prodotti**: la vista catalogo, i criteri e l&#39;origine catalogo sono nuove origini catalogo prodotti introdotte da Merchandising Services. Queste origini del catalogo prodotti sostituiscono le origini del catalogo del sito web, dello store e della visualizzazione dello store nel livello dei servizi di storefront. [Ulteriori informazioni](#product-context-management). | <ul><li>Con le nuove origini del catalogo, Merchandising Services consente di scalare i casi d’uso di più aree geografiche, più business unit, più marchi e più lingue con facilità utilizzando un singolo catalogo di base.</li><li>Eliminazione della ridondanza dei dati nella gestione dei cataloghi.</li></ul> |
| **Scalabilità a decine di milioni di SKU** | Gestione del catalogo su larga scala. Qui è possibile acquisire e gestire con facilità oltre 200 MM SKU. |
| **Supporto per i tipi di prodotto** | <ul><li>Semplice, configurabile</li><li>Bundle e bundle di bundle (roadmap futura)</li><li>Abbonamenti e piani (roadmap futura)</li></ul> |
| **Commercio headless** | <ul><li>Supporto completo per le implementazioni di e-commerce headless tramite le API Catalog Service, Product Discovery e Recommendations.</li></ul> |
| **Componenti dell&#39;interfaccia utente moderni e veloci** | <ul><li>Supporto predefinito dei componenti dell’interfaccia utente per la ricerca dei prodotti e la funzione Consigli.</li><li>I componenti dell’interfaccia utente sono estensibili e flessibili e possono essere utilizzati sia dal servizio Edge Delivery di Adobe che da qualsiasi altra implementazione storefront.</li></ul> |

## Quale tipo di commerciante trae maggior vantaggio dai servizi di merchandising?

La tabella seguente evidenzia le problematiche più comuni incontrate dai commercianti e il modo in cui i servizi di merchandising basati sulle visualizzazioni e sui criteri del catalogo consentono di risolverle.

| Tipo di commerciante | Caso d’uso | Problemi risolti |
|---|---|---|
| Conglomerato multimarca | <ul><li>Vendono diversi marchi</li><li>Vendono in diversi paesi</li><li>Vendono in diverse lingue</li></ul> | Utilizza un catalogo unificato basato su un&#39;unica base e ottieni efficienza operativa con l&#39;espansione a diversi marchi, aree geografiche e lingue. |
| Conglomerato di parti di automobili/produzione | <ul><li>Vende parti automatiche o meccaniche. I prodotti sono gli stessi per tutti i clienti.</li><li>Diversi dealer vendono pezzi ai clienti</li><li>Ogni dealer ha i propri prezzi, stock e metodi di spedizione</li></ul> | Per avere diverse integrazioni di spedizione, ogni rivenditore deve disporre di un sito Web separato. Tuttavia, siti web separati forzano il tipico modello di dati di catalogo a duplicare i dati. Quindi, se ci sono 3000 rivenditori negli Stati Uniti, un commerciante crea 3000 copie del catalogo anche se lo stesso catalogo è utilizzato da tutti i rivenditori. Questa duplicazione dei dati interferisce con i limiti delle prestazioni. I servizi di merchandising eliminano la duplicazione dei dati. |
| Impresa di imballaggio/logistica | <ul><li>Hanno diverse sedi di spedizione</li><li>Hanno un prezzo diverso per ogni cliente</li><li>Lo stesso prodotto disponibile in 2 sedi per 2 clienti ha 4 prezzi possibili</li></ul> | Nonostante l&#39;utilizzo di gruppi di clienti per coprire i prezzi per cliente, il modello di dati di catalogo tipico non ha la capacità di gestire i prezzi per posizione. Inoltre, i commercianti desiderano regole di visibilità univoche per posizione/sito web. La gestione di queste regole complesse di prezzo e visibilità può essere sbloccata su larga scala con i servizi di merchandising. |
