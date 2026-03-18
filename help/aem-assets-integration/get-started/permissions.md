---
title: Configurare le autorizzazioni utente IMS per l’integrazione di AEM Assets
description: Scopri in che modo i profili Admin Console e di identità IMS consentono l’accesso alla consegna AEM Assets, il Selettore risorse e i campi di configurazione di Commerce con compilazione automatica.
feature: CMS, Media, Configuration
source-git-commit: 0fd98bf86555c914f7a5b1e177c31c37764dbf84
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Autorizzazioni utente e IMS

**IMS** (Adobe Identity Management System) è il livello di autenticazione. Per Adobe Commerce as a Cloud Service, l’autenticazione IMS è abilitata per impostazione predefinita in Admin. Per Adobe Commerce su cloud o on-premise, IMS è facoltativo;[L&#39;abilitazione di IMS per Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank} fornisce un&#39;interfaccia utente di configurazione avanzata (selettore risorse, elenchi a discesa con compilazione automatica), ma puoi configurare l&#39;integrazione senza IMS immettendo manualmente **ID programma** e **ID ambiente**.

L&#39;integrazione AEM Assets richiede inoltre **profili di prodotto Adobe Admin Console** specifici quando si utilizza IMS. Gli utenti che configurano l&#39;integrazione in Commerce Admin hanno bisogno del profilo di prodotto **Utenti AEM Assets DM OpenAPI - delivery** oppure del profilo di prodotto **author** come fallback. Questo viene controllato tramite i profili di prodotto di Admin Console nell’organizzazione IMS dell’utente e consente di:

* **Il selettore risorse** consente di selezionare immagini da AEM Assets durante la gestione di immagini di categorie o contenuti di Page Builder.
* **Campi di configurazione con compilazione automatica**, ad esempio **ID programma**, **ID ambiente** e **Mappatura dominio**, che estraggono valori dalla sessione IMS dell&#39;utente in base ai profili di prodotto di Admin Console (consegna o creazione).

Se non disponi delle autorizzazioni corrette, il Selettore risorse non è disponibile e questi campi appaiono vuoti o richiedono l’immissione manuale.
>[!BEGINSHADEBOX]

**Funzionamento di IMS e delle autorizzazioni**

Adobe IMS fornisce l&#39;identità utente e il contesto dell&#39;organizzazione, mentre Adobe Admin Console definisce i **profili di prodotto**(autorizzazioni) di cui dispone. L’integrazione di AEM Assets utilizza i dettagli IMS più il profilo assegnato per determinare se può compilare automaticamente i campi di configurazione e abilitare il selettore delle risorse.

>[!ENDSHADEBOX]

## Perché sono richiesti i profili di prodotto

L’integrazione può caricare solo domini mappati a un profilo. Pertanto, gli utenti possono disporre dei seguenti profili di prodotto:

* **Profilo prodotto di consegna AEM**. Obbligatorio per il selettore delle risorse e l’interfaccia utente di configurazione quando l’utente dispone sia di profili di authoring che di profili di consegna. L’integrazione utilizza il profilo di prodotto di consegna AEM, se disponibile.

* **Crea profilo prodotto**. Necessario per accedere all’interfaccia utente di AEM Assets. Funge anche da fallback per il selettore delle risorse e l’interfaccia utente di configurazione quando l’utente non dispone del profilo di prodotto di consegna AEM nel proprio Admin Console.

I domini (inclusi l’ID del programma, l’ID ambiente e la mappatura del dominio) sono assegnati al profilo di prodotto di consegna AEM. L&#39;integrazione carica i domini dal **profilo di prodotto di consegna AEM** se disponibile, oppure torna al **profilo di prodotto Author** se il profilo di prodotto di consegna AEM non è incluso nell&#39;Admin Console dell&#39;utente. Gli utenti devono disporre di uno di questi profili per:

* Compila i menu a discesa **ID programma**, **ID ambiente** e **Mappatura dominio** nella configurazione di amministrazione di Commerce.
* Utilizza il Selettore risorse per sfogliare e selezionare le risorse da AEM Assets.

Se nessuno dei due profili è configurato, gli utenti possono immettere manualmente **ID programma** e **ID ambiente**, ma il selettore risorse non sarà disponibile.

## Concedere le autorizzazioni per tipo di distribuzione

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE Solo SaaS]{type=Positive tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."}

L’autenticazione IMS è attivata per impostazione predefinita. Aggiungi l&#39;utente al profilo di prodotto **Utenti OpenAPI di AEM Assets DM - delivery** in [Adobe Admin Console](https://adminconsole.adobe.com/) o al profilo di prodotto **author** (ad esempio, `<environment-name> - author - <program-id> - <environment-id>`) come fallback quando l&#39;utente non dispone del profilo di prodotto AEM delivery nel proprio Admin Console.

>[!NOTE]
>
> Gli utenti devono essere aggiunti anche a Commerce e AEM Assets. Consulta [Aggiungere un utente ad AEM Assets o Product Visuals](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} nella _Guida per l&#39;utente e Identity Management_ per l&#39;installazione completa.

![Profilo prodotto Admin Console per la consegna AEM Assets](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB Adobe Commerce sul cloud o on-premise]

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."}

L&#39;ID client **IMS** è necessario affinché PaaS abiliti il selettore risorse. Consulta [Configurare il progetto AEM Assets](configure-aem.md#prerequisites) per i prerequisiti, incluso come ottenere l&#39;ID client IMS quando si abilita Dynamic Media con OpenAPI.

Per utilizzare il Selettore risorse e i campi di configurazione con compilazione automatica (ID programma, ID ambiente, Mappatura dominio):

1. [Abilita Adobe IMS per Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank} in modo che l&#39;amministratore di Commerce utilizzi l&#39;autenticazione IMS e possa leggere i profili di prodotto Admin Console dell&#39;utente.

1. [Apri un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) per richiedere un ID client IMS personalizzato per il selettore risorse.

1. Da [Adobe Admin Console](https://adminconsole.adobe.com/), aggiungi l&#39;utente al profilo di prodotto **Utenti AEM Assets DM OpenAPI - delivery** o al profilo di prodotto **author** (ad esempio, `<environment-name> - author - <program-id> - <environment-id>`) come fallback quando l&#39;utente non ha il profilo di prodotto AEM delivery nel proprio Admin Console.

Senza IMS, puoi comunque configurare l’integrazione immettendo manualmente l’ID programma e l’ID ambiente in Commerce Admin.

>[!ENDTABS]

## Documentazione correlata

* [Configurare le autorizzazioni utente IMS per l&#39;integrazione di AEM Assets](setup-synchronization.md)—Connettere Commerce ad AEM Assets e configurare le regole corrispondenti.
* [Selezione manuale delle risorse](../synchronize/asset-selector-integration.md): utilizza il selettore delle risorse per le immagini delle categorie e Page Builder.
* [Aggiungere un utente ad AEM Assets o ai visualizzatori di prodotto](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank}. Per ACS, aggiungere prima gli utenti a Commerce e AEM Cloud Manager (Proprietario business, Responsabile della distribuzione). Il profilo **Utenti OpenAPI di AEM Assets DM - consegna** (o profilo **autore** come fallback) è un requisito aggiuntivo per le funzioni Selettore risorse e di compilazione automatica.
* [Assegna membri del gruppo al livello di consegna di AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}. Documentazione di AEM per l’accesso alla consegna.
