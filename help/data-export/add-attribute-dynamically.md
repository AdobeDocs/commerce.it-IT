---
title: Aggiungere dinamicamente attributi di prodotto
description: Scopri come aggiungere attributi di prodotto personalizzati ai feed di esportazione dei dati in modo dinamico durante il processo di sincronizzazione dei dati.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
TQID: https://experienceleague.adobe.com/SZWtLSvxb-w-968f4wqWrPTBn1c9IEuthvhIv86Pvss
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
source-wordcount: 267
ht-degree: 0%

---

# Aggiungere dinamicamente attributi di prodotto

È possibile estendere gli attributi del prodotto senza registrarli in [!DNL Adobe Commerce] creando un plug-in per aggiungere gli attributi durante il processo di sincronizzazione dei dati.

>[!NOTE]
>
>Il modo migliore per estendere gli attributi del prodotto è [aggiungerli a [!DNL Adobe Commerce]](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) where you can configure and manage them from the Commerce Admin. Only add them dynamically if you need them solely for Commerce storefront services and do not want to register them in [!DNL Adobe Commerce]. You also have the option to manage custom attributes using [[!DNL API Mesh] con  [!DNL Catalog Service]](../catalog-service/mesh.md) per estendere lo schema [!DNL Catalog Service] [!DNL GraphQL].

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

   ```shell
   bin/magento saas:resync --feed=products
   ```

## Dichiarare metadati di attributi di prodotto personalizzati

Se crei dinamicamente un attributo di prodotto personalizzato e desideri utilizzarlo per la visualizzazione, la ricerca o il filtro nei servizi di vetrina, aggiungi i metadati dell’attributo di prodotto per configurare il comportamento della vetrina.

1. Aggiornare il file di configurazione [dependency injection](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) per definire il plug-in per i metadati dell&#39;attributo del prodotto.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. Creare il plug-in per il provider `Magento\CatalogDataExporter\Model\Provider\ProductMetadata` seguente.

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

   ```shell
   bin/magento saas:resync --feed=productAttributes
   ```

>[!MORELIKETHIS]
>
> * [Estendere e personalizzare i feed di esportazione dei dati SaaS](extensibility-and-customizations.md)
> * [Sincronizzare i feed utilizzando Commerce CLI](data-export-cli-commands.md)
> * [Funzionamento della sincronizzazione](sync-overview.md): informazioni sulle modalità di sincronizzazione e sulla risincronizzazione pianificata e manuale.
> * [Esaminare i registri e risolvere i problemi](troubleshooting/logging.md)
