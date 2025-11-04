---
title: Connettore Commerce Salesforce
description: Scopri di più su [!DNL Commerce Optimizer SFCC Connector] che fornisce un punto di partenza per integrare Salesforce Commerce B2C con [!DNL Adobe Commerce Optimizer] per sincronizzare i dati del catalogo e implementare e personalizzare il connettore per supportare le operazioni aziendali.
role: Admin, Developer
source-git-commit: fc6f8566a1932e830a37bcfa32cd1c4168c67c68
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# Connettore Commerce Salesforce per Adobe Commerce Optimizer

Basato sulla tecnologia Adobe App Builder, [!DNL Commerce Optimizer Salesforce Commerce Connector] consente il trasferimento e la gestione senza soluzione di continuità dei dati del catalogo da Salesforce Commerce Cloud B2C a [!DNL Adobe Commerce Optimizer]. Collega entrambe le piattaforme, mantenendo sincronizzate le informazioni sui prodotti, i prezzi e gli aggiornamenti, senza necessità di riposizionare le piattaforme.

Il connettore offre funzionalità affidabili di sincronizzazione dei dati e la flessibilità necessaria per personalizzare i flussi di lavoro in base alle esigenze aziendali.

Per una serie di esercitazioni video end-to-end, consulta [Scopri Salesforce Commerce Cloud Starter Kit](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/sfcc-starter-kit/overview).

## Funzionalità principali

* **Sincronizzazione dati catalogo:** invia i dati dei prodotti, incluse varianti, listini prezzi e strutture, da Salesforce Commerce B2C a Adobe Commerce Optimizer per mantenere aggiornati i punti vendita e le applicazioni basate sull&#39;esperienza.
* **Sincronizzazione prezzi:** Importa e gestisci i dati sui prezzi direttamente da Salesforce Commerce B2C.
* **Supporta più tipi di dati:** sincronizza prodotti, prezzi e strutture di catalogo per riflettere configurazioni di merchandising complesse.

* **Flussi di lavoro di sincronizzazione flessibili**
   * **Sincronizzazioni pianificate:** automatizza gli aggiornamenti utilizzando la pianificazione dei processi cron, senza richiedere alcuno sforzo manuale.
   * **Aggiornamenti on-demand:** attiva immediatamente gli aggiornamenti a livello di SKU per modifiche, correzioni o avvii di prodotti urgenti.

* **Generato per l&#39;estensibilità**
   * Utilizza gli endpoint personalizzati dell&#39;[API B2C di Salesforce Commerce](https://developer.salesforce.com/docs/commerce/commerce-api/guide/get-started.html) (SCAPI) per compatibilità e facile adattamento a casi d&#39;uso univoci o avanzati.
   * Scalabile con il tuo business-start con la sincronizzazione di cataloghi e prezzi, quindi estendere i flussi di lavoro per supportare integrazioni aggiuntive o logica di business.
   * Configurare ed evolvere i flussi di lavoro senza ricostruire le integrazioni di base.

>[!NOTE]
>
>Il connettore è progettato specificamente per Salesforce Commerce Cloud B2C. Non supporta i prodotti Salesforce B2B o D2C, che sono basati su diversi stack di tecnologia.

## Chi trae vantaggio dal connettore Salesforce?

[!DNL Salesforce Commerce Connector] è ideale per:

* **Clienti Salesforce Commerce Cloud B2C esistenti** che hanno migliorato le funzionalità della vetrina
* **Organizzazioni multimarca** che richiedono funzioni avanzate di merchandising e personalizzazione su più vetrine
* **Aziende alla ricerca di miglioramenti delle prestazioni** tramite Edge Delivery Services di Adobe per esperienze di vetrina più veloci
* **Aziende con strutture di prezzo complesse** che sincronizzano listini prezzi sofisticati e prezzi specifici per le impostazioni internazionali
* **Clienti AEM** che gestiscono cataloghi di prodotti da Salesforce Commerce B2C mentre utilizzano Adobe Commerce storefront con Edge Delivery Services
* **Rivenditori con requisiti per più impostazioni locali** che sincronizzano le informazioni sui prodotti localizzati nei diversi mercati e lingue

## Casi d’uso

Il connettore supporta diversi casi d’uso principali:

### Acquisizione dei dati del catalogo e visualizzazione della vetrina

Questo caso d’uso principale illustra l’intero flusso di dati da Salesforce Commerce B2C alla vetrina Adobe Commerce:

1. **Acquisizione iniziale del catalogo:** Carica in blocco l&#39;intero catalogo di Salesforce commerce, inclusi i prodotti semplici con varianti, listini prezzi e informazioni sui prezzi.
1. **Aggiornamenti delta automatizzati:** sincronizza automaticamente gli aggiornamenti dei prodotti dall&#39;interfaccia utente di gestione catalogo di Salesforce Commerce a [!DNL Commerce Optimizer].
1. **Integrazione Storefront:** Visualizza i dati del catalogo sincronizzati nella vetrina del servizio Adobe Commerce Edge Delivery tramite [!DNL Commerce Optimizer] API storefront.
1. **Aggiornamenti in tempo reale:** Visualizza informazioni aggiornate sul prodotto (nomi, prezzi, descrizioni) immediatamente nella vetrina dopo aver apportato modifiche in Salesforce.

### Gestione di prodotti per più paesi

Utilizzo delle funzionalità di localizzazione B2C di Salesforce Commerce:

* Sincronizza le versioni localizzate dei campi di testo del prodotto (nomi, descrizioni) da Salesforce Commerce B2C per diverse lingue.
* Mappare i concetti delle impostazioni locali di Salesforce 1:1 con [!DNL Commerce Optimizer] impostazioni locali.
* Supporta più cicli di inserimento dei prodotti per diverse localizzazioni.
* Mantenere la coerenza tra i cataloghi di prodotti globali.

## Architettura e componenti

[!DNL SFCC Connector] fornisce un livello di integrazione affidabile tra un&#39;istanza B2C di Salesforce Commerce e [!DNL Commerce Optimizer]. Il connettore funziona tramite una serie di azioni di sincronizzazione che trasferiscono i dati del catalogo, i listini prezzi e le informazioni sui prodotti.

1. **Estrazione dati**: esegui l&#39;autenticazione con l&#39;istanza B2C di Salesforce Commerce ed estrai i dati del catalogo utilizzando API SCAPI personalizzate.
1. **Trasformazione dati**: trasforma i dati di prodotto in modo che corrispondano ai requisiti del modello dati e dello schema [!DNL Commerce Optimizer].
1. **Acquisizione dei dati** - Trasmette in modo sicuro i dati trasformati a [!DNL Commerce Optimizer] utilizzando il SDK ACO TypeScript.
1. **Integrazione storefront**: i dati sincronizzati diventano disponibili tramite [!DNL Commerce Optimizer] API per le esperienze storefront.

Il diagramma seguente illustra il flusso di dati di alto livello per l’integrazione:

![Architettura di Salesforce Commerce Connector](../assets/sfcc_starter_kit.png){zoomable="yes"}

### Componenti chiave

[!DNL Commerce Optimizer SFCC Connector] è costituito da diversi componenti chiave:

* **ACO SFCC Starter Kit Applicazione App Builder**-Fornisce funzioni senza server che gestiscono la sincronizzazione dei dati tra SFCC e Adobe Commerce Optimizer.
* **Cartuccia SFCC personalizzata**: cartuccia necessaria che estende l&#39;istanza Salesforce Commerce Cloud con le API necessarie per l&#39;estrazione dei dati.
* **Interfaccia utente di gestione** - Interfaccia Web per monitorare lo stato di sincronizzazione e gestire le operazioni del connettore.

### Processo di sincronizzazione

Il connettore supporta più modalità di sincronizzazione.

| Modalità di sincronizzazione | Descrizione |
|-----------|-------------|
| **Sincronizzazione siti completa** | Esegue una sincronizzazione completa di tutti i prodotti, listini prezzi e prezzi per il sito Commerce Cloud Salesforce configurato e le impostazioni internazionali. Ciò include <ul><li>metadati e attributi del prodotto</li><li>struttura e categorie del catalogo</li><li>listini prezzi</li><li>informazioni sui prezzi</li><li>dati di prodotto per più impostazioni locali</li></ul> |
| **Sincronizzazione delta** | Recupera e sincronizza solo le modifiche apportate nei dati dei prodotti e dei prezzi Salesforce dall&#39;ultima sincronizzazione, garantendo aggiornamenti efficienti e tempestivi.<br>La sincronizzazione delta viene eseguita automaticamente su base pianificata (impostazione predefinita: ogni ora) per mantenere l&#39;aggiornamento dei dati. |
| **Opzioni di sincronizzazione mirate** | Fornisce funzionalità di sincronizzazione granulare: <ul><li>**Sincronizzazione listino prezzi** sincronizza solo le informazioni sul listino prezzi dedicato</li><li>**La sincronizzazione dei metadati** aggiorna i metadati del prodotto e le definizioni degli attributi</li><li>**Sincronizzazione prodotto specifica** sincronizza i singoli prodotti per SKU</li></ul> |

## Considerazioni importanti

Quando pianifichi l’implementazione, considera i seguenti fattori chiave:

### Mappatura dei dati e attributi

* **Attributi ricercabili:** Salesforce Commerce B2C imposta gli attributi ricercabili tramite l&#39;interfaccia utente, che l&#39;API non espone. Utilizzare [[!DNL Catalog Data Ingestion metadata APIs]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) per configurare manualmente questi attributi ricercabili in Adobe Commerce Optimizer.
* **Mappatura attributi:** Pianifica la mappatura degli attributi di prodotto B2C di Salesforce Commerce ai metadati [!DNL Commerce Optimizer] in base ai requisiti aziendali.
* **Campi ricercabili predefiniti:** Il connettore rende automaticamente ricercabili gli attributi principali (`name`, `description`, `ID`) per impostazione predefinita.

### Ambito di sincronizzazione

* **Selezione siti:** Salesforce Commerce B2C ha un concetto di siti collegati ai cataloghi. Durante la sincronizzazione completa, selezionare il sito Salesforce da sincronizzare.
* **Gestione delle impostazioni locali:** ogni impostazione locale di Salesforce Commerce determina un ciclo di acquisizione prodotto separato in [!DNL Commerce Optimizer].
* **Volume dati:** durante la pianificazione dell&#39;implementazione, prendere in considerazione le dimensioni del catalogo e la frequenza di sincronizzazione.

## Monitoraggio e gestione

Una volta installato e configurato, [!DNL Commerce Optimizer SFCC Connector] fornisce funzionalità complete di monitoraggio e gestione da [!DNL SFCC to ACO Sync Panel]:

![Interfaccia utente per la gestione di Salesforce Commerce Connector](../assets/sfcc_management_ui.png){width="700" zoomable="yes"}

L&#39;URL per questa interfaccia viene fornito dopo la distribuzione di [!DNL Commerce Optimizer SFCC Connector Starter Kit] al progetto App Builder.

Le caratteristiche principali includono:

* **Tracciamento stato sincronizzazione:** Monitorare lo stato e i timestamp di tutte le operazioni di sincronizzazione.
* **Convalida connettività:** Verificare le connessioni a Salesforce Commerce Cloud e Adobe Commerce Optimizer.
* **Convalida dati prodotto:** Verificare che i dati di prodotto sincronizzati vengano visualizzati correttamente nella vetrina.
* **Registrazione errori e risoluzione problemi:** È possibile accedere ai registri errori per la risoluzione dei problemi tramite App Builder CLI.
* **Gestione stato:** tenere traccia dell&#39;avanzamento della sincronizzazione e prevenire conflitti con la gestione integrata dello stato.

## Codice Source e risorse di sviluppo

[!DNL Commerce Optimizer SFCC Connector] è open source ed è disponibile per la personalizzazione. Gli archivi principali includono:

* **[ACO SFCC Starter Kit](https://github.com/adobe-commerce/aco-sfcc-starter-kit)** - Applicazione e documentazione del connettore principale.
* **[Cartucce SFCC ACO](https://github.com/adobe-commerce/aco-sfcc-cartridges)** - Cartuccia SFCC necessaria per l&#39;integrazione API.
* **[ACO TypeScript SDK](https://github.com/adobe-commerce/aco-ts-sdk)** - Integrazione con SDK for Adobe Commerce Optimizer.

Questi archivi forniscono codice sorgente completo, documentazione dettagliata ed esempi per l’implementazione e la personalizzazione del connettore.

## Passaggi successivi

Intendete integrare i dati Salesforce Commerce Cloud con Adobe Commerce Optimizer? Per iniziare, controlla la guida dettagliata all&#39;implementazione nell&#39;archivio [ACO SFCC Starter Kit](https://github.com/adobe-commerce/aco-sfcc-starter-kit) e assicurati di disporre dei prerequisiti necessari.
