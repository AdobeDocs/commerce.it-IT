---
title: Guida introduttiva a  [!DNL Adobe Commerce as a Cloud Service]
description: Scopri come iniziare a utilizzare  [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 911d984efa9587c0154db3ab97f6136bf6c34166
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 0%

---

# Introduzione

[!DNL Adobe Commerce as a Cloud Service] fornisce la maggior parte delle configurazioni pronte all&#39;uso. Dopo aver completato alcuni processi di configurazione di base, il tuo negozio sarà operativo in pochissimo tempo. Questa guida illustra come creare e lavorare con un’istanza. Questa guida ti aiuta anche a configurare la tua organizzazione per il successo garantendo ai tuoi team l&#39;accesso corretto a [!DNL Adobe Commerce as a Cloud Service] e agli strumenti necessari per iniziare.

[!DNL Adobe Commerce as a Cloud Service] è una piattaforma di e-commerce nativa per il cloud che offre flessibilità, scalabilità ed efficienza per la distribuzione di esperienze di e-commerce digitali. Questa offerta SaaS è una piattaforma completamente gestita e senza versioni che offre un’esperienza di aggiornamento fluida senza la necessità di interventi manuali.

## Componenti chiave

[!DNL Adobe Commerce as a Cloud Service] è costituito dai seguenti componenti:

* **[Adobe Experience Cloud](https://experience.adobe.com/)** - Punto di ingresso centrale per tutti i [!DNL Adobe Commerce] prodotti in [experience.adobe.com](https://experience.adobe.com/)
   * Fai clic su [!UICONTROL **Commerce**] in [!UICONTROL **Accesso rapido**] per aprire Commerce Cloud Manager
* **[Commerce Cloud Manager](https://experience.adobe.com/#/commerce/cloud-service)** - Crea e gestisci le istanze, accedi agli URL API e al tuo amministratore Commerce
* **[Adobe Admin Console](https://adminconsole.adobe.com/)** - Gestisci utenti e ruoli
* **Amministratore Commerce** - Gestisci prodotti, ordini, clienti e configurazione dello store
* **[Vetrina con tecnologia Edge Delivery Services](./storefront.md)**: crea e personalizza una vetrina rivolta ai clienti utilizzando un sistema componibile ad alte prestazioni che offre velocità, SEO e user experience eccezionali per commercianti e sviluppatori
* **[Adobe Developer App Builder](https://developer.adobe.com/app-builder/)** - Crea integrazioni personalizzate utilizzando App Builder, insieme ad altri strumenti di estensibilità come il [kit di avvio dell&#39;integrazione](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) e la [rete API](https://developer.adobe.com/graphql-mesh-gateway/)

## Configurazione e gestione

Come parte del processo di configurazione di [!DNL Adobe Commerce as a Cloud Service], l&#39;amministratore di sistema, i commercianti e gli sviluppatori configurano l&#39;accesso e le risorse per la tua organizzazione, incluso il provisioning delle risorse cloud e l&#39;assegnazione degli utenti ai ruoli appropriati in base alle loro responsabilità.

### Flusso di lavoro di configurazione e gestione

In qualità di gruppo combinato, l’amministratore di sistema, il commerciante e lo sviluppatore devono seguire questi passaggi essenziali per rendere operativa l’istanza di Commerce:

1. **Tutti gli utenti**: [Crea un&#39;istanza](#create-an-instance)
1. **Amministratore di sistema**: [Aggiungere utenti e assegnare ruoli](user-management.md#add-users-and-admins)
1. **Commercianti**: [Accedi all&#39;amministratore di Commerce](#access-an-instance) e [importa il tuo catalogo](#import-your-catalog)
1. **Sviluppatori**: [Configura la vetrina](storefront.md) ed esplora la [piattaforma per sviluppatori](overview.md#developer-platform)

#### Flusso di lavoro di AEM Assets e Product Visuals

Per integrare [!DNL Adobe Experience Manager Assets] o [!DNL Product Visuals powered by AEM Assets] con [!DNL Adobe Commerce as a Cloud Service] sono necessari i seguenti passaggi:

1. **Amministratore di sistema**: [Aggiungi utenti al profilo di prodotto AEM Assets e Product Visuals](user-management.md#add-a-user-to-aem-assets-or-product-visuals)
1. **Sviluppatori**: [Integrare AEM Assets e Visualizzazioni prodotto](../aem-assets-integration/overview.md)
1. **Commercianti**: [Accedi ai tuoi elementi visivi di AEM Assets e prodotti](./user-management.md#access-the-experience-manager-interface)

### Attività di configurazione e gestione basate sui ruoli

Seleziona una scheda di seguito per visualizzare gli elementi grafici del flusso di lavoro di alto livello per il ruolo corrispondente:

>[!BEGINTABS]

>[!TAB Flusso di lavoro amministratore di sistema e esercente]

Questo diagramma fornisce una panoramica generale del modo in cui amministratori di sistema e commercianti accedono e gestiscono le istanze di [!DNL Adobe Commerce as a Cloud Service]. Per ulteriori informazioni sui flussi di lavoro dell&#39;amministratore, vedere la [Guida di Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html).

![[!DNL Adobe Commerce as a Cloud Service] diagramma flusso esercente](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Flusso di lavoro sviluppatore]

Questo diagramma fornisce una panoramica di alto livello sulla creazione di integrazioni per [!DNL Adobe Commerce as a Cloud Service] da parte degli sviluppatori tramite App Builder. Per ulteriori informazioni, consulta la [documentazione API](https://developer.adobe.com/commerce/webapi/rest/).

![[!DNL Adobe Commerce as a Cloud Service] diagramma di flusso per sviluppatori](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

Seleziona il tuo ruolo per trovare le risorse per iniziare a utilizzare il processo di configurazione:

>[!BEGINTABS]

>[!TAB Amministratore di sistema]

In qualità di amministratore di sistema, sei responsabile della configurazione dell’organizzazione e della gestione dell’accesso degli utenti.

| Attività | Descrizione | Risorsa |
|------|-------------|----------|
| Comprendere la piattaforma | Scopri l’architettura e i vantaggi di Adobe Commerce as a Cloud Service | [Panoramica](overview.md) |
| Confrontare le funzioni | Comprendere le differenze tra Cloud Service e altre offerte Adobe Commerce | [Confronto delle funzionalità](feature-comparison.md) |
| Creare un’istanza | Provisioning di ambienti sandbox e di produzione | [Crea un&#39;istanza](#create-an-instance) |
| Configurare la gestione degli utenti | Aggiungere utenti, assegnare ruoli e gestire autorizzazioni | [Gestione utente](user-management.md) |
| Configurare AEM Assets e Visualizzazioni prodotto (facoltativo) | Aggiungere utenti, assegnare ruoli e gestire autorizzazioni | [Gestione utente](user-management.md#add-a-user-to-aem-assets-or-product-visuals) |

>[!TAB Commerciante]

In qualità di commerciante, ti concentri sulla gestione di prodotti, ordini e contenuti della vetrina.

| Attività | Descrizione | Risorsa |
|------|-------------|----------|
| Accedere all’istanza | Accedi all’amministratore di Commerce per gestire il tuo archivio | [Accedere a un&#39;istanza](#access-an-instance) |
| Esplora casi d’uso | Scopri gli scenari aziendali pratici e i flussi di lavoro | [Casi d&#39;uso](./use-cases.md) |
| Importa catalogo | Scopri come importare i dati di prodotto nella piattaforma | [Importa il catalogo](#import-your-catalog) |
| Accedere ad AEM Assets e ai visualizzatori di prodotto (facoltativo) | Accedi a Experience Manager per iniziare a utilizzare AEM Assets e gli elementi visivi di prodotto | [Accedere all&#39;interfaccia di Experience Manager](./user-management.md#access-the-experience-manager-interface) |

>[!TAB Sviluppatore]

In qualità di sviluppatore, devi sapere come creare integrazioni personalizzate ed estendere le funzionalità della piattaforma.

| Attività | Descrizione | Risorsa |
|------|-------------|----------|
| Architettura | Scopri l’estensibilità e le API della piattaforma | [Panoramica - Piattaforma per sviluppatori](overview.md#developer-platform) |
| Configurare un ambiente di sviluppo | Creare un’istanza sandbox per lo sviluppo e il test | [Crea un&#39;istanza](#create-an-instance) |
| Crea vetrina | Scopri come impostare e personalizzare Commerce Storefront | [Configurazione vetrina](./storefront.md) |
| Configurare la vetrina | Scopri come impostare la vetrina | [Configurazione vetrina](./storefront.md) |
| Esplora le opzioni di integrazione | Scopri App Builder, API Mesh e altri strumenti di estensibilità a cui hai accesso | [Panoramica - Piattaforma per sviluppatori](overview.md#developer-platform) |
| Integrare AEM Assets e Visualizzazioni prodotto (facoltativo) | Scopri come integrare AEM Assets e Product Visuals con Adobe Commerce | [Integrazione AEM Assets](../aem-assets-integration/overview.md) |

>[!ENDTABS]

### Passaggi successivi

Dopo aver completato le attività di configurazione specifiche per il ruolo:

* **Amministratori di sistema**: rivedi le [linee guida per la responsabilità condivisa](shared-responsibility.md)
* **Commercianti**: esplora [casi d&#39;uso](use-cases.md) per scenari aziendali comuni
* **Sviluppatori**: consulta la [documentazione per gli sviluppatori di Adobe Commerce](https://developer.adobe.com/commerce/docs)

## Nozioni di base su Adobe Commerce as a Cloud Service

Le sezioni seguenti descrivono i processi di base da completare per rendere operativa l’istanza di Commerce.

### Creare un’istanza

>[!NOTE]
>
>Prima di poter creare un&#39;istanza, l&#39;amministratore di prodotto o l&#39;amministratore di sistema dell&#39;organizzazione deve aggiungere l&#39;utente come utente del prodotto [!DNL Adobe Commerce as a Cloud Service]. Per ulteriori informazioni, vedere [Aggiungere utenti e amministratori](./user-management.md#add-users-and-admins).

[!DNL Adobe Commerce as a Cloud Service] istanze utilizzano un sistema basato sul credito. È possibile creare più istanze, ma ogni istanza richiede crediti disponibili. Il numero di crediti che hai inizialmente dipende dal tuo abbonamento.

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

### Accedere a un’istanza

Dopo aver creato un&#39;istanza, è possibile accedervi da [!UICONTROL Commerce Cloud Manager].

1. Accedi al tuo account [Adobe Experience Cloud](https://experience.adobe.com/).

1. In [!UICONTROL Quick access], fare clic su [!UICONTROL **Commerce**] per aprire [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] visualizza un elenco delle istanze disponibili nell&#39;organizzazione Adobe IMS.

1. Per aprire [!UICONTROL Commerce Admin] per un&#39;istanza, fare clic sul nome.

>[!TIP]
>
>Per visualizzare le informazioni sull’istanza, inclusi gli endpoint REST e GraphQL e l’URL amministratore, fai clic sull’icona delle informazioni accanto al nome dell’istanza.

Gli URL di base per l’amministratore e gli endpoint variano in base all’area geografica e all’ambiente, utilizzando il seguente pattern:

* Amministratore
   * Amministrazione produzione Nord America: `https://na1.admin.commerce.adobe.com`
   * Amministratore sandbox Nord America: `https://na1-sandbox.admin.commerce.adobe.com`
   * Amministratore produzione Europa: `https://eu1.admin.commerce.adobe.com`
* REST e GRAPHQL
   * GraphQL di produzione Nord America: `https://na1.api.commerce.adobe.com`
   * GraphQL sandbox Nord America: `https://na1-sandbox.api.commerce.adobe.com`
   * GraphQL di produzione Europa: `https://eu1.api.commerce.adobe.com`

### Importa il catalogo

Per impostazione predefinita, [!DNL Adobe Commerce as a Cloud Service] istanze non includono dati di prodotto. Puoi includere dati di prodotto di esempio quando crei un’istanza a scopo di test e apprendimento prima di importare il tuo catalogo.

Esistono due modi per importare il catalogo in [!DNL Adobe Commerce as a Cloud Service]:

* [**Amministratore Commerce**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) - Interfaccia intuitiva che consente di importare i dati del catalogo con pochi clic.
* [**Importa API JSON**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - API REST che consente di importare i dati del catalogo a livello di programmazione.

### Configurare la vetrina

Ora che hai creato un&#39;istanza, puoi [configurare la vetrina](storefront.md) con tecnologia Edge Delivery Services.

## Risorse aggiuntive

* [Note sulla versione](release-notes.md)
* [Guida alla migrazione](migration/overview.md)
* [Documentazione di Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)
