---
title: Opzioni di pagamento
description: Imposta le opzioni di pagamento per personalizzare i metodi disponibili per i clienti del tuo Negozio.
exl-id: 95e648e6-6cb8-4226-b5ea-e1857212f20a
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Opzioni di pagamento

Con [!DNL Adobe Commerce] e [!DNL Magento Open Source] [!DNL Payment Services], hai a disposizione più opzioni di pagamento.

È possibile configurare queste opzioni di pagamento in [Impostazioni home](payments-home.md) o [Configurazione store](configure-admin.md) (consigliato per le opzioni di pagamento legacy o per una configurazione multi-store).

Esistono comportamenti diversi per ogni metodo di pagamento a seconda della posizione in cui sei nel processo di pagamento:

* Pagina prodotto: la pagina di prodotto di un elemento
* Mini carrello: disponibile facendo clic sull&#39;icona del carrello quando un prodotto è stato aggiunto ai carrelli
* Carrello acquisti: disponibile facendo clic su _Visualizza e modifica carrello_ dal mini-carrello
* Vista Pagamento—Disponibile quando fai clic su _Procedi al pagamento_ dal mini-carrello o dal carrello

>[!IMPORTANT]
>
>Per poter elaborare i pagamenti, è necessario completare l&#39;onboarding di [!DNL Payment Services].

## Esperienza pagamenti standard e avanzati

[!DNL Payment Services] fornisce **Opzioni di pagamento avanzate** (completamente supportate) e **Opzioni di pagamento standard** (pagamento rapido) e flussi di onboarding, a seconda del paese in cui operi.

* **Avanzate** - Tutte le [opzioni di pagamento](../payment-services/payments-options.md) disponibili sono disponibili per gli attuali [paesi completamente supportati](../payment-services/introduction.md#availability). Durante l&#39;onboarding per abilitare i pagamenti live, seleziona l&#39;[opzione di onboarding avanzata](../payment-services/production.md#advanced-onboarding).

* **Standard** - È disponibile un sottoinsieme di opzioni di pagamento (Pagamento rapido) (carte di credito e debito PayPal) per altri paesi supportati disponibili. [I campi della carta di credito](#credit-card-fields) e [Apple Pay](#apple-pay-button) non sono disponibili per questa opzione di onboarding. Durante l&#39;onboarding per abilitare i pagamenti live, seleziona l&#39;[opzione di onboarding standard](../payment-services/production.md#standard-onboarding).

Per informazioni sul completamento dell&#39;onboarding avanzato e standard, consulta [Abilita [!DNL Payment Services] per la produzione](../payment-services/production.md#complete-merchant-onboarding).

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] fornisce un pagamento semplice e sicuro per i metodi di pagamento con carta di credito o con carta di debito. Quando un acquirente effettua il check-out utilizzando i campi della carta di credito, inserisce il proprio nome, l’indirizzo di fatturazione e le informazioni sulla carta di credito o di debito per effettuare l’ordine. Le informazioni sui clienti vengono utilizzate in modo sicuro durante la sessione di acquisto per guidarli all’interno del flusso di pagamento.

![Campi carta di credito nell&#39;estrazione](assets/credit-card-fields.png){width="500" zoomable="yes"}

## [!UICONTROL Digital Wallets]

### Pulsante [!DNL Apple Pay]

Con [!DNL Apple Pay], i commercianti possono fornire un&#39;esperienza di pagamento sicura e semplificata in Safari (per un massimo di 99 domini per account commerciante), che può aumentare le conversioni. Il pulsante [!DNL Apple Pay] consente di memorizzare i dettagli di pagamento, contatto e spedizione dai dispositivi iOS o macOS dei clienti, consentendo un&#39;esperienza di pagamento rapida e immediata.

![Pulsante Apple Pay nel minicart](assets/applepay-button.png){width="500" zoomable="yes"}

Quando è abilitato, il pulsante [!DNL Apple Pay] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento. È possibile configurare [!DNL Apple Pay] nella configurazione dell&#39;archivio o nella Home dell&#39;estensione.

Per ulteriori informazioni, vedere [Impostazioni](settings.md#apple-pay).

### Pulsante [!DNL Google Pay]

Integrando [!DNL Google Pay] nell&#39;esperienza di pagamento, gli esercenti possono raccogliere le informazioni salvate relative al pagamento, ai contatti e alla spedizione dall&#39;account Google dell&#39;acquirente, offrendo un&#39;operazione di pagamento semplice e conveniente tra i browser e le app supportate.

[!DNL Google Pay] è disponibile solo in alcuni paesi o aree geografiche e su alcuni dispositivi. Per ulteriori informazioni, consulta la [[!DNL Google Pay] documentazione](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration).

![Pulsante Google Pay nell&#39;estrazione](assets/google-pay-button.png){width="500" zoomable="yes"}

Quando è abilitato, il pulsante [!DNL Google Pay] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento. Per ulteriori informazioni, vedere [Impostazioni](configure-admin.md).

>[!NOTE]
>
> L&#39;API [!DNL Google Pay] può essere utilizzata solo su siti Web in un contesto sicuro. Consulta la [documentazione sulla risoluzione dei problemi](https://developers.google.com/pay/api/web/support/troubleshooting) per ulteriori informazioni.

### [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons], che utilizza PayPal per completare un acquisto, memorizza l&#39;indirizzo di spedizione, gli indirizzi di fatturazione e i dettagli del pagamento del cliente per un uso successivo. Gli acquirenti possono utilizzare qualsiasi metodo di pagamento precedentemente memorizzato o offerto da PayPal.

![Pulsante PayPal](assets/paypal-button.png){width="350" zoomable="yes"}

È possibile configurare [!UICONTROL PayPal payment buttons] nella configurazione dell&#39;archivio o nella home di [!DNL Payment Services]. Per ulteriori informazioni, vedere [Impostazioni](settings.md#payment-buttons).

Scopri la disponibilità dei metodi di pagamento per paese nella [documentazione sui metodi di pagamento](https://developer.paypal.com/docs/checkout/payment-methods/) di PayPal.

#### Pulsante [!DNL PayPal]

I clienti possono effettuare il check-out con facilità e sicurezza utilizzando il pulsante PayPal.

Il pulsante [!DNL PayPal] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento.

#### Pulsante [!DNL Venmo]

I clienti possono estrarre utilizzando il pulsante [Venmo](https://venmo.com/).

Il pulsante [!DNL Venmo] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento.

#### Pulsante di addebito o carta di credito PayPal

I clienti possono effettuare il check-out utilizzando il pulsante PayPal Debit o carta di credito.

Il pulsante PayPal Debit o carta di credito è visibile dalla pagina di pagamento.

Questa opzione può essere utilizzata per presentare un&#39;opzione di pagamento con carta di debito o di credito agli acquirenti con un pulsante ospitato da PayPal come alternativa all&#39;integrazione con carta di credito.

#### Pulsante [!DNL Pay Later]

Offri ai tuoi clienti pagamenti a breve termine senza interessi e altre opzioni di finanziamento in modo che possano acquistare subito e pagare in seguito con il pulsante [!DNL Pay Later].

Il pulsante [!DNL Pay Later] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento.

Consulta le informazioni sulle offerte Paga più tardi nella documentazione sulle offerte Paga più tardi di [PayPal](https://developer.paypal.com/docs/checkout/pay-later/us/). Utilizza il menu a discesa **Paese** per selezionare un&#39;area di interesse.

Scopri come disabilitare o abilitare i messaggi [!DNL Pay Later] aggiornando la configurazione di [Impostazioni](settings.md#payment-buttons).

### Utilizza solo i pulsanti di pagamento PayPal

Per attivare rapidamente la modalità di produzione del tuo Negozio, puoi configurare _solo_ pulsanti di pagamento PayPal (Venmo, PayPal e così via).- invece di utilizzare anche l&#39;opzione di pagamento con carta di credito PayPal.

Questo consente di:

* Fornisci diverse opzioni di pagamento per i tuoi clienti, tra cui i pulsanti di pagamento Venmo e PayPal, con la possibilità di disattivare i campi della carta ospitata PayPal e utilizzare un provider di carta di credito esistente.
* Utilizza il provider di carte di credito esistente per i pagamenti con carta di credito, utilizzando anche le altre opzioni di pagamento di PayPal.
* Utilizza i pulsanti di pagamento di PayPal nelle aree in cui PayPal non supporta le carte di credito come opzione di pagamento.

Per **acquisire pagamenti con _solo_ pulsanti di pagamento PayPal (_non_ l&#39;opzione di pagamento con carta di credito PayPal)**:

1. Assicurati che l&#39;archivio sia [in modalità di produzione](settings.md#enable-payment-services).
1. [Configura i pulsanti di pagamento PayPal desiderati](settings.md#payment-buttons) in Impostazioni.
1. Disattiva _l&#39;opzione **[[!UICONTROL Show PayPal Credit and Debit card button]](settings.md#payment-buttons)**&#x200B;nella sezione&#x200B;_[!UICONTROL Payment buttons]_._

Per **acquisire i pagamenti con il provider di carte di credito esistente _e_ i pulsanti di pagamento PayPal**:

1. Assicurati che l&#39;archivio sia [in modalità di produzione](settings.md#enable-payment-services).
1. [Configura i pulsanti di pagamento PayPal desiderati](settings.md#payment-buttons).
1. Disattiva _l&#39;opzione **[[!UICONTROL PayPal Show Credit and Debit card button]](settings.md#payment-buttons)**&#x200B;nella sezione&#x200B;_[!UICONTROL Payment buttons]_._
1. Disattiva _l&#39;opzione **[[!UICONTROL Show on checkout page]](settings.md#credit-card-fields)**&#x200B;nella sezione&#x200B;_[!UICONTROL Credit card fields]_ e utilizza l&#39;account [provider di carte di credito esistente](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html#payments)._

## Opzioni di pagamento

Con [!DNL Payment Services] puoi configurare l&#39;esperienza di pagamento per Adobe Commerce in base alle preferenze e ai comportamenti degli acquirenti. Caratteristiche quali il vaulting con carta di credito [1&rbrace; e lo svuotamento automatico dell&#39;ordine garantiscono ai clienti una transazione semplice e senza problemi.](vaulting.md)

Con Adobe Commerce e Magento Open Source [!DNL Payment Services], sono disponibili più esperienze di pagamento. Esistono comportamenti diversi per ogni metodo di pagamento a seconda della posizione in cui sei nel processo di pagamento:

* Pagina prodotto: la pagina di prodotto di un articolo

* Mini carrello: disponibile facendo clic sull&#39;icona del carrello quando un prodotto è stato aggiunto ai carrelli

* Carrello acquisti: disponibile facendo clic su Visualizza e modifica il carrello dal mini-carrello

* Vista di checkout: disponibile facendo clic su Procedi al checkout dal mini-carrello o dal carrello acquisti

### Ricalcolo ordine

Quando un cliente accede al flusso di pagamento dal mini-carrello, dal carrello o dalla pagina del prodotto, viene indirizzato a una pagina di revisione dell’ordine in cui può visualizzare l’indirizzo di spedizione selezionato in una finestra a comparsa PayPal. Dopo che il cliente ha selezionato il metodo di spedizione, l&#39;importo dell&#39;ordine viene ricalcolato in modo appropriato e il cliente può visualizzare le spese di spedizione e le imposte.

Quando un cliente accede al flusso di pagamento dalla pagina di pagamento, il sistema è già a conoscenza dell&#39;indirizzo di spedizione e dell&#39;importo calcolato finale e i totali sono rappresentati in modo appropriato.

Le esenzioni fiscali, le spese di spedizione e l&#39;IVA possono variare notevolmente da un&#39;ubicazione all&#39;altra. Dopo che [!DNL Payment Services] ha ricevuto l&#39;indirizzo e la tariffa di spedizione, ricalcola rapidamente tutti i costi applicabili e li visualizza in modo appropriato durante le ultime fasi del pagamento.

Scopri la disponibilità dei metodi di pagamento per paese nella documentazione relativa ai metodi di pagamento di [PayPal](https://developer.paypal.com/docs/checkout/payment-methods/){target=_blank}.
