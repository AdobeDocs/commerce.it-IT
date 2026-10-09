---
title: Introduzione a [!DNL Adobe Commerce Optimizer Connector]
description: Scopri come installare [!DNL Adobe Commerce Optimizer Connector], configurare le impostazioni di esportazione dell'ambito, abilitare l'autenticazione IMS e verificare la sincronizzazione del catalogo.
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T16:55:50.934Z'
last-update: 2026-10-01
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: c76e776250d9f996daf61d3cf62e2070803e998c
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%
---

# Introduzione

Installa e configura [!DNL Adobe Commerce Optimizer Connector] per sincronizzare i dati del catalogo [!DNL Adobe Commerce] con [!DNL Adobe Commerce Optimizer], quindi monitora lo stato di sincronizzazione dei dati per garantire che la vetrina sia aggiornata.

{{aco-integration-environment-alignment}}

>[!NOTE]
>
>Questo argomento riguarda [!DNL Adobe Commerce Optimizer Connector]. Se utilizzi [!DNL Adobe Commerce] cataloghi B2B condivisi, segui la [Guida introduttiva [!DNL Adobe Commerce Optimizer Connector for B2B]](get-started-b2b-shared-catalogs.md). Il connettore B2B estende la sincronizzazione dei dati del catalogo base per supportare la sincronizzazione di cataloghi condivisi personalizzati.

## Requisiti per l’utilizzo dell’integrazione {#requirements-to-use-the-integration}

* [Adobe Commerce](https://business.adobe.com/it/products/magento/magento-commerce.html) 2.4.7+. Per i requisiti dettagliati, vedere [Requisiti di sistema](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/system-requirements).

* Licenza [!DNL Commerce Optimizer] con istanza sandbox predisposta.

* [Chiavi di autenticazione](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) per scaricare il metapacchetto del connettore tramite Compositore.

* Accesso amministratore a un&#39;istanza [[!DNL Commerce Optimizer] sandbox](../optimizer/get-started.md).

L&#39;utente [!DNL Adobe Commerce] che configura l&#39;integrazione deve avere:

* Accesso amministratore all’amministrazione di Commerce.

* [Accesso alla riga di comando al  [!DNL Adobe Commerce] server applicazioni](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/project/user-access).

* Accesso per sviluppatori all&#39;organizzazione [IMS](https://experienceleague.adobe.com/it/docs/core-services/interface/administration/organizations?) in cui è stato eseguito il provisioning del progetto [!DNL Commerce Optimizer].

>[!BEGINSHADEBOX]

## Rimuovere le estensioni in conflitto

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## Passaggi di configurazione {#configuration-steps}

Per abilitare [!DNL Adobe Commerce Optimizer Connector] e iniziare la sincronizzazione dei dati da [!DNL Adobe Commerce] all&#39;istanza [!DNL Commerce Optimizer], eseguire la procedura seguente.

1. **[Installa il  [!DNL Adobe Commerce Optimizer Connector] pacchetto](#install-the-adobe-commerce-optimizer-connector-package)** utilizzando Composer per connettere l&#39;istanza [!DNL Adobe Commerce] a [!DNL Commerce Optimizer].

1. **[Personalizzare la configurazione di esportazione degli ambiti di Commerce](#customize-the-commerce-scopes-export-configuration)** dall&#39;amministratore.

1. **[Abilita l&#39;integrazione [!DNL Commerce Optimizer] &#x200B;](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verificare che la sincronizzazione dei dati funzioni](#verify-that-the-data-sync-is-working)**.

## Installa il pacchetto [!DNL Adobe Commerce Optimizer Connector] {#install-the-adobe-commerce-optimizer-connector-package}

[!DNL Adobe Commerce Optimizer Connector] viene consegnato come metapacchetto Compositore disponibile per tutti i commercianti Commerce con una licenza attiva per [!DNL Commerce Optimizer].

### Passaggi per l’installazione

1. Aggiungi il modulo `adobe-commerce/commerce-data-export-aco-adapter` tramite Compositore:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Distribuire le modifiche nell&#39;ambiente di staging [!DNL Adobe Commerce].

   Al termine della distribuzione, l&#39;opzione [!DNL Commerce Optimizer] è disponibile nel menu di amministrazione di Commerce. Seleziona **[!UICONTROL Commerce Optimizer]** per aprire l&#39;istanza di [!DNL Commerce Optimizer] direttamente dall&#39;amministratore di Commerce.

{{install-extension-links}}

## Personalizzare la configurazione di esportazione degli ambiti di Commerce {#customize-the-commerce-scopes-export-configuration}

Per impostazione predefinita, la sincronizzazione dei dati del catalogo è abilitata per tutti gli ambiti di Commerce (siti Web, gruppi di clienti e visualizzazioni archivio). È possibile personalizzare le impostazioni di esportazione per sincronizzare i dati solo per ambiti specifici in base alle esigenze aziendali. Ad esempio, se più visualizzazioni archivio condividono la stessa lingua, è possibile esportare i dati per una visualizzazione archivio e utilizzarli come [origine catalogo](../optimizer/setup/catalog-sources.md) per più visualizzazioni catalogo in [!DNL Commerce Optimizer].

>[!IMPORTANT]
>
>La modifica delle impostazioni di esportazione attiva una reindicizzazione completa, che può richiedere molto tempo a seconda delle dimensioni del catalogo. Adobe consiglia di configurare gli ambiti Commerce da sincronizzare con [!DNL Commerce Optimizer] prima di abilitare l&#39;integrazione e avviare la sincronizzazione dati iniziale.

Nella tabella seguente vengono descritti i dati esportati a ogni livello di ambito:

| Ambito | Dati esportati | Note |
| ----- | ------------- | ----- |
| Sito web e gruppo di clienti | Prezzi e listini prezzi | Ogni set di prezzi viene esportato come [listino prezzi](../optimizer/setup/pricebooks.md) utilizzando la convenzione di denominazione `&lt;website&gt;::&lt;SHA1 of customer group ID&gt;`. Sono inclusi tutti i gruppi di clienti per il sito Web. |
| Visualizzazione store | Prodotti e attributi del prodotto | Ogni visualizzazione archivio crea una [origine catalogo](../optimizer/setup/catalog-sources.md) separata in [!DNL Commerce Optimizer]. |

![Archivia griglia con impostazioni di sincronizzazione Commerce Optimizer](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

### Per modificare le impostazioni di esportazione dell&#39;ambito

1. In Amministrazione Commerce, vai a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Seleziona la visualizzazione del sito web o store che desideri configurare.

1. Nelle impostazioni dell&#39;utilità di esportazione **[!DNL Commerce Optimizer]**, utilizzare la casella di controllo per abilitare o disabilitare la sincronizzazione dei dati in base alle esigenze.

   ![Aggiorna configurazione sincronizzazione dati](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. Salva le modifiche.

### Attivare e disattivare il comportamento

| Azione | Risultato |
| -------- | -------- |
| Disattiva una visualizzazione store | **La disabilitazione della sincronizzazione rimuove i dati del catalogo dalla vetrina.** L&#39;origine del catalogo rimane in [!DNL Commerce Optimizer], ma tutti i dati sincronizzati vengono rimossi alla successiva esecuzione cron. |
| Disattiva e riattiva la visualizzazione dello store | La stessa origine del catalogo viene ripopolata con una risincronizzazione completa dei dati. |

## Abilita l&#39;integrazione di [!DNL Commerce Optimizer] {#enable-the-adobe-commerce-optimizer-integration}

Abilitare l&#39;integrazione e avviare la sincronizzazione dei dati eseguendo il comando CLI `aco:config:init`. Questo comando completa i passaggi seguenti:

1. Ottiene un token di accesso IMS utilizzando le credenziali fornite come argomenti della riga di comando.
1. Chiama il servizio Commerce Cloud Manager (CCM) in `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` per convalidare il tenant ed estrarre l&#39;URL di acquisizione e l&#39;URL di [!DNL Commerce Optimizer] Studio.
1. Salva tutta la configurazione (segreto client crittografato) in `core_config_data`.
1. Pianifica la sincronizzazione completa iniziale invalidando tutti gli indicizzatori di feed [!DNL Commerce Optimizer].


{{aco-data-sync-processing-note}}

## Ottieni i dettagli di connessione richiesti

{{$include /help/_includes/aco-connector/connection-details.md}}

### Ottieni dettagli istanza [!DNL Commerce Optimizer]

{{$include /help/_includes/aco-connector/configure-connection.md}}

## Verifica che la sincronizzazione dei dati funzioni {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Passaggi successivi

1. **Configura [!DNL Commerce Optimizer] visualizzazioni catalogo e criteri**

   Creare visualizzazioni e criteri catalogo nell&#39;interfaccia utente [!DNL Commerce Optimizer]. I listini prezzi vengono creati automaticamente da [!DNL Adobe Commerce] gruppi di clienti. Per istruzioni, vedere la documentazione [Visualizzazioni catalogo](../optimizer/setup/catalog-view.md) e [Criteri](../optimizer/setup/policies.md) nella Guida utente *[!DNL Commerce Optimizer]*. Per limitare l&#39;accesso a una visualizzazione catalogo, vedere [Visualizzazioni catalogo privato](../optimizer/setup/private-catalog-view.md).

1. **Configura una vetrina Commerce su[!DNL Edge Delivery Services]**

   Per connettere la vetrina all&#39;istanza [!DNL Commerce Optimizer] e iniziare a distribuire esperienze e-commerce personalizzate, segui la [documentazione di configurazione della vetrina](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}.
