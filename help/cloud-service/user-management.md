---
title: Gestione degli utenti
description: Scopri come gestire gli utenti in [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
role: Admin
source-git-commit: 00d31ca7e4e81ecbc34373ce95b1256a7ae012db
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# Gestione degli utenti

Se si desidera che gli utenti accedano all&#39;amministratore in [!DNL Adobe Commerce as a Cloud Service], è necessario aggiungerli come utenti nell&#39;organizzazione e assicurarsi che abbiano accesso al prodotto Cloud Service in [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

Questo processo richiede un&#39;organizzazione IMS con accesso a [!DNL Adobe Commerce as a Cloud Service]. Questi processi possono essere eseguiti solo dall’amministratore di sistema o dall’amministratore di prodotto dell’organizzazione.

>[!TIP]
>
>Per aggiungere più utenti contemporaneamente, puoi eseguire un [caricamento CSV in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
> 
> È inoltre possibile aggiungere più utenti a un ruolo creando un [gruppo di utenti](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Quindi puoi aggiungere il prodotto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] al gruppo di utenti.

## Informazioni sui ruoli

I seguenti ruoli sono disponibili per [!DNL Adobe Commerce as a Cloud Service]. Per visualizzare o modificare questi ruoli, nell&#39;amministratore di Commerce passa a **Sistema** > **Autorizzazioni** > **Ruoli utente**.

* **Utenti** - Gli utenti hanno accesso come amministratore all&#39;amministratore di Commerce, ma non possono gestire l&#39;accesso a livello di prodotto in Admin Console. Gli utenti possono inoltre utilizzare i crediti per [creare istanze](./getting-started.md#create-an-instance) in [!DNL Commerce Cloud Manager].

  >[!NOTE]
  >
  >A tutti gli utenti di Commerce, inclusi sviluppatori e amministratori, deve essere assegnato anche il ruolo Utente. È richiesto per le autorizzazioni di base di Commerce.

* Gli sviluppatori [**Developers**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} dispongono di autorizzazioni utente e vengono aggiunti all&#39;istanza di Commerce come utente sviluppatore. Ciò significa che possono utilizzare [SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"} dell&#39;interfaccia utente amministratore, [configurare gli eventi](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} e [creare webhook](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Amministratori: esistono tre diversi tipi di amministratori:
   * [Amministratori di sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - L&#39;amministratore di sistema ha accesso a tutti i prodotti e i profili di prodotto dell&#39;organizzazione tramite Admin Console.
   * [Amministratori di prodotto](#add-a-product-admin) - Gli amministratori di prodotto possono [gestire utenti, ruoli e autorizzazioni per il prodotto](#add-users) in [!DNL Adobe Admin Console] e [gestire gli utenti nell&#39;amministratore di Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
   * [Amministratori del profilo di prodotto](#add-developers-and-product-profile-admins) - Gli amministratori del profilo di prodotto non hanno accesso all&#39;amministratore Adobe Commerce, ma possono gestire gli utenti per il prodotto in [!DNL Adobe Admin Console].

Per informazioni dettagliate sulle autorizzazioni concesse a ogni ruolo all&#39;interno di Adobe Commerce, consulta [autorizzazioni utente](#user-permissions).

## Aggiungi un amministratore prodotto

>[!NOTE]
>
>Assegna agli amministratori di prodotto il [ruolo utente](#add-users) prima di aggiungerli come amministratori di prodotto. Il ruolo Utente è richiesto per le autorizzazioni di base di Commerce.

1. Passa a https://adminconsole.adobe.com e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Nella scheda [!UICONTROL **Prodotti**], in [!UICONTROL **Prodotti e servizi**], selezionare il prodotto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![seleziona il prodotto](./assets/backend.png){width="600" zoomable="yes"}

1. Selezionare la scheda [!UICONTROL **Amministratori**].

1. Fai clic su [!UICONTROL **Aggiungi amministratore**].

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere come amministratori e fare clic su [!UICONTROL **Salva**].

## Aggiungi utenti

Le istruzioni seguenti forniscono informazioni su come aggiungere utenti a [!DNL Commerce Cloud Manager] e all&#39;amministratore di Commerce. L&#39;interfaccia [!DNL Commerce Cloud Manager] consente di creare e gestire le istanze di Commerce. Questo processo è necessario per tutti gli utenti, inclusi sviluppatori e amministratori.

>[!NOTE]
>
>Solo gli amministratori di prodotto e gli amministratori di sistema possono aggiungere utenti e sviluppatori al prodotto Adobe Commerce as a Cloud Service.

1. Passa a https://adminconsole.adobe.com e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Nella scheda [!UICONTROL **Prodotti**], in [!UICONTROL **Prodotti e servizi**], selezionare il prodotto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![seleziona il prodotto](./assets/backend.png){width="600" zoomable="yes"}

1. Fare clic sul profilo di prodotto [!UICONTROL **Predefinito - Cloud Manager**].

1. Selezionare la scheda [!UICONTROL **Utenti**] e fare clic su [!UICONTROL **Aggiungi utenti**].

   ![scheda selezionata](./assets/tab-select.png){width=600 zoomable="yes"}

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere come amministratori e fare clic su [!UICONTROL **Salva**].

### Aggiungere sviluppatori e amministratori dei profili di prodotto

Per aggiungere sviluppatori e amministratori dei profili di prodotto, ripetere il processo [aggiungi utenti](#add-users), ma selezionare la scheda [!UICONTROL **Sviluppatori**] o [!UICONTROL **Amministratori**] invece della scheda [!UICONTROL **Utenti**].

>[!NOTE]
>
>Gli amministratori dei profili di prodotto non hanno accesso all’amministratore di Commerce. Per ulteriori informazioni, consultare [Informazioni sui ruoli](#understanding-roles).
>
>Assegna agli sviluppatori il ruolo Utente prima di aggiungerli come sviluppatori. Il ruolo Utente è richiesto per le autorizzazioni di base di Commerce.

![scheda selezionata](./assets/tab-select.png){width=600 zoomable="yes"}

## Risorse per il ruolo

L’elenco seguente descrive le risorse alle quali i ruoli predefiniti sono autorizzati ad accedere all’interno di Adobe Commerce Admin. Per modificare le autorizzazioni predefinite per ogni ruolo, passa a **Sistema** > **Autorizzazioni** > **Ruoli utente** nell&#39;amministrazione di Commerce.

**Utenti**

* Catalogo
   * Inventario
      * Prodotti
         * Leggi prezzo prodotto

**Sviluppatori**

* Catalogo
   * Inventario
      * Prodotti
         * Leggi prezzo prodotto
* Sistema
   * Trasferimento dati
      * Cronologia importazione
* Configurazione eventi Adobe IO
   * Verifica configurazione
   * Crea provider di eventi
   * Aggiornamento configurazione
   * Sincronizza eventi
   * Ottieni elenco provider eventi
* Framework eventi
   * Elenco eventi
   * Verifica connessione eventi
   * Iscriviti a un evento
   * Annullare l’abbonamento a un evento
   * Stato evento
   * API per ottenere gli abbonamenti agli eventi
   * Visualizza interfaccia utente di amministrazione sottoscrizioni eventi
   * Interfaccia utente amministratore per creare sottoscrizioni eventi
   * Richiedi nuova interfaccia utente di amministrazione eventi
* Webhook
   * Firma digitale webhook
      * Impostazioni firma digitale webhook
      * Webhook Digital Signature Generate Keys
   * Gestione dei webhook
      * Griglia webhook
      * Modifica webhook
      * Webhook di prova
      * Iscrizione API al webhook
      * Annullamento dell’abbonamento API al webhook
      * Elenco webhook
      * Richiedi nuovo webhook
      * Registri webhook
      * Ottieni elenco di webhook

**Amministratori**

Gli amministratori hanno accesso a tutte le autorizzazioni.

## Aggiungere un utente ad AEM Assets o ai visualizzatori di prodotto

La seguente configurazione è richiesta per [!DNL Adobe Experience Manager Assets] e [!DNL Product Visuals powered by AEM Assets] utenti.

Se il tuo account ha accesso a [Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service) e desideri consentire a un utente di accedere alle funzioni avanzate di [AEM Assets](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/overview){target="_blank"} insieme a [!DNL Adobe Commerce as a Cloud Service], utilizza la procedura seguente:

>[!NOTE]
>
>Gli utenti che non dispongono delle autorizzazioni appropriate per le risorse non potranno accedere alle funzionalità avanzate di [!DNL AEM Assets], ad esempio [Generazione di immagini AI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generative-ai-in-aem){target="_blank"}, [Varianti generate](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations-integrated-editor){target="_blank"} e altro ancora.

>[!TIP]
>
>Per aggiungere più utenti contemporaneamente, puoi eseguire un [caricamento CSV in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
>
>È inoltre possibile aggiungere più utenti a un ruolo creando un [gruppo di utenti](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Quindi puoi aggiungere il prodotto [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] al gruppo di utenti.

1. Passa a https://adminconsole.adobe.com e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Nella scheda [!UICONTROL **Prodotti**], in [!UICONTROL **Prodotti e servizi**], selezionare il prodotto [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**].

   ![seleziona il prodotto](./assets/backend-aem.png){width="600" zoomable="yes"}

1. Selezionare la scheda [!UICONTROL **Utenti**].

1. Fare clic su [!UICONTROL **Aggiungi utente**].

1. Immetti il nome utente o l’indirizzo e-mail degli utenti che desideri aggiungere.

1. Fare clic su [!UICONTROL **Aggiungi prodotto**].

1. Seleziona i seguenti profili di prodotto, necessari per integrare AEM Assets con Commerce:

   * Proprietario business: necessario per creare e gestire i programmi.
   * Responsabile dell’implementazione: necessario per distribuire il codice dagli archivi ad AEM.

   Se aggiungi uno sviluppatore che non ha bisogno di accedere alle interfacce Cloud Manager o Experience Manager, puoi invece assegnare loro il ruolo di sviluppatore.

   >[!NOTE]
   >
   >Per ulteriori informazioni su come queste autorizzazioni influiscono sul tuo accesso ad AEM Assets, consulta [Profili di prodotto di Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/concepts/aem-cs-team-product-profiles#cloud-manager-product-profiles){target="_blank"}.

1. Fare clic su [!UICONTROL **Applica**].

1. Fai clic su [!UICONTROL **Salva**].

Per confermare che l’utente ha accesso, fai clic sul nome dell’utente per aprire la pagina del suo profilo. Nella sezione [!UICONTROL **Prodotti**], dovrebbe essere indicato [!UICONTROL **Completati**] nel prodotto [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**]. Potrebbero essere necessari alcuni secondi dopo l’aggiunta dell’utente per vedere lo stato aggiornato sul suo profilo. Aggiorna la pagina per visualizzare lo stato aggiornato.

![accesso al prodotto](./assets/product-access.png){width="600" zoomable="yes"}

## Accedere all’interfaccia di Experience Manager

Dopo aver aggiunto un utente ad AEM Assets, può accedere all&#39;interfaccia [!DNL Experience Manager] passando a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}.

1. Nella sezione [!UICONTROL **Accesso rapido**], fai clic su [!UICONTROL **Experience Manager**] o su [!UICONTROL **Visualizza tutto**] se non trovi [!UICONTROL **Experience Manager**]. Quindi fare clic su [!UICONTROL **Cloud Manager**] o passare direttamente a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}.

1. Dalla pagina [!UICONTROL **Cloud Manager**], fai clic su [!UICONTROL **Aggiungi programma**] per iniziare.

1. [Crea un nuovo programma](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program){target="_blank"}.

1. [Crea un nuovo ambiente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/creating-an-environment){target="_blank"}.

1. Dopo aver creato l&#39;ambiente, tornare a [Admin Console](https://adminconsole.adobe.com){target="_blank"} e selezionare [!UICONTROL **Adobe Experience Manager as a Cloud Service**].

1. Ora dovresti visualizzare nuovi profili di prodotto. Selezionare che contiene `- author -`. Ad esempio, `<environment-name> - author - <program-id> - <environment-id>`.

1. [Aggiungi utenti al profilo di prodotto](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles){target="_blank"}.

* [Configura AEM Assets per supportare i metadati di Commerce](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem)
* [Integrare AEM Assets con Commerce per la sincronizzazione delle risorse](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization)
