---
title: Utilizza Adobe Journey Optimizer per inviare un’e-mail con carrello abbandonato
description: Scopri come utilizzare Adobe Journey Optimizer per inviare un’e-mail con carrello abbandonato.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 0%

---

# Utilizzare Adobe Journey Optimizer per inviare un messaggio e-mail per carrello abbandonato

Scopri come inviare un’e-mail o una notifica di ricoinvolgimento personalizzata se una sessione del carrello o del browser è stata abbandonata. In questo articolo, puoi utilizzare dati generati da clienti che hanno visualizzato una serie di prodotti e categorie, che sono coinvolti in un prodotto o che hanno trascorso del tempo su una pagina.

## Quali dati devo prendere in considerazione per l’utilizzo?

Crea un carrello abbandonato, sfoglia le e-mail o notifica utilizzando i dati provenienti da eventi di vetrina e di back office.

| Tipi di dati | Dati storefront (eventi comportamentali) | Dati di back office (eventi lato server) |
|---|---|---|
| **Definizione** | Clic o azioni eseguite dai clienti sul sito. | Informazioni sul ciclo di vita e dettagli di ciascun ordine (passato e corrente). |
| **Eventi acquisiti da Adobe Commerce** | [pageView](https://experienceleague.adobe.com/it/docs/commerce/data-connection/event-forwarding/events#pageview)<br>[productPageView](https://experienceleague.adobe.com/it/docs/commerce/data-connection/event-forwarding/events)<br>[addToCart](https://experienceleague.adobe.com/it/docs/commerce/data-connection/event-forwarding/events#addtocart)<br>[openCart](https://experienceleague.adobe.com/it/docs/commerce/data-connection/event-forwarding/events#opencart)<br>[startCheckout](https://experienceleague.adobe.com/it/docs/commerce/data-connection/event-forwarding/events#startcheckout)<br>[completeCheckout](https://experienceleague.adobe.com/it/docs/commerce/data-connection/event-forwarding/events#completecheckout) | [orderPlaced](https://experienceleague.adobe.com/it/docs/commerce/data-connection/event-forwarding/events-backoffice#orderplaced)<br>[Storico ordini](https://experienceleague.adobe.com/it/docs/commerce/data-connection/fundamentals/connect-data#send-historical-order-data) |

### Quali sono stati i risultati ottenuti dagli altri clienti?

I clienti Adobe [!DNL Commerce] hanno ottenuto un impatto significativo sul business implementando campagne di abbandono personalizzate con Adobe [!DNL Commerce], Adobe [!DNL Journey Optimizer] e Adobe [!DNL Real-Time CDP].

Un rivenditore di abbigliamento globale e multimarca ha raggiunto:

- Conversione 1.9x al clic delle nuove campagne
- Aumento del 57% dei ricavi derivanti dai percorsi di abbandono omni-channel
- Aumento del 41% del tasso di conversione delle campagne di ricoinvolgimento
- Più di 1000 nuovi acquirenti impegnati a settimana

Un&#39;azienda di bevande globale ha ottenuto:

- Il 36% dei tassi di apertura delle e-mail di ricoinvolgimento
- Incremento del 21% nelle percentuali di clickthrough
- Aumento dell&#39;8,5% nel tasso di conversione
- L&#39;89% degli abbandoni reimpiegati si converte

## Iniziamo

Questo caso d&#39;uso particolare si concentra sulla creazione di un&#39;e-mail del carrello abbandonata utilizzando i dati dell&#39;istanza [!DNL Commerce] e inviandola ad Adobe [!DNL Journey Optimizer].

### Cos’è Adobe Journey Optimizer?

[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=it) ti consente di personalizzare l&#39;esperienza di e-commerce per i tuoi acquirenti. Ad esempio, puoi utilizzare Journey Optimizer per creare e distribuire campagne di marketing pianificate, come le promozioni settimanali di un negozio al dettaglio, o generare un’e-mail abbandonato nel carrello se un cliente ha aggiunto un prodotto a un carrello ma non lo ha completato.

In questo argomento imparerai a creare un&#39;e-mail del carrello abbandonata ascoltando un evento `checkout` generato dalla tua istanza di [!DNL Commerce] e rispondendo a tale evento in Journey Optimizer.

>[!IMPORTANT]
>
>A scopo dimostrativo, utilizza l&#39;ambiente sandbox [!DNL Commerce] per non diluire i dati dell&#39;evento di produzione con i dati dell&#39;evento di vetrina e di back office inviati ad Experience Platform.

### Prerequisiti

Prima di iniziare con questi passaggi, assicurati:

- È stato eseguito il provisioning per utilizzare Adobe [!DNL Journey Optimizer]. In caso di dubbi, rivolgiti all’integratore di sistemi o al team di sviluppo che gestisce progetti e ambienti.
- Hai [installato](install.md) e [configurato](connect-data.md) l&#39;estensione [!DNL Data Connection] in [!DNL Commerce].
- Hai [confermato](connect-data.md#confirm-that-event-data-is-collected) che i dati dell&#39;evento [!DNL Commerce] stanno arrivando al server Edge di Experience Platform.

## Passaggio 1: creare un utente nell&#39;ambiente sandbox [!DNL Commerce]

Crea un utente nell’ambiente sandbox e verifica che le informazioni sull’account utente siano visualizzate in Experience Platform. Verifica che l’e-mail specificata sia valida, poiché verrà utilizzata più avanti in questa sezione per inviare l’e-mail del carrello abbandonato.

1. Accedi o crea un account nell&#39;ambiente sandbox [!DNL Commerce].

   ![Accedi al tuo account di prova](assets/sign-in-account.png){width="700" zoomable="yes"}

   Con l&#39;estensione [!DNL Data Connection] installata e configurata, queste informazioni sull&#39;account vengono inviate ad Experience Platform come profilo.

1. Verificare che le informazioni sull&#39;account utente siano visualizzate nella sezione **[!UICONTROL Profile]** di Experience Platform.

   Vai a **[!UICONTROL Profiles]** nel Adobe Experience Platform. Fare clic su **[!UICONTROL Detail]** nel profilo per visualizzare il profilo creato.

   ![Conferma profilo](assets/check-event-profile.png){width="700" zoomable="yes"}

## Passaggio 2: visualizzare gli eventi in Journey Optimizer

Nell&#39;ambiente sandbox [!DNL Commerce], attiva gli eventi nella vetrina visualizzando le pagine dei prodotti, aggiungendo elementi al carrello e completando varie altre attività eseguite da un acquirente. Quindi, verifica che questi eventi vengano trasmessi a Journey Optimizer.

1. Avvia [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=it).
1. Selezionare **[!UICONTROL Profiles]**.
1. Imposta **[!UICONTROL Identity namespace]** su `Email`.
1. Imposta **[!UICONTROL Identity value]** sul tuo indirizzo e-mail.
1. Selezionare il profilo, quindi la scheda **[!UICONTROL Events]**.

   ![Verifica dettagli evento](assets/check-event-details.png){width="700" zoomable="yes"}

   Cercare l&#39;evento `commerce.checkouts` ed esaminare il payload dell&#39;evento:

   ```json
   "personID": "84281643067178465783746543501073369488", 
   "eventType": "commerce.checkouts", 
   "_id": "4b41703f-e42e-485b-8d63-7001e3580856-0", 
   "commerce": { 
       "cart": {}, 
       "checkouts": { 
           "value": 1 
       } 
   ```

   Come puoi vedere, il payload completo dell’evento contiene dati dettagliati sull’evento. Nella sezione successiva, configurerai gli eventi in Journey Optimizer per l&#39;ascolto e la risposta all&#39;evento `commerce.checkouts` generato dalla tua vetrina [!DNL Commerce].

## Passaggio 3: configurare gli eventi in Journey Optimizer

Configurare due eventi in Journey Optimizer: uno ascolta l&#39;evento `commerce.checkouts` da Commerce e l&#39;altro è un evento di timeout di base che attende un periodo di tempo specifico prima di attivare un&#39;e-mail del carrello abbandonata.

### Creare un evento listener

1. Avvia [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=it).

1. Fare clic su **[!UICONTROL Configurations]** nella sezione **[!UICONTROL Administration]** del riquadro sinistro.

1. Nel riquadro **[!UICONTROL Events]**, fare clic su **[!UICONTROL Manage]**.

   ![Configurazione evento Journey Optimizer](assets/ajo-config.png){width="700" zoomable="yes"}

1. Nella pagina **[!UICONTROL Events]**, fare clic su **[!UICONTROL Create Event]**.

1. Nella navigazione corretta, imposta l’evento come segue:

   1. Imposta **[!UICONTROL Name]** su: `firstname_lastname_checkout`.
   1. Imposta **[!UICONTROL Type]** su **[!UICONTROL Unitary]**.
   1. Imposta **[!UICONTROL Event id typ]e** su **[!UICONTROL Rule based]**.
   1. Imposta **[!UICONTROL Schema]** sullo [!DNL Commerce] [schema](update-xdm.md).
   1. Selezionare **[!UICONTROL Fields]** per aprire la pagina **[!UICONTROL Fields]**. Quindi, seleziona i campi utili per questo evento. Selezionare ad esempio tutti i campi in **[!UICONTROL Product list items]**, **[!UICONTROL Commerce]**, **[!UICONTROL eventType]** e **[!UICONTROL Web]**.
   1. Fare clic su **[!UICONTROL OK]** per salvare i campi selezionati.
   1. Fare clic all&#39;interno del campo **[!UICONTROL Event id condition]**. Quindi, crea una condizione: `eventType` è uguale a `commerce.checkouts` E `personalEmail.address` è uguale all&#39;indirizzo e-mail utilizzato al momento della creazione del profilo nella sezione precedente.

      ![Imposta condizione Journey Optimizer](assets/ajo-set-condition.png){width="700" zoomable="yes"}

   1. Fare clic su **[!UICONTROL OK]**.
   1. Fai clic su **[!UICONTROL Save]** per salvare l&#39;evento.

### Creare un evento di timeout

1. Crea un evento in Journey Optimizer come hai fatto in precedenza.

1. Nella navigazione corretta, imposta l’evento come segue:

   1. Imposta **[!UICONTROL Name]** su: `firstname_lastname_timeout`.
   1. Imposta **[!UICONTROL Type]** su **[!UICONTROL Unitary]**.
   1. Imposta **[!UICONTROL Event id type]** su **[!UICONTROL Rule based]**.
   1. Imposta **[!UICONTROL Schema]** sullo [!DNL Commerce] [schema](update-xdm.md).
   1. Impostare **[!UICONTROL Schema]**, **[!UICONTROL Fields]** e **[!UICONTROL Event id condition]** come sopra.
   1. Fai clic su **[!UICONTROL Save]** per salvare l&#39;evento.

Con questi due eventi configurati, crea un percorso che invia un’e-mail del carrello abbandonata.

## Passaggio 4: creare un percorso di pagamento

Creare un percorso che ascolti l&#39;evento `commerce.checkouts` e quindi invii un&#39;e-mail del carrello abbandonato dopo un periodo di tempo specificato.

1. In Journey Optimizer, selezionare **[!UICONTROL Journeys]** in **J[!UICONTROL OURNEY MANAGEMENT]**.
1. Fare clic su **[!UICONTROL Create Journey]**.
1. Specifica il nome del percorso.
1. Fare clic su **[!UICONTROL OK]** per salvare il percorso.
1. Nel menu di navigazione a sinistra della sezione **[!UICONTROL EVENTS]**, cerca l&#39;evento di estrazione creato in precedenza: `firstname_lastname_checkout` e trascinalo sull&#39;area di lavoro.

   >[!TIP]
   >
   >Facendo doppio clic sull’evento, questo viene aggiunto automaticamente all’area di lavoro.

1. Cerca l’evento timeout e aggiungilo all’area di lavoro.
1. Fare doppio clic sull&#39;evento di timeout.

   1. Nella sezione **[!UICONTROL Timeout]** selezionare la casella di controllo **[!UICONTROL Define the event time]**.
   1. Nel campo **[!UICONTROL Wait for]** immettere `1` e `Minute`.
   1. Selezionare la casella di controllo **[!UICONTROL Set a timeout path]**.

   Con questa configurazione di timeout, un acquirente che esegue un pagamento ma non completa l’ordine entro un minuto attiva questo ramo di timeout. In un ambiente di produzione effettivo, imposterai questo valore per un periodo più lungo, ad esempio 24 ore.

1. Nella barra di navigazione a sinistra in **[!UICONTROL ACTIONS]**, aggiungi l&#39;azione **[!UICONTROL Email]** al ramo di timeout. Il percorso deve essere simile al seguente:

   ![Area di lavoro Journey Optimizer](assets/ajo-canvas.png){width="700" zoomable="yes"}

### Creare un messaggio e-mail per carrello abbandonato

Crea un’e-mail carrello abbandonata che viene inviata quando viene rilevato un carrello abbandonato.

1. Nel percorso creato in precedenza, fare doppio clic sull&#39;icona **[!UICONTROL Email]** nell&#39;area di lavoro.

1. Segui i [passaggi](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/personalization/personalization-use-cases/personalization-use-case-helper-functions.html?lang=it#configure-email) nella guida di Journey Optimizer per creare l’e-mail del carrello abbandonato.

Ora disponi di un percorso in Journey Optimizer che ascolta l&#39;evento `commerce.checkouts` dal tuo archivio [!DNL Commerce] e di un&#39;e-mail del carrello abbandonata, inviata dopo un certo periodo di tempo. Nella sezione successiva viene illustrato come verificare il funzionamento del percorso.

## Passaggio 5: attivare l’evento di pagamento in tempo reale

In questa sezione l’evento viene testato in tempo reale.

1. In Journey Optimizer, attiva la modalità di test.

   ![Abilita modalità di test](assets/ajo-enable-test.png){width="700" zoomable="yes"}

1. Per eseguire il test del percorso in tempo reale, aprire un&#39;altra scheda del browser e visitare il sito Web [!DNL Commerce] nell&#39;ambiente sandbox.

   1. Aggiungi un prodotto al carrello.
   1. Passa alla pagina di pagamento.
   1. Dalla pagina di pagamento, abbandona il carrello tornando alla pagina principale o chiudendo la scheda.

      Il percorso è ora attivato. Per confermare, apri la scheda con il percorso in Journey Optimizer. Dovresti trovare una freccia verde che mostra il percorso attraversato dall’utente.

1. Controlla la casella in entrata dell’e-mail.
