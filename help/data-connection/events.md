---
title: Eventi comportamentali
description: Scopri i dati acquisiti da ogni evento comportamentale.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
TQID: https://experienceleague.adobe.com/YS3jKQ3jmy76aeaqAp1PR8cGpD0euagdhoqL6CoMAnQ
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 467
ht-degree: 0%

---

# [!DNL Data Connection] eventi comportamentali

Nell&#39;elenco seguente sono elencati gli eventi comportamentali di Commerce disponibili quando si installa l&#39;estensione [!DNL Data Connection]. I dati raccolti da questi eventi vengono inviati a Adobe Experience Platform. Puoi anche creare [eventi personalizzati](custom-events.md) per raccogliere dati aggiuntivi non forniti come predefiniti.

Oltre ai dati raccolti dai seguenti eventi, si ottengono anche [altri dati](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=it) forniti da Adobe Experience Platform Web SDK.

Gli eventi comportamentali raccolgono dati comportamentali anonimi dagli acquirenti che navigano sul tuo sito. Puoi utilizzare i dati raccolti da questi eventi per creare promozioni e campagne indirizzate a un gruppo specifico di acquirenti.

>[!NOTE]
>
>Tutti gli eventi comportamentali includono il campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=it), che include l&#39;indirizzo e-mail dell&#39;acquirente, se disponibile, ed ECID.

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

Gli eventi B2B contengono [informazioni sull&#39;elenco di richieste](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=it), ad esempio se è stato creato, aggiunto o eliminato un elenco di richieste. Tenendo traccia degli eventi specifici degli elenchi di richieste di acquisto, è possibile vedere quali prodotti i clienti acquistano frequentemente e creare campagne basate su tali dati.

Per ulteriori informazioni sugli eventi B2B, consulta la [documentazione per sviluppatori](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection).
