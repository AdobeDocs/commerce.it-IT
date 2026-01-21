---
title: Note sulla versione di [!DNL Adobe Commerce as a Cloud Service]
description: Scopri le funzionalità e i miglioramenti più recenti in [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: b8a2ea53f686cc92e380afeb39c467338f91f991
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Note sulla versione

Le seguenti note sulla versione contengono aggiornamenti a [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Se utilizzi Adobe Commerce on-premise o Adobe Commerce sull&#39;infrastruttura cloud, consulta le [note sulla versione di Adobe Commerce](https://experienceleague.adobe.com/it/docs/commerce-operations/release/notes/overview).

## Gennaio 2026 {#latest}

[!BADGE Produzione]{type=Neutral tooltip="Gli elementi elencati sono attualmente disponibili negli ambienti di produzione."}

I seguenti elementi sono stati rilasciati negli ambienti di produzione di [!DNL Adobe Commerce as a Cloud Service] il 20 gennaio 2026.

>[!BEGINSHADEBOX]

### Miglioramenti all’autenticazione

I token di accesso per l’autenticazione dell’amministratore Adobe IMS ora sono accettati solo tramite richieste POST. <!-- CCSAAS-4421 -->

### Eliminazioni B2B

Sono state apportate le seguenti modifiche ai componenti di rilascio B2B:

* [!DNL Commerce Storefront on Edge Delivery Services] ora include [componenti di eliminazione B2B](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=it). Sono ora disponibili i seguenti menu a discesa B2B:

   * **Gestione società** - Abilita la gestione del profilo società e le autorizzazioni basate sui ruoli per le vetrine di Adobe Commerce.
   * **Commutatore società** - Fornisce un componente dell&#39;interfaccia utente che consente agli utenti di passare da un&#39;azienda all&#39;altra a cui sono associati.
   * **Ordini di acquisto** - Gestisce i flussi di lavoro degli ordini di acquisto, le regole di approvazione e la cronologia degli ordini di acquisto per le transazioni B2B.
   * **Gestione dei preventivi** - Abilita i preventivi negoziabili per i clienti B2B con flussi di lavoro di richiesta, negoziazione e approvazione dei preventivi.
   * **Elenchi di richieste** - Fornisce gli strumenti per la creazione e la gestione degli elenchi di richieste per acquisti ripetuti e ordini in blocco.

     >[!NOTE]
     >
     >La documentazione dettagliata dei componenti B2B da rilasciare sarà disponibile quando questa funzione verrà promossa in Produzione.

* È stato rilasciato il pacchetto di compatibilità per la vetrina B2B. Questo pacchetto migliora lo schema GraphQL B2B di [!DNL Adobe Commerce] per migliorare lo sviluppo dei sistemi B2B.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/?lang=it). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### Collegamenti cliccabili ai tracker di spedizione esterni

Trasforma i numeri di tracciamento della spedizione inclusi nelle e-mail dei clienti da testo normale in collegamenti cliccabili [abilitando gli URL di tracciamento personalizzati](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Questa funzionalità è supportata per USPS, UPS, FedEx e DHL. <!-- See PR #716 in commerce-admin -->

### Supporto di Google reCAPTCHA Enterprise

[!DNL Adobe Commerce as a Cloud Service] storefront ora supportano [reCAPTCHA Enterprise](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Questa funzione offre una protezione avanzata dei bot utilizzando l’analisi adattiva dei rischi e l’apprendimento automatico per distinguere con precisione gli utenti umani dai bot automatizzati. Rafforza la sicurezza del sito, impedisce le attività fraudolente e riduce lo spam e gli abusi per mantenere un’esperienza di acquisto affidabile. <!-- CCSAAS-4242 -->

### Accesso amministratore specifico per istanza

Ora puoi [assegnare agli utenti l&#39;accesso](./user-management.md#add-users) alle singole [!DNL Adobe Commerce as a Cloud Service] istanze in Admin Console. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### Osservabilità

Ottieni una visibilità più approfondita nell&#39;istanza [!DNL Adobe Commerce as a Cloud Service] con [Osservabilità OpenTelemetry](https://developer.adobe.com/commerce/extensibility/observability/), ora disponibile automaticamente. OpenTelemetry fornisce metriche, registri e tracce che consentono di monitorare le prestazioni, risolvere più rapidamente i problemi e ottimizzare la vetrina. Questa funzionalità consente di ottenere informazioni proattive sullo stato del sistema e migliora l’affidabilità per i clienti.

### Determinazione prezzi a livello per le regole di prezzo catalogo

È ora possibile combinare gli sconti per prezzi su più livelli con gli sconti delle regole di catalogo utilizzando [regole di prezzo catalogo](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). Questo miglioramento consente di creare strategie di prezzo più dinamiche e competitive, premiando gli acquisti in blocco e applicando contemporaneamente sconti promozionali. Il risultato è una maggiore flessibilità per attrarre clienti, aumentare il valore dell&#39;ordine e favorire le conversioni.<!-- See PR #708 in commerce-admin -->

### Miglioramenti e correzioni di bug

I miglioramenti, le ottimizzazioni e le correzioni di bug seguenti inclusi in questa versione:

* È stato risolto un errore che poteva verificarsi durante il caricamento di un file in S3. <!-- CCSAAS-4189 -->

* È stato risolto un errore `User is not entitled to access this instance` che poteva verificarsi quando si accedeva all&#39;amministrazione di Commerce o all&#39;API REST. <!-- CCSAAS-4324 -->

* È stato corretto un errore che si verificava durante l’anteprima o l’accodamento di una newsletter dalla griglia del modello della newsletter. <!-- CCSAAS-4398 -->

* È stato corretto un errore `404` che si verificava facendo clic sul pulsante [!UICONTROL **Ricarica dati**] nel dashboard di amministrazione. <!-- CCSAAS-4468 -->

* È stato risolto un problema che impediva l&#39;aggiornamento degli attributi personalizzati del prodotto tramite l&#39;API REST quando [!DNL AEM Assets integration] era abilitato e il prodotto conteneva immagini. <!-- ACAP-1178 -->

* Vari miglioramenti a livello di prestazioni e ottimizzazione.<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Novembre 2025

>[!BEGINSHADEBOX]

### Miglioramenti

* [Gestione utenti](./user-management.md) - È stato modificato il ruolo **Amministratore prodotti** in Admin Console per aggiornare automaticamente l&#39;accesso degli utenti all&#39;Amministratore Commerce. <!-- CCSAAS-3012 -->

* È stata aggiunta la possibilità di caricare e recuperare in Amazon S3 allegati di preventivi negoziabili nonché file e immagini associati a clienti e indirizzi dei clienti utilizzando URL prefirmati in [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) e [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). Con REST è possibile caricare anche immagini di categorie. <!-- CCSAAS-3250 -->

* Sono stati aggiunti gli endpoint `POST /V1/customers` e `PUT /V1/customers/{customerId}` all&#39;[API REST](https://developer.adobe.com/commerce/webapi/rest/reference/) per creare e aggiornare i clienti. Questi endpoint richiedono l’autorizzazione dell’amministratore. <!-- CCSAAS-3112 -->

* È stata aggiunta la mutazione [`exchangeOtpForCustomerToken`](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), che richiede l&#39;indirizzo e-mail di un acquirente e una password monouso (OTP) e riceve in cambio un token cliente. Questa mutazione viene generalmente utilizzata in scenari in cui un cliente deve eseguire l’autenticazione utilizzando un OTP inviato alla propria e-mail o al proprio telefono.

* Se un indirizzo definito nella schermata di configurazione [!UICONTROL **Archivia indirizzi e-mail**] nell&#39;amministratore contiene un valore che termina con `example.com`, Commerce non invia e-mail a questo indirizzo. Il sistema invece registra che l’e-mail non è stata inviata.  <!-- CCSAAS-3533 -->

#### Attributi ordine personalizzati

* Gli utenti amministratori ora possono visualizzare e modificare [attributi dell&#39;ordine personalizzati](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) direttamente dalle schermate Visualizzazione ordine, Modifica e Crea nel pannello Amministratore. Questo miglioramento migliora la gestione dei dati degli ordini personalizzati creati tramite GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
