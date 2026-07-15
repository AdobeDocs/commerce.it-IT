---
title: Metadati Commerce in AEM Assets
description: Scopri lo spazio dei nomi di Commerce, lo schema dei metadati e il testo alternativo aggiunto dall’integrazione AEM Assets all’ambiente di authoring AEM Assets.
feature: CMS, Media, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 749
ht-degree: 0%

---

# Metadati Commerce in AEM Assets

I metadati di Commerce sono il contratto tra AEM Assets e Commerce. Indica a Commerce quali risorse sono per Commerce, a quali prodotti appartengono e come devono essere utilizzate o visualizzate. Questi metadati consentono all’integrazione di AEM Assets di mappare e sincronizzare correttamente i file di risorse.

I metadati di Commerce offrono le seguenti funzionalità:

* **Contrassegna una risorsa come idonea per Commerce** tramite il campo `commerce:isCommerce`.
* **Associa una risorsa a uno o più SKU di prodotto** tramite il campo `commerce:skus`.
* **Definire la modalità di visualizzazione della risorsa in Commerce** tramite i campi `commerce:roles` e `commerce:positions`.
* **Aggiungi testo alternativo specifico per Commerce codificato dalla visualizzazione archivio** tramite i campi `commerce:altTextStoreViews` e `commerce:altTextValues`.
* **Esporre questi campi nell&#39;interfaccia utente delle proprietà di AEM Assets** tramite una scheda **[!UICONTROL Commerce]** e un modulo schema.

>[!IMPORTANT]
>
>La funzionalità **Testo alternativo specifico per Commerce** non è ancora disponibile tramite [onboarding self-service](get-started/configure-aem.md#enable-aem-commerce-self-service). Attualmente viene fornito solo quando distribuisci il pacchetto di codice personalizzato `assets-commerce` (vedi [Installare il pacchetto assets-commerce manualmente](get-started/configure-aem.md#install-the-assets-commerce-package-manually)). Il supporto nativo è pianificato per la prossima versione di AEM.

Per configurare queste risorse nel progetto AEM, vedi [Configurare il progetto AEM Assets](get-started/configure-aem.md). Il resto di questo argomento descrive come vengono forniti i metadati.

## contenuti del pacchetto AEM Commerce assets-commerce

Adobe fornisce il pacchetto di codice AEM Commerce `assets-commerce` per aggiungere spazi dei nomi Commerce e risorse schema metadati alla configurazione di Experience Manager Assets as a Cloud Service.

Questo codice di pacchetto aggiunge le seguenti risorse all’ambiente di authoring AEM Assets:

* Uno [spazio dei nomi personalizzato](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json), `Commerce` per identificare le proprietà relative a Commerce.

   * Tipo di metadati personalizzato `commerce:isCommerce` con etichetta `Eligible for Commerce` per assegnare tag alle risorse Commerce associate a un progetto Adobe Commerce.

   * Un tipo di metadati personalizzato `commerce:skus` e un componente dell&#39;interfaccia utente corrispondente per aggiungere una proprietà **[!UICONTROL Product Data]**. I dati prodotto includono le proprietà dei metadati per associare una risorsa Commerce agli SKU di prodotto.

     ![Controllo interfaccia utente dati prodotto personalizzato](assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Attributi del tipo di metadati personalizzato `commerce:roles` e `commerce:positions` che mostrano come la risorsa viene visualizzata in Commerce.

   * Metadati multifield di testo alternativo (_[!UICONTROL Alt texts]_) che consentono agli editor di immettere testo alternativo per ogni codice di visualizzazione dell&#39;archivio Commerce. Il multifield persiste in due proprietà `String[]` allineate all&#39;indice:

      * `commerce:altTextStoreViews` — memorizza il codice di visualizzazione per ogni riga.
      * `commerce:altTextValues` — testo alt corrispondente nello stesso indice di ogni voce in `commerce:altTextStoreViews`.

     Le implementazioni di App Builder che utilizzano una [corrispondenza esterna](synchronize/custom-match.md){target=_blank} possono intercettare queste proprietà durante la trasformazione dei payload delle risorse. Questo non cambia il modo in cui le immagini del prodotto vengono assegnate o definite nell’ambito del catalogo. Vedi [Testo alternativo localizzato nei metadati di AEM Assets](#localized-alt-text-in-aem-assets-metadata).

* Modulo schema metadati con scheda Commerce che include i campi `Eligible for Commerce` e `Product Data` per l&#39;assegnazione di tag alle risorse Commerce. Il modulo fornisce inoltre opzioni per mostrare o nascondere i campi `roles` e `position` dall&#39;interfaccia utente di AEM Assets.

  ![Scheda Commerce per modulo schema metadati AEM Assets](assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* [Esempio di risorsa con tag e approvata da Commerce](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg` per supportare la sincronizzazione iniziale delle risorse. Solo le risorse Commerce approvate possono essere sincronizzate da AEM Assets ad Adobe Commerce.

>[!NOTE]
>
> Per ulteriori informazioni sul **codice pacchetto AEM Commerce**, consulta la pagina [readme](https://github.com/ankumalh/assets-commerce) su GitHub.

## Testo alternativo localizzato nei metadati di AEM Assets

Il multifield _[!UICONTROL Alt texts]_&#x200B;è disponibile nell&#39;editor metadati risorse di AEM Assets nella scheda **[!UICONTROL Commerce]**&#x200B;quando si modifica un&#39;immagine idonea.

>[!IMPORTANT]
>
> Il comportamento di visualizzazione per punto vendita si applica solo al testo alternativo. L’integrazione di AEM Assets non sincronizza diverse immagini di prodotto per ogni vista store di Adobe Commerce. Le immagini dei prodotti di AEM continuano a essere sincronizzate con Commerce con lo stesso comportamento di assegnazione della galleria utilizzato prima di questa versione.

Il campo multiplo contiene una riga per ogni visualizzazione store di Commerce. Ogni riga dispone di due input:

* **[!UICONTROL Store View Code]** — Identificatore della visualizzazione archivio (ad esempio `default` o `en_US`).

* **[!UICONTROL Alt Text]** — Testo alternativo per la visualizzazione archivio, limitato a 255 caratteri.

Selezionare **[!UICONTROL Add]** per aggiungere altre righe per altre visualizzazioni dello store. Per rimuovere una riga, selezionare l&#39;icona **[!UICONTROL Delete]** sulla riga per rimuoverla.

![Testi Alt con più campi con input Codice visualizzazione archivio e Testo Alt](assets/commerce-metadata-alt-texts-multifield.png){width="600" zoomable="yes"}

Quando si salva, la convalida lato client blocca l&#39;invio se una riga presenta un _[!UICONTROL Store View Code]_&#x200B;vuoto o se due righe utilizzano lo stesso codice di visualizzazione archivio (senza distinzione maiuscole/minuscole).

Le voci di testo alternative vengono mantenute nei metadati delle risorse JCR come due proprietà `String[]` allineate all&#39;indice:

* `commerce:altTextStoreViews`: memorizzare il codice di visualizzazione per ogni riga.
* `commerce:altTextValues`: Corrispondenza del testo alternativo nello stesso indice di ogni voce in `commerce:altTextStoreViews`.

Quando queste risorse vengono sincronizzate con Adobe Commerce, nella galleria di supporti del prodotto viene scritto del testo alternativo per la visualizzazione del negozio per i codici di visualizzazione del negozio corrispondenti. La mappatura immagine sottostante è invariata.
