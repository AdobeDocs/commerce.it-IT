---
title: Estendere e personalizzare i dati del feed di esportazione dei dati SaaS
description: Scopri come estendere e personalizzare i dati del feed  [!DNL SaaS Data Export] .
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 815
ht-degree: 0%

---

# Estendere e personalizzare i dati del feed di esportazione dei dati SaaS

L&#39;estensione [!DNL Commerce Data Export] consente di esportare dati dall&#39;applicazione [!DNL Commerce] a servizi Commerce quali Live Search, Catalog Service e Product Recommendations. Se necessario, puoi estendere e personalizzare i dati del feed per includere dati di attributi aggiuntivi o modificare i dati raccolti.

Dopo aver aggiunto i dati degli attributi, è possibile accedervi dal campo [attributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type) nello schema di GraphQL per i servizi storefront.

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

Consulta [Creare gli attributi del prodotto](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) nella *Guida dell&#39;amministratore di Adobe Commerce*.

#### Creare l’attributo del prodotto a livello di programmazione

Aggiungere un attributo di prodotto a livello di programmazione creando una patch di dati che implementa `DataPatchInterface` e creare un&#39;istanza della classe `EavSetup Factory` nel costruttore per configurare le opzioni dell&#39;attributo.

Quando si definiscono le opzioni di attributo, tutti i parametri di attributo eccetto `type`, `label` e `input` sono facoltativi. Definite i seguenti parametri aggiuntivi ed eventuali altri che differiscono dalle impostazioni di default.

- **`user_defined`=`1`** - Esporta l&#39;attributo in servizi storefront durante la sincronizzazione dei dati
- **`used_in_product_listing`=`1`**—Rendi l&#39;attributo accessibile nella query del database dell&#39;elenco prodotti

Per informazioni sulla creazione di patch di dati, vedere [Develop data and schema patches](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) in *PHP Developer Guide*.

### Aggiungere l’attributo di prodotto in modo dinamico

Per informazioni dettagliate sulla creazione dinamica di attributi di prodotto senza l&#39;introduzione di nuovi attributi EAV, vedere [Aggiungere dinamicamente attributi di prodotto](add-attribute-dynamically.md).

## Panoramica schema feed (`et_schema.xml`) {#feed-schema-overview}

Ogni struttura di dati del feed è dichiarata in `etc/et_schema.xml` utilizzando un DSL XML semplice. Il framework legge questo file per determinare quali campi raccogliere e quali classi provider PHP chiamare.

```xml
<record name="Product">
  <field name="sku" type="ID" />
  <field name="name" type="String" />
  <field name="attributes" type="Attribute" repeated="true"
         provider="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
    <using field="productId" />
    <using field="storeViewCode" />
  </field>
</record>
```

Elementi chiave:

- `<record>` - definisce l&#39;entità feed
- `<field>` - dichiara un campo dati; l&#39;attributo `provider` punta a una classe PHP che implementa `DataProcessorInterface` che recupera i dati
- `repeated="true"` - il campo è un array di oggetti
- `<using>` - parametri di input passati dal contesto del record padre al provider

>[!IMPORTANT]
>
>L&#39;aggiunta di un nuovo campo a `et_schema.xml` modifica solo ciò che [!DNL Adobe Commerce] raccoglie localmente. Anche il servizio SaaS ricevente deve essere aggiornato per accettare ed elaborare il nuovo campo prima che abbia effetto sulla vetrina.

## Osservare i dati dopo l’invio {#observe-data-after-submission}

[!DNL SaaS Data Export] invia l&#39;evento `data_sent_outside` dopo ogni invio batch riuscito a un servizio SaaS. Utilizza questo evento per la registrazione di controllo, i trigger del webhook o la raccolta di metriche.

**Evento:** `data_sent_outside`

**Dati disponibili:**

| Chiave | Descrizione |
|---|---|
| `timestamp` | Timestamp Unix dell’invio |
| `type` | Nome feed (ad esempio, `products`, `prices`) |
| `data` | Il payload del feed inviato |

**Osservatore di esempio:**

```php
<?php
namespace My\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class DataSentOutsideObserver implements ObserverInterface
{
    public function execute(Observer $observer): void
    {
        $feedName = $observer->getData('type');
        $timestamp = $observer->getData('timestamp');
        $data = $observer->getData('data');

        // Custom logic: audit logging, webhook, metrics
    }
}
```

Registra l&#39;osservatore in `etc/events.xml`:

```xml
<event name="data_sent_outside">
    <observer name="my_module_data_sent_outside"
              instance="My\Module\Observer\DataSentOutsideObserver" />
</event>
```

Per informazioni generali su eventi e osservatori, consulta [Eventi e osservatori](https://developer.adobe.com/commerce/php/development/components/events-and-observers){target="_blank"} nella documentazione per sviluppatori di Adobe Commerce.

## Filtrare i dati prima dell’invio

Utilizzare il punto di estensione `Magento\SaaSCommon\Model\DataFilter` per reimpostare i campi sensibili o ignorare entità specifiche prima che i dati vengano inviati al servizio SaaS. Questo è utile per i requisiti di conformità come GDPR o PCI, in cui alcuni campi non devono uscire dall’istanza di Commerce.

Implementare l&#39;interfaccia e collegarla tramite una preferenza ID in `etc/di.xml`:

```xml
<preference for="Magento\SaaSCommon\Model\DataFilter"
            type="My\Module\Model\MyDataFilter" />
```

>[!NOTE]
>
>Il filtro viene applicato dopo la raccolta dei dati. Se `PERSIST_EXPORTED_FEED=1` è impostato, la tabella di feed memorizza il payload non filtrato prima che venga applicato il filtro.

>[!MORELIKETHIS]
>
> - [Aggiungi attributo prodotto in modo dinamico](add-attribute-dynamically.md)
> - [Aggiungere classe fiscale, set di attributi e metadati di inventario](add-tax-attribute-set-inventory-attributes.md)
> - [Funzionamento della sincronizzazione](sync-overview.md)
