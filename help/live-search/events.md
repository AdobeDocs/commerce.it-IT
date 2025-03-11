---
title: '[!DNL Live Search] eventi'
description: Scopri come gli eventi raccolgono i dati per  [!DNL Live Search].
feature: Services, Eventing
exl-id: a9f4f254-d8ff-46f1-8deb-a75b90d70d52
source-git-commit: 94d2a9911ab10d164d75779d1f310e5bdf2aea74
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# [!DNL Live Search] eventi

[!DNL Live Search] utilizza gli eventi per attivare gli algoritmi di ricerca, ad esempio &quot;Più visualizzati&quot; e &quot;Più visualizzati, visualizzati&quot;. Anche se il [tema Luma di esempio di Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/design/themes/themes#the-default-theme) ottiene eventi pronti all&#39;uso, le implementazioni headless e personalizzate devono implementare eventi per le proprie esigenze.

Questa tabella descrive gli eventi utilizzati da [!DNL Live Search] [strategie di classificazione](rules-add.md#intelligent-ranking).

| Strategia di classificazione | Eventi | Pagina |
| --- | --- | --- |
| Articoli più visualizzati | `page-view`<br>`product-view` | Pagina dettagli prodotto |
| Più acquistati | `page-view`<br>`place-order` | Carrello/Pagamento |
| Più aggiunti al carrello | `page-view`<br>`add-to-cart` | Pagina dettagli prodotto<br>Pagina elenco prodotti<br>Carrello<br>Elenco desideri |
| Ha visualizzato questo, ha visualizzato quello | `page-view`<br>`product-view` | Pagina dettagli prodotto |

>[!NOTE]
>
>La raccolta dei dati ai fini di [!DNL Live Search] non include informazioni personali (PII). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi. [Ulteriori informazioni](https://www.adobe.com/privacy/experience-cloud.html).

## Eventi dashboard richiesti

Alcuni eventi sono necessari per popolare il [dashboard di Live Search](performance.md)

| Area del dashboard | Eventi | Unisci campo |
| ------------------- | ------------- | ---------- |
| Ricerche univoche | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Nessuna ricerca di risultati | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Percentuale risultati zero | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Ricerche comuni | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Media posizione clic | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId` |
| Percentuale di click-through | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId`, `sku`, `parentSku` |
| Tasso di conversione | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click`, `product-view`, `add-to-cart`, `place-order` | `searchRequestId`, `sku`, `parentSku` |

### Contesti richiesti

Tutti gli eventi richiedono i contesti `Page` e `Storefront`. Questo dovrebbe accadere a livello di pagina/livello di applicazione vetrina piuttosto che durante la generazione di singoli eventi (ad esempio, in una vetrina PHP, il contenitore di applicazioni PHP è responsabile della loro impostazione in fase di esecuzione).

## Utilizzo

Di seguito è riportato un esempio di implementazione dell&#39;evento `search-request-sent`:

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## Avvertenze

- Gli ad blocker e le impostazioni di privacy possono impedire l&#39;acquisizione degli eventi e causare la mancata generazione di rapporti per [metriche](performance.md) relative a coinvolgimento e ricavi. Inoltre, alcuni eventi potrebbero non essere inviati a causa di acquirenti che abbandonano la pagina o di problemi di rete.
- Le implementazioni headless devono implementare eventi per potenziare il merchandising intelligente.

>[!NOTE]
>
>Se è abilitata la modalità di restrizione dei cookie [](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html), Adobe Commerce non raccoglie i dati comportamentali fino a quando l&#39;acquirente non acconsente all&#39;utilizzo dei cookie. Se la modalità di restrizione dei cookie è disabilitata, Adobe Commerce raccoglie i dati comportamentali per impostazione predefinita.
