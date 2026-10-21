---
title: Responsabilità condivisa
description: Scopri le responsabilità di sicurezza di ogni parte coinvolta nel progetto [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud, Security
role: Admin, Developer, Leader
level: Intermediate
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
autotag-review: '2026-06-18T16:19:21.186Z'
TQID: 'https://experienceleague.adobe.com/ZjR9eFTVz8RIrYIN1CxyEgegGoZljXJKrtWZStx-ln0'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
subfeature_v2:
  - id: d9ced453-36f4-4eb5-b2f3-1d593e32476b
    internal-label: Account management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: 8b3db59ed02539646dd53a2e9c7a0925b7c3a804
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%
---
# Responsabilità condivisa sicurezza e modello operativo

[!DNL Adobe Commerce as a Cloud Service] è un servizio su richiesta che si basa su un modello operativo e di sicurezza con responsabilità condivisa. Adobe e i suoi clienti condividono queste responsabilità, e ciascuna delle parti è responsabile della sicurezza e del funzionamento dell’applicazione Adobe Commerce.

[!DNL Adobe Commerce as a Cloud Service with Managed Operations] è un&#39;offerta premium che aggiunge un CSE (Customer Success Engineer) denominato e un team di supporto P1 per operazioni gestite 24 ore su 24, 7 giorni su 7 oltre al modello di responsabilità condivisa standard. Adobe continua a essere proprietaria della piattaforma, dell’infrastruttura, della sicurezza e dell’applicazione di base e tu continui a essere proprietario delle tue personalizzazioni e integrazioni, ma grazie alle operazioni gestite, Adobe Managed Services viene consultato su:

- Integrazioni
- App App Builder
- Edge Delivery Storefront
- Gestione degli eventi
- Aggiornamenti della piattaforma

Adobe Managed Services condivide inoltre la responsabilità del disaster recovery, del debug e dell&#39;isolamento dei problemi. Il CSE ti guida dall’onboarding fino al go-live e oltre, in modo da poter contare su un esperto Adobe in ogni fase invece di operare da solo.

>[!BEGINSHADEBOX]

Le tabelle di riepilogo seguenti utilizzano il modello RACI per mostrare le responsabilità di sicurezza condivise tra Adobe, Adobe Managed Operations e i clienti.

**R** - Responsabile
**A** — Responsabile
**C** - Consultato
**I** - Informato

>[!ENDSHADEBOX]

| Attività | Adobe | Operazioni gestite di Adobe | Cliente |
| --- | --- | --- | --- |
| Definizione delle regole WAF dell’origine back-end | RA | | |
| Definizione delle regole del WAF CDN back-end | RA | | |
| Distribuzione e manutenzione di [!DNL Adobe Developer App Builder] applicazioni | | | RA |
| Distribuzione delle regole di WAF della piattaforma back-end | RA | | |
| Distribuzione delle regole di WAF CDN back-end | RA | | |
| Correzione dei bug principali in [!DNL Adobe Commerce as a Cloud Service] | RA | | I |
| Rilascio di [!DNL Adobe Commerce as a Cloud Service] patch per l&#39;infrastruttura | RA | | |
| Scalabilità (infrastruttura) | RA | | |
| Ridimensionamento (applicazione principale) | RA | | |
| Integrazione di applicazioni esterne | | C | RA |
| Installazione delle app App Builder | | C | RA |
| Verifica delle prestazioni di tutte le app App Builder | | C | RA |
| Tema e progettazione delle app App Builder personalizzate | | C | RA |
| Configurazione del DNS di back-end | RA | | I |
| CDN back-end di onboarding | RA | | I |
| CDN back-end di supporto | RA | | I |
| Ottenimento di un provider DNS di back-end | RA | | |
| Provisioning degli ambienti di produzione e sandbox | A | | R |
| Accesso a Dynamics for Adobe Commerce sull’infrastruttura cloud | R | | C |
| Risoluzione dei problemi di sicurezza del cliente back-end | RA | | I |
| Risoluzione dei problemi di sicurezza CDN back-end | RA | | |
| Assistenza ad Adobe nella ricerca sulla sicurezza (scansioni/audit) | RA | | |
| Esecuzione di scansioni PCI ASV | RA | | I |
| Correzione delle scansioni PCI dell&#39;infrastruttura Adobe Commerce | R | | |
| Gestione dei segreti del sistema operativo e della piattaforma | RA | | |
| Monitoraggio dei registri di sicurezza back-end | RA | | |
| Controllo dell’assistenza clienti e dell’accesso | A | C | R |
| Test e documentazione annuali del piano di ripristino di emergenza Adobe e backup e ripristino | RA | C | |
| Test annuali e documentazione del piano di ripristino di emergenza | RA | RA | |
| Debug e isolamento dei problemi | R | R | R |
| Supporto tempestivo del processo di debug e isolamento dei problemi | R | R | R |
| Pubblicazione di aggiornamenti e patch nella versione di base di Adobe Commerce | RA | C | I |
| Installazione di aggiornamenti e patch per Adobe Commerce Core | RA | C | I |
| Qualità applicazione Adobe Commerce di base | RA | C | |
