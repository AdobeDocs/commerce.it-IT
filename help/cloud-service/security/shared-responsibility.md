---
title: Responsabilità condivisa
description: Scopri le responsabilità di sicurezza di ogni parte coinvolta nel tuo  [!DNL Adobe Commerce as a Cloud Service]  progetto.
feature: Cloud, Security
role: Admin, Developer, Leader
level: Intermediate
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
TQID: 'https://experienceleague.adobe.com/ZjR9eFTVz8RIrYIN1CxyEgegGoZljXJKrtWZStx-ln0'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: ef32511703a96b5f4db32d54229e9a7cbe961f12
workflow-type: tm+mt
source-wordcount: 340
ht-degree: 0%

---

# Responsabilità condivisa sicurezza e modello operativo

[!DNL Adobe Commerce as a Cloud Service] è un servizio su richiesta che si basa su un modello operativo e di sicurezza con responsabilità condivisa. Adobe e i suoi clienti condividono queste responsabilità, e ciascuna delle parti è responsabile della sicurezza e del funzionamento dell’applicazione Adobe Commerce.

>[!BEGINSHADEBOX]

Le tabelle di riepilogo seguenti utilizzano il modello RACI per mostrare le responsabilità di sicurezza condivise tra Adobe e i clienti.

**R** - Responsabile
**A** — Responsabile
**C** - Consultato
**I** - Informato

>[!ENDSHADEBOX]

| Attività | Adobe | Cliente |
| --- | --- | --- |
| Definizione delle regole WAF dell’origine back-end | RA | |
| Definizione delle regole del WAF CDN back-end | RA | |
| Distribuzione e manutenzione di [!DNL Adobe Developer App Builder] applicazioni | | RA |
| Distribuzione delle regole di WAF della piattaforma back-end | RA | |
| Distribuzione delle regole di WAF CDN back-end | RA | |
| Correzione dei bug principali in [!DNL Adobe Commerce as a Cloud Service] | RA | I |
| Rilascio di [!DNL Adobe Commerce as a Cloud Service] patch per l&#39;infrastruttura | RA | |
| Scalabilità (infrastruttura) | RA | |
| Ridimensionamento (applicazione principale) | RA | |
| Integrazione di applicazioni esterne | | RA |
| Installazione delle app App Builder | | RA |
| Verifica delle prestazioni di tutte le app App Builder | | RA |
| Tema e progettazione delle app App Builder personalizzate | | RA |
| Configurazione del DNS di back-end | RA | I |
| CDN back-end di onboarding | RA | I |
| CDN back-end di supporto | RA | I |
| Ottenimento di un provider DNS di back-end | RA | |
| Provisioning degli ambienti di produzione e sandbox | A | R |
| Accesso a Dynamics for Adobe Commerce sull’infrastruttura cloud | R | C |
| Risoluzione dei problemi di sicurezza del cliente back-end | RA | I |
| Risoluzione dei problemi di sicurezza CDN back-end | RA | |
| Assistenza ad Adobe nella ricerca sulla sicurezza (scansioni/audit) | RA | |
| Esecuzione di scansioni PCI ASV | RA | I |
| Correzione delle scansioni PCI dell&#39;infrastruttura Adobe Commerce | R | |
| Gestione dei segreti del sistema operativo e della piattaforma | RA | |
| Monitoraggio dei registri di sicurezza back-end | RA | |
| Controllo dell’assistenza clienti e dell’accesso | A | R |
| Test e documentazione annuali del piano di ripristino di emergenza Adobe e backup e ripristino | RA | |
| Test annuali e documentazione del piano di ripristino di emergenza | RA | |
| Debug e isolamento dei problemi | R | R |
| Supporto tempestivo del processo di debug e isolamento dei problemi | R | R |
| Pubblicazione di aggiornamenti e patch nella versione di base di Adobe Commerce | RA | I |
| Installazione di aggiornamenti e patch per Adobe Commerce Core | RA | I |
| Qualità applicazione Adobe Commerce di base | RA | |
