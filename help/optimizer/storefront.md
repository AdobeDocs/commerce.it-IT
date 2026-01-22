---
title: Configurare la vetrina
description: Scopri come configurare la vetrina  [!DNL Adobe Commerce Optimizer] .
role: Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# Configurare la vetrina

Questa guida illustra come configurare una vetrina per l&#39;istanza [!DNL Adobe Commerce Optimizer] tramite Adobe Edge Delivery Services. La vetrina include codice standard, contenuti di esempio e supporto per le pagine dei dettagli del prodotto e l’individuazione del prodotto (ricerca e filtro).

**Tempo stimato per il completamento:** 30-45 minuti

## Prerequisiti

* **Account GitHub** che può creare archivi ed è configurato per lo sviluppo locale (github.com)
* **[!DNL Adobe Commerce Optimizer]istanza** con dati di esempio e viste e criteri di catalogo configurati
   * Per istruzioni sull&#39;installazione, vedere [Aggiungere dati di esempio](get-started.md#add-sample-data).

### Dati istanza richiesti

Prima di iniziare, raccogliere le seguenti informazioni dall&#39;istanza [!DNL Adobe Commerce Optimizer]:

* **ID tenant** (chiamato anche ID istanza)
   * Disponibile dalla [pagina dei dettagli dell&#39;istanza](get-started.md#manage-instances)
* **Endpoint GraphQL** per l&#39;istanza
   * Disponibile dalla [pagina dei dettagli dell&#39;istanza](get-started.md#manage-instances)
* **ID visualizzazione catalogo** per la visualizzazione catalogo globale
   * Disponibile dalla [pagina dettagli catalogo](./setup/catalog-view.md#manage-catalog-view)
* **Impostazioni locali di Source** per la visualizzazione del catalogo
   * Il valore predefinito per i dati di esempio è `en-US`

>[!NOTE]
>
>I clienti con accesso di prova possono trovare l’endpoint GraphQL nell’e-mail di benvenuto ricevuta al momento della creazione dell’istanza. Le istanze di prova sono preconfigurate con dati di esempio, visualizzazioni di catalogo e criteri.

## Passaggi di configurazione

1. **[Crea il progetto vetrina](#create-your-storefront-project)**-Utilizza lo strumento [Site Creator](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) per creare un nuovo progetto vetrina con codice standard, contenuto di esempio e un file di configurazione.

1. **[Personalizzare la configurazione della vetrina](#customize-the-storefront-configuration)**-Aggiornare il file `config.json` nel repository per connettersi all&#39;istanza [!DNL Adobe Commerce Optimizer].

1. **[Verifica la configurazione](#verify-your-setup)** (10 minuti)
   * Anteprima del sito vetrina
   * Verificare le pagine dei dettagli del prodotto e la funzionalità di ricerca

## Crea il progetto storefront

Lo strumento Site Creator (Creazione sito) crea un progetto completo di vetrina con i seguenti componenti:

* **Sito**: pagina di destinazione della vetrina con contenuto standard
* **Codice**: archivio con file di origine standard
* **Contenuto**: ambiente di authoring dei documenti con file di contenuto del sito
* **Configurazione Commerce**: file `config.json` per la configurazione specifica dell&#39;istanza

### Passaggio 1: generare il progetto

1. Apri lo strumento [Creatore sito](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. Selezionare **Crea nuovo sito (codice e contenuto)**.

1. Completa la configurazione del sito:

   * **Organizzazione/nome utente GitHub**: immetti il nome utente o il nome dell&#39;organizzazione GitHub
   * **Nome sito**: scegli un nome descrittivo per la vetrina
   * **Endpoint Commerce GraphQL (facoltativo)**: immettere l&#39;endpoint GraphQL per l&#39;istanza [!DNL Adobe Commerce Optimizer]

1. Fai clic su **Crea sito** per creare l&#39;archivio GitHub con il codice boilerplate della vetrina.

   Quando l’archivio viene creato, Site Creator si aggiorna e richiede di installare l’app Code Sync.

### Passaggio 2: installare l’app Code Sync

1. Fare clic su **[!UICONTROL Install AEM Code Sync App]** per aprire il programma di installazione di Sincronizzazione codice in una nuova scheda.

1. Configura l&#39;app di sincronizzazione codice:
   * Seleziona la tua organizzazione GitHub, quindi fai clic su **[!UICONTROL Configure]**.
   * Nell&#39;interfaccia di Sincronizzazione codice fare clic su **[!UICONTROL Only select repositories]**.
   * Fare clic sul menu **[!UICONTROL Select repositories]**, quindi scegliere l&#39;archivio del codice storefront creato.
   * Fare clic su **[!UICONTROL Save]** per registrare l&#39;archivio.

1. Tornare alla finestra del browser in cui è aperto il creatore del sito e fare clic su **Crea sito**.

   Il creatore del sito copia il contenuto della vetrina nell’ambiente di authoring del documento. Questo processo richiede 1-2 minuti.

### Passaggio 3: salvare i collegamenti del progetto

1. Nella sezione Dettagli sito, controlla i collegamenti del progetto vetrina:

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   Utilizza questi collegamenti per gestire il codice, il contenuto e la configurazione della vetrina.

1. Copiare e salvare questi collegamenti per riferimento futuro: fare clic su **[!UICONTROL Copy].

## Configurare la vetrina

Aggiorna la configurazione della vetrina per connetterti all&#39;istanza [!DNL Adobe Commerce Optimizer].

1. Apri il file `config.json` nell&#39;archivio del codice standard.

   `https://github.com/<username or org>/<repo name>/config.json`

1. Individua la sezione `cs` (Catalog Service) nella configurazione.

1. Sostituisci i valori segnaposto con i valori della tua istanza. Consulta [Prerequisiti](#prerequisites).

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Source-Locale": "en-US",
      "AC-Price-Book-ID": "{priceBookId}"
   }
   ```

   >[!NOTE]
   >
   >Per trovare l&#39;ID del listino prezzi dedicato, controllare i [dettagli di configurazione della vista catalogo](./setup/catalog-view.md) in Adobe Commerce Optimizer per visualizzare i listini prezzi assegnati. Se non vengono assegnati listini prezzi, è possibile rimuovere questa intestazione dal file di configurazione. Aggiungerlo nuovamente quando un listino prezzi dedicato è stato assegnato alla vista catalogo.

1. Salva il file di configurazione.

   La propagazione delle modifiche alla configurazione potrebbe richiedere alcuni minuti. Se i dati non vengono visualizzati immediatamente, attendere 2-3 minuti prima della risoluzione dei problemi.

## Verifica la configurazione

Verificare che la vetrina sia connessa correttamente all&#39;istanza [!DNL Adobe Commerce Optimizer].

### Passaggio 1: visualizza la home page della vetrina

1. Passa all’URL dell’anteprima live:

   `https://main--{SITE}--{ORG}.aem.live`

   Sostituisci `{ORG}` e `{SITE}` con il nome dell&#39;organizzazione GitHub e del sito.

1. **Criteri di successo**: dovresti visualizzare la home page della vetrina con contenuti standard.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### Passaggio 2: verifica delle pagine dei dettagli del prodotto

Visualizza la pagina dei dettagli del prodotto predefinita per verificare che i dati del prodotto siano caricati correttamente.

1. Passa a una pagina di prodotto di esempio:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   Utilizza qualsiasi SKU presente nei dati di esempio, ad esempio:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   Per la vetrina predefinita, è possibile utilizzare il valore `placeholder` nella route per visualizzare il prodotto. Quando inizi a personalizzare la vetrina, puoi personalizzare il codice della vetrina per impostare il percorso della pagina dei dettagli del prodotto in base ai percorsi definiti nel catalogo.

   >[!TIP]
   >
   >Visualizza gli SKU disponibili dalla pagina [Sincronizzazione dati](./setup/data-sync.md) nella tua istanza di [!DNL Adobe Commerce Optimizer].

1. **Criteri di successo**: la pagina deve essere visualizzata:
   * Nome, descrizione e prezzo del prodotto
   * Immagini del prodotto
   * Funzionalità Aggiungi al carrello
   * Dati recuperati dall&#39;istanza [!DNL Adobe Commerce Optimizer]

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### Passaggio 3: verificare la funzionalità di ricerca predefinita

Verifica le funzioni predefinite del prodotto, incluse le funzioni di ricerca e filtro.

1. Nella home page della vetrina, fai clic sull’icona della lente di ingrandimento nell’intestazione.

1. Digitare la stringa di ricerca `tires` e premere **Invio**.

1. **Criteri di successo**: dovresti vedere:
   * Pagina dei risultati di ricerca con prodotti pneumatici
   * Opzioni di filtro nella barra laterale
   * Elenco prodotti con immagini e prezzi

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. Fare clic su un prodotto pneumatico per visualizzarne la pagina dei dettagli.

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## Risoluzione dei problemi

Se si verificano problemi durante l&#39;installazione, utilizzare la console del controllo pagina Web per verificare la presenza di errori. Prova anche a cancellare la cache del browser o a utilizzare un altro browser.

Per verificare i problemi comuni, attenersi alle istruzioni riportate di seguito.

### Problemi comuni

| Problema | Sintomi | Soluzione |
|-------|----------|----------|
| **L&#39;installazione della sincronizzazione codice non riesce** | Impossibile completare la configurazione di Sincronizzazione codice | <ul><li>Assicurati di avere accesso come amministratore all’organizzazione GitHub.</li><li>Prova a utilizzare un archivio personale invece di un’organizzazione.</li><li>Controlla le autorizzazioni GitHub e riprova.</li></ul> |
| **Impossibile caricare il sito** | 404 o errori di connessione | <ul><li>Verifica il formato URL del sito: `https://main--{SITE}--{ORG}.aem.live`</li><li>Controlla che l&#39;app di sincronizzazione codice sia installata correttamente.</li><li>Verifica che l’archivio sia pubblico o configurato correttamente.</li></ul> |
| **Nessun dato prodotto visualizzato** | Le pagine dei prodotti mostrano segnaposto o errori | <ul><li>Verifica i valori di configurazione in `config.json`</li><li>Nell&#39;istanza [!DNL Adobe Commerce Optimizer], controllare la pagina Sincronizzazione dati per verificare che i prodotti di esempio siano stati caricati. Se non sono disponibili prodotti, ricaricare i dati di esempio o aggiungere un prodotto utilizzando [Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request). Attendere alcuni minuti per la propagazione delle modifiche alla configurazione.</li><li>Prova a recuperare i dettagli del prodotto utilizzando la [query prodotti](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details) del servizio di merchandising utilizzando le stesse intestazioni configurate nel file `config.json`. Se è possibile recuperare i dati, è probabile che si tratti di un problema di configurazione della vista catalogo o di un errore di indice.</li></ul> |
| **La ricerca non restituisce alcun risultato** | Pagina risultati ricerca vuota | <ul><li>Verificare che sia possibile recuperare i risultati della ricerca prodotti utilizzando la query [productSearch](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search) di Merchandising Services utilizzando le stesse intestazioni configurate nel file `config.json`. Se è possibile recuperare i dati, è probabile che si tratti di un problema di configurazione della vista catalogo o di un errore di indice.</li><li>Verificare che l&#39;ID della vista catalogo nel file `config.json` corrisponda all&#39;ID della vista catalogo in [!DNL Adobe Commerce Optimizer].</li><li>In Adobe Commerce Optimizer, verifica la configurazione dei criteri, delle impostazioni locali e dei listini prezzi utilizzati nella configurazione dell’intestazione della vetrina.</li><li>Verificare che le [impostazioni dei metadati dell&#39;attributo](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata) siano impostate correttamente per la ricerca.</li></ul> |

### Elenco di controllo per la convalida

Prima di procedere con i passaggi successivi, assicurati che la vetrina funzioni correttamente verificando quanto segue:

![Elenco di controllo](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) I valori di configurazione corrispondono alle impostazioni dell&#39;istanza<br>
![La home page della vetrina](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) viene caricata senza errori<br>
![Elenco di controllo](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Almeno una pagina dei dettagli del prodotto visualizza informazioni complete<br>
![La funzionalità di ricerca](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) restituisce risultati rilevanti<br>
![Elenco di controllo](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Le immagini di prodotto sono state caricate correttamente<br>
![Elenco di controllo](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) I valori di configurazione corrispondono alle impostazioni dell&#39;istanza<br>

### Ottieni aiuto

Se i problemi persistono:

* Consulta la [documentazione di Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)
* Consulta la [Guida per gli sviluppatori di Adobe Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/)
* Visita le [risorse di supporto Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)

## Passaggi successivi

Dopo aver configurato e verificato la vetrina, puoi:

1. **[Installa l&#39;estensione del browser Sidekick](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#install-and-configure-sidekick)** per modificare, visualizzare in anteprima e pubblicare contenuti direttamente dal sito Web.

2. **[Imposta un ambiente di sviluppo locale](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment)**—Crea un ambiente locale per personalizzare il codice e il contenuto della vetrina.

### Scopri ed esplora

* **[Completa il caso d&#39;uso end-to-end](./use-case/admin-use-case.md)**. Ulteriori informazioni sulla configurazione della vetrina e sulla gestione del catalogo tramite [!DNL Adobe Commerce Optimizer].

* **[Esplora la personalizzazione della vetrina](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)**: scopri le opzioni di configurazione e configurazione avanzate.

* **[Usa i menu a discesa di Commerce per personalizzare l&#39;esperienza della vetrina](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/)**-Aggiungi componenti predefiniti per migliorare la tua esperienza della vetrina.

* **Esegui migrazione al servizio di configurazione Storefront**. Dopo aver creato la vetrina iniziale, puoi eseguire la migrazione della configurazione per utilizzare il servizio di configurazione che supporta casi di utilizzo avanzati, come la configurazione e le sovrapposizioni senza interruzioni. Per informazioni dettagliate, vedere la documentazione del [Servizio di configurazione](https://www.aem.live/docs/config-service-setup) in Adobe Experience Manager.

>[!MORELIKETHIS]
>
> Per ulteriori informazioni sull&#39;aggiornamento del contenuto del sito e sull&#39;integrazione con i componenti front-end e i dati back-end di Commerce, consulta la [documentazione di Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).
