---
title: Introduzione
description: Scopri come iniziare a utilizzare  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# Introduzione

Questo articolo illustra come imparare a utilizzare [!DNL Adobe Commerce Optimizer]. Questa guida si concentra sui ruoli di merchandiser e amministratore, ma include anche brevi attività di alto livello che uno sviluppatore potrebbe eseguire. Per informazioni dettagliate sui contenuti specifici per gli sviluppatori, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

## Qual è il tuo ruolo?

La corretta configurazione di [!DNL Adobe Commerce Optimizer] coinvolge in genere i seguenti membri del team:

- Amministratore
- Sviluppatore
- Merchandiser

Ogni membro del team ha il proprio set di ruoli e responsabilità come descritto nella tabella seguente:

| Ruolo/i | Attività |
|---|---|
| Amministratore | Utilizza Admin Console per creare amministratori, gruppi di utenti, utenti e sviluppatori&#x200B;. |
|  | Creare una nuova istanza [!DNL Adobe Commerce Optimizer] in Commerce Cloud Manager.&#x200B; |
|  | Imposta i criteri e le viste catalogo. |
| Sviluppatore | Utilizza Developer Console per creare un progetto, concedere agli sviluppatori l’accesso alle API e installare le applicazioni e le personalizzazioni necessarie. |
|  | Connettiti al tuo sistema di back office (carrello, pagamento) utilizzando API Mesh e App Builder&#x200B;. |
|  | Acquisisci i dati del catalogo dalle soluzioni commerce esistenti utilizzando l’API di acquisizione dati di Merchandising Services&#x200B; |
|  | Configurare la vetrina |
| Merchandiser | Configurare l&#39;individuazione del prodotto&#x200B; |
|  | Configurare i consigli di prodotto. |

Ciascun ruolo svolge un ruolo fondamentale nell&#39;onboarding e nel lancio dell&#39;ambiente [!DNL Adobe Commerce Optimizer]. Il diagramma seguente mostra un flusso di lavoro di alto livello dall’inizio alla fine per ogni ruolo dell’organizzazione:

![Flusso di lavoro di alto livello](./assets/high-level-workflow.png){zoomable="yes"}

### Amministratore

Gli amministratori sono responsabili della configurazione delle istanze e della gestione di utenti, gruppi e autorizzazioni per la tua organizzazione.

- **[Accedi a Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html)** - Gestisci i diritti Adobe in tutta l&#39;organizzazione. Consulta [gestione utenti](./user-management.md) per scoprire come l&#39;amministratore di prodotto o l&#39;amministratore di sistema della tua organizzazione può aggiungere utenti al prodotto [!DNL Adobe Commerce Optimizer].

- **Crea un&#39;istanza** - [!DNL Adobe Commerce Optimizer] istanze utilizzano un sistema basato sul credito. Puoi creare più istanze Sandbox e Produzione, ciascuna delle quali richiede un credito corrispondente. La quantità di crediti che hai inizialmente dipende dal tuo abbonamento. [Ulteriori informazioni](#create-an-instance).

- **Accedere a un&#39;istanza** - Dopo aver creato un&#39;istanza, è possibile accedervi da [!UICONTROL Commerce Cloud Manager]. [Ulteriori informazioni](#access-an-instance).

- **Imposta le visualizzazioni e i criteri del catalogo** - Scopri come [definire le visualizzazioni e i criteri del catalogo](./setup/catalog-view.md). Il catalogo non solo contiene i dati dei prodotti, ma consente anche di definire la struttura aziendale.

### Sviluppatore

Gli sviluppatori creano progetti e credenziali, installano estensioni, acquisiscono dati di catalogo ed eseguono attività generali sull’architettura della piattaforma. Per informazioni dettagliate sui contenuti specifici per gli sviluppatori, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

- **Accedi a Developer Console** - Accedi a [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) per creare un progetto per [!DNL Adobe Commerce Optimizer], generare token di accesso e installare le applicazioni e le personalizzazioni necessarie.

- **Acquisisci dati catalogo**. Per informazioni su come importare i dati del catalogo in [!DNL Adobe Commerce Optimizer], consulta la [documentazione dell&#39;API di acquisizione dati](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).

  I dati del catalogo acquisiti sono visibili nella pagina [sincronizzazione dati](./setup/data-sync.md).

- **Configura la vetrina** - Prima di configurare la vetrina, devi prima creare un&#39;istanza, che è un&#39;attività in genere eseguita dall&#39;[amministratore](#administrator) della tua organizzazione. Dopo aver creato l&#39;istanza, puoi procedere con [la configurazione](./storefront.md) della Commerce Storefront con tecnologia Edge Delivery Services.

### Merchandiser

Il merchandiser utilizza i dati e le analisi dei clienti per prendere decisioni strategiche sul posizionamento dei prodotti, sui prezzi e sulle promozioni sul punto vendita, ottimizzando al contempo le esperienze di acquisto attraverso l’individuazione dei prodotti e i consigli.

- **Configurazione dell&#39;individuazione del prodotto e raccomandazioni** - Scopri come [creare esperienze personalizzate](./merchandising/overview.md) per gli acquirenti tramite l&#39;individuazione del prodotto e i consigli.

## Creare un’istanza

1. Accedi al tuo account [Adobe Experience Cloud](https://experience.adobe.com/).

1. In [!UICONTROL Quick access], fare clic su [!UICONTROL **Commerce**] per aprire [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visualizza un elenco di [!DNL Adobe Commerce] istanze disponibili nell&#39;organizzazione Adobe IMS, incluse entrambe le istanze con provisioning per [!DNL Adobe Commerce Optimizer] e [!DNL Adobe Commerce as a Cloud Service].

1. Fai clic su [!UICONTROL **Aggiungi istanza**] nell&#39;angolo superiore destro della schermata.

   ![Crea istanza](./assets/create-aco-instance.png){width="100%" align="center" zoomable="yes"}

1. Seleziona [!UICONTROL **Commerce Optimizer**].

1. Immetti **Nome** e **Descrizione** per l&#39;istanza.

1. Seleziona l’area geografica in cui desideri che sia ospitata l’istanza.

   >[!NOTE]
   >
   >Dopo aver creato un&#39;istanza, non potete modificare l&#39;area.

1. Scegli uno dei seguenti [!UICONTROL **Tipo di ambiente**] per l&#39;istanza:

   - [!UICONTROL **Sandbox**] - Ideale per scopi di progettazione e test. Devi iniziare il percorso [!DNL Adobe Commerce Optimizer] utilizzando l&#39;ambiente sandbox.
   - [!UICONTROL **Produzione**] - Per negozi live e siti rivolti ai clienti.

   >[!NOTE]
   >
   >Le istanze sandbox sono attualmente limitate all’area Nord America.

1. Fai clic su [!UICONTROL **Aggiungi istanza**].

   La nuova istanza è ora disponibile in Cloud Manager.

1. Per visualizzare i dettagli dell’istanza, inclusi gli endpoint di GraphQL e Catalog Service, l’URL per accedere all’applicazione Adobe Commerce Optimizer e l’ID istanza (ID tenant), fai clic sull’icona delle informazioni accanto al nome dell’istanza.

   ![Crea istanza](./assets/aco-instance-details.png){width="100%" align="center" zoomable="yes"}

## Accedere a un’istanza

1. Accedi al tuo account [Adobe Experience Cloud](https://experience.adobe.com/).

1. In [!UICONTROL Quick access], fare clic su [!UICONTROL **Commerce**] per aprire [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visualizza un elenco delle istanze disponibili nell&#39;organizzazione Adobe IMS.

1. Per aprire l&#39;applicazione [!UICONTROL Commerce Optimizer] associata a un&#39;istanza, fare clic sul nome dell&#39;istanza.


