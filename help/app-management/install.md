---
title: Installa e accedi [!DNL App Management]
description: Prerequisiti e requisiti di accesso per utilizzare Adobe Commerce [!DNL App Management].
feature: App Builder, Extensibility, Integration
source-git-commit: 86c0945bbb0a562de1b66d420dec2a05d4d81e5f
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Installa e accedi a [!DNL App Management]

[!DNL App Management] è disponibile in Commerce Admin per le istanze di Commerce idonee. La disponibilità dipende dal tipo di distribuzione.

## Disponibilità

Dopo aver soddisfatto i seguenti requisiti, selezionare la scheda corrispondente per il tipo di distribuzione in uso per verificare se [!DNL App Management] richiede l&#39;installazione o è già disponibile nell&#39;istanza.

## Prerequisiti

Prima di associare un’app, assicurati di disporre dei seguenti elementi:

| Requisito | Descrizione |
|-------------|-------------|
| **Accesso amministratore** | Amministratore Commerce con autorizzazioni [!DNL App Management] |
| **App implementata** | Applicazione App Builder distribuita nella tua organizzazione e pronta per la connessione |
| **Accesso organizzazione** | Accesso all’organizzazione Adobe in cui è distribuita l’app |

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!DNL App Management] è disponibile automaticamente il [!DNL Adobe Commerce as a Cloud Service]. Non è richiesta alcuna installazione. [Abilitala nell&#39;amministratore](#access-app-management) e inizia ad associare le app.

>[!TAB Adobe Commerce on Cloud (PaaS) e on-premise]

* **Adobe Commerce 2.4.8 e versioni successive**—[!DNL App Management] è incluso automaticamente. Non è richiesta alcuna installazione.

* **Adobe Commerce da 2.4.5 a 2.4.7**—Installa [!DNL Admin UI SDK] (che include [!DNL App Management]) utilizzando il Compositore:

  ```bash
  composer require "magento/commerce-backend-sdk": ">=3.3"
  ```

  Quindi esegui:

  ```bash
  composer update
  bin/magento setup:upgrade
  bin/magento indexer:reindex
  bin/magento cache:clean
  ```

Per ulteriori informazioni, vedere [Installare o aggiornare Adobe Commerce Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/installation/){target="_blank"}.

>[!ENDTABS]

## Accedi a [!DNL App Management]

1. Accedi all’amministratore di Commerce.

1. Passa a **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

Viene visualizzata la visualizzazione [!DNL App Management]. Qui puoi associare, configurare e gestire le applicazioni App Builder.

## Installazione delle app App Builder

Se devi installare un&#39;app App Builder da Adobe Exchange (ad esempio, un&#39;integrazione predefinita o un&#39;app marketplace), consulta [Installare le app App Builder da Adobe Exchange](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"} per istruzioni dettagliate.

Dopo aver installato e distribuito un&#39;app, utilizzare [!DNL App Management] per [associarla all&#39;istanza di Commerce](manage-app.md#associate-an-app) e configurarne le impostazioni.

## Webhook e app Commerce

Alcune applicazioni App Builder utilizzano [webhook di Adobe Commerce](https://developer.adobe.com/commerce/extensibility/webhooks/) in modo che Commerce possa chiamare l&#39;app tramite HTTP quando si verificano determinati eventi (ad esempio, dopo il salvataggio di un prodotto). Gli endpoint del webhook e la logica di sottoscrizione sono definiti dallo sviluppatore **app** quando l&#39;applicazione viene generata e distribuita. Gli amministratori di store non configurano i webhook separatamente in Gestione app.

Dopo aver [associato l&#39;app](https://experienceleague.adobe.com/en/docs/commerce/app-management/manage-app/manage-app) all&#39;istanza di Commerce e aver completato le istruzioni di configurazione dell&#39;app, il comportamento del webhook segue l&#39;implementazione dell&#39;app.

Se [!DNL App Management] non è in grado di attivare l&#39;endpoint di convalida dell&#39;app (ad esempio, l&#39;URL non è raggiungibile o la risposta non soddisfa i requisiti), è possibile che nel dashboard [!DNL App Management] venga visualizzato un errore simile al seguente:

![Errore di convalida del webhook](assets/webhook-validation-error.png){width="600" zoomable="yes"}

Collabora con **lo sviluppatore di app** per correggere la configurazione o la distribuzione del webhook in modo che la convalida possa avere esito positivo.

**Sviluppatori di app**. Per implementare le sottoscrizioni dei webhook e le risposte del gestore da App Builder, vedi [Webhook](https://developer.adobe.com/commerce/extensibility/app-management/installation/webhooks/) nella documentazione per gli sviluppatori Commerce Extensibility e il pacchetto [`@adobe/aio-commerce-lib-webhooks`](https://github.com/adobe/aio-commerce-sdk/tree/main/packages/aio-commerce-lib-webhooks) su GitHub.
