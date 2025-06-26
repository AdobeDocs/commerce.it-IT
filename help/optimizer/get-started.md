---
title: Introduzione
description: Scopri come iniziare a utilizzare  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 036e04a02edadf4b8a48fc38e784d9dde734ba45
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Introduzione

Questa guida illustra come configurare [!DNL Adobe Commerce Optimizer] dall&#39;inizio alla fine. Questa guida descrive tutti i ruoli. Per informazioni dettagliate sui contenuti specifici per gli sviluppatori, consultare la [documentazione per gli sviluppatori](https://developer.adobe.com/commerce/services/optimizer/).

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **Account Adobe Experience Cloud** con [!DNL Adobe Commerce Optimizer] adesioni
- **Accesso amministratore organizzazione** per creare istanze e gestire utenti
- **Account GitHub** (per il caricamento dei dati di esempio e lo sviluppo della vetrina)
- **Nozioni di base** sui concetti di e-commerce

## Guida rapida

Segui questi passaggi essenziali per eseguire l&#39;ambiente [!DNL Adobe Commerce Optimizer]:

### Passaggio 1: Creare un’istanza

1. Accedi a [Adobe Experience Cloud](https://experience.adobe.com/).
1. Passa a **Commerce** > **Commerce Cloud Manager**.
1. Fai clic su **Aggiungi istanza** > **Commerce Optimizer**.

   ![Crea istanza](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. Configurare le impostazioni delle istanze:
   - **Nome**: nome descrittivo (ad esempio, &quot;My Company Sandbox&quot;)
   - **Descrizione**: breve descrizione dello scopo
   - **Regione**: seleziona l&#39;area geografica preferita
   - **Tipo di ambiente**: inizia con un ambiente **Sandbox** per il test

1. Fai clic su **Aggiungi istanza**.

   Cloud Manager viene aggiornato per includere la nuova istanza. Per informazioni dettagliate sull&#39;accesso e la gestione, vedere [Gestire un&#39;istanza](#manage-an-instance).

>[!NOTE]
>
>Le istanze sandbox sono limitate all’area Nord America. Non è possibile modificare la regione dopo la creazione.

### Passaggio 2: Configurare l’ambiente

Dopo aver creato l’istanza:

1. [Gestisci l&#39;istanza](#manage-an-instance) da Commerce Cloud Manager.
1. Configurare le visualizzazioni e i criteri del catalogo utilizzando la [Guida alla visualizzazione del catalogo](./setup/catalog-view.md).
1. Configurare l&#39;accesso utente utilizzando la [Guida alla gestione utente](./user-management.md).

### Passaggio 3: Aggiungi dati di esempio (facoltativo)

Per il test e l&#39;apprendimento, seguire le istruzioni [Load Sample Data](#add-sample-data).

## Flussi di lavoro basati sul ruolo

La configurazione e la gestione di [!DNL Adobe Commerce Optimizer] si basano su tre ruoli chiave. Ciascun ruolo ha compiti e responsabilità specifiche:

![Flusso di lavoro di alto livello](./assets/high-level-workflow.png){zoomable="yes"}

### Attività di amministratore

Gli amministratori gestiscono istanze, utenti e impostazioni organizzative.

| Attività | Descrizione | Collegamento |
|---|---|---|
| **Gestisci utenti** | Aggiungere utenti, sviluppatori e amministratori | [Gestione utente](./user-management.md) |
| **Crea istanze** | Configurare ambienti sandbox e di produzione | [Crea istanza](#create-an-instance) |
| **Configura accesso** | Impostare le visualizzazioni e i criteri del catalogo | [Visualizzazioni catalogo](./setup/catalog-view.md) |

### Attività degli sviluppatori

Gli sviluppatori gestiscono l’implementazione tecnica e l’integrazione dei dati, incluse le attività dell’architettura della piattaforma.

| Attività | Descrizione | Collegamento |
|---|---|---|
| **Accedi a Developer Console** | Creare progetti e generare credenziali | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **Acquisisci dati catalogo** | Importa dati prodotto da sistemi esistenti | [API di acquisizione dati](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) |
| **Configura vetrina** | Configurare Edge Delivery Services storefront | [Installazione di Storefront](./storefront.md) |

### Attività merchandiser

I commercianti ottimizzano e personalizzano l’esperienza di acquisto tramite l’individuazione dei prodotti e i consigli. Inoltre, utilizzano i dati e le analisi dei clienti per prendere decisioni strategiche sul posizionamento dei prodotti, sui prezzi e sulle promozioni in vetrina.

| Attività | Descrizione | Collegamento |
|---|---|---|
| **Individuazione prodotto** | Configurare la ricerca e il filtro | [Panoramica sul merchandising](./merchandising/overview.md) |
| **Consigli** | Configurare i consigli di prodotto basati sull’intelligenza artificiale | [Consigli di prodotto](./merchandising/recommendations/overview.md) |
| **Tracciamento delle prestazioni** | Monitorare le metriche di successo | [Metriche di successo](./manage-results/success-metrics.md) |

## Gestire un’istanza

1. Accedi a [Adobe Experience Cloud](https://experience.adobe.com/).

1. Apri Commerce Cloud Manager:
   - In **Accesso rapido**, fare clic su **Commerce**.
   - Visualizza le istanze disponibili.

1. Accedi all’istanza:

   Fare clic sul nome istanza per aprire l&#39;applicazione [!DNL Adobe Commerce Optimizer].

1. Ottieni dettagli istanza:
   - Fai clic sull’icona delle informazioni accanto al nome dell’istanza.
   - Prendere nota dell&#39;endpoint GraphQL, dell&#39;endpoint Catalog Service per l&#39;acquisizione dei dati e dell&#39;ID istanza (noto anche come `tenant ID`).

   ![Dettagli istanza](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

   I dettagli dell’endpoint e dell’ID istanza (ID tenant) sono necessari per l’integrazione con le applicazioni front-end e i sistemi back-end. L&#39;URL per accedere all&#39;applicazione [!DNL Adobe Commerce Optimizer] viene fornito anche qui.

   Non tutti gli utenti di Adobe Commerce Optimizer hanno accesso a Cloud Manager e ai dettagli dell’istanza. L’accesso dipende dal ruolo e dalle autorizzazioni assegnati all’account utente. Se non disponi dell’accesso, contatta l’amministratore dell’organizzazione per ottenere i dettagli dell’istanza.

1. Modifica il nome e la descrizione dell’istanza:
   - Fai clic sull&#39;icona **Modifica** accanto al nome di un&#39;istanza.
   - Se necessario, aggiorna il nome e la descrizione.
   - Fai clic su **Salva**.

   Puoi anche utilizzare le opzioni di ricerca e filtro per trovare rapidamente istanze specifiche.

## Aggiungi dati di esempio

Adobe fornisce un archivio GitHub con dati e strumenti di esempio per aiutarti ad apprendere e testare le funzionalità di [!DNL Adobe Commerce Optimizer].
I dati di esempio si basano sullo [scenario aziendale Carvelo](./use-case/admin-use-case.md) e includono:

- Catalogo dei prodotti con parti per autoveicoli
- Più listini prezzi e scenari di determinazione prezzi
- Visualizzazioni del catalogo e criteri per diversi dealer
- Esempi completi di flusso di lavoro end-to-end

**Caricare i dati di esempio:**

1. Accedi all’archivio GitHub:
   - Visita il [archivio di acquisizione dati del catalogo di esempio](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion)
   - Seguire le istruzioni di installazione nel file README dell&#39;archivio.

2. Esegui l’acquisizione:
   - Utilizza gli script forniti per caricare i dati di esempio nell’ambiente di staging Adobe Commerce Optimizer.
   - Verifica che i dati vengano visualizzati nella pagina [Sincronizzazione dati](./setup/data-sync.md).

3. Pulizia (facoltativa):

   Rimuovere i dati di esempio utilizzando lo script `reset.js` incluso nel codice sorgente del caricatore dati di esempio.

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

- **Risorse per sviluppatori**: [Documentazione per sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog/)
- **Risorse Storefront**: [Documentazione Storefront Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/)
- **Supporto**: [Risorse di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)
