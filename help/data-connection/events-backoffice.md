---
title: Eventi di back office
description: Scopri i dati acquisiti da ogni evento di back office.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '3606'
ht-degree: 0%

---

# [!DNL Data Connection] eventi di back office

Nell&#39;elenco seguente sono elencati gli eventi di back office di Commerce disponibili quando si installa l&#39;estensione [!DNL Data Connection]. I dati raccolti da questi eventi vengono inviati a Adobe Experience Platform. Puoi anche creare [eventi personalizzati](custom-events.md) per raccogliere dati aggiuntivi non forniti come predefiniti.

Oltre ai dati raccolti dai seguenti eventi, si ottengono anche [altri dati](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) forniti da Adobe Experience Platform Web SDK.

Gli eventi di back office contengono dati lato server. Questi dati comprendono [informazioni sullo stato dell&#39;ordine](#order-status), ad esempio se un ordine è stato effettuato, annullato, rimborsato, spedito o completato. I dati lato server includono anche [informazioni sugli eventi del profilo cliente](#customer-profile-events), ad esempio se è stato creato, aggiornato o eliminato un account.

>[!NOTE]
>
>Tutti gli eventi di back office includono il campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html), che include l&#39;indirizzo e-mail dell&#39;acquirente, se disponibile, e ECID.

## Stato ordine

I dati sullo stato dell&#39;ordine mostrano una visualizzazione 360 dell&#39;ordine cliente. Questa visualizzazione consente ai commercianti di eseguire meglio il targeting o analizzare l’intero stato dell’ordine durante lo sviluppo di campagne di marketing. Ad esempio, puoi individuare le tendenze in determinate categorie di prodotti che ottengono risultati ottimali in momenti diversi dell’anno. Ad esempio, vestiti invernali che vendono meglio durante i mesi più freddi o alcuni colori di prodotto che gli acquirenti sono interessati negli anni. Inoltre, i dati sullo stato dell&#39;ordine possono essere utili per calcolare il valore del cliente per tutta la sua durata comprendendo la propensione di un acquirente a eseguire la conversione in base agli ordini precedenti.

### orderPlaced

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente effettua un ordine. | `commerce.backofficeOrderPlaced` |

#### Dati raccolti da orderPlaced

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.paymentTransactionID` | Identificatore univoco per questa transazione di pagamento. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.order.payments.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.taxAmount` | Importo dell&#39;imposta pagato dall&#39;acquirente come parte del pagamento finale. |
| `commerce.order.discountAmount` | Indica l&#39;importo dello sconto applicato all&#39;intero ordine. |
| `commerce.order.createdDate` | L’ora e la data di creazione di un nuovo ordine nel sistema commerce. Ad esempio, `2022-10-15T20:20:39+00:00`. |
| `commerce.order.currencyCode` | Il codice valuta ISO 4217 utilizzato per i totali dell’ordine. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |
| `commerce.shipping.currencyCode` | Il codice valuta ISO 4217 utilizzato per il totale delle spedizioni. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `commerce.billing.address` | Indirizzo postale di fatturazione. |
| `commerce.billing.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada |
| `commerce.billing.address.street2` | Campo aggiuntivo per informazioni a livello stradale. |
| `commerce.billing.address.city` | Il nome della città. |
| `commerce.billing.address.state` | Nome dello stato. Questo è un campo in formato libero. |
| `commerce.billing.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.billing.address.country` | Il nome del territorio amministrato dal governo. A parte `xdm:countryCode`, questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.id` | L’identificatore di riga per questa voce di prodotto. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |
| `productListItems.productImageUrl` | URL immagine principale del prodotto. |

### orderInvoiced

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un commerciante presenta una fattura per richiedere il pagamento. | `commerce.backofficeOrderInvoiced` |

#### Dati raccolti da orderInvoiced

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.priceTotal` | Il prezzo totale dell&#39;ordine dopo l&#39;applicazione di tutti gli sconti e le imposte. |
| `commerce.order.currencyCode` | Il codice valuta ISO 4217 utilizzato per i totali dell’ordine. |
| `commerce.order.purchaseOrderNumber` | Identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.id` | L’identificatore di riga per questa voce di prodotto. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |

### orderItemsShipped

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando viene spedito un ordine. | `commerce.backofficeOrderItemsShipped` |

#### Dati raccolti da orderItemsShipped

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.paymentTransactionID` | Identificatore univoco per questa transazione di pagamento. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.order.payments.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.priceTotal` | Il prezzo totale dell&#39;ordine dopo l&#39;applicazione di tutti gli sconti e le imposte. |
| `commerce.order.purchaseOrderNumber` | Identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |
| `commerce.order.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.lastUpdatedDate` | L’ora dell’ultimo aggiornamento di un determinato record dell’ordine nel sistema commerciale. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |
| `commerce.shipping.address` | L&#39;indirizzo fisico di spedizione. |
| `commerce.shipping.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada. |
| `commerce.shipping.address.street2` | Seconda riga facoltativa sulle informazioni stradali. |
| `commerce.shipping.address.city` | Il nome della città. |
| `commerce.shipping.address.state` | Il nome dello Stato. Questo è un campo in formato libero. |
| `commerce.shipping.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.shipping.address.country` | Il nome del territorio amministrato dal governo. A parte `xdm:countryCode`, questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| `commerce.shipping.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.shipping.trackingNumber` | Il numero di registrazione fornito dal vettore di spedizione per una spedizione dell&#39;articolo dell&#39;ordine. |
| `commerce.shipping.trackingURL` | URL per tenere traccia dello stato di spedizione di un articolo dell&#39;ordine. |
| `commerce.shipping.shipDate` | Data di spedizione di uno o più articoli di un ordine. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `commerce.billing.address` | Indirizzo postale di fatturazione. |
| `commerce.billing.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada |
| `commerce.billing.address.street2` | Campo aggiuntivo per informazioni a livello stradale. |
| `commerce.billing.address.city` | Il nome della città. |
| `commerce.billing.address.state` | Nome dello stato. Questo è un campo in formato libero. |
| `commerce.billing.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.billing.address.country` | Il nome del territorio amministrato dal governo. A parte `xdm:countryCode`, questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |

### orderCanceled

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente annulla un ordine. | `commerce.backofficeOrderCancelled` |

#### Dati raccolti da orderCanceled

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.purchaseOrderNumber` | Identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |
| `commerce.order.cancelDate` | La data e l’ora in cui un acquirente annulla un ordine. |
| `commerce.order.lastUpdatedDate` | L’ora dell’ultimo aggiornamento di un determinato record dell’ordine nel sistema commerciale. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |

### orderLineItemRereturned

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente viene rimborsato per un articolo restituito. | `commerce.backofficeCreditMemoIssued` |

#### Dati raccolti da orderLineItemRereturned

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.lastUpdatedDate` | L’ora dell’ultimo aggiornamento di un determinato record dell’ordine nel sistema commerciale. |
| `commerce.order.purchaseOrderNumber` | Identificatore univoco assegnato dall’acquirente a questo acquisto o contratto. |
| `commerce.refunds` | Elenco dei rimborsi per questo ordine. |
| `commerce.refunds.transactionID` | Identificatore univoco per questo rimborso. |
| `commerce.refunds.refundAmount` | Il valore del rimborso. |
| `commerce.refunds.refundPaymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.refunds.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |

### orderItemsReturnInitiated

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente richiede di restituire un elemento. | `commerce.backofficeOrderItemsReturnInitiated` |

#### Dati raccolti da orderItemsReturnInitiated

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.returns` | Le informazioni RMA (Return Merchandise Authorization) per questo ordine. |
| `commerce.order.returns.returnID` | L&#39;identificatore univoco di questa RMA (Return Merchandise Authorization). |
| `commerce.order.returns.returnStatus` | Lo stato della RMA (Return Merchandise Authorization), ad esempio In sospeso, Chiuso e così via. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |
| `productListItems.returnItem` | Le informazioni RMA (Return Merchandise Authorization) per questo oggetto. |
| `productListItems.returnItem.returnStatus` | Lo stato dell&#39;elemento restituito, ad esempio In sospeso, Approvato e così via. |
| `productListItems.returnItem.returnReason` | Motivo per cui è richiesta una restituzione per questo oggetto. |
| `productListItems.returnItem.returnItemCondition` | La condizione dell&#39;elemento per cui viene richiesta la restituzione. |
| `productListItems.returnItem.returnResolution` | La risoluzione richiesta dell&#39;articolo restituito, ad esempio Rimborso, Scambio e così via. |
| `productListItems.returnItem.returnQuantityRequested` | Il numero di questo oggetto che l&#39;acquirente ha richiesto di restituire. |
| `productListItems.returnItem.returnQuantityAuthorized` | Il numero di questo elemento che può essere restituito. |
| `productListItems.returnItem.eturnQuantityReceived` | Numero di elementi restituiti ricevuti. |
| `productListItems.returnItem.returnQuantityApproved` | Il numero di questo oggetto con restituzione completa e approvata. |

### orderItemReturnCompleted

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando viene completato un elemento che un acquirente ha richiesto di restituire. | `commerce.backofficeOrderItemsReturnCompleted` |

#### Dati raccolti da orderItemReturnCompleted

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.returns` | Le informazioni RMA (Return Merchandise Authorization) per questo ordine. |
| `commerce.order.returns.returnID` | L&#39;identificatore univoco di questa RMA (Return Merchandise Authorization). |
| `commerce.order.returns.returnStatus` | Lo stato della RMA (Return Merchandise Authorization), ad esempio In sospeso, Chiuso e così via. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |
| `productListItems.returnItem` | Le informazioni RMA (Return Merchandise Authorization) per questo oggetto. |
| `productListItems.returnItem.returnStatus` | Lo stato dell&#39;elemento restituito, ad esempio In sospeso, Approvato e così via. |
| `productListItems.returnItem.returnReason` | Motivo per cui è richiesta una restituzione per questo oggetto. |
| `productListItems.returnItem.returnItemCondition` | La condizione dell&#39;elemento per cui viene richiesta la restituzione. |
| `productListItems.returnItem.returnResolution` | La risoluzione richiesta dell&#39;articolo restituito, ad esempio Rimborso, Scambio e così via. |
| `productListItems.returnItem.returnQuantityRequested` | Il numero di questo oggetto che l&#39;acquirente ha richiesto di restituire. |
| `productListItems.returnItem.returnQuantityAuthorized` | Il numero di questo elemento che può essere restituito. |
| `productListItems.returnItem.eturnQuantityReceived` | Numero di elementi restituiti ricevuti. |
| `productListItems.returnItem.returnQuantityApproved` | Il numero di questo oggetto con restituzione completa e approvata. |

### orderShipmentCompleted

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione al completamento di una spedizione. | `commerce.backofficeOrderShipmentCompleted` |

#### Dati raccolti da orderShipmentCompleted

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `commerce.order` | Contiene informazioni sull’ordine. |
| `commerce.order.purchaseID` | Identificatore univoco assegnato dal venditore per questo acquisto o contratto. Non c&#39;è alcuna garanzia che l&#39;ID sia univoco. |
| `commerce.order.payments` | Elenco dei pagamenti per questo ordine. |
| `commerce.order.payments.paymentTransactionID` | Identificatore univoco per questa transazione di pagamento. |
| `commerce.order.payments.paymentAmount` | Il valore del pagamento. |
| `commerce.order.payments.paymentType` | Il metodo di pagamento per questo ordine. Conteggiato, sono consentiti valori personalizzati. |
| `commerce.order.payments.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `commerce.order.taxAmount` | Importo dell&#39;imposta pagato dall&#39;acquirente come parte del pagamento finale. |
| `commerce.order.createdDate` | L’ora e la data di creazione di un nuovo ordine nel sistema commerce. Ad esempio, `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Dettagli di spedizione per uno o più prodotti. |
| `commerce.shipping.shippingMethod` | Il metodo di spedizione scelto dal cliente, ad esempio consegna standard, consegna rapida, ritiro in negozio e così via. |
| `commerce.shipping.shippingAmount` | L&#39;importo che il cliente ha dovuto pagare per la spedizione. |
| `commerce.shipping.shipDate` | Data di spedizione di uno o più articoli di un ordine. |
| `commerce.shipping.address` | L&#39;indirizzo fisico di spedizione. |
| `commerce.shipping.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada. |
| `commerce.shipping.address.street2` | Seconda riga facoltativa sulle informazioni stradali. |
| `commerce.shipping.address.city` | Il nome della città. |
| `commerce.shipping.address.state` | Il nome dello Stato. Questo è un campo in formato libero. |
| `commerce.shipping.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.shipping.address.country` | Il nome del territorio amministrato dal governo. A parte `xdm:countryCode`, questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| `commerce.billing.address` | Indirizzo postale di fatturazione. |
| `commerce.billing.address.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada |
| `commerce.billing.address.street2` | Campo aggiuntivo per informazioni a livello stradale. |
| `commerce.billing.address.city` | Il nome della città. |
| `commerce.billing.address.state` | Nome dello stato. Questo è un campo in formato libero. |
| `commerce.billing.address.postalCode` | Il codice postale della località. I codici postali non sono disponibili per tutti i paesi. In alcuni paesi, questa conterrà solo una parte del codice postale. |
| `commerce.billing.address.country` | Il nome del territorio amministrato dal governo. A parte `xdm:countryCode`, questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `productListItems` | Array di prodotti nell’ordine. |
| `productListItems.SKU` | Unità di stoccaggio. L’identificatore univoco del prodotto. |
| `productListItems.name` | Il nome visualizzato o leggibile del prodotto. |
| `productListItems.priceTotal` | Il prezzo totale per la voce di prodotto. |
| `productListItems.quantity` | Il numero di unità prodotto nel carrello. |
| `productListItems.discountAmount` | Indica l&#39;importo dello sconto applicato. |
| `productListItems.currencyCode` | Codice valuta [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) utilizzato, ad esempio `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizzato per un prodotto configurabile. |
| `productListItems.selectedOptions.attribute` | Identifica un attributo del prodotto configurabile, ad esempio `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica il valore dell&#39;attributo come `small` o `black`. |
| `productListItems.categories` | Contiene informazioni sulla categoria di un prodotto. |
| `productListItems.categories.id` | L’identificatore univoco della categoria. |
| `productListItems.categories.name` | Nome della categoria. |
| `productListItems.categories.path` | Percorso della categoria. |

## Eventi profilo cliente

Gli eventi profilo acquisiti dal lato server includono informazioni sull&#39;account, ad esempio `accountCreated`, `accountUpdated` e `accountDeleted`. Questi dati vengono utilizzati per compilare i dettagli chiave dei clienti necessari per definire meglio i segmenti o eseguire campagne di marketing, ad esempio inviare offerte di sconto per l’iscrizione, conferme di modifica dell’account e così via. Sono presenti eventi di profilo simili acquisiti dalla [vetrina](events.md#customer-profile-events).

>[!NOTE]
>
>Ogni evento del profilo cliente include anche il campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html), che include l&#39;ID cliente Commerce generato dal sistema come identificatore primario del profilo e un ID e-mail utilizzato come identificatore secondario.

### accountCreated

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di creare un account. | `userAccount.backofficeCreateProfile` |

#### Dati raccolti da accountCreated

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `person` | Contiene informazioni sul cliente. |
| `person.name` | Contiene informazioni sul nome del cliente. |
| `person.name.firstName` | Contiene il nome del cliente. |
| `person.name.lastName` | Contiene il cognome del cliente. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### accountUpdated

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di modificare un account. | `userAccount.backofficeUpdateProfile` |

#### Dati raccolti dall&#39;accountUpdated

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `person` | Contiene informazioni sul cliente. |
| `person.name` | Contiene informazioni sul nome del cliente. |
| `person.name.firstName` | Contiene il nome del cliente. |
| `person.name.lastName` | Contiene il cognome del cliente. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |

### accountDeleted

| Descrizione | Nome evento XDM |
|---|---|
| Attivazione quando un acquirente tenta di eliminare un account. | `userAccount.backofficeDeleteProfile` |

#### Dati raccolti da accountDeleted

Nella tabella seguente sono descritti i dati raccolti per questo evento.

| Campo | Descrizione |
|---|---|
| `person` | Contiene informazioni sul cliente. |
| `person.name` | Contiene informazioni sul nome del cliente. |
| `person.name.firstName` | Contiene il nome del cliente. |
| `person.name.lastName` | Contiene il cognome del cliente. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `commerce.commerceScope` | Indica dove si è verificato un evento (visualizzazione store, store, sito Web e così via). |
| `commerce.commerceScope.environmentID` | ID ambiente. Un ID alfanumerico di 32 cifre separato da un trattino. |
| `commerce.commerceScope.storeCode` | Il codice univoco dell’archivio. Puoi avere molti negozi per sito web. |
| `commerce.commerceScope.storeViewCode` | Il codice univoco della visualizzazione store. Puoi avere molte visualizzazioni per negozio. |
| `commerce.commerceScope.websiteCode` | Il codice univoco del sito web. In un ambiente possono essere presenti molti siti Web. |
