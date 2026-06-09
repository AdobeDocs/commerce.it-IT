---
title: Utente e Identity Management
description: Scopri come creare e gestire utenti e assegnare ruoli utente per  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
TQID: https://experienceleague.adobe.com/ORS8H-GM48FMaTL7ywENU6lJnPrz7PULLhlu5AVlzDc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
  - id: ce84ce08-883f-4337-ae83-6bb1855ca732
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: dc50e4d7bcd118b2b9a800779c600ade5560e0bf
workflow-type: tm+mt
source-wordcount: 816
ht-degree: 0%

---

# Gestione degli utenti

Per abilitare l&#39;accesso a [!DNL Adobe Commerce Optimizer], aggiungi gli utenti di [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} e assicurati che abbiano accesso al prodotto Commerce.

Puoi assegnare gli utenti a uno qualsiasi dei seguenti ruoli:

- **Utente**: gli utenti hanno accesso all&#39;interfaccia utente [!DNL Adobe Commerce Optimizer] per visualizzare e gestire le visualizzazioni catalogo e le regole di merchandising e per tenere traccia delle metriche delle prestazioni.

- [**Sviluppatore**](https://helpx.adobe.com/it/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}: gli sviluppatori dispongono delle autorizzazioni utente e dell&#39;accesso a Adobe Developer Console. Ciò significa che possono creare progetti e configurare le credenziali per utilizzare strumenti per sviluppatori come API e SDK di [!DNL Adobe Commerce Optimizer] insieme a strumenti di estensibilità di Adobe come App Builder e API Mesh.

- **Amministratore** - Esistono tre diversi tipi di ruoli di amministratore:
   - [Amministratori di sistema](https://helpx.adobe.com/it/enterprise/using/admin-roles.html){target="_blank"} - L&#39;amministratore di sistema ha accesso a tutti i prodotti e i profili di prodotto dell&#39;organizzazione tramite Adobe Admin Console.
   - [Amministratori prodotto](#add-a-product-admin) - Gli amministratori prodotto possono [gestire utenti, ruoli e autorizzazioni per il prodotto](#add-users) in [!DNL Adobe Admin Console].
   - [Amministratori dei profili di prodotto](#add-developers-and-product-profile-admins) - Gli amministratori dei profili di prodotto possono gestire gli utenti per il prodotto in [!DNL Adobe Admin Console].

## Aggiungi un amministratore prodotto

>[!BEGINTABS]

>[!NOTE]
>
>Assegna agli amministratori di prodotto il [ruolo utente](#add-users) prima di aggiungerli come amministratori di prodotto. Il ruolo Utente è richiesto per le autorizzazioni di base di Commerce.

Esistono due modi diversi per aggiungere utenti amministratori di prodotto a [!DNL Adobe Commerce Optimizer] in base al momento in cui è stato eseguito il provisioning della tua organizzazione. Nelle organizzazioni con accesso anticipato, ogni utente a cui viene assegnato il ruolo di amministratore del prodotto dispone dell’autorizzazione per gestire tutte le istanze dell’organizzazione. Nelle organizzazioni con disponibilità generale (GA, General Availability) per le quali è stato eseguito il provisioning dopo il 13 ottobre 2025, è possibile assegnare un utente come amministratore del prodotto per istanze specifiche. Quando l’utente amministratore del prodotto effettua l’accesso, può visualizzare solo le istanze che dispone dell’autorizzazione per gestire.

>[!TAB GA (con provisioning dopo il 13 ottobre 2025)]

1. Passa a <https://adminconsole.adobe.com> e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Selezionare la scheda [!UICONTROL **Utenti**].

1. Selezionare la scheda [!UICONTROL **Amministratori**].

1. Fai clic su [!UICONTROL **Aggiungi amministratore**].

1. Immettere il nome utente o l&#39;indirizzo di posta elettronica degli utenti che si desidera aggiungere come amministratori e fare clic su [!UICONTROL **Avanti**].

1. Selezionare il ruolo [!UICONTROL **Amministratore del profilo di prodotto**].

1. Fai clic su **+** per aggiungere prodotti.

1. Seleziona l’istanza Commerce Optimizer esistente a cui aggiungere l’amministratore. Le istanze di Commerce Optimizer utilizzano il seguente formato: `Adobe Commerce - <instance-name> - Commerce Optimizer - <environment-type> - <tenant-id>`.

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
>Solo gli amministratori di prodotto e di sistema possono aggiungere utenti e sviluppatori al prodotto [!DNL Adobe Commerce Optimizer].

>[!BEGINTABS]

>[!TAB GA (con provisioning dopo il 13 ottobre 2025)]

1. Passa a <https://adminconsole.adobe.com> e accedi con il tuo Adobe ID.

1. Seleziona la tua organizzazione.

1. Selezionare la scheda [!UICONTROL **Prodotti**].

1. Seleziona il prodotto [!UICONTROL **Adobe Commerce**].

1. Seleziona il prodotto Commerce Cloud Manager se desideri aggiungere l’utente all’interfaccia di Cloud Manager, in cui può creare e gestire le istanze di Commerce Optimizer, oppure seleziona l’istanza Commerce Optimizer esistente a cui aggiungere l’utente. Le istanze di Commerce Optimizer utilizzano il seguente formato: `Adobe Commerce - <instance-name> - Commerce Optimizer - <environment-type> - <tenant-id>`.

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

- Utilizza la funzionalità **Aggiungi utenti da CSV** in Adobe Admin Console per eseguire un [caricamento CSV in blocco](https://helpx.adobe.com/it/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Aggiungere più utenti a un ruolo creando un [gruppo di utenti](https://helpx.adobe.com/it/enterprise/using/user-groups.html){target="_blank"}. Quindi puoi aggiungere i prodotti appropriati al gruppo di utenti.

## Gestione delle identità e configurazione single sign-on

{{ims-identity-and-sso-config}}
