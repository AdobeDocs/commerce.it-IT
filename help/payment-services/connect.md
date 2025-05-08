---
title: Connetti l’istanza
description: Connetti la tua istanza di Commerce utilizzando una chiave API e una chiave privata e specifica lo spazio di dati nella configurazione.
exl-id: 5038fd31-bac5-419e-a172-66919a9b5272
feature: Payments, Checkout, Configuration, Paas
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 0f2e9c3a7d990a46bafc5f3b8a083436d42643b5
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Connetti l’istanza

È possibile connettere l&#39;istanza di Commerce utilizzando una chiave API e una chiave privata e specificare lo spazio dati nella configurazione utilizzando [Connettore servizi Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html). **La connessione è stata configurata una sola volta.**

>[!VIDEO](https://video.tv.adobe.com/v/3447835)

>[!INFO]
>
> Per ulteriori informazioni, guarda il video [[!DNL Adobe Commerce] Connettore servizi](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=en).

* Se *hai già connesso l&#39;istanza*, ottenendo e utilizzando le credenziali API e configurando Commerce Services, puoi passare a [configurare la sandbox di prova](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html).
* Se ancora *devi connettere l&#39;istanza*, consulta le informazioni in questo argomento su [come ottenere le credenziali API](#obtain-api-credentials) e [come configurare Commerce Services](#configure-commerce-services).
* Se *non sei sicuro che l&#39;istanza sia connessa*, passa a **Sistema** > Servizi > **Connettore servizi Commerce** e visualizza i valori delle chiavi API pubblica e privata nelle sezioni [!UICONTROL Sandbox Keys] e [!UICONTROL Production Keys] e i campi *Progetto* e *Spazio dati* nella sezione [!UICONTROL SaaS Identifier]. Se tali valori sono presenti, l’istanza è connessa.

>[!NOTE]
>
>Tutti i commercianti autorizzati a Payment Services possono utilizzare uno spazio dati di produzione e due spazi dati di test.

## Ottenere le credenziali API

Per utilizzare un servizio SaaS di Commerce, è necessario utilizzare le chiavi API dell&#39;istanza (chiave API pubblica di Commerce e chiave privata) sia per la sandbox che per la produzione, che vengono create e gestite nel [dashboard del mio account](https://account.magento.com/customer/account/login). [È possibile creare la coppia di chiavi](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) per un account Commerce, uno per sandbox e uno per la produzione, anche se è possibile utilizzare attivamente una sola coppia alla volta.

>[!NOTE]
>
>Hai bisogno di assistenza per accedere al tuo dashboard [!UICONTROL My Account]? Consulta [Creare un account Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-create).

Una volta creata, una chiave API pubblica è sempre disponibile nella dashboard Il mio account. Può essere copiata o eliminata in base alle esigenze. La chiave API privata diventa visibile quando crei una chiave API pubblica per sandbox o produzione; è disponibile solo per la copia o il salvataggio dalla finestra di dialogo successiva e non è più accessibile in un secondo momento.

Una determinata coppia di chiavi API è valida per tutti i servizi Commerce in un ambiente, quindi se per l’istanza sono già configurati i servizi Commerce, la coppia di chiavi API è già presente nel connettore dei servizi Commerce.

Se la chiave API viene persa, una nuova coppia di chiavi API deve essere [generate](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#generate-an-api-key-and-private-key) e [applicate](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html#configure-saas-project) alla configurazione di Commerce Services Connector nell&#39;amministratore. Se nella configurazione sono configurate le chiavi errate o non ne esistono, in Payment Services viene visualizzata una finestra di dialogo di errore di verifica dell&#39;account che informa che l&#39;account non è stato verificato.

Visualizza un elenco [dei servizi Commerce disponibili che utilizzano l&#39;API](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas#availableservices).

Per informazioni su come generare una chiave API per ambienti sandbox o di produzione, consulta [Credenziali](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html#apikey).

>[!IMPORTANT]
>
>È consigliabile non rigenerare una coppia di chiavi API *e* per modificare l&#39;identificatore SaaS e/o lo spazio dati in un&#39;istanza di produzione attiva. Se vengono modificati, i dati dell’istanza andranno persi.

## Configurare i servizi Commerce

La stessa chiave API può essere utilizzata in più istanze, ma ogni istanza deve avere il proprio [Spazio dati SaaS](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html#saasenv).

>[!NOTE]
>
>I commercianti devono utilizzare le stesse chiavi generate per MageID per i propri diritti all’aiuto.

Dopo aver ottenuto le credenziali, è possibile configurare il progetto SaaS e Saas Data Space.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**.
1. Fare clic su **[!UICONTROL Configure Commerce Services]**.

   Questa opzione è visibile se per l&#39;account non sono ancora stati configurati i servizi Commerce.

   Si è indirizzati all&#39;area di configurazione in Admin, **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**, per configurare Commerce Services Connector.

1. Per configurare i Servizi Commerce, seguire i passaggi descritti in [Configurazione SaaS](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html#saasenv).

   >[!INFO]
   >
   > Per ulteriori informazioni, guarda il video [[!DNL Adobe Commerce] Connettore servizi](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=en#configuration-faqs).

## Endpoint

[!DNL Payment Services] utilizza [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html) per connettersi a Commerce Services e distribuire come SaaS. [!DNL Commerce Services Connector] comunica tramite l&#39;endpoint in:

* `commerce-beta.adobe.io` per gli ambienti sandbox.
* `commerce.adobe.io for` per gli ambienti live.
