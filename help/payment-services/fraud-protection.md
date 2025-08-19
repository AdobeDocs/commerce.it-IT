---
title: Protezione contro le frodi Signifyd
description: Abilita la protezione antifrode automatizzata per  [!DNL Payment Services]  con Signifyd.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security, Paas, Saas
exl-id: 440296bb-a6ff-408b-8195-3027916e4f84
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Protezione contro le frodi significative

È possibile abilitare la protezione antifrode automatica per [!DNL Payment Services] con l&#39;estensione [Signifyd](https://commercemarketplace.adobe.com/signifyd-module-connect.html).

Adobe Commerce supporta Signifyd versioni 5.4.0 e successive. [!DNL Payment Services] supporta flussi Signifyd di pre-autenticazione e post-autenticazione.

L&#39;integrazione Signifyd/[!DNL Payment Services] fornisce copertura per carte di credito, carte di debito, carte di vaulting, pagamento tramite Admin e metodi di pagamento PayPal e Apple Pay. Mentre alcuni dettagli delle transazioni non sono condivisi tra Payment Services e Signifyd, Signifyd fornisce una copertura completa dei rischi per tutti i metodi di pagamento, garantendo la massima protezione.

>[!CAUTION]
>
> [Fastlane](payments-options.md#fastlane-button) non è compatibile con Signifyd.

Per informazioni sull&#39;installazione e la configurazione dell&#39;estensione, consulta la [documentazione di Signifyd](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension).

## Onboarding

È necessario comunicare direttamente con Signifyd per integrare l&#39;estensione da utilizzare con [!DNL Payment Services]. Non è necessaria alcuna configurazione di [!DNL Payment Services]. Una volta installata, puoi configurare l’estensione Signifyd in Admin. Qualsiasi supporto relativo a questa estensione verrà gestito da Signifyd.

Durante l’onboarding con Signifyd è necessario:

1. Contatta Signifyd per impostare un nuovo account.
1. Per impostazione predefinita, Signifyd è [inserito nell&#39;elenco Consentiti](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md) per garantire che Signifyd non venga attivato per altre opzioni di pagamento attualmente non supportate. Se si desidera vietare un particolare metodo di pagamento, è necessario apportare modifiche.
1. Conferma con Signifyd che PayPal non rifiuterà gli ordini che potrebbero essere approvati da Signifyd tramite l&#39;impostazione di protezione dalle frodi del commerciante in Paypal.
1. Abilita l&#39;estensione Signifyd per la compatibilità con [!DNL Payment Services]:
   * Quando si utilizza [!DNL Payment Services] in modalità _Live_, Signifyd deve essere in modalità Produzione.
   * Quando si utilizza [!DNL Payment Services] in modalità _Sandbox_, Signifyd deve essere in modalità di test.

## Configurazione

Poiché Signifyd esegue alcune azioni sugli ordini, è necessario configurare l&#39;estensione in modo che si comporti in modo appropriato in base all&#39;azione di pagamento impostata per [!DNL Payment Services].

Queste opzioni di configurazione non sono compatibili con Payment Services e l’integrazione Signifyd:

* Quando [!DNL Payment Services] è configurato con l&#39;azione di pagamento `Authorize` _e_ Signifyd è in modalità `PostAuth` con l&#39;opzione _[!UICONTROL Decline Guarantees]_&#x200B;impostata su **Crea nota di credito**.

  Motivo: [!DNL Payment Services] crea una transazione di autorizzazione che Signify tenta quindi di rimborsare.


* [!DNL Payment Services] è configurato con l&#39;azione di pagamento `Authorize and Capture` _e_ Signifyd è in modalità `PostAuth` con l&#39;opzione _[!UICONTROL Decline Guarantees]_&#x200B;impostata su **Annulla ordine**.

  Motivo: [!DNL Payment Services] crea una transazione di acquisizione che Signifyd tenta quindi di annullare.


Consulta la documentazione di Signifyd per informazioni sulla [configurazione dell&#39;estensione](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension).

Per ulteriori informazioni sui flussi di lavoro degli ordini[, consulta la documentazione di Signifyd.](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works)
