---
title: Creare eventi personalizzati
description: Scopri come creare eventi personalizzati per collegare i dati di Adobe Commerce ad altri prodotti Adobe DX.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 81fbcde11da6f5d086c2b94daeffeec60a9fdbcc
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

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

Le sostituzioni di attributi per gli eventi standard sono supportate solo per Experience Platform. I dati personalizzati non vengono inoltrati alle dashboard e ai tracciatori delle metriche di Commerce.

Per qualsiasi evento con `customContext`, l&#39;agente di raccolta sostituisce i campi di join impostati nei contesti rilevanti con i campi in `customContext`. Il caso d’uso per le sostituzioni si verifica quando uno sviluppatore desidera riutilizzare ed estendere i contesti impostati da altre parti della pagina in eventi già supportati.

### Esempi

Visualizzazione prodotto con sostituzioni pubblicata tramite Adobe Commerce Events SDK:

```javascript
mse.publish.productPageView({
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

In Experience Platform Edge:

```javascript
{
  xdm: {
    eventType: 'commerce.productViews',
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true,
        }
      ]
    },
    commerce: {
      productViews: {
        value : 1,
      }
    },
    productListItems: [{
        SKU: "1234",
        name: "leora summer pants",
        productCategories: [{
            categoryID: "cat_15",
            categoryName: "summer pants",
            categoryPath: "pants/mens/summer",
        }],
    }],
  }
}
```

Archivi basati su Luma:

Negli store basati su Luma, gli eventi di pubblicazione vengono implementati in modo nativo. Pertanto, è possibile impostare dati personalizzati estendendo `customContext`.

Ad esempio:

```javascript
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
```

Per ulteriori informazioni sulla gestione dei dati personalizzati, consulta [sostituzione evento personalizzata](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md).

>[!NOTE]
>
> La sostituzione di eventi con attributi personalizzati può influire sui rapporti predefiniti di Adobe Analytics.
