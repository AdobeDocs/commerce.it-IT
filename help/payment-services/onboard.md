---
title: Onboarding [!DNL Payment Services]
description: Connetti la tua istanza con la funzionalità  [!DNL Payment Services]  completando alcuni passaggi di onboarding.
role: User
level: Intermediate
feature: Payments, Checkout, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Onboarding [!DNL Payment Services]

Per iniziare a utilizzare [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source], è necessario completare alcuni passaggi di onboarding per collegare la tua istanza alla funzionalità dei pagamenti.

## Flusso di onboarding

Questo diagramma di flusso mostra il processo generale di onboarding di [!DNL Payment Services].

![Flusso di onboarding](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> Per Adobe Commerce versione 2.4.7 o successiva, puoi saltare il passaggio dell&#39;estensione Marketplace, in quanto [!DNL Payment Services] è disponibile come strumento pronto all&#39;uso.

Dopo aver completato l&#39;onboarding per i pagamenti sandbox o live, il reporting finanziario è accessibile da [!DNL Payment Services] nell&#39;amministratore.

Se i pagamenti sandbox e live sono entrambi integrati e abilitati, è possibile passare facilmente da una modalità all&#39;altra dalla home di [!DNL Payment Services].

## Prerequisiti

Per utilizzare [!DNL Payment Services], è necessario che tutti i moduli dipendenti siano abilitati e che siano disponibili i seguenti elementi per l&#39;istanza:

* Modulo Connettore servizi
* Modulo ID servizi
* Chiavi API

I moduli Connettore servizi e ID servizi vengono installati automaticamente durante l&#39;installazione [di [!DNL Payment Services]](install.md).

Al termine dell&#39;installazione, sarà possibile visualizzare una nuova sezione nelle impostazioni di configurazione (**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**) se si espande **[!UICONTROL Services]**—**[!UICONTROL Commerce Services Connector]**.

Per informazioni su come creare o accedere alle chiavi API, vedere [Credenziali API](#obtain-api-credentials).

## Passaggi di onboarding

1. [Installa  [!DNL Payment Services] estensione](install.md#get-payment-services).
1. [Ottieni credenziali API](connect.md#obtain-api-credentials).
1. [Connetti l&#39;istanza](connect.md#configure-commerce-services) ai servizi Commerce. Questa connessione deve essere completata una sola volta per ogni istanza di Commerce.
1. [Configura il servizio sandbox](sandbox.md#enable-sandbox-testing) (oppure, in alternativa, accedi a [abilitazione dei pagamenti live](sandbox.md#enable-live-payments) se hai testato funzionalità in un altro ambiente) con un account di elaborazione pagamento PayPal di prova.
1. [Imposta [!DNL Payment Services] come metodo di pagamento](production.md#set-payment-services-as-payment-method), in modalità sandbox, per iniziare a elaborare i pagamenti di prova.
1. [Richiedi il pagamento del diritto](production.md#request-payments-entitlement-from-adobe) per abilitare l&#39;onboarding in tempo reale.
1. [Completa l&#39;onboarding degli esercenti](production.md#complete-merchant-onboarding) per abilitare i pagamenti live per i tuoi siti Web Commerce.
1. [Ottieni il tuo [!DNL Payment Services] ID commerciante](production.md#configure-pricing-tier) e trasmettilo alle vendite per configurare il piano tariffario corretto.
1. [Attiva [!DNL Payment Services] in modalità live](production.md#enable-live-payments) per iniziare l&#39;elaborazione dei pagamenti live.
1. Pagamenti di prova, in entrambi gli ambienti [sandbox](sandbox.md#test-in-sandbox-environment) e [production](production.md#test-in-production).

>[!NOTE]
>
>Se non configuri i servizi Commerce nell’amministratore (passaggio 3), non puoi impostare pagamenti sandbox o live.

## Risoluzione dei problemi

* [Risoluzione dei problemi [!DNL Payment Services] installazione](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
* [Conto sandbox PayPal non verificato](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
* [Dati di report](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html) ritardati [!DNL Payment Services] 
* [Il test della carta di credito non riesce con PayPal durante l&#39;elaborazione dei pagamenti in un ambiente Sandbox](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
