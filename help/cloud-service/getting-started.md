---
title: Guida introduttiva a  [!DNL Adobe Commerce as a Cloud Service]
description: Scopri come iniziare a utilizzare  [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: d8c0cf5f54a8518b033013cdb24b25f8ff363f02
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Introduzione

[!DNL Adobe Commerce as a Cloud Service] fornisce la maggior parte delle configurazioni pronte all&#39;uso. Dopo aver completato alcuni processi di configurazione di base, il tuo negozio sarà operativo in pochissimo tempo. Questa guida illustra come creare e lavorare con un’istanza.

Fai clic sulle schede seguenti per visualizzare le panoramiche dei flussi di lavoro di alto livello per i seguenti tipi di utenti:

* Amministratori
* Commercianti
* Sviluppatori

>[!BEGINTABS]

>[!TAB Flusso di lavoro amministratore e esercente]

Questo diagramma fornisce una panoramica generale del modo in cui amministratori e commercianti accedono e gestiscono le istanze di [!DNL Adobe Commerce as a Cloud Service]. Per ulteriori informazioni sui flussi di lavoro dell&#39;amministratore, vedere la [Guida di Adobe Admin Console](https://helpx.adobe.com/it/enterprise/admin-guide.html).

![[!DNL Adobe Commerce as a Cloud Service] diagramma flusso esercente](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Flusso di lavoro sviluppatore]

Questo diagramma fornisce una panoramica di alto livello sulla creazione di integrazioni per [!DNL Adobe Commerce as a Cloud Service] da parte degli sviluppatori tramite App Builder. Per ulteriori informazioni, consulta la [documentazione API](https://developer.adobe.com/commerce/webapi/rest/).

![[!DNL Adobe Commerce as a Cloud Service] diagramma di flusso per sviluppatori](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## Creare un’istanza

>[!NOTE]
>
>Prima di poter creare un&#39;istanza, l&#39;amministratore di prodotto o l&#39;amministratore di sistema dell&#39;organizzazione deve aggiungere l&#39;utente come utente del prodotto [!DNL Adobe Commerce as a Cloud Service]. Per ulteriori informazioni, vedere [Aggiungere utenti e amministratori](./user-management.md#add-users-and-admins).

[!DNL Adobe Commerce as a Cloud Service] istanze utilizzano un sistema basato sul credito. È possibile creare più istanze, ma ogni istanza richiede una quantità relativa di crediti. La quantità di crediti che hai inizialmente dipende dal tuo abbonamento.

1. Accedi al tuo account [Adobe Experience Cloud](https://experience.adobe.com/).

1. In [!UICONTROL Quick access], fare clic su [!UICONTROL **Commerce**] per aprire [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visualizza un elenco di [!DNL Adobe Commerce as a Cloud Service] istanze disponibili nell&#39;organizzazione Adobe IMS.

1. Fai clic su [!UICONTROL **Aggiungi istanza**] nell&#39;angolo superiore destro della schermata.

   ![Crea istanza](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Seleziona [!UICONTROL **Commerce as a Cloud Service**].

1. Immetti **Nome** e **Descrizione** per l&#39;istanza.

1. Scegli il [!UICONTROL **Tipo di ambiente**] per la tua istanza. Puoi scegliere tra le seguenti opzioni:

   * [!UICONTROL **Sandbox**] - Ideale per scopi di progettazione e test. Devi iniziare il percorso [!DNL Adobe Commerce as a Cloud Service] utilizzando l&#39;ambiente sandbox.
   * [!UICONTROL **Produzione**] - Per negozi live e siti rivolti ai clienti.

   >[!NOTE]
   >
   >* Le istanze sandbox sono limitate all’area Nord America.
   >* L’opzione per installare i dati di esempio non è attualmente disponibile.

1. Seleziona l’area geografica in cui desideri che sia ospitata l’istanza.

   >[!NOTE]
   >
   >Dopo aver creato l’istanza, non potrai modificare l’area geografica.

1. Fai clic su [!UICONTROL **Aggiungi istanza**].

## Accedere a un’istanza

Dopo aver creato un&#39;istanza, è possibile accedervi da [!UICONTROL Commerce Cloud Manager].

1. Accedi al tuo account [Adobe Experience Cloud](https://experience.adobe.com/).

1. In [!UICONTROL Quick access], fare clic su [!UICONTROL **Commerce**] per aprire [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visualizza un elenco delle istanze disponibili nell&#39;organizzazione Adobe IMS.

1. Per aprire [!UICONTROL Commerce Admin] per un&#39;istanza, fare clic sul nome.

>[!TIP]
>
>Per visualizzare le informazioni sull’istanza, inclusi gli endpoint REST e GraphQL e l’URL amministratore, fai clic sull’icona delle informazioni accanto al nome dell’istanza.

## Importa il catalogo

Per impostazione predefinita, [!DNL Adobe Commerce as a Cloud Service] istanze non includono dati di prodotto. Puoi includere dati di prodotto di esempio quando crei un’istanza a scopo di test e apprendimento prima di importare il tuo catalogo.

Esistono due modi per importare il catalogo in [!DNL Adobe Commerce as a Cloud Service]:

* [**Amministratore Commerce**](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/import/data-import) - Interfaccia intuitiva che consente di importare i dati del catalogo con pochi clic.
* [**Importa API JSON**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - API REST che consente di importare i dati del catalogo a livello di programmazione.

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## Configurare la vetrina

Ora che hai creato un&#39;istanza, sei pronto per procedere con [la configurazione](storefront.md) della tua vetrina Commerce con tecnologia Edge Delivery Services.
