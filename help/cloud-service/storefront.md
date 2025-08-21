---
title: Configurare la vetrina
description: Scopri come eseguire lo strumento di scaffolding per configurare la vetrina  [!DNL Adobe Commerce as a Cloud Service] .
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: b0d492ffab2dcf5742772d02bed026e241ac43cd
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Configurare la vetrina

Per configurare la vetrina Adobe Commerce con tecnologia Edge Delivery Services per Adobe Commerce as a Cloud Service (SaaS), procedi come segue.

Per una procedura dettagliata più personalizzabile e dettagliata, consultare la [documentazione della vetrina](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=it).

1. Aprire lo strumento [creatore del sito](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Selezionare **Crea nuovo sito (codice e contenuto)**.

1. Immetti l&#39;**organizzazione Github/nome utente** in cui desideri creare l&#39;archivio del codice storefront.

1. Immetti un **nome sito**.

1. Nel campo **Commerce GraphQL Endpoint (facoltativo)**, inserisci l&#39;endpoint Adobe Commerce as a Cloud Service (SaaS) GraphQL, a cui puoi accedere in Commerce Cloud Manager dopo [la creazione della tua istanza](./getting-started.md#create-an-instance).

   In alternativa, se utilizzi [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), immetti l&#39;endpoint API Mesh GraphQL nel campo **Commerce GraphQL Endpoint (facoltativo)**. Per ulteriori informazioni, vedere [creare una mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh).

1. Fare clic su **Crea sito**. Segui le istruzioni visualizzate per autorizzare l’accesso all’archivio Github.

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
* Per ulteriori informazioni sull&#39;aggiornamento del contenuto del sito e sull&#39;integrazione con i componenti front-end e i dati back-end di Commerce, consulta la [documentazione Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=it).
