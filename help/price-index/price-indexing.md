---
title: Indicizzazione dei prezzi SaaS
description: Utilizzo dell'indicizzazione dei prezzi SaaS per migliorare le prestazioni
seo-title: Adobe SaaS Price Indexing
seo-description: Price indexing give performance improvements using SaaS infrastructure
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Indicizzazione dei prezzi SaaS

L&#39;indicizzazione dei prezzi SaaS ottimizza le prestazioni del sito ripartendo le attività a uso intensivo di risorse, come l&#39;indicizzazione e il calcolo dei prezzi, dall&#39;applicazione Commerce all&#39;infrastruttura cloud di Adobe. Questo approccio consente ai commercianti di scalare rapidamente le risorse per accelerare i tempi di indicizzazione dei prezzi e fornire aggiornamenti dei prezzi allo storefront e ai servizi Commerce connessi in modo più rapido.

Il diagramma seguente mostra il flusso di dati di indicizzazione ai servizi SaaS quando Commerce utilizza il processo di indicizzazione dei prezzi [&#128279;](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/manage-indexers) incluso nell&#39;applicazione Commerce:

![Flusso di dati predefinito](assets/old_way.png)

Con l’indicizzazione dei prezzi SaaS abilitata, il flusso di dati cambia. L&#39;indicizzazione dei prezzi viene eseguita utilizzando [esportazione dati Commerce SaaS](../data-export/data-synchronization.md).

![Flusso dati indicizzazione prezzo SaaS](assets/new_way.png)

Tutti i commercianti possono beneficiare dell’indicizzazione dei prezzi SaaS, ma i commercianti che hanno progetti con le seguenti caratteristiche possono realizzare i maggiori vantaggi:

* **Cambiamenti di prezzo costanti**-Commercianti che richiedono modifiche ripetute ai loro prezzi per soddisfare obiettivi strategici come promozioni frequenti, sconti stagionali o riduzioni di inventario.
* **Più siti Web e/o gruppi di clienti**-Commercianti con cataloghi di prodotti condivisi su più siti Web (domini/marchi) e/o gruppi di clienti.
* **Molti prezzi univoci per siti Web o gruppi di clienti**-Commercianti con cataloghi di prodotti condivisi estesi che contengono prezzi univoci per siti Web o gruppi di clienti. Alcuni esempi includono i commercianti B2B che hanno prezzi pre-negoziati o marchi con diverse strategie di prezzo.

## Usa indicizzazione prezzi SaaS

L’indicizzazione dei prezzi SaaS viene abilitata automaticamente quando si installa Adobe Commerce Services. Supporta il calcolo dei prezzi per tutti i tipi di prodotto Adobe Commerce incorporati.

### Requisiti

* Adobe Commerce 2.4.4+

### Prerequisiti

* Con la versione più recente dell&#39;estensione Commerce deve essere installato uno dei servizi Commerce seguenti:

   * [Servizio catalogo](../catalog-service/overview.md)
   * [Live Search](../live-search/overview.md)
   * [Consigli di prodotto](../product-recommendations/guide-overview.md)


>[!NOTE]
>
>Se necessario, è possibile disabilitare l&#39;indicizzatore prezzi predefinito nell&#39;applicazione Commerce utilizzando [Catalog Adapter](catalog-adapter.md).

## Sincronizzare i prezzi con l&#39;indicizzazione SaaS

Dopo aver abilitato l’indicizzazione dei prezzi SaaS per Adobe Commerce, aggiorna i prezzi su Storefront e in Commerce Services sincronizzando i nuovi feed:

```bash
bin/magento saas:resync --feed=scopesCustomerGroup
bin/magento saas:resync --feed=scopesWebsite
bin/magento saas:resync --feed=prices
```

### Prezzi per tipi di prodotto personalizzati

I calcoli dei prezzi sono supportati per i tipi di prodotto personalizzati, ad esempio il prezzo di base, il prezzo speciale, il prezzo di gruppo, il prezzo delle regole di catalogo e così via.

Se si dispone di un tipo di prodotto personalizzato che utilizza una formula specifica per calcolare il prezzo finale, è possibile estendere il comportamento del feed del prezzo del prodotto.

1. Creare un plug-in nella classe `Magento\ProductPriceDataExporter\Model\Provider\ProductPrice`.

   ```xml
   <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
       <type name="Magento\ProductPriceDataExporter\Model\Provider\ProductPrice">
           <plugin name="custom_type_price_feed" type="YourModule\CustomProductType\Plugin\UpdatePriceFromFeed" />
       </type>
   </config>
   ```

1. Crea un metodo con la formula personalizzata:

   ```php
   class UpdatePriceFromFeed
   {
       /**
       * @param ProductPrice $subject
       * @param array $result
       * @param array $values
       *
       * @return array
       */
       public function afterGet(ProductPrice $subject, array $result, array $values) : array
       {
           // Override the output $result with your data for the corresponding products (see original method for details) 
           return $result;
       }
   }
   ```

