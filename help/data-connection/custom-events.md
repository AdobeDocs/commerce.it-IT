---
title: Creare eventi personalizzati
description: Scopri come creare eventi personalizzati per collegare i dati di Adobe Commerce ad altri prodotti Adobe DX.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 25d796da49406216f26d12e3b1be01902dfe9302
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Creare eventi personalizzati

Puoi estendere la [piattaforma di gestione eventi](events.md) creando i tuoi eventi storefront per raccogliere dati specifici per il tuo settore. Quando crei e configuri un evento personalizzato, questo viene inviato all&#39;[Agente di raccolta eventi di Adobe Commerce](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector).

## Gestire eventi personalizzati

Gli eventi personalizzati sono supportati solo per Adobe Experience Platform. I dati personalizzati non vengono inoltrati alle dashboard di Adobe Commerce e ai tracker di metriche.

Per qualsiasi evento `custom`, l&#39;agente di raccolta:

- Aggiunge `identityMap` con `ECID` come identità primaria
- Include `email` in `identityMap` come identità secondaria _se_ `personalEmail.address` è impostato nell&#39;evento
- Racchiude l&#39;evento completo all&#39;interno di un oggetto `xdm` prima di inoltrarlo ad Edge

Esempio:

Evento personalizzato pubblicato tramite Adobe Commerce Events SDK:

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

In Experience Platform Edge:

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> L’utilizzo di eventi personalizzati può influire sui rapporti predefiniti di Adobe Analytics.

## Gestire le sostituzioni di eventi (attributi personalizzati)

Per qualsiasi set di eventi con `customContext`, l&#39;agente di raccolta sostituisce o estende i campi nel payload dell&#39;evento dai campi in `custom context`. Il caso d’uso per le sostituzioni si verifica quando uno sviluppatore desidera riutilizzare ed estendere i contesti impostati da altre parti della pagina in eventi già supportati.

Le sostituzioni degli eventi sono applicabili solo quando si inoltra ad Experience Platform. Non vengono applicati agli eventi di analisi di Adobe Commerce e Sensei. L&#39;agente di raccolta eventi di Adobe Commerce [README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md) fornisce informazioni aggiuntive.

>[!NOTE]
>
>Durante l&#39;aumento di `productListItems` con attributi personalizzati nei payload dell&#39;evento Experience Platform, abbina i prodotti utilizzando lo SKU. Questo requisito non si applica a `product-page-view` eventi.

### Utilizzo

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### Esempio 1 - aggiunta di `productCategories`

```javascript
magentoStorefrontEvents.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

### Esempio 2: aggiunta di contesto personalizzato prima della pubblicazione dell’evento

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      productCategories: [
        {
          categoryID: "cat_15",
          categoryName: "summer pants",
          categoryPath: "pants/mens/summer",
        },
      ],
    },
  ],
});

mse.publish.productPageView();
```

### Esempio 3: il contesto personalizzato impostato nell’editore sovrascrive il contesto personalizzato precedentemente impostato in Adobe Client Data Layer.

In questo esempio, l&#39;evento `pageView` avrà **Nome pagina personalizzato 2** nel campo `web.webPageDetails.name`.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### Esempio 4: aggiunta di contesto personalizzato a `productListItems` con eventi con più prodotti

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

>[!NOTE]
>
> La sostituzione di eventi con attributi personalizzati può influire sui rapporti predefiniti di Adobe Analytics.
