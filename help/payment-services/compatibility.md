---
title: Compatibilità per  [!DNL Payment Services]
description: Scopri se  [!DNL Payment Services]  è disponibile nel tuo paese e se è compatibile con la versione di Adobe Commerce.
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
exl-id: 4bef8429-5053-424d-806a-9e8b96295b1b
TQID: https://experienceleague.adobe.com/UUD0IiEiwh0sZKMkclOJtoC2bKYcmDN3WAWD16mfad4
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 4235bf48bb5f24a076621ee5985e9e7316fcb1cc
workflow-type: tm+mt
source-wordcount: 498
ht-degree: 0%

---

# Compatibilità per [!DNL Payment Services]

[!DNL Payment Services] è disponibile per [!DNL Adobe Commerce as a Cloud Service], tutte le versioni supportate di [!DNL Adobe Commerce on Cloud] e on-premise e Magento Open Source. Per informazioni specifiche sulla versione, vedere la pagina [Criteri del ciclo di vita](https://experienceleague.adobe.com/it/docs/commerce-operations/release/planning/lifecycle-policy).

## Prerequisiti

Per utilizzare [!DNL Payment Services], devi prima connettere la tua istanza Commerce. **La connessione viene eseguita una sola volta**.

1. Se non sei sicuro che l&#39;istanza sia connessa, passa a **Sistema** > Servizi > **Connettore servizi Commerce** per visualizzare le chiavi API e i dettagli dell&#39;identificatore SaaS. Se tali valori sono presenti, l’istanza è connessa.

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

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

Per ulteriori informazioni sulla configurazione dell&#39;estensione [!DNL Payment Services], vedere [Connect](connect.md).

>[!BEGINTABS]

>[!TAB Standard (Estrazione rapida)]

![assegno](assets/icon-check.png) Pagamento PayPal

![assegno](assets/icon-check.png) Pulsante Addebito PayPal o carta di credito

![check](assets/icon-check.png) Configurazioni di estrazione personalizzate

![verifica](assets/icon-check.png) Prezzi standard

![verifica](assets/icon-check.png) **Disponibile in più di 200 paesi**

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

![check](assets/icon-check.png) disponibile in 37 paesi. Australia, Austria, Belgio, Bulgaria, Canada, Cina, Cipro, Repubblica ceca, Danimarca, Estonia, Finlandia, Francia, Germania, Grecia, Hong Kong, Irlanda, Italia, Giappone, Lettonia, Liechtenstein, Lituania, Lussemburgo, Malta, Messico, Norvegia, Paesi Bassi, Polonia, Portogallo, Romania, Singapore, Slovacchia, Slovenia, Spagna, Svezia, Regno Unito, Stati Uniti. **Tariffe negoziate disponibili in Stati Uniti (USA), Canada (CA), Australia (AU), Francia (FR), Regno Unito (GB), Italia (IT), Paesi Bassi (NL), Germania (DE)**

[![ulteriori informazioni](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

Per ulteriori informazioni sulla versione e sulle specifiche della versione, consulta le pagine [Ciclo di vita](https://experienceleague.adobe.com/it/docs/commerce-operations/release/planning/lifecycle-policy) e [[!DNL Payment Services] note sulla versione](release-notes.md).

Per istruzioni complete e avviare il processo di onboarding, consulta [Introduzione a [!DNL Payment Services]](onboard.md).

### Carte di credito accettate e valute

[!DNL Payment Services] accetta le valute dei paesi in cui è disponibile. Per ulteriori informazioni sull&#39;impostazione dei tassi di cambio, vedere [Configurazione della valuta](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration).

Per ulteriori informazioni sulle valute e sui metodi di pagamento disponibili con i prodotti e i servizi PayPal, consulta le pagine seguenti:

* [Documentazione sulle valute supportate](https://developer.paypal.com/reports/reference/supported-currencies).

* [Documentazione sui metodi di pagamento](https://developer.paypal.com/payment-methods).
