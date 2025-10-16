---
title: Onboarding  [!DNL Payment Services]  flusso
description: Connetti la tua istanza con la funzionalità  [!DNL Payment Services]  completando alcuni passaggi di onboarding.
role: User
level: Intermediate
exl-id: 1ee8c660-0941-4378-a1d7-ae45de3de211
feature: Payments, Checkout, Integration, Paas, Saas
source-git-commit: 999407f00b118441abe39209a15f587ec73fa75d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# Onboarding del flusso [!DNL Payment Services]

Per iniziare a utilizzare [!DNL Payment Services], devi completare alcuni passaggi di onboarding. Per istruzioni precise, seleziona l’opzione Adobe Commerce seguente che si allinea al meglio all’istanza e alla versione della tua organizzazione.

Questo diagramma di flusso mostra il processo generale per l&#39;onboarding di [!DNL Payment Services] in tutte le versioni:

![Flusso di onboarding](assets/flow-payment-services.png){width="700" zoomable="yes"}

Di seguito trovi la versione Adobe Commerce specifica da integrare con [!DNL Payment Services].

## Aiutami a trovare l’istanza e la versione

### ADOBE COMMERCE o MAGENTO OPEN SOURCE | v2.4.7+

Questi diagrammi di flusso mostrano il processo generale per l&#39;onboarding di [!DNL Payment Services] con un Adobe Commerce o Magento Open Source più recente della versione v2.4.7.

>[!BEGINTABS]

>[!TAB Sandbox]

Questo diagramma di flusso mostra il processo sandbox di onboarding con un Adobe Commerce o Magento Open Source successivo alla versione 2.4.7, dove [!DNL Payment Services] è pronto all&#39;uso con Adobe Commerce.

![Flusso di onboarding](assets/flow-sandbox-configuration-onboarding-2.4.7.png){width="700" zoomable="yes"}

**Passaggi per l&#39;onboarding delle versioni v2.4.7+ Parte 1: Sandbox**

1. [Connetti l&#39;istanza](connect.md#configure-commerce-services) ai servizi Commerce. Questa connessione deve essere completata una sola volta per ogni istanza di Commerce. [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."}
1. [Configura il servizio sandbox](sandbox.md#enable-sandbox-testing) (oppure, in alternativa, accedi a [abilitazione dei pagamenti live](sandbox.md#enable-live-payments) se hai testato funzionalità in un altro ambiente) con un account di elaborazione pagamento PayPal di prova.
1. Verifica dei pagamenti in un ambiente [sandbox](sandbox.md#test-in-sandbox-environment).

[![ulteriori informazioni](assets/learn-more-button.svg)](https://helpx.adobe.com/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB Produzione]

Questo diagramma di flusso mostra i passaggi di produzione necessari per abilitare [!DNL Payment Services].

![Flusso di onboarding](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

**Passaggi per l&#39;onboarding delle versioni v2.4.7+ Parte 2: Produzione**

1. [Imposta [!DNL Payment Services] come metodo di pagamento](production.md#set-payment-services-as-payment-method), in modalità sandbox, per iniziare a elaborare i pagamenti di prova.
1. [Richiedi il pagamento del diritto](production.md#request-payments-entitlement-from-adobe) per abilitare l&#39;onboarding in tempo reale.
1. [Completa l&#39;onboarding degli esercenti](production.md#complete-merchant-onboarding) per abilitare i pagamenti live per i tuoi siti Web Commerce.
1. [Ottieni il tuo [!DNL Payment Services] ID commerciante](production.md#configure-pricing-tier) e trasmettilo alle vendite per configurare il piano tariffario corretto.
1. [Attiva [!DNL Payment Services] in modalità live](production.md#enable-live-payments) per iniziare l&#39;elaborazione dei pagamenti live.
1. Pagamenti di prova, in entrambi gli ambienti [sandbox](sandbox.md#test-in-sandbox-environment) e [production](production.md#test-in-production).

[![ulteriori informazioni](assets/learn-more-button.svg)](production.md)

>[!ENDTABS]

### ADOBE COMMERCE o MAGENTO OPEN SOURCE | v2.4.0-2.4.6 [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."}

Questi diagrammi di flusso mostrano il processo generale per l&#39;onboarding di [!DNL Payment Services] con Adobe Commerce o Magento Open Source versioni da 2.4.0 a 2.4.6. È necessario scaricare e installare [!DNL Payment Services] per iniziare l&#39;onboarding.

>[!BEGINTABS]

>[!TAB Sandbox]

Questo diagramma di flusso mostra i passaggi sandbox necessari per l&#39;onboarding di [!DNL Payment Services] con Adobe Commerce o Magento Open Source versioni da 2.4.0 a 2.4.6.

![Flusso di onboarding](assets/flow-sandbox-installation-configuration-onboarding-2.4.0.png){width="700" zoomable="yes"}

**Passaggi di onboarding per le versioni v2.4.0-2.4.6 Parte 1: Sandbox**

1. [Installare l&#39;estensione [!DNL Payment Services] &#x200B;](install.md#get-payment-services) se necessario.
1. [Ottieni credenziali API](connect.md#obtain-api-credentials).
1. [Connetti l&#39;istanza](connect.md#configure-commerce-services) ai servizi Commerce. Questa connessione deve essere completata una sola volta per ogni istanza di Commerce.
1. [Configura il servizio sandbox](sandbox.md#enable-sandbox-testing) (oppure, in alternativa, accedi a [abilitazione dei pagamenti live](sandbox.md#enable-live-payments) se hai testato funzionalità in un altro ambiente) con un account di elaborazione pagamento PayPal di prova.
1. Verifica dei pagamenti in un ambiente [sandbox](sandbox.md#test-in-sandbox-environment).

[![ulteriori informazioni](assets/learn-more-button.svg)](https://helpx.adobe.com/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB Produzione]

Questo diagramma di flusso mostra il processo generale per abilitare [!DNL Payment Services] in un ambiente di produzione con Adobe Commerce o Magento Open Source versioni da 2.4.0 a 2.4.6.

![Flusso di onboarding](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

**Passaggi di onboarding per le versioni v2.4.0-2.4.6 Parte 2: Produzione**

1. [Imposta [!DNL Payment Services] come metodo di pagamento](production.md#set-payment-services-as-payment-method), in modalità sandbox, per iniziare a elaborare i pagamenti di prova.
1. [Richiedi il pagamento del diritto](production.md#request-payments-entitlement-from-adobe) per abilitare l&#39;onboarding in tempo reale.
1. [Completa l&#39;onboarding degli esercenti](production.md#complete-merchant-onboarding) per abilitare i pagamenti live per i tuoi siti Web Commerce.
1. [Ottieni il tuo [!DNL Payment Services] ID commerciante](production.md#configure-pricing-tier) e trasmettilo alle vendite per configurare il piano tariffario corretto.
1. [Attiva [!DNL Payment Services] in modalità live](production.md#enable-live-payments) per iniziare l&#39;elaborazione dei pagamenti live.
1. Pagamenti di prova, in entrambi gli ambienti [sandbox](sandbox.md#test-in-sandbox-environment) e [production](production.md#test-in-production).

[![ulteriori informazioni](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

>[!NOTE]
>
>Se non configuri i servizi Commerce nell’amministratore (parte 1), non puoi impostare pagamenti sandbox o live.

>[!MORELIKETHIS]
>
> * [Risoluzione dei problemi [!DNL Payment Services] installazione](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
> * [Conto sandbox PayPal non verificato](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
> * [Dati di report [!DNL Payment Services]  ritardati](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
> * [Il test della carta di credito non riesce con PayPal durante l&#39;elaborazione dei pagamenti in un ambiente Sandbox](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
> * [Disabilita l&#39;estensione [!DNL Payment Services] &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions#manage-extensions-1)