---
title: Note sulla versione di Adobe Commerce Optimizer
description: Informazioni sulla versione mensili per  [!DNL Adobe Commerce Optimizer], inclusi aggiornamenti all'API REST di acquisizione dati e all'API GraphQL per il recupero dei dati del catalogo della vetrina.
feature: Release Notes
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
TQID: https://experienceleague.adobe.com/apcpxN0AOniRcHDCa5MMAVWysxRO5mTcudXXXjET-Lo
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: f1c7779558406641972e9c690d0f508d46da3e0c
workflow-type: tm+mt
source-wordcount: 1328
ht-degree: 0%

---

# Note sulla versione

Le seguenti note sulla versione contengono aggiornamenti a [!DNL Adobe Commerce Optimizer], tra cui:

* Nuove funzionalità e miglioramenti a [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour).
* Aggiornamenti a [API REST per l&#39;acquisizione dei dati](https://developer.adobe.com/commerce/services/reference/rest/) e [API GraphQL per il recupero dei dati del catalogo vetrina](https://developer.adobe.com/commerce/services/reference/graphql/).

  {{aco-api-updates-and-dropins}}

## Giugno 2026

>[!BEGINSHADEBOX]

_24 giugno 2026_

<!-- v1.3 -->

![Nuovo](../assets/new.svg) **Nuovo campo `canEditQuantity`**—Aggiunto `canEditQuantity` a `ProductViewOptionValueProduct` in Catalog Service GraphQL. Espone l&#39;impostazione facoltativa della quantità **Definita dall&#39;utente** per le selezioni del bundle da Commerce Admin, in modo che i consumatori di vetrina possano determinare se la quantità di una selezione del bundle è modificabile.
<!--COMOPT-2050-->

### Ricerca semantica

[!DNL Adobe Commerce Optimizer] ora supporta **[la ricerca semantica]** nella scheda [**Ricerca avanzata**](./settings.md#advanced-search) in **[!UICONTROL Settings]**. La ricerca semantica utilizza l’intelligenza artificiale per far corrispondere i prodotti in base al significato e al contesto, insieme alla ricerca per parole chiave, riducendo le pagine di ricerca vuote per le query in linguaggio naturale. Per impostazione predefinita, questa opzione è abilitata per i cataloghi in inglese idonei. Facoltativamente, è possibile regolare **[!UICONTROL Semantic boost]**, **[!UICONTROL Similarity threshold]** e **[!UICONTROL Fuzzy search]** nella stessa scheda. Non sono richieste modifiche alla configurazione degli attributi o alla vetrina. [Ulteriori informazioni](./setup/semantic-search.md).

### Filtri per prezzi consigli (beta)

Le unità di raccomandazione del prodotto ora supportano [**filtri prezzo**](./merchandising/recommendations/filters.md#price) nel passaggio **[!UICONTROL Filter products]**. Includi o escludi i candidati utilizzando gli intervalli minimo e massimo di **static** o le regole di **dynamic** nella pagina dei dettagli del prodotto che confrontano i prodotti consigliati con il **prezzo calcolato finale** del prodotto attualmente visualizzato dal listino prezzi attivo della vetrina. Le regole di prezzo filtrano il set di candidati. Non riclassificano i prodotti. [Ulteriori informazioni](./merchandising/recommendations/filters.md#price).

{{aco-release}}

>[!ENDSHADEBOX]

## Maggio 2026

>[!BEGINSHADEBOX]

### Miglioramento intelligente della classificazione

[Le regole di merchandising](./merchandising/rules/add.md#intelligent-ranking-boost) per la ricerca, gli elenchi di prodotti predefiniti e le [pagine categoria](./merchandising/rules/add.md#rule-types) ora includono **[!UICONTROL Intelligent Ranking Boost]**. Puoi regolare il livello di influenza delle strategie come **Most viewed** o **Trending** sull&#39;ordine dei prodotti in base alla rilevanza testuale dei segnali di ricerca e comportamentali negli elenchi delle categorie. L&#39;anteprima della regola riflette l&#39;impostazione. L’incremento viene applicato al momento della query, pertanto non è necessaria una risincronizzazione del catalogo quando lo modifichi.

### Aggiornamenti API

_28 maggio 2026_

<!-- v1.2 -->

![Correzione](../assets/fix.svg) **Struttura di navigazione completa**. Le categorie discendenti con tag sono ora incluse correttamente nelle strutture `navigation` filtrate dalla famiglia quando nel percorso esiste un nodo intermedio senza tag. Questa correzione assicura che gli acquirenti vedano tutte le categorie pertinenti nella navigazione, semplificando la navigazione e l’individuazione degli articoli.
<!--DATA-7183-->

![Correzione](../assets/fix.svg) **Gestione slug vuota in `categoryTree` richieste**—È stato risolto un problema a causa del quale la query [`categoryTree`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) restituiva un errore interno del server quando l&#39;argomento `slugs` includeva una stringa vuota. I valori di slug vuoti vengono ora ignorati, pertanto gli storefront e le integrazioni continuano a risolvere i dati di categoria senza richieste non riuscite.
<!--DATA-7184-->

![Correzione](../assets/fix.svg) **`searchCategory`richieste restituiscono risultati alfabetizzati senza distinzione tra maiuscole e minuscole**. La query `searchCategory` ordina ora i risultati della ricerca in ordine alfabetico senza distinzione tra maiuscole e minuscole, garantendo un ordinamento coerente e prevedibile. Le categorie con prefissi più brevi vengono visualizzate per prime quando i nomi sono identici.
<!--COMOPT-2142-->

_4 maggio 2026_

<!--v1.53-->

**Visualizzazione valuta corretta**. I prezzi dei prodotti di vetrina ora visualizzano il codice valuta corretto (ad esempio, USD) per tutti i tipi di prodotto. In precedenza, alcuni prodotti mostravano `NONE` invece della valuta prevista, con conseguente perdita dei prezzi.

<!--DATA-7115-->

{{aco-release}}

>[!ENDSHADEBOX]

## Aprile 2026

**Data di rilascio**: 7 aprile 2026

>[!BEGINSHADEBOX]

### Regole del catalogo

[Regole categoria](./merchandising/rules/add.md) estendono le regole di merchandising in modo da poter indirizzare le categorie e controllare l&#39;ordine dei prodotti sulle pagine delle categorie con la stessa classificazione e le stesse azioni (pin, boost, bury) della ricerca.

### Filtro prezzo (beta)

I filtri per i consigli ora includono un [filtro per la fascia di prezzo](./merchandising/recommendations/filters.md#price) (minimo e massimo).

### Aggiornamenti API

_29 aprile 2026_

<!--v1.52 release-->

**Richiesta batch richieste**: l&#39;API GraphQL ora applica un massimo di 100 SKU per richiesta quando si recuperano i dati del catalogo. Vedi [limiti e limiti documentati](https://experienceleague.adobe.com/it/docs/commerce/optimizer/boundaries-limits#product-discovery).

<!--DATA-7156-->

_17 aprile 2026_

<!--v1.51 release-->

**Trova categorie per nome con GraphQL**. La nuova query [`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/) restituisce categorie corrispondenti con paginazione per storefront e integrazioni. Per i parametri e i campi di risposta, consulta il riferimento API. <!--COMOPT-1819-->

_7 aprile 2026_

<!--v1.50 release-->

**Ricerche di categorie più semplici**. La query [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) tratta `family` come facoltativo, in modo da poter risolvere le categorie tramite slug senza fornire una famiglia.

{{aco-release}}

>[!ENDSHADEBOX]

## Marzo 2026

Nessun rilascio di [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) questo mese. Consulta Aggiornamenti API di seguito.

>[!BEGINSHADEBOX]

### Aggiornamenti API

_24 marzo 2026_

I bundle dinamici ora restituiscono una fascia di prezzo calcolata. <!--DATA-7014-->

{{aco-release}}

>[!ENDSHADEBOX]

## Febbraio 2026

**Data di rilascio**: 19 febbraio 2026

>[!BEGINSHADEBOX]

### Vista catalogo per regole e consigli di merchandising

È ora possibile specificare una visualizzazione del catalogo quando si [creano unità di consigli](./merchandising/recommendations/create.md) o [regole di merchandising](./merchandising/rules/add.md).

### Aggiornamenti API

_19 febbraio 2026_

<!--v1.48-->

**Contenuto categoria più ricco per storefronts**. La query [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) restituisce ora descrizioni, immagini e metatag SEO in modo che gli storefront possano eseguire il rendering di pagine categoria più ricche.<!--DATA-6933-->

_12 febbraio 2026_

<!--v1.49-->

**Dati prodotto migliorati per categoria**. L&#39;API GraphQL aggiunge il tipo [`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"} per consentire di eseguire query e filtrare i prodotti per categoria con un numero inferiore di round trip.

{{aco-release}}

>[!ENDSHADEBOX]

## Gennaio 2026

Nessun rilascio di [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) questo mese. Consulta Aggiornamenti API di seguito.

>[!BEGINSHADEBOX]

### Aggiornamenti API

_19 gennaio 2026_

* **Le operazioni REST API** supportano categorie più ricche. [Categories API](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories). Accettano ora valori `metaTags`, `images` e `description` facoltativi oltre a `families`, in modo da poter fornire merchandising e dettagli SEO più completi per le categorie.

{{aco-release}}

>[!ENDSHADEBOX]

## Dicembre 2025

**Data di rilascio**: 10 dicembre 2025

>[!BEGINSHADEBOX]

### Opportunità

I venditori possono ora ottenere consigli basati sull&#39;intelligenza artificiale tramite [Adobe Sites Optimizer](./manage-results/opportunities.md) per rilevare i problemi del sito e suggerire correzioni delle prestazioni.

### Livelli del catalogo

I venditori possono ora utilizzare [livelli catalogo](./setup/catalog-layer.md) per sovrapporre i dati dei prodotti senza modificare il catalogo di origine, gestire la priorità dei livelli e utilizzare la correzione automatica di Adobe Sites Optimizer.

{{aco-release}}

>[!ENDSHADEBOX]

## Novembre 2025

Nessun rilascio di [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) questo mese. Consulta Aggiornamenti API di seguito.

>[!BEGINSHADEBOX]

### Aggiornamenti API

_21 novembre 2025_

**Sono state aggiornate le istruzioni di autenticazione per l&#39;acquisizione dei dati REST API**. Le istruzioni ora fanno riferimento ai token di accesso OAuth e agli ambiti delle credenziali Developer Console corretti per il servizio di acquisizione dati. Se gli ambiti delle credenziali sono obsoleti, rigenerali per mantenere l’accesso.

_3 novembre 2025_

<!-- v1.43 -->

**Contenuto di prodotto localizzato e con livelli in GraphQL**: è ora possibile distribuire contenuto di prodotto specifico per il canale e in base alle impostazioni locali da [!DNL Adobe Commerce Optimizer].

* Personalizzare il contenuto dei prodotti per segmento di clienti
* Applicare sostituzioni specifiche delle impostazioni internazionali senza duplicare i dati del catalogo di base
* Controllare le sostituzioni a livello di campo con le maschere di livello
* Utilizzare livelli di contenuto premium, stagionali e ottimizzati per dispositivi mobili

Nessuna modifica allo schema API GraphQL: i livelli vengono applicati tramite le intestazioni di query e richiesta `products` esistenti. Vedi [Livello catalogo](./setup/catalog-layer.md).

{{aco-release}}

>[!ENDSHADEBOX]

## Ottobre 2025

**Data di rilascio**: 14 ottobre 2025

>[!BEGINSHADEBOX]

### Connettore Commerce Salesforce Commerce Optimizer

[!DNL Commerce Optimizer Salesforce Commerce Connector] è un nuovo kit di avvio App Builder che sincronizza i dati del catalogo Salesforce B2C Commerce in [!DNL Commerce Optimizer].<!--COMOPT-536-->

**Per gli amministratori:**

* Le modifiche al catalogo di Salesforce (prodotti, prezzi, metadati, listini prezzi) vengono sincronizzate automaticamente con [!DNL Commerce Optimizer].
* Esegue all&#39;esterno di [!DNL Adobe Commerce] per un numero inferiore di punti di contatto di integrazione.
* Gli aggiornamenti pianificati mantengono aggiornati [!DNL Commerce Optimizer] dati per merchandising e consigli.

**Per sviluppatori:**

* Framework estensibile per l’acquisizione del catalogo Salesforce in SaaS Merchandising Services.
* Fai riferimento a implementazioni, documenti di progettazione ed esempi di codice per velocizzare le build e la risoluzione dei problemi.

### Ricerca con livelli

* **Ricerca con livelli (GA)**. La ricerca di prodotti ora supporta la corrispondenza `startsWith` e `contains`. Vedi [Tipi di ricerca con livelli ed espansi](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### Aggiornamenti API

* _17 ottobre 2025_

  **Aggiungi il supporto REST API per acquisire i livelli di prodotto**. Utilizza l&#39;API [Catalog Layer](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) per personalizzare e sostituire i dati di prodotto di base per contesti, impostazioni locali o requisiti aziendali specifici. Dopo aver creato i livelli, puoi applicarli e gestirli da [Adobe Commerce Optimizer Studio](./setup/catalog-layer.md).<!--DATA-6632-->

* _14 ottobre 2025_

  **Alberi delle categorie a livello di programmazione**: creazione, aggiornamento e gestione di alberi delle categorie per la navigazione e il raggruppamento tramite REST (globale o specifico per canale), su una scala fino a 10.000 alberi e 500 categorie per albero. Vedi [Categorie](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"} nel _Riferimento API REST per l&#39;acquisizione dei dati del catalogo_.<!--DCAT-2649-->

* _8 ottobre 2025_

  **Mappatura più chiara delle categorie per l&#39;acquisizione dei dati**. Le nuove linee guida illustrano il formato del tag di categoria e le regole gerarchiche e specificano che i valori del prodotto `routes.path` devono corrispondere a un tag di categoria esistente (ad esempio, `men/clothing`).

{{aco-release}}

>[!ENDSHADEBOX]

## Settembre 2025

Nessun rilascio di [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) questo mese. Consulta Aggiornamenti API di seguito.

>[!BEGINSHADEBOX]

### Aggiornamenti API

_23 settembre 2025_

* **Gestione delle categorie tramite l&#39;API REST**. Utilizzare l&#39;API [Categories](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) per creare e gestire le categorie. Le categorie organizzano i prodotti in gruppi logici e supportano gerarchie nidificate tramite percorsi basati su tag. Dopo aver assegnato le categorie ai prodotti, recuperarle con le query GraphQL `[navigation](https://developer.adobe.com/commerce/services/reference/graphql/#navigation)` e `[categoryTree](https://developer.adobe.com/commerce/services/reference/graphql/#categorytree)` per eseguire il rendering dei menu della vetrina e delle strutture delle categorie.<!--DCAT-2626-->

{{aco-release}}

>[!ENDSHADEBOX]

## Agosto 2025

**Data di rilascio**: 28 agosto 2025

>[!BEGINSHADEBOX]

### Area geografica UE ora disponibile

L’area di produzione UE (**eu1**) è disponibile per le organizzazioni IMS. Quando [aggiungi un&#39;istanza  [!DNL Commerce Optimizer] &#x200B;](./get-started.md#step-1-create-an-instance) in Cloud Manager, scegli **[!UICONTROL European Union]** come **[!UICONTROL Region]** (solo produzione).

Gli URL di produzione di base per la regione dell’Unione Europea sono:

* Amministratore: `https://eu1.admin.commerce.adobe.com`
* REST e GraphQL: `https://eu1.api.commerce.adobe.com`

![Finestra di dialogo per la creazione di un&#39;istanza di Cloud Manager con il campo Regione](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]
