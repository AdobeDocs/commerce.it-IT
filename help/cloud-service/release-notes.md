---
title: Note sulla versione di [!DNL Adobe Commerce as a Cloud Service]
description: Scopri le funzionalità e i miglioramenti più recenti in [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 1ce3b6b6b94b1b4e94c0d34c081dec2884d7f0f8
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Note sulla versione

Le seguenti note sulla versione contengono aggiornamenti a [!DNL Adobe Commerce as a Cloud Service]. Per informazioni sulla versione di altri prodotti, consulta [Adobe Commerce Optimizer](../optimizer/release-notes.md) o [Adobe Commerce on-premise e Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

[!DNL Adobe Commerce as a Cloud Service] contiene le versioni più recenti di servizi di merchandising, servizi di pagamento e versioni di estensibilità. Utilizza i seguenti collegamenti per visualizzare le note sulla versione di ciascuno:

* Servizi
   * [Servizio catalogo](../catalog-service/release-notes.md)
   * [Live Search](../live-search/release-notes.md)
   * [Servizi di pagamento](../payment-services/release-notes.md)
   * [Consigli di prodotto](../product-recommendations/release-notes.md)
   * [Esportazione dati SaaS](../data-export/release-notes.md)
* Estensibilità
   * [SDK interfaccia utente amministratore](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)
   * [Mesh API](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)
   * [Eventi](https://developer.adobe.com/commerce/extensibility/events/release-notes/)
   * [Webhook](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)

## Novembre 2025

>[!BEGINSHADEBOX]

### Miglioramenti

* [Gestione utenti](./user-management.md) - È stato modificato il ruolo **Amministratore prodotti** in Admin Console per aggiornare automaticamente l&#39;accesso degli utenti all&#39;Amministratore Commerce. <!-- CCSAAS-3012 -->

* È stata aggiunta la possibilità di caricare e recuperare in Amazon S3 allegati di preventivi negoziabili nonché file e immagini associati a clienti e indirizzi dei clienti utilizzando URL prefirmati in [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) e [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). Con REST è possibile caricare anche immagini di categorie. <!-- CCSAAS-3250 -->

* Sono stati aggiunti gli endpoint `POST /V1/customers` e `PUT /V1/customers/{customerId}` all&#39;[API REST](https://developer.adobe.com/commerce/webapi/rest/reference/) per creare e aggiornare i clienti. Questi endpoint richiedono l’autorizzazione dell’amministratore. <!-- CCSAAS-3112 -->

* È stata aggiunta la mutazione [`exchangeOtpForCustomerToken`](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), che richiede l&#39;indirizzo e-mail di un acquirente e una password monouso (OTP) e riceve in cambio un token cliente. Questa mutazione viene generalmente utilizzata in scenari in cui un cliente deve eseguire l’autenticazione utilizzando un OTP inviato alla propria e-mail o al proprio telefono.

* Se un indirizzo definito nella schermata di configurazione [!UICONTROL **Archivia indirizzi e-mail**] nell&#39;amministratore contiene un valore che termina con `example.com`, Commerce non invia e-mail a questo indirizzo. Il sistema invece registra che l’e-mail non è stata inviata.  <!-- CCSAAS-3533 -->

#### Attributi ordine personalizzati

* Gli utenti amministratori ora possono visualizzare e modificare [attributi dell&#39;ordine personalizzati](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) direttamente dalle schermate Visualizzazione ordine, Modifica e Crea nel pannello Amministratore. Questo miglioramento migliora la gestione dei dati degli ordini personalizzati creati tramite GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
