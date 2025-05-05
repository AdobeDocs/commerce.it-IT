---
title: Opzioni di pagamento
description: Imposta le opzioni di pagamento per personalizzare i metodi disponibili per i clienti del tuo Negozio.
feature: Payments, Checkout, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1174'
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

* **Avanzate** - Tutte le [opzioni di pagamento](../payment-services/payments-options.md) disponibili sono disponibili per gli attuali [paesi completamente supportati](../payment-services/overview.md#availability). Durante l&#39;onboarding per abilitare i pagamenti live, seleziona l&#39;[opzione di onboarding avanzata](../payment-services/production.md#advanced-onboarding).
* **Standard** - È disponibile un sottoinsieme di opzioni di pagamento (Pagamento rapido) (carte di credito e debito PayPal) per altri paesi supportati disponibili. [I campi della carta di credito](#credit-card-fields) e [Apple Pay](#apple-pay-button) non sono disponibili per questa opzione di onboarding. Durante l&#39;onboarding per abilitare i pagamenti live, seleziona l&#39;[opzione di onboarding standard](../payment-services/production.md#standard-onboarding).

Per informazioni sul completamento dell&#39;onboarding avanzato e standard, consulta [Abilita [!DNL Payment Services] per la produzione](../payment-services/production.md#complete-merchant-onboarding).

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] fornisce un pagamento semplice e sicuro per i metodi di pagamento con carta di credito o con carta di debito. Quando un acquirente effettua il check-out utilizzando i campi della carta di credito, inserisce il proprio nome, l’indirizzo di fatturazione e le informazioni sulla carta di credito o di debito per effettuare l’ordine. Le informazioni sui clienti vengono utilizzate in modo sicuro durante la sessione di acquisto per guidarli all’interno del flusso di pagamento.

![Campi carta di credito nell&#39;estrazione](assets/credit-card-fields.png){width="500" zoomable="yes"}

Abilita [vaulting carta di credito](#vaulting) per i tuoi negozi per consentire agli acquirenti di archiviare (salvare) le informazioni sulla carta di credito per un pagamento rapido in un secondo momento.

È possibile configurare [!UICONTROL Credit Card Fields] nella configurazione dell&#39;archivio o nella home di [!DNL Payment Services]. Per ulteriori informazioni, vedere [Impostazioni](settings.md#credit-card-fields).

È inoltre possibile modificare il layout, la larghezza, l&#39;altezza e lo stile esterno dei campi della carta di credito. Per ulteriori informazioni, consulta la [documentazione di PayPal](https://developer.paypal.com/docs/checkout/advanced/customize/card-field-style/).

## Pulsante [!DNL Apple Pay]

I clienti possono utilizzare [[!DNL Apple Pay]](https://www.apple.com/apple-pay/), che utilizza le credenziali di pagamento con carta di credito e debito memorizzate in un dispositivo iOS o macOS, per effettuare acquisti.

[!DNL Apple Pay] è disponibile solo nel browser Safari. Gli esercenti possono aggiungere fino a 99 domini per account esercente.

![Pulsante Apple Pay nel minicart](assets/applepay-button.png){width="500" zoomable="yes"}

Il pulsante [!DNL Apple Pay] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento.

Per utilizzare [!DNL Apple Pay] per i tuoi archivi, completa [la registrazione autonoma con [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) (_Registra il dominio live_ solo nella sezione) e [configuralo per i tuoi archivi in [!DNL Payment Services]](settings.md#payment-buttons).

>[!NOTE]
>
> Consulta [pagamento avanzato](https://www.paypal.com/us/cshelp/article/what-is-paypal-advanced-checkout-and-how-do-i-get-started-help953){target=_blank} nella documentazione per gli sviluppatori di PayPal per verificare come consentire agli acquirenti di pagare con Apple Pay sul tuo sito.

È possibile configurare [!UICONTROL Apple Pay] nella configurazione del negozio o nella Home page di Payment Services. Per ulteriori informazioni, vedere [Impostazioni](settings.md#apple-pay).

## Pulsante [!DNL Google Pay]

I clienti possono utilizzare [[!DNL Google Pay]](https://pay.google.com/about/) aggiungendo i dettagli di pagamento al proprio account Google, dove vengono memorizzati in modo sicuro per un&#39;esperienza di pagamento senza soluzione di continuità.

[!DNL Google Pay] è disponibile solo in alcuni paesi o aree geografiche e su alcuni dispositivi. Per ulteriori informazioni, consulta la [[!DNL Google Pay] documentazione](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration).

![Pulsante Google Pay nell&#39;estrazione](assets/google-pay-button.png){width="500" zoomable="yes"}

Il pulsante [!DNL Google Pay] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento.

È possibile configurare [!UICONTROL Google Pay] nella configurazione del negozio o nella Home page di Payment Services. Per ulteriori informazioni, vedere [Impostazioni](configure-admin.md).

>[!NOTE]
>
> L&#39;API [!DNL Google Pay] può essere utilizzata solo su siti Web in un contesto sicuro. Consulta la [documentazione sulla risoluzione dei problemi](https://developers.google.com/pay/api/web/support/troubleshooting) per ulteriori informazioni.

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons], che utilizza PayPal per completare un acquisto, memorizza l&#39;indirizzo di spedizione, gli indirizzi di fatturazione e i dettagli del pagamento del cliente per un uso successivo. Gli acquirenti possono utilizzare qualsiasi metodo di pagamento precedentemente memorizzato o offerto da PayPal.

![Pulsante PayPal](assets/paypal-button.png){width="350" zoomable="yes"}

È possibile configurare [!UICONTROL PayPal payment buttons] nella configurazione dell&#39;archivio o nella home di [!DNL Payment Services]. Per ulteriori informazioni, vedere [Impostazioni](settings.md#payment-buttons).

Scopri la disponibilità dei metodi di pagamento per paese nella [documentazione sui metodi di pagamento](https://developer.paypal.com/docs/checkout/payment-methods/) di PayPal.

### Pulsante [!DNL PayPal]

I clienti possono effettuare il check-out con facilità e sicurezza utilizzando il pulsante PayPal.

Il pulsante [!DNL PayPal] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento.

### Pulsante [!DNL Venmo]

I clienti possono estrarre utilizzando il pulsante [Venmo](https://venmo.com/).

Il pulsante [!DNL Venmo] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento.

### Pulsante di addebito o carta di credito PayPal

I clienti possono effettuare il check-out utilizzando il pulsante PayPal Debit o carta di credito.

Il pulsante PayPal Debit o carta di credito è visibile dalla pagina di pagamento.

Questa opzione può essere utilizzata per presentare un&#39;opzione di pagamento con carta di debito o di credito agli acquirenti con un pulsante ospitato da PayPal come alternativa all&#39;integrazione con carta di credito.

### Pulsante [!DNL Pay Later]

Offri ai tuoi clienti pagamenti a breve termine senza interessi e altre opzioni di finanziamento in modo che possano acquistare subito e pagare in seguito con il pulsante [!DNL Pay Later].

Il pulsante [!DNL Pay Later] è visibile dalla pagina del prodotto, dal mini-carrello, dal carrello e dalle visualizzazioni per il pagamento.

Consulta le informazioni sulle offerte Paga più tardi nella documentazione sulle offerte Paga più tardi di [PayPal](https://developer.paypal.com/docs/checkout/pay-later/us/). Utilizza il menu a discesa **Paese** per selezionare un&#39;area di interesse.

Scopri come disabilitare o abilitare i messaggi [!DNL Pay Later] aggiornando la configurazione di [Impostazioni](settings.md#payment-buttons).

## Utilizza solo i pulsanti di pagamento PayPal

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
1. Disattiva _l&#39;opzione **[[!UICONTROL Show on checkout page]](settings.md#credit-card-fields)**&#x200B;nella sezione&#x200B;_[!UICONTROL Credit card fields]_ e utilizza l&#39;account [provider di carte di credito esistente](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html?lang=it#payments)._

## Ricalcolo ordine

Quando un cliente accede al flusso di pagamento dal mini-carrello, dal carrello o dalla pagina del prodotto, viene indirizzato a una pagina di revisione dell’ordine in cui può visualizzare l’indirizzo di spedizione selezionato in una finestra a comparsa PayPal. Dopo che il cliente ha selezionato il metodo di spedizione, l&#39;importo dell&#39;ordine viene ricalcolato in modo appropriato e il cliente può visualizzare le spese di spedizione e le imposte.

Quando un cliente accede al flusso di pagamento dalla pagina di pagamento, il sistema è già a conoscenza dell&#39;indirizzo di spedizione e dell&#39;importo calcolato finale e i totali sono rappresentati in modo appropriato.

Le esenzioni fiscali, le spese di spedizione e l&#39;IVA possono variare notevolmente da un&#39;ubicazione all&#39;altra. Dopo che [!DNL Payment Services] ha ricevuto l&#39;indirizzo e la tariffa di spedizione, ricalcola rapidamente tutti i costi applicabili e li visualizza in modo appropriato durante le ultime fasi del pagamento.

## Vaulting con carta di credito

Gli acquirenti possono vagliare, o &quot;salvare&quot;, le informazioni sulla loro carta di credito per acquisti futuri a livello del sito web (qualsiasi negozio all&#39;interno dello stesso account del commerciante).

Per ulteriori informazioni, vedere [Archivio carte di credito](vaulting.md).

## Sicurezza

Per ulteriori informazioni, vedere [Conformità PCI](security.md#pci-compliance).
