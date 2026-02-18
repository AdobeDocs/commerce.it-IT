---
title: Corrispondenza automatica personalizzata
description: Scopri come la corrispondenza automatica personalizzata è particolarmente utile per i commercianti con logica di corrispondenza complessa o che si affidano a un sistema di terze parti che non può popolare i metadati in AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: 6e8d266aeaec4d47b82b0779dfc3786ccaa7d83a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Corrispondenza automatica personalizzata

Se la strategia di corrispondenza automatica predefinita (**Corrispondenza automatica OOTB**) non è allineata ai requisiti aziendali specifici, selezionare l&#39;opzione di corrispondenza personalizzata. Questa opzione supporta l&#39;utilizzo di [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) per sviluppare un&#39;applicazione di corrispondenza personalizzata che gestisca logiche di corrispondenza complesse o risorse provenienti da un sistema di terze parti che non possono popolare i metadati in AEM Assets.

## Configurare la corrispondenza automatica personalizzata

1. Dall&#39;amministratore di Commerce, passare a **[!UICONTROL Store]** > Configurazione > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Selezionare **[!UICONTROL Custom Matcher]** come regola corrispondente.

1. Quando selezioni questa regola corrispondente, l&#39;amministratore visualizza campi aggiuntivi per configurare gli **endpoint** e i **parametri di autenticazione** necessari per la logica di corrispondenza personalizzata.

### workspace.json

Il campo **[!UICONTROL Adobe I/O Workspace Configuration]** consente di configurare in modo semplificato la corrispondenza personalizzata importando il file di configurazione di App Builder `workspace.json`.

È possibile scaricare il file `workspace.json` da [Adobe Developer Console](https://developer.adobe.com/console). Il file contiene tutte le credenziali e i dettagli di configurazione per l’area di lavoro App Builder.

+++Esempio `workspace.json`

```json
{
  "project": {
    "id": "project_id",
    "name": "project_name",
    "title": "title_name",
    "org": {
      "id": "id",
      "name": "Organization_name",
      "ims_org_id": "ims_id"
    },
    "workspace": {
      "id": "workspace_id",
      "name": "workspace_name_id",
      "title": "workspace_title_id",
      "action_url": "https://action_url.net",
      "app_url": "https://app_url.net",
      "details": {
        "credentials": [
          {
            "id": "credential_id",
            "name": "credential_name_id",
            "integration_type": "oauth_server_to_server",
            "oauth_server_to_server": {
              "client_id": "client_id",
              "client_secrets": ["secret"],
              "technical_account_email": "xx@technical_account_email.com",
              "technical_account_id": "technical_account_id",
              "scopes": [
                "AdobeID",
                "openid",
                "read_organizations",
                "additional_info.projectedProductContext",
                "additional_info.roles",
                "adobeio_api",
                "read_client_secret",
                "manage_client_secrets"
              ]
            }
          }
        ],
        "services": [
          {
            "code": "AdobeIOManagementAPISDK",
            "name": "I/O Management API"
          }
        ],
        "runtime": {
          "namespaces": [
            {
              "name": "namespace_name",
              "auth": "example_auth"
            }
          ]
        },
        "events": {
          "registrations": []
        },
        "mesh": {}
      }
    }
  }
}
```

+++

1. Trascina il file `workspace.json` dal progetto App Builder nel campo **[!UICONTROL Adobe I/O Workspace Configuration]**. In alternativa, è possibile fare clic su per sfogliare e selezionare il file.

![Configurazione Workspace](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. Il sistema automaticamente:

   * Convalida la struttura JSON
   * Estrae e popola le credenziali OAuth
   * Recupera le azioni di runtime disponibili per l’area di lavoro
   * Popola le opzioni a discesa per i campi **[!UICONTROL Product to Asset URL]** e **[!UICONTROL Asset to Product URL]**

1. Seleziona le azioni di runtime appropriate dai menu a discesa per ciascun flusso.

1. Fare clic su **[!UICONTROL Save Config]**.

## Endpoint API di corrispondenza personalizzati

Quando si crea un&#39;applicazione di corrispondenza personalizzata utilizzando [App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, l&#39;applicazione deve esporre i seguenti endpoint:

* Endpoint **da risorsa App Builder all&#39;URL prodotto**
* Endpoint **da prodotto App Builder a URL risorsa**

### Endpoint da risorsa App Builder a URL prodotto

Questo endpoint recupera l’elenco di SKU associati a una determinata risorsa:

#### Esempio di utilizzo

```javascript
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

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**Richiesta**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parametro | Tipo di dati | Descrizione |
| --- | --- | --- |
| `assetId` | Stringa | Rappresenta l’ID risorsa aggiornato. |
| `eventData` | Stringa | Restituisce il payload di dati associato all’ID risorsa. |

**Risposta**

```json
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail", "image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ],
  "skip": false
}
```

| Parametro | Tipo di dati | Descrizione |
| --- | --- | --- |
| `asset_id` | Stringa | ID risorsa di cui viene trovata una corrispondenza. |
| `product_matches` | Array | Elenco di prodotti associati alla risorsa. |
| `skip` | Booleano | (Facoltativo) Quando `true`, il motore di regole ignora la sincronizzazione per questa risorsa (nessun aggiornamento della mappatura del prodotto). Se `false` o viene omesso, viene eseguita l&#39;elaborazione normale. Vedi [Ignora elaborazione sincronizzazione](#skip-sync-processing). |

### Endpoint &quot;product to asset URL&quot; di App Builder

Questo endpoint recupera l’elenco delle risorse associate a un determinato SKU:

#### Esempio di utilizzo

```javascript
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**Richiesta**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parametro | Tipo di dati | Descrizione |
| --- | --- | --- |
| `productSKU` | Stringa | Rappresenta lo SKU del prodotto aggiornato. |
| `eventData` | Stringa | Restituisce il payload di dati associato allo SKU del prodotto. |

**Risposta**

```json
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail", "image"],
      "asset_position": 1,
      "asset_format": "image"
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"],
      "asset_position": 2,
      "asset_format": "image"
    }
  ],
  "skip": false
}
```

| Parametro | Tipo di dati | Descrizione |
| --- | --- | --- |
| `product_sku` | Stringa | SKU prodotto corrispondente. |
| `asset_matches` | Array | Elenco di risorse associate al prodotto. |
| `skip` | Booleano | (Facoltativo) Quando `true`, il motore di regole ignora la sincronizzazione per questo prodotto (nessun aggiornamento di mappatura risorse). Se `false` o viene omesso, viene eseguita l&#39;elaborazione normale. Vedi [Ignora elaborazione sincronizzazione](#skip-sync-processing). |

Il parametro `asset_matches` contiene i seguenti attributi:

| Attributo | Tipo di dati | Descrizione |
| --- | --- | --- |
| `asset_id` | Stringa | ID risorsa. |
| `asset_roles` | Array | Ruoli risorsa. Utilizza i [ruoli di risorse Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) supportati come `thumbnail`, `image`, `small_image` e `swatch_image`. |
| `asset_format` | Stringa | Il formato della risorsa. I valori possibili sono `image` e `video`. |
| `asset_position` | Numero | Posizione della risorsa nella galleria di prodotti. |

## Ignora elaborazione sincronizzazione

Il parametro `skip` consente alla corrispondenza personalizzata di ignorare l&#39;elaborazione della sincronizzazione per risorse o prodotti specifici.

Quando l&#39;applicazione App Builder restituisce `"skip": true` nella risposta, il motore di regole non invia richieste di aggiornamento o rimozione API a Commerce per quella risorsa o quel prodotto. Questa ottimizzazione riduce le chiamate API non necessarie e migliora le prestazioni.
