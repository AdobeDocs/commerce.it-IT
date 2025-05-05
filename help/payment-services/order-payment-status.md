---
title: Rapporto Stato pagamento ordine
description: Utilizzare il rapporto Stato pagamento ordine per ottenere visibilità sullo stato di pagamento degli ordini e identificare eventuali problemi.
role: User
level: Intermediate
feature: Payments, Checkout, Orders
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 0%

---

# Rapporto Stato pagamento ordine

[!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] offre report completi che consentono di ottenere una chiara visualizzazione delle [transazioni](transactions.md), ordini e pagamenti del tuo Negozio.

Sono disponibili due visualizzazioni per la generazione di rapporti sullo stato dei pagamenti degli ordini per consentirti di visualizzare rapidamente lo stato dei pagamenti degli ordini:

* **[Visualizzazione dello stato dei pagamenti dell&#39;ordine](#order-payment-status-data-visualization-view)**—Grafico disponibile nella home di Payment Services che rappresenta visivamente gli stati dei pagamenti aggregati al giorno dalla visualizzazione del report Stato pagamenti dell&#39;ordine
* **[Visualizzazione report stato pagamento ordine](#order-payment-status-report-view)**—Report disponibile nello stato Pagamento ordine che mostra gli stati dettagliati di pagamento, fatturazione, spedizione, rimborso e controversia per tutte le transazioni

Le visualizzazioni dello stato del pagamento dell&#39;ordine consentono di comprendere facilmente la posizione di un ordine specifico all&#39;interno del flusso di elaborazione del contante dell&#39;ordine. Questi rapporti ti consentono di visualizzare rapidamente gli ordini in base allo stato e alla data di pagamento, identificando eventuali problemi.

È possibile [scaricare gli stati dei pagamenti degli ordini](#download-order-payment-statuses) in un formato di file .csv da utilizzare nel software di contabilità o gestione ordini esistente.

>[!NOTE]
>
>Non puoi visualizzare i report finanziari se non hai [attivato la modalità Live](production.md#enable-live-payments) per [!DNL Payment Services].

## Visualizzazione dati stato pagamento ordine

La visualizzazione dei dati sullo stato del pagamento dell&#39;ordine è disponibile nella Home page di Payment Services. Si tratta di una rappresentazione visiva degli stati di pagamento aggregati al giorno dalla tabella dettagliata [Visualizzazione report stato pagamento ordine](#order-payment-status-report-view).

Nella barra laterale _Amministratore_, vai a **Vendite** > **Servizi di pagamento** > _Ordini_ per visualizzare la visualizzazione dei dati [grafico degli stati dei pagamenti](#statuses-information).

![Visualizzazione dati di pagamento nell&#39;amministratore](assets/orderpayment-dataviz.png){width="800" zoomable="yes"}

Fare clic su **[!UICONTROL View Report]** per passare alla tabella dettagliata [Visualizzazione report stato pagamento ordini](#order-payment-status-report-view).

### Personalizzare gli stati nell’arco temporale

Per impostazione predefinita, vengono visualizzati 30 giorni di stato del pagamento.

Nella vista Visualizzazione stato pagamento ordine è possibile personalizzare l&#39;intervallo di tempo per gli stati di pagamento che si desidera visualizzare selezionando un intervallo di date:

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**. La visualizzazione dei dati di stato del pagamento dell&#39;ordine è visibile nella sezione _Ordini_.
1. Fare clic sul filtro del selettore **[!UICONTROL Range]**.
1. Scegliere l&#39;intervallo di date applicabile: 30 giorni, 15 giorni o 7 giorni.
1. Visualizza le informazioni sullo stato per le date specificate.

### Informazioni sugli stati

Gli stati dei pagamenti per un intervallo di date selezionato sono visualizzati a sinistra della visualizzazione dei dati di stato dei pagamenti dell&#39;ordine. Le date per l’intervallo di date selezionato sono visualizzate nella parte inferiore della visualizzazione. Se non vi sono ordini in una data specifica, tale data non viene visualizzata.

La visualizzazione dei dati relativi allo stato del pagamento dell&#39;ordine include le seguenti informazioni.

| Dati | Descrizione |
| ------------ | -------------------- |
| [!UICONTROL Orders] | Intervallo di importi per ordini nell&#39;intervallo di tempo specificato; dati sull&#39;asse Y (a sinistra) |
| Intervallo di date | Intervallo di date per l’intervallo di tempo specificato; dati sull’asse X (in basso) |
| Autorizzato | Ordine autorizzato |
| Acquisizione richiesta | Acquisizione richiesta per l’ordine |
| Acquisizione confermata | Acquisizione ordine completata |
| Acquisizione parziale | Ordine parzialmente acquisito |
| Acquisizione non riuscita | Acquisizione ordine non riuscita |
| Annullato | Ordine annullato |

## Visualizzazione report stato pagamento ordine

La vista del rapporto Stato pagamento ordine è disponibile nella vista Home di Payment Services. Include stati dettagliati (pagamento, fatturazione, spedizione, rimborso, controversia e altro) per tutte le transazioni.

Nella barra laterale _Amministratore_, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**&#x200B;per visualizzare la tabella dettagliata relativa al report sullo stato dei pagamenti degli ordini.

![Transazioni dello stato del pagamento dell&#39;ordine nell&#39;amministratore](assets/orders-report-data.png){width="800" zoomable="yes"}

È possibile configurare questa visualizzazione in base alle sezioni di questo argomento per presentare al meglio i dati che si desidera visualizzare.

È possibile [scaricare le transazioni di pagamento](#download-order-payment-statuses) in un formato di file .csv da utilizzare nel software di accounting o di gestione degli ordini esistente.

>[!NOTE]
>
>I dati visualizzati in questa tabella sono ordinati in ordine decrescente (`DESC`) per impostazione predefinita utilizzando `TRANS DATE`. `TRANS DATE` è la data e l&#39;ora in cui è stata avviata la transazione.

### Aggiornamenti dello stato del pagamento

Alcuni metodi di pagamento richiedono un periodo di tempo per l&#39;acquisizione del pagamento. [!DNL Payment Services] ora rileva gli stati in sospeso di una transazione di pagamento in un ordine da:

* Rilevamento sincrono di `pending capture` transazioni
* Monitoraggio asincrono di `pending capture` transazioni

>[!NOTE]
>
>Il rilevamento degli stati in sospeso delle transazioni di pagamento in un ordine impedisce la spedizione accidentale di ordini se il pagamento non è ancora stato ricevuto. Ciò può verificarsi per gli assegni elettronici e le transazioni PayPal.

#### Rilevamento sincrono delle transazioni di acquisizione in sospeso

Rileva automaticamente le transazioni di acquisizione con stato `Pending` e impedisce agli ordini di immettere uno stato `Processing` quando viene rilevata una transazione di questo tipo.

Durante l&#39;estrazione del cliente o quando un amministratore crea una fattura per un pagamento autorizzato in precedenza, [!DNL Payment Services] rileva automaticamente le transazioni di acquisizione con stato `Pending` e sposta gli ordini corrispondenti nello stato `Payment Review`.

#### Monitoraggio asincrono delle transazioni di acquisizione in sospeso

Rileva quando una transazione di acquisizione in sospeso entra nello stato `Completed` in modo che gli esercenti possano riprendere l&#39;elaborazione dell&#39;ordine interessato.

Per assicurarti che questo processo funzioni come previsto, gli esercenti devono configurare un nuovo processo cron. Una volta configurato il processo per l’esecuzione automatica, non sono previsti altri interventi da parte del commerciante.

Consulta [Configurare i processi cron](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html?lang=it). Una volta configurato, il nuovo processo viene eseguito ogni 30 minuti per recuperare gli aggiornamenti per gli ordini con stato `Payment Review`.

Gli esercenti possono controllare lo stato aggiornato del pagamento tramite la visualizzazione rapporto Stato pagamento ordine.

### Dati utilizzati nel rapporto

[!DNL Payment Services] utilizza i dati degli ordini e li combina con i dati di pagamento aggregati provenienti da altre origini (incluso PayPal) per fornire rapporti significativi e molto utili.

I dati dell’ordine vengono esportati e memorizzati nel servizio di pagamento. Quando [modifichi o aggiungi gli stati dell&#39;ordine](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/orders/order-status#custom-order-status) o [modifichi una visualizzazione dello store](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/site-store/store-views#edit-a-store-view), [store](https://experienceleague.adobe.com/it/docs/commerce-admin/start/setup/store-details#store-information) o il nome del sito Web, tali dati vengono combinati con i dati di pagamento e il report sullo stato del pagamento dell&#39;ordine viene compilato con le informazioni combinate.

Questo processo prevede due fasi:

1. L&#39;indice viene modificato in base ai dati `ON SAVE` (ogni volta che vengono modificate le informazioni sull&#39;ordine o sull&#39;archivio) o `BY SCHEDULE` (secondo una pianificazione cron preconfigurata), a seconda di come viene configurato in [Gestione indice](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/tools/index-management) nell&#39;amministratore.

   Per impostazione predefinita, l&#39;indicizzazione dei dati si verifica `ON SAVE`, il che significa che ogni volta che qualcosa cambia nell&#39;ordine, nello stato dell&#39;ordine, nella visualizzazione store, nello store o nel sito Web, il processo di reindicizzazione si verifica immediatamente.

1. I dati indicizzati vengono inviati al servizio di pagamento, che quindi compila il rapporto Stato pagamento ordine.

Gli unici dati esportati e confrontati a scopo di reporting sono i dati utilizzati dal rapporto Stato pagamento ordine.

>[!NOTE]
>
>I dati visualizzati in questa tabella sono ordinati in ordine decrescente (`DESC`) per impostazione predefinita utilizzando `ORDER DATE`. `ORDER DATE` è la data/ora di creazione dell&#39;ordine.

#### Configurare l’esportazione dei dati

Anche se per impostazione predefinita la reindicizzazione avviene in modalità `ON SAVE`, si consiglia di indicizzare in modalità `BY SCHEDULE`. L&#39;indice `BY SCHEDULE` viene eseguito con una pianificazione cron di un minuto ed eventuali dati modificati vengono visualizzati nel report sullo stato dell&#39;ordine entro due minuti da eventuali modifiche dei dati. Questa reindicizzazione programmata consente di ridurre qualsiasi tensione sul negozio, soprattutto se si dispone di un grande volume di ordini in entrata, perché avviene secondo un programma (non come ogni ordine viene effettuato).

È possibile modificare la modalità indice: `ON SAVE` o `BY SCHEDULE`—[in Admin](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/tools/index-management#change-the-index-mode).

Per informazioni su come configurare l&#39;esportazione dei dati, vedere [Configurazione della riga di comando](configure-cli.md#configure-data-export).

### Seleziona origine dati

Nella visualizzazione del report Stato pagamento ordine è possibile selezionare l&#39;origine dati **[!UICONTROL Live]** _ o **[!UICONTROL Sandbox]** per la quale si desidera visualizzare i risultati del report.

![Selezione origini dati](assets/datasource.png){width="300" zoomable="yes"}

Se _[!UICONTROL Live]_&#x200B;è l&#39;origine dati selezionata, è possibile visualizzare le informazioni del report per gli archivi che utilizzano [!DNL Payment Services] in modalità di produzione. Se&#x200B;_[!UICONTROL Sandbox]_ è l&#39;origine dati selezionata, è possibile visualizzare le informazioni del report per la modalità sandbox.

Le selezioni delle origini dati funzionano come segue:

* Se non si dispone di archivi che utilizzano [!DNL Payment Services] in modalità Live, la selezione dell&#39;origine dati predefinita è _[!UICONTROL Sandbox]_.
* Se sono presenti archivi (uno o più) che utilizzano [!DNL Payment Services] in modalità Live, la selezione dell&#39;origine dati predefinita è _[!UICONTROL Live]_.
* Le esportazioni dei rapporti rispettano sempre la selezione dell’origine dati.

Per selezionare l&#39;origine dati per il report [!UICONTROL Order Payment Status]:

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Orders]** > **[!UICONTROL View Report]**.
1. Fare clic sul filtro di selezione _[!UICONTROL Data source]_&#x200B;e selezionare **[!UICONTROL Live]**&#x200B;o **[!UICONTROL Sandbox]**.

   I risultati del report vengono rigenerati in base all&#39;origine dati selezionata.

### Personalizzare le date dell’ordine nell’arco temporale

Nella visualizzazione del rapporto Stato pagamento ordine è possibile personalizzare l&#39;intervallo temporale dei risultati dello stato che si desidera visualizzare selezionando date specifiche. Per impostazione predefinita, nella griglia sono visualizzati 30 giorni di stato di pagamento dell&#39;ordine.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Fare clic sul filtro del selettore del calendario _[!UICONTROL Order dates]_.
1. Scegli l’intervallo di date applicabile.
1. Visualizza gli stati di pagamento dell&#39;ordine per le date specificate nella griglia.

### Filtrare le informazioni del rapporto

Nella visualizzazione del rapporto Stato pagamento ordine è possibile filtrare i risultati degli stati che si desidera visualizzare selezionando i criteri di filtro.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Fare clic sul selettore **[!UICONTROL Filter]**.
1. Attiva le opzioni _Stato pagamento_ per visualizzare i risultati del rapporto solo per gli stati di pagamento dell&#39;ordine selezionati.
1. Visualizzare i risultati del report entro un intervallo di importi dell&#39;ordine immettendo _[!UICONTROL Min Order Amount]_&#x200B;o _[!UICONTROL Max Order Amount_].
1. Fare clic su **[!UICONTROL Hide filters]** per nascondere il filtro.

### Mostra e nascondi colonne

Il rapporto Stato pagamento ordine mostra tutte le colonne di informazioni disponibili per impostazione predefinita. È tuttavia possibile personalizzare le colonne visualizzate nel rapporto.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Fare clic sull&#39;icona _Impostazioni colonna_ (![icona impostazioni colonna](assets/column-settings.png){width="20" zoomable="yes"}).
1. Per personalizzare le colonne visualizzate nel report, selezionare o deselezionare le colonne nell&#39;elenco.

   Nel rapporto Stato pagamento ordine vengono immediatamente visualizzate le modifiche apportate nel menu Impostazioni colonna. Le preferenze di colonna vengono salvate e rimangono attive se ci si sposta dalla vista del rapporto.

### Stati di visualizzazione

La visualizzazione del rapporto Stato pagamento ordine mostra informazioni complete sullo stato del pagamento per ogni ordine.

Per impostazione predefinita, nella griglia sono visualizzati 30 giorni di stato di pagamento dell&#39;ordine.

Scorri verso sinistra e destra per visualizzare [informazioni sullo stato del pagamento dell&#39;ordine](#column-descriptions), inclusa la data dell&#39;ordine, la data autorizzata, la fatturazione, la spedizione, lo stato del pagamento e altro ancora.

Il numero di righe restituite in una ricerca o visualizzate negli stati di pagamento dell&#39;ordine predefiniti per 30 giorni viene visualizzato sopra la griglia di visualizzazione dello stato del pagamento dell&#39;ordine insieme al filtro del selettore calendario Date ordine.

#### Stato della retribuzione

La colonna Stato pagamento mostra lo stato corrente di qualsiasi pagamento. Un pagamento di `Capture failed` presenta uno stato di avviso rosso e un pagamento di `Voided` presenta uno stato di avviso grigio.

#### Stato rimborso

La colonna Stato rimborso mostra lo stato corrente di qualsiasi rimborso. Un pagamento di `Capture failed` presenta uno stato di avviso rosso e un pagamento di `Voided` presenta uno stato di avviso grigio.

### Aggiornare i dati del rapporto

La visualizzazione del report Stato pagamento ordine mostra un timestamp _[!UICONTROL Last updated]_&#x200B;che indica l&#39;ultima volta che le informazioni del report sono state aggiornate. Per impostazione predefinita, i dati del rapporto Stato pagamento ordine vengono aggiornati automaticamente ogni tre ore.

È inoltre possibile forzare manualmente l&#39;aggiornamento dei dati del rapporto Stato pagamento ordine per visualizzare le informazioni più aggiornate.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Fai clic sull&#39;icona _Aggiorna_ (![aggiorna icona](assets/refresh-button-med.png){width="20" zoomable="yes"}).

   I dati del report sullo stato del pagamento dell&#39;ordine vengono aggiornati, viene visualizzata una conferma *[!UICONTROL Update complete]* e nella griglia sono presenti le informazioni più recenti.

### Visualizza controversie

Puoi visualizzare eventuali controversie sugli ordini del tuo Negozio e passare al Centro di risoluzione PayPal per intervenire su di essi, dall&#39;interno del rapporto Stato pagamento ordine.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Passare a **[!UICONTROL Disputes column]**.
1. Visualizzare eventuali controversie per un ordine specifico e visualizzare [lo stato della controversia](#order-payment-status-information).
1. Rivedi i dettagli della controversia dal [Centro di risoluzione PayPal](https://www.paypal.com/us/cshelp/article/what-is-the-resolution-center-help246) facendo clic sul collegamento ID controversia che inizia con _PP-D-_.
1. Adottare le misure appropriate per la controversia, se necessario.

   Per ordinare le controversie per stato, fare clic sull&#39;intestazione di colonna [!UICONTROL Disputes].

### Scarica stati di pagamento ordine

È possibile scaricare un file .csv con tutti gli stati visibili nella griglia di visualizzazione dello stato del pagamento dell&#39;ordine, sia che si visualizzino gli stati predefiniti di 30 giorni o un intervallo temporale personalizzato.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Se desideri visualizzare gli stati per un intervallo di tempo diverso dagli ultimi 30 giorni, [personalizza l&#39;intervallo di date per i tuoi stati](#customize-dates-timeframe).
1. Fai clic sull&#39;icona _Scarica_ (![icona di download](assets/icon-download.png){width="20" zoomable="yes"}).

Gli stati di pagamento dell&#39;ordine vengono scaricati in formato .csv.

### Descrizioni delle colonne

I rapporti sullo stato dei pagamenti degli ordini includono le seguenti informazioni.

| Colonna | Descrizione |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | ID ordine Commerce<br> <br>Per visualizzare le [informazioni sull&#39;ordine](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"} correlate, fare clic sull&#39;ID. |
| [!UICONTROL Order Date] | Timestamp data ordine |
| [!UICONTROL Authorized Date] | Data e ora dell’autorizzazione di pagamento |
| [!UICONTROL Order Status] | [stato ordine](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/orders/order-status){target="_blank"} di Commerce corrente |
| [!UICONTROL Invoiced] | Stato fattura ordine: *[!UICONTROL No]*, *[!UICONTROL Partial]* o *[!UICONTROL Yes]* |
| [!UICONTROL Shipped] | Stato spedizione ordine: *[!UICONTROL No]*, *[!UICONTROL Partial]* o *[!UICONTROL Yes]* |
| [!UICONTROL Order Amt] | Importo totale totale dell’ordine |
| [!UICONTROL Cur] | Tipo di valuta dell’ordine |
| [!UICONTROL Pay Status] | Stato del pagamento per un ordine specifico |
| [!UICONTROL Paid Amt] | Importo pagato su un ordine |
| [!UICONTROL Cur] | Tipo di valuta dell’importo pagato su un ordine |
| [!UICONTROL Refund Status] | Stato di un rimborso su un ordine (ad esempio informazioni da restituzioni, RMA e note di accredito)—   *[!UICONTROL Requires refund]*, *[!UICONTROL Refund requested]*, *[!UICONTROL Refunded]*, *[!UICONTROL Refund failed]* o *[!UICONTROL Voided]* |
| [!UICONTROL Refund Amount] | Totale dell&#39;importo rimborsato per un ordine |
| [!UICONTROL Cur] | Tipo di valuta dell&#39;importo rimborsato per un ordine |
| [!UICONTROL Disputes] | Stato di qualsiasi controversia relativa a un ordine (informazioni da controversie e rimborsi): *[!UICONTROL Open]*, *[!UICONTROL Waiting for buyer response]*, *[!UICONTROL Waiting for seller response]*, *[!UICONTROL Under review]*, *[!UICONTROL Resolved]* o *[!UICONTROL Other]* |
| [!UICONTROL Payment Method] | Metodo di pagamento utilizzato nella transazione Commerce per un ordine |
| [!UICONTROL Website] | Sito web da cui è stato effettuato l’ordine |
| [!UICONTROL Store] | Archivio da cui è stato effettuato l’ordine |
| [!UICONTROL Store View] | Visualizzazione del Negozio da cui è stato effettuato l&#39;ordine |
