---
title: '[!DNL Composable Catalog Data Model]'
description: Scopri in che modo  [!DNL Composable Catalog Data Model] for Adobe Commerce ti consente di configurare il catalogo per adattarlo al tuo modello di business e alla tua strategia di commercializzazione
hidefromtoc: true
hide: true
recommendations: noCatalog
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 0%

---

# [!DNL Composable Catalog Data Model]

Un catalogo di prodotti è essenziale per le esperienze di acquisto online, consentendo ai clienti di sfogliare, cercare e fare acquisti. Per l&#39;efficienza operativa, un catalogo di prodotti deve rispecchiare fedelmente la struttura aziendale dell&#39;azienda. Le aziende spesso devono vendere i prodotti a prezzi diversi in base al mercato geografico, al canale di distribuzione, al segmento di clienti e ad altre variabili. Per soddisfare questo requisito, una piattaforma di e-commerce deve offrire un modello dati di catalogo flessibile che consenta alle aziende di produrre varianti del proprio catalogo su misura per questi scenari. Il modello CCDM (Composable Catalog Data Model) di Adobe Commerce soddisfa queste esigenze. CCDM fornisce blocchi predefiniti che i commercianti possono utilizzare per creare e gestire cataloghi su larga scala. Questo consente alle aziende di configurare cataloghi in linea con la propria struttura aziendale e con le strategie di go-to-market.

Ad alto livello, con CCDM è possibile:

- Utilizza un singolo catalogo di base per tutte le tue esigenze aziendali. Scalabilità rapida del catalogo per nuovi marchi, mercati, business unit, canali go-to-market e segmenti di clienti senza la necessità di una riarchitettura completa. Questo elimina la duplicazione dei dati e imposta la piattaforma di e-commerce per un&#39;elevata efficienza operativa.
- Sblocca la distribuzione del catalogo e fornisci i contenuti giusti progettando il catalogo dei prodotti in modo che rifletta la tua attività, inclusi prodotti, clienti, prezzi e distribuzione.
- Acquisisci e aggiorna rapidamente i dati del catalogo e distribuisci rapidamente gli aggiornamenti allo storefront in base alle tue esigenze di promozioni e campagne.
- Ottieni punteggi perfetti con componenti dell’interfaccia utente pronti all’uso e veloci grazie a Edge Delivery Services, per una navigazione fluida dei prodotti e consigli.
- Adottare un&#39;architettura componibile moderna utilizzando l&#39;architettura di estensibilità di Adobe ([App Builder](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-development)) per importare i dati dei prodotti e alimentare le vetrine commerciali headless utilizzando la [Mesh API](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-and-api-mesh) di Adobe.

>[!INFO]
>
>Per informazioni sulle API disponibili in CCDM, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog).

## Architettura

CCDM è un modello di dati a catalogo altamente scalabile e flessibile che consente di sbloccare con facilità casi di utilizzo multi-brand, multi-business unit e multilingue. Il modello sostituisce l’utilizzo degli ambiti di prodotto classici di Adobe Commerce (sito web, store, storeview) con i nuovi ambiti di prodotto CCDM (canale, criteri e impostazioni internazionali).

Il diagramma seguente fornisce una vista di alto livello del framework CCDM.

Architettura ![[!DNL Composable Catalog Data Model]](assets/ccdm-architecture.png)

Nella parte superiore di questo diagramma, i dati del catalogo (PIM, ERP e così via) vengono acquisiti nel framework CCDM. Questi dati del catalogo contengono SKU. Ogni SKU contiene i dettagli dell&#39;ambito (impostazioni internazionali) e gli attributi del prodotto, che vengono mappati ai nuovi ambiti del prodotto CCDM (canali, criteri e impostazioni internazionali).

Quando tutti questi dati vengono acquisiti nel framework CCDM, il risultato è un nuovo catalogo di base unificato disponibile nella pipeline di dati di Catalog Service. Nella parte successiva del diagramma vengono visualizzati più canali. Ogni canale rappresenta una business unit. Ad esempio, *Vendita al dettaglio in Texas*, *Vendita al dettaglio in Texas stagionale* e così via. Come è possibile vedere dal diagramma, le impostazioni internazionali, le policy e i listini prezzi possono essere condivisi tra i diversi canali&#x200B;

Infine, il diagramma mostra come questi dati distinti del catalogo possano essere visualizzati in varie posizioni, ad esempio in una vetrina Edge Delivery Services, in un mercato, in un canale pubblicitario, in una vetrina personalizzata e così via.

Per informazioni su come acquisire i dati del catalogo in CCDM utilizzando l&#39;API di acquisizione dati del catalogo e su come impostare le impostazioni internazionali, i criteri e i listini prezzi utilizzando l&#39;API gestione catalogo e regole, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Per ulteriori informazioni sui concetti che compongono CCDM, vedere le sezioni seguenti.

## Gestione catalogo prodotti

La gestione del catalogo dei prodotti comprende due aspetti distinti: i dati dei prodotti e il contesto dei prodotti. Il CCDM rispetta la separazione di questi compiti, offrendo una gestione indipendente per ciascuno di essi.

- **Dati prodotto** - Quale prodotto è in vendita e a quale prezzo?
- **Contesto del prodotto** - Chi vende a chi e dove?

![[!DNL Composable Catalog Data Model] aspetti](assets/ccdm-parts.png)

### Dati prodotto

I dati di prodotto includono i seguenti tipi:

- **Prodotti** - Singoli SKU o raccolte di SKU che rappresentano beni fisici o servizi immateriali con attributi che rappresentano il prodotto, tra cui descrizione, peso, dimensioni e molto altro. Gli attributi specificano anche gli ambiti di canale e criteri per uno SKU. I prodotti possono essere raggruppati in vari tipi di prodotti, ad esempio semplici, configurabili, bundle, bundle di bundle, abbonamenti e altro ancora.
- **Metadati** - I metadati dell&#39;attributo del prodotto definiscono e gestiscono la modalità di visualizzazione degli attributi del prodotto nella vetrina in elenchi di prodotti, pagine di dettaglio, risultati di ricerca e così via. I metadati definiscono inoltre il modo in cui gli attributi del prodotto vengono utilizzati nella ricerca: ordinamento, filtro, ponderazione della ricerca e così via.
- **Listini prezzi e listini prezzi** - Determina i prezzi di vendita dei prodotti. In CCDM, uno SKU di prodotto e un prezzo sono disaccoppiati, pertanto hai il potere di definire più listini prezzi per un singolo SKU. Separando i prezzi dallo SKU, puoi sbloccare i prezzi specifici dell’ambito tra diversi livelli cliente, business unit e aree geografiche. Puoi definire prezzi regolari e scontati e gestire tutto questo su larga scala.
- **Assets** - Artefatti associati a prodotti quali immagini, video, PDF o altri tipi di file (roadmap futura).

### Gestione del contesto del prodotto

La gestione del contesto del prodotto riguarda i seguenti aspetti:

- **Canale** - Il canale di distribuzione definisce il percorso attraverso cui un&#39;azienda desidera vendere i prodotti. Un canale è l’astrazione di livello più alto che racchiude le impostazioni internazionali e i criteri.
   - Esempio: rivenditori per l&#39;industria automobilistica. Filiali di conglomerati multimarca. Ubicazione di produzione per i fornitori.
- **Criterio** - Filtro di accesso ai dati che ti consente di inviare il contenuto corretto alla destinazione giusta. Questo concetto abilita le funzionalità di distribuzione del catalogo.
   - Esempio: punti vendita negozi fisici, mercati, pipeline pubblicitarie (Google, Facebook, Instagram)
- **Ambito** - Rappresenta la lingua (lingua) per i cataloghi, ad esempio `en-US`. L’ambito viene impostato a livello di SKU durante l’inserimento dei dati del catalogo.

Durante l’acquisizione e l’aggiornamento dei dati del prodotto, uno SKU contiene i dettagli di ambiti e attributi (gli attributi vengono mappati su canali e criteri). Questi definiscono gli identificatori del contesto del prodotto a cui appartiene una SKU:

![[!DNL Composable Catalog Data Model] identificatori contesto prodotto](assets/ccdm-product-id.png)

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

Mapping di canali, criteri e ambiti ![[!DNL Composable Catalog Data Model]](assets/ccdm-scope-map.png)

- **Ambito** (impostazioni locali): impostato a livello SKU durante l&#39;acquisizione dei dati del prodotto.&#x200B;
- **Canale** - Definizione creata utilizzando API dedicate. &#x200B;
- **Criterio** - Definizione creata utilizzando API dedicate.

## Funzioni principali

| Funzioni principali | Beneficio |
|---|---|
| **Acquisizione diretta dei dati del catalogo nella pipeline dei servizi di vetrina**: acquisisci i dati del catalogo direttamente nella pipeline del servizio di catalogo per il ciclo di vita di ricerca e navigazione di vetrina (pagina di visualizzazione del prodotto, pagina dell&#39;elenco dei prodotti, pagina dei risultati di ricerca e così via). | <ul><li>Acquisisci direttamente i dati del catalogo nella pipeline del servizio di vetrina che alimenta: Catalog Service, Product Discovery (Live Search) e Product Recommendations. Con questo, puoi distribuire aggiornamenti del catalogo su larga scala per milioni di SKU. Questo consente di gestire le promozioni su larga scala in base al tempo. </li></ul> |
| **Nuovi ambiti prodotti del catalogo**: canale, criteri e ambito sono nuovi ambiti prodotti introdotti da CCDM. Questi ambiti prodotto sostituiscono gli ambiti sito web, store e storeview nel livello servizi vetrina. [Ulteriori informazioni](#product-context-management). | <ul><li>Con i nuovi ambiti, CCDM semplifica la scalabilità a casi di utilizzo con più aree geografiche, più business unit, più marchi e più lingue utilizzando un unico catalogo di base.</li><li>Eliminazione della ridondanza dei dati nella gestione dei cataloghi.</li></ul> |
| **Scalabilità a decine di milioni di SKU** | Gestione del catalogo su larga scala. Qui è possibile acquisire e gestire con facilità oltre 200 MM SKU. |
| **Supporto per i tipi di prodotto** | <ul><li>Semplice, configurabile</li><li>Bundle e bundle di bundle (roadmap futura)</li><li>Abbonamenti e piani (roadmap futura)</li></ul> |
| **Commercio headless** | <ul><li>Supporto completo per le implementazioni di e-commerce headless tramite le API Catalog Service, Product Discovery (Live Search) e Product Recommendations.</li></ul> |
| **Componenti dell&#39;interfaccia utente moderni e veloci** | <ul><li>Supporto dei componenti dell’interfaccia utente predefiniti per la ricerca dei prodotti e i consigli di prodotto.</li><li>I componenti dell’interfaccia utente sono estensibili e flessibili e possono essere utilizzati sia dal servizio Edge Delivery di Adobe che da qualsiasi altra implementazione storefront.</li></ul> |

## Quale tipologia di esercenti trae il massimo vantaggio dal CCDM?

La tabella seguente illustra le problematiche comuni incontrate dai commercianti e il modo in cui CCDM le affronta.

| Tipo di commerciante | Caso d’uso | Problemi risolti |
|---|---|---|
| Conglomerato multimarca | <ul><li>Vendono diversi marchi</li><li>Vendono in diversi paesi</li><li>Vendono in diverse lingue</li></ul> | Utilizza un catalogo unificato basato su un&#39;unica base e ottieni efficienza operativa con l&#39;espansione a diversi marchi, aree geografiche e lingue. |
| Conglomerato di parti di automobili/produzione | <ul><li>Vende parti automatiche o meccaniche. I prodotti sono gli stessi per tutti i clienti.</li><li>Diversi dealer vendono pezzi ai clienti</li><li>Ogni dealer ha i propri prezzi, stock e metodi di spedizione</li></ul> | Per avere diverse integrazioni di spedizione, ogni rivenditore deve disporre di un sito Web separato. Tuttavia, siti web separati forzano il tipico modello di dati di catalogo a duplicare i dati. Quindi, se ci sono 3000 rivenditori negli Stati Uniti, un commerciante crea 3000 copie del catalogo anche se lo stesso catalogo è utilizzato da tutti i rivenditori. Questa duplicazione dei dati interferisce con i limiti delle prestazioni. Il CCDM elimina la duplicazione dei dati. |
| Impresa di imballaggio/logistica | <ul><li>Hanno diverse sedi di spedizione</li><li>Hanno un prezzo diverso per ogni cliente</li><li>Lo stesso prodotto disponibile in 2 sedi per 2 clienti ha 4 prezzi possibili</li></ul> | Nonostante l&#39;utilizzo di gruppi di clienti per coprire i prezzi per cliente, il modello di dati di catalogo tipico non ha la capacità di gestire i prezzi per posizione. Inoltre, i commercianti desiderano regole di visibilità univoche per posizione/sito web. La gestione di tali regole complesse di prezzo e visibilità può essere sbloccata su larga scala con il CCDM. |

### Dove andare da qui

- Acquisire dati in CCDM utilizzando [Data Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Gestisci il tuo catalogo e definisci i canali, i criteri e gli ambiti utilizzando [API di gestione catalogo](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Completa un&#39;esercitazione](https://developer-stage.adobe.com/commerce/services/composable-catalog/ccdm-use-case/) che mostra come un&#39;azienda con un singolo catalogo di base può utilizzare le API CCDM per aggiungere dati di prodotto, definire cataloghi utilizzando le proiezioni e recuperare i dati di catalogo da visualizzare in una vetrina headless.
