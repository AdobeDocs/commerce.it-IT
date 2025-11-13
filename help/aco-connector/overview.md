---
title: Connettore Adobe Commerce Optimizer
description: Scopri come collegare i dati dal cloud Commerce o dal progetto on-premise a Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
hidefromtoc: true
hide: true
source-git-commit: 1654aede42cf53b2dffe2965680f122d7c247234
workflow-type: tm+mt
source-wordcount: '1529'
ht-degree: 0%

---


# Connettore Adobe Commerce Optimizer per Commerce

Il connettore Adobe Commerce è il ponte di integrazione che sincronizza i dati di catalogo e di prezzo tra un’implementazione Adobe Commerce Cloud on cloud o on-premise esistente e il modello dati di catalogo componibile di Adobe Commerce Optimizer. Ciò consente di abilitare funzioni come la ricerca dinamica basata su IA, raccomandazioni, vetrine headless a caricamento rapido, incluse le vetrine Adobe Commerce su Edge Delivery Services, e analisi delle prestazioni in tempo reale.

>[!NOTE]
>
>Questa documentazione descrive un prodotto in fase di sviluppo con accesso anticipato e non riflette tutte le funzionalità previste per la disponibilità generale.

## Architettura ed esperienza

Il connettore Adobe Commerce funziona mappando la gerarchia del catalogo `website/store/storeview` di Commerce al modello dati Adobe Commerce Optimizer `channel/policy/source`.

Invece di configurare e gestire i servizi Commerce (Live Search e Product Recommendations) dall&#39;amministratore Commerce, puoi utilizzare [gli strumenti di merchandising di Adobe Commerce Optimizer](../optimizer/merchandising/overview.md) per gestire l&#39;individuazione dei prodotti (Live Search) e la configurazione delle regole dei consigli (Product Recommendations).  L’istanza Adobe Commerce diventa l’origine dati per i dati di catalogo e prezzo. Quando i dati vengono aggiornati in Commerce, gli aggiornamenti vengono sincronizzati nell’istanza Adobe Commerce Optimizer.

## Flussi di lavoro

Il connettore consente diversi flussi di lavoro chiave:

* **Esporta i dati del catalogo Commerce in Adobe Commerce Optimizer**. I dati del listino prezzi e del listino prezzi vengono esportati al livello `website`. I dati degli attributi del prodotto e del prodotto vengono esportati al livello `store view`. Per impostazione predefinita, la sincronizzazione dei dati del catalogo è abilitata per tutti gli ambiti di Commerce (siti Web e visualizzazioni dello store).

  Per abilitare questo flusso di lavoro, utilizzare Composer per installare l&#39;estensione PHP `adobe-commerce/commerce-data-export-aco-adapter` e quindi fornire le credenziali IMS per autenticare la connessione tra il progetto Commerce.

* **Mappa i dati di Commerce `website/store/storeview` da esportare in Adobe Commerce Optimizer**

  È possibile personalizzare le impostazioni di esportazione di Adobe Commerce Optimizer per esportare i dati solo per ambiti specifici aggiornando la configurazione di esportazione dalla griglia dell&#39;archivio in Amministrazione (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* **Configurazione e gestione regole merchandising**

  Quando il connettore è abilitato, le regole di merchandising per l’individuazione dei prodotti e i consigli vengono definite e gestite dall’interfaccia utente di Adobe Commerce Optimizer, non dalle pagine [!UICONTROL Live Search] e [!UICONTROL Product Recommendations] nell’amministrazione di Commerce.

* **Distribuisci Commerce Storefront su Edge Delivery Services**

  Dopo aver configurato l’integrazione con Adobe Commerce Optimizer, puoi configurare e implementare uno store front Commerce sui servizi Edge Delivery per fornire prestazioni ultra veloci, scalabilità, authoring di contenuti fluido, personalizzazione integrata e costi operativi ridotti utilizzando l’architettura componibile basata su API e i componenti modulari disponibili con Adobe Commerce Optimizer.

## Requisiti per l’utilizzo dell’integrazione

* Adobe Commerce 2.4.7+

   * PHP 8.2, 8.3 o 8.4
   * Compositore 2.x

* Licenza Adobe Commerce Optimizer con un’istanza sandbox predisposta.

* Accedi a [repo.magento.com](https://repo.magento.com) per scaricare il metapacchetto del connettore Commerce tramite Composer.

* Accesso amministratore a un&#39;istanza sandbox [Adobe Commerce Optimizer](https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

L’utente di Adobe Commerce che configura l’integrazione deve disporre di:

* Accesso amministratore all’amministrazione di Adobe Commerce.

* [Accesso alla riga di comando al server applicazioni Adobe Commerce](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/project/user-access).

* Accesso per sviluppatori all&#39;organizzazione [IMS](https://experienceleague.adobe.com/it/docs/core-services/interface/administration/organizations?) in cui è stato eseguito il provisioning del progetto Adobe Commerce Optimizer.

## Introduzione

1. **Configura l&#39;integrazione**

   1. [Installare il pacchetto del connettore Commerce](#install-the-commerce-connector-package).

   1. [Ottieni i valori richiesti per la configurazione della connessione Commerce Optimizer](#get-required-values-for-configuring-the-commerce-optimizer-connection)

   1. [Abilitare l&#39;integrazione di Adobe Commerce Optimizer](#enable-the-adobe-commerce-optimizer-integration).

   1. [Verificare che la sincronizzazione dei dati funzioni](#verify-that-the-data-sync-is-working).

   1. [Personalizzare la configurazione di esportazione dei dati](#customize-commerce-data-export-configuration) (facoltativo).

1. **[Configura archivi Adobe Commerce Optimizer](#configure-adobe-commerce-optimizer-stores)**

1. **[Configura una vetrina Commerce in Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## Installare il pacchetto Commerce Connector

Il metapacchetto Adobe Commerce Connector Composer è disponibile per tutti i commercianti Commerce con una licenza attiva per Adobe Commerce Optimizer.

### Passaggi per l’installazione

1. Aggiungi il modulo `adobe-commerce/commerce-data-export-aco-adapter` tramite Compositore:

```shell
 composer require adobe-commerce/commerce-data-export-aco-adapter
```

1. Implementa le modifiche nell’ambiente di staging Adobe Commerce.

Dopo aver distribuito le modifiche, l’opzione Commerce Optimizer Optimizer è disponibile nel menu Amministrazione di Commerce.

>[!NOTE]
>
>Per istruzioni dettagliate sull’installazione dell’estensione, consulta le seguenti guide:
>
>[Installa estensione su Adobe Commerce su infrastruttura cloud](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Installa l&#39;estensione Adobe Commerce on-premise](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/tutorials/extensions)

## Ottieni i valori richiesti per la configurazione della connessione Commerce Optimizer

### Ottieni credenziali API

>[!NOTE]
>
>Se disponi già di un progetto per sviluppatori configurato con l’API di acquisizione dati nell’organizzazione IMS in cui è distribuita l’istanza di Commerce Optimizer, puoi ottenere le credenziali API e l’ID organizzazione richiesti dalle credenziali server-to-server OAUTH in tale progetto.

Crea un nuovo progetto per sviluppatori nella console Adobe Developer per ottenere le credenziali API di acquisizione Adobe Commerce Optimizer per configurare l’integrazione tra le istanze di Commerce e Commerce Optimizer. Per istruzioni, consulta [Ottenere le credenziali IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) nella *Guida per gli sviluppatori di merchandising*.

Dopo aver creato il progetto, salvare i valori seguenti dalla pagina delle credenziali server-to-server OAUTH:

* **ID organizzazione** (`org_id`)

* **IMS `client_id` e`client_secret`**

### Ottieni dettagli istanza Adobe Commerce Optimizer

Salva i seguenti valori dai dettagli dell’istanza di Adobe Commerce Optimizer.

* **Instance ID—**&#x200B;L&#39;identificatore univoco dell&#39;istanza Adobe Commerce Optimizer. Noto anche come ID tenant.

  Ottieni l’ID dell’istanza dall’URL per accedere all’istanza di Adobe Commerce Optimizer. Ad esempio, nell&#39;URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`, l&#39;ID istanza è `1234567890abcdef`.

* **Regione—**&#x200B;L’area in cui è ospitata l’istanza sandbox di Adobe Commerce Optimizer.

  Ottieni la regione dall’URL di Adobe Commerce Optimizer. Ad esempio, nell&#39;URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`, l&#39;area geografica è `na1`.

## Abilitare l’integrazione con Adobe Commerce Optimizer

>[!IMPORTANT]
>
>L&#39;elaborazione della sincronizzazione dati viene avviata quando si esegue il comando di configurazione. Per impostazione predefinita, la sincronizzazione dei dati del catalogo è abilitata per tutti gli ambiti di Commerce (siti Web e visualizzazioni dello store). A seconda delle dimensioni del catalogo, il processo di sincronizzazione dei dati può richiedere molte ore.

Utilizzando le credenziali API e i dettagli dell’istanza raccolti nei passaggi precedenti, ora puoi configurare l’integrazione tra le istanze Commerce e Adobe Commerce Optimizer.

1. Dall&#39;amministratore di Commerce, selezionare **[!UICONTROL Adobe Commerce Optimizer]** per visualizzare la pagina di configurazione con le istruzioni.

   ![Pagina di configurazione di Adobe Commerce Optimizer](../assets/aco-connector-config-page.png)

1. Dalla riga di comando, [utilizzare SSH](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/develop/secure-connections) per connettersi all&#39;ambiente di staging di Commerce.

1. Esegui il seguente comando Commerce CLI per configurare l’integrazione, sostituendo i valori segnaposto con i valori per il progetto Commerce Optimizer:

```terminal
bin/magento aco:config:init --org_id=<<your_org_id>> --tenant_id=<<your_tenant_id>> --client_id=<<your_client_id>> --client_secret=<<your_client_secret>> --region=<<na1>> --type=sandbox
```

1. Verificare la connessione tornando all&#39;amministratore di Commerce e selezionando l&#39;opzione [!UICONTROL Adobe Commerce Optimizer].

   Quando fai clic sull’opzione, viene aperta l’interfaccia utente di Adobe Commerce Optimizer in una nuova scheda.

## Verifica che la sincronizzazione dei dati funzioni

Puoi controllare la sincronizzazione dei dati sia dall’amministratore di Commerce che da Commerce Optimizer.

* La **[pagina Stato sincronizzazione feed dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.md)** mostra l&#39;avanzamento della sincronizzazione dei dati del catalogo da Commerce a Adobe Commerce Optimizer.

* La pagina **[[!UICONTROL Data Sync]](https://experienceleague.adobe.com/it/docs/commerce/optimizer/setup/data-sync)** in Adobe Commerce Optimizer mostra i dati del catalogo trasferiti dall&#39;istanza Commerce.

1. Verifica che i dati del catalogo scorrano da Commerce a Commerce Optimizer:

   Dall&#39;amministratore di Commerce, aprire la pagina [!UICONTROL Data Feed Sync Status] selezionando [!UICONTROL System] **&#x200B; > [!UICONTROL Data Transfer] > &#x200B;** [!UICONTROL Data Feed Sync Status]**.

   ![Pagina Stato sincronizzazione feed dati con report sullo stato degli elementi del feed](./assets/data-feed-sync-status.png)

   Se la sincronizzazione dei dati è stata avviata, i dati del feed mostrano i record inviati correttamente. È inoltre possibile visualizzare e risolvere i problemi di sincronizzazione visualizzando i dettagli di ciascun feed.

1. Verifica che Adobe Commerce Optimizer riceva i dati del catalogo:

   Dal menu Commerce Optimizer, selezionare **[!UICONTROL Data Sync]** per aprire la pagina Sincronizzazione dati.

   ![Sincronizzazione dati](./assets/data-sync.png)

### Risoluzione dei problemi

Se la sincronizzazione dei dati non è stata avviata, verificare che gli indici di catalogo siano validi. Se gli indici non sono validi, eseguire il comando seguente da Commerce CLI per reindicizzare i dati del catalogo:

```terminal
bin/magento indexer:reindex" catalog indexer re-index CLI command to start PaaS to ACO catalog data synchronization.
```

## Personalizzare la configurazione di esportazione dei dati di Commerce

È possibile personalizzare le impostazioni di esportazione di Adobe Commerce Optimizer per esportare i dati solo per ambiti specifici aggiornando la configurazione di esportazione dalla griglia dell&#39;archivio in Amministrazione (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* Al livello `website`, la disabilitazione dell&#39;impostazione di esportazione interrompe l&#39;esportazione dei prezzi e dei dati del listino prezzi in Adobe Commerce Optimizer.

* Al livello `storeview`, la disabilitazione dell&#39;impostazione di esportazione interrompe l&#39;esportazione di prodotti e attributi di prodotto in Adobe Commerce Optimizer.

Quando la configurazione viene modificata, gli indici corrispondenti vengono invalidati per attivare la riesportazione delle entità interessate.

## Configurare gli store di Adobe Commerce Optimizer

Configurare gli store di Adobe Commerce Optimizer creando visualizzazioni catalogo e criteri&#x200B; Vedi [Creazione di visualizzazioni catalogo](../optimizer/setup/catalog-view.md) nella Guida di Adobe Commerce Optimizer.

I listini prezzi vengono creati automaticamente dai gruppi di clienti Adobe Commerce.

## Configurare una vetrina Commerce su Edge Delivery Services

Questa sezione fornisce una panoramica generale dei passaggi necessari per configurare la vetrina Commerce. Informazioni dettagliate sono disponibili nel sito della documentazione di [Adobe Commerce Storefront] (https://experienceleague.adobe.com/developer/commerce/storefront/?lang=it).

1. Clona e distribuisci il boilerplate di Adobe Commerce Storefront in EDS utilizzando lo [strumento Site Creator](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. [Configurare un ambiente di sviluppo locale](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=it#set-up-local-environment).

1. [Installare il pacchetto di compatibilità di GraphQL Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/?lang=it).&#x200B;

1. [Configurare le intestazioni CORS per l&#39;istanza di Commerce nell&#39;ambiente cloud](#configure-cors-headers-for-commerce-instance).

1. [Connetti la vetrina alle origini dati di Commerce](#connect-the-storefront-to-commerce-data-sources).

### Configurare le intestazioni CORS per l’istanza di Commerce

Per consentire alle richieste GraphQL di provenire da una vetrina Edge Delivery Services (EDS) ad Adobe Commerce in ambiente cloud o locale, aggiungi intestazioni CORS (Cross-Origin Resource Sharing) specifiche agli endpoint Adobe Commerce GraphQL. &#x200B; Per istruzioni, consulta [Configurazione CORS](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/cors-setup/?lang=it) nella *documentazione di Adobe Commerce Storefront*.

### Collegare la vetrina alle origini dati di Commerce

Nell&#39;archivio GitHub per il codice boilerplate Storefront, aggiorna il file di configurazione storefront, `config.json`, con i seguenti parametri:

* `"commerce-core-endpoint": "Commerce cloud instance GraphQL endpoint"`, ad esempio `https://{{your store}}/graphql`.

* `"commerce-endpoint": "Commerce Optimizer instance GraphQL endpoint"`, ad esempio `https://na1-sandbox.api.commerce.adobe.com/{{instanceId}}/v1/catalog&#x200B;`.

* `"AC-Environment-Id": "Customer organization ID"` - Ottieni questo valore dal [progetto cloud Commerce](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/project/overview#project-overview).

* `"AC-View-ID": "Catalog view ID in Commerce Optimizer Admin"` - Ottieni questo valore dai [dettagli della visualizzazione catalogo](../optimizer/setup/catalog-view.md#view-details) in Adobe Commerce Optimizer.

* `"AC-Price-Book-ID": "base::b6589fc6ab0dc82cf12099d1c2d40ab994e8410c"` — Ottieni questo valore dall&#39;elenco dei listini prezzi assegnati in [dettagli visualizzazione catalogo](../optimizer/setup/catalog-view.md#view-details) in Adobe Commerce Optimizer.

* `"AC-Source-Locale": "catalogSource"`— Specificare l&#39;origine associata allo storeview Commerce per la connessione allo storefront. Puoi visualizzare le origini disponibili dalla pagina [Sincronizzazione dati](../optimizer/setup/data-sync.md) in Adobe Commerce Optimizer.

Per ulteriori informazioni, vedi [Configurazione storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=it) nella *documentazione di Adobe Commerce Storefront*.


