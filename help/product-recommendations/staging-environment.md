---
title: Test in ambiente di staging
description: Scopri come utilizzare  [!DNL Product Recommendations]  dall'ambiente di produzione nell'ambiente di staging a scopo di test.
feature: Services, Recommendations, Staging
exl-id: 5b6d7615-6021-4419-98ea-006c8a299fe4
TQID: https://experienceleague.adobe.com/7e7e3T-vgkN-Pbqx6TwrBAWTEozhzS0h--tguOGe0yI
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 436
ht-degree: 0%

---

# Test in ambiente di staging

Prima di implementare i consigli nell’ambiente di produzione, testa il servizio in un ambiente non di produzione per assicurarti che tutto funzioni come previsto.

[!DNL Product Recommendations] restituiscono i prodotti in base a [dati sul comportamento dell&#39;acquirente](events.md) raccolti dalla tua vetrina. In un ambiente non di produzione, tuttavia, è probabile che non siano presenti dati comportamentali provenienti dagli acquirenti. L&#39;unico tipo di consiglio che è possibile verificare senza dati comportamentali è `More like this`. Questo tipo di consiglio non richiede alcun dato di input, in quanto utilizza una corrispondenza diretta di somiglianza dei contenuti.

I seguenti tipi di consigli richiedono dati comportamentali:

- Articoli più visualizzati
- Ha visualizzato questo, ha visualizzato quello
- Ho comprato questo e quello

Come puoi testare i consigli in un ambiente non di produzione utilizzando i dati comportamentali? Ci sono un paio di opzioni.

## Recupera consigli dall’ambiente di produzione (scelta consigliata)

Adobe Commerce ti consente di recuperare i consigli dall&#39;ambiente di produzione e di visualizzarli in anteprima nell&#39;ambiente non di produzione [cambiando](settings.md) lo spazio dati SaaS.

Per recuperare i consigli dall’ambiente di produzione, è necessario assicurarsi che:

- La raccolta dati Storefront è [configurata e abilitata](install-configure.md) nell&#39;ambiente di produzione.
- Il catalogo nell’ambiente non di produzione è in gran parte lo stesso di quello nell’ambiente di produzione. L’utilizzo di cataloghi simili garantisce che i prodotti restituiti nelle unità di consigli rispecchino fedelmente quelli dell’ambiente di produzione.

## Generare dati comportamentali in ambienti non di produzione

1. Distribuire il modulo `magento/product-recommendations` in un ambiente non di produzione in cui i dati del catalogo sono simili a quelli del catalogo di produzione.

1. Utilizza uno degli ID spazio dati non di produzione per la [configurazione](../landing/saas.md#saas-configuration) nell&#39;amministratore.

1. Genera i dati da solo facendo clic sulla vetrina per simulare il comportamento degli acquirenti effettivi (o crea uno script di automazione). Attraverso i test, puoi generare eventi comportamentali nell’ambiente non di produzione. Tali eventi vengono utilizzati per produrre affinità di prodotto che alimentano le raccomandazioni. Per il test, [!DNL Commerce] consiglia di interagire con i seguenti tipi di consigli:

   - Più visualizzati: richiede un minimo di dati di input. Gli utenti devono visualizzare i prodotti.
   - Visualizzato questo, visto che - Richiede più utenti per visualizzare più prodotti.
   - Ha acquistato questo, acquistato che - Richiede più utenti per acquistare più prodotti.

### Avvertenze

- I dati comportamentali e di catalogo provenienti da [SaaS Data Space](../landing/saas.md#saas-configuration) non di produzione identificano un ambiente isolato in cui i prodotti consigliati risultanti si basano interamente sui dati comportamentali generati nella vetrina associata.

- Poiché non si dispone di grandi quantità di dati comportamentali, i dati di input per il calcolo delle associazioni di prodotti sono sparsi. Tuttavia, tali dati vengono comunque inviati a Sensei per calcolare i modelli di apprendimento automatico e fornire consigli in base ai dati generati in questo ambiente.
