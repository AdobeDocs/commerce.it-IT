---
title: Installazione
description: Installa  [!DNL Store Fulfillment solution]  per una vetrina Adobe Commerce utilizzando Composer for PHP.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Installazione

Completare l&#39;installazione iniziale dell&#39;estensione [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] in un ambiente non di produzione con gestione code in esecuzione e caching configurati per consentire la gestione delle eccezioni. Assicurati che il tuo ambiente di sviluppo includa strumenti di sviluppo per garantire best practice per il funzionamento e la manutenzione dell’istanza di Adobe Commerce.

>[!TIP]
>
>Aggiorna l&#39;estensione Store Fulfillment per Adobe Commerce on-premise seguendo le [istruzioni di aggiornamento](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/modules/upgrade.html?lang=it) nella _Guida all&#39;aggiornamento di Adobe Commerce_. Per Adobe Commerce su infrastruttura cloud, consulta [Aggiornare un&#39;estensione](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/extensions.html?lang=it#upgrade-an-extension) nella *Guida di Commerce su infrastruttura cloud*.

## Prerequisiti

Rivedi i [requisiti](solution-requirements.md) per la soluzione Store Fulfillment e raccogli le informazioni richieste prima di installare o aggiornare l&#39;estensione [!DNL Store Fulfillment] per Adobe Commerce.

Se hai installato una versione pre-release o beta dell’estensione Store Fulfillment per Adobe Commerce, rimuovilo con il seguente comando prima di installare la versione corrente.

```bash
rm -rf composer.lock vendor/walmart &&
composer require walmart/magento-bopis-metapackage:1.0.0
```

## Requisiti di installazione

- **Accesso all&#39;archivio del software Store Fulfillment di Walmart Commerce Technologies (file .zip)**. Durante il processo di onboarding e abilitazione, rivolgiti al tuo Account Manager per accedere al file di installazione per l&#39;estensione Store Fulfillment.

- **Informazioni account Adobe Commerce**-L&#39;installazione della soluzione [!DNL Store Fulfillment] richiede un account [[!DNL Commerce] account](https://experienceleague.adobe.com/it/docs/commerce-admin/start/commerce-account/commerce-account-create){target="_blank"}. È necessario disporre di un ID account e di credenziali con accesso proprietario o amministratore al progetto [!DNL Adobe Commerce].

- Per [!DNL Adobe Commerce] su progetti di infrastruttura cloud, i programmi di installazione software devono avere accesso come amministratore al progetto Cloud. Consulta [Gestire l&#39;accesso utente](https://experienceleague.adobe.com/it/docs/commerce-cloud-service/user-guide/project/user-access).

- **Esperienza con Composer e[!DNL Commerce CLI]**. Per informazioni sull&#39;utilizzo di questi strumenti per installare e gestire le estensioni sulla piattaforma [!DNL Adobe Commerce], vedere [Installazione CLI generale](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/tutorials/extensions){target="_blank"}.

- **Prova a installare estensioni di terze parti su Adobe Commerce**. Per maggiori informazioni, consulta la documentazione di Adobe Commerce.

   - [Installa un&#39;estensione per un&#39;istanza di Adobe Commerce sull&#39;infrastruttura cloud](https://experienceleague.adobe.com/it/docs/commerce-cloud-service/user-guide/configure-store/extensions#install-an-extension).

   - [Installa un&#39;estensione per un&#39;istanza locale di Adobe Commerce](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/tutorials/extensions).

### Passaggio 1: scaricare il bundle dell’estensione

Segui le istruzioni fornite dai rappresentanti del tuo account per scaricare il file di archivio che contiene i pacchetti Composer per installare l’estensione Store Fulfillment Services.

### Passaggio 2: estrarre gli artefatti dell’estensione nell’applicazione

Estrai il file di archivio che contiene il bundle di integrazione per installare l’estensione Store Fulfillment Services.

1. Creare una directory di destinazione per i file estratti.

   - Dalla riga di comando, vai alla directory principale dei documenti del server web.

   - Creare una directory `artifacts`.

1. Estrarre il file di archivio nella nuova directory.

1. Verificare che i file siano stati estratti correttamente esaminando l&#39;elenco dei file.

   ```
   ../var/www/html/artifacts]$ ls -a
   .
   ..
   bopis-sdk.zip
   module-magento-bopis-alternate-pickup-contact-admin-ui.zip
   module-magento-bopis-alternate-pickup-contact-api.zip
   ```

### Passaggio 3: configurare l’app tramite Compositore

Utilizzare Composer per configurare la directory di origine per l&#39;installazione e installare l&#39;estensione Store Fulfillment Services.

1. Configurare l&#39;archivio di origine per l&#39;installazione del Compositore.

   ```bash
   composer config repositories.artifacts artifact artifacts/
   ```

1. Aggiungere l&#39;estensione Store Fulfillment Services a `composer.json`.

   ```bash
   composer require walmart/magento-bopis-metapackage:1.0.0
   ```

>[!NOTE]
>
>Per prestazioni migliori sulle istanze locali di Adobe Commerce, puoi [aggiornare la configurazione del caricamento automatico](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/deployment-flow.html?lang=it#update-the-autoloader): `composer dump-autoload --optimize`

### Passaggio 4: aggiornare lo schema e i dati del database

Completare l&#39;installazione utilizzando `bin/magento setup:upgrade` per aggiornare lo schema e i dati del database con le modifiche per supportare la soluzione Store Fulfillment.

>[!NOTE]
>
>Per i progetti Adobe Commerce su infrastrutture cloud, non è necessario registrare l’estensione. Esegui il commit delle modifiche al codice rispetto al passaggio precedente e inviale al ramo dell’ambiente. I comandi per aggiornare lo schema e i dati del database vengono eseguiti automaticamente durante il processo di creazione e distribuzione del cloud.

### Passaggio 5: completare l&#39;installazione

1. Registrare l&#39;estensione con Adobe Commerce utilizzando il comando CLI di Magento `setup:upgrade`.

   ```bash
   bin/magento setup:upgrade
   ```

1. Se richiesto, ricompilare il progetto [!DNL Commerce].

   ```bash
   bin/magento setup:di:compile
   ```

1. Pulire la cache.

   ```bash
   bin/magento cache:clean
   ```

1. Disattiva la modalità di manutenzione.

   ```bash
   bin/magento maintenance:disable
   ```

### Passaggio 6: verificare l’installazione

Dal server Adobe Commerce, verifica che i moduli per l’estensione Store Fulfillment Services siano installati e abilitati.

1. Accedi al server.

   Per le installazioni su Adobe Commerce nell&#39;infrastruttura cloud, [utilizza SSH per accedere all&#39;ambiente remoto](https://experienceleague.adobe.com/it/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh).

1. Verificare che i moduli Servizi di evasione del punto vendita siano abilitati.

   ```bash
   bin/magento module:status  --enabled | grep Walmart
   ```

   L’output deve includere i seguenti moduli:

   ```
   Walmart_BopisBase
   Walmart_BopisAlternatePickupContact
   Walmart_BopisAlternatePickupContactFrontend
   Walmart_BopisApiConnector
   Walmart_BopisAlternatePickupContactAdminUi
   Walmart_BopisCheckoutPickInStoreApi
   Walmart_BopisInventorySourceAdminUi
   Walmart_BopisCheckoutPickInStore
   Walmart_BopisInventoryCatalogApi
   Walmart_BopisPreferredLocationApi
   Walmart_BopisHomeDeliveryApi
   Walmart_BopisHomeDelivery
   Walmart_BopisPreferredLocation
   Walmart_BopisInventoryCatalog
   Walmart_BopisPreferredLocationFrontend
   Walmart_BopisCheckoutPickInStoreAdminUi
   Walmart_BopisInventorySourceApi
   Walmart_BopisInventorySourceFaasSync
   Walmart_BopisInventorySourceReservation
   Walmart_BopisLocationCheckInApi
   Walmart_BopisLogging
   Walmart_BopisStoreAssociateApi
   Walmart_BopisLocationCheckInFrontend
   Walmart_BopisStoreAssociate
   Walmart_BopisOperationQueue
   Walmart_BopisOperationQueueAdminUi
   Walmart_BopisOperationQueueApi
   Walmart_BopisOrderFaasSync
   Walmart_BopisOrderUpdateApi
   Walmart_BopisLocationCheckIn
   Walmart_BopisInventoryCatalogAdminUi
   Walmart_BopisPreferredLocationAdminUi
   Walmart_BopisDeliverySelection
   Walmart_BopisCheckoutPickInStoreFrontend
   Walmart_BopisLocationCheckInAdminUi
   Walmart_BopisStoreAssociateAdminUi
   Walmart_BopisOrderUpdate
   Walmart_BopisStoreAssociateTfa
   Walmart_BopisStoreAssociateTfaApi
   ```

### Passaggi aggiuntivi

Se necessario, utilizzare il comando CLI [setup:static-content:deploy](https://experienceleague.adobe.com/it/docs/commerce-operations/tools/cli-reference/commerce-on-premises){target="_blank"} per distribuire i file di visualizzazione statica nell&#39;ambiente di produzione.

```bash
php bin/magento setup:static-content:deploy -f
```

L&#39;opzione `-f` è necessaria se si utilizza un tema vuoto.

>[!NOTE]
>
>Per ulteriori informazioni, consulta l&#39;articolo sulle best practice per la distribuzione di contenuti statici [in Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/development/static-content-deployment.html?lang=it) nell&#39;Help Center di Adobe Commerce.


