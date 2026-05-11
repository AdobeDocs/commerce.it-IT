---
title: Responsabilità condivisa
description: Scopri le responsabilità di sicurezza di ogni parte coinvolta nel tuo  [!DNL Adobe Commerce Optimizer]  progetto.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: 9e09790f-832d-43ab-b2df-6389ad52b43d
TQID: https://experienceleague.adobe.com/lOn0WJYdUi5qMX7OlRKeNAIc-TA29OFWWSqN3yQzt30
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 278
ht-degree: 0%

---

# Responsabilità condivisa sicurezza e modello operativo

>[!BEGINSHADEBOX]

Le tabelle di riepilogo seguenti utilizzano il modello RACI per mostrare le responsabilità di sicurezza condivise tra Adobe e i clienti.

**R** - Responsabile
**A** — Responsabile
**C** - Consultato
**I** - Informato

>[!ENDSHADEBOX]

| Attività | Adobe | Cliente |
| --- | --- | --- |
| Applicazione delle patch dell&#39;infrastruttura Adobe Commerce | RA | |
| Applicazione di patch ai servizi di supporto | RA | |
| Definizione delle regole WAF dell’origine back-end | RA | |
| Definizione delle regole del WAF CDN back-end | RA | |
| Distribuzione delle regole di WAF della piattaforma back-end | RA | |
| Distribuzione delle regole di WAF CDN back-end | RA | |
| Correzione dei bug in [!DNL Adobe Commerce Optimizer] | RA | I |
| Rilascio di [!DNL Adobe Commerce Optimizer] patch per l&#39;infrastruttura | RA | |
| Scalabilità (infrastruttura) | RA | I |
| Integrazione di applicazioni esterne | | RA |
| Installazione delle app App Builder | | RA |
| Verifica delle prestazioni di tutte le app App Builder | | RA |
| Tema e progettazione delle app App Builder personalizzate | | RA |
| Configurazione del DNS di back-end | RA |  |
| CDN back-end di onboarding | RA |  |
| CDN back-end di supporto | RA |  |
| Ottenimento di un provider DNS di back-end | RA | |
| Provisioning degli ambienti di produzione e sandbox | A | R |
| Accesso a Dynamics per [!DNL Adobe Commerce Optimizer] | R | C |
| Risoluzione dei problemi di sicurezza del cliente back-end | RA | I |
| Risoluzione dei problemi di sicurezza CDN back-end | RA | |
| Assistenza ad Adobe nella ricerca sulla sicurezza (scansioni/audit) | RA | |
| Esecuzione di scansioni PCI ASV | RA | I |
| Correzione delle scansioni PCI dell&#39;infrastruttura [!DNL Adobe Commerce Optimizer] | R | |
| Gestione dei segreti del sistema operativo e della piattaforma | RA | |
| Monitoraggio dei registri di sicurezza back-end | RA | |
| Controllo dell’assistenza clienti e dell’accesso | A | R |
| Test e documentazione annuali del piano di ripristino di emergenza Adobe e backup e ripristino | RA | |
| Test annuali e documentazione del piano di ripristino di emergenza | RA | |
| Debug e isolamento dei problemi | R | R |
| Supporto tempestivo del processo di debug e isolamento dei problemi | R | R |
| Installazione di aggiornamenti e patch in [!DNL Adobe Commerce Optimizer] | RA | I |
| Qualità applicazione [!DNL Adobe Commerce Optimizer] di base | RA | |
