---
title: Aggiungere dinamicamente attributi di prodotto
description: Scopri come aggiungere attributi di prodotto personalizzati ai feed di esportazione dei dati in modo dinamico durante il processo di sincronizzazione dei dati.
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
source-git-commit: 37d5699315e34f1504602090fae5201ee51cf470
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Aggiungi gli attributi del prodotto in modo dinamico durante la sincronizzazione dei dati

Puoi estendere gli attributi del prodotto senza registrarli in Adobe Commerce creando un plug-in per aggiungerli durante il processo di sincronizzazione dei dati.

>[!NOTE]
>
>Il modo migliore per estendere gli attributi del prodotto è [aggiungerli ad Adobe Commerce](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) dove puoi configurarli e gestirli dall&#39;amministratore Commerce. Aggiungili in modo dinamico solo se sono necessari solo per i servizi di vetrina Commerce e non desideri registrarli in Adobe Commerce. È inoltre possibile gestire gli attributi personalizzati utilizzando [Mesh API con Catalog Service](../catalog-service/mesh.md) per estendere lo schema GraphQL di Catalog Service.

## Aggiungi attributi prodotto

Creare un plug-in che aggiunga `customer_attribute` alla classe `Magento\CatalogDataExporter\Model\Provider\Product\Attributes`.

1. Aggiorna il file di configurazione [dependency injection](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) per definire il plug-in.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. Crea il plug-in.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\Product\Attributes;
   
    class AddAttribute {
   
         /**
          * @param Attributes $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
          public function afterGet(Attributes $subject, array $result, $arguments): array
          {
              $additionalAttributes = [];
              $attributeCode = 'customer_attribute';
              foreach ($result as $product) {
                  if (!isset($product['productId']) || !isset($product['storeViewCode'])) {
                      continue;
                  }
                  // HINT: if needed, do filtration by "storeViewCode" and or "productId"
   
                  $productId = $product['productId'];
                  $storeViewCode = $product['storeViewCode'];
   
                  $newKey = \implode('-', [$product['storeViewCode'], $product['productId'], $attributeCode]);
                  if (isset($additionalAttributes[$newKey])) {
                      continue;
                  }
                  $additionalAttributes[$newKey] = [
                      'productId' => $productId,
                      'storeViewCode' => $storeViewCode,
                      'attributes' => [
                          'attributeCode' => $attributeCode,
                          // provide single or multiple values for the attribute
                          'value' => [
                              rand(1, 42)
                          ]
                      ]
                  ];
   
              }
   
              return array_merge($result, $additionalAttributes);
          }
    }
   ```

   Dopo aver aggiunto il plug-in, le modifiche vengono sincronizzate con i servizi vetrina connessi durante la successiva sincronizzazione pianificata. Per inviare immediatamente gli aggiornamenti, utilizzare il seguente comando CLI per avviare manualmente il processo di sincronizzazione.

   ```
   bin/magento saas:resync --feed=products
   ```

## Dichiarare metadati di attributi di prodotto personalizzati

Se crei dinamicamente un attributo di prodotto personalizzato e desideri utilizzarlo per la visualizzazione, la ricerca o il filtro nei servizi di vetrina, aggiungi i metadati dell’attributo di prodotto per configurare il comportamento della vetrina.

1. Aggiornare il file di configurazione [dependency injection](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) per definire il plug-in per i metadati dell&#39;attributo del prodotto.

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. Creare il plug-in al provider `\Magento\CatalogDataExporter\Model\Provider\ProductMetadata` seguente.

   Controlla `ProductAttributeMetadata` in `vendor/magento/module-catalog-data-exporter/etc/et_schema.xml` per i campi obbligatori.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\ProductMetadata;
   
    class AddAttributeMetadata {
   
         /**
          * @param ProductMetadata $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(ProductMetadata $subject, array $result, $arguments): array
         {
              $result[] = [
                'id' => '123',
                // provide storeCode, websiteCode and storeViewCode applicable for your AC instance
                'storeCode' => 'default',
                'websiteCode' => 'base',
                'storeViewCode' => 'default',
                // specify the customer attribute code - should be the same as used in the products attributes plugin
                'attributeCode' => 'customer_attribute',
                // only product attributes are supported
                'attributeType' => 'catalog_product',
                // specify the data type
                'dataType' => 'int',
                'multi' => false,
                'label' => 'Customer Attribute',
                'frontendInput' => 'select',
                'required' => false,
                'unique' => false,
                'global' => true,
                'visible' => true,
                'searchable' => true,
                'filterable' => true,
                // This value must be set to true to export it to the storefront services
                'visibleInCompareList' => true,
                'visibleInListing' => true,
                'sortable' => true,
                'visibleInSearch' => true,
                'filterableInSearch' => true,
                'searchWeight' => 1.0,
                'usedForRules' => true,
                'boolean' => false,
                'systemAttribute' => false,
                'numeric' => false,
                // specify the list of attribute options
                'attributeOptions' => [
                    'option1',
                    'option2',
                    'option3'
                ]
             ];
   
              return $result;
         }
      }
   ```

   Dopo aver aggiunto il plug-in, le modifiche vengono sincronizzate con i servizi vetrina connessi durante la successiva sincronizzazione pianificata. Per inviare immediatamente gli aggiornamenti, utilizzare il seguente comando CLI per avviare manualmente il processo di sincronizzazione.

   ```
   bin/magento saas:resync --feed=productattributes
   ```

