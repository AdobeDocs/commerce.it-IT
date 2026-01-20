---
title: Raccogli dati
description: Scopri come gli eventi raccolgono i dati per  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---

# Raccogli dati

Quando installi e configuri [[!DNL Product Recommendations]](install-configure.md), il modulo distribuisce la raccolta di dati comportamentali nella vetrina. Questo meccanismo raccoglie dati comportamentali anonimi dagli acquirenti e potenzia [!DNL Product Recommendations]. Ad esempio, l&#39;evento `view` viene utilizzato per calcolare il tipo di consiglio `Viewed this, viewed that` e l&#39;evento `place-order` per calcolare il tipo di consiglio `Bought this, bought that`.

Per ulteriori informazioni sui dati comportamentali raccolti dagli eventi [, consulta la &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations)documentazione per sviluppatori[!DNL Product Recommendations].

>[!NOTE]
>
>La raccolta dei dati ai fini di [!DNL Product Recommendations] non include informazioni personali (PII). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi. Ulteriori informazioni [su](https://www.adobe.com/privacy/experience-cloud.html).

## Clienti del settore sanitario

Se sei un cliente del settore sanitario e hai installato l&#39;estensione [HIPAA Data Services](../data-connection/hipaa-readiness.md#installation), che fa parte dell&#39;estensione [Data Connection](../data-connection/overview.md), i dati dell&#39;evento storefront utilizzati da [!DNL Product Recommendations] non vengono più acquisiti. Questo perché i dati dell’evento storefront vengono generati lato client. Per continuare l&#39;acquisizione e l&#39;invio di dati evento vetrina, riattivare la raccolta eventi per [!DNL Product Recommendations]. Per ulteriori informazioni, consulta la [configurazione generale](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services).

## Tipi di dati ed eventi

Esistono due tipi di dati utilizzati in Product Recommendations:

- **Comportamento**: dati del coinvolgimento di un acquirente sul tuo sito, ad esempio visualizzazioni di prodotti, elementi aggiunti a un carrello e acquisti.
- **Catalogo** - Metadati del prodotto come nome, prezzo, disponibilità e così via.

Quando installi il modulo `magento/product-recommendations`, Adobe AI aggrega i dati comportamentali e di catalogo, creando consigli di prodotto per ogni tipo di consiglio. Il servizio Consigli di prodotto distribuisce quindi tali consigli nella vetrina sotto forma di un widget contenente il prodotto consigliato _elementi_.

Alcuni tipi di consigli utilizzano i dati comportamentali dei tuoi acquirenti per addestrare modelli di apprendimento automatico per creare consigli personalizzati. Altri tipi di consigli utilizzano solo i dati di catalogo e non utilizzano dati comportamentali. Se desideri iniziare rapidamente a utilizzare i consigli di prodotto sul tuo sito, puoi utilizzare i seguenti tipi di consigli solo catalogo:

- `More like this`
- `Visual similarity`

### Avvio a freddo

Quando puoi iniziare a utilizzare i tipi di consigli che utilizzano dati comportamentali? Dipende. Questo problema è denominato _Avvio a freddo_.

Il problema di _Avvio a freddo_ si riferisce al tempo necessario per l&#39;addestramento e l&#39;efficacia di un modello. Per i consigli di prodotto, significa attendere che Adobe AI raccolga un numero sufficiente di dati per addestrare i suoi modelli di apprendimento automatico prima di distribuire unità di consigli sul sito. Maggiore è il numero di dati di cui dispongono i modelli, più accurati e utili sono i consigli. Poiché la raccolta dati viene eseguita su un sito attivo, è consigliabile avviare questo processo in anticipo installando e configurando il modulo `magento/production-recommendations`.

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

Durante la raccolta dei dati sul sito live e l’apprendimento dei modelli di apprendimento automatico, puoi completare altre attività di test e configurazione necessarie per impostare i consigli. Al termine di questo lavoro, i modelli avranno a disposizione dati sufficienti per creare consigli utili e distribuirli nella vetrina.

Se il sito non riceve abbastanza traffico (visualizzazioni, acquisti, tendenze) per la maggior parte delle SKU di prodotto, potrebbero non esserci dati sufficienti per completare il processo di apprendimento. In questo modo l’indicatore di preparazione nell’amministratore potrebbe sembrare bloccato. Gli indicatori di preparazione hanno lo scopo di fornire agli esercenti un altro punto di dati nella scelta del tipo di consigli migliore per il negozio. I numeri sono una guida e potrebbero non raggiungere mai il 100%. [Ulteriori informazioni](create.md#readiness-indicators) sugli indicatori di preparazione.

### Raccomandazioni per il backup {#backuprecs}

Se i dati di input sono insufficienti per fornire tutti gli elementi dei consigli richiesti in un&#39;unità, Adobe Commerce fornisce consigli di backup per popolare le unità dei consigli. Ad esempio, se distribuisci il tipo di consiglio `Recommended for you` nella tua home page, un acquirente sul tuo sito non ha generato abbastanza dati comportamentali per consigliare accuratamente prodotti personalizzati. In questo caso, Adobe Commerce fa emergere a questo acquirente gli elementi in base al tipo di consiglio `Most viewed`.

In caso di raccolta dati di input insufficiente, i seguenti tipi di consigli eseguono il fallback al tipo di consiglio `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### Avvertenze

- Gli ad blocker e le impostazioni di privacy possono impedire l&#39;acquisizione degli eventi e causare la mancata generazione di rapporti per [metriche](workspace.md#column-descriptions) relative a coinvolgimento e ricavi. Inoltre, alcuni eventi potrebbero non essere inviati a causa di acquirenti che abbandonano la pagina o di problemi di rete.
- [Le implementazioni headless](headless.md) devono implementare gli eventi per alimentare il dashboard Consigli di prodotto.
- Per i prodotti configurabili, la funzione Consigli di prodotto utilizza l’immagine del prodotto principale nell’unità Consigli. Se per il prodotto configurabile non è stata specificata un’immagine, l’unità di consigli sarà vuota per quel prodotto specifico.

>[!NOTE]
>
>Se è abilitata la modalità di restrizione dei cookie [&#128279;](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html), Adobe Commerce non raccoglie i dati comportamentali fino a quando l&#39;acquirente non acconsente all&#39;utilizzo dei cookie. Se la modalità di restrizione dei cookie è disabilitata, Adobe Commerce raccoglie i dati comportamentali per impostazione predefinita.
