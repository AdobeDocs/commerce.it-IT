---
title: Configurare la vetrina
description: Scopri come eseguire lo strumento di scaffolding per configurare la tua [!DNL Adobe Commerce as a Cloud Service] vetrina.
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 6eda2197fde2e88292e58b2bb4fc4759f24da558
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Configurare la vetrina

Per configurare [!DNL Adobe Commerce Storefront] con tecnologia [!DNL Edge Delivery Services] per [!DNL Adobe Commerce as a Cloud Service] (SaaS), completare la procedura seguente.

Per informazioni dettagliate e personalizzabili, consulta la [documentazione della vetrina](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

1. Aprire lo strumento [creatore del sito](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Selezionare **[!UICONTROL Create New Site (Code & Content)]**.

1. Immettere **[!UICONTROL Github Organization/Username]** dove si desidera creare l&#39;archivio del codice storefront.

1. Immetti **[!UICONTROL Site Name]**.

1. Nel campo **[!UICONTROL Commerce GraphQL Endpoint (optional)]**, immetti l&#39;endpoint GraphQL [!DNL Adobe Commerce as a Cloud Service] (SaaS), a cui puoi accedere in Commerce Cloud Manager dopo [la creazione dell&#39;istanza](./getting-started.md#create-an-instance).

   In alternativa, se utilizzi [[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), immetti l&#39;endpoint GraphQL [!DNL API Mesh] nel campo **[!UICONTROL Commerce GraphQL Endpoint (optional)]**. Per ulteriori informazioni, vedere [creare una mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh).

1. Fare clic su **[!UICONTROL Create Site]**. Segui le istruzioni visualizzate per autorizzare l’accesso all’archivio GitHub.

Al termine del processo, puoi personalizzare la vetrina utilizzando i seguenti metodi:

* Personalizzare il codice: `https://github.com/<username or org>/<repo name>`
* Modifica il contenuto: `https://da.live/#/<username or org>/<repo name>`
* Gestisci configurazione: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* Anteprima vetrina: `https://main--<repo name>--<username or org>.aem.page/`

## Passaggi successivi

Per ulteriori informazioni, consulta i seguenti articoli:

* Per ulteriori informazioni sulla gestione e la visualizzazione di contenuto e dati nella vetrina, vedere [aggiornamento del contenuto della vetrina](./use-cases.md#update-storefront-content).
* Per ulteriori informazioni sulle funzionalità di sperimentazione contestuale, vedere [sperimentazione contestuale](./use-cases.md#contextual-experimentation).
* Per ulteriori informazioni sull&#39;utilizzo dell&#39;intelligenza artificiale generativa per automatizzare la generazione di contenuti di alta qualità, vedere [Genera varianti](./use-cases.md#generate-variations).
* Per ulteriori informazioni sull&#39;aggiornamento del contenuto del sito e sull&#39;integrazione con i componenti front-end e i dati di back-end di Commerce, vedere [[!DNL Adobe Commerce Storefront documentation]](https://experienceleague.adobe.com/developer/commerce/storefront/).
