---
title: '[!DNL Storefront Popover]'
description: ' [!DNL Live Search storefront popover] restituisce dinamicamente i prodotti suggeriti e le miniature.'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# [!DNL Storefront Popover]

Quando [!DNL Live Search] è [installato](install.md), viene visualizzato un [!DNL popover] nella vetrina quando gli acquirenti digitano nella casella [Cerca](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search). Con ogni carattere digitato, [!DNL popover] viene aggiornato con i prodotti suggeriti e le miniature dei risultati di ricerca principali.

[!DNL Live Search] restituisce risultati per una query di due o più caratteri. Per una corrispondenza parziale, il numero massimo di caratteri per parola è 20. Il numero di caratteri in una query di ricerca durante la digitazione non è configurabile.

Per impostazione predefinita, [!DNL Live Search] supporta [reindirizzamenti termini di ricerca](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html).

![[!DNL Live Search popover]](assets/storefront-search-as-you-type.png)

>[!TIP]
>
>Scopri come impostare gli attributi del prodotto come ricercabili nell&#39;articolo [Configurazione di Live Search](workspace.md).

## [!DNL Popover] dimensioni pagina

Le dimensioni della pagina di [!DNL popover] determinano il numero di righe di prodotti completati automaticamente che possono essere restituite. Durante l&#39;installazione di Live Search, il valore `page_size` viene modificato nel valore corrente dell&#39;impostazione [Ricerca nel catalogo](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/catalog.html) - `Autocomplete Limit`.

Per impostazione predefinita, il valore Ricerca nel catalogo - Limite completamento automatico è impostato su otto righe. Per modificare le dimensioni della pagina di [!DNL popover], eseguire le operazioni seguenti:

1. Nella barra laterale *Admin*, vai a **Archivi** > Impostazioni > **Configurazione**.
1. Nel pannello a sinistra, espandi **Catalogo** e scegli **Catalogo** dall&#39;elenco delle impostazioni.
1. Espandi la sezione *Ricerca nel catalogo*.
1. Impostare il **limite completamento automatico** sul numero di righe che si desidera consentire in [!DNL popover].
1. Al termine, fare clic su **Salva configurazione**.

## Esempio di stile [!DNL Popover]

Puoi personalizzare l&#39;aspetto del widget [!DNL Popover] in base alle linee guida di branding e di stile della tua azienda.

[!DNL storefront popover] visualizza sempre il prodotto `name` e `price` e la selezione dei campi non è configurabile. Tuttavia, è possibile formattare [!DNL popover] elementi utilizzando [classi CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/). Ad esempio, le seguenti dichiarazioni modificano il colore di sfondo del contenitore e del piè di pagina [!DNL popover].

```css
.livesearch.popover-container {
    background-color: lavender;
}

.livesearch.view-all-footer {
    background-color: magenta;
}
```

## Visibilità contenitore

Il componente padre di `.livesearch.popover-container` è `.search-autocomplete`.  La classe `.active` indica la visibilità del contenitore. La classe `.active` viene aggiunta in modo condizionale quando [!DNL popover] è aperto.

```css
.search-autocomplete.active   /* visible */
.search-autocomplete          /* not visible */
```

Per ulteriori informazioni sullo stile degli elementi della vetrina, consultare [Cascading Style Sheet (CSS)](https://developer.adobe.com/commerce/frontend-core/guide/css/) nella [Guida per gli sviluppatori di front-end](https://developer.adobe.com/commerce/frontend-core/guide/).

## Selettori di classi

È possibile utilizzare i selettori di classe seguenti per assegnare uno stile agli elementi contenitore e prodotto in [!DNL popover].

- `.livesearch.popover-container`
- `.livesearch.view-all-footer`
- `.livesearch.products-container`
- `.livesearch.product-result`
- `.livesearch.product-name`
- `.livesearch.product-price`

### Selettori di classi contenitore

#### .livesearch.popover-container

Contenitore ![[!DNL Popover]](assets/livesearch-popover-container.png)

#### .livesearch.view-all-footer

![Visualizza tutto il piè di pagina](assets/livesearch-view-all-footer.png)

### Selettori di classi di prodotto

#### .livesearch.products-container

![Contenitore prodotto](assets/livesearch-product-container.png)

#### .livesearch.product-result

![Risultato prodotto](assets/livesearch-product-result.png)

#### .livesearch.product-name

![Nome prodotto](assets/livesearch-product-name.png)

#### .livesearch.product-price

![Prezzo del prodotto](assets/livesearch-product-price.png)

#### .livesearch product-link

![Risultato prodotto](assets/livesearch-product-link.png)

## Utilizzo di un tema modificato {#working-with-modified-theme}

È possibile utilizzare [!DNL storefront popover] con un [tema](https://developer.adobe.com/commerce/frontend-core/guide/themes/) personalizzato che eredita i file richiesti da *Luma*. Il blocco `top.search` in `header-wrapper` del modulo `Magento_Search` non deve essere modificato.

```html
<referenceContainer name="header-wrapper">
   <block class="Magento\Framework\View\Element\Template" name="top.search" as="topSearch" template="Magento_Search::form.mini.phtml">
      <arguments>
         <argument name="configProvider" xsi:type="object">Magento\Search\ViewModel\ConfigProvider</argument>
      </arguments>
   </block>
</referenceContainer>
```

## Disabilitazione di [!DNL popover]

Per disabilitare [!DNL popover] e ripristinare la funzionalità standard [Ricerca rapida](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search), immettere il comando seguente:

```bash
bin/magento module:disable Magento_LiveSearchStorefrontPopover
```

## Implementazioni headless

Per gli utenti con implementazioni headless, è possibile installare [!DNL Live Search popover] utilizzando un pacchetto [npm](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
