---
title: Gestione di identità e accessi
description: Scopri le funzioni di gestione delle identità e degli accessi per Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
autotag-review: '2026-06-18T16:14:06.699Z'
TQID: 'https://experienceleague.adobe.com/lbI3nsLtafel6GtquXnkZmXD2Z3b-rRGPOyr8EqzrjE'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
subfeature_v2: id: e126554b-28f9-4290-b58c-10b888b88174
role_v2: id: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: d378ca77-2da1-4f39-ad92-1917fe974a38id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 419
ht-degree: 0%

---


# Gestione di identità e accessi

[!DNL Adobe Commerce as a Cloud Service] sfrutta l&#39;infrastruttura di identità di livello enterprise di Adobe per garantire un controllo degli accessi sicuro, scalabile e centralizzato in tutti gli ambienti. La gestione delle identità e degli accessi (IAM) in [!DNL Adobe Commerce as a Cloud Service] è progettata per semplificare il provisioning degli utenti, applicare l&#39;accesso con privilegi minimi e supportare la conformità agli standard di sicurezza globali.

- **[!DNL Adobe Identity Management Services (IMS)]**: [!DNL Adobe Commerce as a Cloud Service] utilizza [Adobe Identity Management Services (IMS)](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview) per autenticare gli utenti e gestire i diritti. Ciò include il supporto per i provider di identità federati e il controllo dell&#39;accesso basato su [ruolo](../user-management.md).

- **Governance di Admin Console**: gli amministratori gestiscono l&#39;accesso alla vetrina e al backend tramite [!DNL Adobe Admin Console]. È possibile definire l’ambito delle autorizzazioni per funzioni e ruoli specifici, garantendo l’accesso con i privilegi minimi.

## Servizi Adobe Identity Management (IMS)

[!DNL Adobe Commerce as a Cloud Service] utilizza [!DNL Adobe Identity Management Services (IMS)] per autenticare gli utenti e gestire i diritti in tutta la piattaforma. IMS fornisce:

- **Supporto identità federativa**: integrazione con provider di identità aziendali, quali Azure AD e Okta, tramite SAML o OIDC.
- **Single Sign-On (SSO)**: accesso semplificato a [!DNL Adobe Commerce] e ad altri prodotti [!DNL Adobe Experience Cloud].
- **Multi-Factor Authentication (MFA)**: applicato a livello di organizzazione per una maggiore sicurezza.
- **Ridondanza globale**: i dati delle identità sono archiviati in un&#39;infrastruttura cloud con bilanciamento del carico e aree geografiche multiple.

## Controllo degli accessi ad Admin Console

[!DNL Adobe Admin Console] è l&#39;hub centrale per la gestione dell&#39;accesso utente a [!DNL Adobe Commerce as a Cloud Service]:

- **RBAC (Role-Based Access Control)**: assegna autorizzazioni granulari agli utenti in base ai loro ruoli, ad esempio Sviluppatore, Amministratore e Analista.
- **Profili di prodotto**: definisci gli ambiti di accesso per diversi ambienti, ad esempio staging e produzione.
- **Amministrazione delegata**: gli amministratori di sistema e gli amministratori di prodotto possono gestire l&#39;accesso degli utenti senza il coinvolgimento dell&#39;IT.

Per ulteriori informazioni, consulta [gestione utenti](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management).

## Autenticazione API e sicurezza dell’integrazione

L&#39;autenticazione REST API di [!DNL Adobe Commerce as a Cloud Service] viene gestita tramite Adobe [!DNL Adobe Identity Management Services (IMS)] utilizzando protocolli OAuth 2 standardizzati. Questo sistema di autenticazione supporta sia flussi di lavoro interattivi basati sugli utenti che integrazioni automatizzate server-to-server, garantendo un accesso sicuro e appropriato per casi d’uso diversi.

>[!NOTE]
>
>I metodi di generazione dei token di integrazione e di amministrazione nelle versioni PaaS di [!DNL Adobe Commerce] non sono supportati negli ambienti SaaS. Al contrario, devi ottenere un token di amministrazione IMS tramite l’autenticazione OAuth.

- **Supporto OAuth 2.0**: autenticazione sicura basata su token per integrazioni e servizi di terze parti.
- **Accesso API con ambito**: limita l&#39;accesso API a risorse e operazioni specifiche.
- **Registrazione controllo**: tieni traccia degli eventi di autenticazione e delle modifiche di accesso per conformità e risoluzione dei problemi.

Per ulteriori informazioni, vedere [autenticazione REST](https://developer.adobe.com/commerce/webapi/rest/authentication/).
