---
title: Personalizza
description: Scopri come personalizzare i consigli di prodotto.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Personalizza

Quando si installa il modulo Consigli di prodotto, Adobe Commerce crea la directory `ProductRecommendationsLayout`. Questa directory contiene file modello che è possibile personalizzare per modificare la modalità di visualizzazione dei consigli nella vetrina. In particolare, puoi modificare o sostituire il seguente modello:

`<your theme>/Magento_ProductRecommendationsLayout/web/template/recommendations.html`

Per ulteriori informazioni sulla modifica dei file modello, consultare [Personalizzazione modello](https://developer.adobe.com/commerce/frontend-core/guide/templates/walkthrough/) nella Guida per gli sviluppatori di Frontend.

Se modifichi il file `recommendations.html`, devi mantenere i seguenti tag nel file per garantire che Adobe Commerce possa raccogliere le metriche dei consigli dalla vetrina:

| Tag | Utilizzare |
|---|---|
| `<div data-bind="attr : {'data-unit-id' : unitId }"...</div>` | Raccoglie gli eventi di visualizzazione. |
| `<a data-bind="attr : {'data-sku' : sku, 'data-unit-id'}"...</a>` | Raccoglie eventi di clic. <br/>**Nota:** se aggiungi tag di ancoraggio, devi includere questi attributi. |

Oltre al file `recommendations.html`, la directory `ProductRecommendationsLayout` contiene le seguenti sottodirectory:

| Directory | Finalità |
|---|---|
| `layout` | Contiene `*.xml` file per ogni tipo di pagina |
| `templates` | Contiene file che chiamano gli script di recupero e rendering |
| `web/js` | Contiene i file JavaScript che recuperano ed eseguono il rendering dei consigli per l’archivio |
| `web/template` | Contiene il modello per il modulo `magento/product-recommendations` |

## Posizionamento dell’unità per i consigli

Quando [crei](create.md) un consiglio, specifica il [percorso](placement.md) in cui viene visualizzato nella pagina. Un’unità di consigli può essere posizionata nella parte superiore o inferiore del contenitore di contenuto principale. Tuttavia, potete personalizzare questo posizionamento. Se crei un tipo di contenuto per consigli di Page Builder, utilizza gli strumenti di Page Builder per posizionare l’unità di consigli sulla pagina. Per tutti gli altri tipi di pagina, modifica i file `*.xml` generati al momento della creazione del consiglio.

1. Passare alla directory `layout`:

   ```bash
   cd `<your theme>/Magento_ProductRecommendationsLayout/layout`
   ```

   Nella tabella seguente sono elencati i file XML presenti in questa directory:

   | Nome file | Pagina |
   |---|---|
   | `catalog_category_view.xml` | Categoria |
   | `catalog_product_view.xml` | Dettagli del prodotto |
   | `checkout_cart_index.xml` | Carrello |
   | `checkout_onepage_success.xml` | Pagamento |
   | `cms_index_index.xml` | Home |

   >[!NOTE]
   >
   >I nomi dei file nella directory `layout` potrebbero essere diversi se l&#39;archivio utilizza estensioni di terze parti.

1. Modificare il file `catalog_product_view.xml` in modo che l&#39;unità di consigli venga visualizzata dopo l&#39;immagine del prodotto nella pagina dei dettagli del prodotto. Prima di personalizzare il file XML, esaminare il file e comprendere le sezioni da modificare:

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="main.content">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   Nel frammento precedente, il blocco di riferimento `main.content` indica che l&#39;unità di consigli verrà posizionata in un punto relativo a tale elemento. L&#39;elemento `block` contiene l&#39;attributo `after="-"`, che specifica che l&#39;unità di consigli verrà visualizzata nella pagina dopo il blocco di contenuto principale.

1. Modifichiamo questo file specificando un blocco di contenuto diverso.

   Modificare il blocco di riferimento `name` da `main.content` a `product.info.media`.

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="product.info.media">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   Con questa modifica, l’unità di consigli viene visualizzata dopo l’immagine del prodotto nella pagina dei dettagli del prodotto. Se si desidera che l&#39;unità di consigli venga visualizzata prima di `product.info.media`, modificare l&#39;attributo `after="-"` in `before="-"`. L&#39;argomento `pagePlacement` è un argomento interno da non modificare.

Per ulteriori informazioni sui tipi di blocchi nella pagina, consulta [panoramica del layout](https://developer.adobe.com/commerce/frontend-core/guide/layouts/).

## Attributi di prodotto personalizzati

Gli sviluppatori spesso hanno bisogno di accedere a valori di attributi di prodotto personalizzati nelle unità Consigli su vetrine in modo da poter aggiungere trattamenti visivi ai prodotti basati su tali attributi.

Ad esempio, se il tuo negozio vende alcuni prodotti biologici, potresti avere un attributo personalizzato su tali prodotti che li designa come `Organic = Yes`. Potresti aver bisogno dell’accesso a questo valore di attributo nella vetrina in modo da poter dare a questi prodotti un trattamento visivo speciale quando compaiono in Consigli. Allo stesso modo, l’accesso a questi valori di attributi di prodotto personalizzati consente di assegnare distintivi ai prodotti o applicare una logica personalizzata nel livello di presentazione del sito.

![Aggiungi badge](assets/unit-custom.png)

Per assicurarsi che un attributo di prodotto personalizzato sia disponibile quando si esegue il rendering dell&#39;unità di consigli sulla pagina, impostare la proprietà `Used in Product Listing` su `Yes` nella pagina [Attributi di prodotto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=it) dell&#39;amministratore.

Quando questa proprietà è impostata, il payload JSON include un oggetto `attributes` che contiene un array di codici e valori di attributo. Puoi quindi applicare uno stile di vetrina personalizzato in base a questi valori di attributo, ad esempio aggiungendo speciali trattamenti visivi o badge come indicato in precedenza.

>[!NOTE]
>
>Le modifiche all’attributo del prodotto possono richiedere fino a un’ora per essere visualizzate nel payload JSON.
