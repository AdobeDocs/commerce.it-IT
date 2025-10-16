---
title: Gestione degli utenti
description: Scopri come creare e gestire utenti e assegnare ruoli utente per  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: 36a953d4fb0e1e14c7cb88a80f3b59d6fe8eb49e
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Gestione degli utenti

Per abilitare l&#39;accesso a [!DNL Adobe Commerce Optimizer], aggiungi gli utenti di [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} e assicurati che abbiano accesso al prodotto Commerce.

Puoi assegnare gli utenti a uno qualsiasi dei seguenti ruoli:

- **Utente**: gli utenti hanno accesso all&#39;interfaccia utente [!DNL Adobe Commerce Optimizer] per visualizzare e gestire le visualizzazioni catalogo e le regole di merchandising e per tenere traccia delle metriche delle prestazioni.

- [**Sviluppatore**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}: gli sviluppatori dispongono delle autorizzazioni utente e dell&#39;accesso a Adobe Developer Console. Ciò significa che possono creare progetti e configurare le credenziali per utilizzare strumenti per sviluppatori come API e SDK di [!DNL Adobe Commerce Optimizer] insieme a strumenti di estensibilità di Adobe come App Builder e API Mesh.

- **Amministratore** - Esistono tre diversi tipi di ruoli di amministratore:
   - [Amministratori di sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - L&#39;amministratore di sistema ha accesso a tutti i prodotti e i profili di prodotto dell&#39;organizzazione tramite Adobe Admin Console.
   - [Amministratori prodotto](#add-a-product-admin) - Gli amministratori prodotto possono [gestire utenti, ruoli e autorizzazioni per il prodotto](#add-users-and-admins) in [!DNL Adobe Admin Console].
   - [Amministratori dei profili di prodotto](#add-users-developers-and-product-profile-admins) - Gli amministratori dei profili di prodotto possono gestire gli utenti per il prodotto in [!DNL Adobe Admin Console].

## Aggiungi un amministratore prodotto

>[!BEGINTABS]

>[!NOTE]
>
>Assegna agli amministratori di prodotto il [ruolo utente](#add-users) prima di aggiungerli come amministratori di prodotto. Il ruolo Utente è richiesto per le autorizzazioni di base di Commerce.

>[!TAB GA (con provisioning dopo il 13 ottobre 2025)]

1. Passa a <https://adminconsole.adobe.com> e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Selezionare la scheda [!UICONTROL **Utenti**].

1. Selezionare la scheda [!UICONTROL **Amministratori**].

1. Fai clic su [!UICONTROL **Aggiungi amministratore**].

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere come amministratori e fare clic su [!UICONTROL **Avanti**].

1. Selezionare il ruolo [!UICONTROL **Amministratore del profilo di prodotto**].

1. Fai clic su **+** per aggiungere prodotti.

1. Seleziona l’istanza Commerce Optimizer esistente a cui aggiungere l’amministratore. Le istanze di Commerce Optimizer utilizzano il seguente formato: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Seleziona il profilo di prodotto.

1. Fare clic su [!UICONTROL **Applica**].

1. Fai clic su [!UICONTROL **Salva**].

>[!TAB Accesso anticipato (eseguito prima del 13 ottobre 2025)]

1. Passa a <https://adminconsole.adobe.com> e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Nella scheda [!UICONTROL **Prodotti**], in [!UICONTROL **Prodotti e servizi**], selezionare il prodotto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![seleziona il prodotto](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Selezionare la scheda [!UICONTROL **Amministratori**].

1. Fai clic su [!UICONTROL **Aggiungi amministratore**].

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere come amministratori e fare clic su [!UICONTROL **Salva**].

>[!ENDTABS]

## Aggiungi utenti

Le istruzioni seguenti forniscono informazioni su come aggiungere utenti a [!DNL Commerce Cloud Manager] e Commerce Optimizer. L&#39;interfaccia [!DNL Commerce Cloud Manager] consente di creare e gestire le istanze di Commerce Optimizer. Questo processo è necessario per tutti gli utenti, inclusi sviluppatori e amministratori.

>[!NOTE]
>
>Solo gli amministratori di prodotto e gli amministratori di sistema possono aggiungere utenti e sviluppatori al prodotto Adobe Commerce Optimizer.

>[!BEGINTABS]

>[!TAB GA (con provisioning dopo il 13 ottobre 2025)]

1. Passa a <https://adminconsole.adobe.com> e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Selezionare la scheda [!UICONTROL **Prodotti**].

1. Seleziona il prodotto [!UICONTROL **Adobe Commerce**].

1. Seleziona il prodotto Commerce Cloud Manager se desideri aggiungere l’utente all’interfaccia di Cloud Manager, in cui può creare e gestire le istanze di Commerce Optimizer, oppure seleziona l’istanza Commerce Optimizer esistente a cui aggiungere l’utente. Le istanze di Commerce Optimizer utilizzano il seguente formato: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Selezionare la scheda [!UICONTROL **Utenti**] e fare clic su [!UICONTROL **Aggiungi utenti**].

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere e fare clic su [!UICONTROL **Salva**].

1. Seleziona il profilo di prodotto desiderato.

1. Fare clic su [!UICONTROL **Applica**].

1. Fai clic su [!UICONTROL **Salva**].

>[!TAB Accesso anticipato (eseguito prima del 13 ottobre 2025)]

1. Passa a <https://adminconsole.adobe.com> e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Nella scheda [!UICONTROL **Prodotti**], in [!UICONTROL **Prodotti e servizi**], selezionare il prodotto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![seleziona il prodotto](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. Fare clic sul profilo di prodotto [!UICONTROL **Predefinito - Cloud Manager**].

1. Selezionare la scheda [!UICONTROL **Utenti**] e fare clic su [!UICONTROL **Aggiungi utenti**].

   ![scheda selezionata](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere e fare clic su [!UICONTROL **Salva**].

>[!ENDTABS]

### Aggiungere sviluppatori e amministratori dei profili di prodotto

Per aggiungere sviluppatori e amministratori dei profili di prodotto, ripetere il processo [aggiungi utenti](#add-users), ma selezionare la scheda [!UICONTROL **Sviluppatori**] o [!UICONTROL **Amministratori**] invece della scheda [!UICONTROL **Utenti**].

>[!NOTE]
>
>Assegna agli sviluppatori il ruolo Utente prima di aggiungerli come sviluppatori. Il ruolo Utente è richiesto per le autorizzazioni di base di Commerce.

![scheda selezionata](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## Gestione di utenti in blocco

Puoi aggiungere più utenti in modo più efficiente con uno dei seguenti metodi:

- Utilizza la funzionalità **Aggiungi utenti da CSV** in Adobe Admin Console per eseguire un [caricamento CSV in blocco](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Aggiungere più utenti a un ruolo creando un [gruppo di utenti](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Aggiungere quindi il prodotto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] al gruppo di utenti.

