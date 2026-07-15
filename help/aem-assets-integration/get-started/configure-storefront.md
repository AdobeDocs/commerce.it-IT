---
title: Configurare Storefront
description: Scopri come collegare la vetrina Edge Delivery Services all’integrazione AEM Assets.
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7f901cec90291e264376e3f93e6ebaaccf7c15f0
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 0%

---

# Configurare Storefront

## Abilitare la visualizzazione di immagini prodotto da AEM Assets {#enable-product-images}

L’integrazione di AEM Assets visualizza le immagini dei prodotti AEM Assets invece di Adobe Commerce, consentendo l’ottimizzazione, il ritaglio e la distribuzione CDN avanzati.

Per abilitare l&#39;integrazione in vetrine di Commerce con tecnologia Edge Delivery Services, aggiungere il parametro `"commerce-assets-enabled": true` al file di configurazione della vetrina (`config.json`).

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

I menu a discesa di Commerce rilevano automaticamente la configurazione `commerce-assets-enabled` e regolano di conseguenza la gestione delle immagini.

Per ulteriori informazioni sull&#39;utilizzo di AEM Assets con Commerce Storefront basato su Edge Delivery Services, consulta l&#39;argomento [Integrazione di AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=it) nella documentazione di *Adobe Commerce Storefront*.

>[!TIP]
>
>Per consentire agli autori di sfogliare e inserire AEM Assets nelle pagine di contenuto statico, vedere [Connettere AEM Assets a Da.live per l&#39;authoring di contenuto statico](#connect-aem-assets-authoring).

## Connettere AEM Assets a Da.live per l’authoring di contenuti statici {#connect-aem-assets-authoring}

>[!NOTE]
>
>Questa configurazione è separata dall&#39;estensione di integrazione AEM Assets. Fornito da [Da.live](https://da.live){target="_blank"}, consente agli autori di sfogliare e inserire AEM Assets nelle pagine di contenuto statico (ad esempio, pagine di destinazione o blocchi di contenuto) tramite il pannello [!UICONTROL Library] e [!UICONTROL Content Advisor]. Le immagini dei prodotti sincronizzate tramite l&#39;integrazione di AEM Assets vengono configurate separatamente utilizzando l&#39;impostazione `commerce-assets-enabled`.

Utilizzare la procedura seguente per connettere AEM Assets a una vetrina di Document Authoring (Da.live) in modo che gli autori possano sfogliare e inserire AEM Assets da **[!UICONTROL Content Advisor]** durante la modifica di contenuto statico.

>[!NOTE]
>
>Per istruzioni di installazione dettagliate, vedi [Configurare AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} nella documentazione di Da.live e [Integrare AEM Assets durante l&#39;authoring dei contenuti per Edge Delivery Services](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank} nella documentazione di AEM Assets.

### Passaggio 1: aprire la configurazione del sito in Da.live

1. Da [Da.live](https://da.live){target=_blank}, individua e apri la vetrina.

1. Nel pannello di navigazione, seleziona l’icona **[!UICONTROL Settings]** accanto al nome del sito per aprire il foglio di calcolo di configurazione del sito.

### Passaggio 2: copia l’URL dell’archivio AEM

1. In una nuova scheda, passa a [experience.adobe.com](https://experience.adobe.com){target=_blank} e passa a **[!UICONTROL Experience Manager]**.

1. Apri Adobe Experience Manager Assets: scorri fino alla sezione **[!UICONTROL My Authoring]**, quindi seleziona **[!UICONTROL Assets]** accanto al tuo ambiente **[!UICONTROL Production]**.

1. Dalla barra degli indirizzi del browser, copia il segmento che inizia con `author` fino a `.com` incluso, ad esempio `author-p107634-e1009805.adobeaemcloud.com`.

### Passaggio 3: aggiungi l’ID dell’archivio alla configurazione

1. Per configurare il sito, torna a Da.live e seleziona **[!UICONTROL data]** nella configurazione del sito.

1. Completare il foglio di calcolo come segue:

   | Cella | Valore |
   |---|---|
   | A1 | `key` |
   | B1 | `value` |
   | A2 | `aem.repositoryId` |
   | B2 | URL copiato nel passaggio 2 |

1. Selezionare **[!UICONTROL Save]**, quindi la freccia indietro accanto al nome del sito per tornare alla directory principale del sito.

   >[!NOTE]
   >
   > L&#39;host con prefisso `author-` sfoglia le risorse dal livello di authoring. Per distribuire le risorse tramite Dynamic Media, utilizza un host con prefisso `delivery-`. Per tutte le `aem.repositoryId` opzioni, vedere [Configurazione di AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}.

### Passaggio 4: collegare AEM Assets tramite la libreria

1. Dalla directory principale del sito, selezionare la cartella **[!UICONTROL index]** per aprirla.

1. Nell&#39;editor, aprire il pannello **[!UICONTROL Library]** e selezionare **[!UICONTROL AEM Assets]**.

   Il popover **[!UICONTROL Content Advisor]** si apre e mostra le cartelle e i file di AEM Assets.

La vetrina ora è connessa ad AEM Assets. È possibile sfogliare e inserire risorse direttamente da **[!UICONTROL Content Advisor]**.

## Documentazione correlata

* [Integrazione AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=it){target=_blank} nella *documentazione di Adobe Commerce Storefront*: configurazione della vetrina e comportamento di gestione delle immagini.

* [Integra AEM Assets durante la creazione di contenuti per Edge Delivery Services](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank} nella documentazione di *AEM Assets*.

* [Configura AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} e [Utilizzo dei file multimediali](https://docs.da.live/authors/guides/adding-media){target=_blank} nella documentazione di Da.live.
