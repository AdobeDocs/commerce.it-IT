---
title: Introduzione a  [!DNL Adobe Commerce Optimizer Connector]
description: Scopri come installare  [!DNL Adobe Commerce Optimizer Connector], configurare le impostazioni di esportazione dell'ambito, abilitare l'autenticazione IMS e verificare la sincronizzazione del catalogo.
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T16:55:50.934Z'
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 69f39a6a62e05c86a0e2897d09079543b3d8830e
workflow-type: tm+mt
source-wordcount: 1184
ht-degree: 0%

---


# Introduzione

Installa e configura [!DNL Adobe Commerce Optimizer Connector] per sincronizzare i dati del catalogo [!DNL Adobe Commerce] con [!DNL Adobe Commerce Optimizer], quindi monitora lo stato di sincronizzazione dei dati per garantire che la vetrina sia aggiornata.

{{aco-integration-environment-alignment}}

## Requisiti per l’utilizzo dell’integrazione {#requirements-to-use-the-integration}

* [!DNL Adobe Commerce] 2.4.7+

   * PHP 8.2, 8.3 o 8.4
   * Compositore 2.x

* Licenza [!DNL Adobe Commerce Optimizer] con istanza sandbox predisposta.

* [Chiavi di autenticazione](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) per scaricare il metapacchetto del connettore tramite Compositore.

* Accesso amministratore a un&#39;istanza [[!DNL Adobe Commerce Optimizer] sandbox](../optimizer/get-started.md).

L&#39;utente [!DNL Adobe Commerce] che configura l&#39;integrazione deve avere:

* Accesso amministratore all’amministrazione di Commerce.

* [Accesso alla riga di comando al  [!DNL Adobe Commerce] server applicazioni](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/project/user-access).

* Accesso per sviluppatori all&#39;organizzazione [IMS](https://experienceleague.adobe.com/it/docs/core-services/interface/administration/organizations?) in cui è stato eseguito il provisioning del progetto [!DNL Adobe Commerce Optimizer].

>[!BEGINSHADEBOX]

## Prerequisiti

Se è installata una delle seguenti estensioni, disinstallarle prima di installare [!DNL Adobe Commerce Optimizer Connector]:

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* Dashboard di gestione dati (`magento-catalog-sync-admin`)

I dati associati a queste estensioni sono ancora disponibili nel database di Commerce. Tuttavia, non viene esportato in [!DNL Adobe Commerce Optimizer] quando il connettore è abilitato. Per implementare le funzionalità di ricerca e merchandising fornite da queste estensioni dopo l&#39;abilitazione del connettore, configurale dall&#39;[[!DNL Adobe Commerce Optimizer] interfaccia utente amministratore](https://experienceleague.adobe.com/it/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Se queste estensioni non vengono rimosse prima di abilitare il connettore, è possibile che vengano visualizzate schermate di configurazione interrotte, dati duplicati in [!DNL Adobe Commerce Optimizer] perché gli stessi dati vengono esportati sia dal connettore che dalle estensioni esistenti ed errori 401 o 403 nei registri a causa di conflitti nel modo in cui le estensioni e il connettore si autenticano con i servizi connessi.

>[!ENDSHADEBOX]

## Passaggi di configurazione

Segui questi passaggi per abilitare [!DNL Commerce Optimizer Connector] e iniziare a sincronizzare i dati da [!DNL Adobe Commerce] all&#39;istanza [!DNL Commerce Optimizer].

1. **[Installa il  [!DNL Commerce Optimizer Connector] pacchetto](#install-the-adobe-commerce-optimizer-connector-package)** utilizzando Composer per connettere l&#39;istanza [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer].

1. **[Personalizzare la configurazione di esportazione dei dati](#customize-the-commerce-scopes-export-configuration)** dall&#39;amministratore.

1. **[Abilita l&#39;integrazione [!DNL Adobe Commerce Optimizer] &#x200B;](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verificare che la sincronizzazione dei dati funzioni](#verify-that-the-data-sync-is-working)**.

## Installa il pacchetto [!DNL Commerce Optimizer Connector] {#install-the-adobe-commerce-optimizer-connector-package}

[!DNL Commerce Optimizer Connector] viene consegnato come metapacchetto Compositore disponibile per tutti i commercianti Commerce con una licenza attiva per [!DNL Adobe Commerce Optimizer].

### Passaggi per l’installazione

1. Aggiungi il modulo `adobe-commerce/commerce-data-export-aco-adapter` tramite Compositore:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Distribuire le modifiche nell&#39;ambiente di staging [!DNL Adobe Commerce].

   Al termine della distribuzione, l&#39;opzione [!DNL Commerce Optimizer] è disponibile nel menu di amministrazione di Commerce. Seleziona **[!UICONTROL Commerce Optimizer]** per aprire l&#39;istanza di [!DNL Adobe Commerce Optimizer] direttamente dall&#39;amministratore di Commerce.

>[!NOTE]
>
>Per istruzioni dettagliate sull’installazione dell’estensione, consulta le seguenti guide:
>
>[Installa estensione su [!DNL Adobe Commerce] in Cloud Infrastructure](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Installa estensione in [!DNL Adobe Commerce] locale](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/tutorials/extensions)

## Personalizzare la configurazione di esportazione degli ambiti di Commerce {#customize-the-commerce-scopes-export-configuration}

Per impostazione predefinita, la sincronizzazione dei dati del catalogo è abilitata per tutti gli ambiti di Commerce (siti web, gruppi di clienti e visualizzazioni store). È possibile personalizzare le impostazioni di esportazione per sincronizzare i dati solo per ambiti specifici in base alle esigenze aziendali. Se ad esempio si dispone di più visualizzazioni archivio che condividono la stessa lingua, è possibile scegliere di esportare i dati per una sola delle visualizzazioni archivio e utilizzarli come [origine catalogo](../optimizer/setup/catalog-source.md) per più visualizzazioni catalogo in [!DNL Adobe Commerce Optimizer].

>[!IMPORTANT]
>
>La modifica delle impostazioni di esportazione attiva una reindicizzazione completa, che può richiedere molto tempo a seconda delle dimensioni del catalogo. Adobe consiglia di configurare gli ambiti Commerce da sincronizzare con [!DNL Adobe Commerce Optimizer] prima di abilitare l&#39;integrazione e avviare la sincronizzazione dati iniziale.

Nella tabella seguente vengono descritti i dati esportati a ogni livello di ambito:

| Ambito | Dati esportati | Note |
| ----- | ------------- | ----- |
| Sito web e gruppo di clienti | Prezzi e listini prezzi | Ogni set di prezzi viene esportato come [listino prezzi](../optimizer/setup/pricebooks.md) utilizzando la convenzione di denominazione `<website>::<SHA1 of customer group ID>`. Sono inclusi tutti i gruppi di clienti per il sito Web. |
| Visualizzazione store | Prodotti e attributi del prodotto | Ogni visualizzazione archivio crea una [origine catalogo](../optimizer/setup/catalog-source.md) separata in [!DNL Adobe Commerce Optimizer]. |

![Archivia griglia con impostazioni di sincronizzazione Commerce Optimizer](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

**Per modificare le impostazioni di una visualizzazione sito Web o archivio:**

1. In Amministrazione Commerce, passa a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

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

Abilitare l&#39;integrazione e avviare la sincronizzazione dei dati eseguendo il comando CLI `aco:config:init`. Questo comando completa i passaggi seguenti:

1. Ottiene un token di accesso IMS utilizzando le credenziali fornite come argomenti della riga di comando.
1. Chiama il servizio Commerce Cloud Manager (CCM) in `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` per convalidare il tenant ed estrarre l&#39;URL di acquisizione e l&#39;URL di [!DNL Adobe Commerce Optimizer] Studio.
1. Salva tutta la configurazione (segreto client crittografato) in `core_config_data`.
1. Pianifica la sincronizzazione completa iniziale invalidando tutti gli indicizzatori di feed [!DNL Commerce Optimizer].

>[!IMPORTANT]
>
>L’elaborazione della sincronizzazione dati viene avviata in background non appena viene completata la configurazione. A seconda delle dimensioni del catalogo, il processo di sincronizzazione dei dati può richiedere da alcuni minuti a diverse ore.

### Ottieni i dettagli di connessione richiesti

Da [Adobe Developer Console](https://developer.adobe.com/console), crea un nuovo progetto abilitato per il servizio di acquisizione [!DNL Adobe Commerce Optimizer] e genera le credenziali da server a server OAuth. Per istruzioni dettagliate, consulta [Ottenere le credenziali IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) nella *Guida per gli sviluppatori di merchandising*.

Salva i seguenti valori dalla pagina delle credenziali:

* **ID organizzazione** (`org_id`)
* **ID client** (`client_id`)
* **Segreto client** (`client_secret`)

![Ottieni dettagli sulle credenziali dalla pagina del progetto Adobe Developer Console](./assets/developer-console-project-credentials.png){width="500" zoomable="yes"}

### Ottieni dettagli istanza [!DNL Adobe Commerce Optimizer]

Ottieni l&#39;ID _tenant_ dal campo _[!DNL Instance Id]_&#x200B;nell&#39;istanza [[!DNL Instance details] page](../optimizer/get-started.md#manage-instances) di [!DNL Adobe Commerce Optimizer] o dall&#39;URL utilizzato per accedere all&#39;istanza. Ad esempio, in `https://experience.adobe.com/#/@<your organization>/in:<tenant ID>/commerce-optimizer-studio/home`.

1. Dall&#39;amministratore di Commerce, selezionare **[!UICONTROL Adobe Commerce Optimizer]** per visualizzare la pagina di configurazione con le istruzioni.

   ![[!DNL Adobe Commerce Optimizer] pagina di configurazione](./assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Dalla riga di comando, [utilizzare SSH](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/develop/secure-connections) per connettersi all&#39;ambiente di staging [!DNL Adobe Commerce].

1. Esegui il seguente comando CLI [!DNL Adobe Commerce] per configurare l&#39;integrazione, sostituendo i valori segnaposto con i valori per il progetto [!DNL Commerce Optimizer]:

   ```terminal
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Verificare la connessione tornando all&#39;amministratore di Commerce e selezionando l&#39;opzione [!UICONTROL Adobe Commerce Optimizer].

   Quando selezioni l&#39;opzione, viene aperta l&#39;interfaccia utente [!DNL Adobe Commerce Optimizer] in una nuova scheda.

## Verifica che la sincronizzazione dei dati funzioni

È possibile monitorare e verificare che la sincronizzazione funzioni dalla pagina [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) disponibile nell&#39;amministratore.

1. **Verifica lo stato di sincronizzazione nell&#39;amministratore di Commerce:**

   Vai a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Pagina Stato sincronizzazione feed dati con report sullo stato degli elementi del feed](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   Quando la sincronizzazione è in esecuzione, i dati del feed mostrano i record inviati correttamente. Seleziona un feed per visualizzare i dettagli o risolvere i problemi di sincronizzazione.

1. **Dati di conferma arrivati in [!DNL Commerce Optimizer]:**

   Dal menu [!DNL Adobe Commerce Optimizer], selezionare **[!UICONTROL Data Sync]**.

   ![Pagina di sincronizzazione dati in Adobe Commerce Optimizer con i dati del catalogo sincronizzati](./assets/data-sync.png){width="500" zoomable="yes"}

   Verifica che vengano visualizzati i prodotti, i prezzi e gli attributi previsti.

>[!TIP]
>
>In caso di problemi con la sincronizzazione dei dati, consulta la [guida alla risoluzione dei problemi](troubleshooting.md).

## Passaggi successivi

1. **Configura [!DNL Adobe Commerce Optimizer] visualizzazioni catalogo e criteri**

   Creare visualizzazioni e criteri catalogo nell&#39;interfaccia utente [!DNL Adobe Commerce Optimizer]. I listini prezzi vengono creati automaticamente da [!DNL Adobe Commerce] gruppi di clienti. Per istruzioni, vedere la documentazione [Visualizzazioni catalogo](../optimizer/setup/catalog-view.md) e [Criteri](../optimizer/setup/policies.md) nella Guida utente *[!DNL Adobe Commerce Optimizer]*.

1. **Configura una vetrina Commerce su[!DNL Edge Delivery Services]**

   Segui la [documentazione di configurazione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/?lang=it){target="_blank"} per connettere la tua vetrina all&#39;istanza [!DNL Adobe Commerce Optimizer] e iniziare a distribuire esperienze di e-commerce personalizzate.

