---
title: Responsabilità condivisa
description: Scopri le responsabilità di sicurezza di ogni parte coinvolta nel tuo  [!DNL Adobe Commerce as a Cloud Service]  progetto.
role: Admin, Architect, Leader
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
source-git-commit: d38066b6db7da5bb029391716063ed098be1f519
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Responsabilità condivisa sicurezza e modello operativo

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] è un servizio su richiesta che si basa su un modello operativo e di sicurezza con responsabilità condivisa. Queste responsabilità sono condivise tra Adobe e i clienti. Ciascuna parte ha la responsabilità distinta di proteggere e gestire l’applicazione Adobe Commerce.

>[!BEGINSHADEBOX]

Le tabelle di riepilogo seguenti utilizzano il modello RACI per mostrare le responsabilità di sicurezza condivise tra Adobe e i clienti.

**R** - Responsabile
**A** — Responsabile
**C** — Consultato
**I** - Informato

>[!ENDSHADEBOX]

| Attività | Adobe | Cliente |
| --- | --- | --- |
| Applicazione delle patch dell&#39;infrastruttura Adobe Commerce | RA | |
| Applicazione di patch ai servizi di supporto (ad esempio, Nginx o MySQL) | RA | |
| Definizione delle regole WAF dell’origine back-end | RA | |
| Definizione delle regole del WAF CDN back-end | RA | |
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
