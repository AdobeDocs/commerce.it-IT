---
title: Impostazioni servizi di pagamento
description: Dopo l'installazione, puoi configurare  [!DNL Payment Services]  nella Home.
role: Admin, User
level: Intermediate
exl-id: 108f2b24-39c1-4c87-8deb-d82ee1c24d55
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 9e7eb509aa19f3382d36221ac0c7dcf2130e8d8d
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 0%

---

# Impostazioni

Puoi personalizzare [!DNL Payment Services] in base alle tue esigenze con impostazioni utili nella Home di [!DNL Payment Services].

Per configurare [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source], fare clic su **[!UICONTROL Settings]**. Queste opzioni di configurazione si applicano solo all&#39;ambiente impostato nel campo _[!UICONTROL Payment mode]_&#x200B;delle[_ Opzioni di configurazione generali _](#configure-general-settings).

Per la configurazione di più store o legacy, vedi [Configurazione in Admin](configure-admin.md).

## Configurare le impostazioni generali

Le impostazioni di [!UICONTROL General] consentono di abilitare o disabilitare Servizi di pagamento come metodo di pagamento e di aggiungere informazioni alle transazioni dei clienti per contrassegnare o aggiungere come prefisso alle informazioni personalizzate una visualizzazione del sito Web o del Negozio.

### Abilita servizi di pagamento

Puoi abilitare [!DNL Payment Services] per il tuo sito Web e abilitare i test sandbox o i pagamenti live.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

1. Fare clic su **[!UICONTROL Settings]**. Per ulteriori informazioni, vedere [Introduzione alla [!DNL Payment Services] Home](payments-home.md).

   ![Visualizzazione impostazioni React](assets/react-settings-view.png){width="500" zoomable="yes"}

   La sezione _[!UICONTROL General]_&#x200B;include le impostazioni utilizzate per abilitare [!DNL Payment Services] come metodo di pagamento.

1. Per abilitare [!DNL Payment Services] come metodo di pagamento per il tuo archivio, nella sezione _[!UICONTROL General]_, passa da **[!UICONTROL Enable Payment Services as payment method]**&#x200B;a `Yes`.

1. Se stai ancora testando [!DNL Payment Services] per il tuo archivio, imposta **Modalità di pagamento** su `Sandbox`. Se si è pronti ad abilitare i pagamenti live, impostarli su `Production`.

1. I valori **[!UICONTROL Payment Services Sandbox ID]** e **[!UICONTROL Payment Services Production ID]** vengono compilati automaticamente dopo aver configurato [Commerce Services Connector](https://experienceleague.adobe.com/it/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} e aver visitato il dashboard [!DNL Payment Services] per la prima volta. Esegui questa operazione per completare l’onboarding per gli ambienti sandbox e/o di produzione. Questi valori associano il tuo ID SaaS a [!DNL Payment Services].

   >[!WARNING]
   >
   > Se ripristini gli ID [!DNL Payment Services], devi effettuare di nuovo l&#39;onboarding.

1. Fare clic su **[!UICONTROL Save]**.

   Se si tenta di uscire da questa visualizzazione senza salvare le modifiche, viene visualizzata una finestra modale che richiede di ignorare le modifiche, di continuare a modificarle o di salvarle.

1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

Ora puoi cambiare le impostazioni predefinite per le funzioni [opzioni di pagamento](#configure-payment-options) e la visualizzazione della vetrina.

### Aggiungi descrittore soft

Puoi aggiungere [!UICONTROL Soft Descriptor] alla configurazione dei tuoi siti Web o delle singole visualizzazioni dello store. I descrittori soft vengono visualizzati nei rendiconti bancari delle transazioni dei clienti. Se ad esempio si dispone di più store/marchi/cataloghi, è possibile distinguere facilmente tra questi aggiungendo testo personalizzato al campo [!UICONTROL Soft Descriptor].

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Fare clic su **[!UICONTROL Settings]**. Per ulteriori informazioni, vedere [Introduzione alla [!DNL Payment Services] Home](payments-home.md).
1. Selezionare la visualizzazione del sito Web o dello store, nel menu a discesa **[!UICONTROL Scope]**, per la quale si desidera creare un soft descriptor. Per la configurazione iniziale, lasciare **[!UICONTROL Default]** per impostare il valore predefinito.
1. Aggiungere il testo personalizzato (fino a 22 caratteri) nel campo di testo, sostituendo `Soft descriptor`.
1. Fare clic su **[!UICONTROL Save]**.
1. Per creare un soft descriptor diverso da quello predefinito configurato per una visualizzazione per siti web o store:
   1. Selezionare la visualizzazione del sito Web o dello store, nel menu a discesa **[!UICONTROL Scope]**, per la quale si desidera creare un soft descriptor.
   1. Attiva _disattiva_ **[!UICONTROL Use website]** (o **[!UICONTROL Use default]**, a seconda dell&#39;ambito selezionato).
   1. Aggiungi il testo personalizzato nel campo di testo.
   1. Fare clic su **[!UICONTROL Save]**.
1. Per abilitare per una visualizzazione del sito Web o dell&#39;archivio il descrittore soft predefinito _o_, il descrittore soft utilizzato per il sito Web padre:
   1. Selezionare la visualizzazione del sito Web o dello store, nel menu a discesa **[!UICONTROL Scope]**, per la quale si desidera attivare un soft descriptor esistente.
   1. Attiva _su_ **[!UICONTROL Use website]** (o **[!UICONTROL Use default]**, a seconda dell&#39;ambito selezionato).
   1. Fare clic su **[!UICONTROL Save]**.

   Se si tenta di uscire da questa visualizzazione senza salvare le modifiche, viene visualizzata una finestra modale che richiede di ignorare le modifiche, di continuare a modificarle o di salvarle.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Enable] | sito web | Attiva o disattiva [!DNL Payment Services] per il tuo sito Web. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Payment mode] | visualizzazione store | Imposta il metodo o l’ambiente per lo store. Opzioni: [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | visualizzazione store | L’ID venditore della sandbox, generato automaticamente durante l’onboarding della sandbox. |
| [!UICONTROL Payment Services Production ID] | visualizzazione store | L’ID esercente di produzione, generato automaticamente durante l’onboarding della produzione (dal vivo). |
| [!UICONTROL Soft Descriptor] | visualizzazione sito Web o store | Aggiungi un soft descriptor ai tuoi siti web e alle viste store per aggiungere informazioni alle transazioni dei clienti che delineano marchi, store o linee di prodotti. L&#39;opzione [!UICONTROL Use website] applica qualsiasi soft descriptor aggiunto a livello di sito Web. L&#39;opzione [!UICONTROL Use default] applica qualsiasi descrittore soft aggiunto come predefinito. |

## Configurare le opzioni di pagamento

Dopo aver abilitato [!UICONTROL Payment Services] per il sito Web, è possibile modificare le impostazioni predefinite per le funzioni di pagamento e la visualizzazione della vetrina.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Fare clic su **[!UICONTROL Settings]**. Per ulteriori informazioni, vedere [Introduzione alla [!DNL Payment Services] Home](payments-home.md).
1. Configurare le opzioni di pagamento per [carte di credito](#credit-card-fields), [pulsanti di pagamento](#payment-buttons) e [stile pulsante](#button-style), in base alle sezioni seguenti.

### Campi carta di credito

Le impostazioni di _[!UICONTROL Credit Card Fields]_&#x200B;forniscono un&#39;opzione di pagamento semplice e sicura per i metodi di pagamento con carta di credito o di debito.

Per ulteriori informazioni, vedere [Opzioni di pagamento](payments-options.md#credit-card-fields).

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Selezionare la visualizzazione punto vendita nel menu a discesa **[!UICONTROL Scope]** per la quale si desidera attivare un metodo di pagamento.
1. Nella sezione **[!UICONTROL Credit card fields]** modificare il valore nel campo **[!UICONTROL Checkout title]** per modificare il nome del metodo di pagamento visualizzato durante l&#39;estrazione.
1. Per [impostare l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), impostare **[!UICONTROL Payment action]** su `Authorize` o `Authorize and Capture`.
1. Per assegnare la priorità a un metodo di pagamento nella pagina di pagamento, specificare un valore `Numeric Only` nel campo **[!UICONTROL Sort order]**.
1. Per abilitare l&#39;autenticazione protetta di [3DS](security.md#3ds) (`Off` per impostazione predefinita) impostare il selettore **[!UICONTROL 3DS Secure authentication]** su `Always` o `When required`.
1. Per abilitare o disabilitare i campi della carta di credito nella pagina di pagamento, attiva il selettore **[!UICONTROL Show on checkout page]**.
1. Per abilitare o disabilitare [il vaulting delle schede](#card-vaulting), attiva/disattiva il selettore **[!UICONTROL Vault enabled]**.
1. Per abilitare o disabilitare [metodi di pagamento in Vault nell&#39;amministratore](#card-vaulting) (per consentire agli esercenti di completare gli ordini dei clienti nell&#39;amministratore utilizzando il metodo di pagamento in Vault), attivare o disattivare il selettore **[!UICONTROL Show vaulted methods in Admin]**.
1. Per attivare o disattivare la modalità di debug, attivare/disattivare il selettore **[!UICONTROL Debug Mode]**.
1. Fare clic su **[!UICONTROL Save]**.

   Se si tenta di uscire da questa visualizzazione senza salvare le modifiche, viene visualizzata una finestra modale che richiede di ignorare le modifiche, di continuare a modificarle o di salvarle.

1. [Svuotare la cache](#flush-the-cache).

#### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella vista Metodo di pagamento durante l&#39;estrazione. Opzioni: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sito web | [azione di pagamento](https://experienceleague.adobe.com/it/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | visualizzazione store | L&#39;ordinamento per il metodo di pagamento specificato nella pagina di pagamento. Valore `Numeric Only` |
| [!UICONTROL 3DS Secure authentication] | sito web | Attiva o disattiva [3DS Secure Authentication](security.md#3ds). Opzioni: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Show on checkout page] | sito web | Attiva o disattiva i campi della carta di credito da visualizzare nella pagina di pagamento. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Vault enabled] | visualizzazione store | Attiva o disattiva [il vaulting della carta di credito](vaulting.md). Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show vaulted payment methods in Admin] | visualizzazione store | Abilita o disabilita la possibilità per l&#39;esercente di completare gli ordini per i clienti nell&#39;Amministratore [utilizzando un metodo di pagamento con Vault](vaulting.md). Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |

### Apple Pay

L&#39;opzione di pagamento del pulsante [!UICONTROL Apple Pay] consente di fornire un pulsante di pagamento [!UICONTROL Apple Pay] nell&#39;estrazione del Negozio dal browser Safari (per un massimo di 99 domini per account esercente).

Puoi utilizzare Apple Pay solo se completi l&#39;autoregistrazione di [Apple Pay tramite Paypal](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) e quindi [configura Apple Pay](settings.md/#payment-buttons) per i tuoi store.

Per ulteriori informazioni, vedere [Opzioni di pagamento](payments-options.md#apple-pay-button).

È possibile abilitare e configurare l&#39;opzione di pagamento del pulsante [!UICONTROL Apple Pay]:

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Selezionare la visualizzazione punto vendita nel menu a discesa **[!UICONTROL Scope]** per la quale si desidera attivare un metodo di pagamento.
1. Nella sezione **[!UICONTROL Apple Pay]** modificare il valore nel campo _[!UICONTROL Checkout title]_&#x200B;per modificare il nome del metodo di pagamento visualizzato durante l&#39;estrazione.
1. Per [impostare l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), impostare **[!UICONTROL Payment action]** su `Authorize` o `Authorize and Capture`.
1. Per attivare o disattivare Apple Pay nella pagina di pagamento, attiva il selettore **[!UICONTROL Show Apple Pay on checkout page]**.
1. Per abilitare o disabilitare Apple Pay nella pagina dei dettagli del prodotto, attiva il selettore **[!UICONTROL Show Apple Pay on product detail page]**.
1. Per attivare o disattivare Apple Pay nell&#39;anteprima del mini carrello, attiva il selettore **[!UICONTROL Show Apple Pay on the mini cart preview]**.
1. Per attivare o disattivare Apple Pay nella pagina del carrello, attiva il selettore **[!UICONTROL Show Apple Pay on cart page]**.
1. Per attivare o disattivare la modalità di debug, attivare/disattivare il selettore **[!UICONTROL Debug Mode]**.
1. Fare clic su **[!UICONTROL Save]**.

   Se si tenta di uscire da questa visualizzazione senza salvare le modifiche, viene visualizzata una finestra modale che richiede di ignorare le modifiche, di continuare a modificarle o di salvarle.

1. [Svuotare la cache](#flush-the-cache).

#### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Checkout title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella vista Metodo di pagamento durante l&#39;estrazione. Opzioni: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sito web | [azione di pagamento](https://experienceleague.adobe.com/it/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions) per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | sito web | Attiva o disattiva il pulsante Apple Pay da visualizzare nella pagina di pagamento. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on checkout page] | sito web | Attiva o disattiva il pulsante Apple Pay per visualizzarlo nella pagina dei dettagli del prodotto. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on mini cart preview] | sito web | Attiva o disattiva il pulsante Apple Pay per visualizzarlo nell’anteprima del mini carrello. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on cart page] | sito web | Abilita o disabilita il pulsante Apple Pay per visualizzarlo nella pagina del carrello. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |

### Pulsanti di pagamento

Le opzioni di pagamento di [!DNL PayPal payment buttons] offrono al cliente un processo di pagamento semplice, veloce e sicuro. Per ulteriori informazioni, vedere [Opzioni di pagamento](payments-options.md#paypal-smart-buttons).

Puoi abilitare e configurare le opzioni di pagamento dei pulsanti di pagamento PayPal:

1. Selezionare la visualizzazione punto vendita nel menu a discesa **[!UICONTROL Scope]** per la quale si desidera attivare un metodo di pagamento.
1. Per modificare il nome del metodo di pagamento come mostrato durante l&#39;estrazione, modificare il valore nel campo **[!UICONTROL Checkout Title]**.
1. Per [impostare l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), impostare **[!UICONTROL Payment action]** su `Authorize` o `Authorize and Capture`.
1. Per assegnare la priorità a un metodo di pagamento nella pagina di pagamento, specificare un valore `Numeric Only` nel campo **[!UICONTROL Sort order]**.
1. Utilizza i selettori di attivazione/disattivazione per abilitare o disabilitare le funzionalità di visualizzazione di [!DNL PayPal smart button]:

   - **[!UICONTROL Show PayPal buttons on product checkout page]**
   - **[!UICONTROL Show PayPal buttons on product detail page]**
   - **[!UICONTROL Show PayPal buttons in mini-cart preview]**
   - **[!UICONTROL Show PayPal buttons on cart page]**
   - **[!UICONTROL Show PayPal Pay Later button]**
   - **[!UICONTROL Show PayPal Pay Later message]**
   - **[!UICONTROL Show Venmo button]**
   - **[!UICONTROL Show Apple Pay button]**
   - **[!UICONTROL Show PayPal Credit and Debit Card button]**

     >[!NOTE]
     >
     > Per utilizzare Apple Pay è necessario disporre di un account Apple sandbox tester[&#128279;](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account) (completo di informazioni sulla fatturazione e sulla carta di credito false) per testarlo.  Quando sei pronto a utilizzare Apple Pay in modalità di produzione sandbox _o_, dopo aver completato [test e convalida](test-validate.md#test-in-sandbox-environment), completa [la registrazione autonoma con [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) (_Registra il dominio live_) e [configuralo per i tuoi store in [!DNL Payment Services]](settings.md#payment-buttons).

     Quando attivi/disattivi la visibilità dei pulsanti di pagamento o del messaggio PayPal Pay Later (Paga più tardi), nella parte inferiore della pagina Settings (Impostazioni) viene visualizzata un&#39;anteprima visiva della configurazione.

1. Per abilitare la modalità di debug, attivare/disattivare il selettore **[!UICONTROL Debug Mode]**.
1. Fare clic su **[!UICONTROL Save]**.

   Se si tenta di uscire da questa visualizzazione senza salvare le modifiche, viene visualizzata una finestra modale che richiede di ignorare le modifiche, di continuare a modificarle o di salvarle.

1. [Svuotare la cache](#flush-the-cache).

#### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella visualizzazione Metodo di pagamento durante l&#39;estrazione. Opzioni: campo di testo |
| [!UICONTROL Payment Action] | sito web | [azione di pagamento](https://experienceleague.adobe.com/it/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | visualizzazione store | L&#39;ordinamento per il metodo di pagamento specificato nella pagina di pagamento. Valore `Numeric Only` |
| [!UICONTROL Show PayPal buttons on checkout page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina di estrazione. Opzioni: [!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons on product detail page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina dei dettagli del prodotto. Opzioni: [!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons in mini-cart preview] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nell&#39;anteprima del mini-carrello. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal buttons on cart page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina del carrello. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later button] | visualizzazione store | Abilita o disabilita l&#39;aspetto dell&#39;opzione di pagamento successivo in cui vengono visualizzati i pulsanti di pagamento. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later Message] | sito web | Abilita o disabilita la funzione di messaggistica Paga più tardi nel carrello, nella pagina del prodotto, nel mini-carrello e durante il flusso di pagamento. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Venmo button] | visualizzazione store | Abilita o disabilita l&#39;opzione di pagamento Venmo in cui sono visualizzati i pulsanti di pagamento. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Apple Pay button] | visualizzazione store | Abilita o disabilita l&#39;opzione di pagamento Apple Pay in cui sono visualizzati i pulsanti di pagamento. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Credit and Debit card button] | visualizzazione store | Abilita o disabilita l&#39;opzione di pagamento con carta di credito e debito in cui sono visualizzati i pulsanti di pagamento. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |

### Stile pulsante

È inoltre possibile configurare le opzioni _[!UICONTROL Button style]_&#x200B;dei pulsanti di pagamento:

1. Per modificare **[!UICONTROL Layout]**, selezionare `Vertical` o `Horizontal`.

   >[!NOTE]
   >
   > Se lo stile del pulsante è configurato come `Horizontal` e il tuo negozio è configurato per visualizzare più pulsanti di pagamento, è possibile che nella pagina del prodotto vengano visualizzati solo due pulsanti, pagina di pagamento e mini-carrello, e un pulsante nel carrello.

1. Per attivare la tagline in un layout orizzontale, attiva il selettore **[!UICONTROL Show tagline]**.
1. Per modificare **[!UICONTROL Color]**, selezionare l&#39;opzione di colore desiderata.
1. Per modificare **[!UICONTROL Shape]**, selezionare `Pill` o `Rectangle`.
1. Per abilitare il selettore altezza pulsante, attivare/disattivare il selettore **[!UICONTROL Responsive button height]**.
1. Per modificare **[!UICONTROL Label]**, selezionare l&#39;opzione di etichetta desiderata.

   Quando si modificano le opzioni di configurazione per layout, colore, forma, altezza ed etichetta, nella parte inferiore della pagina Impostazioni viene visualizzata un&#39;anteprima visiva della configurazione. Nell&#39;immagine seguente, **[!UICONTROL Shape]** è impostato su _Rettangolo_ e **[!UICONTROL Label]** è impostato su _PayPal (consigliato)_.

   ![[!DNL PayPal payment buttons] opzioni](assets/payment-buttons.png){width="400" zoomable="yes"}

1. Fare clic su **[!UICONTROL Save]**.

   Se si tenta di uscire da questa visualizzazione senza salvare le modifiche, viene visualizzata una finestra modale che richiede di ignorare le modifiche, di continuare a modificarle o di salvarle.

1. [Svuotare la cache](#flush-the-cache).

Puoi configurare lo stile del pulsante di pagamento [ nella configurazione legacy in Admin](configure-admin.md#configure-paypal-smart-buttons) o qui in [!DNL Payment Services Home]. Consulta la [Guida allo stile Pulsanti di PayPal](https://developer.paypal.com/docs/checkout/standard/customize/buttons-style-guide/) per ulteriori informazioni sullo stile dei pulsanti di pagamento di PayPal.

#### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|--- |--- |--- |
| [!UICONTROL Layout] | Visualizzazione store | Consente di definire lo stile del layout dei pulsanti di pagamento. Opzioni: [!UICONTROL Vertical] / [!UICONTROL Horizontal] |
| [!UICONTROL Tagline] | Visualizzazione store | Attiva/disattiva tagline. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Color] | Visualizzazione store | Definire il colore dei pulsanti di pagamento. Opzioni: [!UICONTROL Blue] / [!UICONTROL Gold] / [!UICONTROL Silver] / [!UICONTROL White] / [!UICONTROL Black] |
| [!UICONTROL Shape] | Visualizzazione store | Definire la forma dei pulsanti di pagamento. Opzioni: [!UICONTROL Rectangular] / [!UICONTROL Pill] |
| [!UICONTROL Responsive Button Height] | Visualizzazione store | Definisce se i pulsanti di pagamento utilizzano un&#39;altezza predefinita. Opzioni: [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Height] | Visualizzazione store | Definire l&#39;altezza dei pulsanti di pagamento. Valore predefinito: nessuno |
| [!UICONTROL Label] | Visualizzazione store | Definire l&#39;etichetta visualizzata nei pulsanti di pagamento. Opzioni: [!UICONTROL PayPal] / [!UICONTROL Checkout] / [!UICONTROL Buynow] / [!UICONTROL Pay] / [!UICONTROL Installment] |

## Configurare i ruoli

Per garantire che gli utenti Admin possano creare e gestire gli ordini in Commerce Admin, abilita risorse specifiche di [!DNL Payment Services] per i ruoli utente.

Consulta [Ruoli utente](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html?lang=it) per scoprire come gestire i ruoli.

Quando si assegnano risorse al ruolo, è necessario selezionare:

- **Paga con[!DNL Payment Services]**. Questa risorsa garantisce che quando crei un ordine nell&#39;amministratore, [!DNL Payment Services] carte di credito siano disponibili come metodo di pagamento. Se selezioni la risorsa principale **Azioni**, verrà selezionata anche questa risorsa.
- **[!DNL Payment Services]**—Questa risorsa include le risorse **Dashboard** e **Proxy servizi SaaS**, che devono essere selezionate. Assicurano che [!DNL Payment Services] venga visualizzato nel menu _Vendite_.

  ![Risorse di servizi di pagamento](assets/roles-payments.png){width="400" zoomable="yes"}

## Svuota la cache

Se modifichi la configurazione in _Impostazioni_, ad esempio attivando i pulsanti Apple Pay, Venmo o PayPal PayLater, svuota manualmente la cache in modo che nel tuo store vengano visualizzate le configurazioni più recenti.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**.
1. Fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

Se un tipo di cache nella tabella Gestione cache ha lo stato `INVALIDATED`, l&#39;archivio potrebbe non mostrare la configurazione più recente per l&#39;elemento. Svuota la cache per aggiornare l’archivio in modo da visualizzare la configurazione più recente.

Per assicurarsi che l&#39;archivio mostri la configurazione corretta, [svuotare periodicamente la cache](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/tools/cache-management).

## Vaulting delle carte

È possibile abilitare funzionalità che consentono ai clienti di archiviare, o &quot;salvare&quot;, le informazioni sulla carta di credito nel proprio Account personale per utilizzarle per acquisti futuri.

Puoi anche utilizzare il vaulting delle carte nell’amministratore per completare gli ordini successivi per i clienti esistenti.

Attiva o disattiva il vaulting delle carte di credito nelle [impostazioni del campo carta di credito](#credit-card-fields).

Per ulteriori informazioni, vedere [Archivio carte di credito](vaulting.md).

## 3DS

3DS protegge clienti e commercianti da attività fraudolente nei loro negozi e consente la conformità con gli standard dell&#39;Unione europea (UE).

Attiva o disattiva 3DS nelle [impostazioni del campo Carta di credito](#credit-card-fields).

Per ulteriori informazioni, vedere [3DS in Security](security.md#3ds).

## Usa più account PayPal

In [!UICONTROL Payment Services], puoi utilizzare più account PayPal all&#39;interno di **un** account esercente a livello di sito Web. Ad esempio, se gestisci i tuoi store in più paesi (che utilizzano [valute](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/site-store/currency/currency) diverse) o desideri utilizzare Adobe Commerce per alcune parti della tua attività ma non _tutti_, puoi impostare il tuo account esercente in modo che utilizzi più account PayPal.

Per ulteriori informazioni sulla gerarchia di siti Web, store e visualizzazioni dello store, vedere [Ambito sito, archivio e visualizzazione](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=it).

Per ulteriori informazioni sulla configurazione degli ambiti per più account PayPal tramite CLI, vedere [Configurazione della riga di comando](configure-cli.md#configure-scope-via-cli).

Il tuo rappresentante commerciale può creare un nuovo [ambito](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=it#scope-settings) per il tuo account esercente e integrare il sito aggiuntivo con PayPal in modo che tutti i pulsanti PayPal configurati per essere visualizzati vengano visualizzati sul tuo sito. Contatta il tuo rappresentante commerciale per assistenza sull&#39;utilizzo di più account PayPal per i tuoi siti Web.
