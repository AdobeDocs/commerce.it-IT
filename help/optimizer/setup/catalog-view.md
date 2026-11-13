---
title: Visualizzazioni catalogo
description: Scopri cosa sono le visualizzazioni catalogo e come crearle per organizzare il catalogo dei prodotti in base alla struttura aziendale, alle politiche e ai prezzi.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e [!DNL Adobe Commerce Optimizer] (infrastruttura SaaS gestita da Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
last-update: 2026-11-12
source-git-commit: 44918d5b636f0577c75010def79737acee1ffe0b
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
# Visualizzazioni catalogo per Merchandising Services

{{$include /help/_includes/ccdm-shared/setup/catalog-view.md}}

## Gestire le visualizzazioni catalogo

Utilizza queste istruzioni per gestire le visualizzazioni del catalogo:

- [Creare una visualizzazione catalogo](#create-a-catalog-view)—Impostare il nome, l&#39;origine del catalogo, i criteri e il listino prezzi. Quindi [specificare la visualizzazione del catalogo per i consigli e le regole di individuazione dei prodotti](#specify-catalog-views-for-recommendations-and-product-discovery-rules), esaminare [i livelli del catalogo](#catalog-layers) che sostituiscono gli attributi del prodotto o [rendere la visualizzazione del catalogo privata](#make-a-catalog-view-private).
- [Modificare una visualizzazione catalogo](#edit-a-catalog-view) - Aggiornarne le origini, i criteri, il listino prezzi e le impostazioni di protezione.
- [Eliminare una visualizzazione catalogo](#delete-a-catalog-view)—Rimuovere una visualizzazione catalogo non più necessaria.
- [Visualizza dettagli visualizzazione catalogo](#view-catalog-view-details)—Esamina la configurazione di una visualizzazione catalogo dalla tabella Visualizzazioni catalogo.

### Creare una vista catalogo

Prima di creare una vista catalogo, preparate i seguenti elementi in base alle esigenze:

- [origine catalogo](catalog-sources.md)
- [Criteri](policies.md) che definiscono i filtri dei prodotti
- [Livelli del catalogo](catalog-layer.md) se devi ignorare gli attributi del prodotto
- [Listini prezzi](pricebooks.md) per i prezzi visualizzati nella visualizzazione
- [Chiavi di accesso limitate](restricted-access-keys.md) se si desidera creare una visualizzazione di catalogo privata

#### Configurazione

In questa sezione, puoi creare una visualizzazione catalogo, selezionare un [criterio](policies.md) e un [listino prezzi dedicato](pricebooks.md).

1. Dal menu a sinistra, passare a **[!UICONTROL Store setup]** e fare clic su **[!UICONTROL Catalog views]**.

1. Fare clic su **[!UICONTROL Create catalog view]**. &#x200B;

1. Configura i dettagli di visualizzazione del catalogo:

   - **Nome** - Immettere il nome della visualizzazione del catalogo, ad esempio `Celport`. &#x200B;
   - **Origini catalogo** - Selezionare l&#39;[origine catalogo](catalog-sources.md), ad esempio `en-US`.
   - **Livelli catalogo** - Controlla i livelli acquisiti e la priorità.
   - **Criteri**: utilizzare il menu a discesa per selezionare i criteri rilevanti. Ad esempio, &quot;Marchio&quot;, &quot;Modello&quot;. &#x200B;Assicurarsi di avere già [creato un criterio](policies.md).

1. Selezionare il listino prezzi dedicato da collegare alla vista catalogo.

   - **Utilizzare tutti i listini prezzi disponibili**. Questa opzione consente di estrarre i dati relativi ai prezzi da tutti i listini prezzi disponibili.
   - **Consenti solo listini prezzi selezionati**. Questa opzione visualizza la finestra di dialogo **Aggiungi listini prezzi consentiti**. Utilizzare questa finestra di dialogo per selezionare il listino prezzi specifico da utilizzare per la visualizzazione catalogo.
   - **Solo listino prezzi dedicato**. Selezionare questa opzione se si applica un solo listino prezzi dedicato. Questa opzione è necessaria se si desidera configurare una vista di catalogo privata, che può fare riferimento a un solo listino prezzi dedicato. Consulta [Restrizione del listino prezzi dedicato alle visualizzazioni di cataloghi privati](private-catalog-view.md#price-book-restriction-on-private-catalog-views).
   - **Disabilita determinazione prezzi**. Questa opzione non è attualmente disponibile.

   >[!NOTE]
   >
   >L&#39;ID di un listino prezzi controlla la determinazione dei prezzi richiesta. Non limita l’accesso alla vista catalogo. Per limitare l&#39;accesso, abilitare Protezione catalogo per creare una [visualizzazione del catalogo privato](private-catalog-view.md).

1. (Facoltativo) Impostare **[!UICONTROL Catalog Protection]** su **[!UICONTROL Enabled]** per limitare i dati della visualizzazione catalogo ai client con un token firmato valido. Consulta [Proteggere una vista catalogo](private-catalog-view.md#protect-a-catalog-view) per i passaggi di configurazione.

1. Fare clic su **[!UICONTROL Add]** per creare la visualizzazione catalogo con i listini prezzi e i criteri collegati.

La pagina Visualizzazioni catalogo viene aggiornata per visualizzare la nuova visualizzazione del catalogo.&#x200B;

Dopo aver completato questi passaggi, la vista catalogo viene ora configurata per visualizzare prodotti e prezzi in base alle origini e ai criteri selezionati.

#### Specificare le viste catalogo per i consigli e le regole di individuazione prodotti

È possibile specificare una visualizzazione del catalogo quando si [creano unità di consigli](../merchandising/recommendations/create.md) o [regole di merchandising](../merchandising/rules/add.md).

#### Livelli del catalogo

I livelli catalogo consentono di ignorare gli attributi di prodotto selezionati senza modificare i dati del catalogo di origine. I livelli consentono di personalizzare nomi, descrizioni, immagini, collegamenti o metadati per una vista catalogo.

Vedi [Livelli catalogo](catalog-layer.md).

#### Imposta come privata la visualizzazione di un catalogo

Per impostazione predefinita, una vista catalogo è pubblica per le applicazioni client che possono accedere all’API di merchandising di GraphQL. Per limitare l&#39;accesso, configurare una visualizzazione del catalogo privato abilitando **[!UICONTROL Catalog Protection]**.

Per informazioni su come proteggere una visualizzazione catalogo e verificare che l&#39;accesso sia applicato, vedere [Visualizzazioni catalogo privato](private-catalog-view.md).

### Modificare una vista catalogo

1. Nell&#39;area di lavoro **[!UICONTROL Catalog views]** individuare la visualizzazione del catalogo.
1. Per aprire il menu delle azioni, selezionare (**[!UICONTROL ...]**).
1. Selezionare **[!UICONTROL Edit]** per accedere all&#39;editor di visualizzazione del catalogo.
1. Aggiornare il nome, le origini del catalogo, i criteri, le informazioni sul listino prezzi e le impostazioni di **[!UICONTROL Catalog Protection]** (incluse le chiavi di accesso con restrizioni assegnate) in base alle esigenze.
1. Fare clic su **[!UICONTROL Save]**.

### Eliminare una vista catalogo

1. Nell&#39;area di lavoro **[!UICONTROL Catalog views]** individuare la visualizzazione del catalogo.
1. Per aprire il menu delle azioni, selezionare (**[!UICONTROL ...]**).
1. Selezionare **[!UICONTROL Delete]**.
1. Conferma l’eliminazione.

   Quando viene visualizzata la finestra di conferma, fare clic su **[!UICONTROL Delete]**.

### Visualizza dettagli visualizzazione catalogo

Questa opzione consente di visualizzare rapidamente tutti i parametri di visualizzazione del catalogo mantenendo la tabella **[!UICONTROL Catalog views]**.

Nell&#39;area di lavoro **[!UICONTROL Catalog views]**, selezionare l&#39;icona ![informazioni](/help/assets/ccdm-shared/recommendations/info-icon.png) per una visualizzazione catalogo per visualizzarne i dettagli di configurazione.

![Dettagli visualizzazione catalogo](../assets/catalog-view-details.png)

Da qui puoi vedere i dettagli di configurazione della vista catalogo, ad esempio:

- ID visualizzazione
- Nome
- Origini del catalogo
- Criteri
- Data di creazione
- Dati modificati

Alcune di queste impostazioni di configurazione sono necessarie durante la configurazione della vetrina o l’utilizzo dell’API di acquisizione dati.
