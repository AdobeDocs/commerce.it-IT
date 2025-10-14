---
title: Compatibilità per  [!DNL Payment Services]
description: Scopri se  [!DNL Payment Services]  è disponibile nel tuo paese e se è compatibile con la versione di Adobe Commerce.
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# Compatibilità per [!DNL Payment Services]

[!DNL Payment Services] è disponibile per Adobe Commerce e Magento Open Source. [!DNL Payment Services] è ora compatibile con Adobe Commerce versioni 2.4.x.

## Prerequisiti

Per utilizzare [!DNL Payment Services], devi prima connettere la tua istanza Commerce. **La connessione è stata configurata una sola volta**.

1. Se non sei sicuro che l&#39;istanza sia connessa, passa a **Sistema** > Servizi > **Connettore servizi Commerce** e visualizza i valori delle chiavi API pubblica e privata nelle sezioni Chiavi sandbox e Chiavi di produzione e i campi Progetto e Spazio dati nella sezione Identificatore SaaS. Se tali valori sono presenti, l’istanza è connessa.

1. Se è ancora necessario connettere l&#39;istanza, visualizzare le istruzioni nella pagina [Connettore servizi Commerce](../landing/saas.md).

   >[!TIP]
   >
   > Per ulteriori informazioni, guarda il video tutorial su [Adobe Commerce Services Connector](https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector).

1. Se hai già connesso l&#39;istanza, passa alla pagina [onboarding](onboard.md) per i passaggi successivi.

>[!IMPORTANT]
>
> Tutti i commercianti autorizzati per [!DNL Payment Services] possono utilizzare **uno spazio dati produzione** e **due spazi dati test**.

## Esperienza [!DNL Payment Services] standard e avanzata

[!DNL Payment Services] fornisce **Opzioni di pagamento standard** (pagamento rapido) e **Avanzate** (completamente supportate) e flussi di onboarding, a seconda del paese in cui operi.

>[!NOTE]
>
> [!DNL Payment Services] fornisce [funzionalità di estrazione rapida](../payment-services/payments-options.md) (sottoinsieme di opzioni di pagamento) per altri [paesi disponibili durante l&#39;onboarding](../payment-services/production.md#complete-merchant-onboarding).

### Qual è l&#39;opzione [!DNL Payment Services] più adatta alle tue esigenze?

>[!VIDEO](https://video.tv.adobe.com/v/3447926?captions=ita)

Per ulteriori informazioni sulla configurazione dell&#39;estensione [!DNL Payment Services], vedere [Connect](connect.md).

>[!BEGINTABS]

>[!TAB Standard (Estrazione rapida)]

![assegno](assets/icon-check.png) Pagamento PayPal

![assegno](assets/icon-check.png) Pulsante Addebito PayPal o carta di credito

![check](assets/icon-check.png) Configurazioni di estrazione personalizzate

![verifica](assets/icon-check.png) Prezzi standard

![verifica](assets/icon-check.png) **Disponibile in XX paesi**

[![ulteriori informazioni](assets/learn-more-button.svg)](onboard.md)

>[!TAB Avanzate (Completamente Supportate)]

![assegno](assets/icon-check.png) carta di debito

![verifica](assets/icon-check.png) credito PayPal

![verifica](assets/icon-check.png) campi carta di credito

![spunta](assets/icon-check.png) pulsante Apple Pay

![verifica](assets/icon-check.png) pulsante Google Pay

![assegno](assets/icon-check.png) Pulsanti di pagamento PayPal

![spunta](assets/icon-check.png) pulsante Venmo

![assegno](assets/icon-check.png) Pulsante Addebito PayPal o carta di credito

![assegno](assets/icon-check.png) Pulsante Paga più tardi

![check](assets/icon-check.png) Configurazioni di estrazione personalizzate

![verifica](assets/icon-check.png) prezzi personalizzati

![verifica](assets/icon-check.png) (funzionalità di determinazione prezzi L2/L3 - solo Stati Uniti)

![verifica](assets/icon-check.png) **Disponibile solo negli Stati Uniti, in Canada (CA) e in Australia (AUS). Francia (FR), Regno Unito (UK)**

[![ulteriori informazioni](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

Per ulteriori informazioni sulla versione e sulle specifiche della versione, consulta le pagine [Ciclo di vita](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=it) e [[!DNL Payment Services] note sulla versione](release-notes.md).

Per istruzioni complete e avviare il processo di onboarding, consulta [Introduzione a [!DNL Payment Services]](onboard.md).

### Carte di credito accettate e valute

[!DNL Payment Services] accetta le valute dei paesi [&#x200B; in cui è disponibile](#availability). Per ulteriori informazioni sull&#39;impostazione dei tassi di cambio, vedere [Configurazione della valuta](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=it).

Per ulteriori informazioni sulle valute e sui metodi di pagamento disponibili con i prodotti e i servizi PayPal, consulta le pagine seguenti:

* [Documentazione sulle valute supportate](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

* [Documentazione sui metodi di pagamento](https://developer.paypal.com/docs/checkout/payment-methods/).
