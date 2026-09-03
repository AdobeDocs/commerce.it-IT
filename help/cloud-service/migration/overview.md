---
title: Migra a  [!DNL Adobe Commerce as a Cloud Service]
description: Scopri come eseguire la migrazione a  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-06-18T16:12:28.840Z'
TQID: 'https://experienceleague.adobe.com/GmxaQdGKvAIDpZ2jvmlLFSYw0IFQysIMOT0lUnsJBsI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 289267c4bb76bbe1e9f00fd02faa7749b812d0d0
workflow-type: tm+mt
source-wordcount: 3372
ht-degree: 0%

---

# Migra a [!DNL Adobe Commerce as a Cloud Service]

Questa guida aiuta gli sviluppatori a passare da [!DNL Adobe Commerce on Cloud] o on-premise a [!DNL Adobe Commerce as a Cloud Service] (SaaS). Questo modello SaaS offre prestazioni, scalabilità e integrazione migliorate con [!DNL Adobe Experience Cloud].

>[!NOTE]
>
>Per ulteriori informazioni sugli strumenti di migrazione, vedere [Strumento di migrazione dati in blocco](./bulk-data/migration-tool.md).

## Panoramica

La migrazione di un archivio [!DNL Adobe Commerce] stabilito in [!DNL Adobe Commerce as a Cloud Service] è più che uno spostamento di dati. Una vera migrazione interessa le seguenti aree:

- Applicazione: personalizzazioni ed estensioni create per [!DNL Adobe Commerce on Cloud] o installazioni locali
- Dati: cataloghi, ordini, clienti e configurazione
- Vetrina
- Integrazioni con sistemi esterni

[!DNL Adobe Commerce as a Cloud Service] è una piattaforma SaaS senza versione, il che significa che nessuna di queste aree può essere migrata senza adattarle. Le personalizzazioni vengono modernizzate in applicazioni [!DNL App Builder], le vetrine vengono ricostruite su Edge Delivery Services (EDS), i dati vengono migrati nel nuovo tenant [!DNL Adobe Commerce as a Cloud Service] e le integrazioni vengono ristabilite utilizzando modelli SaaS.

Invece di considerare la migrazione come un singolo progetto monolitico, Adobe fornisce un flusso di lavoro di migrazione integrato basato su [tre strumenti di migrazione](#migration-tools-workflow).

Questo flusso di lavoro condiviso consolida l’individuazione, allinea i team tecnici e di consegna e fornisce un piano di migrazione coerente.

![diagramma del flusso di migrazione](../assets/migration-flow.png)

### Confronto tra SaaS e PaaS

Adobe Commerce è disponibile in diversi modelli di distribuzione. Le principali differenze riguardano il livello di gestione dell&#39;infrastruttura, il controllo delle applicazioni, la personalizzazione e la responsabilità dell&#39;aggiornamento.

Le differenze tra [!DNL Adobe Commerce as a Cloud Service], [!DNL Adobe Commerce on Cloud] e [!DNL Adobe Commerce on-premises] riguardano le modalità di gestione e di interazione dei commercianti con la piattaforma.

| Offerta Adobe Commerce | Modello di hosting | Responsabilità dei servizi e degli aggiornamenti |
|---|---|---|
| **[!DNL Adobe Commerce as a Cloud Service]** | SaaS — ospitato da Adobe | Adobe gestisce l&#39;applicazione, l&#39;infrastruttura e gli aggiornamenti principali di Commerce. I commercianti estendono la piattaforma tramite API supportate e servizi di estensibilità (API, [!DNL Adobe Developer App Builder], SDK per l’interfaccia utente). Gli esercenti non possono modificare il codice dell’applicazione principale. |
| **[!DNL Adobe Commerce on Cloud Infrastructure]** | PaaS: gestito da Adobe | [Responsabilità condivisa](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility): Adobe gestisce la piattaforma ospitata. L’esercente gestisce le patch a livello di applicazione, il codice personalizzato, la configurazione e aggiorna le estensioni e i servizi della piattaforma alle versioni supportate, tra cui database, cache, ricerca, runtime PHP, server web e coda dei messaggi. |
| **[!DNL Adobe Commerce on-premises]** | Ospitato dal commerciante o dal provider di hosting | [Responsabilità dell&#39;esercente](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview#merchant-responsibilities): l&#39;esercente o il provider di hosting gestisce l&#39;infrastruttura e tutti i servizi della piattaforma. |

**Implicazioni di architettura**

- **Piattaforma senza versione**: aggiornamenti continui non significano più aggiornamenti di versione principali per il core.
- **Microservizi e API-first**: maggiore fiducia nelle API per estensibilità e integrazione.
- **Headless per impostazione predefinita (facoltativo)**: supporto avanzato per storefront separati (ad esempio, Commerce Storefront con tecnologia Edge Delivery Services).
- **Edge Delivery Services**: impatto sulle prestazioni e sulla distribuzione front-end.

**Nuovi strumenti e concetti**

- [Mesh API per Adobe Developer App Builder](https://developer.adobe.com/app-builder/) e [per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/)
- [Commerce Optimizer](../../optimizer/overview.md)
- [Servizi di consegna Edge](https://experienceleague.adobe.com/developer/commerce/storefront/)
- Provisioning self-service con [Commerce Cloud Manager](../getting-started.md#create-an-instance)

### Il percorso di migrazione

Una migrazione si sposta nelle seguenti fasi:

- **Valutazione** - Analizzare l&#39;implementazione esistente e considerare quanto segue: personalizzazioni di inventario, integrazioni, caratteristiche di vetrina e strutture di dati. Dopo l’analisi, crea una roadmap con consigli sulla migrazione, valutazione della complessità e stime dello sforzo.
- **Modernizzare l&#39;applicazione ed eseguire la migrazione dei dati**. Ricompilare le personalizzazioni come [!DNL App Builder] applicazioni durante la migrazione dei dati aziendali in [!DNL Adobe Commerce as a Cloud Service].
- **Modernizzare la vetrina** - Rigenerare la vetrina su Edge Delivery Services (EDS) per Commerce.
- **Tagliare e utilizzare** - Passare il traffico a [!DNL Adobe Commerce as a Cloud Service], disattivare i sistemi legacy e passare all&#39;operazione in corso.

La migrazione è solitamente iterativa, non lineare. Le organizzazioni possono valutare più ambienti, convalidare i consigli, modernizzare in modo incrementale e perfezionare i piani di implementazione prima del passaggio finale alla produzione.

### Flusso di lavoro per gli strumenti di migrazione

Ciascuno dei seguenti flussi di lavoro dispone di un proprio strumento. Utilizzali insieme per completare la migrazione con la valutazione della migrazione che funge da blueprint comune utilizzato per tutta la migrazione.

| Flusso di lavoro | Strumento | Descrizione |
| --- | --- | --- |
| [Valutazione](#migration-assessment-tool) | **Strumento di valutazione della migrazione** | Valutazione basata sull’intelligenza artificiale dell’implementazione esistente che inventario moduli personalizzati, estensioni di terze parti, integrazioni, osservazioni di vetrina, schema di database, tabelle personalizzate, consigli sulla migrazione, punteggio di complessità e stime dello sforzo di modernizzazione. |
| [Modernizzazione dell&#39;applicazione e della vetrina](#code-and-storefront-migration-commerce-developer-mcp) | **MCP sviluppatore Commerce** | La modernizzazione basata sull&#39;intelligenza artificiale dell&#39;applicazione Commerce accelera la migrazione delle personalizzazioni a [!DNL App Builder], supporta la trasformazione della vetrina in Edge Delivery Services (EDS) e guida gli sviluppatori attraverso il più ampio percorso di modernizzazione delle applicazioni con implementazione rivista e convalidata dai team di progettazione. |
| [Migrazione dati](#data-migration-commerce-data-migration-service) | **Servizio di migrazione dati di Commerce** | Estrazione, caricamento e verifica dell&#39;integrità dei dati di catalogo, cliente e ordine in [!DNL Adobe Commerce as a Cloud Service]. |

Queste tracce non sono autonome. L&#39;utilizzo congiunto di questi elementi nell&#39;ordine corretto consente di ridurre al minimo la rielaborazione.

- **Esegui prima la valutazione**: l&#39;esecuzione della valutazione identifica innanzitutto le personalizzazioni non supportate, stima lo sforzo di migrazione, espone le considerazioni sulla migrazione dei dati ed evidenzia le dipendenze di integrazione prima dell&#39;inizio dell&#39;implementazione. La valutazione diventa il modello di migrazione utilizzato sia dalla modernizzazione delle applicazioni che dai flussi di lavoro di migrazione dei dati.
- **Modernizzazione delle applicazioni** - Commerce Developer MCP utilizza la valutazione della migrazione per determinare quali personalizzazioni modernizzare e come. MCP genera quindi le applicazioni [!DNL App Builder] e i componenti storefront corrispondenti.
- **Migrazione dei dati** - Il questionario dell&#39;ambito di migrazione dei dati acquisisce l&#39;ambito, i volumi e le tabelle personalizzate visualizzati dalla valutazione.
- **Dati personalizzati e di terze parti** - I dati contenuti nelle tabelle personalizzate da estensioni di terze parti vengono identificati durante la valutazione, ma non vengono gestiti dalla migrazione dei dati standard e richiedono una personalizzazione [!DNL App Builder].

La modernizzazione della vetrina non è solo una migrazione dell’interfaccia utente. Oltre a migrare le funzionalità aziendali, è necessario considerare l’architettura dell’esperienza, la modernizzazione dei componenti riutilizzabili, l’ottimizzazione delle prestazioni e l’adozione di modelli Edge Delivery Services.

Le integrazioni sono valutate nell’ambito della valutazione della migrazione, ma la loro attuazione varia a seconda dello scenario. Le integrazioni possono sfruttare le API [!DNL App Builder], [!DNL API Mesh], Adobe I/O Events e [!DNL Adobe Commerce as a Cloud Service].

Questi strumenti di migrazione continuano a espandersi e a mantenere un flusso di lavoro di migrazione unificato incentrato sulla valutazione della migrazione.

### Passaggi successivi

Quando sei pronto per la migrazione, inizia creando una valutazione. La valutazione della migrazione stabilisce il piano che segue il resto della migrazione.

Lo strumento di valutazione della migrazione e Commerce Developer MCP utilizzano l’intelligenza artificiale per facilitare l’individuazione, la pianificazione e l’implementazione. Come per qualsiasi flusso di lavoro di progettazione, le raccomandazioni e le implementazioni generate dall’intelligenza artificiale devono essere attentamente esaminate e convalidate dal team come parte dell’architettura standard, dei processi di test e di controllo della qualità.

## Strumento di valutazione della migrazione

Prima di iniziare lo sviluppo o la migrazione, è necessario considerare le dimensioni della migrazione e determinare gli elementi che richiedono lo sviluppo. Un archivio [!DNL Adobe Commerce] in [!DNL Adobe Commerce on Cloud] o locale probabilmente include moduli personalizzati, integrazioni, personalizzazioni della vetrina e strutture di dati, che potrebbero non essere evidenti finché non viene analizzata l&#39;implementazione. Lo strumento di valutazione della migrazione analizza automaticamente la base di codice per identificare questi elementi da sviluppare.

### Panoramica sulla valutazione

Lo strumento di valutazione della migrazione esegue una valutazione IA dell&#39;implementazione esistente e produce una valutazione strutturata della modernizzazione e una roadmap di migrazione [!DNL Adobe Commerce as a Cloud Service]. Crea inoltre una visione completa della migrazione valutando le personalizzazioni delle applicazioni, le integrazioni, le strutture di dati, le caratteristiche della vetrina e altri dettagli di implementazione che influenzano la modernizzazione. Trasforma la scoperta in un processo rapido e ripetibile che consente di valutare l&#39;impegno, i rischi e la sequenza prima di assumere impegni.

La valutazione prodotta dallo strumento di valutazione della migrazione non è solo un rapporto. La valutazione diventa un artefatto di migrazione condiviso che informa la pianificazione, l&#39;implementazione e la convalida durante l&#39;intero ciclo di vita della migrazione. Come prima fase del percorso di migrazione, i risultati riguardano sia la modernizzazione delle applicazioni che gli sforzi di migrazione dei dati che ne derivano.

Per ulteriori informazioni su ciò che è incluso in un report di valutazione della migrazione e su come utilizzarlo, vedere [Valutazione della migrazione](./assessment.md).

### Fasi di valutazione

Una valutazione viene eseguita rispetto all&#39;implementazione esistente e procede attraverso una serie di fasi automatizzate:

- **Inventario** — Cataloga l&#39;implementazione. Include: moduli personalizzati, dipendenze del compositore, estensioni di terze parti, configurazione, componenti storefront (se applicabile), file, punti di estensibilità, eventi, plug-in, API, processi cron, code, schema di database e tabelle di database personalizzate.
- **Analizza**: esegue un&#39;analisi statica per identificare le personalizzazioni dell&#39;archivio, le differenze rispetto a un&#39;installazione standard di [!DNL Adobe Commerce] e il modo in cui tali personalizzazioni interagiscono nell&#39;applicazione.
- **Classifica**: utilizza l&#39;intelligenza artificiale per interpretare ogni personalizzazione, riepilogando le operazioni di personalizzazione, raggruppando le funzionalità correlate, identificando i modelli di implementazione e fornendo consigli contestuali sulla migrazione.
- **Mappa e consiglia**: esegue il mapping di ogni funzionalità al relativo equivalente [!DNL Adobe Commerce as a Cloud Service], tra cui: funzionalità predefinite, applicazioni [!DNL App Builder] o servizi Adobe. La valutazione consiglia quindi un percorso di modernizzazione e valuta la complessità, le dipendenze e lo sforzo di implementazione.
- **Report** - Genera una roadmap esportabile per la pianificazione dell&#39;esecuzione della migrazione, che consente di comunicare i rischi alle parti interessate. Identifica inoltre le priorità, le dipendenze, il debito tecnico e i rischi di implementazione.

### Valore di valutazione

Il valore di una valutazione è la quantità di affidabilità che si può avere prima di impegnarsi nelle specifiche di sviluppo. Anziché stimare una migrazione con pratiche di valutazione regolari, la valutazione fornisce una comprensione basata su elementi concreti dell’implementazione. Ciò include quali personalizzazioni sono semplici da migrare, quali richiedono una riprogettazione e quali possono essere completamente ritirate. Le valutazioni di solito presentano funzionalità obsolete o inutilizzate, che consentono di ridurre il debito tecnico.

Ogni raccomandazione include le prove di supporto e le citazioni relative all&#39;implementazione sottostante, che consentono agli architetti e ai tecnici di convalidare durante la pianificazione. Poiché ogni valutazione segue la stessa metodologia, è possibile confrontare più esigenze di sviluppo utilizzando un framework di valutazione e pianificazione coerente.

La valutazione non è solo un punto di partenza. Lo strumento di migrazione a valle utilizza i risultati della valutazione per accelerare l&#39;implementazione e mantenere la coerenza con il piano di migrazione approvato. L’analisi di personalizzazione diventa il blueprint per la modernizzazione delle applicazioni, mentre la valutazione dei dati definisce l’impegno di migrazione dei dati analizzando le dimensioni del database, l’inventario delle entità e le tabelle personalizzate.

### Ambito della valutazione

Lo strumento di valutazione della migrazione è incentrato sulla comprensione dell&#39;intero scenario di migrazione. Analizza moduli personalizzati, plug-in, eventi, API, processi cron, code, integrazioni con sistemi esterni, caratteristiche della vetrina e lo schema di database da cui dipendono tali personalizzazioni. La valutazione mappa ciò che rileva sulle funzionalità [!DNL Adobe Commerce as a Cloud Service] disponibili e identifica dove è necessario riprogettare l&#39;architettura SaaS o modernizzare le funzionalità utilizzando [!DNL App Builder].

La valutazione è più uno strumento di pianificazione che uno strumento di esecuzione. Identifica gli elementi da modernizzare, valuta la complessità dell’implementazione e fornisce consigli. Le decisioni sull’implementazione e la convalida dell’architettura rimangono attività di collaborazione tra Adobe, partner e team di progettazione dei clienti.

I dati memorizzati nelle tabelle personalizzate dalle estensioni di terze parti vengono presentati come una considerazione di migrazione. La migrazione dei dati standard non esegue automaticamente la migrazione di questi dati. Per supportare questi scenari potrebbero essere necessarie applicazioni [!DNL App Builder] personalizzate. Per ulteriori informazioni, consultare la [Guida alla migrazione dei dati](#data-migration-commerce-data-migration-service).

La valutazione fornisce analisi per la personalizzazione della vetrina e per i flussi di lavoro di migrazione dei dati:

- Migrazione di codice e vetrina: l&#39;analisi delle applicazioni della valutazione diventa il blueprint per Commerce Developer MCP
- Migrazione dei dati: l&#39;inventario delle entità, l&#39;analisi delle caratteristiche del database e l&#39;analisi personalizzata delle tabelle della valutazione definiscono l&#39;ambito del servizio di migrazione dei dati di Commerce.

È inoltre possibile eseguire nuovamente le valutazioni man mano che le applicazioni si evolvono. Questo consente ai team di convalidare il lavoro di correzione, misurare i progressi della modernizzazione e perfezionare continuamente i piani di migrazione durante l’intero progetto.

### Passaggi successivi

Ogni migrazione di [!DNL Adobe Commerce as a Cloud Service] inizia con una valutazione. Si tratta di un modo efficiente in termini di costi per stabilire l&#39;ambito, ridurre l&#39;incertezza e creare un piano di migrazione condiviso prima dell&#39;inizio dell&#39;implementazione.

Per ulteriori informazioni sugli strumenti di valutazione e sul flusso di lavoro per sviluppatori a valle, vedi [Adobe Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools/).

Per ulteriori informazioni su Commerce Developer Agent, integrato con lo strumento di valutazione della migrazione, vedere [Commerce Developer Agent](https://developer.adobe.com/commerce/extensibility/developer-agent/)

## Migrazione di codice e vetrina (Commerce Developer MCP)

In [!DNL Adobe Commerce on Cloud] o nelle personalizzazioni locali è possibile utilizzare PHP in-process: moduli, plug-in e osservatori di eventi eseguiti all&#39;interno dell&#39;applicazione. [!DNL Adobe Commerce as a Cloud Service] è una piattaforma SaaS senza versione e tale modello non è più applicabile. Le personalizzazioni vengono eseguite come applicazioni [!DNL Adobe Developer App Builder] non elaborate che si integrano con Commerce tramite eventi e API. La modernizzazione delle personalizzazioni di un archivio per questa architettura è in genere il più significativo sforzo tecnico in una migrazione di [!DNL Adobe Commerce as a Cloud Service].

### Panoramica sulla migrazione del codice

A partire dalla valutazione della migrazione, Commerce Developer MCP offre un&#39;esperienza IDE conversazionale per la modernizzazione delle personalizzazioni PHP legacy nelle applicazioni [!DNL App Builder]. Fornisce inoltre assistenza per la ricostruzione di vetrine su Edge Delivery Services (EDS). Utilizzando direttamente i risultati dello strumento di valutazione della migrazione, Commerce Developer MCP mantiene l’implementazione allineata con la roadmap di migrazione approvata riducendo l’interpretazione manuale, mantenendo la tracciabilità e garantendo la coerenza durante l’intero processo.

Sebbene la migrazione sia il caso d&#39;uso principale, Commerce Developer MCP è progettato come agente di sviluppo di IA completo per [!DNL Adobe Commerce]. MCP supporta la modernizzazione, i nuovi sviluppi, i flussi di lavoro operativi e tutti gli aggiornamenti a [!DNL Adobe Commerce as a Cloud Service]. Questo livello di flessibilità consente ai team di continuare a creare ed estendere le applicazioni Commerce anche dopo la migrazione.

### Commerce Developer MCP

Utilizzando i risultati della [valutazione della migrazione](#migration-assessment-tool), Commerce Developer MCP trasforma le personalizzazioni identificate in [!DNL App Builder] applicazioni tramite un flusso di lavoro di sviluppo iterativo. Quando si sviluppa utilizzando questi strumenti, prendere in considerazione le seguenti linee guida:

- **Inizia con il blueprint**: Commerce Developer MCP utilizza la valutazione della migrazione, utilizzando le personalizzazioni, le raccomandazioni e le priorità di migrazione identificate come base per la pianificazione dell&#39;implementazione.

- **Pianifica ogni personalizzazione**: per ogni personalizzazione, Commerce Developer MCP sviluppa una specifica che descrive l&#39;architettura [!DNL Adobe Commerce as a Cloud Service] consigliata, i modelli di integrazione richiesti e qualsiasi riprogettazione necessaria per la transizione a un&#39;applicazione fuori processo.

- **Generare in modo collaborativo** - Anziché generare inizialmente il codice, Commerce Developer MCP ti assiste durante l&#39;intero ciclo di sviluppo pianificando le implementazioni, discutendo dell&#39;architettura, generando e perfezionando il codice, convalidando i modelli consigliati e fornendo indicazioni sulla distribuzione. Gli sviluppatori possono iterativamente perfezionare le implementazioni generate attraverso il linguaggio naturale, consentendo ai dettagli del progetto di evolvere in modo collaborativo durante lo sforzo di modernizzazione.

  - Le implementazioni generate sono progettate per accelerare la distribuzione pur rimanendo completamente revisionabili, testabili ed estensibili da parte dei team tecnici.

- **Integrazione e distribuzione**: Commerce Developer MCP collega le applicazioni a Commerce tramite i modelli di integrazione appropriati, assiste i flussi di lavoro di distribuzione e convalida le implementazioni in base ai modelli di architettura consigliati prima della distribuzione, migliorando la coerenza e riducendo il lavoro duplicato.

  - Commerce Developer MCP contiene [!DNL Adobe Commerce App Builder] MCP, che fornisce conoscenze sul dominio, modelli di implementazione, indicazioni architetturali, competenze contestuali sui prodotti e pratiche di codifica convalidate direttamente nel flusso di lavoro di sviluppo. Questo assicura che i consigli MCP rimangano in linea con le best practice di Adobe, sia che gli sviluppatori lavorino direttamente con Commerce Developer MCP o in combinazione con altri agenti, come Claude, Cursor o Copilot.

### Modernizzazione della vetrina

Sul front-end, Commerce Developer MCP modernizza [storefronts](https://experienceleague.adobe.com/developer/commerce/storefront/) su Edge Delivery Services (EDS) per Commerce utilizzando i blocchi boilerplate, Drop-in Components ed EDS di Adobe Commerce.

Commerce Developer MCP carica i progetti di vetrina esistenti basati sulla piattaforma standard Commerce. Modernizza la vetrina:

- Generazione di blocchi EDS reattivi
- Generazione di dati di pagina in base a Commerce (home, PLP, PDP, carrello, pagamento, account)
- Composizione ed estensione dei componenti di rilascio
- Traduzione di progetti in implementazioni EDS
- Conversione di vetrine monolitiche legacy in un&#39;architettura a blocchi EDS componibile

MCP offre inoltre assistenza nelle seguenti aree:

- Modernizzazione dei componenti
- Composizione blocco riutilizzabile
- Ottimizzazione delle esperienze
- Allineamento con le best practice correnti di Edge Delivery Services

### Valore MCP sviluppatore

Il passaggio dalle personalizzazioni PHP in-process alle applicazioni [!DNL App Builder] componibili rappresenta un cambiamento significativo dell&#39;architettura. Commerce Developer MCP risolve questo gap incorporando [!DNL Adobe Commerce] conoscenze, [!DNL App Builder] modelli di implementazione e best practice per i prodotti direttamente nel flusso di lavoro di sviluppo.

L’inclusione di questo contesto offre una maggiore coerenza sia nella velocità di consegna che nella qualità ingegneristica. I team possono modernizzare le applicazioni più rapidamente producendo implementazioni che seguono una guida coerente all’architettura.

Integrando i modelli di implementazione consigliati, Commerce Developer MCP riduce la dipendenza dalle singole competenze e aiuta le organizzazioni a scalare gli sforzi di modernizzazione in modo coerente tra i progetti.

Il processo di migrazione rappresenta anche un’opportunità per migliorare l’attuazione esistente. I team possono semplificare le personalizzazioni legacy, smantellare le funzionalità obsolete, adottare funzionalità SaaS e modernizzare l’architettura delle applicazioni anziché portare avanti il debito tecnico storico.

Poiché Commerce Developer MCP utilizza direttamente la valutazione della migrazione, ogni sforzo di modernizzazione mantiene la tracciabilità fino alla valutazione originale, garantendo l’implementazione in linea con la roadmap di migrazione approvata.

Commerce Developer MCP promuove inoltre la progettazione di applicazioni componibili incoraggiando le applicazioni modulari [!DNL App Builder] che possono evolvere in modo indipendente con l&#39;evolversi dei requisiti aziendali.

### Ambito MCP per sviluppatori

Nel back-end, Commerce Developer MCP modernizza il livello di personalizzazione e integrazione trasformando moduli PHP, plug-in e osservatori di eventi in applicazioni [!DNL App Builder] e stabilisce modelli di integrazione per collegarli ad Adobe Commerce. Accelera inoltre lo sviluppo tra pagamento, pagamento e interfaccia utente amministratore.

Nel front-end, Commerce Developer MCP [modernizza gli storefront di Commerce](#storefront-modernization) in Edge Delivery Services.

MCP non gestisce la migrazione dei dati. I dati aziendali vengono migrati tramite il [Servizio di migrazione dati di Commerce](#data-migration-commerce-data-migration-service). MCP supporta le applicazioni [!DNL App Builder] necessarie quando la logica di business o le tabelle personalizzate richiedono la modernizzazione delle applicazioni.

### Passaggi successivi

La modernizzazione del codice e della vetrina inizia una volta che la roadmap dello strumento di valutazione della migrazione ha stabilito l’ambito e le priorità della migrazione.

Per ulteriori informazioni su come installare e utilizzare MCP, consulta la documentazione di [Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/coding-tools/).

Per ulteriori informazioni su Commerce Developer Agent, integrato con lo strumento di valutazione della migrazione, vedere [Commerce Developer Agent](https://developer.adobe.com/commerce/extensibility/developer-agent/)

## Migrazione dei dati (Servizio di migrazione dati di Commerce)

La migrazione a [!DNL Adobe Commerce as a Cloud Service] richiede la migrazione di anni di dati, inclusi cataloghi, ordini, clienti e configurazione.

Il Servizio di migrazione dati di Commerce sostituisce la migrazione manuale con un unico processo automatizzato ripetibile. Rende più prevedibili ed efficienti le migrazioni complesse dei database.

### Servizio di migrazione dati di Commerce

Una migrazione utilizza un flusso di lavoro guidato, guidato da uno strumento della riga di comando Docker (`./bin/console migration`). Un integratore di sistemi o un operatore esegue questo flusso di lavoro nell&#39;archivio di origine.

La migrazione dei dati di base è automatizzata, ma la maggior parte delle migrazioni coinvolge schemi, estensioni e casi edge non standard, ed è per questo che tutte le migrazioni iniziano con una [valutazione](#migration-assessment-tool) dell&#39;archivio di origine. Dopo aver convalidato le credenziali e la connettività, registrato la migrazione e stabilito una linea di base di verifica, puoi procedere con la migrazione dei dati.

Lo strumento del servizio di migrazione esegue i seguenti passaggi di gestione dei dati:

1. **Estrai e trasforma** - Estrae tutti i dati rilevanti dall&#39;origine in parallelo e li riforma per [!DNL Adobe Commerce as a Cloud Service]. I dati non compatibili vengono filtrati e gli attributi personalizzati e altre strutture vengono rimappati.
1. **Carica** — trasferisce i dati estratti al servizio di migrazione dati di Commerce. Il servizio carica i dati in [!DNL Adobe Commerce as a Cloud Service], quindi rigenera gli indici e acquisisce il catalogo.
1. **Verifica** - Confronta i dati di origine e di destinazione a livello di database. Il servizio convalida quindi un esempio di record live tramite le API REST di GraphQL e admin per verificare i dati.
1. **Report** — consolida i risultati di ogni passaggio in un report di migrazione finale.

Queste fasi di spostamento dei dati richiedono una finestra di manutenzione, ma durante la fase di preparazione l&#39;archivio rimane operativo, riducendo al minimo i tempi di inattività.

### Valore del servizio di migrazione

Il servizio di migrazione dei dati di Commerce preserva l’integrità dei dati utilizzando le prove. Ogni migrazione viene verificata confrontando i dati di origine e di destinazione e convalidando un campione di record live tramite le API. I dati non mappati correttamente su [!DNL Adobe Commerce as a Cloud Service], ad esempio gli attributi personalizzati, vengono filtrati e rimappati automaticamente durante l&#39;estrazione.

Il servizio di migrazione è progettato per database di dimensioni enterprise. La migrazione dei dati viene partizionata ed elaborata in modo asincrono, consentendo la migrazione affidabile di cataloghi di grandi dimensioni e cronologie di ordini estese. Man mano che la pipeline cresce, è possibile eseguire più migrazioni in parallelo. Se una migrazione viene interrotta, riprende dall’ultima fase completata e i processi in stallo vengono rilevati e ritentati automaticamente.

I tempi di inattività vengono ridotti al minimo nei seguenti modi:

- La maggior parte del lavoro viene eseguita mentre il negozio rimane attivo, il che significa che solo il cutover finale richiede una finestra di manutenzione.
- La migrazione dei dati utilizza le operazioni dirette di lettura e scrittura SQL e ignora tabelle e record che non richiedono la migrazione.

Poiché le migrazioni richiedono lo spostamento dei dati di produzione attraverso l’infrastruttura Adobe, l’intero percorso è protetto:

- Tutti i caricamenti vengono analizzati alla ricerca di malware prima di raggiungere la destinazione
- Il livello di acquisizione convalida i tipi di file e blocca le operazioni del database non sicure
- Ogni richiesta viene autenticata utilizzando Adobe IMS e la verifica della firma del gateway

Il servizio di migrazione dei dati di Commerce è attivo in tutto il mondo e ha già fornito più migrazioni a livello aziendale.

### Dati personalizzati e di terze parti

Il servizio di migrazione supporta solo i dati di e-commerce di prime parti. Il servizio di migrazione non gestisce entità di terze parti personalizzate.

È possibile migrare i dati di terze parti caso per caso, il che richiede una personalizzazione corrispondente nello strumento di estrazione Docker. Dopo aver creato strumenti personalizzati, i dati possono essere estratti dall&#39;origine e scritti nel database di [!DNL App Builder] o di terze parti.

Poiché ogni estensione modella i propri dati in modo diverso, un percorso di migrazione per dati di terze parti può essere progettato solo dopo aver determinato lo schema e le posizioni dell’archiviazione di origine e di destinazione. Le migrazioni di dati di terze parti devono essere identificate in anticipo per fornire il tempo necessario per la valutazione.

### Passaggi successivi

Quando si è pronti per eseguire la migrazione, completare il [questionario di valutazione della migrazione dei dati](../assets/data-migration-scoping-questionnaire.xlsx), che richiede la topologia di origine, l&#39;ambito dell&#39;entità, i volumi, i vincoli di conformità, la meccanica di cutover e le [tabelle personalizzate](#custom-and-third-party-data) necessarie per pianificare la migrazione. Il completamento di questo questionario consente ad Adobe di valutare l’ambiente e pianificare una finestra di migrazione.

Per ulteriori informazioni sul flusso di lavoro, i dati supportati e la verifica, consulta la [guida dello strumento Bulk Data Migration](bulk-data/migration-tool.md).

Gli integratori di sistemi che preparano un ambiente di origine possono inoltre utilizzare [Adobe Commerce Cloud CLI](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) standard e [Adobe Developer Console](https://developer.adobe.com) per le credenziali IMS.
