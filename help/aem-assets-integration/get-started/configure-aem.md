---
title: Configurare il progetto AEM Assets per supportare i metadati di Commerce
description: Abilita la sincronizzazione perfetta delle risorse tra Adobe Commerce e AEM Assets aggiungendo i metadati richiesti per l’integrazione.
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
source-git-commit: 722ff812fbc196f3a678b4cefc38e6612739bd67
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---

# Configurare il progetto AEM Assets per supportare i metadati di Commerce

Quando si utilizza AEM Assets as a Digital Asset Management System (DAM) for Commerce, l&#39;installazione del pacchetto `assets-commerce` consente di gestire immagini e video per i prodotti Commerce dall&#39;ambiente di authoring AEM.

Completa i seguenti passaggi per configurare il progetto AEM Assets con il codice pacchetto e i metadati richiesti per gestire le risorse Commerce dall’ambiente di authoring AEM:

1. [Scopri di più su &#x200B;](#aem-commerce-assets-commerce-package-contents)

1. [Completa i passaggi di installazione per configurare il progetto AEM Assets per il supporto dei metadati Commerce](#step-1-install-the-assets-commerce-package)

## contenuti del pacchetto AEM Commerce assets-commerce

Adobe fornisce un codice pacchetto di AEM Commerce `assets-commerce` per aggiungere risorse dello spazio dei nomi e dello schema dei metadati Commerce alla configurazione dell&#39;ambiente Experience Manager Assets as a Cloud Service.

Questo codice di pacchetto aggiunge le seguenti risorse all’ambiente di authoring AEM Assets:

* Uno [spazio dei nomi personalizzato](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json), `Commerce` per identificare le proprietà relative a Commerce.

   * Tipo di metadati personalizzato `commerce:isCommerce` con etichetta `Eligible for Commerce` per assegnare tag alle risorse Commerce associate a un progetto Adobe Commerce.

   * Un tipo di metadati personalizzato `commerce:skus` e un componente dell&#39;interfaccia utente corrispondente per aggiungere una proprietà **[!UICONTROL Product Data]**. I dati prodotto includono le proprietà dei metadati per associare una risorsa Commerce agli SKU di prodotto.

     ![Controllo interfaccia utente dati prodotto personalizzato](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Attributi del tipo di metadati personalizzati `commerce:roles` e `commerce:positions` per mostrare come viene visualizzata la risorsa in Commerce.

* Modulo schema metadati con scheda Commerce che include i campi `Eligible for Commerce` e `Product Data` per l&#39;assegnazione di tag alle risorse Commerce. Il modulo fornisce inoltre opzioni per mostrare o nascondere i campi `roles` e `position` dall&#39;interfaccia utente di AEM Assets.

  ![Scheda Commerce per modulo schema metadati AEM Assets](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* [Esempio di risorsa con tag e approvata da Commerce](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg` per supportare la sincronizzazione iniziale delle risorse. Solo le risorse Commerce approvate possono essere sincronizzate da AEM Assets ad Adobe Commerce.

>[!NOTE]
>
> Per ulteriori informazioni sul [codice pacchetto AEM Commerce](https://github.com/ankumalh/assets-commerce), vedere la pagina **leggimi**.

## Prerequisiti

Per distribuire il codice pacchetto `assets-commerce` nell&#39;ambiente AEM Assets as a Cloud Service AEM sono necessarie le risorse e le autorizzazioni seguenti:

* [Accesso al programma e agli ambienti AEM Assets Cloud Manager](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo) con i ruoli Responsabile del programma e Responsabile della distribuzione.

* [ambiente di sviluppo AEM locale](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) e familiarità con il processo di sviluppo locale AEM.

* Comprendere la struttura del progetto [AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) e come distribuire pacchetti di contenuti personalizzati con Cloud Manager.

* L&#39;**ID organizzazione IMS** configurato per l&#39;istanza di Commerce.

## Passaggio 1: installare il pacchetto assets-commerce

1. Passa a AEM Cloud Manager, seleziona un programma e [crea ambienti di produzione e di staging](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments#creating-environments) che desideri integrare con Adobe Commerce.

1. Configura una [pipeline di distribuzione](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/pipeline-setup#create-front-end-pipeline) oppure verifica che la pipeline possa distribuire modifiche all&#39;ambiente selezionato.

1. [Clona l&#39;archivio Git gestito da Adobe](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/retrieve-access#repo-access) per il programma selezionato.

1. Da GitHub scaricare il codice del pacchetto dall&#39;[archivio Commerce di AEM Assets](https://github.com/ankumalh/assets-commerce).

1. Dall&#39;[ambiente di sviluppo AEM locale](https://experienceleague.adobe.com/it/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview), copia manualmente il codice scaricato nell&#39;archivio gestito Adobe esistente.

1. In tutti i `filter.xml` e i `pom.xml files` per il progetto, sostituisci tutte le occorrenze di `<my-app>` con il nome dell&#39;app.

>[!NOTE]
>
> In alternativa, puoi installare il codice personalizzato nella configurazione del progetto AEM Assets come pacchetto **Maven**.

1. Apporta le modifiche e invia il ramo di sviluppo locale all’archivio Git di Cloud Manager.

1. Da AEM Cloud Manager, [aggiorna l&#39;ambiente AEM utilizzando la pipeline per distribuire il codice](https://experienceleague.dobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager).

1. Vai a una risorsa e modificane le proprietà per convalidare le modifiche:

   * Lo schema metadati predefinito include la scheda **Commerce**.

   * Sono visibili gli SKU del prodotto e i campi `Eligible for Commerce`.

### La scheda Commerce non è visibile nelle proprietà

Se la scheda **Commerce** non viene visualizzata nelle proprietà, è necessario crearne manualmente una nell&#39;editor schema metadati.

1. Passa all’editor schema metadati.

1. Fai clic su **Modifica** per modificare il modulo schema metadati predefinito.

1. Creare una scheda **Commerce** e selezionarla.

1. Trascina e rilascia il componente **Product** nella scheda **Commerce** e mappalo sulla proprietà `commerce:skus`.

1. Selezionare la casella di controllo **mostra ruoli** e **mostra ordine**.

1. Trascina e rilascia un componente **checkbox** nella scheda **Commerce** e mapparlo sulla proprietà `commerce:isCommerce`. Definisci **Sì** e **No** come opzioni.

Se riscontri altri problemi, crea un [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=it#submit-ticket) o contatta il rappresentante commerciale per l&#39;integrazione di AEM Assets.

## Passaggio 2: facoltativo. Configurare un profilo di metadati

Nell’ambiente di authoring di AEM Assets, imposta i valori predefiniti per i metadati delle risorse Commerce creando un profilo di metadati. Quindi, applica il nuovo profilo alle cartelle di AEM Asset per utilizzare automaticamente queste impostazioni predefinite. Questa configurazione semplifica l’elaborazione delle risorse riducendo i passaggi manuali.

Quando configuri il profilo di metadati, devi configurare solo i seguenti componenti:

* Aggiungi una scheda Commerce. Questa scheda abilita le impostazioni di configurazione specifiche di Commerce aggiunte dal modello.

* Aggiungere il campo `Eligible for Commerce` alla scheda Commerce.

Il componente Interfaccia utente dati prodotto viene aggiunto automaticamente in base al modello.

### Definire il profilo di metadati

1. Accedi all’ambiente di authoring di Adobe Experience Manager.

1. Dall’area di lavoro di Adobe Experience Manager, vai all’area di lavoro Amministrazione contenuto authoring per AEM Assets facendo clic sull’icona Adobe Experience Manager.

   ![Authoring di AEM Assets](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

1. Apri gli strumenti di amministrazione selezionando l’icona a forma di martello.

   ![Amministrazione autori AEM gestisce i profili di metadati](../assets/aem-manage-metadata-profiles.png){width="600" zoomable="yes"}

1. Aprire la pagina di configurazione del profilo facendo clic su **[!UICONTROL Metadata Profiles]**.

1. **[!UICONTROL Create]** un profilo di metadati per l&#39;integrazione Commerce.

   ![Amministrazione autori AEM aggiungi profili metadati](../assets/aem-create-metadata-profile.png){width="600" zoomable="yes"}

1. Aggiungi una scheda per i metadati di Commerce.

   1. A sinistra, fare clic su **[!UICONTROL Settings]**.

   1. Fare clic su **[!UICONTROL +]** nella sezione scheda e quindi specificare **[!UICONTROL Tab Name]**, `Commerce`.

1. Aggiungi il campo `Eligible for Commerce` al modulo.

   ![L&#39;amministratore di AEM Author aggiunge campi di metadati al profilo](../assets/aem-edit-metadata-profile-fields.png){width="600" zoomable="yes"}

   * Fare clic su **[!UICONTROL Build form]**.

   * Trascina il campo `Single Line text` nel modulo.

   * Aggiungere il testo `Eligible for Commerce` per l&#39;etichetta facendo clic su **[!UICONTROL Field Label]**.

   * Nella scheda Impostazioni, aggiungere il testo dell&#39;etichetta a **Etichetta campo**.

   * Impostare il testo segnaposto su `yes`.

   * Nel campo **[!UICONTROL Map to Property]**, copia e incolla il seguente valore

     ```terminal
     ./jcr:content/metadata/commerce:isCommerce
     ```

1. Facoltativo. Per sincronizzare automaticamente le risorse Commerce approvate durante il caricamento nell&#39;ambiente AEM Assets, impostare su _[!UICONTROL Review Status]_&#x200B;il valore predefinito per il campo `Basic` nella scheda `approved`.

1. Salva l’aggiornamento.

### Applicare il profilo di metadati alla cartella di origine delle risorse di Commerce

1. Dalla pagina [!UICONTROL &#x200B; Metadata Profiles], seleziona il profilo di integrazione di Commerce.

1. Dal menu Azioni, selezionare **[!UICONTROL Apply Metadata Profiles to Folders]**.

1. Seleziona la cartella contenente le risorse Commerce.

   Crea una cartella Commerce se non esiste.

1. Fare clic su **[!UICONTROL Apply]**.

## Passaggi successivi

* [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} [Installa pacchetti Adobe Commerce](configure-commerce.md).

* [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} [Configura l&#39;integrazione dall&#39;amministratore di Commerce](setup-synchronization.md).
