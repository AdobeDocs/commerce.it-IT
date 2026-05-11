---
title: Tipi di dati Commerce
description: Scopri i tipi di dati che puoi raccogliere e inviare ad Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
exl-id: 6354963c-f27f-4e69-9ecb-acb4befb7c2a
TQID: https://experienceleague.adobe.com/LXMqOhHAZpUHaCeeU5ioKKXVrkLftospQEPDd9H-MD8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 339
ht-degree: 2%

---

# Tipi di dati Commerce

L&#39;estensione [Connessione dati](overview.md) collega i dati Commerce ad Experience Platform. I dati da utilizzare in Experience Platform sono raggruppati in due tipi di comportamento: dati di serie temporali, che appartengono alla classe **Experience Event**, e dati di record, che appartengono alla classe **Individual Profile**.

Ulteriori informazioni su [comportamento dati](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#data-behaviors) e [classi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#class) in Experience Platform.

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
