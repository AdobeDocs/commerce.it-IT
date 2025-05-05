---
title: Connettere dati Commerce a Adobe Experience Platform
description: Scopri come collegare i dati Commerce a Adobe Experience Platform.
feature: Personalization, Integration, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 0%

---

# Connettere i dati Commerce a Adobe Experience Platform

Quando installi l&#39;estensione [!DNL Data Connection], nel menu **System** di **Services** in Commerce _Admin_ vengono visualizzate due nuove pagine di configurazione.

- Connettore servizi Commerce
- [!DNL Data Connection]

Per connettere l&#39;istanza Adobe Commerce a Adobe Experience Platform, è necessario configurare entrambi i connettori, partendo dal connettore Commerce Services e terminando con l&#39;estensione [!DNL Data Connection].

## Configurare il connettore dei servizi Commerce

Se in precedenza hai installato un servizio Adobe Commerce, probabilmente hai già configurato il connettore dei servizi Commerce. In caso contrario, è necessario completare le seguenti attività nella pagina [Connettore servizi Commerce](../landing/saas.md):

1. Accedi al tuo account Commerce per [recuperare le chiavi API di produzione e sandbox](../landing/saas.md#credentials).
1. Selezionare uno [spazio dati SaaS](../landing/saas.md#saas-configuration).
1. Accedi al tuo account Adobe per [recuperare l&#39;ID organizzazione](../landing/saas.md#ims-organization-optional).

Dopo aver configurato il connettore Commerce Services, configurare l&#39;estensione [!DNL Data Connection].

## Configura l&#39;estensione [!DNL Data Connection]

In questa sezione imparerai a configurare l&#39;estensione [!DNL Data Connection].

### Aggiungi dettagli account servizio e credenziali

Se si prevede di raccogliere e inviare [dati cronologici degli ordini](#send-historical-order-data) o [dati del profilo cliente](#send-customer-profile-data), è necessario aggiungere i dettagli dell&#39;account del servizio e delle credenziali. Inoltre, se stai configurando l&#39;estensione [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=it), devi completare questi passaggi.

Se raccogli e invii solo dati di vetrina o di back office, puoi passare alla sezione [generale](#general).

#### Passaggio 1: creare un progetto in Adobe Developer Console

Crea un progetto in Adobe Developer Console che autentica Commerce in modo che possa effettuare chiamate API Experience Platform.

Per creare il progetto, segui i passaggi descritti nell&#39;esercitazione [Autentica e accedi alle API di Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=it).

Durante l’esercitazione, assicurati che il progetto presenti quanto segue:

- Accesso ai [profili di prodotto](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=it#select-product-profiles) seguenti: **Accesso predefinito a tutti i prodotti** e **Accesso predefinito a tutti i prodotti AEP**.
- [ ruoli e autorizzazioni corretti configurati](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=it#assign-api-to-a-role).
- Se hai deciso di utilizzare i token web JSON (JWT) come metodo di autenticazione server-to-server, devi caricare anche una chiave privata.

Il risultato di questo passaggio crea un file di configurazione da utilizzare nel passaggio successivo.

#### Passaggio 2: scarica il file di configurazione

Scarica il [file di configurazione dell&#39;area di lavoro](https://developer.adobe.com/commerce/extensibility/events/project-setup/#download-the-workspace-configuration-file). Copiare e incollare il contenuto del file nella pagina **Dettagli account di servizio/credenziali** dell&#39;amministratore di Commerce.

1. In Amministrazione Commerce, passa a **Archivi** > Impostazioni > **Configurazione** > **Servizi** > **[!DNL Data Connection]**.

1. Selezionare il metodo di autorizzazione server-to-server implementato dal menu **Tipo di autorizzazione Adobe Developer**. Adobe consiglia di utilizzare OAuth. Il codice JWT è stato dichiarato obsoleto. [Ulteriori informazioni](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

1. (Solo JWT) Copia e incolla il contenuto del file `private.key` nel campo **Segreto client**. Utilizza il seguente comando per copiare il contenuto.

   ```bash
   cat config/private.key | pbcopy
   ```

   Per ulteriori informazioni sul file `private.key`, vedere Autenticazione dell&#39;account di servizio [&#128279;](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

1. Copiare il contenuto del file `<workspace-name>.json` nel campo **Dettagli account/credenziali servizio**.

   Configurazione amministratore ![[!DNL Data Connection]](./assets/epc-admin-config.png){width="700" zoomable="yes"}

1. Fai clic su **Salva configurazione**.

1. Fare clic sul pulsante **[!UICONTROL Test connection]** per verificare che le informazioni sull&#39;account del servizio e sulle credenziali immesse siano corrette.

### Generale

1. In Amministrazione, passa a **Sistema** > Servizi > **[!DNL Data Connection]**.

   Impostazioni ![[!DNL Data Connection]](./assets/epc-settings.png){width="700" zoomable="yes"}

1. Nella scheda **Impostazioni** in **Generale**, verifica l&#39;ID associato al tuo account Adobe Experience Platform, come configurato in [Connettore servizi Commerce](../landing/saas.md#organizationid). L’ID organizzazione è globale. È possibile associare un solo ID organizzazione per istanza di Adobe Commerce.

1. Nel menu a discesa **Ambito**, impostare il contesto su **Sito Web**.

1. (Facoltativo) Se hai già distribuito un [AEP Web SDK (lega)](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=it) nel tuo sito, abilita la casella di controllo e aggiungi il nome del tuo AEP Web SDK. In caso contrario, lasciare vuoti questi campi e l&#39;estensione [!DNL Data Connection] ne distribuisce uno.

   >[!NOTE]
   >
   >Se si specifica il proprio AEP Web SDK, l&#39;estensione [!DNL Data Connection] utilizza l&#39;ID dello stream di dati associato a tale SDK e non l&#39;ID dello stream di dati specificato in questa pagina (se presente).

### Raccolta dati

In questa sezione puoi specificare il tipo di dati da raccogliere e inviare al server Edge di Experience Platform. Esistono tre tipi di dati:

- **Comportamentale** (dati lato client) sono dati acquisiti nella vetrina. Sono incluse le interazioni con gli acquirenti, ad esempio `View Page`, `View Product`, `Add to Cart` e [informazioni sull&#39;elenco richieste](events.md#b2b-events) (per gli esercenti B2B).

- **Back office** (dati lato server) sono dati acquisiti nei server Commerce. Ciò include informazioni sullo stato di un ordine, ad esempio se un ordine è stato effettuato, annullato, rimborsato, spedito o completato. Include anche [dati cronologici dell&#39;ordine](#send-historical-order-data).

- **Il profilo** è costituito da dati relativi alle informazioni del profilo dell&#39;acquirente. Ulteriori informazioni [su](#send-customer-profile-data).

Per garantire che l&#39;istanza di Adobe Commerce possa iniziare la raccolta dati, controlla i [prerequisiti](overview.md#prerequisites).

Per ulteriori informazioni sugli eventi [storefront](events.md#storefront-events), [back office](events-backoffice.md) e [profile](events-backoffice.md#customer-profile-events-server-side), vedere l&#39;argomento eventi.

>[!NOTE]
>
>Tutti i campi nella sezione **Raccolta dati** si applicano all&#39;ambito **Sito Web** o versione successiva.

1. Seleziona **Eventi storefront** se desideri inviare dati comportamentali storefront.

1. Selezionare **Eventi back office** per inviare informazioni sullo stato dell&#39;ordine, ad esempio se un ordine è stato effettuato, annullato, rimborsato o spedito.

   >[!NOTE]
   >
   >Se si seleziona **Eventi back office**, tutti i dati back office vengono inviati al server Edge di Experience Platform. Se un acquirente sceglie di rinunciare alla raccolta dei dati, devi impostare esplicitamente la preferenza relativa alla privacy dell’acquirente in Experience Platform. Questo è diverso dagli eventi di vetrina in cui l’agente di raccolta gestisce già il consenso in base alle preferenze dell’acquirente. [ulteriori](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html?lang=it) informazioni sull&#39;impostazione delle preferenze di privacy di un acquirente in Experience Platform.

1. (Ignora questo passaggio se utilizzi un tuo AEP Web SDK.) [Crea](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=it#create) uno stream di dati in Adobe Experience Platform o seleziona uno stream di dati esistente da utilizzare per la raccolta. Immetti l&#39;ID dello stream di dati nel campo **ID dello stream di dati**.

1. Immettere il **ID set di dati** che si desidera includere nei dati di Commerce. Per trovare l’ID del set di dati:

   1. Apri l&#39;interfaccia utente di Experience Platform e seleziona **Set di dati** nell&#39;area di navigazione a sinistra per aprire il dashboard **Set di dati**. Il dashboard elenca tutti i set di dati disponibili per l’organizzazione. Vengono visualizzati i dettagli di ciascun set di dati elencato, tra cui il nome, lo schema a cui il set di dati aderisce e lo stato dell’esecuzione dell’acquisizione più recente.
   1. Apri il set di dati associato allo stream di dati.
   1. Nel riquadro di destra, visualizzare i dettagli sul set di dati. Copia l’ID del set di dati.

1. Per garantire gli aggiornamenti dei dati degli eventi di back office in base a una pianificazione in base a un processo [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=it), è necessario modificare l&#39;indice `Sales Orders Feed` in `Update by Schedule`.

   1. Nella barra laterale _Admin_, passa a **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Index Management]**.

   1. Selezionare la casella di controllo per l&#39;indicizzatore `Sales Orders Feed`.

   1. Imposta **[!UICONTROL Actions]** su `Update by Schedule`.

   1. Se si abilitano i dati di back office per la prima volta, eseguire i seguenti comandi per reindicizzare e attivare una risincronizzazione. Le successive risincronizzazioni si verificano automaticamente se il processo [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=it) è configurato correttamente.

      ```bash
      bin/magento index:reindex sales_order_data_exporter_v2
      ```

      ```bash
      bin/magento saas:resync --feed orders
      ```

#### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Ambito | Sito Web specifico in cui desideri applicare le impostazioni di configurazione. |
| ID organizzazione (globale) | ID che appartiene all’organizzazione che ha acquistato il prodotto Adobe DX. Questo ID collega l’istanza di Adobe Commerce a Adobe Experience Platform. |
| AEP Web SDK è già distribuito nel sito? | Selezionare questa casella di controllo se AEP Web SDK è stato implementato nel sito |
| Nome AEP Web SDK (globale) | Se nel sito è già stato distribuito un Experience Platform Web SDK, specificare il nome di tale SDK in questo campo. Questo consente a Storefront Event Collector e Storefront Event SDK di utilizzare Experience Platform Web SDK anziché la versione distribuita dall&#39;estensione [!DNL Data Connection]. Se non hai implementato un Experience Platform Web SDK nel tuo sito, lascia vuoto questo campo e l&#39;estensione [!DNL Data Connection] ne distribuisce uno per te. |
| Eventi vetrina | È selezionato per impostazione predefinita, purché l’ID organizzazione e l’ID dello stream di dati siano validi. Gli eventi di vetrina raccolgono dati comportamentali anonimi dai tuoi acquirenti durante la navigazione sul tuo sito. |
| Eventi back office | Se selezionato, il payload dell’evento contiene informazioni anonime sullo stato dell’ordine, ad esempio se un ordine è stato effettuato, annullato, rimborsato o spedito. |
| ID flusso di dati (sito web) | ID che consente il flusso di dati da Adobe Experience Platform ad altri prodotti Adobe DX. Questo ID deve essere associato a un sito web specifico all’interno della tua istanza Adobe Commerce specifica. Se specifichi un Experience Platform Web SDK personalizzato, non specificare un ID dello stream di dati in questo campo. L&#39;estensione [!DNL Data Connection] utilizza l&#39;ID dello stream di dati associato a tale SDK e ignora qualsiasi ID dello stream di dati specificato in questo campo (se presente). |
| ID set di dati (sito web) | ID del set di dati che contiene i dati di Commerce. Questo campo è obbligatorio a meno che non siano state deselezionate le caselle di controllo **Storefront events** o **Back office events**. Inoltre, se utilizzi un tuo Experience Platform Web SDK e pertanto non hai specificato un ID dello stream di dati, devi comunque aggiungere l’ID del set di dati associato allo stream di dati. In caso contrario, non è possibile salvare il modulo. |

Dopo l’onboarding, i dati della vetrina iniziano a fluire verso il server Edge di Experience Platform. I dati di back office richiedono circa cinque minuti per essere visualizzati ai margini. Gli aggiornamenti successivi sono visibili sul server Edge in base alla pianificazione cron.

### Inviare dati del profilo cliente

Esistono due tipi di dati di profilo che puoi inviare ad Experience Platform: i record di profilo e gli eventi di profilo della serie temporale.

Un record di profilo contiene dati salvati quando un acquirente crea un profilo nell’istanza Commerce, ad esempio il nome dell’acquirente. Quando lo schema e il set di dati sono [configurati correttamente](profile-data.md), viene inviato un record di profilo ad Experience Platform e inoltrato al servizio di gestione profili e segmentazione di Adobe: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it).

Gli eventi di profilo della serie temporale contengono dati sulle informazioni del profilo dell’acquirente, ad esempio se creano, modificano o eliminano un account sul sito. Quando i dati dell’evento profilo vengono inviati ad Experience Platform, risiedono in un set di dati in cui possono essere utilizzati da altri prodotti DX.

1. Assicurati di aver [fornito](#add-service-account-and-credential-details) i dettagli dell&#39;account del servizio e delle credenziali.

1. Assicurati di avere uno schema e un set di dati specificati per l&#39;acquisizione dei dati dell&#39;evento del profilo [&#128279;](profile-data.md) e per l&#39;acquisizione dei dati dell&#39;evento del profilo della [serie temporale](update-xdm.md#time-series-profile-event-data).

1. Se desideri inviare i dati del profilo ad Experience Platform, seleziona la casella di controllo **Profili cliente**.

1. Immettere l&#39;ID **Set di dati profilo**.

   I dati del record profilo devono utilizzare un set di dati diverso da quello attualmente in uso per i dati comportamentali e di back office.

1. Se non desideri inviare in streaming gli eventi di profilo attraverso lo stesso ID dello stream di dati utilizzato per i dati comportamentali e di back office, rimuovi il segno di spunta da **Trasmetti profili cliente attraverso lo stesso ID dello stream di dati** e immetti l&#39;ID dello stream di dati che desideri utilizzare al suo posto.

La disponibilità di un record di profilo in Real-Time CDP può richiedere circa 10 minuti. Lo streaming degli eventi del profilo inizia immediatamente.

>[!TIP]
>
>Se non vengono visualizzati i dati del profilo in Experience Platform, consultare [Commerce KnowledgeBase](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported) per suggerimenti sulla risoluzione dei problemi.

#### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Profili cliente | Selezionare questa casella di controllo se si desidera raccogliere e inviare i record del profilo cliente. |
| ID del set di dati profilo | Un record di profilo deve utilizzare un set di dati diverso da quello utilizzato per eventi comportamentali e di back office. |
| Trasmetti i profili cliente attraverso lo stesso ID dello stream di dati | Decidi se utilizzare o meno lo stesso flusso di dati attualmente utilizzato per gli eventi comportamentali e di back office. |
| Stream di dati per i profili cliente | Specifica lo stream di dati specifico per il record del profilo cliente. |

### Inviare dati cronologici degli ordini

Adobe Commerce raccoglie fino a cinque anni di [dati storici sugli ordini e stato](events-backoffice.md#back-office-events). Puoi utilizzare l&#39;estensione [!DNL Data Connection] per inviare tali dati storici ad Experience Platform per arricchire i profili dei clienti e personalizzare le esperienze dei clienti in base a tali ordini passati. I dati vengono memorizzati in un set di dati in Experience Platform.

Anche se Commerce raccoglie già i dati storici dell’ordine, è necessario completare diversi passaggi per inviarli ad Experience Platform.

Guarda questo video per ulteriori informazioni sugli ordini storici, quindi completa i seguenti passaggi per implementare la raccolta degli ordini storici.

>[!VIDEO](https://video.tv.adobe.com/v/3450235?captions=ita)

#### Impostare il servizio di sincronizzazione ordini

Il servizio di sincronizzazione ordini utilizza [Message Queue Framework](https://developer.adobe.com/commerce/php/development/components/message-queues/) e RabbitMQ. Dopo aver completato questi passaggi, i dati sullo stato dell’ordine possono essere sincronizzati con SaaS, operazione necessaria prima dell’invio ad Experience Platform.

1. Assicurati di aver [fornito](#add-service-account-and-credential-details) i dettagli dell&#39;account del servizio e delle credenziali.

1. [Abilita](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq.html?lang=it) RabbitMQ.

   >[!NOTE]
   >
   >RabbitMQ è già configurato per Commerce versione 2.4.7 e successive, ma devi abilitare i consumatori.

1. Abilitare i consumer della coda messaggi tramite il processo cron in `.magento.env.yaml` utilizzando la variabile di ambiente `CRON_CONSUMERS_RUNNER`.

   ```yaml
      stage:
        deploy:
          CRON_CONSUMERS_RUNNER:
            cron_run: true
   ```

   >[!NOTE]
   >
   >Per informazioni su tutte le opzioni di configurazione disponibili, consulta la documentazione sulle [variabili di distribuzione](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html?lang=it#cron_consumers_runner).

Se il servizio di sincronizzazione ordini è abilitato, è possibile specificare l&#39;intervallo di date dell&#39;ordine cronologico nella pagina **[!UICONTROL [!DNL Data Connection]]**.

#### Specifica intervallo date cronologia ordini

Specifica l’intervallo di date per gli ordini storici da inviare ad Experience Platform.

1. In Amministrazione, passa a **Sistema** > Servizi > **[!DNL Data Connection]**.

1. Selezionare la scheda **Cronologia ordini**.

   ![[!DNL Data Connection] cronologia ordini](./assets/epc-order-history.png){width="700" zoomable="yes"}

1. In **Sincronizzazione cronologia ordini**, la casella di controllo **Copia ID set di dati dalle impostazioni** è già abilitata. In questo modo si utilizza lo stesso set di dati specificato nella scheda **Impostazioni**.

1. Nei campi **Da** e **A**, specifica l&#39;intervallo di date per i dati dell&#39;ordine cronologico che desideri inviare. Non puoi selezionare un intervallo di date superiore a cinque anni.

1. Selezionare **[!UICONTROL Start Sync]** per avviare la sincronizzazione. I dati storici dell’ordine sono dati in batch, anziché dati di vetrina e di back office che sono dati in streaming. L’invio dei dati in batch in Experience Platform richiede circa 45 minuti.

##### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Copia ID set di dati dalle impostazioni | Copia l&#39;ID del set di dati immesso nella scheda **Impostazioni**. |
| ID set di dati (sito web) | ID del set di dati che contiene i dati di Commerce. Questo campo è obbligatorio a meno che non siano state deselezionate le caselle di controllo **Storefront events** o **Back office events**. Inoltre, se utilizzi un tuo Experience Platform Web SDK e pertanto non hai specificato un ID dello stream di dati, devi comunque aggiungere l’ID del set di dati associato allo stream di dati. In caso contrario, non è possibile salvare il modulo. |
| Da | Data a partire dalla quale si desidera iniziare la raccolta dei dati della cronologia degli ordini. |
| A | Data a partire dalla quale si desidera terminare la raccolta dei dati della cronologia degli ordini. |
| Avvia sincronizzazione | Avvia il processo di sincronizzazione dei dati della cronologia degli ordini con Experience Platform Edge. Questo pulsante è disabilitato se il campo **[!UICONTROL Dataset ID]** è vuoto o se l&#39;ID del set di dati non è valido. |

### Personalizzazione dei dati

Nella scheda **Personalizzazione dati** puoi visualizzare tutti gli attributi personalizzati configurati in [!DNL Commerce] e inviati ad Experience Platform.

Personalizzazione dei dati ![[!DNL Data Connection]](./assets/epc-data-customization.png){width="700" zoomable="yes"}

>[!IMPORTANT]
>
>Assicurati che l&#39;ID dello stream di dati [specificato](#data-collection) nella scheda **Raccolta dati** corrisponda all&#39;ID collegato allo schema per l&#39;acquisizione degli attributi personalizzati.

Quando si creano attributi personalizzati per gli ordini e li si inviano a Experience Platform, i nomi degli attributi in Commerce devono corrispondere a quelli dello schema [!DNL Commerce] in Experience Platform. Se non corrispondono, può essere difficile identificare le differenze. Se i nomi non corrispondono, la tabella **Attributi ordine personalizzati** può aiutare a risolvere il problema.

La tabella **Attributi ordine personalizzati** fornisce visibilità sulla configurazione e sul mapping degli attributi ordine personalizzati tra il back office [!DNL Commerce] e lo schema [!DNL Commerce] in Experience Platform. Questa tabella consente di visualizzare gli attributi personalizzati del livello dell&#39;ordine e del livello dell&#39;articolo dell&#39;ordine in origini diverse, semplificando l&#39;identificazione degli attributi mancanti o non allineati. Inoltre, visualizza gli ID dei set di dati per distinguere tra set di dati live e storici, in quanto ciascuno può avere i propri attributi personalizzati.

Se nella tabella non viene visualizzato un segno di spunta verde accanto al nome di un attributo personalizzato, significa che non vi è corrispondenza tra i nomi degli attributi nelle origini. Correggere il nome dell&#39;attributo in un&#39;origine. Verrà visualizzato un segno di spunta verde per indicare che i nomi ora corrispondono.

- Se il nome dell&#39;attributo viene aggiornato nello schema in Experience Platform, è necessario salvare la configurazione nella scheda **Personalizzazione dati** per attivare la modifica dello schema di Experience Platform. Questa modifica verrà applicata alla tabella **Attributi ordine personalizzati** quando si fa clic sul pulsante **[!UICONTROL Refresh]**.
- Se il nome dell&#39;attributo viene aggiornato in [!DNL Commerce], è necessario generare un evento ordine per aggiornare il nome nella tabella **Attributi ordine personalizzati**. La modifica si rifletterà in circa 60 minuti.

Ulteriori informazioni su come [impostare attributi personalizzati](custom-attributes.md).

#### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Set di dati | Visualizza i set di dati che contengono gli attributi personalizzati. I set di dati live e storici possono avere i propri attributi personalizzati. |
| Adobe Commerce | Visualizza tutti gli attributi personalizzati creati nel back office [!DNL Commerce]. |
| Experience Platform | Visualizza tutti gli attributi personalizzati specificati nello schema [!DNL Commerce] in Experience Platform. |
| Aggiorna | Recupera eventuali nomi di attributi personalizzati dallo schema [!DNL Commerce] in Experience Platform. |

## Conferma la raccolta dei dati dell’evento

Per verificare che i dati vengano raccolti dall&#39;archivio Commerce, utilizzare [Adobe Experience Platform debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=it) per esaminare il sito Commerce. Dopo aver confermato che i dati vengono raccolti, è possibile verificare che i dati dell&#39;evento storefront e back office vengano visualizzati nel perimetro eseguendo una query che restituisce i dati dal [set di dati creato](overview.md#prerequisites).

1. Seleziona **Query** nella barra di navigazione a sinistra di Experience Platform e fai clic su [!UICONTROL Create Query].

   ![Editor query](assets/query-editor.png)

1. All’apertura dell’editor delle query, immetti una query che selezioni i dati dal set di dati.

   ![Crea query](assets/create-query.png)

   Ad esempio, la query potrebbe essere simile alla seguente:

   ```sql
   SELECT * from `your_dataset_name` ORDER by TIMESTAMP DESC
   ```

1. Dopo l&#39;esecuzione della query, i risultati vengono visualizzati nella scheda **Risultati**, accanto alla scheda **Console**. Questa vista mostra l’output tabulare della query.

   ![Editor query](assets/query-results.png)

In questo esempio vengono visualizzati i dati evento di [`commerce.productListAdds`](events.md#addtocart), [`commerce.productViews`](events.md#productpageview), [`web.webpagedetails.pageViews`](events.md#pageview) e così via. Questa vista ti consente di verificare che i dati Commerce siano arrivati al server Edge di.

Se i risultati non sono quelli previsti, apri il set di dati e cerca eventuali importazioni batch non riuscite. Ulteriori informazioni su [risoluzione dei problemi relativi alle importazioni batch](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/troubleshooting.html?lang=it).

### Verifica che i dati del profilo vengano visualizzati in Experience Platform

Se non vengono visualizzati i dati del profilo in Experience Platform, consultare [Commerce KnowledgeBase](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported) per suggerimenti sulla risoluzione dei problemi.

## Passaggi successivi

Quando i dati di Commerce vengono inviati ad Experience Platform Edge, altri prodotti Adobe Experience Cloud, come Adobe Journey Optimizer, possono utilizzarli. Ad esempio, puoi configurare Journey Optimizer per l’ascolto di determinati eventi e, in base a tali dati, attivare un’e-mail per il primo utente o se viene abbandonato un carrello. Scopri come estendere la piattaforma Commerce [creando percorsi di clienti](using-ajo.md) in Journey Optimizer.
