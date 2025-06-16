---
title: Configurazione servizi di pagamento legacy
description: Dopo l'installazione, puoi configurare  [!DNL Payment Services]  nell'amministratore nella configurazione dell'archivio.
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: fd76c6c017b4fc6bd04881f39415104f333bda85
workflow-type: tm+mt
source-wordcount: '1757'
ht-degree: 0%

---

# Configurazione [!DNL Payment Services] legacy

Puoi personalizzare [!DNL Payment Services] in base alle tue esigenze con utili opzioni di configurazione nell&#39;Admin.

Quando si configura [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] nell&#39;amministratore, tali configurazioni si applicano solo all&#39;ambiente impostato nel campo _[!UICONTROL Method]_di_[!UICONTROL General Configuration]_. Qualsiasi modifica apportata nei campi di configurazione è indipendente dal passaggio alla selezione di _[!UICONTROL Method]_. Se si cambia metodo, le selezioni non vengono reimpostate.

## Configurazione generale

Puoi abilitare [!DNL Payment Services] per il tuo archivio e _[!UICONTROL Merchant Location]_e abilitare i test sandbox o i pagamenti live nella sezione_[!UICONTROL General Configuration]_.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Imposta il campo _[!UICONTROL Merchant Country]_in_[!UICONTROL Merchant Location]_. Se non si specifica un _[!UICONTROL Merchant Country]_, verrà utilizzato il_[!UICONTROL Default Country]_ della configurazione generale.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_per accedere alla sezione_[!UICONTROL [!DNL Payment Services]]_.
1. Nella sezione _[!UICONTROL [!DNL Payment Services]]_, espandere la sezione_[!UICONTROL General Configuration]_.
1. Per **Enable**, impostarlo su `Yes` per abilitare [!DNL Payment Services] per l&#39;archivio.
1. Per il **metodo**, impostalo su `Sandbox` se stai ancora testando [!DNL Payment Services] per il tuo archivio o `Production` se sei pronto ad abilitare i pagamenti live.
1. I valori **[!UICONTROL Payment Services Sandbox ID]** e **[!UICONTROL Payment Services Production ID]** vengono compilati automaticamente dopo aver configurato [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} e aver visitato il dashboard [!DNL Payment Services] per la prima volta. Esegui questa operazione per completare l’onboarding per gli ambienti sandbox e/o di produzione. Questi valori associano il tuo ID SaaS a [!DNL Payment Services].

   >[!WARNING]
   >
   > Se devi modificare l&#39;ID dello spazio dei dati nel connettore dei servizi di Commerce, devi reimpostare l&#39;ID [!DNL Payment Services]. Fai clic su **Reimposta ID servizi di pagamento** per reimpostare l&#39;ID sandbox. Se ripristini l&#39;ID sandbox [!DNL Payment Services], devi eseguire di nuovo l&#39;onboarding.

1. I valori **[!UICONTROL PayPal Merchant ID]** e **[!UICONTROL PayPal Merchant Status]** vengono forniti automaticamente da PayPal dopo la prima visita al dashboard [!DNL Payment Services].
1. Per **Soft Descriptor** (valori personalizzati che vengono visualizzati nei rendiconti bancari delle transazioni dei clienti per distinguere tra negozi, marchi o cataloghi), aggiungi il testo personalizzato (fino a 22 caratteri) nel campo di testo, sostituendo `Soft descriptor` o il valore esistente.
1. Fai clic su **[!UICONTROL Save Config]** per salvare le modifiche.
1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

![Visualizzazione della soluzione Adobe in primo piano](assets/config-view-all.png){width="700" zoomable="yes"}

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Enable] | sito web | Attiva o disattiva [!DNL Payment Services] per il tuo sito Web. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | visualizzazione store | Imposta il metodo o l’ambiente per lo store. Opzioni: [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | visualizzazione store | L’ID venditore della sandbox, generato automaticamente durante l’onboarding della sandbox. |
| [!UICONTROL Payment Services Production ID] | visualizzazione store | L’ID esercente di produzione, generato automaticamente durante l’onboarding della produzione (dal vivo). |
| [!UICONTROL PayPal Merchant ID] | visualizzazione store | L&#39;ID univoco dell&#39;account esercente PayPal, generato al momento della creazione del conto PayPal. |
| [!UICONTROL PayPal Merchant Status] | visualizzazione store | Stato del tuo ID esercente PayPal. |
| [!UICONTROL Soft Descriptor] | visualizzazione sito Web o store | Aggiungi un soft descriptor ai tuoi siti web e alle viste store per aggiungere informazioni alle transazioni dei clienti che delineano marchi, store o linee di prodotti. |

## [!UICONTROL Credit Card Fields]

Le opzioni di pagamento [!UICONTROL Credit Card Fields] forniscono un pagamento semplice e sicuro per i metodi di pagamento con carta di credito o di debito.

Per ulteriori informazioni, vedere [Opzioni di pagamento](payments-options.md#paypal-smart-buttons).

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL Credit Card Fields]_.
1. Per **[!UICONTROL Title]**, immettere il testo (se necessario) per modificare il nome del metodo di pagamento come mostrato durante l&#39;estrazione.
1. Per [impostare l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), selezionare **[!UICONTROL Authorize]** o **Autorizza e acquisisci**.
1. Per assegnare la priorità a un metodo di pagamento nella pagina di pagamento, specificare un valore `Numeric Only` nel campo **[!UICONTROL Sort order]**.
1. Per **[!UICONTROL Show on checkout page]**, scegliere `Yes` per abilitare i campi della carta di credito nella pagina di pagamento.
1. Per **[!UICONTROL Vault Enabled]**, scegliere `Yes` per abilitare il vaulting della carta di credito per l&#39;estrazione.
1. Per **[!UICONTROL Vault Enabled in Admin]**, scegli `Yes` per consentire al commerciante di creare ordini per i clienti che utilizzano la carta di credito a pagamento.
1. Per abilitare **[!UICONTROL 3D Secure authentication]** (`Off` per impostazione predefinita), scegliere `Always` o `When required`.
1. Per **[!UICONTROL Debug Mode]**, scegliere `Yes` per abilitare la modalità di debug oppure `No` per disabilitarla.
1. Fai clic su **[!UICONTROL Save Config]** per salvare le modifiche.
1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella vista Metodo di pagamento durante l&#39;estrazione. Opzioni: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sito web | [azione di pagamento](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | visualizzazione store | L&#39;ordinamento per il metodo di pagamento specificato nella pagina di pagamento. Valore `Numeric Only` |
| [!UICONTROL Show on checkout page] | sito web | Attiva o disattiva i campi della carta di credito nella pagina di pagamento. Opzioni: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | visualizzazione store | Attiva o disattiva [il vaulting della carta di credito](vaulting.md). Opzioni: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | visualizzazione store | Abilita o disabilita la possibilità per l&#39;esercente [di completare gli ordini per i clienti nell&#39;Admin](vaulting.md) utilizzando un metodo di pagamento a scaffale. Opzioni: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | sito web | Attiva o disattiva [3DS Secure Authentication](security.md#3ds). Opzioni: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Apple Pay]

L&#39;opzione di pagamento [!UICONTROL Apple Pay] consente al commerciante di offrire Apple Pay ai propri acquirenti, che possono utilizzare il Touch ID sui loro dispositivi per effettuare acquisti dal browser Safari. Gli esercenti possono aggiungere fino a 99 domini per account esercente.

Per ulteriori informazioni, vedere [Opzioni di pagamento](payments-options.md#apple-pay-button).

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL Apple Pay]_.
1. Per **[!UICONTROL Title]**, immettere il testo (se necessario) per modificare il nome del metodo di pagamento come mostrato durante l&#39;estrazione.
1. Per [impostare l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), selezionare **[!UICONTROL Authorize]** o **[!UICONTROL Authorize and Capture]**.
1. Specificare la posizione in cui l&#39;opzione [!DNL Apple Pay] è abilitata in Adobe Commerce selezionando `Yes` nelle opzioni seguenti, in base alle esigenze:
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. Per abilitare la modalità di debug, selezionare `Yes` per **[!UICONTROL Debug Mode]** (`No` la disabilita).
1. Per salvare le modifiche, fare clic su **[!UICONTROL Save Config]**.
1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella vista Metodo di pagamento durante l&#39;estrazione. Opzioni: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sito web | [azione di pagamento](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | sito web | Attiva o disattiva [!DNL Apple Pay] nella pagina di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | visualizzazione store | Ordinamento per il metodo di pagamento specificato nella pagina di pagamento. Valore `Numeric Only` |
| [!UICONTROL Show buttons on product detail page] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] nella pagina dei dettagli del prodotto. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] nell&#39;anteprima del mini-carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] in nella pagina del carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

L&#39;opzione di pagamento [!UICONTROL Google Pay] consente al commerciante di offrire Google Pay ai propri acquirenti, che possono utilizzare il Google Wallet sui propri dispositivi per effettuare acquisti.

Per ulteriori informazioni, vedere [Opzioni di pagamento](payments-options.md#google-pay-button).

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL Google Pay]_.
1. (Facoltativo) Modificare il nome del metodo di pagamento visualizzato durante l&#39;estrazione immettendo il nuovo nome nel campo **[!UICONTROL Title]**.
1. [Impostare l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method) selezionando **[!UICONTROL Authorize]** o **[!UICONTROL Authorize and Capture]**.
1. Specificare la posizione in cui l&#39;opzione [!DNL Google Pay] è abilitata in Adobe Commerce selezionando `Yes` nelle opzioni seguenti, in base alle esigenze:
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. Per abilitare **[!UICONTROL 3D Secure authentication]** (`Off` per impostazione predefinita), scegliere `Always` o `When required`.
1. Per abilitare la modalità di debug, selezionare `Yes` per **[!UICONTROL Debug Mode]** (`No` la disabilita).
1. Configurare l&#39;aspetto del pulsante _[!UICONTROL Google Pay]_selezionando **[!UICONTROL Button Color]**,**[!UICONTROL Button Type]**e **[!UICONTROL Button Style]**in base alle esigenze.
1. Per impostare l&#39;altezza, utilizza il valore predefinito per l&#39;altezza definito in **[!UICONTROL Button Style]**.
1. Per salvare le modifiche, fare clic su **[!UICONTROL Save Config]**.
1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Title] | visualizzazione store | Specifica l&#39;etichetta di testo visualizzata per questa opzione di pagamento nella visualizzazione Metodo di pagamento durante l&#39;estrazione. Opzioni: `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | sito web | [azione di pagamento](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) per il metodo di pagamento specificato. Opzioni: `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show on checkout page] | sito web | Attiva o disattiva [!DNL Google Pay] nella pagina di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | visualizzazione store | Ordinamento per il metodo di pagamento specificato nella pagina di pagamento. Valore `Numeric Only` |
| [!UICONTROL Show buttons on product detail page] | visualizzazione store | Attiva o disattiva [!DNL Google Pay] nella pagina dei dettagli del prodotto. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | visualizzazione store | Attiva o disattiva [!DNL Google Pay] nell&#39;anteprima del mini-carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | visualizzazione store | Attiva o disattiva [!DNL Google Pay] nella pagina del carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | visualizzazione store | Attiva o disattiva [Autenticazione protetta 3D](security.md#3ds). Opzioni: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | Visualizzazione store | Definire il colore del pulsante [!DNL Google Pay]. Opzioni: `[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | Visualizzazione store | Definire il tipo del pulsante [!DNL Google Pay]. Opzioni: `[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

Per ulteriori informazioni, consulta la documentazione sulle [opzioni per l&#39;oggetto della richiesta API Google Pay](https://developers.google.com/pay/api/web/reference/request-objects).

## [!DNL PayPal Payment Buttons]

Le opzioni di pagamento di [!DNL PayPal payment buttons] offrono al cliente un processo di pagamento semplice, veloce e sicuro.

Per ulteriori informazioni, vedere [Opzioni di pagamento](payments-options.md#paypal-smart-buttons).

Configura [!DNL PayPal payment buttons]

Puoi abilitare e configurare le opzioni di pagamento dei pulsanti di pagamento PayPal in Admin:

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL PayPal payment buttons]_.
1. Per modificare il nome del metodo di pagamento come mostrato durante l&#39;estrazione, modificare il campo _[!UICONTROL Title]_.
1. Per [impostare l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), selezionare **[!UICONTROL Authorize]** o **[!UICONTROL Authorize and Capture]**.
1. Per assegnare la priorità a un metodo di pagamento nella pagina di pagamento, specificare un valore `Numeric Only` nel campo **[!UICONTROL Sort order]**.
1. Per abilitare o disabilitare la [messaggistica posticipata](payments-options.md#pay-later-button), selezionare `Yes`/`No` per **[!UICONTROL Display Pay Later Message]**.
1. Specifica dove i pulsanti di pagamento PayPal sono abilitati in Adobe Commerce selezionando `Yes` nelle seguenti opzioni in base alle esigenze:
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. Per abilitare Venmo come opzione di pagamento, selezionare `Yes` per **[!UICONTROL Venmo Enabled]**.
1. Per abilitare le carte di credito e di debito come opzione di pagamento (pulsante PayPal Smart), selezionare `Yes` per **[!UICONTROL Credit and Debit Card Enabled]**.
1. Per abilitare/disabilitare l&#39;opzione di pagamento [PayPal Pay Later](payments-options.md#pay-later-button), selezionare `Yes`/`No` per **[!UICONTROL PayPal Pay Later Enabled]**.
1. Per abilitare la modalità di debug, selezionare `Yes` per **[!UICONTROL Debug Mode]** (`No` la disabilita).
1. Per salvare le modifiche, fare clic su **[!UICONTROL Save Config]**.
1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella visualizzazione Metodo di pagamento durante l&#39;estrazione. Opzioni: campo di testo |
| [!UICONTROL Payment Action] | sito web | [azione di pagamento](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | sito web | Abilita o disabilita la funzione di messaggistica Paga più tardi nel carrello, nella pagina del prodotto, nel mini-carrello e durante il flusso di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on checkout page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on product detail page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina dei dettagli del prodotto. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nell&#39;anteprima del mini-carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] in nella pagina del carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | visualizzazione store | Abilita o disabilita l&#39;opzione di pagamento Venmo in cui sono visualizzati i pulsanti di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | visualizzazione store | Abilita o disabilita le opzioni per le carte di credito e di debito in cui vengono visualizzati i pulsanti di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | visualizzazione store | Abilita o disabilita l&#39;opzione di pagamento PayPal Pay Later quando vengono visualizzati i pulsanti di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Stile pulsante

È inoltre possibile configurare le opzioni _[!UICONTROL Button style]_dei pulsanti di pagamento:

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Nella sezione _[!UICONTROL [!DNL Payment Services]]_, espandere la sezione_[!UICONTROL PayPal Smart Button Styling]_.
1. Per impostare il layout, selezionare `Vertical` o `Horizontal` per **[!UICONTROL Layout]**
1. Per impostare il colore, selezionare uno dei colori disponibili in **[!UICONTROL Color]**.
1. Per impostare la forma, selezionare `Rectangular` o `Pill` per **[!UICONTROL Shape]**.
1. Per utilizzare l&#39;altezza predefinita, selezionare `Yes` o `No` per **[!UICONTROL Use Default Height]**.
1. Per impostare l&#39;altezza personalizzata, aggiungere l&#39;altezza in pixel desiderata per **[!UICONTROL Height]**.
1. Per impostare il tag, selezionare `Yes` o `No` per **[!UICONTROL Tagline]**.
1. Per salvare le modifiche, fare clic su **[!UICONTROL Save Config]**.
1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

Puoi anche configurare lo stile del pulsante di pagamento [in Impostazioni](settings.md#button-style) dalla Home di Payment Services.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|--- |--- |--- |
| [!UICONTROL Layout] | Visualizzazione store | Definire lo stile del layout per i pulsanti di pagamento Paypal. Opzioni: `[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | Visualizzazione store | Definisci il colore dei pulsanti di pagamento Paypal. Opzioni: [!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | Visualizzazione store | Definire la forma dei pulsanti di pagamento Paypal. Opzioni: `[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | Visualizzazione store | Definisce se i pulsanti di pagamento PayPal utilizzano un&#39;altezza predefinita. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | Visualizzazione store | Definisci l&#39;altezza dei pulsanti di pagamento PayPal. Valore predefinito: nessuno |
| [!UICONTROL Label] | Visualizzazione store | Definisci l&#39;etichetta visualizzata nei pulsanti di pagamento PayPal. Opzioni: `[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | Visualizzazione store | Attiva tagline. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Svuota la cache

Se modifichi la configurazione, [svuota manualmente la cache](/help/payment-services/settings.md#flush-the-cache) in modo che nell&#39;archivio vengano visualizzate le impostazioni di configurazione più recenti.
