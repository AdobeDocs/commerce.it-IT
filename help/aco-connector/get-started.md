---
title: Introduzione al connettore Adobe Commerce Optimizer
description: Scopri come installare e configurare il connettore, personalizzare la configurazione di esportazione, connettersi a Adobe Commerce Optimizer e monitorare lo stato di sincronizzazione dei dati.
feature: Personalization, Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: dc50e4d7bcd118b2b9a800779c600ade5560e0bf
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 0%

---


# Introduzione

Installa e configura il connettore Adobe Commerce Optimizer per sincronizzare i dati del catalogo Adobe Commerce con [!DNL Adobe Commerce Optimizer], quindi monitora lo stato di sincronizzazione dei dati per garantire che la vetrina sia aggiornata.

{{aco-integration-environment-alignment}}

## Requisiti per l’utilizzo dell’integrazione

* Adobe Commerce 2.4.7+

   * PHP 8.2, 8.3 o 8.4
   * Compositore 2.x

* Licenza [!DNL Adobe Commerce Optimizer] con istanza sandbox predisposta.

* [Chiavi di autenticazione](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) per scaricare il metapacchetto del connettore Commerce tramite Composer.

* Accesso amministratore a un&#39;istanza sandbox [Adobe Commerce Optimizer](../optimizer/get-started.md).

L’utente di Adobe Commerce che configura l’integrazione deve disporre di:

* Accesso amministratore all’amministrazione di Adobe Commerce.

* [Accesso alla riga di comando al server applicazioni Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Accesso per sviluppatori all&#39;organizzazione [IMS](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) in cui è stato eseguito il provisioning del progetto [!DNL Adobe Commerce Optimizer].

>[!BEGINSHADEBOX]

## Prerequisiti

Se è installata una delle seguenti estensioni, disinstallarle prima di installare Adobe Commerce Optimizer Connector:

* Adobe Commerce Live Search (`magento/live-search`)
* Consigli di prodotto di Adobe Commerce (`magento/product-recommendations`)
* Servizio catalogo Adobe Commerce (`magento/catalog-service`, `magento/catalog-service-installer`)
* Dashboard di gestione dati (`magento-catalog-sync-admin`)

I dati associati a queste estensioni sono ancora disponibili nel database di Commerce. Tuttavia, non viene esportato in [!DNL Adobe Commerce Optimizer] quando il connettore è abilitato. Per implementare le funzionalità di ricerca e merchandising fornite da queste estensioni dopo l&#39;abilitazione del connettore, configurale dalla [[!DNL Adobe Commerce Optimizer] interfaccia utente amministratore](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Se queste estensioni non vengono rimosse prima di abilitare il connettore, è possibile che vengano visualizzate schermate di configurazione interrotte, dati duplicati in [!DNL Adobe Commerce Optimizer] perché gli stessi dati vengono esportati sia dal connettore che dalle estensioni esistenti e errori 401 o 403 nei registri a causa di conflitti nel modo in cui le estensioni e il connettore si autenticano con i servizi connessi.

>[!ENDSHADEBOX]

## Passaggi di configurazione

Segui questi passaggi per abilitare il connettore e iniziare a sincronizzare i dati da Commerce all’istanza Adobe Commerce Optimizer.

1. **[Installa il pacchetto Adobe Commerce Optimizer Connector](#install-the-adobe-commerce-optimizer-connector-package)** utilizzando Composer per connettere l&#39;istanza Commerce a [!DNL Adobe Commerce Optimizer].

1. **[Personalizzare la configurazione di esportazione dei dati](#customize-the-commerce-scopes-export-configuration)** dall&#39;amministratore.

1. **[Abilita l&#39;integrazione [!DNL Adobe Commerce Optimizer] ](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verificare che la sincronizzazione dei dati funzioni](#verify-that-the-data-sync-is-working)**.


## Installare il pacchetto Adobe Commerce Optimizer Connector {#install-the-adobe-commerce-optimizer-connector-package}

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

## Personalizzare la configurazione di esportazione degli ambiti di Commerce

Per impostazione predefinita, la sincronizzazione dei dati del catalogo è abilitata per tutti gli ambiti di Commerce (siti web, gruppi di clienti e visualizzazioni store). È possibile personalizzare le impostazioni di esportazione per sincronizzare i dati solo per ambiti specifici in base alle esigenze aziendali. Se ad esempio si dispone di più visualizzazioni archivio che condividono la stessa lingua, è possibile scegliere di esportare i dati per una sola delle visualizzazioni archivio e utilizzarli come [origine catalogo](../optimizer/setup/catalog-source.md) per più visualizzazioni catalogo in [!DNL Adobe Commerce Optimizer].

>[!IMPORTANT]
>
>La modifica delle impostazioni di esportazione attiva una reindicizzazione completa, che può richiedere molto tempo a seconda delle dimensioni del catalogo. Adobe consiglia di configurare gli ambiti Commerce da sincronizzare con Commerce Optimizer prima di abilitare l’integrazione e avviare la sincronizzazione dati iniziale.


Nella tabella seguente vengono descritti i dati esportati a ogni livello di ambito:

| Ambito | Dati esportati | Note |
|----------------------------| --------------- |-------|
| Sito web e gruppo di clienti | Prezzi e listini prezzi | Ogni set di prezzi viene esportato come [listino prezzi](../optimizer/setup/pricebooks.md) utilizzando la convenzione di denominazione `<website>::<SHA1 of customer group ID>`. Sono inclusi tutti i gruppi di clienti per il sito Web. |
| Visualizzazione store | Prodotti e attributi del prodotto | Ogni visualizzazione archivio crea una [origine catalogo](../optimizer/setup/catalog-source.md) separata in [!DNL Adobe Commerce Optimizer]. |

![Archivia griglia con impostazioni di sincronizzazione Commerce Optimizer](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

**Per modificare le impostazioni di una visualizzazione sito Web o archivio:**

1. In Amministrazione Commerce, passa a **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**.

1. Seleziona la visualizzazione del sito web o store che desideri configurare.

1. Nelle impostazioni dell&#39;utilità di esportazione **[!DNL Adobe Commerce Optimizer]**, utilizzare la casella di controllo per abilitare o disabilitare la sincronizzazione dei dati in base alle esigenze.

   ![Aggiorna configurazione sincronizzazione dati](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. Salva le modifiche.

### Attivare e disattivare il comportamento

| Azione | Risultato |
| -------- | -------- |
| Disattiva una visualizzazione store | L&#39;origine del catalogo rimane in [!DNL Adobe Commerce Optimizer], ma tutti i dati vengono rimossi. |
| Disattiva e riattiva la visualizzazione dello store | La stessa origine del catalogo viene ripopolata con una risincronizzazione completa dei dati. |

## Abilita l&#39;integrazione di [!DNL Adobe Commerce Optimizer]

>[!IMPORTANT]
>
>L’elaborazione della sincronizzazione dati verrà avviata in background al termine della configurazione. A seconda delle dimensioni del catalogo, il processo di sincronizzazione dei dati può richiedere da alcuni minuti a diverse ore.

### Ottieni i dettagli di connessione richiesti

Da [Adobe Developer Console](https://developer.adobe.com/console), crea un nuovo progetto abilitato per il servizio di acquisizione [!DNL Adobe Commerce Optimizer] e genera le credenziali da server a server OAuth. Per istruzioni dettagliate, consulta [Ottenere le credenziali IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) nella *Guida per gli sviluppatori di merchandising*.

Salva i seguenti valori dalla pagina delle credenziali:

* **ID organizzazione** (`org_id`)
* **ID client** (`client_id`)
* **Segreto client** (`client_secret`)

![Ottieni dettagli credenziali](assets/developer-console-project-credentials.png){width="500" zoomable="yes"}

### Ottieni dettagli istanza [!DNL Adobe Commerce Optimizer]

Ottieni l&#39;ID _tenant_ dal campo _[!DNL Instance Id]_nell&#39;istanza [[!DNL Instance details] page](../optimizer/get-started.md#manage-instances) di [!DNL Adobe Commerce Optimizer] o dall&#39;URL utilizzato per accedere all&#39;istanza. Ad esempio, in `https://experience.adobe.com/#/@<your organization>/in:<tenant ID>/commerce-optimizer-studio/home`.

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

Puoi monitorare e verificare che la sincronizzazione funzioni dalla pagina [Stato sincronizzazione feed dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) disponibile nell&#39;amministratore.

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

1. **Configura [!DNL Adobe Commerce Optimizer] visualizzazioni catalogo e criteri**

   Creare visualizzazioni e criteri catalogo nell&#39;interfaccia utente [!DNL Adobe Commerce Optimizer]. I listini prezzi vengono creati automaticamente dai gruppi di clienti Adobe Commerce. Per istruzioni, consulta la documentazione [Visualizzazioni catalogo](../optimizer/setup/catalog-view.md) e [Criteri](../optimizer/setup/policies.md) nella *Guida utente di Commerce Optimizer*.

1. **Configura una vetrina Commerce in Edge Delivery Services**

   Segui la [documentazione di configurazione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/) per connettere la tua vetrina all&#39;istanza [!DNL Adobe Commerce Optimizer] e iniziare a distribuire esperienze di e-commerce personalizzate.


