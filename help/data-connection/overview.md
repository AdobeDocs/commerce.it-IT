---
title: Introduzione a [!DNL Data Connection]
description: Scopri come integrare i dati di Adobe Commerce con Adobe Experience Platform utilizzando l’estensione  [!DNL Data Connection] .
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
TQID: https://experienceleague.adobe.com/-wfkGM2isTVmAaJokndxVy0-UtZ4pM9msYXmh2IE-Hc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 5ba5dfa23580b5eefa8271277e78c6ea67879b90
workflow-type: tm+mt
source-wordcount: 1373
ht-degree: 1%

---

# Introduzione a [!DNL Data Connection]

>[!IMPORTANT]
>
>Il connettore Experience Platform è stato rinominato in [!DNL Data Connection].

L&#39;estensione [!DNL Data Connection] collega l&#39;istanza Web Adobe Commerce a Adobe Experience Platform e Edge Network. Per gli sviluppatori di app mobili, utilizzi Adobe Experience Platform Mobile SDK con Commerce per acquisire e inviare dati Commerce ad Experience Platform. [Ulteriori informazioni](./mobile-sdk-epc.md).

I commercianti multisito possono configurare le impostazioni [!DNL Data Connection] applicabili per sito Web, inclusa la selezione della sandbox di Experience Platform. Vedere [Connettere i dati di Commerce a Adobe Experience Platform](connect-data.md#configuration-scope) per i campi globali rispetto ai campi con ambito sito Web.

Lo store Commerce contiene molti dati. Le informazioni su come gli acquirenti navigano, visualizzano e infine acquistano i prodotti sul sito possono rivelare opportunità per creare un’esperienza di acquisto più personalizzata. Anche se tali dati possono informare le funzioni native di Commerce, come le regole di prezzo del carrello e i blocchi dinamici, i dati rimangono in silos nell’istanza Commerce.

Adobe Experience Platform offre una suite di tecnologie che, se utilizzate con i dati provenienti dal tuo store Commerce, possono distribuire attraverso Edge Network ad altri prodotti Adobe DX per conoscere il comportamento d’acquisto dei tuoi acquirenti. Con queste informazioni approfondite, puoi creare un’esperienza di acquisto più personalizzata su tutti i canali.

L&#39;immagine seguente mostra il flusso di dati Commerce dallo store ad altri prodotti Adobe DX quando l&#39;estensione [!DNL Data Connection] viene installata e configurata.

![Flusso dei dati verso il server Edge di Experience Platform](assets/commerce-edge.png)

Nell’immagine precedente, i dati comportamentali, di back office e del profilo cliente vengono inviati ad Experience Platform Edge utilizzando un SDK, un’API e un connettore di origine. Non è necessario comprendere appieno il funzionamento di tali parti, in quanto l’estensione gestisce automaticamente la complessità della condivisione dei dati. Quando i dati dell&#39;evento si trovano nel perimetro, è possibile utilizzarli nei prodotti Adobe DX downstream come [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it), [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html?lang=it) e [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=it). Per esempi guidati, consulta [Utilizzare Adobe Journey Optimizer per inviare un&#39;e-mail del carrello abbandonata](using-ajo.md) e [Creare un pubblico in Real-Time CDP utilizzando i dati evento di Commerce](create-audience.md).

## Recuperare i dati di Experience Platform in Commerce

L&#39;invio dei dati Commerce ad Experience Platform tramite l&#39;estensione [!DNL Data Connection] rappresenta un lato delle funzionalità di condivisione dei dati di Commerce. L&#39;altro lato, che è un&#39;estensione facoltativa, è denominato [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=it). Questa estensione consente di creare tipi di pubblico in Real-Time CDP e distribuirli nel tuo store di Commerce per informarti sulle regole di prezzo del carrello, sulle regole di prodotto correlate e sui blocchi dinamici.

Ad alto livello, il flusso di dati dall’archivio Commerce ad Experience Platform e viceversa attraverso l’estensione Audience Activation si presenta come segue:

![[!DNL Data Connection] flusso](assets/data-connection.png)

Dopo aver impostato la connessione tra Commerce ad Experience Platform e Experience Platform a Commerce, i dati continuano a scorrere. Non è necessario riconnettersi, a meno che non sia richiesto da un aggiornamento.

## Concetti

La condivisione di dati tra questi due sistemi richiede la comprensione di diversi concetti.

- **Tipi di dati** - [!DNL Data Connection] raccoglie dati **comportamentali (vetrina)** dal browser, **dati back office** dai server Commerce e **dati profilo**. La raccolta vetrina delle etichette amministratore **Eventi vetrina**. Per la tassonomia completa, vedere [Tipi di dati Commerce](data-ingestion.md).

- **Dati comportamentali (storefront)** - Acquisiti dalle interazioni dell&#39;acquirente sul sito, ad esempio `addToCart`, `pageView`, `startCheckout` e `completeCheckout`. Vedi [eventi vetrina](events.md#storefront-events).

- **Dati di back office** — Acquisiti sui server Commerce, inclusi [eventi di stato dell&#39;ordine](events-backoffice.md#order-status) come [`orderPlaced`](events-backoffice.md#orderplaced) e [`orderShipped`](events-backoffice.md#ordershipmentcompleted). Consulta [eventi di back office](events-backoffice.md).

- **Record profilo** - Dati snapshot inviati quando viene creato un profilo cliente in Commerce. Consulta [record profilo](events-profilerecord.md) e [Aggiorna schema record profilo](profile-data.md).

- **Eventi profilo** — Eventi serie temporali per le modifiche del ciclo di vita del profilo sul server. Vedi [eventi profilo cliente](events-backoffice.md#customer-profile-events).

- **Experience Platform e Edge Network**: data warehouse per la maggior parte dei prodotti Adobe DX. I dati inviati ad Experience Platform vengono propagati ai prodotti Adobe DX tramite Experience Platform Edge Network. Ad esempio, puoi avviare Journey Optimizer, recuperare i dati di un evento Commerce specifico dal server Edge di e creare un’e-mail del carrello abbandonato in Journey Optimizer. Journey Optimizer può quindi inviare l&#39;e-mail in caso di carrelli abbandonati nel Commerce store. Ulteriori informazioni su [Experience Platform e Edge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html?lang=it).

- **Schema** - Lo schema descrive la struttura dei dati inviati. Prima che Experience Platform possa acquisire i dati Commerce, è necessario comporre uno schema per descrivere la struttura dei dati e fornire vincoli per il tipo di dati che possono essere contenuti all’interno di ciascun campo. Gli schemi sono costituiti da una classe base e da zero o più gruppi di campi schema. Lo schema utilizza la struttura XDM, che può essere letta da tutti i prodotti Adobe DX. Lo schema garantisce che i dati inviati all’Experience Platform siano compresi in tutti i prodotti DX. Ulteriori informazioni su [schemi](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it).

- **Set di dati**: costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella contenente uno schema (colonne) e campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati. Tutti i dati acquisiti correttamente in Adobe Experience Platform sono contenuti all’interno dei set di dati. Ulteriori informazioni sui [set di dati](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=it).

- **Datastream** - ID che consente il flusso di dati da Adobe Experience Platform ad altri prodotti Adobe DX. Questo ID deve essere associato a un sito web specifico all’interno della tua istanza Adobe Commerce specifica. Quando crei questo flusso di dati, specifica lo schema XDM creato in precedenza. Ulteriori informazioni su [flussi di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=it).

## Architettura supportata

L&#39;estensione [!DNL Data Connection] è disponibile nelle seguenti architetture:

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html?lang=it)

>[!BEGINSHADEBOX]

## Prerequisiti

Per utilizzare l&#39;estensione [!DNL Data Connection], è necessario disporre dei seguenti elementi:

- Adobe Commerce 2.4.4 o versione successiva
- Adobe ID e ID organizzazione
- [Adobe Client Data Layer (ACDL)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=it), necessario per raccogliere i dati evento storefront
- Diritti ad altri prodotti Adobe DX.

>[!ENDSHADEBOX]

## Abilitare l’estensione {#enable-extension}

A un livello avanzato, l&#39;abilitazione dell&#39;estensione [!DNL Data Connection] prevede i seguenti passaggi:

1. [Installa](install.md) l&#39;estensione [!DNL Data Connection].
1. [Accedi](https://helpx.adobe.com/it/manage-account/using/access-adobe-id-account.html) al tuo account Adobe e [visualizza per confermare](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=it#concept_EA8AEE5B02CF46ACBDAD6A8508646255) l&#39;ID organizzazione. L’ID organizzazione è l’ID associato all’azienda con provisioning di Experience Cloud. Questo ID è una stringa alfanumerica composta da 24 caratteri, seguita da (deve includere) `@AdobeOrg`.
1. Assicurati di disporre dell&#39;autorizzazione [per la raccolta dati in Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=it).
1. Rivedi i [tipi di dati](data-ingestion.md) che puoi raccogliere e inviare.
1. Crea o aggiorna lo [schema evento serie temporali](update-xdm.md) o lo [schema dati record profilo](profile-data.md) con gruppi di campi specifici di Commerce.
1. [Crea un set di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=it#create-a-dataset) in base allo schema creato o aggiornato. Questo set di dati contiene i dati Commerce inviati ad Experience Platform Edge.
1. [Crea un flusso di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=it) e seleziona lo schema XDM che contiene i gruppi di campi specifici di Commerce.
1. [Connetti a Servizi Commerce](../landing/saas.md).
1. [Connetti a Adobe Experience Platform](connect-data.md).

Il resto di questa guida illustra in modo più dettagliato tutti questi passaggi, consentendoti di imparare a usare al meglio e iniziare a utilizzare la potenza dei prodotti Adobe DX nel tuo store Commerce.

>[!NOTE]
>
>Per gli sviluppatori di dispositivi mobili, scopri come [integrare](./mobile-sdk-epc.md) Adobe Experience Platform Mobile SDK con Commerce.

## Preparazione HIPAA

L&#39;estensione [!DNL Data Connection] consente di condividere [!DNL Commerce] dati di back office con Experience Platform e di mantenere la conformità HIPAA. [Ulteriori informazioni](hipaa-readiness.md).

## Pubblico

Questa guida è stata progettata per i commercianti di Adobe Commerce che desiderano arricchire e personalizzare il proprio negozio Commerce per migliorare l’esperienza di acquisto dei loro clienti.

## Supporto

Se hai bisogno di informazioni o hai domande che non sono trattate in questa guida, utilizza le risorse seguenti:

- [Centro assistenza](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html?lang=it){target="_blank"}
- [Ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=it#submit-ticket){target="_blank"} - Invia un ticket per ricevere ulteriore assistenza.
