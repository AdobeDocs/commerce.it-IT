---
title: 'Crea un pubblico in Real-Time CDP utilizzando i dati dell''evento  [!DNL Commerce] '
description: Scopri come utilizzare i dati evento  [!DNL Commerce]  per creare un pubblico in Real-Time CDP
role: Admin, Developer
feature: Personalization, Integration
exl-id: 0e9d286b-c459-44db-bbf8-2cb46e21739d
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# Crea tipi di pubblico in Real-Time CDP utilizzando i dati evento [!DNL Commerce]

Utilizza i dati evento acquisiti dall&#39;archivio [!DNL Commerce] per creare tipi di pubblico in Real-Time CDP. I dati acquisiti si basano sul comportamento di navigazione, sugli acquisti precedenti, sugli attributi del profilo, sulle tendenze di conversione o abbandono, sullo stato di fedeltà, sul valore elevato e basso per il cliente e su altro ancora.

## Quali dati devo prendere in considerazione per l’utilizzo?

Crea tipi di pubblico in Real-Time CDP utilizzando dati provenienti da eventi di vetrina, back office e profilo.

| Tipi di dati | Dati storefront (eventi comportamentali) | Dati di back office (eventi lato server) | Profilo cliente e dati dei segmenti |
|---|---|---|---|
| **Definizione** | Clic o azioni eseguite dai clienti sul sito. | Informazioni sul ciclo di vita e dettagli di ciascun ordine (passato e corrente). | Chi sono i tuoi acquirenti e a quali segmenti si qualificano. |
| **Eventi acquisiti da Adobe Commerce** | `productPageView`<br>`addToCart` | `placeOrder`<br>`orderplaced`<br>`orderLineItemRefunded`<br>`order Canceled`<br>`order history` | `createAccount`<br>`editAccount`<br>`Profile Record` |

## Quali sono stati i risultati ottenuti dagli altri clienti?

I clienti Adobe [!DNL Commerce] hanno ottenuto un impatto significativo sul business attivando tipi di pubblico incorporati in Real-Time CDP e distribuendoli alla loro istanza [!DNL Commerce].

Un retailer di abbigliamento globale e multi-brand ha ottenuto:

- Una fonte di verità con 10 milioni di profili cliente unificati
- Oltre 40 tipi di pubblico univoci di &quot;clienti ad alto intento&quot; creati per interagire con i diversi canali

Una società di bevande globale ha raccolto:

- 98 milioni di profili cliente da oltre 100 paesi

## Iniziamo

In questo articolo imparerai a:

- Creazione di un pubblico in Real-Time CDP in base ai dati [!DNL Commerce] raccolti dagli eventi
- Attiva il pubblico per l&#39;archivio [!DNL Commerce]
- Utilizza il pubblico in [!DNL Commerce] per informare una regola del prezzo del carrello

>[!IMPORTANT]
>
>Completa le attività descritte in questo articolo utilizzando il tuo ambiente sandbox [!DNL Commerce]. In questo modo, i dati dell’evento di vetrina e di back office inviati ad Experience Platform non diluiscono i dati dell’evento di produzione.

### Prerequisiti

Prima di iniziare, assicurati:

- È stato eseguito il provisioning per utilizzare Real-Time CDP. In caso di dubbi, rivolgiti all’integratore di sistemi o al team di sviluppo che gestisce progetti e ambienti.
- Hai [installato](install.md) e [configurato](connect-data.md) l&#39;estensione [!DNL Data Connection] in [!DNL Commerce].
- Hai [confermato](connect-data.md#confirm-that-event-data-is-collected) che i dati dell&#39;evento [!DNL Commerce] stanno arrivando al server Edge di Experience Platform.

### &#x200B;1. Creare un pubblico

Un pubblico è un insieme di clienti che condividono comportamenti o caratteristiche simili. In questo esercizio creerai un pubblico che qualifichi le persone interessate a un particolare prodotto del tuo negozio.

Per semplificare questo esercizio, utilizzare i dati evento dell&#39;evento `productPageView`. Questo evento acquisisce i dettagli del prodotto visualizzato, ad esempio nome del prodotto, SKU, prezzo e così via.

Utilizza questi dati evento per specificare che il pubblico include persone che hanno almeno un evento &quot;Visualizzazioni prodotto&quot; in cui lo SKU (identificatore prodotto) è uguale a un prodotto specifico sul sito e l’evento si verifica nell’ultimo giorno. &#x200B;

1. Apri Experience Platform e seleziona **[!UICONTROL Audiences]** dal menu di navigazione a sinistra.

   ![Dashboard del pubblico](assets/audience-left-rail.png)

1. Fare clic su **[!UICONTROL Create Audience]**.

   ![Crea pubblico](assets/browse-create-audience.png)

   Viene visualizzata l&#39;area di lavoro **Generatore di segmenti**.

1. Nell&#39;area di lavoro **Generatore di segmenti**, selezionare il metodo di creazione **Genera regola**.

   ![Genera regola](assets/build-rule.png)

   Nell&#39;area di lavoro **Generatore di segmenti** puoi definire le regole e le condizioni per il pubblico&#x200B; Queste regole e condizioni si basano sui dati di eventi e profili provenienti dal tuo archivio Commerce e definiscono i criteri che determinano se un utente è idoneo per il pubblico. Ad esempio, puoi creare una regola che includa gli utenti che hanno visualizzato un prodotto specifico o quelli che hanno effettuato un acquisto entro un determinato intervallo di tempo. Ulteriori informazioni su [Generatore di segmenti](https://experienceleague.adobe.com/it/docs/experience-platform/segmentation/ui/segment-builder) e sulle regole e condizioni.

1. Selezionare la scheda [Eventi](https://experienceleague.adobe.com/it/docs/experience-platform/segmentation/ui/segment-builder#events).

   ![Scheda Eventi](assets/audience-events-tab.png)

1. Cerca il tipo di evento &quot;Visualizzazioni prodotto&quot;. Trascinarlo quindi nell&#39;area di lavoro **Segment Builder**.

1. Torna alla scheda **Eventi** e cerca &quot;SKU&quot;, che è il campo dati nel campo `productListItems`. Trascinalo nell&#39;area di lavoro **Generatore di segmenti** sopra l&#39;evento **Visualizzazione prodotto**.

   La sezione **Regole evento** mostra dove puoi specificare il prodotto specifico da cui desideri creare il pubblico.

   ![Seleziona SKU](assets/audience-addsku.png)

1. Impostare l&#39;intervallo di tempo su un giorno facendo clic su **Qualsiasi ora** e selezionando *Ultimo* con valore di *1*.

   Durante la creazione di un pubblico, puoi specificare un intervallo di tempo per acquisire le attività recenti. Impostando un intervallo di tempo puoi indirizzare l’attività agli utenti in base alle loro interazioni o comportamenti recenti entro un arco temporale specifico.

1. Nella sezione **Proprietà pubblico** sul lato destro dell&#39;area di lavoro, imposta le proprietà del pubblico fornendo un nome, una descrizione e un metodo di valutazione per il pubblico.

1. Per salvare il pubblico, fare clic su **[!UICONTROL Save and Close]**.

   I dettagli del pubblico vengono visualizzati nel dashboard **Pubblico**.

### &#x200B;2. Attiva il pubblico nella destinazione [!DNL Commerce]

È possibile rendere disponibile un pubblico in [!DNL Commerce] attivandolo per la destinazione [!DNL Commerce].

>[!IMPORTANT]
>
>Se non hai già impostato [!DNL Commerce] come destinazione disponibile per la ricezione dei dati, consulta l&#39;argomento [Adobe [!DNL Commerce] Connection](https://experienceleague.adobe.com/it/docs/experience-platform/destinations/catalog/personalization/adobe-commerce).

1. Nella scheda **Dettagli** del pubblico, fai clic su **Attiva nella destinazione**.

1. Seleziona la destinazione [!DNL Commerce]. Quindi fare clic su **Avanti**.

1. Completare il processo di attivazione facendo clic su **[!UICONTROL Finish]**.

## &#x200B;3. Visualizzare il pubblico nel dashboard Pubblico

In [!DNL Commerce], puoi visualizzare tutti i [tipi di pubblico attivi](https://experienceleague.adobe.com/it/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations) che possono essere personalizzati per la tua istanza di [!DNL Commerce] utilizzando la dashboard **Tipi di pubblico di Real-Time CDP**.

Per accedere al dashboard **Tipi di pubblico di Real-Time CDP**, passa alla barra laterale _Amministratore_, quindi passa a **[!UICONTROL Customers]** > **[!UICONTROL Real-time CDP Audience]**.

Nel dashboard, cerca il pubblico creato. Nota che non viene utilizzato in una regola del prezzo del carrello o in un blocco dinamico. Nella sezione successiva, colleghi il pubblico a una regola del prezzo del carrello.

![Dashboard tipi di pubblico di Real-Time CDP](assets/real-time-cdp-dashboard.png)

### &#x200B;4. Crea una regola di prezzo del carrello in base al pubblico

Questa sezione mostra come creare una regola di prezzo del carrello in base al nuovo pubblico.

1. Verifica che il nuovo pubblico sia visualizzato nel dashboard **Tipi di pubblico di Real-Time CDP**.
1. [Crea una regola prezzo carrello](https://experienceleague.adobe.com/it/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create).
1. [Imposta la condizione](https://experienceleague.adobe.com/it/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#use-real-time-cdp-audiences-to-set-a-condition) della regola del prezzo del carrello utilizzando il nuovo pubblico.
1. [Imposta l&#39;azione](https://experienceleague.adobe.com/it/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#step-3-define-the-actions) che desideri eseguire quando il prodotto viene aggiunto al carrello.
1. Continua a configurare la regola prezzo carrello.
1. Vai alla visualizzazione del cliente dell’istanza sandbox.
1. Aggiungi al carrello il prodotto di cui hai basato il pubblico. Tieni presente che la regola del prezzo del carrello è abilitata.

## A capo

In questo esercizio hai creato un pubblico in Real-Time CDP e lo hai attivato nella destinazione [!DNL Commerce]. Quindi, nell&#39;amministratore [!DNL Commerce], hai creato una regola del prezzo del carrello basata su quel pubblico e hai abilitato la regola nel tuo ambiente sandbox.
