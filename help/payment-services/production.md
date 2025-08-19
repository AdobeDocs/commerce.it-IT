---
title: Abilita  [!DNL Payment Services]  per la produzione
description: Completa il processo di onboarding abilitando  [!DNL Payment Services]  per la produzione.
exl-id: 3b1269e8-127b-47f8-9738-9722a5737c63
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Abilita [!DNL Payment Services] per la produzione

Puoi mettere il servizio in produzione e completare il [processo di onboarding](onboard.md), seguendo i passaggi descritti in questo argomento, dopo aver:

* [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} [Installa](install.md) l&#39;estensione di Payment Services
* [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} [Configura e connetti](connect.md) la tua istanza
* [Configura](sandbox.md) e [verifica](test-validate.md) la tua sandbox

## Imposta [!DNL Payment Services] come metodo di pagamento

Dopo aver [configurato i servizi Commerce](connect.md#configure-commerce-services) e abilitato i [test sandbox](sandbox.md#enable-sandbox-testing) o i [pagamenti live](#enable-live-payments), è necessario impostare [!DNL Payment Services] come metodo di pagamento.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Fare clic su **[!UICONTROL Enable Payment Services]**.

   Questa opzione è visibile se non hai ancora configurato [!DNL Payment Services] come metodo di pagamento per uno o più siti Web.

   Si viene indirizzati all&#39;area delle impostazioni nella visualizzazione Home con le opzioni pertinenti espanse (**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Settings]_), dove è possibile abilitare le opzioni [!DNL Payment Services] come [metodo di pagamento](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods){target="_blank"}.

1. In _[!UICONTROL General Configuration]_, impostare **[!UICONTROL Enable]**&#x200B;su `Yes`.
1. Impostare **[!UICONTROL Payment Action]**, sia per _[!UICONTROL Credit Card Fields]_&#x200B;che per&#x200B;_[!UICONTROL PayPal payment buttons]_, su una delle opzioni seguenti:

   | Impostazione | Descrizione |
   |---|---|
   | `Authorize` | Approva l&#39;acquisto e blocca i fondi. L&#39;importo non viene prelevato fino a quando non viene &quot;catturato&quot; dal mercante. |
   | `Authorize and Capture` | Approva l&#39;acquisto e il commerciante &quot;cattura&quot; i fondi. |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services] supporta le acquisizioni parziali. Un commerciante può acquisire parzialmente (fatturare) parti di un ordine. Ad esempio, puoi acquisire ogni elemento singolarmente oppure un elemento ora e il resto in un secondo momento.

1. Fare clic su **[!UICONTROL Save]**.
1. Fare clic su **[!UICONTROL Go to Payment Services]** per tornare alla home di [!DNL Payment Services].
1. [Cancella la cache](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html).

   La cancellazione deve essere eseguita dopo ogni modifica della configurazione.

Consulta [Configura [!DNL Payment Services]](configure-admin.md) per ulteriori informazioni sulla configurazione dei campi della carta di credito e dei pulsanti di pagamento PayPal.

## Onboarding completo per gli esercenti

Il passaggio successivo per consentire ai negozi di andare in diretta con Payment Services consiste nel completare l’onboarding in tempo reale.

Payment Services fornisce [**opzioni di pagamento avanzate** (completamente supportate) e **standard** (pagamento rapido)](../payment-services/payments-options.md#standard-vs-advanced-payments-experience) e flussi di onboarding, a seconda del paese in cui operi e dell&#39;esperienza di pagamento preferita.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Fare clic su **[!UICONTROL Live onboarding]**.

   Questa opzione è visibile se non hai ancora completato l&#39;onboarding live per [!DNL Payment Services].

1. Nella finestra modale _Seleziona il tuo paese_, seleziona il paese da cui stai operando.

   Payment Services offre supporto completo per tutte le opzioni di pagamento attualmente disponibili in [cinque paesi](../payment-services/introduction.md#availability). Payment Services fornisce funzionalità di pagamento rapido (un sottoinsieme di opzioni di pagamento) per tutti gli altri paesi rappresentati nell&#39;elenco dei paesi.

   Il paese selezionato dall&#39;elenco determina le opzioni di pagamento e il flusso di onboarding [Avanzate](#advanced-onboarding) (completamente supportato) o [Standard](#standard-onboarding) (pagamento rapido) a tua disposizione.

>[!TIP]
>
> Una volta scelta e portata avanti l’opzione di onboarding (Standard o Avanzata), è necessario completare di nuovo l’onboarding per effettuare l’aggiornamento o il downgrade dalla selezione iniziale.

### Onboarding avanzato

Questo flusso di onboarding è disponibile per i commercianti in [paesi completamente supportati](../payment-services/introduction.md#availability).

Dopo aver selezionato il paese:

1. Nel modale visualizzato, selezionare **Avanzate**.

   Per l&#39;opzione **Standard**, passare al [Flusso di onboarding standard](#standard-onboarding).

1. Fai clic su **Continua**.
1. Continua con il flusso PayPal per l&#39;onboarding avanzato completamente supportato, utilizzando le credenziali del tuo account PayPal (non le credenziali del tuo account sandbox) _o_ iscriviti a un nuovo account PayPal.

>[!IMPORTANT]
>
>**L&#39;onboarding avanzato** richiede agli esercenti di [richiedere il diritto ai pagamenti](#request-payments-entitlement-from-adobe) per abilitare l&#39;onboarding in tempo reale.

### Onboarding standard

Questo flusso di onboarding standard è disponibile per i commercianti nei paesi disponibili per i quali è fornito il supporto per [solo Express Checkout](../payment-services/introduction.md#availability).

Dopo aver selezionato il paese:

1. Nel modale _Contratto di servizi di pagamento_ visualizzato, fare clic sul collegamento **Contratto di servizi di pagamento** per visualizzare il contratto di servizi di pagamento Adobe Commerce.
1. Nel modale _Contratto di servizi di pagamento_, fare clic su **Accetto**.
1. Continua con il flusso PayPal per l&#39;onboarding del Checkpoint rapido, utilizzando le credenziali del tuo account PayPal (non le credenziali del tuo account sandbox) o iscriviti a un nuovo account PayPal.

>[!IMPORTANT]
>
>[I campi Paga e carta di credito di Apple](../payment-services/payments-options.md) non sono disponibili per **l&#39;onboarding standard**.

## Conferma indirizzo e-mail

1. Nella barra laterale di amministrazione, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**

   Il pulsante _[!UICONTROL Live onboarding]_&#x200B;non è più visibile. Verrà visualizzata una casella di testo &quot;[!UICONTROL Live payments pending]&quot;.

   In questa casella di testo, ti potrebbe anche essere chiesto di confermare il tuo indirizzo e-mail con PayPal per completare l&#39;onboarding.

1. Se ti viene richiesto di confermare il tuo indirizzo e-mail, controlla la tua e-mail per il messaggio di conferma inviato da PayPal e fai clic per confermare il tuo indirizzo e-mail.
1. Nella barra laterale di amministrazione, vai a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Aggiorna la finestra del browser.

   Quando l&#39;onboarding del commerciante PayPal viene approvato, dovrebbe essere visualizzata una notifica che informa che il sistema di pagamento è in modalità sandbox e non elabora pagamenti live.

   >[!IMPORTANT]
   >
   >Se revoci il consenso a [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] per l&#39;elaborazione dei pagamenti (nelle impostazioni del tuo conto PayPal), gli ordini nel tuo Negozio non possono essere elaborati da [!DNL Payment Services]. Nella pagina Home di Payment Services viene visualizzato un avviso relativo alla revoca del consenso.

## Richiedi diritti pagamenti da Adobe

Per abilitare la pubblicazione dei tuoi store, richiedi pagamenti a Adobe (solo per [l&#39;onboarding avanzato](#advanced-onboarding)):

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Fai clic su **[!UICONTROL Get Live Payments]** nella Home di [!DNL Payment Services].

   ![Richiedi adesioni](assets/request-entitlements.png){width="500" zoomable="yes"}

1. Compila il modulo.
1. Un membro del team vendite ti contatterà.

In alternativa, puoi richiedere i pagamenti a Adobe all&#39;indirizzo [business.adobe.com](https://business.adobe.com/resources/payment-services.html).

>[!IMPORTANT]
>
>**L&#39;onboarding in tempo reale** non è accessibile fino a quando il diritto ai pagamenti non viene approvato.

## Configura piano tariffario

Ottieni il tuo [!DNL Payment Services] _ID esercente_:

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Nella visualizzazione Home, fare clic su **[!UICONTROL Settings]**. Per ulteriori informazioni, vedere [Home](payments-home.md).
1. Seleziona il _ID commerciante_ richiesto e invialo al tuo rappresentante commerciale che configurerà il piano tariffario corretto.

Per ulteriori informazioni sulle transazioni di pagamento, vedere [Elaborazione di livello 2 e livello 3](levels-card-payment-transactions.md).

## Abilita pagamenti live

Un _ID commerciante di produzione_ è generato automaticamente e popolato nella [configurazione](configure-admin.md). Non modificare o alterare questo ID.

Abilita pagamenti live:

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Nella Home, fare clic su **[!UICONTROL Settings]** in alto a destra della pagina. Per ulteriori informazioni, vedere [Home](payments-home.md).
1. Nella sezione _[!UICONTROL General Configuration]_&#x200B;impostare **[!UICONTROL Payment mode]**&#x200B;su `Production`.
1. Fare clic su **[!UICONTROL Save]**.
1. [Cancella la cache](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management){target="_blank"}.

   >[!IMPORTANT]
   >
   >Se non cancelli la cache, i clienti non possono vedere le opzioni di pagamento PayPal durante il pagamento.

Se si torna alla home di [!DNL Payment Services], il messaggio della modalità di pagamento Sandbox non viene più visualizzato perché si stanno elaborando pagamenti live.

Consulta [Configurare in Admin](configure-admin.md) per le opzioni di configurazione legacy.

>[!IMPORTANT]
>
>Se revoci il consenso a [!DNL Payment Services] per l&#39;elaborazione dei pagamenti (nelle impostazioni del tuo conto PayPal), gli ordini nel tuo Negozio non possono essere elaborati da [!DNL Payment Services]. Se desideri riabilitare l’elaborazione dei pagamenti, devi completare di nuovo l’onboarding. Nella pagina Home di Payment Services viene visualizzato un avviso relativo alla revoca del consenso.

## Test in produzione

Si consiglia vivamente di testare i pagamenti in produzione, con carte di credito reali e banche, prima di esporre questa funzionalità agli acquirenti.

Per ulteriori informazioni, vedere [Verifica e convalida](test-validate.md).
