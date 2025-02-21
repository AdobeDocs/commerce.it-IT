---
title: Onboarding e installazione
description: Scopri come installare [!DNL Catalog Service]
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Onboarding e installazione

Installa Catalog Service per richiedere e ricevere i dati di prodotto da un&#39;istanza di Commerce utilizzando l&#39;[API GraphQL di Catalog Service](https://developer.adobe.com/commerce/services/graphql/catalog-service/). Catalog Service viene fornito come metapacchetto del compositore dall’archivio repo.magento.com.

>[!NOTE]
>
>Se la tua istanza di Commerce utilizza Live Search o Product Recommendations, il Servizio catalogo viene installato o aggiornato automaticamente quando effettui l’onboarding o l’aggiornamento di tali servizi. Per informazioni dettagliate, vedere le istruzioni di installazione per [Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/install) e [Product Recommendations](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure).



## Requisiti di sistema

**Requisiti software**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3
- Compositore: 2.x

**Piattaforme supportate**

- Adobe Commerce sull’infrastruttura cloud: 2.4.4+
- Adobe Commerce on-premise: 2.4.4+

## Endpoint

[!DNL Catalog Service] ha due endpoint disponibili per l&#39;onboarding:

- Sandbox (`https://catalog-service-sandbox.adobe.io/graphql`): utilizzata per il test e la convalida prima della pubblicazione
- Produzione (`https://catalog-service.adobe.io/graphql`): utilizzato per il traffico in tempo reale per i commercianti e i siti Web Commerce

Tutte le istanze di test di Commerce utilizzano l’endpoint Sandbox.

Esegui tutti i test di carico sull’endpoint Sandbox. Prima di iniziare il test di caricamento, invia un [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) in modo che il team dei servizi possa prevedere il traffico server aggiuntivo.

## Installazione e configurazione

Per iniziare a utilizzare [!DNL Catalog Service] per Adobe Commerce, sono necessari i seguenti passaggi:

- Installa l&#39;estensione del servizio catalogo (`magento/catalog-service`)
- Configurare il servizio e l’esportazione dei dati
- Accedere al servizio

### Installare l’estensione Catalog Service

>[!BEGINSHADEBOX]

**Prerequisito**

- Accedi a [repo.magento.com](https://repo.magento.com) per installare l&#39;estensione. Per generare le chiavi e ottenere i diritti necessari, vedere [Ottenere le chiavi di autenticazione](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Per le installazioni cloud, consulta la [Guida di Commerce sull&#39;infrastruttura cloud](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- Accedere alla riga di comando del server applicazioni Adobe Commerce.

>[!ENDSHADEBOX]

Installare la versione più recente dell&#39;estensione Catalog Services (`magento/catalog-service`) in un&#39;istanza di Adobe Commerce che esegue Adobe Commerce versione 2.4.4 o successiva. Catalog Service viene distribuito come metapacchetto del compositore dall&#39;archivio [repo.magento.com](https://repo.magento.com).

>[!BEGINTABS]

>[!TAB Infrastruttura cloud]

Utilizzare questo metodo per installare [!DNL Catalog Service] per un&#39;istanza di Commerce Cloud.

1. Sulla workstation locale, passa alla directory del progetto per il progetto Adobe Commerce su infrastruttura cloud.

   >[!NOTE]
   >
   >Per informazioni sulla gestione locale degli ambienti di progetto Commerce, vedere [Gestione dei rami con CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) nella _Guida utente di Adobe Commerce on Cloud Infrastructure_.

1. Consulta il ramo dell’ambiente da aggiornare utilizzando Adobe Commerce Cloud CLI.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Aggiungi il modulo Catalog Service.

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Aggiornare le dipendenze del pacchetto.

   ```bash
   composer update "magento/catalog-service"
   ```

1. Modifiche al codice di commit e push per i file `composer.json` e `composer.lock`.

1. Aggiungere, eseguire il commit e inviare le modifiche al codice per i file `composer.json` e `composer.lock` all&#39;ambiente cloud.

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   Il push degli aggiornamenti all&#39;ambiente cloud avvia il [processo di distribuzione cloud di Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) per applicare le modifiche. Controllare lo stato della distribuzione dal [registro distribuzione](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB Locale]

Utilizzare questo metodo per installare [!DNL Catalog Service] per un&#39;istanza locale.

1. Utilizza Composer per aggiungere il modulo Catalog Service al progetto:

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update  "magento/catalog-service"
   ```

1. Aggiorna Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Cancella la cache:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >In alcuni casi, in particolare durante la distribuzione in produzione, potrebbe essere opportuno evitare di cancellare il codice compilato perché potrebbe richiedere del tempo. Prima di apportare qualsiasi modifica, assicurati di eseguire il backup del sistema.

>[!ENDTABS]

### Configurare il servizio e l’esportazione dei dati

Dopo aver installato [!DNL Catalog Service], completa le seguenti attività per integrare il servizio Catalog con l&#39;istanza Adobe Commerce. Questa integrazione consente la sincronizzazione dei dati e la comunicazione tra l’istanza di Commerce, Catalog Service e altri servizi di supporto. La sincronizzazione dei dati è gestita dall&#39;estensione [SaaS Data Export](../data-export/overview.md).

1. Configurare [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) specificando le chiavi API e selezionando uno spazio dati SaaS.

   La configurazione del Connettore servizi Commerce è un processo una tantum necessario per utilizzare i servizi Adobe Commerce come Catalog Service, Live Search e Product Recommendations. Se hai già configurato il connettore per un altro servizio, salta questo passaggio.

1. Eseguire una sincronizzazione dati iniziale dal [dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

   La sincronizzazione iniziale può richiedere da alcuni minuti ad ore, a seconda della dimensione del catalogo. Puoi monitorare lo stato della sincronizzazione dal dashboard Gestione dati. Dopo la sincronizzazione iniziale, il catalogo esporta i dati dei prodotti su base continuativa per mantenere aggiornati i servizi.

   >[!NOTE]
   >
   >È inoltre possibile avviare la sincronizzazione iniziale dalla riga di comando utilizzando Commerce CLI. Vedere [Sincronizzazione iniziale](../data-export/data-export-cli-commands.md#initial-sync) nella _Guida all&#39;esportazione dei dati SaaS_.

Per garantire il corretto funzionamento dell’esportazione del catalogo:

- [Verificare che i processi cron siano in esecuzione](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Verificare che gli indicizzatori siano in esecuzione da [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) o utilizzando il comando CLI di Commerce `bin/magento indexer:info`.
- Verificare che gli indici `Catalog Attributes Feed, Product Feed, Product Overrides Feed` e `Product Variant Feed` siano impostati su `Update by Schedule`.

### Monitoraggio e risoluzione dei problemi di sincronizzazione dei dati

L&#39;amministratore di Commerce può monitorare il processo di sincronizzazione utilizzando [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Utilizza [Commerce CLI](../data-export/data-export-cli-commands.md#troubleshooting) e i registri per gestire il processo e risolverlo.

### Accedere al servizio

L&#39;API GraphQL [!DNL Catalog Service] è accessibile dall&#39;endpoint ` https://catalog-service.adobe.io/graphql` utilizzando i comandi POST su HTTPS.

Nelle query GraphQL, devi specificare più intestazioni HTTP, inclusa la chiave API pubblica aggiunta alla configurazione del connettore di servizi Adobe Commerce nell’amministratore. Per informazioni dettagliate, vedere la documentazione di [Servizi Storefront GraphQL](https://developer.adobe.com/commerce/services/graphql/).

### Configurazione del firewall

Per consentire a [!DNL Catalog Service] di attraversare un firewall, aggiungere `commerce.adobe.io` al inserisco nell&#39;elenco Consentiti di.

## Catalog Service e Mesh API

La rete API [per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) consente agli sviluppatori di integrare API private o di terze parti e altre interfacce con i prodotti Adobe utilizzando Adobe IO.

Per informazioni dettagliate sull&#39;installazione e la configurazione, vedere l&#39;argomento [[!DNL Catalog Service] and API Mesh](mesh.md).

## Dashboard di gestione dati

Per ulteriori informazioni sulla sincronizzazione dei dati di [!DNL Catalog Service], vedere [Dashboard di gestione dei dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).
