---
title: Aggiornare gli schemi evento serie temporali per l’acquisizione dei dati di Commerce
description: Scopri come creare schemi, set di dati e flussi di dati per raccogliere e inviare dati di eventi di serie temporali per l’acquisizione di dati Commerce.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# Aggiornare gli schemi evento serie temporali per l’acquisizione dei dati di Commerce

Uno dei [passaggi di onboarding](overview.md#onboarding-steps) per l&#39;utilizzo dell&#39;estensione [!DNL Data Connection] consiste nell&#39;accedere all&#39;area di lavoro dello stream di dati e [creare uno stream di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=it) specifico per Adobe Commerce. Quando crei tale flusso di dati, devi anche selezionare uno schema che descriva i dati che intendi acquisire. Tale schema deve includere gruppi di campi specifici per l’e-commerce.

Questo articolo fornisce i gruppi di campi che lo schema deve includere per raccogliere correttamente i seguenti dati delle serie temporali forniti dagli eventi di Adobe Commerce:

- [Comportamento](events.md) - Include eventi di vetrina, profilo, ricerca e B2B.
- [Back office](events-backoffice.md) - Include lo stato dell&#39;ordine ed eventi di profilo.

Ulteriori informazioni su [dati della serie temporale](data-ingestion.md).

Ulteriori informazioni sulle [nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it).

## Aggiornamento dello schema con i dati comportamentali e di evento di back office delle serie temporali

In questa sezione imparerai ad aggiornare lo schema esistente o a creare uno schema per includere i dati comportamentali e di back office degli eventi.

>[!NOTE]
>
>Consulta [dati evento profilo serie temporale](#time-series-profile-event-data) per scoprire come aggiungere campi specifici per il profilo.

1. Se non disponi già di uno schema, [creane](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=it#create) uno con la classe impostata su **Experience Event**.

1. [Aggiungi](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=it#add-field-groups) i seguenti gruppi di campi specifici di Commerce (oppure modifica lo schema esistente e aggiungi questi gruppi di campi):

   - Ricerca nel sito
   - Visita pagina web
   - Processo di accesso utente
   - Chiavi di riferimento
   - Dettagli di contatto personali
   - Dettagli canale
   - Dettagli Commerce
   - Adobe Analytics ExperienceEvent Commerce (se desideri inviare dati ad Adobe Analytics)

   >[!NOTE]
   >
   > Non impostare alcun gruppo di campi specifico di Commerce come `Primary identity`. In questo modo il campo viene identificato come obbligatorio e Experience Platform lo prevede in ogni evento. Se tale campo è assente, l’acquisizione dei dati non riesce.

   Il tuo schema ora contiene gruppi di campi specifici di Commerce in modo che i dati delle serie temporali raccolti dagli eventi [comportamentali](events.md) e [back office](events-backoffice.md) di Commerce siano rappresentati nello schema.

1. [Attiva](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=it#profile) lo schema per il profilo.

   Quando uno schema è abilitato per il profilo, tutti i set di dati creati da questo schema partecipano a Real-Time CDP, che unisce dati da origini diverse per creare una visualizzazione completa di ciascun cliente.

1. [Crea un set di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=it#create-a-dataset) in base allo schema creato o aggiornato.

   Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

1. [Crea un flusso di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=it) e seleziona lo schema contenente i gruppi di campi specifici di Commerce e il set di dati corrispondente.

   Lo stream di dati inoltra i dati raccolti al set di dati. I dati vengono rappresentati nel set di dati in base allo schema selezionato.

Con gli schemi, i set di dati e i flussi di dati configurati per i dati comportamentali e di back office, puoi [configurare](connect-data.md#data-collection) l&#39;istanza Commerce per raccogliere e inviare tali dati ad Experience Platform.

Per includere le informazioni sul profilo dell&#39;acquirente, vedere [dati evento profilo serie temporale](#time-series-profile-event-data).

## Dati evento profilo serie temporali

I dati dell’evento profilo di serie temporali vengono generati dai seguenti eventi:

- [&#39;accountCreated&#39;](events-backoffice.md#accountcreated)
- [&#39;accountUpdated&#39;](events-backoffice.md#accountupdated)
- [&#39;accountDeleted&#39;](events-backoffice.md#accountdeleted)

Se desideri acquisire i dati dell’evento profilo del cliente in Experience Platform, puoi aggiornare lo schema Commerce esistente e utilizzare lo stesso flusso di dati già configurato, oppure puoi creare uno schema e uno stream di dati specifici del profilo. Tale decisione si basa sulla governance dei dati della tua azienda. Le due sezioni successive illustrano entrambi i casi.

### Invia dati evento profilo serie temporale ad Experience Platform utilizzando lo stream di dati esistente

Se desideri aggiungere i dati evento profilo lato server [serie temporali](events-backoffice.md#customer-profile-events-server-side) al flusso di dati esistente di Commerce, aggiungi il gruppo di campi `Demographic Details` allo schema. Il tuo schema ora contiene i seguenti gruppi di campi specifici per Commerce:

- Ricerca nel sito
- Visita pagina web
- Processo di accesso utente
- Chiavi di riferimento
- Dettagli di contatto personali
- Dettagli canale
- Dettagli Commerce
- Adobe Analytics ExperienceEvent Commerce (se desideri inviare dati ad Adobe Analytics)
- Nuovo: **Dettagli demografici**

Con l&#39;aggiunta del gruppo di campi `Demographic Details` nello schema Commerce esistente, il set di dati e lo stream di dati già associati allo schema Commerce vengono utilizzati per questi dati di profilo della serie temporale.

### Inviare i dati dell’evento profilo di serie temporali ad Experience Platform in un flusso di dati separato

Se desideri aggiungere [dati evento profilo lato server](events-backoffice.md#customer-profile-events-server-side) a un nuovo schema e flusso di dati specifico per il profilo, completa i passaggi seguenti.

1. [Crea](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=it#create) uno schema e imposta la classe su **Evento esperienza**.

1. [Aggiungi](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=it#add-field-groups) i seguenti gruppi di campi specifici del profilo:

   - Dettagli demografici
   - Dettagli di contatto personali
   - Dettagli canale
   - Dettagli Commerce

1. [Attiva](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=it#profile) lo schema per il profilo.

   Quando uno schema è abilitato per il profilo, tutti i set di dati creati da questo schema partecipano a Real-Time CDP, che unisce dati da origini diverse per creare una visualizzazione completa di ciascun cliente.

1. [Crea un set di dati](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=it#create-a-dataset) in base allo schema creato.

   Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella che contiene uno schema (colonne) e dei campi (righe). I set di dati contengono anche metadati che descrivono vari aspetti dei dati memorizzati.

1. [Crea un flusso di dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=it) e seleziona lo schema XDM che contiene i gruppi di campi specifici di Commerce e il set di dati corrispondente.

   Lo stream di dati inoltra i dati raccolti al set di dati. I dati vengono rappresentati nel set di dati in base allo schema selezionato.

Con gli schemi, i set di dati e i flussi di dati configurati per i dati del profilo cliente, puoi [configurare](connect-data.md#data-collection) l&#39;istanza di Commerce per raccogliere e inviare tali dati ad Experience Platform.

Per creare uno schema, un set di dati e uno stream di dati per i dati del record profilo, vedere [Inviare i dati del record profilo ad Experience Platform](profile-data.md).
