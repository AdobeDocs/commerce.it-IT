---
title: Gestione utente
description: Scopri come gestire gli utenti in [!DNL Adobe Commerce as a Cloud Service].
source-git-commit: 25a0d658776ea95fcae07f6390abeeb559642613
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---

# Gestione utente

{{accs-early-access}}

Se si desidera che gli utenti accedano all&#39;amministratore in [!DNL Adobe Commerce as a Cloud Service], è necessario aggiungerli come utenti nell&#39;organizzazione e assicurarsi che abbiano accesso al prodotto Cloud Service in [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

Questo processo richiede un&#39;organizzazione IMS con accesso a [!DNL Adobe Commerce as a Cloud Service]. Questi processi possono essere eseguiti solo dall’amministratore di sistema o dall’amministratore di prodotto dell’organizzazione.

>[!TIP]
>
>Per aggiungere più utenti contemporaneamente, puoi eseguire un [caricamento CSV in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
> 
> È inoltre possibile aggiungere più utenti a un ruolo creando un [gruppo di utenti](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Quindi puoi aggiungere il prodotto [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**] al gruppo di utenti.

## Informazioni sui ruoli

I seguenti ruoli sono disponibili per [!DNL Adobe Commerce as a Cloud Service]. Per visualizzare o modificare questi ruoli, nell&#39;amministratore di Commerce passa a **Sistema** > **Autorizzazioni** > **Ruoli utente**.

* **Utenti** - Gli utenti hanno accesso come amministratore all&#39;amministratore di Commerce, ma non possono gestire l&#39;accesso a livello di prodotto in Admin Console. Gli utenti possono inoltre utilizzare i crediti per [creare istanze](./getting-started.md#create-an-instance) in [!DNL Commerce Cloud Manager].

* Gli sviluppatori [**Developers**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} dispongono di autorizzazioni utente e vengono aggiunti all&#39;istanza di Commerce come utente sviluppatore. Ciò significa che possono utilizzare l&#39;[interfaccia utente amministratore SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [configurare eventi](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} e [creare webhook](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Amministratori: esistono tre diversi tipi di amministratori:
   * [Amministratori di sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - L&#39;amministratore di sistema ha accesso a tutti i prodotti e profili di prodotto dell&#39;organizzazione tramite Admin Console.
   * [Amministratori di prodotto](#add-a-product-admin) - Gli amministratori di prodotto possono [gestire utenti, ruoli e autorizzazioni per il prodotto](#add-users-and-admins) in [!DNL Adobe Admin Console] e [gestire gli utenti in Commerce Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
   * [Amministratori del profilo di prodotto](#add-users-developers-and-product-profile-admins) - Gli amministratori del profilo di prodotto non hanno accesso all&#39;amministratore Adobe Commerce, ma possono gestire gli utenti per il prodotto in [!DNL Adobe Admin Console].

Per informazioni dettagliate sulle autorizzazioni concesse a ogni ruolo all&#39;interno di Adobe Commerce, consulta [autorizzazioni utente](#user-permissions).

## Aggiungi un amministratore prodotto

1. Passa a https://adminconsole.adobe.com e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Nella scheda [!UICONTROL **Prodotti**], in [!UICONTROL **Prodotti e servizi**], selezionare il prodotto [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**].

   ![seleziona il prodotto](./assets/backend.png){width="600" zoomable="yes"}

1. Selezionare la scheda [!UICONTROL **Amministratori**].

1. Fai clic su [!UICONTROL **Aggiungi amministratore**].

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere come amministratori e fare clic su [!UICONTROL **Salva**].

## Aggiungere utenti, sviluppatori e amministratori dei profili di prodotto

Le istruzioni seguenti forniscono informazioni su come aggiungere utenti e sviluppatori a [!DNL Commerce Cloud Manager] e all&#39;amministratore di Commerce. L&#39;interfaccia [!DNL Commerce Cloud Manager] consente di creare e gestire le istanze di Commerce.

>[!NOTE]
>
>Solo gli amministratori di prodotto e gli amministratori di sistema possono aggiungere utenti e sviluppatori al prodotto Adobe Commerce as a Cloud Service.

1. Passa a https://adminconsole.adobe.com e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Nella scheda [!UICONTROL **Prodotti**], in [!UICONTROL **Prodotti e servizi**], selezionare il prodotto [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**].

   ![seleziona il prodotto](./assets/backend.png){width="600" zoomable="yes"}

1. Fare clic sul profilo di prodotto [!UICONTROL **Predefinito - Cloud Manager**].

1. Seleziona la scheda [!UICONTROL **Utenti**], [!UICONTROL **Sviluppatori**] o [!UICONTROL **Amministratori**] e fai clic su [!UICONTROL **Aggiungi utenti**] o [!UICONTROL **Aggiungi sviluppatori**] o [!UICONTROL **Aggiungi amministratori**].

   >[!NOTE]
   >
   >Gli amministratori aggiunti da questa schermata sono [amministratori del profilo di prodotto](#understanding-roles) e non hanno accesso all&#39;amministratore di Commerce.

   ![tab select](./assets/tab-select.png){width=600 zoomable=&quot;yes&quot;}

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere come amministratori e fare clic su [!UICONTROL **Salva**].

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
