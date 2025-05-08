---
title: Generazione rapporti
description: Utilizzare il rapporto Transazioni per ottenere visibilità sui tassi di autorizzazione delle transazioni e sulle relative tendenze.
role: User
level: Intermediate
exl-id: dd1d80f9-5983-4181-91aa-971522eb56fa
source-git-commit: 4482c1f93a424c73497b88c707d0ab93a694c957
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# Generazione rapporti

[!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] offre report completi che consentono di ottenere una chiara visualizzazione delle transazioni, degli ordini e dei pagamenti del tuo Negozio.

![Rapporto transazioni](assets/transactions-report.png){width="700" zoomable="yes"}

Il rapporto Transazioni fornisce visibilità sui tassi di autorizzazione delle transazioni e sulle tendenze negative delle transazioni, consentendo di monitorare in modo efficace lo stato del tuo archivio e di identificare in modo preventivo e risolvere eventuali problemi relativi alle transazioni.

Vedi singole transazioni per gli ordini inseriti in vetrina e relativi metodi di pagamento, risultato, codici di risposta pagamento e altro ancora.

Le informazioni fornite nel rapporto Transazioni sono destinate esclusivamente all&#39;uso da parte degli esercenti. Non condividere queste informazioni con clienti o altri potenziali truffatori. Le informazioni sulle transazioni possono essere utilizzate per evitare controlli di sicurezza o per eseguire ordini che determinano rettifiche.

È possibile scaricare il report Transazioni in un formato di file .csv da utilizzare nel software di contabilità o gestione ordini esistente.

>[!NOTE]
>
>Non puoi visualizzare i report finanziari se non hai [attivato la modalità Live](production.md#enable-live-payments) per [!DNL Payment Services].

## Visualizzazione report transazioni

La vista del rapporto Transazioni è disponibile nella vista Transazioni di Payment Services. Include tutte le informazioni disponibili sulle transazioni per i tuoi store.

Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**per visualizzare la visualizzazione dettagliata del report Transazioni in tabella.

![Visualizzazione report transazioni](assets/transactions-report-view.png){width="800" zoomable="yes"}

È possibile configurare questa visualizzazione in base alle sezioni di questo argomento per presentare al meglio i dati che si desidera visualizzare.

Vedi gli ID transazione PayPal e ordine Commerce collegati, gli importi delle transazioni, il metodo di pagamento per transazione e molto altro all&#39;interno di questo rapporto.

Non tutti i metodi di pagamento forniscono la stessa granularità delle informazioni. Ad esempio, le transazioni con carta di credito forniscono i codici di risposta, AVS e CCV e le ultime quattro cifre della carta nel rapporto Transazioni; i pulsanti di pagamento PayPal no.

È possibile [scaricare le transazioni](#download-transactions) in un formato di file .csv da utilizzare nel software di accounting o di gestione ordini esistente.

>[!WARNING]
>
> Il report delle transazioni non includerà alcuna acquisizione eseguita al di fuori di [!DNL Payment Services].

### Seleziona origine dati

Nella visualizzazione del report Transazioni è possibile selezionare l&#39;origine dati **[!UICONTROL Live]** o **[!UICONTROL Sandbox]** per la quale si desidera visualizzare i risultati del report.

![Selezione origini dati](assets/datasource.png){width="300" zoomable="yes"}

Se _[!UICONTROL Live]_è l&#39;origine dati selezionata, è possibile visualizzare le informazioni del report per gli archivi che utilizzano [!DNL Payment Services] in modalità di produzione. Se_[!UICONTROL Sandbox]_ è l&#39;origine dati selezionata, è possibile visualizzare le informazioni del report per la modalità sandbox.

Le selezioni delle origini dati funzionano come segue:

* Se non si dispone di archivi che utilizzano [!DNL Payment Services] in modalità di produzione, la selezione dell&#39;origine dati predefinita è _[!UICONTROL Sandbox]_.
* Se sono presenti uno o più archivi che utilizzano [!DNL Payment Services] in modalità di produzione, la selezione dell&#39;origine dati predefinita è _[!UICONTROL Live]_.
* Le esportazioni dei rapporti rispettano sempre la selezione dell’origine dati.

Per selezionare l&#39;origine dati per il report [!UICONTROL Transactions]:

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Fare clic su **[!UICONTROL Data source]** e selezionare **[!UICONTROL Live]** o **[!UICONTROL Sandbox]**.

   I risultati del report vengono rigenerati in base all&#39;origine dati selezionata.

### Personalizzare l’intervallo temporale delle date

Nella visualizzazione del rapporto Transazioni è possibile personalizzare l&#39;intervallo temporale delle transazioni da visualizzare selezionando date specifiche. Per impostazione predefinita, nella griglia sono visualizzati 30 giorni di transazioni.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Fare clic sul filtro del selettore del calendario **[!UICONTROL Transaction dates]**.
1. Scegli l’intervallo di date applicabile.
1. Visualizza le transazioni per le date specificate nella griglia.

### Filtrare le informazioni del rapporto

Dalla vista del rapporto Transazioni, è possibile filtrare i risultati degli stati che si desidera visualizzare selezionando i criteri di filtro.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Fare clic sul selettore **[!UICONTROL Filter]**.
1. Attiva le opzioni _[!UICONTROL Transaction Result]_per visualizzare i risultati del rapporto solo per le transazioni ordine selezionate.
1. Attiva le opzioni _[!UICONTROL Payment Method]_per visualizzare i risultati del report per il tipo di pagamento utilizzato per la transazione.
1. Attiva le opzioni _[!UICONTROL Payment Detail]_per visualizzare ulteriori informazioni sul tipo di pagamento utilizzato, se disponibili.
1. Immettere un valore di _Importo minimo ordine_ o di _Importo massimo ordine_ per visualizzare i risultati del rapporto all&#39;interno di tale intervallo di importi ordine.
1. Immettere _[!UICONTROL Order ID]_per cercare una transazione specifica.
1. Introdurre _[!UICONTROL Card Last Four]_per cercare una carta di credito o di debito specifica.
1. Immettere _[!UICONTROL Customer ID]_per visualizzare tutte le transazioni di un cliente specifico.
1. Immettere _[!UICONTROL Customer Email]_per filtrare le transazioni per l&#39;e-mail.
1. Fare clic su **[!UICONTROL Hide filters]** per nascondere il filtro.

### Mostra e nascondi colonne

Il rapporto Transazioni mostra tutte le colonne di informazioni disponibili per impostazione predefinita. È tuttavia possibile personalizzare le colonne visualizzate nel rapporto.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Fare clic sull&#39;icona **[!UICONTROL Column settings]** ![icona impostazioni colonna](assets/column-settings.png){width="20" zoomable="yes"}.
1. Per personalizzare le colonne visualizzate nel report, selezionare o deselezionare le colonne nell&#39;elenco.

   Nel rapporto Transazioni vengono immediatamente visualizzate le modifiche apportate nel menu Impostazioni colonna. Le preferenze di colonna vengono salvate e rimangono attive se ci si sposta dalla vista del rapporto.

### Aggiornare i dati del rapporto

La visualizzazione del report Transazioni mostra un timestamp _[!UICONTROL Last updated]_che indica l&#39;ultima volta che le informazioni del report sono state aggiornate. Per impostazione predefinita, i dati del rapporto Transazioni vengono aggiornati automaticamente ogni tre ore.

Puoi anche forzare manualmente un aggiornamento dei dati del rapporto per visualizzare le informazioni più aggiornate.

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Fai clic sull&#39;icona _Aggiorna_ (![aggiorna icona](assets/refresh-button-med.png){width="20" zoomable="yes"}).

   I dati del report Transazioni vengono aggiornati, viene visualizzata una conferma *[!UICONTROL Update complete]* e nella griglia sono presenti le informazioni più recenti.

### Scarica transazioni

È possibile scaricare un file .csv con tutte le transazioni visibili nella griglia di visualizzazione delle transazioni, sia che si visualizzino i 30 giorni predefiniti delle transazioni o un intervallo temporale personalizzato.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Transactions]**.
1. Se desideri visualizzare le transazioni per un intervallo di tempo diverso dagli ultimi 30 giorni, [personalizza l&#39;intervallo di date per i tuoi stati](#customize-dates-timeframe).
1. Fai clic sull&#39;icona _Scarica_ ![scarica](assets/icon-download.png){width="20" zoomable="yes"}.

Le transazioni vengono scaricate in formato .csv.

### Descrizioni delle colonne

I rapporti sulle transazioni includono le seguenti informazioni.

| Colonna | Descrizione |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | ID ordine Commerce (contiene solo i valori per le transazioni riuscite ed è vuoto per le transazioni rifiutate)<br> <br>Per visualizzare le [informazioni ordine](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"} correlate, fare clic sull&#39;ID. |
| [!UICONTROL PayPal Transaction ID] | ID transazione fornito dal provider dei pagamenti; contiene solo valori per le transazioni riuscite e un trattino per le transazioni rifiutate. Puoi fare clic su questo ID per accedere alla pagina dei dettagli della transazione PayPal. |
| [!UICONTROL Customer ID] | ID cliente Commerce di un ordine<br> <br>Per ulteriori informazioni, consulta l&#39;argomento [Informazioni cliente](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/account-create){target="_blank"}. |
| [!UICONTROL Transaction Date] | Timestamp data transazione |
| [!UICONTROL Payment Method] | Tipo di pagamento utilizzato per la transazione con informazioni sul marchio e sul tipo di carta. Consulta [tipi di carta](https://developer.paypal.com/docs/api/orders/v2/#definition-card_type) per ulteriori informazioni; disponibile per le versioni di Payment Services 1.6.0 e successive |
| [!UICONTROL Payment Detail] | Fornisce informazioni aggiuntive sul tipo di pagamento utilizzato per la transazione, se disponibili. |
| [!UICONTROL Card Last Four] | Ultime quattro cifre delle carte di credito o di debito utilizzate per la transazione |
| [!UICONTROL Result] | Risultato della transazione: *[!UICONTROL OK]* (transazione riuscita), *[!UICONTROL Rejected by Payment Provider]* (rifiutato da PayPal), *[!UICONTROL Rejected by Bank]* (rifiutato dalla banca che ha emesso la carta) |
| [!UICONTROL Response Code] | Codice di errore che fornisce il motivo del rifiuto del provider di pagamenti o della banca. Vedere l&#39;elenco dei possibili codici di risposta e descrizioni per lo stato [`Rejected by Bank`](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) e lo stato [`Rejected by Payment Provider`](https://developer.paypal.com/api/rest/reference/orders/v2/errors/). |
| [!UICONTROL AVS Code] | Indirizzo: codice del servizio di verifica; informazioni di risposta del processore per le richieste di pagamento. Per ulteriori informazioni, consulta [elenco dei codici e delle descrizioni possibili](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response). |
| [!UICONTROL CVV Code] | Codice valore di verifica della carta per le carte di credito e di debito; per ulteriori informazioni, vedere [elenco dei codici e delle descrizioni possibili](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response). |
| [!UICONTROL Amount] | Importo dell’ordine della transazione |
| [!UICONTROL Currency] | Valuta utilizzata per l&#39;ordine nella transazione |
| [!UICONTROL Type] | [Azione di pagamento](../payment-services/production.md#set-payment-services-as-payment-method) per la transazione—`Authorize` o `Authorize and Capture` |

### Codici di risposta di errore

La colonna _Codice risposta_ mostra un errore specifico o un codice di operazione riuscita relativo alla transazione. Alcuni codici di errore comuni che potresti visualizzare includono:

* `PAYMENT_DENIED` - La transazione è stata rifiutata da PayPal perché sospettata di frode.
* `INTERNAL_SERVER_ERROR` - La transazione è stata rifiutata da PayPal e si è verificato un errore del server PayPal. È possibile ritentare la transazione.
* `INSTRUMENT_DECLINED` - Il cliente è stato rifiutato da PayPal per il metodo di pagamento selezionato. La transazione può essere ritentata con un metodo di pagamento diverso.
* `9500` - La transazione è stata rifiutata dalla banca associata perché sospettata di frode.
* `5120` - La transazione è stata rifiutata dalla banca associata perché il cliente non disponeva di fondi sufficienti per il pagamento.
* `5650` - La transazione è stata rifiutata dalla banca associata perché la banca richiede l&#39;autenticazione forte del cliente ([3DS](security.md#3ds)).

I codici di risposta di errore dettagliati per le transazioni non riuscite sono disponibili per le transazioni successive al 1° giugno 2023. I dati del rapporto parziale verranno visualizzati per le transazioni avvenute prima del 1° giugno 2023.
