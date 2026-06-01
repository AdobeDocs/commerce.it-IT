---
title: Introduzione
description: Scopri come iniziare a utilizzare  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
TQID: https://experienceleague.adobe.com/1dcKMjOut1GtiOevvGJECsaU7URFmYg-mQ-m9wi7n4Y
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: dba482e5-29a8-4127-afa2-c4b913512ef8
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 423b35b15e845e49b1cf36910ffbad775de9758c
workflow-type: tm+mt
source-wordcount: 1332
ht-degree: 0%

---

# Introduzione

Questa guida illustra come configurare [!DNL Adobe Commerce Optimizer] dall&#39;inizio alla fine. Questa guida descrive tutti i ruoli. Per informazioni dettagliate sui contenuti specifici per gli sviluppatori, consultare la [documentazione per gli sviluppatori](https://developer.adobe.com/commerce/services/optimizer/).

## Tipi di istanze e isolamento dell’ambiente

Adobe Commerce Optimizer utilizza istanze separate per ambienti diversi, ad esempio **sandbox** e **production**. Ogni istanza ha il proprio ID istanza e i propri dati isolati, incluse le viste del catalogo, i criteri, la configurazione della ricerca e i consigli di prodotto.

Durante l’integrazione con Adobe Commerce as a Cloud Service, piattaforme commerce di terze parti o vetrine Edge Delivery Services, gli ambienti corrispondono sempre:

- Connetti **istanze di Sandbox Optimizer** ad ambienti commerce e storefront non di produzione.
- Connetti **istanze Production Optimizer** agli ambienti Production Commerce e Storefront.

La combinazione di ambienti sandbox con ambienti di produzione causa dati di catalogo incoerenti, comportamenti di ricerca e merchandising imprevisti e metriche inaffidabili. Utilizza il tipo di istanza e l’ID dell’istanza in Commerce Cloud Manager come fonte di verità durante la configurazione delle integrazioni.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **Account Adobe Experience Cloud** con [!DNL Adobe Commerce Optimizer] adesioni
- **Accesso amministratore organizzazione** per creare istanze e gestire utenti
- **Account GitHub** per il caricamento dei dati di esempio e lo sviluppo della vetrina
- **Nozioni di base** sui concetti di e-commerce

## Guida rapida

Segui questi passaggi essenziali per eseguire l&#39;ambiente [!DNL Adobe Commerce Optimizer]:

### Passaggio 1: Creare un’istanza

1. Accedi a [Adobe Experience Cloud](https://experience.adobe.com/).
1. Passa a **Commerce** > **Commerce Cloud Manager**.
1. Fai clic su **Aggiungi istanza** > **Commerce Optimizer**.

   ![Schermata Aggiungi istanza di Adobe Commerce Cloud Manager per la creazione di un ambiente Commerce Optimizer](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. Configurare le impostazioni delle istanze:
   - **Nome istanza**: nome descrittivo (ad esempio, &quot;My Company Sandbox&quot;)
   - **Descrizione**: breve descrizione dello scopo
   - **Tipo di ambiente**: inizia con un ambiente **Sandbox** per il test
   - **Regione**: seleziona l&#39;area geografica preferita

1. Fai clic su **Aggiungi istanza**.

   Cloud Manager viene aggiornato per includere la nuova istanza. Per informazioni dettagliate sull&#39;accesso e la gestione, vedere [Gestire un&#39;istanza](#manage-instances).

>[!NOTE]
>
>Puoi creare ambienti sandbox solo nell’area Nord America. Una volta creata un’istanza, non è possibile modificarla.

### Passaggio 2: Configurare l’ambiente

Dopo aver creato l’istanza:

1. [Gestisci l&#39;istanza](#manage-instances) da Commerce Cloud Manager.
1. Configurare l&#39;accesso utente utilizzando la [Guida alla gestione utente](./user-management.md).

### Passaggio 3: Aggiungi dati di esempio (facoltativo)

Per il test e l&#39;apprendimento, seguire le istruzioni [Load Sample Data](#add-sample-data).

## Flussi di lavoro basati sul ruolo

La configurazione e la gestione di [!DNL Adobe Commerce Optimizer] si basano su tre ruoli chiave. Ciascun ruolo ha compiti e responsabilità specifiche:

![Flusso di lavoro basato su ruoli per l&#39;installazione di [!DNL Adobe Commerce Optimizer] con attività di amministratore, sviluppatore e utente](./assets/high-level-workflow.png){zoomable="yes"}

### Attività di amministratore

Gli amministratori gestiscono istanze, utenti e impostazioni organizzative.

| Attività | Descrizione | Collegamento |
|---|---|---|
| **Gestisci utenti** | Aggiungere utenti, sviluppatori e amministratori | [Gestione utente](./user-management.md) |
| **Crea istanze** | Configurare ambienti sandbox e di produzione | [Crea istanza](#step-1-create-an-instance) |
| **Gestisci istanze** | Controlla lo stato, aggiorna il nome e la descrizione dell’istanza e ottieni gli URL chiave per l’accesso all’applicazione e all’API | [Gestisci istanze](#manage-instances) |
| **Configura accesso** | Impostare le visualizzazioni e i criteri del catalogo | [Visualizzazioni catalogo](./setup/catalog-view.md) |

### Attività degli sviluppatori

Gli sviluppatori gestiscono l’implementazione tecnica e l’integrazione dei dati, incluse le attività dell’architettura della piattaforma.

| Attività | Descrizione | Collegamento |
|---|---|---|
| **Accedi a Developer Console** | Creare progetti e generare credenziali | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **Acquisisci dati catalogo** | Importa dati prodotto da sistemi esistenti | Per acquisire i dati direttamente in Adobe Commerce Optimizer, consulta [API di acquisizione dati](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}.<br><br>Per acquisire dati da Commerce in ambienti cloud o locali o in altri sistemi di terze parti, consulta l&#39;argomento [Integrazioni](./integrations/integrations-overview.md){target="_blank"}. |
| **Configura la vetrina** | Configurare Edge Delivery Services storefront | [Installazione di Storefront](./storefront.md) |

### Attività merchandiser

I commercianti ottimizzano e personalizzano l’esperienza di acquisto tramite l’individuazione dei prodotti e i consigli. Inoltre, utilizzano i dati e le analisi dei clienti per prendere decisioni strategiche sul posizionamento dei prodotti, sui prezzi e sulle promozioni in vetrina.

| Attività | Descrizione | Collegamento |
|---|---|---|
| **Individuazione prodotto** | Configurare la ricerca e il filtro | [Panoramica sul merchandising](./merchandising/overview.md) |
| **Consigli** | Configurare i consigli di prodotto basati sull’intelligenza artificiale | [Consigli di prodotto](./merchandising/recommendations/overview.md) |
| **Tracciamento delle prestazioni** | Monitorare le metriche di successo | [Metriche di successo](./manage-results/success-metrics.md) |

## Gestire le istanze

Gestisci le istanze da Commerce Cloud Manager.

>[!NOTE]
>
>Non tutti gli utenti [!DNL Adobe Commerce Optimizer] hanno accesso a Cloud Manager. L’accesso dipende dal ruolo e dalle autorizzazioni assegnati all’account utente.

1. Accedi a [Adobe Experience Cloud](https://experience.adobe.com/).

1. Apri Commerce Cloud Manager:

   - In **Accesso rapido**, fare clic su **Commerce**.
   - Visualizza le istanze disponibili.

### Cerca e filtra istanze

Dopo aver effettuato l’accesso, il dashboard mostra tutte le istanze di prodotto Commerce disponibili nell’organizzazione.
La colonna Prodotto indica per quale applicazione Commerce è stato eseguito il provisioning dell’istanza.

![Dashboard che mostra le opzioni di ricerca e filtro per le istanze di prodotto Adobe Commerce Cloud](./assets/search-filter-instances.png){zoomable="yes"}

Utilizza gli strumenti Filtro e Ricerca per trovare rapidamente istanze specifiche in base alla data di creazione, all’area geografica, al creatore, al tipo di prodotto, all’ambiente o allo stato.

### Accedi all&#39;interfaccia di amministrazione [!DNL Adobe Commerce Optimizer Studio]

Una volta aperta l’app, passa facilmente da un ambiente all’altro, come sandbox e produzione, per visualizzare dati e impostazioni per ciascuno di essi, senza dover tornare a Commerce Cloud Manager.

1. Da Commerce Cloud Manager, fare clic sul nome dell&#39;istanza per aprire [!DNL Adobe Commerce Optimizer Studio].

1. Passa da [!DNL Adobe Commerce Optimizer] istanze all&#39;altra senza uscire dall&#39;applicazione.

   - Fai clic sull’elenco a discesa delle istanze per visualizzare tutte le istanze di Optimizer disponibili nell’organizzazione.

     ![Menu a discesa del commutatore di istanza per selezionare [!DNL Adobe Commerce Optimizer] ambienti](./assets/context-switcher.png){zoomable="yes"}

- Seleziona l’istanza da visualizzare.

>[!NOTE]
>
>Per tornare a Commerce Cloud Manager per visualizzare i dettagli dell&#39;istanza o gestire le istanze, fare clic sull&#39;icona ![Icona per aprire Experience Cloud Applications](./assets/apps-icon.png) (Apps) nell&#39;angolo superiore sinistro della navigazione superiore di Commerce Optimizer.

### Ottieni dettagli istanza

Per visualizzare i dettagli dell’istanza, fai clic sull’icona delle informazioni accanto al nome dell’istanza.

Il pannello dei dettagli dell&#39;istanza ![[!DNL Adobe Commerce Optimizer] mostra gli endpoint e l&#39;ID istanza](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

Tieni presente le seguenti informazioni chiave:

- **Endpoint GraphQL** Endpoint GraphQL utilizzato dalla vetrina per eseguire query sui dati di catalogo e merchandising da questa istanza tramite l&#39;[API servizio merchandising](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/){target=_blank}
- **Endpoint catalogo** endpoint REST API utilizzato per acquisire prodotti e prezzi in Adobe Commerce Optimizer dal sistema commerce o PIM. Visualizza [API di acquisizione dati](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- **URL Commerce Optimizer** Apre l&#39;interfaccia utente amministratore di [Adobe Commerce Optimizer Studio](overview.md) per configurare e gestire le visualizzazioni catalogo, i criteri e il merchandising.
- **ID istanza**: identificatore univoco (ID tenant) per questa istanza di Adobe Commerce Optimizer, utilizzato da storefront, API e strumenti per connettersi all&#39;ambiente corretto.

Se si è uno sviluppatore, è necessario disporre di questi dettagli per configurare l&#39;ambiente di sviluppo e connettersi alle API [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Per accedere ai dettagli dell’istanza, devi disporre delle autorizzazioni necessarie nell’organizzazione Adobe IMS. Se non trovi i dettagli dell’istanza o non riesci ad accedere all’applicazione, contatta l’amministratore dell’organizzazione.

### Modifica nome e descrizione istanza

Se necessario, aggiorna il nome e la descrizione dell’istanza.

1. Fai clic sull&#39;icona **Modifica** accanto al nome di un&#39;istanza.
1. Aggiornare **Nome istanza** e **Descrizione** in base alle esigenze.
1. Fai clic su **Salva**.

## Aggiungi dati di esempio

Adobe fornisce un archivio GitHub con dati e strumenti di esempio per aiutarti ad apprendere e testare le funzionalità di [!DNL Adobe Commerce Optimizer].
I dati di esempio si basano sullo [scenario aziendale di Carvelo](./use-case/admin-use-case.md) e includono:

- Catalogo dei prodotti con parti per autoveicoli
- Più listini prezzi e scenari di determinazione prezzi
- Visualizzazioni del catalogo e criteri per diversi dealer
- Esempi completi di flusso di lavoro end-to-end

**Caricare i dati di esempio:**

1. Accedi all&#39;archivio GitHub [Esempio di acquisizione dati catalogo](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion).

1. Seguire le istruzioni di installazione nel file README dell&#39;archivio per completare le operazioni seguenti:

   - Configurare l’ambiente
   - Completa il processo di acquisizione dei dati
   - Creare viste e criteri del catalogo utilizzando i dati di esempio
   - Verifica l&#39;acquisizione dei dati controllando i dati di Catalog Service nella pagina [Sincronizzazione dati](./setup/data-sync.md)

## Passaggi successivi

Dopo aver completato la configurazione:

1. Configura la vetrina:
   - Configura [Edge Delivery Services storefront](./storefront.md)
   - Connetti ai dati del catalogo

1. Esplora il caso di utilizzo di Carvelo:
   - Segui il [flusso di lavoro end-to-end](./use-case/admin-use-case.md)
   - Esercitazione con scenari reali

1. Configurare merchandising:
   - Configura [individuazione prodotto](./merchandising/overview.md)
   - Crea [consigli](./merchandising/recommendations/overview.md)

1. Monitorare le prestazioni:
   - Traccia [metriche di successo](./manage-results/success-metrics.md)
   - Analizza [prestazioni di ricerca](./manage-results/search-performance.md)

## Risoluzione dei problemi

### Problemi comuni

| Problema | Soluzione |
|---|---|
| **Impossibile creare un&#39;istanza** | Verifica di disporre di [!DNL Adobe Commerce Optimizer] diritti e autorizzazioni di amministratore. |
| **Istanza non visualizzata** | Controlla la tua organizzazione Adobe IMS e aggiorna la pagina. |
| **Impossibile accedere all&#39;istanza** | Assicurati di essere aggiunto come utente in Admin Console. |
| **Impossibile caricare i dati di esempio** | Verifica le credenziali dell’istanza e gli endpoint API. |

### Ottieni aiuto

- **Risorse per sviluppatori**: [Documentazione per sviluppatori](https://developer.adobe.com/commerce/services/optimizer/)
- **Risorse storefront**: [Documentazione storefront Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/)
- **Esercitazioni**: [Esercitazioni Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview)
- **Supporto**: [Risorse di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)
