---
title: Panoramica del catalogo
description: Scopri come definire canali e criteri.
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 0%

---

# Panoramica del catalogo

>[!NOTE]
>
>Questa documentazione descrive un prodotto in fase di sviluppo con accesso anticipato e non riflette tutte le funzionalità previste per la disponibilità generale.

Un catalogo di prodotti è essenziale per le esperienze di acquisto online, consentendo ai clienti di sfogliare, cercare e fare acquisti. Per l&#39;efficienza operativa, un catalogo di prodotti deve rispecchiare fedelmente la struttura aziendale dell&#39;azienda. Le aziende spesso devono vendere i prodotti a prezzi diversi in base al mercato geografico, al canale di distribuzione, al segmento di clienti e ad altre variabili. Per soddisfare questo requisito, una piattaforma di e-commerce deve offrire un modello dati di catalogo flessibile che consenta alle aziende di produrre varianti del proprio catalogo su misura per questi scenari. Adobe Systems risponde a queste esigenze offrendo Servizi di merchandising basati su Canali e Politiche. I servizi di merchandising forniscono elementi di base che i commercianti possono utilizzare per creare e gestire cataloghi su larga scala. Ciò consente alle aziende di configurare cataloghi in linea con la struttura aziendale e le strategie di mercato.

Ad alto livello, con Merchandising Services puoi:

- Utilizza un unico catalogo di base per tutte le tue esigenze aziendali. Ridimensiona rapidamente il tuo catalogo su nuovi marchi, mercati, business unit, canali go-to-mercato e segmenti di clienti senza la necessità di una riarchitettura completa. Ciò elimina la duplicazione dei dati e imposta la tua piattaforma di e-commerce per un&#39;elevata efficienza operativa.
- Sblocca la diffusione del catalogo e offri il contenuto giusto progettando il tuo catalogo prodotti per riflettere la tua attività, inclusi prodotti, clienti, prezzi e distribuzione.
- Acquisisci e aggiorna rapidamente i dati del catalogo e distribuisci rapidamente gli aggiornamenti allo storefront in base alle tue esigenze di promozioni e campagne.
- Ottieni punteggi perfetti con componenti dell’interfaccia utente pronti all’uso e veloci grazie a Edge Delivery Services, per una navigazione fluida dei prodotti e consigli.
- Adottare un&#39;architettura componibile moderna utilizzando l&#39;architettura di estensibilità di Adobe ([App Builder](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-development)) per importare i dati dei prodotti e alimentare le vetrine commerciali headless utilizzando la [Mesh API](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-and-api-mesh) di Adobe.

>[!INFO]
>
>Per informazioni sulle API disponibili in Merchandising Services basate su canali e criteri, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog).

## Architettura

I servizi di merchandising basati su canali e criteri sono un modello di dati di catalogo altamente scalabile e flessibile che consente di sbloccare con facilità casi di utilizzo multi-brand, multi-business unit e multilingue. Questo modello sostituisce l’utilizzo degli ambiti di prodotto classici di Adobe Commerce (sito web, store, storeview) con i nuovi ambiti di prodotto di Merchandising Services (canale, criteri e impostazioni internazionali).

Il diagramma seguente fornisce una panoramica di alto livello del framework Merchandising.

Architettura ![[!DNL Merchandising Services]](../assets/merchandising-svcs-architecture.png)

Nella parte superiore di questo diagramma, i dati del catalogo (PIM, ERP e così via) vengono acquisiti nel framework dei servizi di merchandising. Questi dati del catalogo contengono SKU. Ogni SKU contiene i dettagli dell’ambito (impostazioni internazionali) e gli attributi del prodotto, mappati ai nuovi ambiti di prodotto di Merchandising Services (canali, criteri e impostazioni internazionali).

Quando tutti questi dati vengono acquisiti nel framework Merchandising, il risultato è un nuovo catalogo di base unificato disponibile nella pipeline di dati di Catalog Service. Nella parte successiva del diagramma vengono visualizzati più canali. Ogni canale rappresenta una business unit. Ad esempio, *Vendita al dettaglio in Texas*, *Vendita al dettaglio in Texas stagionale* e così via. Come puoi vedere dal diagramma, le impostazioni internazionali, le policy e i listini prezzi possono essere condivisi tra i diversi canali&#x200B;

Infine, il diagramma mostra come questi dati distinti del catalogo possano essere visualizzati in varie posizioni, ad esempio in una vetrina Edge Delivery Services, in un mercato, in un canale pubblicitario, in una vetrina personalizzata e così via.

Per informazioni su come acquisire i dati del catalogo in Merchandising utilizzando l&#39;API di acquisizione dati del catalogo e su come impostare le impostazioni internazionali, le policy e i listini prezzi utilizzando l&#39;API gestione catalogo e regole, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Per ulteriori informazioni sui concetti che compongono Merchandising Services, consulta le sezioni seguenti.

## Gestione catalogo prodotti

La gestione del catalogo dei prodotti comprende due aspetti distinti: i dati dei prodotti e il contesto dei prodotti. I servizi di merchandising rispettano la separazione di questi compiti, offrendo una gestione indipendente per ciascuno di essi.

- **Dati prodotto** - Quale prodotto è in vendita e a quale prezzo?
- **Contesto del prodotto** - Chi vende a chi e dove?

![[!DNL Merchandising Services] aspetti](../assets/merchandising-svcs-parts.png)

### Dati prodotto

I dati di prodotto includono i seguenti tipi:

- **Prodotti** - Singoli SKU o raccolte di SKU che rappresentano beni fisici o servizi immateriali con attributi che rappresentano il prodotto, tra cui descrizione, peso, dimensioni e molto altro. Gli attributi specificano anche gli ambiti di canale e criteri per uno SKU. I prodotti possono essere raggruppati in vari tipi di prodotti, ad esempio semplici, configurabili, bundle, bundle di bundle, abbonamenti e altro ancora.
- **Metadati** - I metadati dell&#39;attributo del prodotto definiscono e gestiscono la modalità di visualizzazione degli attributi del prodotto nella vetrina in elenchi di prodotti, pagine di dettaglio, risultati di ricerca e così via. I metadati definiscono inoltre il modo in cui gli attributi del prodotto vengono utilizzati nella ricerca: ordinamento, filtro, ponderazione della ricerca e così via.
- **Listini prezzi e listini prezzi** - Determina i prezzi di vendita dei prodotti. In Merchandising Services, uno SKU di prodotto e un prezzo sono separati, pertanto hai il potere di definire più listini prezzi per una singola SKU. Separando i prezzi dallo SKU, puoi sbloccare i prezzi specifici dell’ambito tra diversi livelli cliente, business unit e aree geografiche. Puoi definire prezzi regolari e scontati e gestire tutto questo su larga scala.
- **Assets** - Artefatti associati a prodotti quali immagini, video, PDF o altri tipi di file (roadmap futura).

### Gestione del contesto del prodotto

La gestione del contesto del prodotto riguarda i seguenti aspetti:

- **Canale** - Il canale di distribuzione definisce il percorso attraverso cui un&#39;azienda desidera vendere i prodotti. Un canale è l’astrazione di livello più alto che racchiude le impostazioni internazionali e i criteri.
   - Esempio: rivenditori per l&#39;industria automobilistica. Filiali di conglomerati multimarca. Ubicazione di produzione per i fornitori.
- **Criterio** - Filtro di accesso ai dati che ti consente di inviare il contenuto corretto alla destinazione giusta. Questo concetto abilita le funzionalità di distribuzione del catalogo.
   - Esempio: punti vendita negozi fisici, mercati, pipeline pubblicitarie (Google, Facebook, Instagram)
- **Ambito** - Rappresenta la lingua (lingua) per i cataloghi, ad esempio `en-US`. L’ambito viene impostato a livello di SKU durante l’inserimento dei dati del catalogo.

Durante l’acquisizione e l’aggiornamento dei dati del prodotto, uno SKU contiene i dettagli di ambiti e attributi (gli attributi vengono mappati su canali e criteri). Questi definiscono gli identificatori del contesto del prodotto a cui appartiene una SKU:

![[!DNL Merchandising Services] identificatori contesto prodotto](../assets/merchandising-svcs-product-id.png)

Nell’immagine precedente, ogni SKU fornisce:

- Identificatori ambito&#x200B;
   - Lingua: obbligatoria&#x200B;
- Attributi del prodotto
   - Gli attributi del prodotto vengono utilizzati per la mappatura ai canali e ai criteri pertinenti&#x200B;
   - Esempio: in qualità di produttore di automobili, puoi scegliere di creare una combinazione di canali e criteri per gli attributi del prodotto: (1) rivenditori (2) marchi di automobili.&#x200B;
- Prezzi e listini prezzi assegnati
   - Ogni SKU può avere più prezzi definiti utilizzando più listini prezzi.
   - Esempio: Offri ai dipendenti un prezzo regolare ridotto sui pezzi di ricambio con uno sconto aggiuntivo del 25%. Offri ai clienti VIP un prezzo più alto a tariffa regolare con uno sconto del 10%. Le informazioni sul prezzo SKU del prodotto garantiscono che venga visualizzato il prezzo corretto per ogni segmento di cliente.

Le definizioni dei canali e dei criteri vengono create utilizzando API dedicate:

Mapping di canali, criteri e ambiti ![[!DNL Merchandising Services]](../assets/merchandising-svcs-scope-map.png)

- **Ambito** (impostazioni locali): impostato a livello SKU durante l&#39;acquisizione dei dati del prodotto.&#x200B;
- **Canale** : definizione creata tramite API dedicate.
- **Policy** - Definizione creata utilizzando API dedicate.

## Funzionalità chiave

| Funzionalità chiave | Beneficio |
|---|---|
| **Acquisizione diretta dei dati del catalogo nella pipeline dei servizi di vetrina**: acquisisci i dati del catalogo direttamente nella pipeline del servizio di catalogo per il ciclo di vita di ricerca e navigazione di vetrina (pagina di visualizzazione del prodotto, pagina dell&#39;elenco dei prodotti, pagina dei risultati di ricerca e così via). | <ul><li>Acquisisci direttamente i dati del catalogo nella pipeline del servizio di vetrina che alimenta: Catalog Service, Product Discovery (Live Search) e Product Recommendations. Con questo, puoi distribuire aggiornamenti del catalogo su larga scala per milioni di SKU. Questo consente di gestire le promozioni su larga scala in base al tempo. </li></ul> |
| **Nuovi ambiti prodotti del catalogo**: Canale, criteri e ambito sono nuovi ambiti prodotti introdotti da Merchandising Services. Questi ambiti prodotto sostituiscono gli ambiti sito web, store e storeview nel livello servizi vetrina. [Ulteriori informazioni](#product-context-management). | <ul><li>Con i nuovi ambiti, i servizi di merchandising consentono di scalare facilmente casi d’uso in più aree geografiche, più business unit, più marchi e più lingue utilizzando un unico catalogo di base.</li><li>Eliminazione della ridondanza dei dati nella gestione dei cataloghi.</li></ul> |
| **Scalabilità a decine di milioni di SKU** | Gestione del catalogo su larga scala. Qui è possibile acquisire e gestire con facilità oltre 200 MM SKU. |
| **Supporto per i tipi di prodotto** | <ul><li>Semplice, configurabile</li><li>Bundle e bundle di bundle (roadmap futura)</li><li>Abbonamenti e piani (roadmap futura)</li></ul> |
| **Commercio headless** | <ul><li>Supporto completo per le implementazioni di e-commerce headless tramite le API Catalog Service, Product Discovery (Live Search) e Product Recommendations.</li></ul> |
| **Componenti dell&#39;interfaccia utente moderni e veloci** | <ul><li>Supporto dei componenti dell’interfaccia utente predefiniti per la ricerca dei prodotti e i consigli di prodotto.</li><li>I componenti dell’interfaccia utente sono estensibili e flessibili e possono essere utilizzati sia dal servizio Edge Delivery di Adobe che da qualsiasi altra implementazione storefront.</li></ul> |

## Quale tipo di commerciante trae maggior vantaggio dai servizi di merchandising?

La tabella seguente evidenzia le problematiche più comuni incontrate dai commercianti e come i servizi di merchandising basati su canali e policy li affrontano.

| Tipo di commerciante | Caso d’uso | Problemi risolti |
|---|---|---|
| Conglomerato multimarca | <ul><li>Vendono diversi marchi</li><li>Vendono in diversi paesi</li><li>Vendono in diverse lingue</li></ul> | Utilizza un catalogo unificato basato su un&#39;unica base e ottieni efficienza operativa con l&#39;espansione a diversi marchi, aree geografiche e lingue. |
| Conglomerato di parti di automobili/produzione | <ul><li>Vende parti automatiche o meccaniche. I prodotti sono gli stessi per tutti i clienti.</li><li>Diversi dealer vendono pezzi ai clienti</li><li>Ogni dealer ha i propri prezzi, stock e metodi di spedizione</li></ul> | Per avere diverse integrazioni di spedizione, ogni rivenditore deve disporre di un sito Web separato. Tuttavia, siti web separati forzano il tipico modello di dati di catalogo a duplicare i dati. Quindi, se ci sono 3000 rivenditori negli Stati Uniti, un commerciante crea 3000 copie del catalogo anche se lo stesso catalogo è utilizzato da tutti i rivenditori. Questa duplicazione dei dati interferisce con i limiti delle prestazioni. I servizi di merchandising eliminano la duplicazione dei dati. |
| Impresa di imballaggio/logistica | <ul><li>Hanno diverse sedi di spedizione</li><li>Hanno un prezzo diverso per ogni cliente</li><li>Lo stesso prodotto disponibile in 2 sedi per 2 clienti ha 4 prezzi possibili</li></ul> | Nonostante l&#39;utilizzo di gruppi di clienti per coprire i prezzi per cliente, il modello di dati di catalogo tipico non ha la capacità di gestire i prezzi per posizione. Inoltre, i commercianti desiderano regole di visibilità univoche per posizione/sito web. La gestione di queste regole complesse di prezzo e visibilità può essere sbloccata su larga scala con i servizi di merchandising. |

<!--### Where to go from here

- Ingest data into Merchandising Services using the [data ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Manage your catalog and define the channels, policies, and scopes using the [catalog management API](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Complete a tutorial](https://developer-stage.adobe.com/commerce/services/composable-catalog/merchandising-services-use-case/) that shows how a company with a single base catalog can use the Merchandising Services APIs to add product data, define catalogs using projections, and retrieve the catalog data for display in a headless storefront.-->
