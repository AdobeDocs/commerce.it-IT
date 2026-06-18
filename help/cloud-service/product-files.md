---
title: Aggiungere file ai prodotti
description: Scopri come allegare file come PDF, manuali e fogli dati ai prodotti utilizzando gli attributi di prodotto di tipo file in [!DNL Adobe Commerce as a Cloud Service].
feature: Catalog Management, Products, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
autotag-review: '2026-06-18T16:03:48.301Z'
TQID: 'https://experienceleague.adobe.com/fFbsXGO54L1lSuQULqfP7A-BJKSYggdt7cy-GDvaSzU'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 753
ht-degree: 0%

---

# Aggiungere file ai prodotti

[!DNL Adobe Commerce as a Cloud Service] supporta un tipo di input per l&#39;attributo &quot;File&quot; [product](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/attributes-input-types){target="_blank"} che consente ai commercianti di allegare file, ad esempio PDF, manuali, certificati e fogli dati direttamente ai prodotti. I file sono memorizzati nell’archiviazione multimediale Amazon S3 e sono accessibili tramite la vetrina tramite GraphQL o tramite integrazioni tramite l’API REST.

Esistono tre modi per caricare i file negli attributi del file di prodotto:

* [Interfaccia utente amministratore](#upload-files-through-the-admin) - Carica i file manualmente nella pagina di modifica del prodotto.
* [REST API](#upload-through-the-rest-api) - Carica i file tramite l&#39;API REST utilizzando URL con prefisso S3.
* [Importazione prodotto](#upload-through-product-import) - Importa i file in blocco fornendo URL esterni in formato CSV.

## Prerequisiti

Prima di caricare i file, è necessario creare un attributo di file e assegnarlo a un set di attributi.

* [Crea un attributo di file](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} - Imposta **[!UICONTROL Catalog Input Type for Store Owner]** su **[!UICONTROL File]**.

* [Assegnare l&#39;attributo a un set di attributi](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/create/attribute-sets#create-an-attribute-set){target="_blank"}. Trascinare il nuovo attributo di file nel gruppo desiderato.

* Configura i tipi e le dimensioni di file consentiti nella configurazione di [Attributi file di prodotto](https://experienceleague.adobe.com/it/docs/commerce-admin/config/catalog/product-file-attributes).

## Caricare file tramite Admin

Dopo aver [creato un attributo di file](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} e averlo assegnato a un set di attributi, puoi caricare i file direttamente dalla pagina di modifica del prodotto.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Apri il prodotto da modificare.

1. Individuare il campo attributo file e fare clic su **[!UICONTROL Upload]** per selezionare un file.

![Pulsante Carica file nell&#39;amministratore](./assets/upload-file.png){width="600" zoomable="yes"}

1. Fare clic su **[!UICONTROL Save]**.

Per sostituire un file, elimina il file esistente e caricane uno nuovo. Il file caricato viene archiviato nell’archivio multimediale Amazon S3.

## Caricare tramite l’API REST

Utilizza il flusso URL [S3 prefirmato](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads/){target="_blank"} per caricare i file a livello di programmazione tramite l&#39;API REST. Questo processo funziona per gli attributi dei file di prodotto come per altri tipi di file multimediali, come le immagini delle categorie e i file di attributi cliente.

Il processo prevede quattro fasi:

1. Chiamare `POST V1/media/initiate-upload` con il nome file e `media_resource_type` per gli attributi del file di prodotto.
1. Utilizzare l&#39;URL prefirmato restituito per `PUT` il file direttamente in Amazon S3.
1. Chiamare `POST V1/media/finish-upload` per confermare il caricamento.
1. Assegna la chiave restituita all&#39;attributo file del prodotto tramite `PUT /V1/products/{sku}`, passando la chiave come valore dell&#39;[attributo personalizzato](https://developer.adobe.com/commerce/webapi/rest/modules/custom-attributes/).

## Carica tramite importazione prodotto

Puoi allegare i file ai prodotti in blocco utilizzando l&#39;[API di importazione](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"} o l&#39;interfaccia utente di importazione amministratore. Gli attributi del file di prodotto supportano l&#39;importazione solo da URL esterni, che seguono lo stesso approccio di [Metodo 2 per l&#39;importazione di immagini di prodotto](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/import/data-import-product-images#method-2-import-images-from-external-server){target="_blank"}. Commerce scarica il file dall’URL fornito e lo salva nell’archiviazione multimediale S3.

>[!NOTE]
>
>L&#39;importazione di file da un percorso server locale (metodo 1) non è supportata in [!DNL Adobe Commerce as a Cloud Service] perché non è disponibile l&#39;accesso diretto al file system.

### Fornisci l’URL in una colonna dedicata

Utilizza il codice attributo come intestazione di colonna CSV e l’URL completo come valore. Ad esempio, se il codice attributo è `file_upload`, il file CSV sarà simile al seguente:

```csv
sku,name,file_upload
ADB112,"My Product",https://example.com/files/manual.pdf
```

### Fornisci l&#39;URL in `additional_attributes`

In alternativa, includere l&#39;attributo file nella colonna `additional_attributes`:

```csv
sku,name,additional_attributes
ADB112,"My Product",file_upload=https://example.com/files/manual.pdf
```

In entrambi i casi, l&#39;URL deve essere accessibile al pubblico e l&#39;estensione e la dimensione del file devono essere conformi alle [limitazioni configurate](https://experienceleague.adobe.com/it/docs/commerce-admin/config/catalog/product-file-attributes){target="_blank"}.

## Recuperare i file tramite GraphQL

In [!DNL Adobe Commerce as a Cloud Service], l&#39;endpoint [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} di Catalog Service fornisce i dati del prodotto. Gli attributi del file vengono visualizzati nel campo `attributes` in `ProductView`, con `value` che contiene l&#39;URL pubblico completo del file:

```graphql
{
  products(skus: ["ADB112"]) {
    sku
    name
    attributes(roles: []) {
      name
      label
      value
    }
  }
}
```

La risposta include l’attributo file con il relativo URL pubblico:

```json
{
  "data": {
    "products": [
      {
        "sku": "ADB112",
        "name": "Example product",
        "attributes": [
          {
            "name": "file",
            "label": "FILE",
            "value": "https://<host>/media/catalog/product_file/manual.pdf",
          }
        ]
      }
    ]
  }
}
```

>[!NOTE]
>
>Questa query richiede le intestazioni `Magento-Website-Code` e `Magento-Store-View-Code`. Per ulteriori informazioni, vedere la [query sui prodotti Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}.

## Recuperare i file tramite API REST

Durante il recupero di un prodotto tramite l&#39;[API REST](https://developer.adobe.com/commerce/webapi/reference/rest/saas/){target="_blank"} (`GET /V1/products/{sku}`), gli attributi del file vengono visualizzati nell&#39;array `custom_attributes` con il nome file come valore:

```json
{
  "custom_attributes": [
    {
      "attribute_code": "file_upload",
      "value": "manual_7aa0b2d63f6d3dbf.pdf"
    }
  ]
}
```
