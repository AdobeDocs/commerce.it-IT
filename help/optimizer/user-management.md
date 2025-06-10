---
title: Gestione degli utenti
description: Scopri come gestire gli utenti in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 1427db02c65fd45777f69eac3d10417d6e6177a1
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Gestione degli utenti

>[!NOTE]
>
>Questa documentazione sulla gestione degli utenti è destinata ai partecipanti con accesso anticipato e istruzioni di onboarding per gestire ed eseguire il provisioning di [!DNL Adobe Commerce Optimizer] utenti all&#39;interno della propria organizzazione Adobe. Se non disponi di queste istruzioni, contatta il rappresentante del tuo account per assistenza nella gestione degli utenti. Durante il programma di accesso anticipato, il provisioning degli utenti per [!DNL Adobe Commerce Optimizer] viene gestito assegnando gli utenti alla soluzione di prodotto **[!UICONTROL Adobe Commerce as a Cloud Service - backend]**.

Per abilitare l&#39;accesso a [!DNL Adobe Commerce Optimizer], aggiungi gli utenti di [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} e assicurati che abbiano accesso al prodotto Commerce.

Puoi assegnare gli utenti a uno qualsiasi dei seguenti ruoli:

* **Utente** - Gli utenti hanno accesso all&#39;interfaccia utente [!DNL Adobe Commerce Optimizer] per visualizzare e gestire le visualizzazioni catalogo e le regole di merchandising e per tenere traccia delle metriche delle prestazioni.

* [**Sviluppatore**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Gli sviluppatori dispongono delle autorizzazioni utente e dell&#39;accesso a Adobe Developer Console. Ciò significa che possono creare progetti e configurare le credenziali per utilizzare strumenti per sviluppatori come API e SDK di [!DNL Adobe Commerce Optimizer] insieme a strumenti di estensibilità di Adobe come App Builder e API Mesh.

* **Amministratore** - Esistono tre diversi tipi di ruoli di amministratore:
   * [Amministratori di sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - L&#39;amministratore di sistema ha accesso a tutti i prodotti e i profili di prodotto dell&#39;organizzazione tramite Adobe Admin Console.
   * [Amministratori prodotto](#add-a-product-admin) - Gli amministratori prodotto possono [gestire utenti, ruoli e autorizzazioni per il prodotto](#add-users-and-admins) in [!DNL Adobe Admin Console].
   * [Amministratori dei profili di prodotto](#add-users-developers-and-product-profile-admins) - Gli amministratori dei profili di prodotto possono gestire gli utenti per il prodotto in [!DNL Adobe Admin Console].

## Aggiungi un amministratore prodotto

1. Passa a [Admin Console](https://adminconsole.adobe.com) e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Nella scheda [!UICONTROL **Prodotti**], in [!UICONTROL **Prodotti e servizi**], selezionare il prodotto [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**].

   ![seleziona il prodotto](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Selezionare la scheda [!UICONTROL **Amministratori**].

1. Fai clic su [!UICONTROL **Aggiungi amministratore**].

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere come amministratori e fare clic su [!UICONTROL **Salva**].

## Aggiungere utenti, sviluppatori e amministratori dei profili di prodotto

>[!BEGINSHADEBOX &quot;Prerequisiti&quot;]
>
>Per la gestione degli utenti è necessario il provisioning seguente:

* Organizzazione IMS con provisioning per [!DNL Adobe Commerce Optimizer]
* Un account Adobe Experience Cloud nella stessa organizzazione IMS con il ruolo di amministratore di sistema o di prodotto

>[!ENDSHADEBOX]

Utilizzare le istruzioni seguenti per aggiungere utenti e sviluppatori a [!DNL Commerce Cloud Manager], dove si gestiscono le istanze di Commerce.

1. Passa a https://adminconsole.adobe.com e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Nella scheda [!UICONTROL **Prodotti**], in [!UICONTROL **Prodotti e servizi**], selezionare il prodotto [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**].

   ![seleziona il prodotto](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Fare clic sul profilo di prodotto [!UICONTROL **Predefinito - Cloud Manager**].

1. Seleziona la scheda [!UICONTROL **Utenti**], [!UICONTROL **Sviluppatori**] o [!UICONTROL **Amministratori**] e fai clic su [!UICONTROL **Aggiungi utenti**] o [!UICONTROL **Aggiungi sviluppatori**] o [!UICONTROL **Aggiungi amministratori**].

   Gli amministratori aggiunti da questa schermata vengono assegnati al gruppo [amministratori del profilo di prodotto](#understanding-roles).

   ![scheda selezionata](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere come amministratori e fare clic su [!UICONTROL **Salva**].

## Gestione di utenti in blocco

Puoi aggiungere più utenti in modo più efficiente con uno dei seguenti metodi:

* Utilizza la funzionalità **Aggiungi utenti da CSV** in Adobe Admin Console per eseguire un [caricamento CSV in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
* Aggiungere più utenti a un ruolo creando un [gruppo di utenti](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Quindi, aggiungi il prodotto [!UICONTROL **Adobe Commerce as a Cloud Service - Backend**] al gruppo di utenti.

