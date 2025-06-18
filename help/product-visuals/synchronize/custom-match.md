---
title: Corrispondenza automatica personalizzata
description: Scopri come la corrispondenza automatica personalizzata è particolarmente utile per i commercianti con logica di corrispondenza complessa o che si affidano a un sistema di terze parti che non può popolare i metadati degli elementi visivi del prodotto in AEM Assets.
feature: CMS, Media, Integration
source-git-commit: 3ecc429003490235211a812af064d1b10d053e38
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Corrispondenza automatica personalizzata

Se la strategia di corrispondenza automatica predefinita (**Corrispondenza automatica OOTB**) non è allineata ai requisiti aziendali specifici, selezionare l&#39;opzione di corrispondenza personalizzata. Questa opzione supporta l&#39;utilizzo di [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) per sviluppare un&#39;applicazione di corrispondenza personalizzata che gestisca logiche di corrispondenza complesse o risorse provenienti da un sistema di terze parti che non possono popolare i metadati degli elementi visivi dei prodotti in AEM Assets.

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
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**Richiesta**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parametro | Tipo di dati | Descrizione |
| --- | --- | --- |
| `assetId` | Stringa | Rappresenta l’ID risorsa aggiornato |

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
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**Richiesta**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parametro | Tipo di dati | Descrizione |
| --- | --- | --- |
| `productSKU` | Stringa | Rappresenta lo SKU del prodotto aggiornato |

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

>[!TIP]
>
> Nella chiave `asset_roles`, utilizza i [ruoli di risorse Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) supportati come `thumbnail`, `image`, `small_image` e `swatch_image`.
