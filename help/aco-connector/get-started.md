---
title: Introduzione al connettore Adobe Commerce Optimizer
description: Scopri come installare e configurare il connettore, personalizzare la configurazione di esportazione, connettersi a Adobe Commerce Optimizer e monitorare lo stato di sincronizzazione dei dati.
feature: Personalization, Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: f302efcb6c08d5a3c695a47ae16fdac790a8bc24
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---


# Introduzione

Installa e configura il connettore Commerce Optimizer per sincronizzare i dati del catalogo Adobe Commerce con [!DNL Adobe Commerce Optimizer], quindi monitora lo stato di sincronizzazione dei dati per garantire che la vetrina sia aggiornata.

## Requisiti per l’utilizzo dell’integrazione

* Adobe Commerce 2.4.7+

   * PHP 8.2, 8.3 o 8.4
   * Compositore 2.x

* Licenza [!DNL Adobe Commerce Optimizer] con istanza sandbox predisposta.

* Accedi a [repo.magento.com](https://repo.magento.com) per scaricare il metapacchetto del connettore Commerce tramite Composer.

* Accesso amministratore a un&#39;istanza sandbox [Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

L’utente di Adobe Commerce che configura l’integrazione deve disporre di:

* Accesso amministratore all’amministrazione di Adobe Commerce.

* [Accesso alla riga di comando al server applicazioni Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Accesso per sviluppatori all&#39;organizzazione [IMS](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) in cui è stato eseguito il provisioning del progetto [!DNL Adobe Commerce Optimizer].

>[!BEGINSHADEBOX]

## Prerequisiti

Se è installata una delle seguenti estensioni, disinstallarle prima di installare Commerce Optimizer Connector:

* Adobe Commerce Live Search (`magento/live-search`)
* Consigli di prodotto di Adobe Commerce (`magento/product-recommendations`)
* Servizio catalogo Adobe Commerce (`magento/catalog-service`, `magento/catalog-service-installer`)
* Dashboard di gestione dati (`magento-catalog-sync-admin`)

I dati associati a queste estensioni sono ancora disponibili nel database di Commerce. Tuttavia, non viene esportato in [!DNL Adobe Commerce Optimizer] quando il connettore è abilitato. Per implementare le funzionalità di ricerca e merchandising fornite da queste estensioni dopo l&#39;abilitazione del connettore, configurale dalla [[!DNL Adobe Commerce Optimizer] interfaccia utente amministratore](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!ENDSHADEBOX]

## Passaggi di configurazione

Segui questi passaggi per abilitare il connettore e iniziare a sincronizzare i dati da Commerce all’istanza Adobe Commerce Optimizer.

1. **[Installa il pacchetto Commerce Optimizer Connector](#install-the-commerce-connector-package)** utilizzando Composer per connettere l&#39;istanza Commerce a [!DNL Adobe Commerce Optimizer].

1. **[Rivedi e personalizza la configurazione di esportazione dei dati](#customize-commerce-data-export-configuration)** dall&#39;amministratore.

1. **[Ottieni le credenziali API necessarie per stabilire la connessione tra Commerce e Commerce Optimizer](#get-required-values-for-configuring-the-commerce-optimizer-connection)**.

1. **[Abilita l&#39;integrazione [!DNL Adobe Commerce Optimizer] &#x200B;](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verificare che la sincronizzazione dei dati funzioni](#verify-that-the-data-sync-is-working)**.


## Installare il pacchetto Commerce Optimizer Connector

Il connettore Adobe Commerce Optimizer viene fornito come metapacchetto Compositore disponibile per tutti i commercianti Commerce con una licenza attiva per [!DNL Adobe Commerce Optimizer].

### Passaggi per l’installazione

1. Aggiungi il modulo `adobe-commerce/commerce-data-export-aco-adapter` tramite Compositore:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Implementa le modifiche nell’ambiente di staging Adobe Commerce.

Al termine dell’implementazione, l’opzione Commerce Optimizer è disponibile nel menu Amministrazione di Commerce. Fai clic su **[!UICONTROL Commerce Optimizer]** per aprire l&#39;istanza di Commerce Optimizer direttamente dall&#39;amministratore Commerce.

>[!NOTE]
>
>Per istruzioni dettagliate sull’installazione dell’estensione, consulta le seguenti guide:
>
>[Installa estensione su Adobe Commerce su infrastruttura cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Installa l&#39;estensione in Adobe Commerce locale](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

### Ottieni i dettagli di connessione richiesti

Da Adobe Developer Console, creare un progetto per sviluppatori abilitato per il servizio di acquisizione [!DNL Adobe Commerce Optimizer] e generare le credenziali da server a server OAuth. Per istruzioni dettagliate, consulta [Ottenere le credenziali IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) nella *Guida per gli sviluppatori di merchandising*.

>[!TIP]
>
>Se disponi già di un progetto per sviluppatori configurato con l’API di acquisizione dati nella stessa organizzazione IMS dell’istanza di Commerce Optimizer, puoi riutilizzare le credenziali server-to-server OAuth esistenti.

Salva i seguenti valori dalla pagina delle credenziali:

* **ID organizzazione** (`org_id`)
* **ID client** (`client_id`)
* **Segreto client** (`client_secret`)

### Ottieni dettagli istanza [!DNL Adobe Commerce Optimizer]

Salva l&#39;ID istanza (detto anche ID tenant) dall&#39;istanza [!DNL Adobe Commerce Optimizer]. Puoi trovarli nell’URL utilizzato per accedere all’istanza. Ad esempio, in `https://experience.adobe.com/#/@<project-id>/in:TToyu73daQRn66KAYaq8YZ/commerce-optimizer-studio/home`, l&#39;ID istanza è `TToyu73daQRn66KAYaq8YZ`.

## Personalizzare la configurazione di esportazione dei dati di Commerce

Per impostazione predefinita, la sincronizzazione dei dati del catalogo è abilitata per tutti gli ambiti di Commerce (siti Web e visualizzazioni dello store). È possibile personalizzare le impostazioni di esportazione per sincronizzare i dati solo per ambiti specifici in base alle esigenze aziendali. Ad esempio, se si dispone di più visualizzazioni dello store ma si desidera esportare solo i dati per una di esse, è possibile disattivare la funzione di esportazione per le altre visualizzazioni dello store.

>[!IMPORTANT]
>
>La modifica delle impostazioni di esportazione attiva una reindicizzazione completa, che può richiedere molto tempo a seconda delle dimensioni del catalogo. Pianifica queste modifiche durante i periodi di traffico ridotto per ridurre al minimo l’impatto sulle prestazioni.

### Esportazione dati per ambito

Nella tabella seguente vengono descritti i dati esportati a ogni livello di ambito:

| Ambito | Dati esportati | Note |
| ------- | --------------- | ------- |
| Sito Web | Prezzi e listini prezzi | Ogni set di prezzi viene esportato come [listino prezzi](../optimizer/setup/pricebooks.md) utilizzando la convenzione di denominazione `website::customergroupcode`. Sono inclusi tutti i gruppi di clienti per il sito Web. |
| Visualizzazione store | Prodotti e attributi del prodotto | Ogni visualizzazione archivio crea un&#39;origine catalogo separata in [!DNL Adobe Commerce Optimizer]. |

### Attivare e disattivare il comportamento

| Azione | Risultato |
| -------- | -------- |
| Disattiva una visualizzazione store | L&#39;origine del catalogo rimane in [!DNL Adobe Commerce Optimizer], ma tutti i dati vengono rimossi. |
| Disattiva e riattiva la visualizzazione dello store | La stessa origine del catalogo viene ripopolata con una risincronizzazione completa dei dati. |

### Aggiornare la configurazione di esportazione

Dopo aver installato il pacchetto Connector, la griglia Store in Admin ora mostra le impostazioni di configurazione dell’esportazione per Commerce Optimizer.

![Archivia griglia con impostazioni di sincronizzazione Commerce Optimizer](./assets/aco-connector-sync-config.png){width="600" zoomable="yes"}

**Per modificare le impostazioni di una visualizzazione sito Web o archivio:**

1. In Amministrazione Commerce, passa a **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**.

1. Seleziona la visualizzazione del sito web o store che desideri configurare.

1. Nelle impostazioni dell&#39;utilità di esportazione **[!DNL Adobe Commerce Optimizer]**, utilizzare la casella di controllo per abilitare o disabilitare la sincronizzazione dei dati in base alle esigenze.

   ![Aggiorna configurazione sincronizzazione dati](./assets/aco-connector-store-website-export-settings.png){width="500" zoomable="yes"}

1. Salva le modifiche.

## Abilita l&#39;integrazione di [!DNL Adobe Commerce Optimizer]

>[!IMPORTANT]
>
>L&#39;elaborazione della sincronizzazione dati viene avviata non appena si esegue il comando di configurazione. Per impostazione predefinita, la sincronizzazione dei dati del catalogo è abilitata per tutti gli ambiti di Commerce (siti Web e visualizzazioni dello store). A seconda delle dimensioni del catalogo, il processo di sincronizzazione dei dati può richiedere da alcuni minuti a diverse ore.

Utilizzando le credenziali API e i dettagli dell&#39;istanza raccolti nei passaggi precedenti, ora puoi configurare l&#39;integrazione tra le istanze Commerce e [!DNL Adobe Commerce Optimizer].

1. Dall&#39;amministratore di Commerce, selezionare **[!UICONTROL Adobe Commerce Optimizer]** per visualizzare la pagina di configurazione con le istruzioni.

   ![[!DNL Adobe Commerce Optimizer] pagina di configurazione](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Dalla riga di comando, [utilizzare SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) per connettersi all&#39;ambiente di staging di Commerce.

1. Esegui il seguente comando Commerce CLI per configurare l’integrazione, sostituendo i valori segnaposto con i valori per il progetto Commerce Optimizer:

```terminal
bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
```

1. Verificare la connessione tornando all&#39;amministratore di Commerce e selezionando l&#39;opzione [!UICONTROL Adobe Commerce Optimizer].

   Quando si fa clic sull&#39;opzione, viene aperta l&#39;interfaccia utente [!DNL Adobe Commerce Optimizer] in una nuova scheda.

## Verifica che la sincronizzazione dei dati funzioni

Dopo aver abilitato l’integrazione, la sincronizzazione dei dati inizia automaticamente. A seconda delle dimensioni del catalogo, la sincronizzazione iniziale può richiedere da alcuni minuti a diverse ore.

1. **Verifica lo stato di sincronizzazione nell&#39;amministratore di Commerce:**

   Vai a **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**.

   ![Pagina Stato sincronizzazione feed dati con report sullo stato degli elementi del feed](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   Quando la sincronizzazione è in esecuzione, i dati del feed mostrano i record inviati correttamente. Seleziona un feed per visualizzare i dettagli o risolvere i problemi di sincronizzazione.

1. **Dati di conferma arrivati in Commerce Optimizer:**

   Dal menu [!DNL Adobe Commerce Optimizer], selezionare **[!UICONTROL Data Sync]**.

   ![Sincronizzazione dati](./assets/data-sync.png){width="500" zoomable="yes"}

   Verifica che vengano visualizzati i prodotti, i prezzi e gli attributi previsti.

>[!TIP]
>
>In caso di problemi con la sincronizzazione dei dati, consulta la sezione [Risoluzione dei problemi](/help/data-export/troubleshooting-logging.md) nella *Esportazione dati SaaS*.

## Passaggi successivi

1. **[Configura [!DNL Adobe Commerce Optimizer] visualizzazioni catalogo e criteri](#configure-adobe-commerce-optimizer-stores)**

   Creare visualizzazioni e criteri del catalogo nella Guida di [!DNL Adobe Commerce Optimizer]. I listini prezzi vengono creati automaticamente dai gruppi di clienti Adobe Commerce.

1. **[Configura una vetrina Commerce in Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

   Segui la [documentazione di configurazione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/) per connettere la tua vetrina all&#39;istanza [!DNL Adobe Commerce Optimizer] e iniziare a distribuire esperienze di e-commerce personalizzate.


