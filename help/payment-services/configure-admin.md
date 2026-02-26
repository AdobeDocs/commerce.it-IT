---
title: Configurazione [!DNL Payment Services]
description: Dopo l'installazione, puoi configurare  [!DNL Payment Services]  nell'amministratore nella configurazione dell'archivio.
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: 6727102c54e0ac81df289ecd66ec61156662b8b9
workflow-type: tm+mt
source-wordcount: '3209'
ht-degree: 0%

---

# Configurazione [!DNL Payment Services]

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

## [!UICONTROL Fastlane]

[[!DNL Fastlane by PayPal]](https://www.paypal.com/us/cshelp/article/what-is-fastlane-by-paypal-help1096) è un metodo rapido e semplice per pagare online in modo sicuro. Durante un **pagamento per gli ospiti**, puoi memorizzare in modo sicuro la tua carta e i dettagli di spedizione per acquisti ancora più veloci in futuro.

Consulta [Opzioni di pagamento](payments-options.md#fastlane-button) per ulteriori informazioni.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL Fastlane]_.
1. Per abilitarlo, selezionare `Yes` per **[!UICONTROL Enable Fastlane]** (`No` lo disabilita).

   >[!NOTE]
   >
   > Se [!UICONTROL Fastlane] è abilitato, l&#39;opzione di pagamento [!UICONTROL Credit Card Fields] è disabilitata.

1. Per **[!UICONTROL Title]**, immettere il testo (se necessario) per modificare il nome del metodo di pagamento come mostrato durante l&#39;estrazione. Il titolo predefinito è `Credit Card (via Fastlane)`
1. Per [impostare l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), selezionare **[!UICONTROL Authorize]** o **Autorizza e acquisisci**.
1. Per abilitare **[!UICONTROL 3D Secure Authentication for Fastlane]** (`Off` per impostazione predefinita), scegli `When required` per rispettare le normative dell&#39;UE o `Always` per aggiungere un livello di protezione dalle frodi aggiuntivo.

   >[!NOTE]
   >
   > Se l&#39;emittente della scheda richiede l&#39;autenticazione 3D Secure, questo passaggio non può essere ignorato, indipendentemente dalla configurazione [!UICONTROL Payment Services].

1. Per assegnare la priorità a un metodo di pagamento nella pagina di pagamento, specificare un valore `Numeric Only` nel campo **[!UICONTROL Sort order]**.
1. Specificare se il marchio [!UICONTROL Fastlane] è abilitato durante l&#39;estrazione in Adobe Commerce impostando il campo **[!UICONTROL Enable messaging]** su `Yes`.
1. Fai clic su **[!UICONTROL Save Config]** per salvare le modifiche.
1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Enable Fastlane] | visualizzazione store | Attiva o disattiva [!DNL Fastlane] nella pagina di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | visualizzazione store | Aggiungere il testo da visualizzare come titolo per questa opzione di pagamento nella vista Metodo di pagamento durante l&#39;estrazione. Il valore predefinito è `Credit Card (via Fastlane)`. Opzioni: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | sito web | [azione di pagamento](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html) per il metodo di pagamento specificato. Opzioni: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL 3D Secure authentication] | visualizzazione store | Attiva o disattiva l&#39;autenticazione protetta [3D per Fastlane](security.md#3ds). Opzioni: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Sort order] | visualizzazione store | Ordinamento per il metodo di pagamento specificato nella pagina di pagamento. Valore `Numeric Only` |
| [!UICONTROL Enable messaging] | visualizzazione store | Specifica se il marchio [!UICONTROL Fastlane] è abilitato durante l&#39;estrazione in Adobe Commerce. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

### Facoltativo. Impostazioni di stile avanzate

Queste impostazioni facoltative consentono di personalizzare la visualizzazione di [!UICONTROL Fastlane] nel sito Web.

>[!TIP]
>
>Gli stili che non soddisfano le linee guida per l&#39;accessibilità vengono ripristinati alle impostazioni predefinite.

1. Nella sezione _[!UICONTROL Payment Services]_passare alla sezione_[!UICONTROL Fastlane]_.
1. Espandere la sezione _[!UICONTROL Advanced Style Settings (optional)]_.
1. Modificare le impostazioni in base alle esigenze.
1. Fai clic su **[!UICONTROL Save Config]** per salvare le modifiche.

Per ulteriori informazioni sulla personalizzazione, consulta i [documenti per sviluppatori PayPal](https://developer.paypal.com/limited-release/accelerated-checkout-bt/).

#### Impostazioni radice

Queste impostazioni facoltative modificano il componente di estrazione [!UICONTROL Fastlane] complessivo.

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Background Color] | visualizzazione store | Definisce il colore di sfondo del componente. Solo `RGB` valori |
| [!UICONTROL Border Color] | visualizzazione store | Definisce il colore del bordo del componente. Solo `RGB` valori |
| [!UICONTROL Font Family] | visualizzazione store | Imposta il font del componente. Vengono visualizzati solo i font disponibili nel tema |
| [!UICONTROL Font Size Base] | visualizzazione store | Definisce la dimensione del carattere. Solo `px` valori (pixel) |
| [!UICONTROL Padding] | visualizzazione store | Imposta la spaziatura interna nel componente. Solo `px` valori (pixel) |
| [!UICONTROL Primary Color] | visualizzazione store | Definisce il colore principale del componente. Solo `RGB` valori |
| [!UICONTROL Text Color] | visualizzazione store | Definisce il colore principale del testo nel componente. Solo `RGB` valori |

#### Impostazioni di input

Queste impostazioni facoltative si applicano ai campi di input del cliente del componente [!UICONTROL Fastlane].

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Background Color] | visualizzazione store | Definisce il colore di sfondo del componente. Solo `RGB` valori |
| [!UICONTROL Border Color] | visualizzazione store | Definisce il colore del bordo del componente. Solo `RGB` valori |
| [!UICONTROL Border Radius] | visualizzazione store | Definisce il raggio del bordo. Solo `px` valori (pixel) |
| [!UICONTROL Border Width] | visualizzazione store | Definisce la larghezza del bordo. Solo `px` valori (pixel) |
| [!UICONTROL Focus Border Color] | visualizzazione store | Definisce il colore del bordo dello stato attivo del componente. Solo `RGB` valori |
| [!UICONTROL Text Color Base] | visualizzazione store | Definisce il colore principale del testo nel componente. Solo `RGB` valori |

## [!UICONTROL Apple Pay]

Con [!DNL Apple Pay], i commercianti possono offrire un&#39;esperienza di pagamento sicura, veloce e senza soluzione di continuità in Safari, supportando fino a 99 domini per account commerciante. Il pulsante [!DNL Apple Pay] popola automaticamente le informazioni di pagamento, contatto e spedizione dal dispositivo iOS o macOS del cliente, consentendo acquisti rapidi e immediati che possono contribuire ad aumentare i tassi di conversione.

>[!IMPORTANT]
>
> Apple rifiuta i pagamenti da domini non verificati. I commercianti devono verificare tutti i domini in cui vengono utilizzati i pulsanti Apple Pay. Si applicano restrizioni nazionali. Per ulteriori informazioni sui requisiti di verifica del dominio, consulta la [documentazione di Apple Pay](https://developer.apple.com/documentation/apple_pay_on_the_web).

Per ulteriori informazioni, vedere [Opzioni di pagamento](payments-options.md#apple-pay-button).

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL Apple Pay]_.
1. Per **[!UICONTROL Title]**, immettere il testo (se necessario) per modificare il nome del metodo di pagamento come mostrato durante l&#39;estrazione.
1. Per [impostare l&#39;azione di pagamento](production.md#set-payment-services-as-payment-method), selezionare **[!UICONTROL Authorize]** o **[!UICONTROL Authorize and Capture]**.
1. Specificare la posizione in cui l&#39;opzione [!DNL Apple Pay] è abilitata in Adobe Commerce selezionando `Yes` nelle opzioni seguenti, in base alle esigenze:
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay at start of checkout]**
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
| [!UICONTROL Show Apple Pay on checkout page] | sito web | Attiva o disattiva [!DNL Apple Pay] nella pagina di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay at start of checkout] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] all&#39;inizio del flusso di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | visualizzazione store | Ordinamento per il metodo di pagamento specificato nella pagina di pagamento. Valore `Numeric Only` |
| [!UICONTROL Show Apple Pay on product detail page] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] nella pagina dei dettagli del prodotto. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay in mini cart preview] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] nell&#39;anteprima del mini carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Apple Pay on cart page] | visualizzazione store | Attiva o disattiva [!DNL Apple Pay] in nella pagina del carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
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
   * **[!UICONTROL Show Google Pay at start of checkout]**
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
| [!UICONTROL Show Google Pay on checkout page] | sito web | Attiva o disattiva [!DNL Google Pay] nella pagina di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay at start of checkout] | visualizzazione store | Attiva o disattiva [!DNL Google Pay] all&#39;inizio del flusso di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | visualizzazione store | Ordinamento per il metodo di pagamento specificato nella pagina di pagamento. Valore `Numeric Only` |
| [!UICONTROL Show Google Pay on product detail page] | visualizzazione store | Attiva o disattiva [!DNL Google Pay] nella pagina dei dettagli del prodotto. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay in mini cart preview] | visualizzazione store | Attiva o disattiva [!DNL Google Pay] nell&#39;anteprima del mini carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show Google Pay on cart page] | visualizzazione store | Attiva o disattiva [!DNL Google Pay] nella pagina del carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
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

   * Se si abilita la messaggistica [Paga più tardi](payments-options.md#pay-later-button), verrà visualizzato un pulsante modale **[!UICONTROL Configure Messaging]** che consente di impostare gli stili per **[!UICONTROL PayPal Pay Later messaging]**.

1. Specifica dove i pulsanti di pagamento PayPal sono abilitati in Adobe Commerce selezionando `Yes` nelle seguenti opzioni in base alle esigenze:
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons at start of checkout]**
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
| [!UICONTROL Display Pay Later Message] | sito web | Abilita o disabilita i messaggi PayPal Pay Later (Paga più tardi) nel carrello, nella pagina del prodotto, nel mini-carrello e durante il flusso di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Configure Messaging] | visualizzazione store | Modifica gli stili di messaggio PayPal Pay Later (Paga dopo). Opzioni: `[!UICONTROL Product page]` / `[!UICONTROL Cart]` |
| [!UICONTROL Show buttons on checkout page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons at start of checkout] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] all&#39;inizio del flusso di estrazione. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | visualizzazione store | Ordinamento per il metodo di pagamento specificato nella pagina di pagamento. Valore `Numeric Only` |
| [!UICONTROL Show buttons on product detail page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nella pagina dei dettagli del prodotto. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini cart preview] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] nell&#39;anteprima del mini carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | visualizzazione store | Attiva o disattiva [!DNL PayPal payment buttons] in nella pagina del carrello. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL App Switch] | visualizzazione store | Questa opzione è valida solo per i venditori e gli acquirenti **US**. Quando abilitato, tutti i pagamenti PayPal Express tenteranno di passare attraverso l&#39;app mobile PayPal quando disponibile. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Contact Preference] | visualizzazione store | Questa opzione è valida solo per i venditori e gli acquirenti **US**. Se è impostato su **sì**, l&#39;e-mail e il numero di telefono degli acquirenti verranno visualizzati nel modale di pagamento PayPal. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | visualizzazione store | Abilita o disabilita l&#39;opzione di pagamento Venmo in cui sono visualizzati i pulsanti di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | visualizzazione store | Abilita o disabilita le opzioni per le carte di credito e di debito in cui vengono visualizzati i pulsanti di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | visualizzazione store | Abilita o disabilita l&#39;opzione di pagamento PayPal Pay Later quando vengono visualizzati i pulsanti di pagamento. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | sito web | Attiva o disattiva la modalità di debug. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Metodi di pagamento locali

I metodi di pagamento locali (LPM, Local Payment Methods) forniscono supporto per metodi di pagamento locali e specifici per regione, come i bonifici bancari e le soluzioni di pagamento localizzato, insieme alle opzioni esistenti basate su carta. I commercianti possono abilitare o disabilitare i moduli LPM disponibili direttamente nella configurazione di Commerce. Per ulteriori informazioni sui metodi disponibili, vedere [Opzioni di pagamento](payments-options.md#local-payment-methods).

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione_[!UICONTROL Local Payment Methods]_.
1. Per **[!UICONTROL Active]**, selezionare `Yes` per abilitare i moduli LPM o `No` per disabilitarli.
1. Per **[!UICONTROL Title]**, immettere il testo da visualizzare come nome del metodo di pagamento durante l&#39;estrazione. Questo titolo viene visualizzato anche nella griglia dell&#39;ordine cliente.
1. Per **[!UICONTROL Allowed Payment Methods]**, selezionare i metodi di pagamento che si desidera offrire. I metodi disponibili dipendono dall&#39;indirizzo di fatturazione dell&#39;acquirente e dalla valuta di base del sito Web.
1. Per **[!UICONTROL Sort Order]**, immettere un valore numerico per determinare la posizione di visualizzazione degli LPM nell&#39;elenco dei metodi di pagamento disponibili.
1. Per salvare le modifiche, fare clic su **[!UICONTROL Save Config]**.
1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Active] | sito web | Abilita o disabilita i metodi di pagamento locali. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | visualizzazione store | Il nome del metodo di pagamento visualizzato durante il pagamento e nella griglia dell&#39;ordine di vendita. Opzioni: [!UICONTROL text field] |
| [!UICONTROL Allowed Payment Methods] | sito web | Selezionare i moduli LPM da offrire. I metodi sono visibili solo ai clienti il cui indirizzo di fatturazione e la valuta del sito web corrispondono ai requisiti del metodo. Opzioni: `Bancontact` / `BLIK` / `eps` / `iDEAL` / `MyBank` / `Przelewy24` |
| [!UICONTROL Sort Order] | visualizzazione store | Posizione di visualizzazione del gruppo LPM nell&#39;elenco dei metodi di pagamento disponibili. Questa impostazione si applica a tutti i moduli LPM come gruppo; i singoli moduli LPM non possono essere ordinati in modo indipendente. Valore `Numeric Only` |

>[!NOTE]
>
>Ciascun metodo di pagamento locale (Local Payment Method, LPM) prevede requisiti specifici per paese e valuta. Un metodo di pagamento viene visualizzato solo quando il paese dell’indirizzo di fatturazione del cliente e la valuta di base del sito web soddisfano tali requisiti. Ad esempio, Bancontact viene visualizzato solo per i clienti con un indirizzo di fatturazione belga quando la valuta di base è EUR.

## Elementi riga

Le voci inviano informazioni dettagliate sull&#39;ordine a PayPal, inclusi i dettagli del prodotto, le quantità e i prezzi. Questa funzione è attivata per impostazione predefinita. Per ulteriori informazioni, vedere [Elementi riga](line-items.md).

### Opzioni di configurazione

| Campo | Ambito | Descrizione |
|---|---|---|
| [!UICONTROL Line Items Enabled] | sito web | Abilita o disabilita l&#39;invio di voci e dettagli importo a PayPal. Disattivare questa impostazione se si utilizzano estensioni di terze parti che aggiungono tariffe personalizzate non supportate da [!DNL Payment Services]. Opzioni: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

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

Se modifichi la configurazione in _Impostazioni_, ad esempio attivando i pulsanti Apple Pay, Venmo o PayPal PayLater, svuota manualmente la cache in modo che nel tuo store vengano visualizzate le configurazioni più recenti.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**.
1. Fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

Se un tipo di cache nella tabella Gestione cache ha lo stato `INVALIDATED`, l&#39;archivio potrebbe non mostrare la configurazione più recente per l&#39;elemento. Svuota la cache per aggiornare l’archivio in modo da visualizzare la configurazione più recente.

Per assicurarsi che l&#39;archivio mostri la configurazione corretta, [svuotare periodicamente la cache](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management).

## Configurare i ruoli

Per garantire che gli utenti Admin possano creare e gestire gli ordini in Commerce Admin, abilita risorse specifiche di [!DNL Payment Services] per i ruoli utente.

Consulta [Ruoli utente](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html) per scoprire come gestire i ruoli.

Quando si assegnano risorse al ruolo, è necessario selezionare:

* **Paga con[!DNL Payment Services]**. Questa risorsa garantisce che quando crei un ordine nell&#39;amministratore, [!DNL Payment Services] carte di credito siano disponibili come metodo di pagamento. Se selezioni la risorsa principale **Azioni**, verrà selezionata anche questa risorsa.

* **[!DNL Payment Services]**—Questa risorsa include le risorse **Dashboard** e **Proxy servizi SaaS**, che devono essere selezionate. Assicurano che [!DNL Payment Services] venga visualizzato nel menu _Vendite_.

  ![Risorse di servizi di pagamento](assets/roles-payments.png){width="400" zoomable="yes"}


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

In [!UICONTROL Payment Services], puoi utilizzare più account PayPal all&#39;interno di **un** account esercente a livello di sito Web. Ad esempio, se gestisci i tuoi store in più paesi (che utilizzano [valute](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency) diverse) o desideri utilizzare Adobe Commerce per alcune parti della tua attività ma non _tutti_, puoi impostare il tuo account esercente in modo che utilizzi più account PayPal.

Per ulteriori informazioni sulla gerarchia di siti Web, store e visualizzazioni dello store, vedere [Ambito sito, archivio e visualizzazione](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html).

Per ulteriori informazioni sulla configurazione degli ambiti per più account PayPal tramite CLI, vedere [Configurazione della riga di comando](configure-cli.md#configure-scope-via-cli).

Il tuo rappresentante commerciale può creare un nuovo [ambito](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) per il tuo account esercente e integrare il sito aggiuntivo con PayPal in modo che tutti i pulsanti PayPal configurati per essere visualizzati vengano visualizzati sul tuo sito. Contatta l&#39;ufficio vendite
per assistenza nell&#39;utilizzo di più account PayPal per i siti Web.
