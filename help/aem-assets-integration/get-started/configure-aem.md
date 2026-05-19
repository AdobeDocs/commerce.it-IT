---
title: Configurare il progetto AEM Assets per supportare i metadati di Commerce
description: Abilita la sincronizzazione perfetta delle risorse tra Adobe Commerce e AEM Assets aggiungendo i metadati richiesti per l’integrazione.
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
TQID: https://experienceleague.adobe.com/QPlM-eeRjJ0gwmpGO4SSYR4PLtL97O-NeozWorDWtv0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 5dc61e0351e338c4d184d7d882decff49b13a12b
workflow-type: tm+mt
source-wordcount: 1708
ht-degree: 1%

---

# Configurare il progetto AEM Assets per supportare i metadati di Commerce

Quando si utilizza AEM Assets as a Digital Asset Management System (DAM) for Commerce, l&#39;installazione del pacchetto `assets-commerce` consente di gestire immagini e video per i prodotti Commerce dall&#39;ambiente di authoring AEM.

Completa i seguenti passaggi per configurare il progetto AEM Assets con il codice pacchetto e i metadati richiesti per gestire le risorse Commerce dall’ambiente di authoring AEM:

1. [Informazioni sul contenuto del pacchetto `assets-commerce`](#aem-commerce-assets-commerce-package-contents)

1. [Completa i passaggi di installazione per configurare il progetto AEM Assets per il supporto dei metadati Commerce](#step-1-install-the-assets-commerce-package)

## contenuti del pacchetto AEM Commerce assets-commerce

Adobe fornisce un codice pacchetto AEM Commerce `assets-commerce` per aggiungere risorse dello spazio dei nomi e dello schema dei metadati di Commerce alla configurazione dell&#39;ambiente Experience Manager Assets as a Cloud Service.

Questo codice di pacchetto aggiunge le seguenti risorse all’ambiente di authoring AEM Assets:

* Uno [spazio dei nomi personalizzato](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json), `Commerce` per identificare le proprietà relative a Commerce.

   * Tipo di metadati personalizzato `commerce:isCommerce` con etichetta `Eligible for Commerce` per assegnare tag alle risorse Commerce associate a un progetto Adobe Commerce.

   * Un tipo di metadati personalizzato `commerce:skus` e un componente dell&#39;interfaccia utente corrispondente per aggiungere una proprietà **[!UICONTROL Product Data]**. I dati prodotto includono le proprietà dei metadati per associare una risorsa Commerce agli SKU di prodotto.

     ![Controllo interfaccia utente dati prodotto personalizzato](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Attributi del tipo di metadati personalizzati `commerce:roles` e `commerce:positions` per mostrare come viene visualizzata la risorsa in Commerce.

   * Metadati multifield di testo alternativo (_[!UICONTROL Alt texts]_) che consentono agli editor di immettere testo alternativo con chiave per il codice di visualizzazione dell&#39;archivio di Commerce. Questo non cambia il modo in cui le immagini del prodotto vengono assegnate o definite nell’ambito del catalogo. Vedi [Testo alternativo nei metadati di AEM Assets](#localized-alt-text-in-aem-assets-metadata).

* Modulo schema metadati con scheda Commerce che include i campi `Eligible for Commerce` e `Product Data` per l&#39;assegnazione di tag alle risorse Commerce. Il modulo fornisce inoltre opzioni per mostrare o nascondere i campi `roles` e `position` dall&#39;interfaccia utente di AEM Assets.

  ![Scheda Commerce per modulo schema metadati AEM Assets](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* [Esempio di risorsa con tag e approvata da Commerce](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg` per supportare la sincronizzazione iniziale delle risorse. Solo le risorse Commerce approvate possono essere sincronizzate da AEM Assets ad Adobe Commerce.

>[!NOTE]
>
> Per ulteriori informazioni sul **codice pacchetto AEM Commerce**, vedere la pagina [leggimi](https://github.com/ankumalh/assets-commerce).

## Testo alternativo nei metadati di AEM Assets

Il multifield _[!UICONTROL Alt texts]_&#x200B;è disponibile nell&#39;editor metadati risorse di AEM Assets nella scheda **[!UICONTROL Commerce]**&#x200B;quando si modifica un&#39;immagine idonea.

>[!IMPORTANT]
>
> Il comportamento di visualizzazione per punto vendita si applica solo al testo alternativo. L’integrazione di AEM Assets non sincronizza diverse immagini di prodotto per ogni vista store di Adobe Commerce. Le immagini dei prodotti di AEM continuano a essere sincronizzate con Commerce con lo stesso comportamento di assegnazione della galleria utilizzato prima di questa versione.

Il campo multiplo contiene una riga per ogni visualizzazione store di Commerce. Ogni riga dispone di due input:

* **[!UICONTROL Store View Code]** — Identificatore della visualizzazione archivio (ad esempio `default` o `en_US`).

* **[!UICONTROL Alt Text]** — Testo alternativo per la visualizzazione archivio, limitato a 255 caratteri.

Selezionare **[!UICONTROL Add]** per aggiungere altre righe per altre visualizzazioni dello store. Per rimuovere una riga, selezionare l&#39;icona **[!UICONTROL Delete]** sulla riga per rimuoverla.

![Testi Alt con più campi con input Codice visualizzazione archivio e Testo Alt](../assets/commerce-metadata-alt-texts-multifield.png){width="600" zoomable="yes"}

Quando si salva, la convalida lato client blocca l&#39;invio se una riga presenta un _[!UICONTROL Store View Code]_&#x200B;vuoto o se due righe utilizzano lo stesso codice di visualizzazione archivio (senza distinzione maiuscole/minuscole).

Le voci di testo alternative vengono mantenute nei metadati delle risorse JCR come due proprietà `String[]` allineate all&#39;indice:

* `commerce:altTextStoreViews`: memorizzare il codice di visualizzazione per ogni riga.
* `commerce:altTextValues`: Corrispondenza del testo alternativo nello stesso indice di ogni voce in `commerce:altTextStoreViews`.

Quando queste risorse vengono sincronizzate con Adobe Commerce, nella galleria di supporti del prodotto viene scritto del testo alternativo per la visualizzazione del negozio per i codici di visualizzazione del negozio corrispondenti. La mappatura immagine sottostante è invariata.

## Prerequisiti

Per distribuire il codice pacchetto `assets-commerce` nell&#39;ambiente AEM Assets as a Cloud Service AEM sono necessarie le risorse e le autorizzazioni seguenti:

* [Accesso al programma e agli ambienti AEM Assets Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo) con i ruoli Responsabile del programma e Responsabile della distribuzione.

* [ambiente di sviluppo AEM locale](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) e familiarità con il processo di sviluppo locale AEM.

* Comprendere la struttura del progetto [AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) e come distribuire pacchetti di contenuti personalizzati con Cloud Manager.

* L&#39;**ID organizzazione IMS** per l&#39;istanza di Commerce. Sia l’istanza di Commerce che l’ambiente di authoring di AEM Assets devono essere nella stessa organizzazione IMS.

* Per abilitare [Dynamic Media con funzionalità OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis):

>[!BEGINTABS]

>[!TAB Visualizzazioni prodotto]

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} Dynamic Media con funzionalità OpenAPI è self-service per gli elementi visivi di prodotto basati su AEM Assets.

1. Passa al Cloud Manager.

1. Seleziona l’ambiente desiderato.

1. Abilita **Dynamic Media con funzionalità OpenAPI**.

   Se il pulsante **Dynamic Media con funzionalità OpenAPI** non è attivo, aprire un ticket di supporto.

>[!TAB AEM Assets]

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} In AEM as a Cloud Service, invia un ticket di supporto Adobe con le seguenti informazioni:

* Title: Abilita Dynamic Media OpenAPI per integrare completamente Adobe Commerce con AEM Assets

   * Contenuto del ticket di supporto:

      * **[!UICONTROL AEM Program ID]**
      * **[!UICONTROL Adobe Commerce URL]**
      * **[!UICONTROL AEM Environment ID]**
      * **[!UICONTROL IMS Org ID]**

Dopo aver inviato il ticket di supporto, Adobe abilita Dynamic Media con funzionalità OpenAPI nell’ambiente Cloud Services e condiviso i dettagli, come l’ID client IMS, per consentire all’utente di procedere con l’integrazione.

>[!ENDTABS]

## Passaggio 1: installare il pacchetto assets-commerce

1. Passa a AEM Cloud Manager, seleziona un programma e [crea ambienti di produzione e di staging](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments#creating-environments) che desideri integrare con Adobe Commerce.

1. Configura una [pipeline di distribuzione](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/pipeline-setup#create-front-end-pipeline) oppure verifica che la pipeline possa distribuire modifiche all&#39;ambiente selezionato.

1. [Clona l&#39;archivio Git gestito da Adobe](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/retrieve-access#repo-access) per il programma selezionato.

1. Da GitHub scaricare il codice del pacchetto dall&#39;[archivio Commerce di AEM Assets](https://github.com/ankumalh/assets-commerce).

1. Dall&#39;[ambiente di sviluppo AEM locale](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview), copia manualmente il codice scaricato nell&#39;archivio gestito Adobe esistente.

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

Se riscontri altri problemi, crea un [ticket di supporto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) o contatta il rappresentante commerciale per l&#39;integrazione di AEM Assets.

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

1. Facoltativo. Per sincronizzare automaticamente le risorse Commerce approvate durante il caricamento nell&#39;ambiente AEM Assets, impostare su `approved` il valore predefinito per il campo _[!UICONTROL Review Status]_&#x200B;nella scheda `Basic`.

1. Salva l’aggiornamento.

### Applicare il profilo di metadati alla cartella di origine delle risorse di Commerce

1. Dalla pagina [!UICONTROL &#x200B; Metadata Profiles], seleziona il profilo di integrazione di Commerce.

1. Dal menu Azioni, selezionare **[!UICONTROL Apply Metadata Profiles to Folders]**.

1. Seleziona la cartella contenente le risorse Commerce.

   Crea una cartella Commerce se non esiste.

1. Fare clic su **[!UICONTROL Apply]**.

## Passaggi successivi

* [!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} [Installa pacchetti Adobe Commerce](configure-commerce.md).

* [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} [Configura l&#39;integrazione dall&#39;amministratore di Commerce](setup-synchronization.md).
