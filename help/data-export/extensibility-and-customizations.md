---
title: Estendere e personalizzare i dati del feed di esportazione dei dati SaaS
description: Scopri come estendere e personalizzare i dati del feed  [!DNL SaaS Data Export] .
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Estendere e personalizzare i dati del feed di esportazione dei dati SaaS

L&#39;estensione [!DNL Commerce Data Export] consente di esportare dati dall&#39;applicazione [!DNL Commerce] a servizi Commerce quali Live Search, Catalog Service e Product Recommendations. Se necessario, puoi estendere e personalizzare i dati del feed per includere dati di attributi aggiuntivi o modificare i dati raccolti.

Dopo aver aggiunto i dati degli attributi, è possibile accedervi dal campo [attributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type) nello schema di GraphQL per il servizio vetrina.

>[!NOTE]
>
>L’aggiunta o la modifica di dati di feed può influire sulle prestazioni e sulla logica di elaborazione del backend di Commerce. Verifica il codice personalizzato prima di unirlo alla produzione. Invece di aggiungere dati al backend, utilizza Mesh API per estendere lo schema GraphQL di Catalog Service. Per informazioni dettagliate sulla configurazione, vedere [Catalog Service and API Mesh](../catalog-service/mesh.md).

## Estendere i dati degli attributi di sistema nel feed dei prodotti

Il feed dei prodotti include attributi di sistema predefiniti necessari per l’elaborazione del prodotto o comunemente utilizzati dai consumatori. Puoi includere attributi di sistema aggiuntivi nel feed dei prodotti aggiungendoli al feed.

Per completare l&#39;attività, aggiornare il modulo `magento/catalog-data-exporter` per aggiungere gli attributi di sistema aggiuntivi al file di configurazione [dependency injection](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`).

Aggiungere gli attributi alla query dell&#39;attributo di prodotto (`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`).

**Esempio**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## Aggiungere attributi di prodotto ad Adobe Commerce

Gli sviluppatori possono aggiungere attributi di prodotto accessibili dal campo [attributi di prodotto](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields) utilizzando uno dei metodi seguenti:

- Aggiungere l&#39;attributo ad Adobe Commerce per l&#39;inclusione nei dati del feed `products` esportati in Commerce Storefront Services.
- Aggiungi l’attributo in modo dinamico durante il processo di sincronizzazione dei feed utilizzando un plug-in.

### Aggiungi l’attributo ad Adobe Commerce

Puoi aggiungere un attributo di prodotto dall’amministratore di Commerce oppure a livello di programmazione utilizzando un modulo PHP personalizzato per definire l’attributo e aggiornare Adobe Commerce. L’aggiunta dell’attributo da Commerce Admin è il metodo più semplice, in quanto puoi aggiungere l’attributo e tutti i metadati richiesti contemporaneamente. Il nuovo attributo e le relative proprietà di metadati vengono esportati automaticamente nei servizi SaaS durante la successiva sincronizzazione pianificata.

#### Creare l’attributo del prodotto da Admin

1. Dall&#39;amministratore di Commerce, creare l&#39;attributo dalla pagina di configurazione dell&#39;attributo del prodotto ([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]).

1. Aggiungere l&#39;attributo a un set di attributi in base alle esigenze.

Consulta [Creare gli attributi del prodotto](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) nella *Guida dell&#39;amministratore di Adobe Commerce*.

#### Creare l’attributo del prodotto a livello di programmazione

Aggiungere un attributo di prodotto a livello di programmazione creando una patch di dati che implementa `DataPatchInterface` e creare un&#39;istanza della classe `EavSetup Factory` nel costruttore per configurare le opzioni dell&#39;attributo.

Quando si definiscono le opzioni di attributo, tutti i parametri di attributo eccetto `type`, `label` e `input` sono facoltativi. Definite i seguenti parametri aggiuntivi ed eventuali altri che differiscono dalle impostazioni di default.

- **`user_defined`=`1`** - Esporta l&#39;attributo in servizi storefront durante la sincronizzazione dei dati
- **`used_in_product_listing`=`1`**—Rendi l&#39;attributo accessibile nella query del database dell&#39;elenco prodotti

Per informazioni sulla creazione di patch di dati, vedere [Develop data and schema patches](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) in *PHP Developer Guide*.

### Aggiungere l’attributo di prodotto in modo dinamico

Per informazioni dettagliate sulla creazione dinamica di attributi di prodotto senza l&#39;introduzione di nuovi attributi EAV, vedere [Aggiungere l&#39;attributo in modo dinamico](add-attribute-dynamically.md).
