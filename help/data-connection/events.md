---
title: Eventi comportamentali
description: Scopri i dati acquisiti da ogni evento comportamentale.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 631dfacd26a333e70a70f354d191d256d90d946f
workflow-type: tm+mt
source-wordcount: '402'
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

Gli eventi Storefront acquisiscono dati dalle interazioni degli acquirenti sul sito e includono eventi come `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut` e così via. Gli eventi Storefront si applicano solo a prodotti semplici e configurabili.

Per ulteriori informazioni sugli eventi storefront, consulta la [documentazione per sviluppatori](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection).

## Eventi profilo cliente

Gli eventi profilo acquisiti dalla vetrina includono informazioni sull&#39;account, ad esempio `signIn`, `signOut`, `createAccount` e `editAccount`. Questi dati vengono utilizzati per compilare i dettagli chiave dei clienti necessari per definire meglio i segmenti o eseguire campagne di marketing, ad esempio inviare offerte di sconto per l’iscrizione, conferme di modifica dell’account e così via.

Per ulteriori informazioni sugli eventi del profilo cliente, consulta la [documentazione per sviluppatori](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection).

## Cerca eventi

Gli eventi di ricerca forniscono dati rilevanti per l’intento dell’acquirente. Insight into a shopper&#39;s intent aiuta i commercianti a vedere come i consumatori sono alla ricerca di articoli, cosa fanno clic e alla fine acquistare o abbandonare. Un esempio di come puoi utilizzare questi dati è se desideri eseguire il targeting degli acquirenti esistenti che cercano il tuo prodotto principale, ma non acquistano mai il prodotto. Per accedere a questi eventi è necessario installare l&#39;estensione [[!DNL Live Search]](../live-search/install.md).

Utilizzare i campi `searchRequest.id` e `searchResponse.id` trovati negli eventi `searchRequestSent` e `searchResponseReceived` per creare un riferimento incrociato tra una richiesta di ricerca e la risposta di ricerca corrispondente.

Per ulteriori informazioni sugli eventi di ricerca, consulta la [documentazione per sviluppatori](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection).

## Eventi B2B

![B2B per Adobe Commerce](../assets/b2b.svg) Per i commercianti B2B, è necessario [installare](install.md#install-the-b2b-extension) l&#39;estensione `experience-platform-connector-b2b` per accedere a questi eventi.

Gli eventi B2B contengono [informazioni sull&#39;elenco di richieste](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html), ad esempio se è stato creato, aggiunto o eliminato un elenco di richieste. Tenendo traccia degli eventi specifici degli elenchi di richieste di acquisto, è possibile vedere quali prodotti i clienti acquistano frequentemente e creare campagne basate su tali dati.

Per ulteriori informazioni sugli eventi B2B, consulta la [documentazione per sviluppatori](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection).
