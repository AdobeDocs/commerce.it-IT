---
title: Strumento di migrazione dati in blocco
description: Scopri come utilizzare lo strumento di migrazione dei dati in blocco per migrare i dati dall'istanza esistente di Adobe Commerce on Cloud a  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-07-22T19:18:39.433Z'
TQID: 'https://experienceleague.adobe.com/tkCFabZpBKu-W34wsufHlVIWzCUE8FKm4kK7qZahxBU'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4c0eca0039bab7d015144dd9ac3885a0b2be0563
workflow-type: tm+mt
source-wordcount: 924
ht-degree: 0%

---

# Strumento di migrazione dati in blocco

>[!IMPORTANT]
>
>Lo strumento di migrazione dei dati in blocco è attualmente in fase di accesso anticipato. L’accesso viene fornito esclusivamente tramite il processo di coinvolgimento Commerce Deployed Engineering (CDE).

Lo strumento per la migrazione di massa dei dati consente agli integratori di sistema di migrare i dati commerce di prime parti da [!DNL Adobe Commerce on Cloud] o installazioni locali a [!DNL Adobe Commerce as a Cloud Service].

Lo strumento per la migrazione di massa dei dati è un CLI basato su Docker eseguito dagli integratori di sistemi sul proprio computer di migrazione. Si connette all’istanza sorgente, estrae i dati commerce di prime parti, li carica sul servizio di migrazione di Adobe (Commerce Data Migration Service) e monitora l’avanzamento fino al completamento.

Tutti i comandi vengono eseguiti localmente, in modo da controllare quando viene avviata la migrazione, quando viene applicata la modalità di manutenzione e quando viene eseguita ogni fase.

## Flusso di lavoro di migrazione

Lo strumento gestisce le seguenti fasi end-to-end:

- **Estrazione dati**: estrae i dati di Commerce di base di prime parti dall&#39;istanza di origine ([!DNL Adobe Commerce on Cloud] o locale).
- **Caricamento dati** - Carica i dati estratti nell&#39;istanza [!DNL Adobe Commerce as a Cloud Service] di destinazione.
- **Verifica dell&#39;integrità dei dati**: esegue controlli automatizzati successivi alla migrazione, inclusi il confronto delle API REST e GraphQL e la convalida del conteggio dei record.

>[!NOTE]
>
>Attualmente, lo strumento di migrazione dei dati in blocco supporta solo la migrazione dei dati di Commerce di base di prime parti. La migrazione dei dati personalizzati non è attualmente supportata. Le impostazioni di configurazione (impostazioni archivio, configurazione del sistema) non vengono migrate automaticamente e devono essere impostate sull’istanza di destinazione in modo indipendente prima della migrazione.

## Architettura

Lo strumento per la migrazione di massa dei dati segue un&#39;architettura distribuita che consente una migrazione dei dati sicura ed efficiente. Questo strumento consente agli integratori di sistema di migrare i dati da [!DNL Adobe Commerce on Cloud or on-premises instance] a [!DNL Adobe Commerce as a Cloud Service]. Per ulteriori informazioni sul processo di migrazione, vedere [Panoramica sulla migrazione](../overview.md).

L’immagine seguente descrive l’architettura e il flusso di dati end-to-end utilizzando lo strumento di migrazione dei dati in blocco.

![Diagramma dell&#39;architettura dello strumento di migrazione dati in blocco che mostra il flusso di dati da PaaS a SaaS](../../assets/bulk-data-diagram.png){zoomable="yes"}

### Componenti

| Componente | Ruolo |
| --------- | ---- |
| **Strumento di migrazione dati in blocco** | L’interfaccia CLI basata su Docker eseguita dall’integratore di sistemi sul computer di migrazione, che orchestra l’intera pipeline leggendo lo schema e i dati dall’origine, caricando i dati estratti nel servizio di migrazione di Adobe e guidando le transizioni di stato. |
| **Istanza di Source (Commerce su Cloud o locale)** | L’origine della migrazione. Lo strumento si connette tramite API REST e GraphQL e tramite un tunnel SSH ([!DNL Adobe Commerce on Cloud]) o tramite una connessione di database diretta (locale) per l&#39;estrazione dei dati. |
| **API Servizio di migrazione dati di Commerce (CDMS)** | API REST gestita da Adobe che registra le migrazioni, coordina le transizioni di stato e fornisce endpoint sicuri per il caricamento dei dati estratti. Lo strumento di migrazione si connette a questa API utilizzando l&#39;URL dell&#39;endpoint CDMS e le credenziali IMS nella configurazione di `.env`. |
| **Processo di lavoro del Servizio di migrazione dati di Commerce** | Servizio in background gestito da Adobe che carica i dati estratti nell&#39;istanza di destinazione ed esegue la verifica dell&#39;integrità post-caricamento. |
| **[!DNL Adobe Commerce as a Cloud Service]** | La versione SaaS di Adobe Commerce e la destinazione della migrazione. Riceve i dati caricati ed espone i servizi di catalogo, Live Search e delle regole di determinazione prezzi utilizzati durante la verifica dell&#39;integrità. |

### Flusso di dati

I dati si spostano tra i componenti nella sequenza seguente:

1. Lo strumento di migrazione dati in blocco legge lo schema e i dati del database dall&#39;istanza di origine tramite un tunnel SSH per [!DNL Adobe Commerce on Cloud] o una connessione di database diretta per on-premise.
1. Lo strumento registra la migrazione e carica i dati estratti tramite l’API CDMS.
1. Il processo di lavoro CDMS carica i dati nel tenant di destinazione [!DNL Adobe Commerce as a Cloud Service].
1. [!DNL Adobe Commerce as a Cloud Service] acquisisce i dati del catalogo caricati e crea l&#39;indice del catalogo.
1. Il processo di lavoro del Servizio di migrazione dati di Commerce (CDMS) verifica i dati caricati tramite il confronto del checksum del database, REST e GraphQL tra i seguenti servizi:

   - **Catalogo** (GraphQL): dati di prodotti e categorie.
   - **Live Search** (REST): correttezza indice di ricerca.
   - **Regole di determinazione prezzi** (REST): dati su prezzi e regole.

1. Lo strumento esegue il polling dello stato di migrazione in e recupera il rapporto di migrazione finale al completamento.


## Ciclo di vita del coinvolgimento

L’accesso allo strumento di migrazione dei dati in blocco viene fornito esclusivamente tramite un progetto Commerce Deployed Engineering (CDE). Lo strumento non è accessibile al pubblico.

Il ciclo di vita tipico del coinvolgimento è:

1. **Individuazione CDE** - Completare la chiamata di valutazione iniziale, valutare l&#39;impronta e la complessità dei dati e completare il questionario di valutazione.
1. **Firma offerta** - Il contratto commerciale è in vigore e l&#39;ambito di migrazione è confermato. In questa fase, puoi accedere allo strumento di migrazione.
1. **Supporto e co-innovazione CDE**: collabora con Adobe per installare lo strumento nel tuo ambiente ed eseguire migrazioni di test.
1. **Lancio** - Esegui la migrazione del cutover di produzione e completa la verifica dell&#39;integrità dei dati.

## Distribuzione degli strumenti

Lo strumento viene distribuito come parte del progetto CDE. Il tuo rappresentante Adobe fornisce il pacchetto di strumenti, che include:

- CLI basata su Docker e configurazione della build
- Modello di configurazione `.example.env` con documentazione per tutte le variabili di ambiente richieste
- Documentazione tecnica completa sull&#39;architettura dello strumento, sui riferimenti di configurazione, sui framework di trasformazione e test personalizzati e sulle guide per la risoluzione dei problemi

Per istruzioni di configurazione e operative dettagliate, consulta la documentazione inclusa nel pacchetto di distribuzione dello strumento.

## Guide alla migrazione

Le pagine seguenti illustrano l&#39;intero ciclo di migrazione, dalla preparazione all&#39;esecuzione. Per una comprensione completa del processo di migrazione, esaminarli nell&#39;ordine seguente:

1. [Elenco di controllo preparazione cliente](readiness-checklist.md): prima di richiedere l&#39;accesso allo strumento, confermare i prerequisiti di coinvolgimento, macchina di migrazione, origine e destinazione.
1. [Verificare l&#39;accesso al servizio di migrazione](cdms-access.md): dopo aver ottenuto l&#39;accesso allo strumento, convalidare la raggiungibilità della rete, l&#39;autenticazione IMS e l&#39;autorizzazione del tenant rispetto all&#39;API del servizio di migrazione dati di Commerce (CDMS).
1. [Esegui una migrazione dati in blocco](migration-guide.md): configura lo strumento, prepara la rete e le istanze e avvia la migrazione.

Per informazioni di riferimento sulla configurazione completa, sui framework di trasformazione e test personalizzati e sulla risoluzione dei problemi, consulta la documentazione inclusa nel pacchetto di distribuzione dello strumento.
