---
title: Aggiungi attributi ordine personalizzati
description: Scopri come aggiungere attributi di ordine personalizzati ai dati del backoffice e inviare tali attributi ad Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Aggiungi attributi ordine personalizzati

In questo articolo imparerai ad aggiungere attributi personalizzati agli eventi di back office. Con gli attributi personalizzati, puoi acquisire informazioni approfondite su dati avanzati per migliorare l’analisi e creare ulteriori esperienze personalizzate per gli acquirenti.

Gli attributi personalizzati sono supportati a due livelli:

- Livello dell’ordine
- Livello articolo ordine

>[!NOTE]
>
>Adobe [!DNL Commerce] supporta attributi personalizzati con tipo di dati stringa, booleano o data.

Per aggiungere attributi personalizzati agli eventi di back office è necessario:

1. Crea un progetto nell&#39;installazione di [!DNL Commerce].
1. Aggiorna lo schema in modo che i nuovi attributi personalizzati possano essere correttamente acquisiti in Experience Platform.
1. In Admin, verifica che gli attributi personalizzati vengano acquisiti e inviati ad Experience Platform.

>[!IMPORTANT]
>
>La struttura della directory e gli esempi di codice riportati di seguito illustrano come implementare gli attributi personalizzati. La struttura e il codice effettivi della directory dipendono dalla configurazione e dall’ambiente dell’archivio.

## Passaggio 1: creare la struttura della directory

1. Passare alla directory `app/code` nell&#39;installazione di [!DNL Commerce] e creare una directory di moduli. Esempio: `Magento/AepCustomAttributes`. Questa directory contiene i file necessari per gli attributi personalizzati.
1. Nella directory del modulo, creare una sottodirectory denominata `etc`. La directory `etc` contiene i file `module.xml`, `query.xml`, `di.xml` e `et_schema.xml`.

## Passaggio 2: definire le dipendenze e la versione di impostazione

Creare un file `module.xml` che definisce le dipendenze e la versione di installazione. Ad esempio:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Magento_AepCustomAttributes">
        <sequence>
            <module name="Magento_SalesOrderDataExporter"/>
        </sequence>
    </module>
</config>
```

## Passaggio 3: Recuperare i dati dell&#39;ordine cliente

Creare un file `query.xml` che recupera i dati dell&#39;ordine cliente. Ad esempio:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:Module:Magento_QueryXml:etc/query.xsd">
  <query name="salesOrdersV2">
    <source name="sales_order">
      <link-source name="sales_order_inventory_source" link-type="inner">
        <attribute name="inventory_source_code" alias="inventory_source" />
        <using glue="and">
          <condition attribute="order_id" operator="eq" type="identifier">entity_id</condition>
         </using> 
        </link-source>
    </source>
  </query>
  </config>
```

## Passaggio 4: impostare l’iniezione di dipendenza

Creare un file `di.xml` che configura l&#39;iniezione di dipendenza. Ad esempio:

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
      <type name="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">commerceOrderId</argument>
          </arguments>
      </type>
      <type name="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">entityId</argument>
          </arguments>
      </type>
      <type name="Magento\DataServices\Model\ProductContext">
          <plugin name="product-context-plugin" type="Magento\AepCustomAttributes\Plugin\Model\ProductContext"/>
      </type>
  </config>
```

## Passaggio 5: definire i servizi utilizzati per l’iniezione della dipendenza

Creare un file `et_schema.xml` che definisce i servizi utilizzati per l&#39;iniezione di dipendenza. Ad esempio:

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_DataExporter:etc/et_schema.xsd">
      <record name="OrderV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
              <using field="commerceOrderId"/>
          </field>
      </record>
      <record name="OrderItemV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
              <using field="entityId"/>
          </field>
      </record>
  </config>
```

## Passaggio 6: creare una directory per i file PHP

Allo stesso livello della directory `etc`, creare una directory denominata `Module/Provider`. Questa directory contiene i file PHP `OrderCustomAttributes` e `OrderItemCustomAttributes`.

## Passaggio 7: definire OrderCustomAttributes

Creare un file `OrderCustomAttributes.php` che definisce gli attributi personalizzati dell&#39;ordine. Ad esempio:

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class CustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param string $usingField
   * @param Json $jsonSerializer
   */
  public function __construct(
      string $usingField,
      Json $jsonSerializer
  ) {
      $this->usingField = $usingField;
      $this->jsonSerializer = $jsonSerializer;
  }

  /**
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];

      /**
       * Entity IDs
       */
      $ids = array_column($values, $this->usingField);

      foreach ($this->flatten($values) as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];

          if (isset($row)) {
              $unserializedData['order_channel'] = 'order_channel';
              $unserializedData['order_status'] = 'order_status';

              $additionalInformation = [];
              foreach ($unserializedData as $name => $value) {
                  $additionalInformation[] = [
                      'name' => $name,
                      'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
                  ];
              }
              foreach ($additionalInformation as $information) {
                  $output[] = [
                      'additionalInformation' => $information,
                      $this->usingField => $row[$this->usingField],
                  ];
              }
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## Passaggio 8: definire OrderItemCustomAttributes

Creare un file `OrderItemCustomAttributes.php` che definisce gli attributi personalizzati dell&#39;elemento dell&#39;ordine. Ad esempio:

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class OrderItemCustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param Json $jsonSerializer
   * @param string $usingField
   */
  public function __construct(
      Json $jsonSerializer,
      string $usingField
  ) {
      $this->jsonSerializer = $jsonSerializer;
      $this->usingField = $usingField;
  }

  /**
   * Getting additional attributes data.
   *
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];
      $values = $this->flatten($values);

      foreach ($values as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];
          $unserializedData['product_brand'] = implode(',', ['label 1', 'label 2']);

          $additionalInformation = [];
          foreach ($unserializedData as $name => $value) {
              $additionalInformation[] = [
                  'name' => $name,
                  'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
              ];
          }
          foreach ($additionalInformation as $information) {
              $output[] = [
                  'additionalInformation' => $information,
                  $this->usingField => $row[$this->usingField],
              ];
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## Passaggio 9: creare una directory per il file productContext

Allo stesso livello della directory `etc`, creare una directory denominata `Plugin/Module`. Questa directory contiene il file `ProductContext.php`.

## Passaggio 10: definire la classe ProductContext

Creare un file denominato `ProductContext.php` che definisce la classe `ProductContext`. Ad esempio:

```php
<?php>
namespace Magento\AepCustomAttributes\Plugin\Model;
use Magento\Catalog\Model\Product;
use Magento\DataServices\Model\ProductContext as Subject;
use Magento\Framework\App\ResourceConnection;

class ProductContext
{
    private ?array $brandCache = [];
    public function __construct(
        private ResourceConnection $resourceConnection ) {
    }  

    public function afterGetContextData(Subject $subject, array $result Product $product)
    {
        $brand = $product->getCustomAttribute('cust_attr1');
        if (!empty($brand) && $brand->getValue()) {
            $result['brands'] = ['brand_label_1', 'brand_label_2'];
            }
            return $result;
      }
  }
```

## Passaggio 11: registrare il modulo

Allo stesso livello della directory `etc`, creare un file `registration.php` che registri il modulo. Ad esempio:

```php
<?php>
declare(strict_types=1);

use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Magento_AepCustomAttributes',
    __DIR__
);
```

## Passaggio 12: estendere lo schema XDM esistente

Per garantire che i nuovi attributi dell&#39;ordine personalizzato possano essere acquisiti dallo schema [!DNL Commerce] in Experience Platform, è necessario estendere lo schema per includere questi campi personalizzati.

Per informazioni su come estendere uno schema XDM esistente per includere questi campi personalizzati, consulta l&#39;articolo [Creare e modificare gli schemi nell&#39;interfaccia utente](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/ui/resources/schemas#custom-fields-for-standard-groups) nella documentazione di Experience Platform. Il campo ID tenant viene generato in modo dinamico; tuttavia, la struttura del campo deve essere simile all’esempio fornito nella documentazione di Experience Platform.

>[!IMPORTANT]
>
>Gli attributi personalizzati XDM devono corrispondere agli attributi inviati da [!DNL Commerce].

A `commerce.order`, aggiungere un campo per il livello Ordine:

![Livello ordine](assets/order-level.png)

A `productListItems`, aggiungere i campi per il livello di elemento dell&#39;ordine:

![Livello elemento ordine](assets/order-item-level.png)

## Passaggio 12: verifica che i dati vengano acquisiti

Visualizza la scheda [Personalizzazione dati](connect-data.md#data-customization) nell&#39;amministratore per verificare che i dati degli attributi personalizzati vengano acquisiti e inviati ad Experience Platform.

### Risoluzione dei problemi

Se viene visualizzato il messaggio `No custom order attributes found.` nella scheda **[!UICONTROL Data Customization]**, confermare quanto segue:

1. Sono stati completati i prerequisiti per abilitare l&#39;estensione [Data Connector](overview.md#prerequisites).
1. Hai configurato [attributi ordine personalizzati](#add-custom-order-attributes).
1. È stato generato almeno un evento ordine.
