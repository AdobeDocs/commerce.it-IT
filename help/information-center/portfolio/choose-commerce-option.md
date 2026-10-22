---
title: Scegli un'opzione Commerce
description: Confronta le architetture Adobe Commerce in base alla proprietà delle transazioni, al modello di distribuzione e alle esigenze di merchandising.
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/5y0IU5nji50eqfFNQHbVDV-R81Mx0I8v5Y0a6nccL-w'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---

# Scegli un&#39;opzione Commerce

Per iniziare, identifica il sistema proprietario del carrello, del pagamento, degli ordini e di altre transazioni. Quindi scegli il percorso di merchandising adatto al backend.

## Domande utili per prendere una decisione

Per identificare le opzioni da valutare, utilizza le domande seguenti. Considera il tuo back-end di e-commerce esistente, quanta responsabilità dell’infrastruttura desideri mantenere e se è necessario migliorare l’individuazione dei prodotti e il merchandising. Adobe Commerce Optimizer fornisce funzionalità di rilevamento e merchandising. Non sostituisce il backend che gestisce le transazioni.

1. **Si desidera che Adobe gestisca la piattaforma Commerce come software as a service (SaaS)?**
   - Sì: valuta Adobe Commerce as a Cloud Service.
   - No: se hai bisogno di Adobe Commerce e desideri mantenere il controllo sull’infrastruttura cloud o on-premise, valuta Adobe Commerce on-premise o on-premise.
1. **È necessario Adobe Commerce per gestire il carrello, il pagamento, gli ordini e altre transazioni?**
   - Sì: valuta Adobe Commerce su Cloud o on-premise, oppure Adobe Commerce as a Cloud Service. Queste opzioni utilizzano Commerce Foundation come back-end transazionale.
   - No: mantieni il backend transazionale esistente o di terze parti. Se hai anche bisogno delle funzionalità di rilevamento e merchandising di Adobe, valuta Adobe Commerce Optimizer standalone.
1. **Utilizzare Adobe Commerce Optimizer per migliorare l&#39;individuazione dei prodotti e il merchandising con il backend di e-commerce di terze parti esistente?**
   - Sì: valuta Adobe Commerce Optimizer standalone mantenendo il backend di terze parti per le transazioni.
1. **Adobe Commerce è già in uso su Cloud o in locale e desideri un&#39;individuazione e un merchandising più solidi?**
   - Sì: valuta il connettore Adobe Commerce Optimizer per sincronizzare i dati di catalogo e determinazione prezzi mentre Adobe Commerce continua a gestire le transazioni.

Utilizza la tabella di confronto seguente per far corrispondere le tue risposte a un punto di partenza. Per i diagrammi di sistema dettagliati, vedere [Opzioni di architettura](../architecture-options/overview.md).

## Confronta opzioni Commerce

| Il tuo requisito | Punto di partenza consigliato | Sistema proprietario delle transazioni | Merchandising e discovery |
| --- | --- | --- | --- |
| Adobe gestisce la piattaforma Commerce come SaaS. | [Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md) | Adobe Commerce as a Cloud Service Foundation | Utilizza i servizi Commerce forniti per Adobe Commerce as a Cloud Service. Per informazioni sulla disponibilità dell’integrazione di Adobe Commerce Optimizer, consulta la nota sotto questa tabella. |
| Hai bisogno di Adobe Commerce e vuoi mantenere il controllo sull’infrastruttura cloud o locale. | [Adobe Commerce su Cloud o locale](https://experienceleague.adobe.com/en/docs/commerce-admin/start/guide-overview) | Adobe Commerce Foundation | Utilizza i servizi Commerce supportati in base alle esigenze. |
| Su Adobe Commerce on Cloud o on-premise e desiderano adottare Adobe Commerce Optimizer per l’individuazione e il merchandising. | Adobe Commerce con il [connettore Adobe Commerce Optimizer](/help/aco-connector/overview.md) | Adobe Commerce rimane il sistema di registrazione per le transazioni. | Il connettore sincronizza i dati di catalogo e prezzo con Adobe Commerce Optimizer, che fornisce esperienze di rilevamento e merchandising. |
| Possiedi un back-end per e-commerce di terze parti e desideri scoprire Adobe Commerce Optimizer e merchandising senza sostituire il back-end. | [Adobe Commerce Optimizer](/help/optimizer/overview.md) autonomo | Back-end di e-commerce di terze parti | Invia dati su catalogo e prezzo a Adobe Commerce Optimizer. Integra carrello, pagamento e altre operazioni transazionali con il backend tramite API Mesh, App Builder o un’integrazione diretta. |

>[!NOTE]
>
>Un’integrazione tra Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer è inclusa nella roadmap di Commerce. Se per il momento sono necessarie entrambe le piattaforme, pianifica di utilizzarle come opzioni di architettura separate. Contatta il tuo account manager Adobe per ulteriori informazioni sulla tempistica dell’integrazione.

## Linee guida correlate

- [Piattaforme e servizi](platform-and-services.md)
- [Opzioni dell&#39;architettura](../architecture-options/overview.md)
- [Introduzione](../get-started/get-started-by-role.md)
