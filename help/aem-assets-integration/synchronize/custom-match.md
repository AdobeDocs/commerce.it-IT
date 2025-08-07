---
title: Corrispondenza automatica personalizzata
description: Scopri come la corrispondenza automatica personalizzata è particolarmente utile per i commercianti con logica di corrispondenza complessa o che si affidano a un sistema di terze parti che non può popolare i metadati in AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: ff6affa5bcc4111e14054f3f6b3ce970619ca295
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Corrispondenza automatica personalizzata

Se la strategia di corrispondenza automatica predefinita (**Corrispondenza automatica OOTB**) non è allineata ai requisiti aziendali specifici, selezionare l&#39;opzione di corrispondenza personalizzata. Questa opzione supporta l&#39;utilizzo di [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) per sviluppare un&#39;applicazione di corrispondenza personalizzata che gestisca logiche di corrispondenza complesse o risorse provenienti da un sistema di terze parti che non possono popolare i metadati in AEM Assets.

## Configurare la corrispondenza automatica personalizzata

1. Dall&#39;amministratore di Commerce, passare a **[!UICONTROL Store]** > Configurazione > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Selezionare **[!UICONTROL Custom Matcher]** come regola corrispondente.

1. Quando selezioni questa regola corrispondente, l&#39;amministratore visualizza campi aggiuntivi per configurare gli **endpoint** e i **parametri di autenticazione** necessari per la logica di corrispondenza personalizzata.

## Endpoint API di corrispondenza personalizzati

Quando si crea un&#39;applicazione di corrispondenza personalizzata utilizzando [App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, l&#39;applicazione deve esporre i seguenti endpoint:

* Endpoint **da risorsa App Builder all&#39;URL prodotto**
* Endpoint **da prodotto App Builder a URL risorsa**

### Endpoint da risorsa App Builder a URL prodotto

Questo endpoint recupera l’elenco di SKU associati a una determinata risorsa:

#### Esempio di utilizzo

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Richiesta**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parametro | Tipo di dati | Descrizione |
| --- | --- | --- |
| `assetId` | Stringa | Rappresenta l’ID risorsa aggiornato |
| `eventData` | Stringa | Restituisce il payload di dati associato a `assetId` |

**Risposta**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### Endpoint &quot;product to asset URL&quot; di App Builder

Questo endpoint recupera l’elenco delle risorse associate a un determinato SKU:

#### Esempio di utilizzo

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Richiesta**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parametro | Tipo di dati | Descrizione |
| --- | --- | --- |
| `productSKU` | Stringa | Rappresenta lo SKU del prodotto aggiornato. |
| `asset_matches` | Stringa | Restituisce tutte le risorse associate a un `productSku` specifico. |

Il parametro `asset_matches` contiene i seguenti attributi:

| Attributo | Tipo di dati | Descrizione |
| --- | --- | --- |
| `asset_id` | Stringa | Rappresenta l’ID risorsa aggiornato. |
| `asset_roles` | Stringa | Restituisce tutti i ruoli di risorse disponibili. Utilizza i [ruoli di risorse Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) supportati come `thumbnail`, `image`, `small_image` e `swatch_image`. |
| `asset_format` | Stringa | Fornisce i formati disponibili per la risorsa. I valori possibili sono `image` e `video`. |
| `asset_position` | Stringa | Mostra la posizione della risorsa. |

**Risposta**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```
