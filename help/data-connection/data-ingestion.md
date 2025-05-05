---
title: Tipi di dati Commerce
description: Scopri i tipi di dati che puoi raccogliere e inviare ad Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Tipi di dati Commerce

L&#39;estensione [Connessione dati](overview.md) collega i dati Commerce ad Experience Platform. I dati da utilizzare in Experience Platform sono raggruppati in due tipi di comportamento: dati di serie temporali, che appartengono alla classe **Experience Event**, e dati di record, che appartengono alla classe **Individual Profile**.

Ulteriori informazioni su [comportamento dati](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it#data-behaviors) e [classi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it#class) in Experience Platform.

## Dati delle serie temporali

I dati di serie temporali forniscono un&#39;istantanea del sistema nel momento in cui un oggetto record ha intrapreso un&#39;azione, direttamente o indirettamente. Ad esempio, quando un acquirente esplora un prodotto sul tuo sito, aggiunge un prodotto al carrello, effettua un ordine e così via. I dati della serie temporale vengono acquisiti in Experience Platform utilizzando uno schema la cui classe è impostata su **Experience Event**.

### Dati acquisiti delle serie temporali

Consulta [eventi comportamentali](events.md) e [eventi di back office](events-backoffice.md) per scoprire quali dati vengono acquisiti quando viene generato un evento di serie temporale.

### Schema necessario per acquisire i dati evento della serie temporale

Scopri come [creare uno schema](update-xdm.md) in grado di acquisire dati di eventi comportamentali e di serie temporali di back office.

## Registra dati

I dati del record forniscono informazioni sugli attributi di un soggetto. Un soggetto potrebbe essere un&#39;organizzazione o un individuo. Ad esempio, un acquirente sul tuo sito crea un account e che genera i dati del record. Questi dati vengono acquisiti in Experience Platform utilizzando uno schema la cui classe è impostata su **Profilo individuale**. Puoi inviare i dati del record al servizio di segmentazione e gestione dei profili di Adobe: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it).

### Dati record profilo acquisiti

Consulta [dati del record del profilo cliente](events-profilerecord.md) per sapere quali dati vengono acquisiti quando viene generato un record del profilo.

### Schema necessario per acquisire i dati del record del profilo

Scopri come [creare uno schema](profile-data.md) in grado di acquisire i dati del record del profilo.
