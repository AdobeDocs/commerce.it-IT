---
title: Installa e accedi [!DNL App Management]
description: Prerequisiti e requisiti di accesso per utilizzare Adobe Commerce [!DNL App Management].
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

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

Se devi installare un&#39;app App Builder da Adobe Exchange (ad esempio, un&#39;integrazione predefinita o un&#39;app marketplace), consulta [Installare le app App Builder da Adobe Exchange](https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"} per istruzioni dettagliate.

Dopo aver installato e distribuito un&#39;app, utilizzare [!DNL App Management] per [associarla all&#39;istanza di Commerce](manage-app.md#associate-an-app) e configurarne le impostazioni.
