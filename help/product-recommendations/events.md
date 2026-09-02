---
title: Raccogli dati
description: Scopri come gli eventi raccolgono i dati per  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
TQID: https://experienceleague.adobe.com/efHRMj3u3w-xvUgMnEYDpX0D-BDCUyjhhrkMaa3n-xg
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: eb30f47f-d87a-400f-8f78-63ce7979ff56id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 937
ht-degree: 0%

---

# Raccogli dati

Quando installi e configuri [[!DNL Product Recommendations]](install-configure.md), il modulo distribuisce la raccolta di dati comportamentali nella vetrina. Questo meccanismo raccoglie dati comportamentali anonimi dagli acquirenti e potenzia [!DNL Product Recommendations]. Ad esempio, l&#39;evento `view` viene utilizzato per calcolare il tipo di consiglio `Viewed this, viewed that` e l&#39;evento `place-order` per calcolare il tipo di consiglio `Bought this, bought that`.

Per ulteriori informazioni sui dati comportamentali raccolti dagli eventi [!DNL Product Recommendations], consulta la [documentazione per gli sviluppatori](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations).

>[!NOTE]
>
>La raccolta dei dati ai fini di [!DNL Product Recommendations] non include informazioni personali (PII). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi. Ulteriori informazioni [su](https://www.adobe.com/privacy/experience-cloud.html).

## Clienti del settore sanitario

Se sei un cliente del settore sanitario e hai installato l&#39;estensione [HIPAA Data Services](../data-connection/hipaa-readiness.md#installation), inclusa con l&#39;estensione [Data Connection](../data-connection/overview.md), [!DNL Product Recommendations] non raccoglie più i dati dell&#39;evento storefront perché sono generati sul lato client.

Per riprendere la raccolta e l&#39;invio dei dati evento vetrina, riattivare la raccolta eventi per [!DNL Product Recommendations]. Per ulteriori informazioni, vedere [Configurazione generale](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services).

## Tipi di dati ed eventi

Esistono due tipi di dati utilizzati in Product Recommendations:

- **Comportamento**: dati del coinvolgimento di un acquirente sul tuo sito, ad esempio visualizzazioni di prodotti, elementi aggiunti a un carrello e acquisti.
- **Catalogo** - Metadati del prodotto come nome, prezzo, disponibilità e così via.

Quando installi il modulo `magento/product-recommendations`, Adobe AI aggrega i dati comportamentali e di catalogo e crea consigli di prodotto per ogni tipo di consiglio. Il servizio Consigli di prodotto distribuisce quindi tali consigli nella vetrina sotto forma di un widget contenente il prodotto consigliato _elementi_.

Alcuni tipi di consigli utilizzano i dati comportamentali degli acquirenti per addestrare modelli di apprendimento automatico e generare consigli personalizzati. Altri si basano solo sui dati del catalogo. Per iniziare a utilizzare rapidamente i consigli di prodotto, scegli uno dei seguenti tipi di consigli per il solo catalogo:

- `More like this`
- `Visual similarity`

### Avvio a freddo

Quando puoi iniziare a utilizzare i tipi di consigli che utilizzano dati comportamentali? Dipende. Questa situazione è definita problema di _Avvio a freddo_.

Il problema di _Avvio a freddo_ è il tempo necessario per l&#39;addestramento di un modello di apprendimento automatico prima che possa produrre consigli efficaci. Per i consigli di prodotto, Adobe AI deve raccogliere un numero sufficiente di dati per addestrare i suoi modelli prima di distribuire le unità di consigli. Più dati in genere migliorano l’accuratezza e l’utilità dei consigli. Poiché la raccolta dei dati si verifica nel sito attivo, avviare questo processo in anticipo installando e configurando il modulo `magento/product-recommendations`.

La tabella seguente fornisce alcune indicazioni generali sul tempo necessario per raccogliere dati sufficienti per ogni tipo di consiglio:

| Tipo di consiglio | Tempo di formazione | Note |
|---|---|---|
| Basato sulla popolarità (`Most viewed`, `Most purchased`, `Most added to cart`) | Varia | Dipende dal volume degli eventi: le visualizzazioni sono più comuni e quindi apprende più rapidamente; quindi aggiunge al carrello, quindi acquista |
| `Viewed this, viewed that` | Richiede più formazione | Il volume delle visualizzazioni dei prodotti è decisamente elevato |
| `Viewed this, bought that`, `Bought this, bought that` | Richiede il massimo della formazione | Gli eventi di acquisto sono gli eventi più rari su un sito di e-commerce, in particolare rispetto alle visualizzazioni di prodotto |
| `Trending` | Richiede tre giorni di dati per stabilire una baseline di popolarità | Il trend è una misura dello slancio recente nella popolarità di un prodotto rispetto alla sua linea di base di popolarità. Il punteggio di tendenza di un prodotto viene calcolato utilizzando un set in primo piano (popolarità recente superiore a 24 ore) e un set in background (linea di base di popolarità superiore a 72 ore). Se la popolarità di un elemento aumenta in modo significativo entro un periodo di 24 ore rispetto alla popolarità al basale, allora riceve un punteggio di tendenza elevato. Ogni prodotto ha questo punteggio e gli elementi con il punteggio più alto in qualsiasi momento comprendono il set di prodotti con tendenze migliori. |

Altre variabili che possono influire sul tempo necessario per la formazione:

- Un volume di traffico più elevato contribuisce a un apprendimento più rapido
- Alcuni tipi di consigli si addestrano più rapidamente di altri
- Adobe Commerce ricalcola i dati comportamentali ogni quattro ore. I consigli diventano più precisi quanto più a lungo vengono utilizzati sul sito.

Per aiutarti a visualizzare l&#39;avanzamento della formazione di ciascun tipo di consiglio, la pagina [crea consiglio](create.md#readiness-indicators) visualizza gli indicatori di preparazione.

Mentre il tuo sito live raccoglie dati e i modelli di apprendimento automatico si addestrano, completa le altre attività di test e configurazione. Una volta che i modelli hanno abbastanza dati per generare consigli utili, distribuisci le unità di consigli nella vetrina.

Se il sito non riceve abbastanza traffico (visualizzazioni, acquisti o tendenze) per la maggior parte delle SKU di prodotto, il processo di apprendimento potrebbe non essere completato, causando il blocco degli indicatori di preparazione nell’amministratore. Gli indicatori di preparazione aiutano i commercianti a scegliere il tipo di consiglio migliore per il loro negozio, ma sono solo una guida e potrebbero non raggiungere mai il 100%. Ulteriori informazioni sugli indicatori di preparazione. [Ulteriori informazioni](create.md#readiness-indicators) sugli indicatori di preparazione.

### Raccomandazioni per il backup {#backuprecs}

Se i dati di input sono insufficienti e un’unità di consigli non è in grado di restituire tutti gli elementi richiesti, Adobe Commerce le riempie di consigli di backup. Ad esempio, dopo aver distribuito il tipo di consiglio `Recommended for you` nella home page, un acquirente alle prime armi potrebbe non aver generato abbastanza dati comportamentali per i consigli personalizzati. In questo caso, Adobe Commerce visualizza gli elementi in base al tipo di consiglio `Most viewed `.

Se la raccolta dei dati di input non è sufficiente, i seguenti tipi di consigli eseguono il fallback al tipo di consiglio `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### Avvertenze

- Gli ad blocker e le impostazioni di privacy possono impedire l&#39;acquisizione degli eventi e causare la mancata generazione di rapporti per [metriche](workspace.md#column-descriptions) relative a coinvolgimento e ricavi. Inoltre, alcuni eventi non vengono inviati a causa di acquirenti che escono dalla pagina o a causa di problemi di rete.
- [Le implementazioni headless](headless.md) devono implementare gli eventi per alimentare il dashboard Consigli di prodotto.
- Per i prodotti configurabili, la funzione Consigli di prodotto utilizza l’immagine del prodotto principale. Se il prodotto principale non ha alcuna immagine, tale prodotto non viene visualizzato nell’unità di consigli.

>[!NOTE]
>
>Se è abilitata la modalità di restrizione dei cookie [](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law), Adobe Commerce non raccoglie i dati comportamentali fino a quando l&#39;acquirente non acconsente all&#39;utilizzo dei cookie. Se la modalità di restrizione dei cookie è disabilitata, Adobe Commerce raccoglie i dati comportamentali per impostazione predefinita.
