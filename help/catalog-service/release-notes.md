---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: Informazioni aggiornate sulla versione di  [!DNL Catalog Service]  per Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
TQID: https://experienceleague.adobe.com/-yxW4sTuk7LPjGy5YsQ65phtkBLiByg8SmBaQPHMevM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 616ad9e9b45a66f127a55ef87dd6c6b9c0b470c8
workflow-type: tm+mt
source-wordcount: 3024
ht-degree: 0%

---

# Note sulla versione [!DNL Commerce Storefront Catalog Service]

Queste note sulla versione descrivono gli ultimi aggiornamenti di Commerce Catalog Service, inclusi:

- **[Versioni di Storefront Catalog Service](#storefront-catalog-service)**

   - Miglioramenti allo schema API di Catalog Service per un migliore recupero dei dati
   - Miglioramenti a livello di sicurezza, prestazioni e affidabilità per l’API Catalog Service e l’infrastruttura sottostante.

  Per ulteriori informazioni su queste API, consulta [Schema servizi Storefront](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/) nella documentazione di Commerce Developer.

- **[Versioni del metapacchetto Catalog Service](#catalog-service-metapackage)**

   - Sono state aggiornate le dipendenze per migliorare le prestazioni, la stabilità e la compatibilità con altri componenti di Adobe Commerce.

- **[Versioni del programma di installazione di Catalog Service](#catalog-service-installer)**

   - Sono state aggiornate le dipendenze per mantenere la compatibilità tra Catalog Service e lo stack Commerce.

>[!NOTE]
>
>Se il progetto Commerce utilizza Adobe Commerce Optimizer per inviare i dati del catalogo a Commerce Edge Delivery Service o headless storefront, consulta le [note sulla versione di Adobe Commerce Optimizer](../optimizer/release-notes.md) per gli ultimi aggiornamenti API.

Gli aggiornamenti sono suddivisi per tipo:

![Nuove](../assets/new.svg) nuove funzionalità
![Correzioni](../assets/fix.svg) correzioni e miglioramenti
![Bug](../assets/bug.svg) problemi noti

È disponibile il supporto per la versione più recente. Sono incluse per riferimento le note sulla versione per le versioni precedenti.

## Servizio catalogo vetrina

## Giugno 2026

**Data di rilascio**: 1 luglio 2026

![Nuovo](../assets/new.svg) **Nuovo campo `canEditQuantity`**—Aggiunto `canEditQuantity` a `ProductViewOptionValueProduct` in Catalog Service GraphQL. Espone l&#39;impostazione facoltativa della quantità **Definita dall&#39;utente** per le selezioni del bundle dall&#39;amministratore Commerce, in modo che i consumatori di vetrina possano determinare se la quantità di una selezione del bundle è modificabile.

### Maggio 2026

**Data di rilascio**: 20 maggio 2026
<!-- v1.55 -->

![Nuovo](../assets/new.svg) Limite massimo imposto di 100 SKU per richiesta per i client Adobe Commerce e Adobe Commerce as a Cloud Service, in base a [limiti e limiti documentati](https://experienceleague.adobe.com/it/docs/commerce/optimizer/boundaries-limits).


**Data di rilascio**: 13 maggio 2026


![Nuovo](../assets/new.svg) **Ordinamento categorie in GraphQL**. Il tipo di GraphQL `CategoryView` include ora un campo posizione, pertanto gli storefront possono visualizzare le categorie nell&#39;ordine configurato dai commercianti nella gerarchia del catalogo.


**Data di rilascio**: 4 maggio 2026
<!-- v1.53 -->

![Correzione](../assets/fix.svg) I prezzi dei prodotti della vetrina ora visualizzano il codice valuta corretto (ad esempio, USD) per tutti i tipi di prodotto. In precedenza, alcuni prodotti mostravano `NONE` invece della valuta prevista, con conseguente perdita dei prezzi. Questo aggiornamento garantisce un rendering dei prezzi coerente e accurato in tutta la vetrina.<!--DATA-7115-->

### Aprile 2026

**Data di rilascio**: 29 aprile 2026


![Nuovo](../assets/new.svg) Limite massimo imposto di 100 SKU per richiesta per Adobe Commerce Optimizer e Adobe Commerce as a Cloud Service
client in base a [limiti e limiti documentati](https://experienceleague.adobe.com/it/docs/commerce/optimizer/boundaries-limits). <!--DATA-7156-->

**Data di rilascio**: 17 aprile 2026


![Nuovo](../assets/new.svg) aggiunta nuova query di GraphQL `searchCategory` che consente ai client di cercare le categorie per nome con risultati impaginati. La query accetta i parametri obbligatori `searchTerm` (minimo 3 caratteri) e facoltativi `family`, `pageSize` e `currentPage`. I risultati includono `CategoryTreeView` oggetti corrispondenti con metadati di categoria completi, `totalCount` e `pageInfo` per l&#39;impaginazione. <!--COMOPT-1819-->

Questa query è disponibile solo per i clienti che utilizzano Adobe Commerce Optimizer Merchandising Services. Vedi [searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/).

### Marzo 2026

**Data di rilascio**: 24 marzo 2026


![Nuovo](../assets/new.svg) Aggiunto supporto per calcolare e restituire l&#39;intervallo di prezzo per i bundle dinamici.


### Dicembre 2025

**Data di rilascio**: 11 dicembre 2025
<!-- v1.46 -->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare prestazioni e stabilità.


### Novembre 2025

**Data di rilascio**: 17 novembre 2025
<!-- v1.45 -->

![Nuovo](../assets/new.svg) **Filtro attributi per nome**-La query di GraphQL `productSearch` ora supporta il filtro degli attributi di prodotto con il campo `names`. <!--DATA-6831--> Con questo filtro, puoi:

- Riduci la dimensione del payload di risposta richiedendo solo attributi specifici
- Combina con il filtro `roles` esistente per restringere per ruolo di visibilità e nome attributo
- Esempi:

  **Filtra solo per nomi di attributo**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **Filtra per ruoli e nomi:**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>Per recuperare tutti gli attributi senza filtro, omettere l&#39;argomento `names` o fornire una matrice vuota.

**Data di rilascio**: 6 novembre 2025
<!-- v1.44 -->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare prestazioni e stabilità. <!--DATA-6852, DATA-6864-->

![Correzione](../assets/fix.svg) È ora possibile eseguire una query sui prodotti raggruppati quando il padre non ha alcun prezzo; i prodotti secondari restituiscono i propri ruoli di visibilità.<!--DATA-6779-->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare prestazioni e stabilità. <!--DATA-6721, DATA-6864-->

### Settembre 2025

**Data di rilascio**: 8 settembre 2025
<!-- v1.42 -->

![Nuovo](../assets/new.svg) **Aggiunta del supporto per la determinazione dei prezzi per il livello** per la determinazione dei prezzi per il volume delle query:<!--DATA-6643-->

Per recuperare i prezzi dei livelli:

1. Utilizza la query `products` con gli SKU desiderati
2. Per **SimpleProductView**, accedere a `price.tiers`
3. Per **ComplexProductView**, accedere a `priceRange.minimum.tiers` e `priceRange.maximum.tiers`
4. Ogni livello contiene il prezzo scontato `tier` e le condizioni `quantity`
5. Definisci soglie quantità con `gte` (maggiore o uguale a) e `lt` (minore di)

**Esempio:**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![Correzione](../assets/fix.svg) **I prezzi di livello sono filtrati in base al prezzo finale minimo** <!--DATA-6643-->

L&#39;API ora restituisce solo i livelli il cui prezzo scontato è **inferiore al** prezzo finale minimo del prodotto. I livelli più alti vengono omessi perché il prezzo finale minimo si applicherebbe invece alla vetrina.

Si applica a:

- **Prodotti semplici**: `price.tiers` include solo livelli con `tier.amount.value` &lt; `price.final.amount.value` (minimo finale).
- **Prodotti complessi**: `priceRange.minimum.tiers` e `priceRange.maximum.tiers` utilizzano la stessa regola per la creazione dell&#39;intervallo di prezzi.

**Data di rilascio**: 2 settembre 2025
<!-- v1.41 -->

![Correzione](../assets/fix.svg) **È stata migliorata la gestione degli errori per le informazioni sul prezzo mancanti**. Quando i dati sul prezzo non vengono ancora ricevuti, l&#39;API restituisce `null` per il campo del prezzo invece di generare un errore, consentendo ai client di gestire i dati mancanti in modo corretto.<!--DATA-6612-->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare le prestazioni e la stabilità.<!--DATA-6671-->

### Luglio 2025

**Data di rilascio**: 30 luglio 2025
<!-- v1.40 -->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6619-->

**Data di rilascio**: 24 luglio 2025
<!-- v1.39 -->

![Nuovo](../assets/new.svg) **Recupera unità di consigli per ID unità**-Il nuovo endpoint GraphQL `recommendationsByUnitIds` recupera le unità di consigli in base al loro ID univoco per un accesso più flessibile e mirato.

- `unitIds` è obbligatorio (elenco di recId da recuperare).
- I parametri di contesto (`currentSku`, `cartSkus`, `userViewHistory`, `userPurchaseHistory`, `category`) si comportano come nella query di consigli esistente.

- **Esempio**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6316-->

**Data di rilascio**: 15 luglio 2025
<!-- v1.38 -->

![Nuovo](../assets/new.svg) **Tipi di prodotto per le carte regalo**-Catalog Storefront Service ora supporta gli attributi di prodotto come oggetti o array JSON, consentendo una gestione flessibile di tipi complessi come le gift card.<!--DATA-6573-->

+++Versioni precedenti

### Giugno 2025

**Data di rilascio**: 20 giugno 2025
<!-- v1.37 -->

![Nuovo](../assets/new.svg) **Configurazione gerarchica del listino prezzi**: intervalli di prezzi precisi per i listini prezzi padre-figlio. I calcoli rispettano la gerarchia e le regole ereditate; riducono gli errori di determinazione prezzi quando più listini prezzi sono collegati. Solo Adobe Commerce Optimizer. Consulta [Libri Prezzi](https://experienceleague.adobe.com/it/docs/commerce/optimizer/setup/pricebooks).

![Nuovo](../assets/new.svg) **Chiavi senza distinzione tra maiuscole e minuscole**. Le ricerche di chiavi nelle query non fanno distinzione tra maiuscole e minuscole, riducendo gli errori relativi alle maiuscole e minuscole. <!--DATA-6494, DCAT-2495-->

**Data di rilascio**: 20 giugno 2025
<!-- v1.36 -->

![Nuovi](../assets/new.svg) **Eventi I/O pubblici per Catalog Storefront**. Sono stati aggiunti eventi I/O pubblici per l&#39;integrazione e l&#39;osservabilità in tempo reale (CSS ed EDS).<!--DATA-6329-->

![Nuovo](../assets/new.svg) **Server-Side Rendering (SSR)**—Miglioramenti architetturali per supportare SSR per migliori prestazioni, SEO e UX in cataloghi di grandi dimensioni.<!--DATA-6278, DATA-6280-->

![Nuovo](../assets/new.svg) **Infrastruttura e sicurezza**: nuovi ruoli AWS, integrazione ServiceNow e pipeline CI/CD per il servizio eventi.

![Nuovo](../assets/new.svg) **Formati degli eventi e osservabilità**—Payload semplificati, monitoraggio migliorato, dati evento variante migliorati.<!--DATA-6332, DATA-6402, -->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6404, DATA-6410, -->

**Data di rilascio**: 13 giugno 2025
<!-- v1.35 -->

![Nuovo](../assets/new.svg) **Recupera dati non memorizzati in cache**-Abilita l&#39;intestazione `Magento-Is-Preview` per passare dati non memorizzati in cache dall&#39;endpoint del catalogo al servizio di ricerca.<!--DATA-6345-->

![Nuovo](../assets/new.svg) **Opzioni di prodotto a selezione multipla**-L&#39;API GraphQL ora indica se le opzioni di prodotto consentono selezioni multiple (ad esempio, il bundle &quot;scegli più elementi&quot;).<!--DATA-6487-->

![Nuovo](../assets/new.svg) È stata aggiornata la convalida del prezzo all&#39;acquisizione dei dati per supportare i prodotti senza prezzi.<!--DATA-6098-->

![Correzione](../assets/fix.svg) è stata migliorata la gestione degli errori per i prezzi dei bundle semplici in Adobe Commerce Optimizer.<!--DATA-6541-->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6273, DATA-6485, -->

### Aprile 2025

**Data di rilascio**: 8 aprile 2025
<!-- v1.34 -->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-5732-->

<!-- v1.33 -->
![Correzione](../assets/fix.svg) L&#39;infrastruttura ora supporta cataloghi di grandi dimensioni (fino a circa 440 milioni di SKU) senza influire sui carichi di lavoro esistenti.

### Marzo 2025

**Data di rilascio**: 28 marzo 2025
<!-- v1.32 -->

![Correzione](../assets/fix.svg) Gli attributi senza ruoli non vengono più indicizzati per impostazione predefinita per il catalogo componibile, migliorando il tempo di indicizzazione e riducendo l&#39;archiviazione. Il comportamento legacy può essere riabilitato tramite un flag di funzione.

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.


### Febbraio 2025

**Data di rilascio**: 18 febbraio 2025
<!-- v1.31 -->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6389, DATA-6367, DATA-6373-->

### Dicembre 2024

**Data di rilascio**: 9 dicembre 2024
<!-- v1.30 -->

Versione principale: [modello dati catalogo componibile](https://developer.adobe.com/commerce/services/optimizer/) per vetrine headless, gestione intestazione e gestione dati prodotto.

![Nuovo](../assets/new.svg) **Composable Catalog Data Model (CCDM)**—Supporta i clienti che utilizzano il catalogo componibile per vetrine headless. I nuovi endpoint accettano gli ID di criteri e vista catalogo (compatibili con le versioni precedenti). Dettagli prodotto configurabili e prezzi con impaginazione incorporata.<!--DATA-6018, DATA-6288-->

![Nuovo](../assets/new.svg) **Gestione intestazioni**-`AC-Locale` rinominato in `AC-Scope-Locale` per le operazioni API del catalogo componibile. Sono stati specificati il mapping delle intestazioni e i valori predefiniti.<!--DATA-6303, DATA-6078-->

![Nuovo](../assets/new.svg) **Dati di prodotto e prezzi**-Supporto per il modello di dati di catalogo componibile e migliore gestione dei prezzi per i prodotti configurabili.<!--DATA-6279-->

`CurrencyEnum` aggiornato per supportare `NONE` per le query di ricerca prodotti, in allineamento con la logica di federazione.<!--DATA-6285-->

![Correzione](../assets/fix.svg) **Infrastruttura e aggiornamenti**: miglioramenti a livello di sistema per sicurezza, prestazioni e stabilità.

![Correzione](../assets/fix.svg) Le opzioni del prodotto del bundle ora visualizzano solo i prodotti abilitati.<!--DATA-6347-->

**Data di rilascio**: 9 dicembre 2024
<!-- v1.29 -->

![Nuovo](../assets/new.svg) **Ordinamento delle immagini nelle query di prodotto**. Le immagini di prodotto nel campo GraphQL `images` ora seguono l&#39;esportazione del catalogo `sortOrder` per un comportamento coerente in vetrina e API.<!--DATA-6258-->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6619-->

**Data di rilascio**: dicembre 2024
<!-- v1.28 -->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.


### Ottobre 2024

**Data di rilascio**: 22 ottobre 2024
<!-- v1.26 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Il nuovo](../assets/new.svg) schema di GraphQL ora include `lastModifiedAt` nelle informazioni sul prodotto per mappe del sito precise e reindicizzazione del motore di ricerca (ad esempio, Google).


### Settembre 2024

**Data di rilascio**: 26 settembre 2024
<!-- v1.27 -->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.


### Agosto 2024

**Data di rilascio**: 22 agosto 2024
<!-- v1.23 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) È ora possibile recuperare le informazioni sul prodotto senza i dati di sostituzione (prezzi) del prodotto. In precedenza, queste query restituivano: 

**Data di rilascio**: 13 agosto 2024
<!-- v1.22 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) è stato aggiunto il supporto per recuperare tutte le varianti per SKU prodotto. Consulta il [Riferimento API di Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).

### Maggio 2024

**Data di rilascio**: 23 maggio 2024
<!-- v1.19 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive


![Correzione](../assets/fix.svg) Il flag `InStock` per i valori delle opzioni ora rispetta lo stato `enabled` con ambito della variante di prodotto.

<!--DATA-5033-->

![Correzione](../assets/fix.svg) aggiunta del supporto per i prezzi dei prodotti fino a 16 cifre e 4 cifre decimali. Risincronizza dal [dashboard di gestione dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) o [CLI](../data-export/data-export-cli-commands.md) per applicare gli aggiornamenti.

#### Limitazioni note

Le seguenti funzioni non sono ancora supportate:

- La dimensione massima per il payload degli attributi dinamici è di 9 MB.
- Il prezzo del prodotto del gruppo può essere calcolato con prezzi del prodotto semplici.
- In un array di immagini, solo la prima immagine contiene ruoli.

Utilizza API Mesh e l’API core di GraphQL per:

- Prezzo minimo annunciato
- Prezzi a livelli
- Prodotti in bundle a prezzi fissi

Per ulteriori dettagli ed esempi, vedere [Catalog Service and API Mesh](mesh.md).

### Aprile 2024

**Data di rilascio**: 11 aprile 2024
<!-- v1.18 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) aggiunto supporto per PHP 8.3.

![Nuovo](../assets/new.svg) Le query [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) e [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) ora restituiscono dati di opzioni personalizzabili per prodotti semplici e complessi.<!--DATA-5538-->

### Febbraio 2024

**Data di rilascio**: 22 febbraio 2024
<!-- v1.17 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=it) è ora disponibile per i flussi di dati (Product Recommendations, Live Search, Catalog Service). Richiede `catalog-service` metapackage v3.1.0+.

**Data di rilascio**: 13 febbraio 2024
<!-- v1.16 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![I nuovi](../assets/new.svg) video di prodotto sono ora supportati dall&#39;API Catalog Service.![Correzione](../assets/fix.svg) Le opzioni esaurite sono ora visualizzate nel widget PDP.

#### Limitazioni note

Queste funzioni non sono ancora supportate:

- La dimensione massima per il payload degli attributi dinamici è di 9 MB.
- Prezzo del prodotto di gruppo. Questo valore può essere calcolato con prezzi dei prodotti semplici.
- In un array di immagini, solo la prima immagine contiene ruoli.

Utilizza API Mesh e l’API core di GraphQL per:

- Prezzo minimo annunciato
- [Prezzi a livelli](mesh.md)

### Ottobre 2023

**Data di rilascio**: 12 ottobre 2023
<!-- v1.13 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service supporta il flag `inStock` per le varianti di prodotto.![Nuovo](../assets/new.svg) I campi `urlKey` e `externalId` sono stati aggiunti allo schema di GraphQL.Sono ora supportati ![Nuovi](../assets/new.svg) prodotti scaricabili e gift card.

### Settembre 2023

**Data di rilascio**: 19 settembre 2023
<!-- v1.12 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service ora utilizza l&#39;indicizzazione dei prezzi SaaS [.](../price-index/price-indexing.md)![Correzione](../assets/fix.svg) Questa versione contiene correzioni di bug e miglioramenti sul lato servizio.

### Luglio 2023

**Data di rilascio**: 18 luglio 2023
<!-- v1.11 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service ora supporta la query GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) per i consigli di prodotto.

### Giugno 2023

**Data di rilascio**: 27 giugno 2023
<!-- v1.10 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) L&#39;API di Catalog Service ora supporta `related products`.

### Aprile 2023

**Data di rilascio**: 12 aprile 2023
<!-- v1.7 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service ora ripulisce le varianti di prodotto eliminate.![Correggi](../assets/fix.svg) Miglioramenti a livello di scalabilità e prestazioni dell&#39;infrastruttura.

### Marzo 2023

**Data di rilascio**: 28 marzo 2023
<!-- v1.6 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovi](../assets/new.svg) campioni aggiunti alla query [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).![Nuovo](../assets/new.svg) Aggiunta la possibilità di ottenere `entityId` utilizzando [Mesh API](mesh.md).

**Data di rilascio**: 6 marzo 2023
<!-- v1.5 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) Aggiunta funzionalità di [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL.![Correzione](../assets/fix.svg) Prestazioni e scalabilità API migliorate.

### Febbraio 2023

**Data di rilascio**: 7 febbraio 2023
<!-- v1.4 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) Metapackage del servizio catalogo pubblicato per semplificare i passaggi dell&#39;installazione.![Correggi](../assets/fix.svg) miglioramenti a livello di scalabilità e prestazioni dell&#39;API.

### Gennaio 2023

**Data di rilascio**: 17 gennaio 2023
<!-- v1.3 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) ha semplificato e migliorato l&#39;esperienza di onboarding.![Nuovi](../assets/new.svg) nuovi endpoint sandbox del cliente sono disponibili per il test di pre-produzione.![Nuovo](../assets/new.svg) supporto aggiunto per i prodotti virtuali.![Correggi](../assets/fix.svg) miglioramenti a livello di scalabilità e prestazioni dell&#39;API.

### Novembre 2022

**Data di rilascio**: 18 novembre 2022
<!-- v1.1 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![New](../assets/new.svg) Catalog Service ora supporta [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) di Adobe.![Correzione](../assets/fix.svg) Miglioramento della scalabilità API e delle prestazioni complessive.

### Ottobre 2022

**Data di rilascio**: 4 ottobre 2022
<!-- v1.0 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) supporto per prodotti raggruppati e raggruppati.![Nuovo](../assets/new.svg) Aggiunte Override Di Visibilità B2B. È ora possibile cercare i prodotti e aggiungerli al carrello per gruppi di clienti specifici.Il servizio ![Correzione](../assets/fix.svg) è ora più stabile e offre prestazioni migliorate.

### Settembre 2022

**Data di rilascio**: 12 settembre 2022
<!-- v0.3 -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuove](../assets/new.svg) immagini variante: le immagini del prodotto restituite in base alle opzioni selezionate.![Nuovo](../assets/new.svg) Ruoli di prezzo: solo i membri di gruppi di clienti specifici possono visualizzare i prezzi dei prodotti.![Correzione](../assets/fix.svg) Sono state migliorate la stabilità e le prestazioni del servizio.![Nuovi](../assets/new.svg) aggiornamenti ricevuti quando i prodotti vengono eliminati dal catalogo.

### Agosto 2022

**Data di rilascio**: 9 agosto 2022
<!-- Beta -->

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) Le query `products` e `refineProduct` restituiscono i dati seguenti:

- Attributi di prodotto predefiniti (di sistema).
- Attributi di prodotto dinamici e filtrali per ruolo (pagina di visualizzazione prodotto/pagina di elenco prodotti).
- Opzioni prodotto.
- Immagini dei prodotti e filtrale per ruolo (PDP/PLP).
- Un prezzo specifico per prodotti semplici e fasce di prezzo per prodotti configurabili.
- Prezzi e fasce di prezzo del gruppo di clienti. Restituiscono un prezzo predefinito di fallback sugli acquirenti senza un gruppo di clienti.
- Tipi di prodotto che utilizzano prezzi specifici per il cliente B2B.

+++

## Metapackage di Catalog Service

Aggiornamenti al metapacchetto PHP del servizio catalogo (`magento/catalog-service`).

- Per i clienti di Adobe Commerce as a Cloud Service, l’ultima versione viene installata nel tuo ambiente.

- Per Adobe Commerce on-premise o sul cloud, Adobe consiglia di utilizzare Composer per aggiornare il metapacchetto Catalog Service negli ambienti cloud all’ultima versione.

### Versione v3.5.0

**Data di rilascio**: 10 luglio 2026

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) **Sincronizzazione chiave URL per categoria pubblicata in staging** - Sono state aggiornate le dipendenze del metapacchetto del servizio catalogo per includere il modulo Esportatore dati di staging catalogo (`magento/module-catalog-staging-data-exporter`). Questo modulo riesporta i feed di prodotto quando si applica una modifica della categoria `url_key` pubblicata in staging, in modo che le modifiche del catalogo pubblicate in staging vengano propagate correttamente al catalogo SaaS (Catalog Service, Live Search e Product Recommendations).

![Nuovo](../assets/new.svg) Sono state aggiornate le dipendenze per mantenere la compatibilità tra Catalog Service e lo stack di Commerce.

### Versione v3.4.0

**Data di rilascio**: 8 giugno 2026

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) **Supporto per il monitoraggio dello stato di sincronizzazione dei feed di dati**. Sono state aggiornate le dipendenze del metapacchetto di Catalog Service per includere l&#39;estensione dello stato di Data Exporter (`magento/module-data-exporter-status`). In questo modo [il monitoraggio dello stato di sincronizzazione del feed dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) verrà attivato dall&#39;amministratore di Commerce senza richiedere ulteriori passaggi di installazione o configurazione

![Nuovo](../assets/new.svg) Sono state aggiornate le dipendenze per mantenere la compatibilità tra Catalog Service e lo stack di Commerce.

### Versione v3.3.0

**Data di rilascio**: 14 ottobre 2025

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuova](../assets/new.svg) **Dipendenza aggiornamento servizi dati**—`magento/data-services` aggiornata a ^8.0.0. Prima dell’aggiornamento, verifica l’utilizzo dell’ambiente e delle API dei servizi dati personalizzate per verificare la compatibilità con la versione 8.x.

![Nuovo](../assets/new.svg) versione aggiornata e metadati per la versione 3.3.0.

### Versione v3.2.0

**Data di rilascio**: 12 aprile 2024

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuova](../assets/new.svg) versione e metadati aggiornati per 3.2.0. Nessun&#39;altra modifica di dipendenza.

### Versione v3.1.0

**Data di rilascio**: 26 gennaio 2024

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) aggiunte nuove dipendenze pacchetto:

- **Esportatore dati autorizzazioni categoria** (`magento/module-category-permission-data-exporter`) per l&#39;esportazione dei dati autorizzazioni categoria utilizzati dal servizio catalogo.
- **Amministrazione sincronizzazione catalogo** `magento/module-catalog-sync-admin` per l&#39;interfaccia utente amministratore e la configurazione relativa alla sincronizzazione catalogo.

![Nuovo](../assets/new.svg) versione aggiornata e metadati per la versione 3.1.0.

## Programma di installazione di Catalog Service

Il programma di installazione viene fornito con l’estensione Catalog Service e gestisce i controlli di installazione e ambiente in modo che Catalog Service corrisponda allo stack di Commerce.

- Per i clienti **Adobe Commerce as a Cloud Service**, è installata la versione più recente del programma di installazione nell&#39;ambiente.

- Per **Adobe Commerce nell&#39;infrastruttura cloud** o **nei locali**, tieni il programma di installazione allineato con il [metapackage Catalog Service](#catalog-service-metapackage).

Ogni volta che si utilizza Composer per aggiornare `magento/catalog-service`, il pacchetto del programma di installazione viene aggiornato automaticamente alla versione più recente. È inoltre possibile utilizzare Composer per aggiornare `magento/catalog-service-installer` separatamente quando queste note sulla versione descrivono una modifica necessaria, ad esempio il supporto per una nuova versione PHP. In questo modo gli strumenti di installazione rimangono compatibili con la versione di Catalog Service eseguita.

### versione v1.0.6

**Data di rilascio**: 25 marzo 2026

![Nuovo](../assets/new.svg) **PHP 8.5**—Garantisce la compatibilità quando Catalog Service funziona su PHP 8.5.

## Documentazione correlata

- Per i progetti distribuiti su **Adobe Commerce su cloud, on-premise o Adobe Commerce as a Cloud Service, consulta la seguente documentazione:

   - [Guida a Catalog Service](overview.md)
   - [Riferimento API GraphQL di Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Guida per l’amministratore di Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Guida di Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Guida di Adobe Commerce su Cloud](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- Per i progetti che utilizzano **Adobe Commerce Optimizer** o **Adobe Commerce Optimizer Connector**, consulta la seguente documentazione:

   - [Guida per gli sviluppatori di Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/)
   - [Riferimento API per Merchandising GraphQL](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Guida di Adobe Commerce Optimizer](../optimizer/overview.md)
