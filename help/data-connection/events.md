---
title: Eventi comportamentali
description: Scopri i dati acquisiti da ogni evento comportamentale.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '4516'
ht-degree: 0%

---

# [!DNL Data Connection] eventi comportamentali

Nell&#39;elenco seguente sono elencati gli eventi comportamentali di Commerce disponibili quando si installa l&#39;estensione [!DNL Data Connection]. I dati raccolti da questi eventi vengono inviati a Adobe Experience Platform. Puoi anche creare [eventi personalizzati](custom-events.md) per raccogliere dati aggiuntivi non forniti come predefiniti.

Oltre ai dati raccolti dai seguenti eventi, si ottengono anche [altri dati](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) forniti da Adobe Experience Platform Web SDK.

Gli eventi comportamentali raccolgono dati comportamentali anonimi dagli acquirenti che navigano sul tuo sito. Puoi utilizzare i dati raccolti da questi eventi per creare promozioni e campagne indirizzate a un gruppo specifico di acquirenti.

>[!NOTE]
>
>Tutti gli eventi comportamentali includono il campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html), che include l&#39;indirizzo e-mail dell&#39;acquirente, se disponibile, ed ECID.

## Eventi vetrina

Gli eventi Storefront acquisiscono dati dalle interazioni degli acquirenti sul sito e includono eventi come [`addToCart`](#addtocart), [`pageView`](#pageview), [`createAccount`](#createaccount), [`editAccount`](#editaccount), [`startCheckout`](#startcheckout), [`completeCheckout`](#completecheckout), [`signIn`](#signin), [`signOut`](#signout) e così via. Gli eventi Storefront si applicano solo a prodotti semplici e configurabili.

### addToCart

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un prodotto viene aggiunto al carrello o quando la quantità di un prodotto nel carrello viene incrementata. | `commerce.productListAdds` |

#### Dati raccolti da addToCart

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListAdds` | Indica se un prodotto è stato aggiunto a un carrello. Il valore `1` indica che è stato aggiunto un prodotto. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |

### openCart

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando viene creato un nuovo carrello, ovvero quando un prodotto viene aggiunto a un carrello vuoto. | `commerce.productListOpens` |

#### Dati raccolti da openCart

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListOpens` | Indica se è stato creato un carrello. Il valore `1` indica che è stato creato un carrello. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |

### removeFromCart

| Descrizione | Nome evento XDM |
|---|---|
| Viene attivato ogni volta che un prodotto viene rimosso o ogni volta che la quantità di un prodotto nel carrello diminuisce. | `commerce.productListRemovals` |

#### Dati raccolti da removeFromCart

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListRemovals` | Indica se un prodotto è stato rimosso dal carrello. Il valore `1` indica che un prodotto è stato rimosso dal carrello. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |

### shoppingCartView

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione al caricamento di qualsiasi pagina del carrello. | `commerce.productListViews` |

#### Dati raccolti da shoppingCartView

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListViews` | Indica se è stato visualizzato un elenco di prodotti. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `commerce.order` | Contiene informazioni sull&#39;ordine in sospeso per uno o più prodotti. |
| `commerce.order.discountAmount` | Indica l&#39;importo dello sconto applicato all&#39;intero ordine. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |

### pageView

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione al caricamento di qualsiasi pagina. | `web.webpagedetails.pageViews` |

#### Dati raccolti da pageView

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `web.webPageDetails.pageViews` | Indica se una pagina è stata caricata. Un `value` di `1` indica che la pagina è stata caricata. |
| `web.webPageDetails.URL` | L’URL normativo o abituale della pagina web. Può essere l&#39;URL effettivo utilizzato per raggiungere la pagina, che verrebbe registrato utilizzando `Web Link`. |
| `web.webPageDetails.name` | Il nome normativo della pagina web. Questo nome non è necessariamente il titolo della pagina o è direttamente associato al contenuto della pagina, ma viene utilizzato per organizzare le pagine di un sito a scopo di classificazione. |
| `web.webReferrer.URL` | L’URL della pagina web visitata da un acquirente prima di fare clic su un collegamento al sito. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### productPageView

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione al caricamento di qualsiasi pagina di prodotto. | `commerce.productViews` |

#### Dati raccolti da productPageView

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productViews` | Indica se il prodotto è stato visualizzato. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |

### startCheckout

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando l&#39;acquirente fa clic su un pulsante di pagamento. | `commerce.checkouts` |

#### Dati raccolti da startCheckout

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.checkouts` | Indica se si è verificata un&#39;azione durante il processo di pagamento. |
| `commerce.cart.cartID` | L’ID univoco che identifica il carrello del cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |

### completeCheckout

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando l’acquirente effettua un ordine. | `commerce.purchases` |

#### Dati raccolti da completeCheckout

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.purchases` | Indica se un ordine è stato accettato. |
| `commerce.order` | Contiene informazioni sull’ordine effettuato per uno o più prodotti. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.paymentTransactionID` | Identificatore univoco per questa transazione di pagamento. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Opzioni: `cash`, `credit_card`, `debit_card`, `gift_card`, `check`, `paypal`, `wire_transfer`, `credit_card_reference`, `other`. |
| `commerce.order.payments.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.taxAmount` | Importo dell&#39;imposta pagato dall&#39;acquirente come parte del pagamento finale. |
| `commerce.order.discountAmount` | Indica l&#39;importo dello sconto applicato all&#39;intero ordine. |
| `commerce.order.createdDate` | L’ora e la data di creazione di un nuovo ordine nel sistema commerce. Ad esempio, `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |  | `shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |

## Eventi profilo cliente

Gli eventi profilo acquisiti dalla vetrina includono informazioni sull&#39;account, ad esempio `signIn`, `signOut`, `createAccount` e `editAccount`. Questi dati vengono utilizzati per compilare i dettagli chiave dei clienti necessari per definire meglio i segmenti o eseguire campagne di marketing, ad esempio inviare offerte di sconto per l’iscrizione, conferme di modifica dell’account e così via. Sono presenti eventi di profilo simili acquisiti da [lato server](events-backoffice.md#customer-profile-events).

### signIn

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di accedere. | `userAccount.login` |

>[!NOTE]
>
> Questo evento viene attivato quando si tenta di eseguire l’azione specifica. Non indica che l’azione è stata eseguita correttamente.

#### Dati raccolti da signIn

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Un singolo attore, contatto o proprietario. |
| `person.accountID` | Acquisisce l’ID dell’account utente. |
| `person.accountType` | Acquisisce il tipo di account utente, ad esempio `Personal` o `Company`, se applicabile. |
| `person.personalEmailID` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `personalEmail` | Acquisisce i dettagli di contatto, ovvero un messaggio di posta elettronica e le informazioni associate. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.login` | Indica se un visitatore ha tentato di accedere. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### disconnetti

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di uscire. | `userAccount.logout` |

>[!NOTE]
>
> Questo evento viene attivato quando si tenta di eseguire l’azione specifica. Non indica che l’azione è stata eseguita correttamente.

#### Dati raccolti da signOut

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.logout` | Indica se un visitatore ha tentato di disconnettersi. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### createAccount

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di creare un account. | `userAccount.createProfile` |

>[!NOTE]
>
> Questo evento viene attivato quando si tenta di eseguire l’azione specifica. Non indica che l’azione è stata eseguita correttamente.

#### Dati raccolti da createAccount

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Un singolo attore, contatto o proprietario. |
| `person.accountID` | Acquisisce l’ID dell’account utente. |
| `person.accountType` | Acquisisce il tipo di account utente, ad esempio `Personal` o `Company`, se applicabile. |
| `person.personalEmailID` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `personalEmail` | Acquisisce i dettagli di contatto, ovvero un messaggio di posta elettronica e le informazioni associate. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.updateProfile` | Indica se un utente ha aggiornato il proprio profilo account. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### editAccount

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di modificare un account. | `userAccount.updateProfile` |

>[!NOTE]
>
> Questo evento viene attivato quando si tenta di eseguire l’azione specifica. Non indica che l’azione è stata eseguita correttamente.

#### Dati raccolti da editAccount

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Un singolo attore, contatto o proprietario. |
| `person.accountID` | Acquisisce l’ID dell’account utente. |
| `person.accountType` | Acquisisce il tipo di account utente, ad esempio `Personal` o `Company`, se applicabile. |
| `person.personalEmailID` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `personalEmail` | Acquisisce i dettagli di contatto, ovvero un messaggio di posta elettronica e le informazioni associate. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.updateProfile` | Indica se un utente ha aggiornato il proprio profilo account. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

## Cerca eventi

Gli eventi di ricerca forniscono dati rilevanti per l’intento dell’acquirente. L&#39;intuizione dell&#39;intento di un cliente aiuta i commercianti a capire come gli acquirenti stanno cercando gli articoli, cosa cliccano e, in ultima analisi, acquistano o abbandonano. Un esempio di come puoi utilizzare questi dati è se desideri eseguire il targeting degli acquirenti esistenti che cercano il tuo prodotto principale, ma non acquistano mai il prodotto. Per accedere a questi eventi è necessario installare l&#39;estensione [[!DNL Live Search]](../live-search/install.md).

Utilizzare i campi `searchRequest.id` e `searchResponse.id` trovati negli eventi `searchRequestSent` e `searchResponseReceived` per creare un riferimento incrociato tra una richiesta di ricerca e la risposta di ricerca corrispondente.

### searchRequestSent

| Descrizione | Nome evento XDM |
|---|---|
| Attivato dai seguenti eventi nel popover &quot;Cerca durante la digitazione&quot;:<br><br>Premi Invio, Fai clic su _Visualizza tutto_<br><br> Attivato dai seguenti eventi nelle pagine dei risultati di ricerca:<br><br>Seleziona un filtro, Modifica l&#39;ordinamento (_Ordina per_), Modifica la direzione di ordinamento (crescente o decrescente), Modifica il numero di risultati per pagina (_Mostra # per pagina_), Passa alla pagina successiva, Passa alla pagina precedente, Passa a una pagina diversa | `searchRequest` |

>[!NOTE]
>
>Gli eventi di ricerca non sono supportati in Adobe Commerce Enterprise Edition con l’estensione B2B installata.

#### Dati raccolti da searchRequestSent

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `searchRequest` | Indica se è stata inviata una richiesta di ricerca. |
| `searchRequest.id` | ID univoco per questa particolare richiesta di ricerca. |
| `searchRequest.value` | Valore quantificabile della richiesta. |
| `siteSearch` | Contiene informazioni sulla ricerca. |
| `siteSearch.filter` | Indica se sono stati applicati filtri per limitare i risultati della ricerca. |
| `siteSearch.filter.attribute` (filtro) | Facet di un elemento utilizzato per determinare se includerlo nei risultati di ricerca. |
| `siteSearch.filter.isRange` | Se è true, i valori indicano gli endpoint di un intervallo di valori accettabile. |
| `siteSearch.filter.value` | Valore attributo utilizzato per determinare quali elementi sono inclusi nei risultati di ricerca. |
| `siteSearch.sort` | Indica come ordinare i risultati della ricerca. |
| `siteSearch.sort.attribute` (ordinamento) | Attributo utilizzato per ordinare gli elementi nei risultati di ricerca. |
| `siteSearch.sort.order` | Ordine in cui restituire i risultati della ricerca. |
| `siteSearch.query` | Termini cercati. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### searchResponseReceived

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando Live Search restituisce i risultati per la pagina dei risultati di ricerca o popover &quot;cerca durante la digitazione&quot;. | `searchResponse` |

>[!NOTE]
>
>Gli eventi di ricerca non sono supportati in Adobe Commerce Enterprise Edition con l’estensione B2B installata.

#### Dati raccolti da searchResponseReceived

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `searchResponse` | Indica se è stata ricevuta una risposta di ricerca. |
| `searchResponse.id` | L’ID univoco per questa particolare risposta di ricerca. |
| `searchResponse.value` | Il valore quantificabile della risposta. |
| `siteSearch.numberOfResults` | Il numero di prodotti restituiti. |
| `siteSearch.suggestions` | Matrice di stringhe che includono i nomi di prodotti e categorie presenti nel catalogo simili alla query di ricerca. |
| `productListItems` | Un array di prodotti che sono stati aggiunti al carrello. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

## Eventi B2B

![B2B per Adobe Commerce](../assets/b2b.svg) Per i commercianti B2B, è necessario [installare](install.md#install-the-b2b-extension) l&#39;estensione `experience-platform-connector-b2b` per accedere a questi eventi.

Gli eventi B2B contengono [informazioni sull&#39;elenco di richieste](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html), ad esempio se è stato creato, aggiunto o eliminato un elenco di richieste. Tenendo traccia degli eventi specifici degli elenchi di richieste di acquisto, è possibile vedere quali prodotti i clienti acquistano frequentemente e creare campagne basate su tali dati.

### createRichiesteList

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente crea un elenco di richieste di acquisto. | `commerce.requisitionListOpens` |

#### Dati raccolti da createRichiesteList

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListOpens` | Indica l&#39;inizializzazione di un nuovo elenco di richieste. |
| `commerce.requisitionList` | Proprietà dell&#39;elenco di richieste di acquisto creato dal cliente. |
| `commerce.requisitionList.ID` | Identificatore univoco dell&#39;elenco di richieste di acquisto. |
| `commerce.requisitionList.name` | Nome dell&#39;elenco di richieste specificato dal cliente. |
| `commerce.requisitionList.description` | Descrizione dell&#39;elenco di richieste di acquisto specificato dal cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### addToRichiesteList

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente aggiunge un prodotto a un elenco di richieste di acquisto esistente o durante la creazione di un elenco. | `commerce.requisitionListAdds` |

#### Dati raccolti da addToRichiitionList

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListAdds` | Indica l&#39;aggiunta di uno o più prodotti a un elenco di richieste. |
| `commerce.requisitionList` | Proprietà dell&#39;elenco di richieste di acquisto creato dal cliente. |
| `commerce.requisitionList.ID` | Identificatore univoco dell&#39;elenco di richieste di acquisto. |
| `commerce.requisitionList.name` | Nome dell&#39;elenco di richieste specificato dal cliente. |
| `commerce.requisitionList.description` | Descrizione dell&#39;elenco di richieste di acquisto specificato dal cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Array di prodotti aggiunti all&#39;elenco delle richieste di acquisto. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |

### removeFromRichiesteList

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente rimuove un prodotto da un elenco di richieste di acquisto. | `commerce.requisitionListRemovals` |

#### Dati raccolti da removeFromRichiitionList

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requsitionListRemovals` | Indica la rimozione di uno o più prodotti da un elenco di richieste di acquisto. |
| `commerce.requisitionList` | Proprietà dell&#39;elenco di richieste di acquisto creato dal cliente. |
| `commerce.requisitionList.ID` | Identificatore univoco dell&#39;elenco di richieste di acquisto. |
| `commerce.requisitionList.name` | Nome dell&#39;elenco di richieste specificato dal cliente. |
| `commerce.requisitionList.description` | Descrizione dell&#39;elenco di richieste di acquisto specificato dal cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `productListItems` | Array di prodotti aggiunti all&#39;elenco delle richieste di acquisto. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |

### deleteRichiesteElenco

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente elimina un elenco di richieste di acquisto. | `commerce.requisitionListDeletes` |

#### Dati raccolti da deleteRichiitionList

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListDeletes` | Indica che un elenco di richieste di acquisto è stato eliminato. |
| `commerce.requisitionList` | Proprietà dell&#39;elenco di richieste di acquisto creato dal cliente. |
| `commerce.requisitionList.ID` | Identificatore univoco dell&#39;elenco di richieste di acquisto. |
| `commerce.requisitionList.name` | Nome dell&#39;elenco di richieste specificato dal cliente. |
| `commerce.requisitionList.description` | Descrizione dell&#39;elenco di richieste di acquisto specificato dal cliente. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
