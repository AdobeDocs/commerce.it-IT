---
title: Migra a  [!DNL Adobe Commerce as a Cloud Service]
description: Scopri come eseguire la migrazione a  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
role: Developer
level: Intermediate
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '3020'
ht-degree: 0%

---

# Migra a [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] fornisce una guida completa per gli sviluppatori che passano da un&#39;implementazione Adobe Commerce PaaS esistente alla nuova offerta Adobe Commerce as a Cloud Service (SaaS). Adobe Commerce as a Cloud Service rappresenta un passaggio significativo verso un modello SaaS completamente gestito e senza versioni, che offre prestazioni migliorate, scalabilità, operazioni semplificate e una maggiore integrazione con il più ampio [!DNL Adobe Experience Cloud].

>[!NOTE]
>
>Per ulteriori informazioni sugli strumenti di migrazione, vedere [Strumento di migrazione dati in blocco](./bulk-data.md).

## Comprendere la transizione: confrontare PaaS e SaaS

**Differenze chiave**

* [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."} **PaaS (corrente)**: il commerciante gestisce il codice dell&#39;applicazione, gli aggiornamenti, l&#39;applicazione di patch e la configurazione dell&#39;infrastruttura nell&#39;ambiente ospitato di Adobe. [Modello di responsabilità condiviso](https://experienceleague.adobe.com/it/docs/commerce-operations/security-and-compliance/shared-responsibility) per i servizi (MySQL, Elasticsearch e altri).
* [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} **SaaS (Nuovo - [!DNL Adobe Commerce as a Cloud Service])**: Adobe gestisce completamente l&#39;applicazione di base, l&#39;infrastruttura e gli aggiornamenti. I commercianti si concentrano sulla personalizzazione tramite punti di estensibilità (API, App Builder, UI SDK). Il codice dell’applicazione core è bloccato.

**Implicazioni di architettura**

* **Piattaforma senza versione**: aggiornamenti continui non significano più aggiornamenti di versione principali per il core.
* **Microservizi e API-first**: maggiore fiducia nelle API per estensibilità e integrazione.
* **Headless per impostazione predefinita (facoltativo)**: supporto avanzato per storefront separati (ad esempio, Commerce Storefront con tecnologia Edge Delivery Services).
* **Edge Delivery Services**: impatto sulle prestazioni e sulla distribuzione front-end.

**Nuovi strumenti e concetti**

* [Mesh API per Adobe Developer App Builder](https://developer.adobe.com/app-builder/) e [per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=it)
* Provisioning self-service con [Commerce Cloud Manager](../getting-started.md#create-an-instance)

## Percorsi di migrazione

[!DNL Adobe Commerce as a Cloud Service] supporta più percorsi di migrazione, a seconda della timeline, della vetrina e delle personalizzazioni.

In alternativa alla migrazione completa, [!DNL Adobe Commerce as a Cloud Service] supporta una migrazione graduale utilizzando Commerce Optimizer o un approccio incrementale.

* **Migrazione incrementale**: questo approccio prevede la migrazione di dati, personalizzazioni e integrazioni in più fasi. Questo approccio è ideale per i grandi commercianti con molte personalizzazioni che desiderano passare gradualmente le loro personalizzazioni complesse e i dati a [!DNL Adobe Commerce as a Cloud Service] al proprio ritmo.

![migrazione incrementale](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer** - Questo approccio consente di eseguire la migrazione iterativa utilizzando Commerce Optimizer come fase di transizione per spostare personalizzazioni e dati complessi in [!DNL Adobe Commerce as a Cloud Service] al proprio ritmo. Commerce Optimizer fornisce l&#39;accesso ai servizi di merchandising basati su visualizzazioni e criteri del catalogo, Commerce Storefront basato su Edge Delivery e [!DNL Product Visuals powered by AEM Assets].

![migrazione iterativa](../assets/optimizer.png){width="600" zoomable="yes"}

* **Migrazione completa**: questo approccio comporta la migrazione simultanea di tutti i dati, le personalizzazioni e le integrazioni. Questo approccio è ideale per i commercianti più piccoli con poche personalizzazioni che desiderano passare rapidamente a [!DNL Adobe Commerce as a Cloud Service].

La tabella seguente fornisce una panoramica del processo di migrazione per diversi storefront e configurazioni:

|                    | LUMA Storefront | PWA Storefront | Commerce Storefront con tecnologia Edge Delivery | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migrazione dei dati | Obbligatorio | Obbligatorio | Obbligatorio | Obbligatorio |
| Vetrina | Migrare a Commerce Storefront con tecnologia Edge Delivery | Migrare a Commerce Storefront con tecnologia Edge Delivery o mantenere | Nessun impatto | Nessun impatto |
| Mesh API | Crea nuova trama | Crea nuova rete o riconfigura esistente | Crea nuova rete o riconfigura esistente | Crea nuova rete o riconfigura esistente |
| Integrazioni | Utilizzo del kit di avvio per l&#39;integrazione | Utilizzo del kit di avvio per l&#39;integrazione | Utilizzo del kit di avvio per l&#39;integrazione | Utilizzo del kit di avvio per l&#39;integrazione |
| Personalizzazioni | Passa ad App Builder e Mesh API | Passa ad App Builder e Mesh API | Passa ad App Builder e Mesh API | Passa ad App Builder e Mesh API |
| Gestione Assets | Migrazione necessaria se si utilizza OOTB | Migrazione necessaria se si utilizza OOTB | Migrazione necessaria se si utilizza OOTB | Migrazione necessaria se si utilizza OOTB |
| Estensioni | Migrare ad App Builder | Migrare ad App Builder | Migrare ad App Builder | Migrare ad App Builder |

Come indicato nella tabella, le mitigazioni per ogni migrazione consisteranno in:

* **Migrazione dei dati** - Utilizzo degli [strumenti di migrazione](./bulk-data.md) forniti per eseguire la migrazione dei dati dall&#39;istanza esistente a [!DNL Adobe Commerce as a Cloud Service].
* **Storefront**: gli storefront Commerce esistenti basati su Edge Delivery e gli storefront headless non richiedono alcuna mitigazione, ma gli storefront Luma richiedono la migrazione a Commerce Storefront basati su Edge Delivery. È possibile migrare le vetrine dei negozi PWA Studio a Commerce basate su Edge Delivery o mantenerle nello stato corrente. Adobe fornirà acceleratori per assistere la migrazione della vetrina.
* **[Rete API](https://developer.adobe.com/graphql-mesh-gateway)**—Crea una nuova rete o modifica quella esistente. Per facilitare questo processo, Adobe fornirà delle maglie preconfigurate.
* **Integrazioni** - Tutte le integrazioni devono utilizzare il [kit di avvio dell&#39;integrazione](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) o l&#39;[[!DNL Adobe Commerce as a Cloud Service] API REST](https://developer.adobe.com/commerce/webapi/reference/rest/saas/).
* **Personalizzazioni** - Tutte le personalizzazioni devono essere spostate in App Builder e API Mesh.
* **Gestione Assets**: la gestione di tutte le risorse richiede la migrazione. Se utilizzi già [!DNL AEM Assets], non è necessario eseguire la migrazione.
* **Estensioni** - Tutte le estensioni in-process devono essere ricreate come estensioni out-of-process. Entro la fine del 2025, Adobe fornirà l’accesso alle nostre estensioni più popolari per ridurre al minimo i tempi di build.

## Fasi di migrazione

Le fasi seguenti descrivono i passaggi e le considerazioni necessari per la migrazione a [!DNL Adobe Commerce as a Cloud Service].

### Valutazione e pianificazione pre-migrazione

Questa fase è fondamentale per ridurre al minimo i rischi e stabilire un percorso di migrazione chiaro e identificare i problemi prima che si presentino.

**Individuazione e controllo dell&#39;ambiente corrente**

**Analisi codebase:**

* Identifica tutti i moduli personalizzati, i temi e le sostituzioni.
* Analizza le modifiche al codice di base e determina quale sarà il refactoring necessario per la migrazione.
* Valutare le estensioni di terze parti e determinare la compatibilità con [!DNL Adobe Commerce as a Cloud Service]. Esistono alternative compatibili con SaaS oppure è necessario creare integrazioni API personalizzate o applicazioni App Builder?
* Identifica eventuali codici o funzionalità obsoleti che non verranno migrati.

**Controllo dati:**

* Valutare le dimensioni e la complessità del database.
* Identifica i dati o le tabelle non utilizzati per la pulizia.
* Esaminare i processi di importazione/esportazione dei dati esistenti.

**Valutazione integrazioni:**

* Elenca tutti i sistemi esterni integrati con Adobe Commerce (ERP, CRM, PIM, gateway di pagamento, fornitori di servizi di spedizione, OMS e qualsiasi altro sistema).
* Valuta i metodi di integrazione (API, script personalizzati e altri metodi).
* Valutare la compatibilità con l&#39;approccio API-first di [!DNL Adobe Commerce as a Cloud Service] e App Builder.

**Benchmark delle prestazioni:**

* Documenta i punteggi correnti di Lighthouse, i tempi di caricamento delle pagine e gli indicatori prestazioni chiave (KPI, Key Performance Indicator), che forniscono una linea di base per misurare i miglioramenti successivi alla migrazione.

**Revisione configurazione protezione:**

* Valuta eventuali regole WAF personalizzate, inserisce nell&#39;elenco Consentiti di IP ed eventuali altre configurazioni di sicurezza.

**Definire l&#39;ambito e la strategia di migrazione:**

* **Migrazione graduale e all-at-once:** Valuta i pro e i contro di ogni approccio.
* **Identificare i processi aziendali principali:** Assegnare priorità alle funzionalità che devono essere migrate per prime, ad esempio:
   * Regole di determinazione prezzi complesse
   * Regole aziendali personalizzate applicate prima che un ordine venga ufficialmente inserito o elaborato
   * Calcoli delle imposte complessi
   * Convalide degli indirizzi
   * Logica personalizzata attivata dopo l’invio di un ordine
* **Storefront headless e monolitico:** punto decisionale per lo sviluppo di nuove storefront o per l&#39;adattamento di storefront esistenti.
* **Strategia di integrazione:** Determina in che modo verranno riorganizzate le integrazioni esistenti (Mesh API, App Builder, API diretta).
* **Strategia di migrazione dati:** determinare se si desidera eseguire la migrazione utilizzando dati cronologici completi, dati parziali o nessun dato migrato.

**Preparazione e formazione del team:**

* Acquisisci familiarità con [!DNL Adobe Commerce as a Cloud Service] concetti, flussi di lavoro di sviluppo e nuovi strumenti.
* Partecipa a corsi di formazione pratici con le pipeline di distribuzione Adobe App Builder, Edge Delivery Services e [!DNL Adobe Commerce as a Cloud Service].

**Configurazione e provisioning ambiente:**

* Esegui il provisioning della sandbox [!DNL Adobe Commerce as a Cloud Service] e degli ambienti di sviluppo con Commerce Cloud Manager.

### Fasi di migrazione incrementale

**Refactoring strategico ed esternalizzazione**

Questa fase è costituita dal nucleo della migrazione e si concentra sull&#39;adattamento della base di codice al paradigma nativo per il cloud [!DNL Adobe Commerce as a Cloud Service]. Ciò comporta l’adozione strategica di nuovi servizi Adobe e lo spostamento della logica personalizzata fuori dalla piattaforma Commerce di base.

#### &#x200B;1. Migrare personalizzazioni ed estensioni &quot;in-process&quot; ad App Builder

Si tratta di una fase cruciale per il raggiungimento di un &quot;nucleo bloccato&quot; e per garantire il futuro della tua soluzione, fondamentale per la filosofia architettonica di [!DNL Adobe Commerce as a Cloud Service].

* **Esternalizzare la logica complessa in App Builder**: analizza i moduli personalizzati esistenti e le estensioni di terze parti all&#39;interno della base di codice PaaS. Per logiche di business complesse, integrazioni personalizzate o microservizi che non richiedono la manipolazione diretta e in-process del modello dati di base di Commerce, esegui il refactoring e la ripiattaforma come applicazioni senza server all’interno di Adobe Developer App Builder.
* **Sfrutta la rete API**: per scenari che richiedono dati da più sistemi back-end (ad esempio, il backend Commerce PaaS, i microservizi ERP, CRM e App Builder personalizzati), implementa un livello Mesh API in App Builder. Questo consolida API diverse in un unico endpoint GraphQL performante utilizzato dalla nuova vetrina o da altri servizi, semplificando il recupero di dati complessi.
* **Architettura basata sugli eventi**: utilizza Adobe I/O Events per attivare le azioni di App Builder in base agli eventi che si verificano nell&#39;istanza PaaS (ad esempio aggiornamenti dei prodotti, registrazioni dei clienti, modifiche dello stato degli ordini) o in altri sistemi connessi. Questo favorisce la comunicazione asincrona, riduce l&#39;accoppiamento stretto e migliora la resilienza del sistema.

**Vantaggio**: questo passaggio riduce in modo significativo il debito tecnico associato a personalizzazioni profondamente incorporate, velocizza notevolmente la transizione dell&#39;istanza Commerce a [!DNL Adobe Commerce as a Cloud Service], migliora la scalabilità e la distribuzione indipendente della logica personalizzata e promuove cicli di sviluppo più rapidi per le estensioni.

#### &#x200B;2. Adottare i servizi di merchandising Adobe Commerce basati su SaaS e integrare i dati del catalogo

Si tratta di un punto di integrazione iniziale fondamentale con due opzioni relative alla gestione dei dati di catalogo:

>[!BEGINTABS]

>[!TAB Opzione 1 - Servizio SaaS catalogo esistente]

**Sfrutta il servizio SaaS del catalogo esistente integrato con il back-end PaaS**

Questa opzione funge da passaggio transitorio, basato su un&#39;integrazione esistente in cui il backend PaaS popola un&#39;istanza esistente del servizio Adobe Commerce SaaS con i dati del [servizio catalogo](../../catalog-service/guide-overview.md), [ricerca live](../../live-search/overview.md) e [consigli prodotto](../../product-recommendations/overview.md).

* **Sincronizzazione dati catalogo**: assicurati che l&#39;istanza Adobe Commerce PaaS continui a sincronizzare i dati di prodotto e catalogo con il servizio Adobe Commerce Catalog SaaS esistente. In genere si basa su connettori o moduli consolidati all’interno dell’istanza PaaS. Il servizio catalogo SaaS rimane la fonte autorevole per le funzioni di ricerca e merchandising, derivando i suoi dati dal backend PaaS.
* **Mesh API per l&#39;ottimizzazione**: anche se la vetrina headless (su Edge Delivery Services) e altri servizi potrebbero utilizzare direttamente i dati del servizio SaaS del catalogo, Adobe consiglia vivamente di utilizzare Mesh API (in App Builder). La funzione Mesh API può unificare le API del servizio SaaS per il catalogo con altre API necessarie dal backend PaaS (ad esempio, controlli di inventario in tempo reale dal database transazionale o attributi di prodotto personalizzati non completamente replicati nel servizio SaaS per il catalogo) in un singolo endpoint GraphQL dalle prestazioni elevate. Ciò consente anche la memorizzazione in cache centralizzata, l’autenticazione e la trasformazione della risposta.
* **Integrazione di Live Search e Product Recommendations**: configura i servizi SaaS di Live Search e Product Recommendations per [acquisire i dati del catalogo](https://experienceleague.adobe.com/it/docs/commerce/live-search/install#configure-the-data) direttamente dal servizio SaaS del catalogo Adobe Commerce esistente, che a sua volta viene popolato dal backend PaaS.

**Vantaggio**: consente di accedere più rapidamente a una vetrina headless e a funzioni di merchandising SaaS avanzate sfruttando un servizio SaaS Catalog esistente e operativo e la relativa pipeline di integrazione con il backend PaaS. Tuttavia, mantiene la dipendenza dal backend PaaS per l’origine dati del catalogo principale e non fornisce le funzionalità di aggregazione multiorigine intrinseche al nuovo Composable Catalog Data Model. Questa opzione rappresenta un valido passo avanti verso un&#39;architettura più completa e componibile.

>[!TAB Opzione 2 - Modello dati catalogo componibile]

**Adottare il nuovo Composable Catalog Data Model (CCDM)**

Questo è l&#39;approccio strategico e a prova di futuro per sfruttare al meglio Adobe Commerce Optimizer. CCDM fornisce un servizio di catalogo flessibile, scalabile e unificato progettato per l’aggregazione di dati da più origini e il merchandising dinamico.

* **Acquisizione e unificazione dei dati**
   * Inizia acquisendo i dati di prodotti e cataloghi dall’istanza Adobe Commerce PaaS esistente (e/o da altri sistemi PIM/ERP) nel nuovo Composable Catalog Data Model (CCDM).
   * Mappa gli attributi di prodotto esistenti sullo schema flessibile del CCDM. Dai priorità ai dati critici del prodotto per l’acquisizione iniziale.
   * Stabilisci pipeline di dati affidabili per la sincronizzazione continua. Ciò può comportare:
      * **Basato su eventi** (tramite App Builder): utilizza Adobe I/O Events dalla tua istanza PaaS per attivare le applicazioni Adobe App Builder personalizzate o disponibili al pubblico. Queste applicazioni trasformano e inviano le modifiche ai dati (creazione, aggiornamento ed eliminazione) al CCDM tramite le relative API.
      * **Acquisizione in batch**: per caricamenti iniziali di grandi dimensioni o aggiornamenti in blocco periodici, utilizza trasferimenti di file protetti (ad esempio, CSV o JSON) in un&#39;area di gestione temporanea, elaborati dai servizi di acquisizione di Adobe Experience Platform (AEP) in CCDM.
      * **Integrazione API diretta** (con orchestrazione App Builder): per scenari più complessi, App Builder può fungere da livello di orchestrazione, effettuando chiamate API dirette al backend PaaS, trasformando i dati e inviandoli a CCDM.
* **Visualizzazione catalogo e definizione dei criteri**: configurare le visualizzazioni catalogo (raggruppamenti logici per la presentazione di cataloghi univoci, ad esempio visualizzazioni archivio, aree geografiche e segmenti B2B/B2C) e definire i criteri (set di regole per la presentazione, il filtraggio e il merchandising dei prodotti) in CCDM. Ciò consente il controllo dinamico su assortimenti di prodotti e logica di visualizzazione per vista catalogo.
* **Integrare Live Search e Product Recommendations**: una volta che i dati del catalogo sono presenti in CCDM, integrare i servizi di Adobe basati su SaaS Live Search e Product Recommendations. Questi sfruttano l’intelligenza artificiale e i modelli di apprendimento automatico di Adobe per migliorare la rilevanza delle ricerche e offrire consigli personalizzati, sfruttando i dati direttamente dal CCDM.

**Vantaggio**: astragendo la gestione e l&#39;individuazione del catalogo in CCDM e nei servizi SaaS associati, puoi ottenere prestazioni migliori, acquisire funzionalità di merchandising basate sull&#39;intelligenza artificiale, ridurre notevolmente il carico delle operazioni di lettura dal backend legacy e abilitare un&#39;esperienza &quot;peel-off&quot; affidabile dell&#39;esperienza top-of-funnel.

>[!ENDTABS]

#### &#x200B;3. Costruisci la vetrina su Edge Delivery Services

Con le pipeline di dati di merchandising stabilite e le personalizzazioni esternalizzate, l’attenzione si sposta sulla creazione di front-end ad alte prestazioni.

* **Configurazione iniziale**: configura il progetto utilizzando Adobe Commerce Storefront boilerplate per Edge Delivery Services. Questo fornisce un front-end headless fondamentale basato sulle moderne tecnologie web.
* **Connetti a Catalog Services e Mesh API**: la vetrina Commerce utilizzerà i dati principalmente tramite le API GraphQL:
   * **Opzione 1**: dal servizio SaaS del catalogo esistente (tramite Mesh API) per informazioni sul prodotto e regole di merchandising.
   * **Opzione 2**: da CCDM per informazioni sul prodotto e regole di merchandising.
   * Da Mesh API per tutti i dati orchestrati dal backend legacy (istanza PaaS) o dai servizi App Builder personalizzati (ad esempio, visualizzazione dell’inventario in tempo reale, degli attributi di prodotto personalizzati e dei punti fedeltà).
* **Migrazione dei contenuti (AEM Services)**: esegui la migrazione dei contenuti statici esistenti (ad esempio, pagine &quot;Chi siamo&quot;, post di blog e banner di marketing) in AEM Services, per alimentare Commerce Storefront. Sfrutta le funzionalità di authoring dei contenuti di AEM e assicurati che le risorse siano ottimizzate per Edge Delivery Services.
* **Sviluppa componenti core dell&#39;interfaccia utente**: crea componenti critici dell&#39;interfaccia utente per le pagine dei dettagli del prodotto (PDP), le pagine di elenco dei prodotti (PLP) e le pagine di contenuto generale utilizzando i componenti di menu a discesa di Edge Delivery Services e i componenti React/Vue personalizzati. Assegna la priorità ai flussi commerce di base.
* **Integrazione con carrello/pagamento esistente**: inizialmente, la vetrina Edge Delivery Services orchestrerà un passaggio al tuo Adobe Commerce PaaS esistente (o altra piattaforma di terze parti) per la gestione del carrello e il pagamento. Ciò comporta in genere:
   * **Reindirizzamento**: reindirizzamento dell&#39;utente al carrello nativo della piattaforma legacy e agli URL di estrazione, passando gli identificatori di sessione e carrello necessari.
   * **Interazione API diretta** (con orchestrazione App Builder): creazione di componenti dell&#39;interfaccia utente per il carrello e il pagamento personalizzati in Edge Delivery Services che interagiscono direttamente con le API del backend PaaS per il pagamento e il carrello. Questo spesso coinvolge App Builder as a Backend-for-Frontend (BFF) per orchestrare chiamate a più servizi back-end (ad esempio, carrello PaaS, gateway di pagamento e calcolatori di spedizione).

**Vantaggio**: offre un&#39;esperienza di vetrina incredibilmente veloce, ottimizzata per SEO e altamente flessibile. Questa fase contribuisce direttamente a migliorare l’esperienza del cliente e getta le basi per future innovazioni front-end.

#### &#x200B;4. Migrazione dei dati (processo graduale)

La migrazione dei dati è un processo critico e complesso che viene eseguito contemporaneamente al refactoring e allo sviluppo della vetrina, garantendo la coerenza e l&#39;integrità dei dati.

* **Pulizia e ottimizzazione dei dati esistenti**: prima di qualsiasi migrazione su larga scala, eseguire operazioni complete di pulizia, deduplicazione e convalida dei dati nel database PaaS esistente. Questo passaggio proattivo è fondamentale per ridurre al minimo il trasferimento di problemi di dati legacy e garantire la qualità dei dati nel nuovo ambiente.

**Migrazioni di dati in blocco**

La migrazione dei dati in blocco comporta l’acquisizione di un’immagine completa dei dati dall’istanza Adobe Commerce PaaS, la trasformazione dell’intero set di dati e l’importazione in Adobe Commerce as a Cloud Service in un’unica operazione. Questo metodo viene in genere utilizzato per la popolazione iniziale di dati.

* **Disponibilità degli strumenti**: a metà luglio 2025 saranno disponibili su richiesta [strumenti per la migrazione di dati in blocco](./bulk-data.md) dedicati per l&#39;utilizzo da parte del cliente per le migrazioni di dati in blocco di Commerce di prime parti. Se i clienti necessitano di assistenza per la migrazione in blocco dei dati in anticipo, Adobe può facilitare il trasferimento di dati per loro conto su richiesta.

* **Processo**:
   * **Esportazione completa dei dati**: estrae un set di dati completo dall&#39;istanza Adobe Commerce PaaS (ad esempio prodotti, categorie, account cliente, dati cronologici degli ordini, blocchi statici e contenuto della pagina).
   * **Trasformazione dei dati**: applica le trasformazioni necessarie per allineare i dati estratti ai requisiti dello schema dei nuovi componenti di Adobe Commerce as a Cloud Service, incluso il Composable Catalog Data Model (CCDM), se adottato, e a tutti gli altri servizi o database Adobe pertinenti. Ciò può richiedere script personalizzati o strumenti di mappatura dei dati specializzati.
   * **Importazione iniziale**: importa il set di dati completo trasformato nei rispettivi componenti di Adobe Commerce as a Cloud Service. Per i dati di prodotto e categoria, viene compilato il servizio catalogo scelto (CCDM o SaaS catalogo esistente). Per i dati relativi a clienti e ordini, questo popolerà il backend transazionale o i servizi associati.
   * **Convalida**: convalida rigorosamente i dati importati per garantire la completezza, l&#39;accuratezza e la coerenza in tutti i nuovi sistemi.

**Migrazioni iterative dei dati**

Le migrazioni iterative dei dati si concentrano sulla sincronizzazione di modifiche e delta incrementali dall’istanza PaaS di origine ai nuovi componenti Cloud Service, per garantire l’aggiornamento dei dati prima e dopo il cutover.

* **Disponibilità degli strumenti**: gli strumenti progettati specificamente per le migrazioni iterative dei dati saranno disponibili nella seconda metà del 2025.

* **Processo**:
   * **Identificazione delta**: stabilire meccanismi per identificare le modifiche (creazioni, aggiornamenti ed eliminazioni) nei set di dati critici nell&#39;ambiente PaaS dall&#39;ultima sincronizzazione. Questo può comportare l’acquisizione di dati di modifica (CDC), confronti di marche temporali o trigger basati su eventi.
   * **Sincronizzazione continua**: implementa solidi meccanismi per la sincronizzazione continua e incrementale dei dati dall&#39;ambiente PaaS ai nuovi componenti di Cloud Service (ad esempio, CCDM e backend transazionale). Questo è fondamentale per mantenere l’aggiornamento dei dati e ridurre al minimo i tempi di inattività durante il passaggio al nuovo sistema.
   * **Utilizzo degli eventi**: utilizza Adobe I/O Events laddove possibile per attivare le azioni di App Builder per aggiornamenti in tempo reale o quasi reale dall&#39;istanza PaaS ai nuovi servizi. Ad esempio, un aggiornamento del prodotto in PaaS potrebbe attivare un evento che aggiorna la voce corrispondente in CCDM.
   * **Aggiornamenti basati su API**: per i dati non basati su eventi, utilizza chiamate API pianificate (tramite App Builder o altre piattaforme di integrazione) per richiamare le modifiche da PaaS e inviarle ai nuovi sistemi.
   * **Gestione e monitoraggio degli errori**: implementa funzioni affidabili di gestione, registrazione e monitoraggio degli errori per tutte le pipeline iterative dei dati per garantire l&#39;integrità dei dati durante l&#39;intero processo.

### Operazioni successive alla migrazione e in corso

**Copertura DNS e pubblicazione:**

* Pianifica attentamente il cutover DNS con tempi di inattività minimi.
* Monitora lo stato e le prestazioni del sito subito dopo il lancio.

**Operazioni successive all&#39;avvio:**

**Disattivazione ambiente PaaS:**

* Archivia o elimina in modo sicuro le vecchie istanze PaaS e i dati dopo il periodo di convalida.

**Flusso di lavoro di sviluppo in corso:**

* Accettare la natura senza versione di [!DNL Adobe Commerce as a Cloud Service], che prevede distribuzioni continue di piccole dimensioni anziché aggiornamenti di grandi dimensioni.
* Utilizza Cloud Manager per gestire ambienti e implementazioni.
* Sfrutta App Builder per estendere le funzionalità senza influire sulle funzionalità principali.

**Monitoraggio, prestazioni e sicurezza:**

* Monitoraggio continuo delle prestazioni del sito, degli errori e dei registri di protezione.
* Utilizza le funzioni di sicurezza integrate di Adobe e rispetta le best practice.

**Formazione e documentazione:**

* Formazione di nuovi sviluppatori e utenti aziendali sulla piattaforma e sui flussi di lavoro [!DNL Adobe Commerce as a Cloud Service].
* Mantiene una documentazione interna aggiornata per le integrazioni e i processi personalizzati.
