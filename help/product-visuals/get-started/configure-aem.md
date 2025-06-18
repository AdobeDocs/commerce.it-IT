---
title: Configurare il progetto AEM Assets
description: Sincronizzazione perfetta delle risorse tra Adobe Commerce e AEM Assets grazie all’aggiunta dei metadati richiesti per l’integrazione di Product Visuals.
feature: CMS, Media, Integration
source-git-commit: ff4dd64c810fd4d2d18c9153be4bde9a1e971fe0
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---


# Configurare il progetto AEM Assets per supportare i metadati di Commerce

Per utilizzare i componenti visivi prodotto per gestire i file di risorse Commerce in AEM Assets, completa i passaggi seguenti per configurare il progetto AEM Assets con il codice standard e i metadati richiesti per gestire le risorse Commerce dall’ambiente di authoring AEM.

* **Passaggio 1:** installa un modello di progetto AEM con il codice standard per aggiungere lo spazio dei nomi Commerce e le risorse dello schema metadati alla configurazione dell&#39;ambiente Experience Manager Assets as a Cloud Service.
* **Passaggio 2:** Configura il profilo metadati da applicare ai file di risorse Commerce

## Aggiungi il codice boilerplate al progetto AEM

Adobe fornisce una piattaforma standard di AEM Commerce, `assets-commerce`, per aggiungere lo spazio dei nomi e le risorse dello schema dei metadati Commerce alla configurazione dell&#39;ambiente Experience Manager Assets as a Cloud Service. Distribuisci questo codice nell&#39;ambiente come pacchetto **Maven**. Quindi, configura i metadati Commerce nell’ambiente di authoring AEM Assets per completare la configurazione.

La boilerplate aggiunge le seguenti risorse all’ambiente di authoring AEM Assets:

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
> Consulta la pagina [leggimi](https://github.com/ankumalh/assets-commerce) per ulteriori informazioni sulla **targhetta Commerce di AEM**.

### Prerequisiti

Per distribuire il pacchetto `commerce-assets` nell&#39;ambiente AEM Assets as a Cloud Service AEM sono necessarie le risorse e le autorizzazioni seguenti:

* [Accesso al programma e agli ambienti AEM Assets Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo) con i ruoli Responsabile del programma e Responsabile della distribuzione.

* [ambiente di sviluppo AEM locale](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) e familiarità con il processo di sviluppo locale AEM.

* Comprendere la struttura del progetto [AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) e come distribuire pacchetti di contenuti personalizzati con Cloud Manager.

### Installa il pacchetto `commerce-assets`

1. Se necessario, crea ambienti di produzione e staging per il progetto AEM Assets da AEM Cloud Manager.

1. Se necessario, configura una pipeline di distribuzione.

1. Da GitHub, scarica il codice dalla [piastra di avvio di AEM Commerce](https://github.com/ankumalh/assets-commerce).

1. Dal [ambiente di sviluppo AEM locale](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview), installa il codice personalizzato nella configurazione dell&#39;ambiente AEM Assets come pacchetto Maven oppure copiando manualmente il codice nella configurazione del progetto esistente.

1. Apporta le modifiche e invia il ramo di sviluppo locale all’archivio Git di Cloud Manager.

1. Da AEM Cloud Manager, [distribuisci il codice per aggiornare l&#39;ambiente AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager).

## Facoltativo. Configurare un profilo di metadati

Nell’ambiente di authoring di AEM Assets, imposta i valori predefiniti per i metadati delle risorse Commerce creando un profilo di metadati. Quindi, applica il nuovo profilo alle cartelle di AEM Asset per utilizzare automaticamente queste impostazioni predefinite. Questa configurazione semplifica l’elaborazione delle risorse riducendo i passaggi manuali.

Quando configuri il profilo di metadati, devi configurare solo i seguenti componenti:

* Aggiungi una scheda Commerce. Questa scheda abilita le impostazioni di configurazione specifiche di Commerce aggiunte dal modello
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

1. Facoltativo. Per sincronizzare automaticamente le risorse Commerce approvate durante il caricamento nell&#39;ambiente AEM Assets, impostare su `approved` il valore predefinito per il campo _[!UICONTROL Review Status]_&#x200B;nella scheda `Basic`.

1. Salva l’aggiornamento.

#### Applicare il profilo di metadati alla cartella di origine delle risorse di Commerce

1. Dalla pagina [!UICONTROL &#x200B; Metadata Profiles], seleziona il profilo di integrazione di Commerce.

1. Dal menu Azioni, selezionare **[!UICONTROL Apply Metadata Profiles to Folders]**.

1. Seleziona la cartella contenente le risorse Commerce.

   Crea una cartella Commerce se non esiste.

1. Fare clic su **[!UICONTROL Apply]**.

## Passaggio successivo

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} [Installa pacchetti Adobe Commerce](configure-commerce.md)
