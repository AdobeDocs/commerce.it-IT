---
title: Configurare la sandbox di prova
description: Utilizza un account sandbox PayPal per utilizzare  [!DNL Payment Services]  in modalità di test.
exl-id: 99c14b4e-e6cf-48f9-9546-5c0d5c71464d
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 6727102c54e0ac81df289ecd66ec61156662b8b9
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Configurare la sandbox di prova

Prima di iniziare l’onboarding in sandbox, devi registrarti per un account PayPal Developer gratuito e creare account sia per esercenti (da utilizzare per l’onboarding) che per acquirenti (da utilizzare per testare l’estrazione). Se necessario, puoi creare più account Developer.

Un account sandbox PayPal ti consente di utilizzare [!DNL Payment Services] in modalità di test. PayPal richiede l’utilizzo di un account di test, di un’e-mail e di una password per l’onboarding in sandbox generato da PayPal Developer Portal (Portale per sviluppatori). *Non creare un altro account durante il processo di onboarding della sandbox.*

## Onboarding nelle sandbox

Per completare l’onboarding della sandbox:

1. Passa alla [pagina dell&#39;account sviluppatore PayPal](https://developer.paypal.com/developer/accounts/).
1. Fai clic su **[!UICONTROL Log in to Dashboard]** e accedi con il tuo account di prova PayPal Developer Portal generato da Business sandbox oppure fai clic su **Registrati** per creare un account.
1. Crea un account sandbox PayPal:
   1. Vai a _[!UICONTROL Testing Tools]_>**[!UICONTROL Sandbox Accounts]**.
   1. Fare clic su **[!UICONTROL Create account]**.

      Se hai creato un account sandbox PayPal durante il processo di onboarding di PayPal sandbox, devi [reimpostare la sandbox di onboarding](#reset-your-sandbox-account) o non puoi verificare l&#39;e-mail.

   1. Selezionare **[!UICONTROL Business]** come tipo di account e fare clic su **[!UICONTROL Create]**.
   1. Nella sezione _[!UICONTROL Sandbox Accounts]_, fai clic sui tre punti nella colonna&#x200B;_[!UICONTROL Manage accounts]_ per l&#39;account sandbox creato.
   1. Fare clic su **[!UICONTROL View/edit account]**.

      ![PayPal - Visualizza/Modifica account sandbox](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. Copia e salva l&#39;ID e-mail e la password generata dal sistema per utilizzi futuri.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Fare clic su **[!UICONTROL Sandbox onboarding]**.

   Questa opzione è visibile se non hai ancora completato l&#39;onboarding della sandbox per [!DNL Payment Services].

   Un ID commerciante sandbox viene generato automaticamente e popolato in [impostazioni](configure-admin.md). Non modificare o alterare questo ID.

   Viene visualizzata una finestra PayPal per collegare un conto PayPal per iniziare ad accettare i pagamenti.

1. Immetti l&#39;e-mail e la password del conto sandbox PayPal generato al passaggio 3 (non le informazioni sul conto aziendale PayPal) e il paese o l&#39;area geografica.
1. Fare clic su **[!UICONTROL Next]**.

   ![PayPal - Connetti conto PayPal per pagamenti](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. Continua a seguire il flusso PayPal, utilizzando le credenziali del tuo account sandbox salvate in precedenza.
1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

   Il pulsante **[!UICONTROL Sandbox onboarding]** non è più visibile. Viene visualizzato il testo &quot;Pagamenti sandbox in sospeso&quot;.

Quando l’onboarding in Sandbox PayPal viene approvato, dovresti visualizzare una notifica che informa che il sistema di pagamento è attualmente in modalità sandbox e non elabora pagamenti live.

>[!IMPORTANT]
>
>Se revoci il consenso a [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] per l&#39;elaborazione dei pagamenti (nelle impostazioni del tuo conto PayPal), gli ordini nel tuo Negozio non possono essere elaborati da [!DNL Payment Services]. Nella pagina principale di Payment Services viene visualizzato un avviso relativo alla revoca del consenso. Per ignorare l&#39;avviso, fare clic su **[!UICONTROL Do not show again]**.

### Reimposta l’account sandbox

Se hai creato un account sandbox PayPal durante il processo di onboarding di PayPal sandbox, devi reimpostare la sandbox di onboarding perché o non puoi verificare l’e-mail.

Per ripristinare l’account sandbox:

1. Fare clic su **[!UICONTROL Reset sandbox]**. [Crea un account PayPal business sandbox](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account).
1. Fare clic su **[!UICONTROL Sandbox onboarding]** e completare il set di passaggi successivo.

## Abilita numero di telefono del contatto

Il numero di telefono di contatto ti consente di ottenere i numeri di telefono di contatto che PayPal raccoglie dai tuoi clienti. PayPal raccoglie sempre i numeri di telefono di contatto dei titolari dei conti PayPal per aiutarli a confermare le loro identità e a contattarli per risolvere i problemi sui loro conti o per completare i loro processi di evasione. Tuttavia, PayPal scoraggia l&#39;uso dei numeri di telefono di contatto direttamente dal commerciante perché può avere un impatto negativo sulle vendite. Per ulteriori informazioni, consulta la documentazione [PayPal per ottenere i numeri di telefono di contatto](https://www.sandbox.paypal.com/businessmanage/preferences/website).

Questa funzionalità è `off` per impostazione predefinita. Quando lo abiliti, gli amministratori dei negozi possono visualizzare i numeri di telefono quando un cliente completa un flusso di pagamento con marchio all’esterno della pagina di pagamento.

>[!IMPORTANT]
>
>Questa impostazione non si applica ad altri flussi di pagamento.

## Paese dell&#39;acquirente

In produzione, PayPal utilizza la geolocalizzazione dell&#39;acquirente per determinare quali metodi di pagamento sono disponibili nei flussi di pagamento rapido e di pagamento. Poiché la modalità sandbox non supporta la geolocalizzazione, utilizza la configurazione **Paese dell&#39;acquirente** per simulare la posizione dell&#39;acquirente e controllare quali metodi di pagamento vengono sottoposti a rendering.

Questa impostazione è utile per testare metodi di pagamento specifici per l&#39;area geografica, come Venmo (solo Stati Uniti), Pay Later (Paga più tardi (Stati Uniti e Regno Unito) o [Local Payment Methods](payments-options.md#local-payment-methods) (Europa) senza bisogno di una VPN.

Per configurare il paese dell&#39;acquirente:

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.

1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e seleziona **[!UICONTROL Payment Methods]**.

1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.

1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione&#x200B;_[!UICONTROL General Configuration]_.

1. Imposta **[!UICONTROL Method]** su `Sandbox`.

1. Selezionare il paese desiderato dal menu a discesa **[!UICONTROL Buyer's country]**.

1. Fai clic su **[!UICONTROL Save Config]** per salvare le modifiche.

>[!NOTE]
>
>L&#39;impostazione **[!UICONTROL Buyer's country]** viene visualizzata solo quando il metodo è impostato su `Sandbox`. Questo non influisce sugli ambienti di produzione.

## Test in ambiente sandbox

Si consiglia vivamente di utilizzare gli spazi di dati di test per gli ambienti di integrazione e staging e per testare Payments in produzione, con carte di credito e banche reali, prima di esporre questa funzionalità agli acquirenti.

Per ulteriori informazioni, vedere [Verifica e convalida](test-validate.md).
