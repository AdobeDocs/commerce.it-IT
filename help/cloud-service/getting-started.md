---
title: Guida introduttiva ad Adobe Commerce as a Cloud Service
description: Scopri come iniziare a utilizzare Adobe Commerce as a Cloud Service.
role: Admin, Developer, User
source-git-commit: 19c49b2b9d630898353addd778e062d3208505c1
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# Introduzione

Adobe Commerce as a Cloud Service fornisce la maggior parte delle configurazioni pronte all’uso. Dopo aver completato alcuni processi di configurazione di base, il tuo negozio sarà operativo in pochissimo tempo. Questa guida illustra come creare e lavorare con un’istanza.

Fai clic sulle schede seguenti per visualizzare le panoramiche dei flussi di lavoro di alto livello per i seguenti tipi di utenti:

* Amministratori
* Commercianti
* Sviluppatori

>[!BEGINTABS]

>[!TAB Flusso di lavoro amministratore e esercente]

Questo diagramma fornisce una panoramica di alto livello del modo in cui amministratori e commercianti accedono e gestiscono le istanze di Adobe Commerce as a Cloud Service. Per ulteriori informazioni sui flussi di lavoro dell&#39;amministratore, vedere la [Guida di Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html).

![Diagramma di flusso per esercenti Adobe Commerce as a Cloud Service](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Flusso di lavoro sviluppatore]

Questo diagramma fornisce una panoramica di alto livello del modo in cui gli sviluppatori creano integrazioni per Adobe Commerce as a Cloud Service utilizzando App Builder. Per ulteriori informazioni, consulta la [documentazione API](https://developer.adobe.com/commerce/services/cloud/).

![Diagramma di flusso per sviluppatori Adobe Commerce as a Cloud Service](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## Creare un’istanza

Le istanze di Adobe Commerce as a Cloud Service utilizzano un sistema basato sul credito. È possibile creare più istanze, ma ogni istanza richiede una quantità relativa di crediti. La quantità di crediti che hai inizialmente dipende dal tuo abbonamento.

1. Accedi al tuo account [Adobe Experience Cloud](https://experience-stage.adobe.com/).

1. In [!UICONTROL Quick access], fare clic su [!UICONTROL **Commerce**] per aprire [!UICONTROL Commerce Cloud Manager].

   In [!UICONTROL Commerce Cloud Manager] viene visualizzato un elenco delle istanze di Adobe Commerce as a Cloud Service disponibili nell&#39;organizzazione Adobe IMS.

1. Fai clic su [!UICONTROL **Aggiungi istanza**] nell&#39;angolo superiore destro della schermata.

   ![Crea istanza](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Seleziona [!UICONTROL **Commerce as a Cloud Service**].

1. Immetti **Nome** e **Descrizione** per l&#39;istanza.

1. Seleziona l’area geografica in cui desideri che sia ospitata l’istanza.

   >[!NOTE]
   >
   >Dopo aver creato l’istanza, non potrai modificare l’area geografica.

1. Scegli il [!UICONTROL **Tipo di ambiente**] per la tua istanza. Puoi scegliere tra le seguenti opzioni:

   * [!UICONTROL **Sandbox**] - Ideale per scopi di progettazione e test. Devi iniziare il percorso Adobe Commerce as a Cloud Service utilizzando l’ambiente sandbox.
   * [!UICONTROL **Produzione**] - Per negozi live e siti rivolti ai clienti.

   >[!NOTE]
   >
   >Le istanze sandbox sono attualmente limitate all’area Nord America.

1. _(Facoltativo)_ Se desideri includere dati di prodotto di esempio a scopo di test e apprendimento, seleziona [!UICONTROL **Adobe Store**] dal menu a discesa [!UICONTROL **Dati di test**].

   Puoi saltare questa opzione, ma se lo fai nella vetrina non ci saranno prodotti. Dovrai [importare il catalogo](#import-your-catalog) per visualizzare l&#39;esperienza completa della vetrina.

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

Per impostazione predefinita, le istanze di Adobe Commerce as a Cloud Service non includono dati di prodotto. Puoi includere dati di prodotto di esempio quando crei un’istanza a scopo di test e apprendimento prima di importare il tuo catalogo.

Esistono due modi per importare il catalogo in Adobe Commerce as a Cloud Service:

* [**Amministratore Commerce**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) - Interfaccia intuitiva che consente di importare i dati del catalogo con pochi clic.
* [**Importa API JSON**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - API REST che consente di importare i dati del catalogo a livello di programmazione.

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## Configurare la vetrina

Ora che hai creato un&#39;istanza, sei pronto per procedere con [la configurazione](storefront.md) della tua vetrina Commerce con tecnologia Edge Delivery Services.
