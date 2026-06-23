---
source-git-commit: 10a91a91337778648e99078bcbf0c9ef25a49f86
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---
# snippet Commerce

## Nota di installazione per l’estensione dello stato di sincronizzazione dei feed di dati {#install-data-sync-feed-status}

>[!NOTE]
>
>Se la pagina Stato di sincronizzazione feed dati non è disponibile in Commerce Admin for Commerce on Cloud o nelle distribuzioni locali, segui le [istruzioni di installazione dell&#39;estensione](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status#install-the-extension){target="_blank"} per abilitarla.


## Allineamento dell’ambiente di integrazione di Adobe Commerce Optimizer {#aco-integration-environment-alignment}

>[!IMPORTANT]
>
>Collega sempre le istanze Sandbox Optimizer agli ambienti non di produzione e le istanze di produzione agli ambienti di produzione. Gli ambienti non corrispondenti causano incoerenza nei dati di catalogo, nei risultati di ricerca e nei consigli.


## Servizi di merchandising per Optimizer {#aco-merchandising-services}

>[!NOTE]
>
>Per le soluzioni Commerce che utilizzano Adobe Commerce Optimizer o il connettore Adobe Commerce Optimizer, utilizzare l&#39;API GraphQL [Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api/) invece dell&#39;API GraphQL Catalog Service.

## Controllo sincronizzazione dati per Optimizer {#aco-data-sync-verification}

>[!NOTE]
>
>Per le distribuzioni che utilizzano [[!DNL Adobe Commerce Optimizer Connector]](../aco-connector/overview.md) per esportare i dati del catalogo in [!DNL Adobe Commerce Optimizer], verificare la sincronizzazione dei dati del catalogo utilizzando la [pagina Stato sincronizzazione feed dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) in Amministrazione Commerce e la [pagina Sincronizzazione dati](../optimizer/setup/data-sync.md) in [!DNL Adobe Commerce Optimizer Studio], non il [dashboard di gestione dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard).

## Nota di rilascio di Adobe Commerce Optimizer per gli aggiornamenti API {#aco-api-updates-and-dropins}

>[!NOTE]
>
>[Componenti di eliminazione](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=it) per [!DNL Commerce Storefront on Edge Delivery Services] rilevano automaticamente le modifiche GraphQL più recenti (nuovi campi, limiti e comportamento di query).

## Accesso anticipato ACS {#accs-early-access}

>[!NOTE]
>
>Questa documentazione descrive un prodotto in fase di sviluppo con accesso anticipato e non riflette tutte le funzionalità previste per la disponibilità generale.

<!--
## Nav hack ACCS {#nav-hack-accs}

>[!BEGINSHADEBOX]

<table style="table-layout:fixed">
  <tr>
    <td style="vertical-align: middle;"><a href="https://developer.adobe.com/commerce/webapi/"><img alt="Developers" src="../assets/icons/developers.svg" /> <strong>Developers</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/?lang=it"><img alt="Storefront" src="../assets/icons/storefront.svg" /> <strong>Storefront</strong></a></td>
    <td style="vertical-align: middle;"><a href="../cloud-service/overview.md"><img alt="Merchants" src="../assets/icons/merchants.svg" /> <strong>Merchants</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/getting-started/commerce-as-a-cloud-service/overview"><img alt="Videos" src="../assets/icons/videos.svg" /> <strong>Videos</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/playgrounds/commerce-services/?lang=it"><img alt="Playgrounds" src="../assets/icons/playgrounds.svg" /> <strong>Playgrounds</strong></a></td>
  </tr>
</table>

>[!ENDSHADEBOX]
-->

## Funzionalità sperimentale solo sandbox ACCS {#accs-sandbox-experimental}

>[!IMPORTANT]
>
>Questa funzione è sperimentale ed è disponibile solo negli ambienti Sandbox di [!DNL Adobe Commerce as a Cloud Service].
>
>Questa funzione è soggetta a modifiche senza preavviso.

[!BADGE Sandbox]{type=Caution tooltip="Gli elementi elencati sono attualmente disponibili solo negli ambienti Sandbox. Adobe rende disponibili le nuove versioni negli ambienti Sandbox per fornire il tempo di testare le modifiche imminenti prima che la versione sia disponibile negli ambienti di produzione."}

## Mappatura dell’istanza di AEM Assets {#aem-assets-instance-mapping}

>[!NOTE]
>
>Quando connetti [!DNL Adobe Commerce as a Cloud Service] a [!DNL AEM Assets], l&#39;istanza di Stage [!DNL AEM Assets] viene mappata all&#39;istanza Sandbox [!DNL Adobe Commerce as a Cloud Service] e a qualsiasi altro ambiente non di produzione. L&#39;istanza di produzione [!DNL AEM Assets] è mappata all&#39;istanza di produzione [!DNL Adobe Commerce as a Cloud Service].

## Informazioni sull’identità IMS e sul single sign-on {#ims-identity-and-sso-config}

La gestione e l’autenticazione delle identità di Adobe Commerce sono gestite da Adobe Identity Management System (IMS) tramite Adobe Admin Console.

Per informazioni sulle opzioni di configurazione delle identità, tra cui Adobe ID, Enterprise ID e Federated ID, e sulle istruzioni per la configurazione del Single Sign-On (SSO) per l&#39;accesso sicuro alle app Adobe, vedi [Configurare l&#39;identità e il Single Sign-On](https://helpx.adobe.com/it/enterprise/using/set-up-identity.html) nella documentazione di *Enterprise Admin Console*.

## Note sulla versione di Servizi ACCS ed estensibilità {#accs-release}

### Note aggiuntive sulla versione

[!DNL Adobe Commerce as a Cloud Service] contiene le versioni più recenti di servizi di merchandising, servizi di pagamento e versioni di estensibilità. Utilizza i seguenti collegamenti per visualizzare le note sulla versione di ciascuno:

| Servizi | Estensibilità | Vetrina |
| --- | --- | --- |
| <ul><li>[Servizio catalogo](../catalog-service/release-notes.md)</li><li>[Live Search](../live-search/release-notes.md)</li><li>[Servizi di pagamento](../payment-services/release-notes.md)</li><li>[Consigli di prodotto](../product-recommendations/release-notes.md)</li><li>[Esportazione dati SaaS](../data-export/release-notes.md)</li></ul> | <ul><li>[SDK interfaccia utente amministratore](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)</li><li>[Mesh API](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)</li><li>[Eventi](https://developer.adobe.com/commerce/extensibility/events/release-notes/)</li><li>[Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)</li></ul> | <ul><li>[Informazioni sulla versione](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=it)</li><li>[Registro modifiche](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=it)</li></ul> |

## Note sulla versione di Adobe Commerce Optimizer Services {#aco-release}

### Note aggiuntive sulla versione

[!DNL Adobe Commerce Optimizer] funziona con le ultime versioni dell&#39;integrazione AEM Assets, il connettore Commerce Optimizer e [!DNL Adobe Commerce Storefront]. Utilizza i seguenti collegamenti per visualizzare le note sulla versione per ogni area:

| Servizi | Vetrina |
| --- | --- |
| [Integrazione AEM Assets](../aem-assets-integration/release-notes.md)<br>[Connettore Commerce Optimizer](../aco-connector/release-notes.md) | [Informazioni sulla versione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/releases/?lang=it)<br>[Storefront changelog](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/?lang=it) |
