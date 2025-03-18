---
title: Migrazione ad Adobe Commerce as a Cloud Service
description: Scopri come effettuare la migrazione ad Adobe Commerce as a Cloud Service.
source-git-commit: 19c49b2b9d630898353addd778e062d3208505c1
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---


# Migrazione ad Adobe Commerce as a Cloud Service

Adobe Commerce as a Cloud Service fornisce la maggior parte delle configurazioni pronte all’uso. Tuttavia, se esegui la migrazione da un’istanza esistente di Adobe Commerce on Cloud o on-premise, dovrai eseguire diverse azioni di migrazione a seconda della configurazione specifica.

## Percorsi di migrazione

Adobe Commerce as a Cloud Service supporta più percorsi di migrazione, a seconda della timeline, della vetrina e delle personalizzazioni.

In alternativa alla migrazione completa, Adobe Commerce as a Cloud Service supporta una migrazione graduale utilizzando Commerce Optimizer o un approccio incrementale.

* **Migrazione incrementale**: questo approccio prevede la migrazione di dati, personalizzazioni e integrazioni in più fasi. Questo approccio è ideale per i grandi commercianti con molte personalizzazioni che desiderano migrare gradualmente le loro complesse personalizzazioni e dati ad Adobe Commerce as a Cloud Service al proprio ritmo.

![migrazione incrementale](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**: questo approccio consente di eseguire la migrazione iterativa utilizzando Commerce Optimizer come fase di transizione per spostare personalizzazioni e dati complessi in Adobe Commerce as a Cloud Service al tuo ritmo. Commerce Optimizer fornisce l’accesso ai servizi di merchandising basati su criteri e canali di catalogo, Commerce Storefront basato su Edge Delivery e Visualizzazioni di prodotto basate su AEM Assets.

![migrazione iterativa](./assets/optimizer.png){width="600" zoomable="yes"}

* **Migrazione completa**: questo approccio comporta la migrazione simultanea di tutti i dati, le personalizzazioni e le integrazioni. Questo approccio è ideale per i commercianti più piccoli con poche personalizzazioni che desiderano passare rapidamente ad Adobe Commerce as a Cloud Service.

La tabella seguente fornisce una panoramica del processo di migrazione per diversi storefront e configurazioni:

|                    | LUMA Storefront | PWA Storefront | Commerce Storefront con tecnologia Edge Delivery | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migrazione dei dati | Obbligatorio | Obbligatorio | Obbligatorio | Obbligatorio |
| Vetrina | Migrare a Commerce Storefront con tecnologia Edge Delivery | Migrare a Commerce Storefront con tecnologia Edge Delivery o Gestisci | Nessun impatto | Nessun impatto |
| Mesh API | Crea nuova rete | Crea nuova rete o riconfigura esistente | Crea nuova rete o riconfigura esistente | Crea nuova rete o riconfigura esistente |
| Integrazioni | Utilizzo del kit di avvio per l&#39;integrazione | Utilizzo del kit di avvio per l&#39;integrazione | Utilizzo del kit di avvio per l&#39;integrazione | Utilizzo del kit di avvio per l&#39;integrazione |
| Personalizzazioni | Passa ad App Builder e Mesh API | Passa ad App Builder e Mesh API | Passa ad App Builder e Mesh API | Passa ad App Builder e Mesh API |
| Gestione Assets | Migrazione necessaria se si utilizza OOTB | Migrazione necessaria se si utilizza OOTB | Migrazione necessaria se si utilizza OOTB | Migrazione necessaria se si utilizza OOTB |
| Estensioni | Migrare ad App Builder | Migrare ad App Builder | Migrare ad App Builder | Migrare ad App Builder |

Come indicato nella tabella, le mitigazioni per ogni migrazione consisteranno in:

* **Migrazione dati** - Utilizzo degli strumenti di migrazione forniti per eseguire la migrazione dei dati dall&#39;istanza esistente ad Adobe Commerce as a Cloud Service.
* **Storefront**: gli EDS e gli storefront headless esistenti non richiedono alcuna mitigazione, ma gli storefront LUMA richiedono la migrazione a Commerce Storefront con tecnologia Edge Delivery. È possibile migrare le vetrine dei negozi PWA Studio a Commerce basate su Edge Delivery o mantenerle nello stato corrente. Adobe fornirà acceleratori per assistere la migrazione della vetrina.
* **[Rete API](https://developer.adobe.com/graphql-mesh-gateway)**—Crea una nuova rete o modifica quella esistente. Per facilitare questo processo, Adobe fornirà delle maglie preconfigurate.
* **Integrazioni** - Tutte le integrazioni devono utilizzare il [kit di avvio dell&#39;integrazione](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) o l&#39;[API REST di Adobe Commerce as a Cloud Service](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/).
* **Personalizzazioni** - Tutte le personalizzazioni devono essere spostate in App Builder e API Mesh.
* **Gestione Assets**: la gestione di tutte le risorse richiede la migrazione. Se utilizzi già AEM Assets, non è necessario eseguire la migrazione.
* **Estensioni** - Tutte le estensioni in-process devono essere ricreate come estensioni out-of-process. Entro la fine del 2025, Adobe fornirà 100 delle nostre estensioni più popolari precaricate e pronte all’uso per ridurre al minimo i tempi di build.

## Fasi di migrazione

La migrazione dall’istanza Adobe Commerce corrente a una nuova istanza Adobe Commerce as a Cloud Service prevede principalmente le seguenti fasi:

* **[Preparazione](#readiness-phase)**: per iniziare, verifica se la distribuzione è pronta per essere spostata in ACS. In questa fase, dovresti anche acquisire familiarità con le modifiche introdotte da ACS&#x200B;.
* **[Implementazione](#implementation-phase)**: prepara il codice, la vetrina, le estensioni e le integrazioni per la migrazione. Per facilitare la transizione, Adobe consente sia [approcci iterativi a breve che a lungo termine](#migration-paths). &#x200B;
* **[Pubblica](#go-live-phase)** - Verifica e conferma che tutto sia pronto, quindi esegui la migrazione dei dati.
* **[Post pubblicazione](#post-go-live-phase)**: in collaborazione con Adobe, monitora eventuali problemi e migliora le prestazioni secondo necessità al termine della migrazione.

### Fase di preparazione

1. Per iniziare, rivedi l’architettura di Adobe Commerce as a Cloud Service, il framework di estensibilità e le funzionalità della vetrina:

   * [Architettura di Adobe Commerce on Cloud Services](./overview.md): verifica l&#39;architettura della piattaforma e le differenze rispetto all&#39;istanza Adobe Commerce corrente.
   * [Adobe Commerce Extensibility Framework](https://developer.adobe.com/commerce/extensibility/)—Identifica come desideri effettuare la transizione alle personalizzazioni correnti.
   * [Commerce Storefront con tecnologia Edge Delivery](https://experienceleague.adobe.com/developer/commerce/storefront/): rivedi la soluzione storefront consigliata.

1. Verifica la compatibilità della personalizzazione:

   * Identifica i moduli personalizzati correnti e le integrazioni di terze parti.
   * Valuta le personalizzazioni che devono essere reimplementate utilizzando App Builder.
   * Mappa le personalizzazioni correnti agli equivalenti delle estensioni App Builder.

1. Conferma i requisiti della vetrina e assicurati che siano in linea con le funzionalità di distribuzione di Adobe Edge.

1. Esamina le integrazioni di terze parti correnti e conferma la compatibilità delle API con la piattaforma Adobe Commerce as a Cloud Service.

### Fase di implementazione

I passaggi seguenti descrivono il processo di sviluppo ed esecuzione della migrazione:

1. Crea una nuova istanza di Adobe Commerce as a Cloud Service in [Commerce Cloud Manager](./getting-started.md#create-an-instance).

1. Installa le app e le personalizzazioni necessarie. Adobe Commerce as a Cloud Service è precaricato con 100 delle app più popolari. Se hai bisogno di app o personalizzazioni aggiuntive, puoi implementarle nuovamente utilizzando App Builder.

1. Imposta uno dei seguenti storefront basati su GraphQL:

   * [Crea una vetrina Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)
   * [Usa PWA Studio per creare una vetrina personalizzata basata su GraphQL](https://developer.adobe.com/commerce/pwa-studio/)

1. Esegui la migrazione dei dati dall’istanza Commerce precedente ad ACCS:

   * Esegui la migrazione dei dati nativi di Adobe Commerce utilizzando gli strumenti di migrazione dei dati.
   * Migrazione di estensioni e personalizzazioni di terze parti
   * Migrazione dei dati di configurazione e integrazione:
      * Trasferisci configurazioni Mesh API, servizi di terze parti e integrazioni di sistema utilizzando [Adobe Commerce Integration Starter Kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/).

### Fase di lancio

Prima di avviare, convalida e verifica la nuova istanza di Adobe Commerce as a Cloud Service:

* **Test funzionali**: garantisce il corretto funzionamento dei dati migrati, delle funzionalità di storefront e delle personalizzazioni.

* **Test delle prestazioni**: valuta la velocità e la scalabilità dei tuoi negozi per garantire prestazioni ottimali a livello globale.

* **Controllo di sicurezza**: verifica le misure di sicurezza, incluso il controllo dell&#39;accesso API e qualsiasi potenziale vulnerabilità.

### Fase post-pubblicazione

Dopo aver convalidato e testato la nuova istanza sandbox di Adobe Commerce as a Cloud Service, puoi avviare l’istanza di produzione:

1. Vai in diretta

   * Reindirizza il traffico alla nuova piattaforma e monitora le prestazioni.
   * Disattiva la vecchia istanza di Adobe Commerce.

1. Monitoraggio post-lancio

   * Utilizza strumenti di monitoraggio per garantire operazioni stabili e risolvere eventuali problemi successivi al lancio.
