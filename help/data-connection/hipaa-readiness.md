---
title: Preparazione HIPAA per  [!DNL Commerce] servizi
description: Scopri come utilizzare l'estensione  [!DNL Data Connection] per condividere [!DNL Commerce] dati con Experience Platform e mantenere la conformità HIPAA.
role: Admin, Leader
feature: Security, Compliance
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Preparazione HIPAA per i servizi [!DNL Commerce]

L&#39;estensione [!DNL Data Connection] consente di condividere [!DNL Commerce] dati di eventi back office con Experience Platform e di mantenere la conformità HIPAA.

>[!IMPORTANT]
>
>Poiché gli eventi storefront vengono generati lato client, è responsabilità del commerciante [non inviare dati evento storefront](connect-data.md#data-collection) ad Experience Platform.

In questo articolo imparerai:

- Cosa installare
- Come garantire che i dati inviati ad Experience Platform siano pronti per HIPAA
- Crittografia dei dati in [!DNL Commerce]

## Installazione

Se hai acquistato il componente aggiuntivo per l&#39;assistenza sanitaria per Adobe [!DNL Commerce], probabilmente hai già installato l&#39;[estensione compatibile con HIPAA](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation). Per assicurarsi che i dati dell&#39;evento di back office [!DNL Commerce] siano pronti per HIPAA, è inoltre necessario installare l&#39;estensione [!DNL Data Connection] con l&#39;estensione aggiuntiva **HIPAA** di Data Services. L&#39;estensione **Data Services HIPAA** garantisce che tutti i dati di back office inviati ad Experience Platform siano pronti per HIPAA. Scopri [come installare l&#39;estensione](install.md#install-the-data-services-hipaa-extension).

>[!IMPORTANT]
>
>Quando installi l&#39;estensione **Data Services HIPAA**, i dati dell&#39;evento storefront utilizzati da Live Search e Product Recommendations non vengono più acquisiti. Questo perché i dati dell’evento storefront vengono generati lato client. Per continuare a catturare e inviare dati di eventi vetrina, riattivare la raccolta eventi per questi servizi. Per ulteriori informazioni, consulta la [configurazione generale](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services).

## Come garantire che i dati inviati ad Experience Platform siano pronti per HIPAA

Tutti i dati degli eventi di back office che l&#39;estensione [!DNL Data Connection] invia ad Experience Platform sono considerati sensibili all&#39;interno di [!DNL Commerce]. Tuttavia, è responsabilità del commerciante applicare le etichette di utilizzo dei dati al proprio schema [!DNL Commerce] in Experience Platform per identificare esplicitamente particolari dati come sensibili. Quando applichi le etichette di utilizzo dei dati direttamente a uno schema, queste vengono propagate a tutti i set di dati esistenti e futuri basati su tale schema.

Per una panoramica delle etichette di utilizzo dei dati e del loro ruolo all&#39;interno del framework di governance dei dati, vedi [panoramica delle etichette di utilizzo dei dati](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/overview) nella documentazione di Experience Platform.

### Applica etichette di utilizzo dati ai campi [!DNL Commerce]

Segui i passaggi descritti nell&#39;esercitazione [gestire le etichette di utilizzo dei dati per uno schema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/labels) per scoprire come applicare le etichette allo schema [!DNL Commerce].

Per informazioni sulle etichette disponibili da applicare ai campi dello schema [!DNL Commerce], consulta il [glossario delle etichette sensibili](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/reference#sensitive). L&#39;etichetta `RHD`, ad esempio, identifica informazioni protette sulla salute (PHI) o informazioni relative a un paziente che Adobe consente contrattualmente di caricare.

Quando i dati di [!DNL Commerce] sono etichettati come sensibili, è possibile applicare criteri per impedire operazioni sui dati che costituiscono violazioni dei criteri. Ulteriori informazioni sull&#39;[applicazione dei criteri](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview) in Experience Platform.

## Crittografia dei dati in Commerce

Adobe [!DNL Commerce] utilizza la crittografia a livello di blocco. Per l&#39;archiviazione, [!DNL Commerce] utilizza Amazon Elastic Block Store (EBS). Tutti i volumi EBS vengono crittografati utilizzando l&#39;algoritmo AES-256, il che significa che i dati vengono crittografati a riposo. I dati [!DNL Commerce] in transito vengono eseguiti tramite connessioni sicure e crittografate utilizzando HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

>[!IMPORTANT]
>
>Commerce non supporta la crittografia a livello di colonna o di riga o la crittografia quando i dati non sono inattivi o in transito tra server diversi.

### Crittografia dei dati in Experience Platform

Quando i commercianti inviano i propri dati ad Experience Platform, questi vengono inviati utilizzando HTTPS TLS v1.2. Ulteriori informazioni sulla crittografia dei dati da parte di [Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/governance-privacy-security/encryption).

## Gestione delle richieste di privacy da parte di [!DNL Commerce]

Scopri come [!DNL Commerce] [gestisce le richieste di privacy](handle-privacy-request.md).
