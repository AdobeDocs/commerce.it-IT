---
title: Panoramica della guida
description: Scopri come integrare i dati di Adobe Commerce con Adobe Experience Platform utilizzando l’estensione  [!DNL Data Connection] .
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# Introduzione a [!DNL Data Connection]

>[!IMPORTANT]
>
>Il connettore Experience Platform è stato rinominato in [!DNL Data Connection].

L&#39;estensione [!DNL Data Connection] collega l&#39;istanza Web Adobe Commerce a Adobe Experience Platform e Edge Network. Per gli sviluppatori di app mobili, utilizzi Adobe Experience Platform Mobile SDK con Commerce per acquisire e inviare dati Commerce ad Experience Platform. [Ulteriori informazioni](./mobile-sdk-epc.md).

Lo store Commerce contiene molti dati. Le informazioni su come gli acquirenti navigano, visualizzano e infine acquistano i prodotti sul sito possono rivelare opportunità per creare un’esperienza di acquisto più personalizzata. Anche se tali dati possono informare le funzioni native di Commerce, come le regole di prezzo del carrello e i blocchi dinamici, i dati rimangono in silos nell’istanza Commerce.

Adobe Experience Platform offre una suite di tecnologie che, se utilizzate con i dati provenienti dal tuo store Commerce, possono distribuire attraverso Edge Network ad altri prodotti Adobe DX per conoscere il comportamento d’acquisto dei tuoi acquirenti. Con queste informazioni approfondite, puoi creare un’esperienza di acquisto più personalizzata su tutti i canali.

L&#39;immagine seguente mostra il flusso di dati Commerce dallo store ad altri prodotti Adobe DX quando l&#39;estensione [!DNL Data Connection] viene installata e configurata.

![Flusso dei dati verso il server Edge di Experience Platform](assets/commerce-edge.png)

Nell’immagine precedente, i dati comportamentali, di back office e del profilo cliente vengono inviati ad Experience Platform Edge utilizzando un SDK, un’API e un connettore di origine. Non è necessario comprendere appieno il funzionamento di tali parti, in quanto l’estensione gestisce automaticamente la complessità della condivisione dei dati. Quando i dati dell’evento si trovano al limite, puoi richiamarli in altre applicazioni Experience Platform. Ad esempio:

| Applicazione | Finalità | Casi d’uso |
|---|---|---|
| [Adobe [!DNL Real-Time CDP]](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it) | Servizio di gestione dei profili e segmentazione | **Segmentazione cronologia acquisti**: i commercianti possono identificare i clienti che acquistano un articolo in base a un periodo di tempo specifico (mensile, trimestrale, annuale e così via). I commercianti possono quindi creare segmenti per questi clienti e destinarli a promozioni, campagne e come _top dei dati funnel_ per i lead per i servizi di abbonamento.<br> **Segmentazione basata su categorie**: i commercianti possono vedere quale categoria di prodotti è stata acquistata.<br> **Segmentazione basata sull&#39;offerta**: i commercianti possono identificare i clienti che restituiscono costantemente i prodotti. Le offerte e gli sconti concessi possono ora essere più intelligenti. Ad esempio, la spedizione gratuita può essere rimossa per un cliente che restituisce prodotti in qualsiasi momento.<br> **Destinazione lookalike**: un pubblico lookalike _è una metodologia adottata da un commerciante per le sue promozioni per raggiungere nuove persone che probabilmente saranno interessate alla sua attività perché condividono caratteristiche simili ai tuoi clienti esistenti._ I segmenti simili possono essere creati in base a dati comportamentali e transazionali.<br> **Propensione cliente**: le modifiche nel comportamento del cliente possono essere identificate come risultato dei profili cliente più profondi che possono essere creati dai dati transazionali. L&#39;affidabilità del punteggio di propensione risulterà maggiore in quanto nei calcoli verranno inseriti più dati, ad esempio restituzioni di prodotti e configurazioni di prodotto.<br> **Cross-selling**: un commerciante può identificare forti opportunità di cross-selling e up-selling dalle informazioni granulari acquisite in Commerce. |
| [Cliente [!DNL Journey Analytics]](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it) | Analisi approfondita dell&#39;intero percorso Commerce | **Tendenze stagionali**: un commerciante può identificare le tendenze stagionali, che li aiuta a prepararsi al cambiamento periodico della domanda di determinati prodotti. Inoltre, i commercianti possono identificare i cambiamenti nella popolarità complessiva di qualsiasi prodotto nel corso degli anni.<br> **Analisi della conversione**: sapendo quando è stato acquistato un prodotto, insieme all&#39;accesso agli eventi di impression della vetrina, i commercianti possono generare un profilo avanzato del cliente per eseguire l&#39;analisi della conversione. |
| [Adobe [!DNL Analytics]](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html?lang=it) | Analisi approfondita del comportamento dei clienti e delle prestazioni della campagna | **Restituzioni ordini**: i commercianti possono identificare i clienti e i segmenti di clienti più grandi che hanno un modello di prodotti di ritorno. In questo modo i commercianti possono migliorare la propria strategia di e-commerce e capire come si presenta il comportamento della base clienti.<br> **Indirizzo ordine**: in base all&#39;indirizzo di spedizione, un commerciante può capire se gli ordini vengono effettuati dai clienti stessi o se si tratta di un altro individuo o entità.<br> **Tendenze stagionali**: un commerciante può identificare le tendenze stagionali, che li aiuta a prepararsi al cambiamento periodico della domanda di determinati prodotti. Inoltre, i commercianti possono identificare i cambiamenti nella popolarità complessiva di qualsiasi prodotto nel corso degli anni.<br> **Analisi della conversione**: sapendo quando è stato acquistato un prodotto, insieme all&#39;accesso agli eventi di impression della vetrina, i commercianti possono generare un profilo avanzato del cliente per eseguire l&#39;analisi della conversione. **Nota** Adobe Analytics supporta solo i dati evento comportamentali (storefront). Adobe Analytics non supporta i dati evento transazionali (di backoffice). |
| [Adobe [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=it) | Orchestrazione di campagne tra canali diversi | **percorsi basati sul comportamento**: i commercianti possono eseguire il targeting di un cliente che ha acquistato un telefono cellulare due anni fa suggerendo di acquistare il nuovo modello. I commercianti possono creare campagne e promozioni personalizzate per questi clienti e utilizzare le funzionalità e-mail e SMS per contattarli. Inoltre, i commercianti possono utilizzare l’ordine storico e i dati comportamentali per identificare le tendenze. Ad esempio, un cliente che ha acquistato in passato un articolo con una particolare configurazione e ora sta cercando di acquistare nuovamente lo stesso prodotto, può migliorare il proprio percorso di acquisto fornendo visibilità e accesso alle stesse configurazioni di prodotto.<br> **Personalization**: con l&#39;accesso alle informazioni del profilo cliente, [!DNL Journey Optimizer] può sbloccare percorsi altamente personalizzati che consentono agli esercenti di contattare i clienti su più canali diversi.<br> **Nuovo profilo creato**: le e-mail di benvenuto e le attività promozionali possono incoraggiare e influenzare i nuovi clienti nei loro percorsi.<br> **Profilo eliminato**: i commercianti possono scegliere di interrompere l&#39;invio di e-mail promozionali ai clienti che hanno chiuso il proprio account. In alternativa, i commercianti possono anche creare campagne per recuperare i clienti persi. |

## Recuperare i dati di Experience Platform in Commerce

L&#39;invio dei dati Commerce ad Experience Platform tramite l&#39;estensione [!DNL Data Connection] rappresenta un lato delle funzionalità di condivisione dei dati di Commerce. L&#39;altro lato, che è un&#39;estensione facoltativa, è denominato [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=it). Questa estensione consente di creare tipi di pubblico in Real-Time CDP e distribuirli nel tuo store di Commerce per informarti sulle regole di prezzo del carrello, sulle regole di prodotto correlate e sui blocchi dinamici.

Ad alto livello, il flusso di dati dall’archivio Commerce ad Experience Platform e viceversa attraverso l’estensione Audience Activation si presenta come segue:

![[!DNL Data Connection] flusso](assets/data-connection.png)

Dopo aver impostato la connessione tra Commerce ad Experience Platform e Experience Platform a Commerce, i dati continuano a scorrere. Non è necessario riconnettersi, a meno che non sia richiesto da un aggiornamento.

## Concetti

La condivisione di dati tra questi due sistemi richiede la comprensione di diversi concetti.

- **Dati** - I dati che vengono condivisi con Experience Platform sono i dati raccolti dagli eventi del browser nella vetrina, dagli eventi di back office sul server e dai dati dei record del profilo. Gli eventi di vetrina vengono acquisiti dalle interazioni degli acquirenti sul sito e includono eventi come `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut` e così via. Per l&#39;elenco completo degli eventi storefront, vedere [eventi storefront](events.md#storefront-events). Gli eventi lato server o back office includono [informazioni sullo stato dell&#39;ordine](events-backoffice.md#order-status), ad esempio [`orderPlaced`](events-backoffice.md#orderplaced), [`orderReturned`](events-backoffice.md#orderitemreturncompleted), [`orderShipped`](events-backoffice.md#ordershipmentcompleted), [`orderCancelled`](events-backoffice.md#ordercancelled) e così via. Per l&#39;elenco completo degli eventi di back office, vedere [eventi di back office](events-backoffice.md). I dati dei record profilo contengono informazioni relative alla creazione, all’aggiornamento o all’eliminazione di un nuovo profilo. Per ulteriori informazioni, consulta [dati record profilo](events-profilerecord.md).

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

## Passaggi di onboarding

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
