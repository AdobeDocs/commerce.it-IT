---
title: Gestione di identità e accessi
description: Scopri le funzioni di gestione delle identità e degli accessi per Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: feb48068137c6a63e6594167fe969c3aa4b044c4
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# Gestione di identità e accessi

[!DNL Adobe Commerce as a Cloud Service] sfrutta l&#39;infrastruttura di identità di livello enterprise di Adobe per garantire un controllo degli accessi sicuro, scalabile e centralizzato in tutti gli ambienti. La gestione delle identità e degli accessi (IAM) in [!DNL Adobe Commerce as a Cloud Service] è progettata per semplificare il provisioning degli utenti, applicare l&#39;accesso con privilegi minimi e supportare la conformità agli standard di sicurezza globali.

- **[!DNL Adobe Identity Management Services (IMS)]**: [!DNL Adobe Commerce as a Cloud Service] utilizza [Adobe Identity Management Services (IMS)](https://experienceleague.adobe.com/it/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview) per autenticare gli utenti e gestire i diritti. Ciò include il supporto per i provider di identità federati e il controllo dell&#39;accesso basato su [ruolo](../user-management.md).

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

Per ulteriori informazioni, consulta [gestione utenti](https://experienceleague.adobe.com/it/docs/commerce/cloud-service/user-management).

## Autenticazione API e sicurezza dell’integrazione

L&#39;autenticazione REST API di [!DNL Adobe Commerce as a Cloud Service] viene gestita tramite Adobe [!DNL Adobe Identity Management Services (IMS)] utilizzando protocolli OAuth 2 standardizzati. Questo sistema di autenticazione supporta sia flussi di lavoro interattivi basati sugli utenti che integrazioni automatizzate server-to-server, garantendo un accesso sicuro e appropriato per casi d’uso diversi.

>[!NOTE]
>
>I metodi di generazione dei token di integrazione e di amministrazione nelle versioni PaaS di [!DNL Adobe Commerce] non sono supportati negli ambienti SaaS. Al contrario, devi ottenere un token di amministrazione IMS tramite l’autenticazione OAuth.

- **Supporto OAuth 2.0**: autenticazione sicura basata su token per integrazioni e servizi di terze parti.
- **Accesso API con ambito**: limita l&#39;accesso API a risorse e operazioni specifiche.
- **Registrazione controllo**: tieni traccia degli eventi di autenticazione e delle modifiche di accesso per conformità e risoluzione dei problemi.

Per ulteriori informazioni, vedere [autenticazione REST](https://developer.adobe.com/commerce/webapi/rest/authentication/).
