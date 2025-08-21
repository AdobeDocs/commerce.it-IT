---
title: Introduzione a  [!DNL Live Search]
description: Scopri i requisiti di sistema e i passaggi di installazione per  [!DNL Live Search]  da Adobe Commerce.
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 7d5e3faeef2fb16779d1558027a0b76ff3fe3a38
workflow-type: tm+mt
source-wordcount: '3138'
ht-degree: 0%

---

# Configurazione per il successo con [!DNL Live Search]

Adobe Commerce [!DNL Live Search] e [[!DNL Catalog Service]](../catalog-service/guide-overview.md) collaborano per fornire una soluzione di ricerca efficiente, pertinente e intuitiva che consenta ai clienti di trovare rapidamente ciò di cui hanno bisogno. In particolare, [!DNL Catalog Service] fa emergere i dati del catalogo per i servizi SaaS, ad esempio [!DNL Live Search] da utilizzare.

Questo articolo fornisce istruzioni dettagliate per l&#39;implementazione di [!DNL Live Search] con [!DNL Catalog Service].

## Pubblico

Questo articolo è destinato agli sviluppatori o agli integratori di sistemi del team, responsabili dell’installazione e della configurazione dell’istanza di Adobe Commerce.

## Requisiti

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP 8.1, 8.2 o 8.3
- [!DNL Composer]
- Esecuzione di processi cron e indicizzatori

>[!IMPORTANT]
>
>Prima di implementare [!DNL Live Search], consulta la sezione [Limiti e limiti](boundaries-limits.md) per assicurarti che [!DNL Live Search] soddisfi le tue esigenze aziendali.

## Aggiornamenti importanti

- A partire dalla versione 3.0.2 di [!DNL Live Search], l&#39;estensione [!DNL Catalog Service] è inclusa nell&#39;installazione.

- A causa dell’annuncio sulla fine del supporto di Elasticsearch 7 relativo ad agosto 2023, Adobe consiglia a tutti i clienti di Adobe Commerce di migrare al motore di ricerca OpenSearch 2.x. Per informazioni sulla migrazione del motore di ricerca durante un aggiornamento del prodotto, vedere [Migrazione a OpenSearch](https://experienceleague.adobe.com/it/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration) nella _Guida all&#39;aggiornamento_.

## Piattaforme supportate

- Adobe Commerce on Cloud (ECE) : 2.4.4+
- Adobe Commerce on-prem (EE) : 2.4.4+

## Panoramica del flusso di lavoro

A un livello avanzato, l&#39;onboarding di [!DNL Live Search] richiede:

1. [Installa](#1-install-the-live-search-extension) l&#39;estensione [!DNL Live Search]
1. [Configurare](#2-configure-api-keys) le chiavi API
1. [Sincronizza](#3-sync-your-catalog-data) i dati del catalogo
1. [Verifica](#4-verify-that-the-data-was-exported) che i dati del catalogo siano stati esportati
1. [Configura](#5-configure-the-data) i dati
1. [Verifica](#6-test-the-connection) la connessione
1. [Verifica](#7-validate-events-are-capturing-data) che gli eventi acquisiscano i dati
1. [Personalizza](#8-customize-for-your-storefront) la vetrina

## &#x200B;1. Installare l&#39;estensione [!DNL Live Search]

[!DNL Live Search] è installato come estensione da [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html) a [Composer](https://getcomposer.org/). Dopo aver installato e configurato [!DNL Live Search], Adobe [!DNL Commerce] inizia a condividere i dati di ricerca e catalogo con i servizi SaaS. A questo punto, *Amministratore* utenti possono impostare, personalizzare e gestire facet di ricerca, sinonimi e regole di merchandising.

>[!BEGINTABS]

>[!TAB Nuova istanza di Commerce]

Segui queste istruzioni se stai installando [!DNL Live Search] in una nuova istanza di Commerce.

1. Verificare che [processi cron](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) e [indicizzatori](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/tools/index-management) siano in esecuzione.

1. Utilizza Composer per aggiungere il modulo Live Search al progetto:

   ```bash
   composer require magento/live-search --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Disattivare temporaneamente [!DNL OpenSearch] e i moduli correlati e installare [!DNL Live Search].

   ```bash
   bin/magento module:disable Magento_ Magento_Elasticsearch8 Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   [!DNL Elasticsearch] continua a gestire le richieste di ricerca dalla vetrina mentre il servizio [!DNL Live Search] sincronizza i dati del catalogo e indicizza i prodotti in background.

1. Installare gli aggiornamenti.

   ```bash
   bin/magento setup:upgrade
   ```

1. Verificare che i seguenti [indicizzatori](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/tools/index-management) siano impostati su &quot;Aggiorna in base alla pianificazione&quot;:

   - Feed prodotto
   - Feed variante prodotto
   - Feed attributi catalogo
   - Feed prezzi prodotto
   - Feed dati del sito Web ambiti
   - Feed di dati dei gruppi di clienti per ambiti
   - Feed categorie
   - Feed di autorizzazioni categoria

Dopo aver verificato gli indicizzatori, il passaggio successivo consiste nel [configurare le chiavi API](#2-configure-api-keys).

>[!TAB Istanza di Commerce esistente]

Seguire queste istruzioni se si sta installando [!DNL Live Search] in un&#39;istanza di Commerce esistente.

1. Verificare che [processi cron](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) e [indicizzatori](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/tools/index-management) siano in esecuzione.

1. Utilizza Composer per aggiungere il modulo Live Search al progetto:

   ```bash
   composer require magento/live-search --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Disabilita i moduli [!DNL Live Search] che forniscono i risultati della ricerca in vetrina.

   ```bash
   bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing
   ```

   [!DNL Elasticsearch] continua a gestire le richieste di ricerca dalla vetrina mentre il servizio [!DNL Live Search] sincronizza i dati del catalogo e indicizza i prodotti in background.

1. Installare gli aggiornamenti.

   ```bash
   bin/magento setup:upgrade
   ```

1. Verificare che i seguenti [indicizzatori](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/tools/index-management) siano impostati su &quot;Aggiorna in base alla pianificazione&quot;:

   - Feed prodotto
   - Feed variante prodotto
   - Feed attributi catalogo
   - Feed prezzi prodotto
   - Feed dati del sito Web ambiti
   - Feed di dati dei gruppi di clienti per ambiti
   - Feed categorie
   - Feed di autorizzazioni categoria

1. Abilitare l&#39;estensione [!DNL Live Search] e disabilitare [!DNL OpenSearch] (moduli Magento Elasticsearch e OpenSearch).

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing
   ```

   ```
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_Elasticsearch8 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   >[!NOTE]
   >
   >Il comando disable include l&#39;elenco dei moduli di Commerce che supportano OpenSearch. Se nell&#39;istanza di Commerce non è installato un modulo, verrà visualizzato un errore `module does not exist`.

1. Installare gli aggiornamenti.

   ```bash
   bin/magento setup:upgrade
   ```

Dopo aver verificato gli indicizzatori, il passaggio successivo consiste nel [configurare le chiavi API](#2-configure-api-keys).

>[!ENDTABS]

### Installa [!DNL Live Search] versione beta

>[!IMPORTANT]
>
>La seguente funzione è in versione beta. Per partecipare alla versione beta, invia una richiesta e-mail a [commerce-storefront-services](mailto:commerce-storefront-services@adobe.com).

Questa versione beta supporta tre nuove funzionalità nella query [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/):

- **Ricerca a livelli** - Ricerca in un altro contesto di ricerca - Con questa funzionalità è possibile eseguire fino a due livelli di ricerca per le query di ricerca. Ad esempio:

   - **Ricerca livello 1** - Ricerca &quot;motor&quot; in &quot;product_attribute_1
   - **Ricerca livello 2** - Cercare &quot;numero parte 123&quot; in &quot;product_attribute_2&quot;. In questo esempio viene cercata la voce &quot;part number 123&quot; all&#39;interno dei risultati per &quot;motor&quot;.

  La ricerca con livelli è disponibile sia per l&#39;indicizzazione di ricerca `startsWith` che per quella `contains` come descritto di seguito:

- **startsWith indicizzazione ricerca** - Effettua la ricerca utilizzando l&#39;indicizzazione `startsWith`. Questa nuova funzionalità consente di:

   - Ricerca di prodotti in cui il valore dell&#39;attributo inizia con una stringa specifica.
   - La configurazione di una ricerca &quot;termina con&quot; consente agli acquirenti di cercare prodotti in cui il valore dell’attributo termina con una stringa specifica. Per abilitare una ricerca &quot;termina con&quot;, l’attributo del prodotto deve essere acquisito in ordine inverso e la chiamata API deve essere anche una stringa inversa.

- **contiene l&#39;indicizzazione della ricerca** -Cercare un attributo utilizzando l&#39;indicizzazione contains. Questa nuova funzionalità consente di:

   - Ricerca di una query all&#39;interno di una stringa più grande. Ad esempio, se un acquirente cerca il numero di prodotto &quot;PE-123&quot; nella stringa &quot;HAPE-123&quot;.

     >[!NOTE]
     >
     >Questo tipo di ricerca è diverso dalla [ricerca frase](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase) esistente, che esegue una ricerca di completamento automatico. Ad esempio, se il valore dell’attributo del prodotto è &quot;pantaloni da esterni&quot;, la ricerca di una frase restituisce una risposta per &quot;out pan&quot;, ma non restituisce una risposta per &quot;o formiche&quot;. Una ricerca contiene, tuttavia, restituisce una risposta per &quot;o formiche&quot;.

Queste nuove condizioni migliorano il meccanismo di filtro delle query di ricerca per perfezionare i risultati della ricerca. Queste nuove condizioni non influiscono sulla query di ricerca principale.

Puoi implementare queste nuove condizioni nella pagina dei risultati della ricerca. Ad esempio, puoi aggiungere una nuova sezione nella pagina in cui l’acquirente può perfezionare ulteriormente i risultati della ricerca. È possibile consentire agli acquirenti di selezionare attributi di prodotto specifici, ad esempio &quot;Produttore&quot;, &quot;Numero parte&quot; e &quot;Descrizione&quot;. Da lì, eseguono ricerche all&#39;interno di tali attributi utilizzando le condizioni `contains` o `startsWith`. Per un elenco degli [attributi](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/attributes-input-types) ricercabili, consulta la Guida dell&#39;amministratore.

1. Per installare la versione beta, aggiungi la seguente dipendenza al progetto:

   ```bash
   composer require magento/module-live-search-search-types:"^1.0.0-beta1"
   ```

1. Eseguire il commit e inviare le modifiche ai file `composer.json` e `composer.lock` al progetto cloud. [Ulteriori informazioni](https://experienceleague.adobe.com/it/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension).

   Questa versione beta aggiunge **[!UICONTROL Search types]** caselle di controllo per **[!UICONTROL Autocomplete]**, **[!UICONTROL Contains]** e **[!UICONTROL Starts with]** nell&#39;amministratore. Aggiorna inoltre l&#39;API GraphQL [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) per includere queste nuove funzionalità di ricerca.

1. Nell&#39;amministratore, [imposta un attributo di prodotto](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) in modo che sia possibile eseguire ricerche e specifica la funzionalità di ricerca per tale attributo, ad esempio **Contains** (impostazione predefinita) o **Starts with**. È possibile specificare un massimo di sei attributi da abilitare per **Contains** e sei attributi da abilitare per **Starts with**. Per la versione beta, tieni presente che l’amministratore non applica questa restrizione, ma che la applica nelle ricerche API.

   ![Specificare la funzionalità di ricerca](./assets/search-filters-admin.png)

1. Consulta la [documentazione per sviluppatori](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) per scoprire come aggiornare le chiamate API di [!DNL Live Search] utilizzando le nuove funzionalità di ricerca di `contains` e `startsWith`.

### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| `Autocomplete` | È attivata per impostazione predefinita e non può essere modificata. Con `Autocomplete`, puoi utilizzare `contains` nel [filtro di ricerca](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering). In questo caso, la query di ricerca in `contains` restituisce una risposta di ricerca di tipo completamento automatico. Adobe consiglia di utilizzare questo tipo di ricerca per i campi di descrizione, che in genere contengono più di 50 caratteri. |
| `Contains` | Abilita una ricerca vera e propria di tipo &quot;testo contenuto in una stringa&quot; invece di una ricerca di completamento automatico. Utilizza `contains` nel [filtro di ricerca](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability). Per ulteriori informazioni, consulta le [limitazioni](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations). |
| `Starts with` | Eseguire query sulle stringhe che iniziano con un determinato valore. Utilizza `startsWith` nel [filtro di ricerca](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability). |

## &#x200B;2. Configurare le chiavi API

Per connettere [!DNL Live Search] a un&#39;installazione di Adobe Commerce sono necessari la chiave API di Adobe Commerce e la chiave privata associata. La chiave API viene generata e mantenuta nell&#39;account del titolare della licenza [!DNL Commerce], che può condividerla con lo sviluppatore o l&#39;integratore di sistemi. Lo sviluppatore può quindi creare e gestire gli spazi dati SaaS per conto del titolare della licenza. Se disponi già di un set di chiavi API, non è necessario rigenerarle.

Scopri come configurare le chiavi API nell’articolo [Commerce Services Connector](../landing/saas.md).

## &#x200B;3. Sincronizzare i dati del catalogo

[!DNL Live Search] sposta i dati del catalogo nell&#39;infrastruttura SaaS di Adobe. I dati vengono indicizzati e i risultati della ricerca vengono consegnati da questo indice direttamente alla vetrina. A seconda delle dimensioni e della complessità, l’indicizzazione può richiedere da 30 minuti a un paio d’ore.

Per avviare la sincronizzazione iniziale dei dati del catalogo con i servizi SaaS, eseguire i comandi seguenti nell&#39;ordine indicato:

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

Quando si eseguono questi comandi, inizia la sincronizzazione iniziale dei dati del catalogo con i servizi SaaS.

>[!WARNING]
>
>Le operazioni di ricerca e di ricerca delle categorie non sono disponibili durante la sincronizzazione. Il processo può richiedere più di 1 ora a seconda della dimensione del catalogo.

### Monitorare l’avanzamento della sincronizzazione

Utilizza [Dashboard di gestione dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-dashboard) per monitorare lo stato di avanzamento della sincronizzazione. Questa dashboard fornisce informazioni utili sulla disponibilità di dati di prodotto nella vetrina, garantendo che possano essere visualizzati tempestivamente ai clienti.

![Dashboard di gestione dati](assets/data-management-dashboard.png)

È inoltre possibile eseguire i comandi di sincronizzazione e risolvere i problemi relativi al processo di sincronizzazione utilizzando [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) e i registri delle estensioni di esportazione dei dati.

#### Aggiornamenti futuri del prodotto

Dopo la sincronizzazione iniziale, possono essere necessari fino a 15 minuti perché gli aggiornamenti incrementali dei prodotti siano disponibili per la ricerca nella vetrina. Per ulteriori informazioni, consulta [Aggiornamenti dei prodotti in streaming](indexing.md) nella documentazione di indicizzazione.

## &#x200B;4. Verificare che i dati siano stati esportati

Per verificare se i dati del catalogo sono stati esportati da Adobe Commerce e sincronizzati con [!DNL Live Search], sono disponibili alcune opzioni:

- Cercare le voci nelle tabelle seguenti:

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >Se si verifica un errore `table does not exist`, cercare le voci nelle tabelle `catalog_data_exporter_products` e `catalog_data_exporter_product_attributes`. Questi nomi di tabella vengono utilizzati in [!DNL Live Search] versioni precedenti alla 4.2.1.

- Utilizza il [parco giochi GraphQL](https://experienceleague.adobe.com/it/docs/commerce/live-search/live-search-admin/graphql) con la query predefinita (consulta [riferimento GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) per ulteriori dettagli) per verificare quanto segue:

   - Il conteggio dei prodotti restituito si avvicina a quello previsto per la visualizzazione Store.
   - Vengono restituiti i facet.

Per ulteriori informazioni, vedere [[!DNL Live Search] catalogo non sincronizzato](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) nella Knowledge Base del supporto tecnico.

## &#x200B;5. Configurare i dati

La corretta configurazione dei dati di prodotto garantisce buoni risultati di ricerca per i clienti. In questa sezione, abiliti i widget per l’elenco dei prodotti e assegna le categorie.

### Abilita widget elenco prodotti

Quando si installa [!DNL Live Search] 4.0.0+, i widget dell&#39;elenco prodotti sono attivati per impostazione predefinita. Quando i widget sono attivati, viene utilizzato un componente diverso dell’interfaccia utente per i risultati della ricerca e per le pagine dell’elenco di prodotti per la navigazione delle categorie. Questo componente dell&#39;interfaccia utente effettua chiamate dirette all&#39;[API Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/), il che si traduce in tempi di risposta più rapidi.

Se la versione di [!DNL Live Search] è precedente alla 4.0.0+, è necessario abilitare manualmente il widget Elenco prodotti.

1. Da *Amministratore*, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. In **[!UICONTROL Live Search]**, selezionare **[!UICONTROL Storefront Features]**.
1. Imposta **[!UICONTROL Enable Product Listing Widgets]** su `Yes`.

   ![Abilita widget elenco prodotti](assets/ls-admin-enable-widget.png)

Quando si modifica questa configurazione, viene visualizzato il messaggio `Page cache is invalidated`. Per salvare le modifiche, è necessario svuotare la cache di Magento.

1. Accedere alla pagina [Gestione cache](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/tools/cache-management) effettuando una delle operazioni seguenti:

   - Fare clic sul collegamento **[!UICONTROL Cache Management]** nel messaggio sopra l&#39;area di lavoro.
   - Nella barra laterale _Admin_, passa a **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Cache Management]**.

1. Selezionare la **configurazione** [!UICONTROL Cache Type] e fare clic su **[!UICONTROL Flush Magento Cache]**.

   Le modifiche alla vetrina vengono apportate subito dopo il flushing della cache.

### Assegna categorie

I prodotti restituiti in [!DNL Live Search] devono essere assegnati a una [categoria](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/categories/categories). In Luma, ad esempio, i prodotti sono inseriti in categorie come &quot;Uomini&quot;, &quot;Donne&quot; e &quot;Attrezzi&quot;. Sono impostate anche delle sottocategorie per &quot;Tops&quot;, &quot;Bottoms&quot; e &quot;Watches&quot;. Queste assegnazioni di categoria migliorano la granularità quando si filtrano.

## &#x200B;6. Verificare la connessione

Con i dati del catalogo ora in SaaS, verifica che i dati del prodotto vengano restituiti nei seguenti scenari:

- La casella [!UICONTROL Search] restituisce correttamente i risultati
- La ricerca delle categorie restituisce correttamente i risultati
- I facet sono disponibili come filtri nelle pagine dei risultati di ricerca

Se tutto funziona correttamente, [!DNL Live Search] è installato, connesso e pronto all&#39;uso.

Se si verificano problemi nella vetrina, controllare il file `var/log/system.log` per individuare eventuali errori o errori di comunicazione API sul lato servizi.

Per consentire a [!DNL Live Search] di attraversare un firewall, aggiungere `commerce.adobe.io` al inserisco nell&#39;elenco Consentiti di.

## &#x200B;7. Verificare che gli eventi acquisiscano i dati

Assicurati che gli eventi storefront distribuiti sul tuo sito funzionino. Questo controllo è particolarmente importante per le implementazioni headless.

- Rivedi gli [eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search) necessari per [!DNL Live Search].
- Assicurati che il [dashboard di Live Search](performance.md) visualizzi i dati dagli ambienti non di produzione.
- [Verifica raccolta eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/).

## &#x200B;8. Personalizza per la vetrina

Hai installato l&#39;estensione [!DNL Live Search], hai sincronizzato, convalidato e configurato i tuoi dati. Il passaggio successivo consiste nel verificare che i widget [!DNL Live Search] siano conformi all&#39;aspetto del tuo Negozio.

Puoi assegnare uno stile ai widget popover e PLP definendo regole CSS personalizzate in base alle esigenze. Consulta [Elementi Popover di stile](storefront-popover.md#styling-popover-example) e [widget pagina elenco prodotti](plp-styling.md#styling-example).

Se desideri estendere la funzionalità dei widget, il codice sorgente per ciascuno di essi è disponibile in un repository pubblico.
In questo scenario, puoi personalizzare il JavaScript in base alle tue esigenze e quindi ospitare il codice personalizzato sulla CDN. Questo script personalizzato comunica con il servizio [!DNL Live Search] e restituisce i risultati come normale, consentendo di controllare la funzionalità del widget.

- [Archivio widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Archivio della barra di ricerca](https://github.com/adobe/storefront-search-as-you-type)

## Aggiornamento di [!DNL Live Search]

Prima di aggiornare [!DNL Live Search], controllare la versione di [!DNL Live Search] installata tramite Composer.

```bash
composer show magento/module-live-search | grep version
```

Per aggiornare [!DNL Live Search], eseguire quanto segue dalla riga di comando:

```bash
composer update magento/live-search --with-dependencies
```

Per eseguire l&#39;aggiornamento a una versione principale, ad esempio da 3.1.1 a 4.0.0, modificare il file [!DNL Composer] principale del progetto come segue:`.json`

1. Se la versione di `magento/live-search` attualmente installata è `3.1.1` o inferiore e si sta eseguendo l&#39;aggiornamento alla versione `4.0.0` o successiva, eseguire il comando seguente prima dell&#39;aggiornamento:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   Per informazioni sulla versione di `magento/live-search` attualmente installata, eseguire il comando seguente:

   ```bash
   composer show magento/live-search
   ```

1. Aprire il file radice `composer.json` e cercare `magento/live-search`.

1. Nella sezione `require`, aggiornare il numero di versione come segue:

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. Salva `composer.json`. Quindi, esegui quanto segue dalla riga di comando:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## Disinstallazione di [!DNL Live Search]

Per disinstallare [!DNL Live Search], fare riferimento a [Moduli di disinstallazione](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/tutorials/uninstall-modules).

## [!DNL Live Search] pacchetti

L&#39;estensione [!DNL Live Search] è costituita dai pacchetti seguenti:

| Pacchetto | Descrizione |
|--- |--- |
| `module-live-search` | Consente ai commercianti di configurare le impostazioni di ricerca per faceting, sinonimi, regole di query e così via e fornisce l&#39;accesso a un&#39;area di riproduzione GraphQL di sola lettura per testare le query di *Admin*. |
| `module-live-search-adapter` | Indirizza le richieste di ricerca dalla vetrina al servizio [!DNL Live Search] ed esegue il rendering dei risultati nella vetrina. <br />- Sfoglia categorie - Indirizza le richieste dalla [navigazione superiore](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/catalog/navigation/navigation-top) della vetrina al servizio di ricerca.<br />- Ricerca globale - Indirizza le richieste dal campo [Ricerca rapida](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/catalog/search/search) al servizio [!DNL Live Search]. Il campo di ricerca rapida si trova nell’angolo superiore destro della pagina della vetrina. |
| `module-live-search-storefront-popover` | Un popover &quot;search as you type&quot; (cerca durante la digitazione) sostituisce la ricerca rapida standard e restituisce dati e miniature dei risultati di ricerca principali. |

## [!DNL Live Search] dipendenze

Il metapackage [!DNL Composer] per installare l&#39;estensione [!DNL Live Search] include le dipendenze del modulo seguenti.

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## Concetti avanzati

Nelle sezioni seguenti vengono forniti argomenti più avanzati quando si utilizzano [!DNL Live Search] e [!DNL Catalog Service].

### Endpoint

[!DNL Live Search] comunica attraverso l&#39;endpoint in `https://catalog-service.adobe.io/graphql`.

Poiché [!DNL Live Search] non ha accesso al database completo dei prodotti, le API principali di GraphQL e Commerce GraphQL per [!DNL Live Search] non dispongono della parità completa.

Adobe consiglia di chiamare direttamente le API SaaS, in particolare l’endpoint Catalog Service.

- Migliorare le prestazioni e ridurre il carico del processore ignorando il database Commerce/processo Graphql
- Sfruttare la federazione [!DNL Catalog Service] per chiamare [!DNL Live Search], [!DNL Catalog Service] e [!DNL Product Recommendations] da un singolo endpoint.

Per alcuni casi d&#39;uso, potrebbe essere meglio chiamare [!DNL Catalog Service] per i dettagli del prodotto e casi simili. Per ulteriori informazioni, vedere [refineProduct](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/).

Se hai un&#39;implementazione headless personalizzata, vedi le [!DNL Live Search] implementazioni di riferimento:

- [widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [[!DNL Live Search] campo](https://github.com/adobe/storefront-search-as-you-type)

La raccolta automatica dei dati di interazione dell’utente non funziona per impostazione predefinita se non si utilizzano i componenti standard come Search Adapter, widget Luma o widget CIF di AEM. Adobe Sensei utilizza i dati raccolti per il merchandising intelligente e il tracciamento delle prestazioni. Per risolvere questo problema, devi sviluppare una soluzione personalizzata per implementare questa raccolta dati in modo headless.

La versione più recente di [!DNL Live Search] utilizza già [!DNL Catalog Service].

### Supporto linguistico

[!DNL Live Search] widget supportano le seguenti lingue:

|  |  |  |  |
|--- |--- |--- |--- |
| Lingua | Regione | Codice lingua | Impostazioni locali Magento |
| Bulgaro | Bulgaria | bg_BG | bg_BG |
| Catalano | Spagna | ca_ES | ca_ES |
| Ceco | Repubblica Ceca | cs_CZ | cs_CZ |
| Danese | Danimarca | da_DK | da_DK |
| Tedesco | Germania | de_DE | de_DE |
| Greco | Grecia | el_GR | el_GR |
| Inglese | Regno Unito | en_GB | en_GB |
| Inglese | Stati Uniti | en_US | en_US |
| Spagnolo | Spagna | es_ES | es_ES |
| Estone | Estonia | et_EE | et_EE |
| Basco | Spagna | eu_ES | eu_ES |
| Persiano | Iran | fa_IR | fa_IR |
| Finlandese | Finlandia | fi_FI | fi_FI |
| Francese | Francia | fr_FR | fr_FR |
| Galiziano | Spagna | gl_ES | gl_ES |
| Hindi | India | hi_IN | hi_IN |
| Ungherese | Ungheria | hu_HU | hu_HU |
| Indonesiano | Indonesia | id_ID | id_ID |
| Italiano | Italia | it_IT | it_IT |
| Coreano | Corea del Sud | ko_KR | ko_KR |
| Lituano | Lituania | lt_LT | lt_LT |
| Lettone | Lettonia | lv_LV | lv_LV |
| Norvegese | Norvegia Bokmal | nb_NO | nb_NO |
| Olandese | Paesi Bassi | nl_NL | nl_NL |
| Polacco | Polonia | pl_PL | pl_PL |
| Portoghese | Brasile | pt_BR | pt_BR |
| Portoghese | Portogallo | pt_PT | pt_PT |
| Rumeno | Romania | ro_RO | ro_RO |
| Russo | Russia | ru_RU | ru_RU |
| Svedese | Svezia | sv_SE | sv_SE |
| Thailandese | Thailandia | th_TH | th_TH |
| Turco | Turchia | tr_TR | tr_TR |
| Cinese | Cina | zh_CN | zh_Hans_CN |
| Cinese | Taiwan | zh_TW | zh_Hant_TW |

Se il widget rileva che l’impostazione della lingua di amministrazione di Commerce corrisponde a una lingua supportata, per impostazione predefinita viene utilizzata tale lingua. In caso contrario, il widget viene impostato automaticamente su Inglese. In Amministrazione, l&#39;impostazione della lingua viene configurata passando a _[!UICONTROL Stores]_> [!UICONTROL Settings] >_[!UICONTROL Configuration]_ > _[!UICONTROL General]_> [!UICONTROL Country Options].

Gli amministratori possono inoltre impostare la lingua dell&#39;[indice di ricerca](settings.md#language) per garantire risultati di ricerca migliori.

### Archivio del codice widget

Il codice per il widget della pagina di elenco prodotti e il widget del campo [!DNL Live Search] è disponibile per il download da GitHub.

Gli sviluppatori che hanno accesso al codice possono personalizzare completamente il suo funzionamento e aspetto. Ospitano il codice sui propri server, ma utilizzano comunque il servizio [!DNL Live Search].

- [widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Barra di ricerca](https://github.com/adobe/storefront-search-as-you-type)

### Estensione Esportazione dati

Dopo l&#39;abilitazione di [!DNL Live Search], l&#39;estensione Esportazione dati sincronizza i dati Commerce tra l&#39;applicazione Commerce e [!DNL Live Search]. In questo modo i dati Commerce più aggiornati saranno disponibili nella vetrina. In Admin (Ammin), puoi controllare lo stato di sincronizzazione utilizzando il dashboard Data Management (Gestione dati). È possibile gestire e risolvere i problemi del processo di esportazione dei dati utilizzando CLI e registri di Commerce. Per ulteriori dettagli, vedere la [Guida all&#39;esportazione dei dati](../data-export/overview.md).

### Inventory management

[!DNL Live Search] supporta le funzionalità [Inventory management](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/introduction) in Commerce (precedentemente noto come Multi-Source Inventory o MSI). Per abilitare il supporto completo, è necessario [aggiornare](install.md#updating-live-search) il modulo di dipendenza `commerce-data-export` alla versione 102.2.0+.

[!DNL Live Search] restituisce un valore booleano che indica se un prodotto è disponibile all&#39;interno di Inventory management, ma non contiene informazioni sull&#39;origine che contiene il titolo.

### Indicizzatore prezzi

I clienti [!DNL Live Search] possono utilizzare l&#39;[Indicizzatore prezzi SaaS](../price-index/price-indexing.md), che fornisce aggiornamenti più rapidi per la modifica del prezzo e tempi di sincronizzazione.

### Supporto del prezzo

I widget [!DNL Live Search] supportano la maggior parte dei tipi di prezzo supportati da Adobe Commerce, ma non tutti.

Attualmente sono sostenuti i prezzi di base. I prezzi avanzati non supportati sono:

- Costo
- Prezzo minimo annunciato

Esaminare [Mesh API](../catalog-service/mesh.md) per calcolare i prezzi più complessi.

Il formato del prezzo supporta l&#39;impostazione di configurazione delle impostazioni locali nell&#39;istanza di Commerce: *Archivi* > Impostazioni > *Configurazione* > Generale > *Generale* > Opzioni locali > Impostazioni internazionali.

### Supporto per vetrina headless

Facoltativamente, potrebbe essere necessario installare il modulo `module-data-services-graphql` che espande la copertura GraphQL esistente dell&#39;applicazione per includere i campi necessari per la raccolta dei dati comportamentali della vetrina.

```bash
composer require magento/module-data-services-graphql
```

Questo modulo aggiunge contesti aggiuntivi alle query GraphQL:

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### Supporto B2B

[!DNL Live Search] supporta la funzionalità [B2B](https://experienceleague.adobe.com/it/docs/commerce-admin/b2b/guide-overview) con ulteriori [limitazioni](boundaries-limits.md#b2b-and-category-permissions).

### Supporto PWA

[!DNL Live Search] funziona con PWA Studio, ma gli utenti potrebbero vedere lievi differenze rispetto ad altre implementazioni di Commerce. Le funzionalità di base, come la ricerca e la pagina di elenco dei prodotti, funzionano in Venia, ma alcune permutazioni di Graphql potrebbero non funzionare correttamente. Potrebbero esserci anche differenze di prestazioni.

- L&#39;implementazione PWA corrente di [!DNL Live Search] richiede più tempo di elaborazione per restituire i risultati della ricerca rispetto a [!DNL Live Search] con la vetrina nativa di Commerce.
- [!DNL Live Search] in PWA non supporta [gestione eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). Di conseguenza, la generazione di rapporti di ricerca e il merchandising intelligente non funzionano sui punti vendita di PWA.
- Quando si utilizza [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/), GraphQL non supporta il filtraggio diretto su `description`, `name`, `short_description`, ma questi campi possono essere restituiti con un filtro più generale.

Per utilizzare [!DNL Live Search] con PWA Studio, gli integratori devono anche:

1. Installa [livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
1. Impostare `environmentId` nell&#39;oggetto `storeDetails`.

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### Cookie

[!DNL Live Search] raccoglie i dati di interazione dell&#39;utente come parte della funzionalità di base e i cookie vengono utilizzati per memorizzare tali dati. Quando raccoglie informazioni sull’utente, quest’ultimo deve accettare di memorizzare i cookie. [!DNL Live Search] e [!DNL Product Recommendations] condividono il flusso di dati e quindi lo stesso meccanismo di cookie. Ulteriori informazioni sono disponibili in [Gestione delle restrizioni dei cookie](https://experienceleague.adobe.com/it/docs/commerce/product-recommendations/developer/setting-cookie).
