---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: Informazioni aggiornate sulla versione di  [!DNL Catalog Service]  per Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 9ba7a964243c616cc7e40fb180a855b839cd4597
workflow-type: tm+mt
source-wordcount: '2252'
ht-degree: 0%

---

# Note sulla versione [!DNL Commerce Storefront Catalog Service]

Queste note sulla versione descrivono gli ultimi aggiornamenti di Commerce Catalog Service, inclusi:

- **Versioni di Storefront Catalog Service**

   - Miglioramenti allo schema API di Catalog Service per un migliore recupero dei dati.
   - Miglioramenti a livello di sicurezza, prestazioni e affidabilità per l’API Catalog Service e l’infrastruttura sottostante.

- **Versioni del metapacchetto Catalog Service**

   - Sono state aggiornate le dipendenze per migliorare le prestazioni, la stabilità e la compatibilità con altri componenti di Adobe Commerce.

Gli aggiornamenti sono suddivisi per tipo:

![Nuove](../assets/new.svg) nuove funzionalità
![Correzioni](../assets/fix.svg) correzioni e miglioramenti
![Bug](../assets/bug.svg) problemi noti

È disponibile il supporto per la versione più recente. Sono incluse per riferimento le note sulla versione per le versioni precedenti.

## Servizio catalogo vetrina

### versione v1.48

_19 febbraio 2025_

![Nuovo](../assets/new.svg) La query `categoryTree` nell&#39;API di GraphQL ora restituisce descrizioni di categorie, immagini e metatag SEO. Questo aggiornamento fornisce i dati necessari agli sviluppatori di vetrine per visualizzare le immagini delle categorie e migliorare l’ottimizzazione dei motori di ricerca con metatitoli, descrizioni e parole chiave appropriati. Supportato solo nelle implementazioni di Commerce che utilizzano il [modello dati catalogo componibile](https://developer.adobe.com/commerce/services/optimizer/) per vetrine headless&lt;<!--DATA-6933-->

### versione v1.47

_12 febbraio 2025_

![Nuovo](../assets/new.svg) Il servizio API ora supporta il tipo `CategoryProductView`, abilitando visualizzazioni e query avanzate per i prodotti per categoria. Questo aggiornamento consente agli sviluppatori di recuperare e filtrare in modo efficiente i dati di prodotto in base alla categoria, migliorando la flessibilità e le prestazioni per i casi d’uso basati sulle categorie. Per ulteriori dettagli, vedere [Implementare le categorie nella vetrina](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/categories-storefront-implementation/). Supportato solo nelle implementazioni di Commerce che utilizzano il [modello dati catalogo componibile](https://developer.adobe.com/commerce/services/optimizer/) per gli storefront headless<!--DATA-6949-->

### versione v1.46

_11 dicembre 2025_

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare prestazioni e stabilità. <!--DATA-6852, DATA-6864-->

### versione v1.45

_17 novembre 2025_

![Nuovo](../assets/new.svg) **Filtro attributi per nome**-La query di GraphQL `productSearch` ora supporta il filtro degli attributi di prodotto con il campo `names`. <!--DATA-6831--> Con questo filtro è possibile:

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

### versione v1.44

_6 novembre 2025_

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare prestazioni e stabilità. <!--DATA-6852, DATA-6864-->

### versione v1.43

_3 novembre 2025_

![Nuovo](../assets/new.svg) **Livelli di prodotto per la personalizzazione di prodotti multidimensionali**. È stato aggiunto il supporto per la distribuzione di contenuti specifici per canale e in base alle impostazioni locali per le implementazioni di Adobe Commerce Optimizer.<!--DATA-6632-->

- Distribuire contenuti di prodotti diversi a segmenti di clienti diversi
- Applicare personalizzazioni specifiche delle impostazioni internazionali senza duplicare i dati di base
- Controllare le sostituzioni a livello di campo con le maschere di livello
- Supporto per livelli di contenuto premium, stagionali e ottimizzati per dispositivi mobili

  I livelli vengono recuperati utilizzando la query `products` esistente, vengono applicati sul lato server dalle intestazioni delle richieste e non richiedono modifiche allo schema. Vedi [Livello catalogo](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-layer) nella _Guida di Adobe Commerce Optimizer_.

![Correzione](../assets/fix.svg) È ora possibile eseguire una query sui prodotti raggruppati quando il padre non ha alcun prezzo; i prodotti secondari restituiscono i propri ruoli di visibilità.<!--DATA-6779-->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare prestazioni e stabilità. <!--DATA-6721, DATA-6864-->

### versione v1.42

_8 settembre 2025_

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

### versione v1.41

_2 settembre 2025_

![Correzione](../assets/fix.svg) **È stata migliorata la gestione degli errori per le informazioni sul prezzo mancanti**. Quando i dati sul prezzo non vengono ancora ricevuti, l&#39;API restituisce `null` per il campo del prezzo invece di generare un errore, consentendo ai client di gestire i dati mancanti in modo corretto.<!--DATA-6612-->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare le prestazioni e la stabilità.<!--DATA-6671-->

### versione v1.40

_30 luglio 2025_

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6619-->

### versione v1.39

_24 luglio 2025_

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

### versione v1.38

_15 luglio 2025_

![Nuovo](../assets/new.svg) **Tipi di prodotto per le carte regalo**-Catalog Storefront Service ora supporta gli attributi di prodotto come oggetti o array JSON, consentendo una gestione flessibile di tipi complessi come le gift card.<!--DATA-6573-->


### versione v1.37

_20 giugno 2025_

![Nuovo](../assets/new.svg) **Configurazione gerarchica del listino prezzi**: intervalli di prezzi precisi per i listini prezzi padre-figlio. I calcoli rispettano la gerarchia e le regole ereditate; riducono gli errori di determinazione prezzi quando più listini prezzi sono collegati. Solo Adobe Commerce Optimizer. Consulta [Libri Prezzi](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks).

![Nuovo](../assets/new.svg) **Chiavi senza distinzione tra maiuscole e minuscole**. Le ricerche di chiavi nelle query non fanno distinzione tra maiuscole e minuscole, riducendo gli errori relativi alle maiuscole e minuscole. <!--DATA-6494, DCAT-2495-->

### versione v1.36

_20 giugno 2025_

![Nuovi](../assets/new.svg) **Eventi I/O pubblici per Catalog Storefront**. Sono stati aggiunti eventi I/O pubblici per l&#39;integrazione e l&#39;osservabilità in tempo reale (CSS ed EDS).<!--DATA-6329-->

![Nuovo](../assets/new.svg) **Server-Side Rendering (SSR)**—Miglioramenti architetturali per supportare SSR per migliori prestazioni, SEO e UX in cataloghi di grandi dimensioni.<!--DATA-6278, DATA-6280-->

![Nuovo](../assets/new.svg) **Infrastruttura e sicurezza**: nuovi ruoli AWS, integrazione ServiceNow e pipeline CI/CD per il servizio eventi.

![Nuovo](../assets/new.svg) **Formati degli eventi e osservabilità**—Payload semplificati, monitoraggio migliorato, dati evento variante migliorati.<!--DATA-6332, DATA-6402, -->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6404, DATA-6410, -->

+++ Versioni precedenti

## versione v1.35

_13 giugno 2025_

![Nuovo](../assets/new.svg) **Recupera dati non memorizzati in cache**-Abilita l&#39;intestazione `Magento-Is-Preview` per passare dati non memorizzati in cache dall&#39;endpoint del catalogo al servizio di ricerca.<!--DATA-6345-->

![Nuovo](../assets/new.svg) **Opzioni di prodotto a selezione multipla**-L&#39;API GraphQL ora indica se le opzioni di prodotto consentono selezioni multiple (ad esempio, il bundle &quot;scegli più elementi&quot;).<!--DATA-6487-->

![Nuovo](../assets/new.svg) È stata aggiornata la convalida del prezzo all&#39;acquisizione dei dati per supportare i prodotti senza prezzi.<!--DATA-6098-->

![Correzione](../assets/fix.svg) è stata migliorata la gestione degli errori per i prezzi dei bundle semplici in Adobe Commerce Optimizer.<!--DATA-6541-->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6273, DATA-6485, -->

## versione v1.34

_23 marzo 2025_

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-5732-->

## versione v1.33

_29 aprile 2025_

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura. L&#39;infrastruttura ora supporta cataloghi di grandi dimensioni (fino a circa 440 milioni di SKU) senza influire sui carichi di lavoro esistenti.

### versione v1.32

_28 marzo 2025_

![Correzione](../assets/fix.svg) Gli attributi senza ruoli non vengono più indicizzati per impostazione predefinita per il catalogo componibile, migliorando il tempo di indicizzazione e riducendo l&#39;archiviazione. Il comportamento legacy può essere riabilitato tramite un flag di funzione.

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità. <!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### versione v1.31

_18 febbraio 2025_

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6389, DATA-6367, DATA-6373-->

### versione v1.30

_9 dicembre 2024_

Versione principale: [modello dati catalogo componibile](https://developer.adobe.com/commerce/services/optimizer/) per vetrine headless, gestione intestazione e gestione dati prodotto.

![Nuovo](../assets/new.svg) **Composable Catalog Data Model (CCDM)**—Supporta i clienti che utilizzano il catalogo componibile per vetrine headless. I nuovi endpoint accettano gli ID di criteri e vista catalogo (compatibili con le versioni precedenti). Dettagli prodotto configurabili e prezzi con impaginazione incorporata.<!--DATA-6018, DATA-6288-->

![Nuovo](../assets/new.svg) **Gestione intestazioni**-`AC-Locale` rinominato in `AC-Scope-Locale` per le operazioni API del catalogo componibile. Sono stati specificati il mapping delle intestazioni e i valori predefiniti.<!--DATA-6303, DATA-6078-->

![Nuovo](../assets/new.svg) **Dati di prodotto e prezzi**-Supporto per il modello di dati di catalogo componibile e migliore gestione dei prezzi per i prodotti configurabili.<!--DATA-6279-->

`CurrencyEnum` aggiornato per supportare `NONE` per le query di ricerca prodotti, in allineamento con la logica di federazione.<!--DATA-6285-->

![Correzione](../assets/fix.svg) **Infrastruttura e aggiornamenti**: miglioramenti a livello di sistema per sicurezza, prestazioni e stabilità.

![Correzione](../assets/fix.svg) Le opzioni del prodotto del bundle ora visualizzano solo i prodotti abilitati.<!--DATA-6347-->

### versione v1.29

_9 dicembre 2024_

![Nuovo](../assets/new.svg) **Ordinamento delle immagini nelle query di prodotto**. Le immagini di prodotto nel campo GraphQL `images` ora seguono l&#39;esportazione del catalogo `sortOrder` per un comportamento coerente in vetrina e API.<!--DATA-6258-->

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6619-->

### versione v1.28

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### versione v1.27

_26 settembre 2024_

![Correzione](../assets/fix.svg) miglioramenti a livello di sistema e di infrastruttura per migliorare la sicurezza, le prestazioni e la stabilità.<!--DATA-6243-->

### versione v1.26

_22 ottobre 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Il nuovo](../assets/new.svg) schema di GraphQL ora include `lastModifiedAt` nelle informazioni sul prodotto per mappe del sito precise e reindicizzazione del motore di ricerca (ad esempio, Google). <!--DATA-6209-->

### versione v1.23

_22 agosto 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) È ora possibile recuperare le informazioni sul prodotto senza i dati di sostituzione (prezzi) del prodotto. In precedenza, queste query restituivano: `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### versione v1.22

_13 agosto 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) è stato aggiunto il supporto per recuperare tutte le varianti per SKU prodotto. Vedi il [riferimento API di Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### versione v1.19

_23 maggio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive


![Correzione](../assets/fix.svg) <!--DATA-5033-->Il flag `InStock` per i valori delle opzioni ora rispetta lo stato `enabled` con ambito della variante di prodotto.

![Correzione](../assets/fix.svg) <!--DATA-5888-->È stato aggiunto il supporto per i prezzi dei prodotti fino a 16 cifre e 4 cifre decimali. Risincronizza dal [dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) o [CLI](../landing/catalog-sync.md#command-line-interface) per applicare gli aggiornamenti.

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

### versione v1.18

_11 aprile 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) aggiunto supporto per PHP 8.3.

![Nuovo](../assets/new.svg) Le query [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) e [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) ora restituiscono dati di opzioni personalizzabili per prodotti semplici e complessi.<!--DATA-5538-->

### versione v1.17

_22 febbraio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) è ora disponibile per i flussi di dati (Product Recommendations, Live Search, Catalog Service). Richiede `catalog-service` metapackage v3.1.0+.

### versione v1.16

_13 febbraio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![I nuovi](../assets/new.svg) video di prodotto sono ora supportati dall&#39;API Catalog Service.
![Correzione](../assets/fix.svg) Le opzioni esaurite sono ora visualizzate nel widget PDP.

#### Limitazioni note

Queste funzioni non sono ancora supportate:

- La dimensione massima per il payload degli attributi dinamici è di 9 MB.
- Prezzo del prodotto di gruppo. Questo valore può essere calcolato con prezzi dei prodotti semplici.
- In un array di immagini, solo la prima immagine contiene ruoli.

Utilizza API Mesh e l’API core di GraphQL per:

- Prezzo minimo annunciato
- [Prezzi a livelli](mesh.md)

### versione v1.13

_12 ottobre 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service supporta il flag `inStock` per le varianti di prodotto.
![Nuovo](../assets/new.svg) I campi `urlKey` e `externalId` sono stati aggiunti allo schema di GraphQL.
Sono ora supportati ![Nuovi](../assets/new.svg) prodotti scaricabili e gift card.

### versione v1.12

_19 settembre 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service ora utilizza l&#39;indicizzazione dei prezzi SaaS [.
](../price-index/price-indexing.md)
![Correzione](../assets/fix.svg) Questa versione contiene correzioni di bug e miglioramenti sul lato servizio.

### versione v1.11

_18 luglio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service ora supporta la query GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) per i consigli di prodotto.

### versione v1.10

_27 giugno 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) L&#39;API di Catalog Service ora supporta `related products`.

### versione v1.7

_12 aprile 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service ora ripulisce le varianti di prodotto eliminate.
![Correggi](../assets/fix.svg) Miglioramenti a livello di scalabilità e prestazioni dell&#39;infrastruttura.

### versione v1.6

_28 marzo 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovi](../assets/new.svg) campioni aggiunti alla query [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Nuovo](../assets/new.svg) Aggiunta la possibilità di ottenere `entityId` utilizzando [Mesh API](mesh.md).

### versione v1.5

_6 marzo 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) Aggiunta funzionalità di [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL.
![Correzione](../assets/fix.svg) Prestazioni e scalabilità API migliorate.

### versione v1.4

_7 febbraio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) Metapackage del servizio catalogo pubblicato per semplificare i passaggi dell&#39;installazione.
![Correggi](../assets/fix.svg) miglioramenti a livello di scalabilità e prestazioni dell&#39;API.

### versione v1.3

_17 gennaio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) ha semplificato e migliorato l&#39;esperienza di onboarding.
![Nuovi](../assets/new.svg) nuovi endpoint sandbox del cliente sono disponibili per il test di pre-produzione.
![Nuovo](../assets/new.svg) supporto aggiunto per i prodotti virtuali.
![Correggi](../assets/fix.svg) miglioramenti a livello di scalabilità e prestazioni dell&#39;API.

### versione v1.1

_18 novembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![New](../assets/new.svg) Catalog Service ora supporta [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) di Adobe.
![Correzione](../assets/fix.svg) Miglioramento della scalabilità API e delle prestazioni complessive.

### versione v1.0

_4 ottobre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) supporto per prodotti raggruppati e raggruppati.
![Nuovo](../assets/new.svg) Aggiunte Override Di Visibilità B2B. È ora possibile cercare i prodotti e aggiungerli al carrello per gruppi di clienti specifici.
Il servizio ![Correzione](../assets/fix.svg) è ora più stabile e offre prestazioni migliorate.

### Versione 0.3 - Beta+

_12 settembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuove](../assets/new.svg) immagini variante: le immagini del prodotto restituite in base alle opzioni selezionate.
![Nuovo](../assets/new.svg) Ruoli di prezzo: solo i membri di gruppi di clienti specifici possono visualizzare i prezzi dei prodotti.
![Correzione](../assets/fix.svg) Sono state migliorate la stabilità e le prestazioni del servizio.
![Nuovi](../assets/new.svg) aggiornamenti ricevuti quando i prodotti vengono eliminati dal catalogo.

### Versione Beta

_9 agosto 2022_

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

- Per Adobe Commerce on-premise su cloud, Adobe consiglia di utilizzare Composer per aggiornare il metapacchetto Catalog Service negli ambienti cloud all’ultima versione.

### Versione v3.3.0

_14 ottobre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuova](../assets/new.svg) **Dipendenza aggiornamento servizi dati**—`magento/data-services` aggiornata a ^8.0.0. Prima dell’aggiornamento, verifica l’utilizzo dell’ambiente e delle API dei servizi dati personalizzate per verificare la compatibilità con la versione 8.x.
ea
![Nuovo](../assets/new.svg) versione aggiornata e metadati per la versione 3.3.0.

### Versione v3.2.0

_12 aprile 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuova](../assets/new.svg) versione e metadati aggiornati per 3.2.0. Nessun&#39;altra modifica di dipendenza.

### Versione v3.1.0

_26 gennaio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) aggiunte nuove dipendenze pacchetto:

- **Esportatore dati autorizzazioni categoria** (`magento/module-category-permission-data-exporter`) per l&#39;esportazione dei dati autorizzazioni categoria utilizzati dal servizio catalogo.
- **Amministrazione sincronizzazione catalogo** `magento/module-catalog-sync-admin` per l&#39;interfaccia utente amministratore e la configurazione relativa alla sincronizzazione catalogo.

![Nuovo](../assets/new.svg) versione aggiornata e metadati per la versione 3.1.0.

## Documentazione correlata

- Per i progetti distribuiti su **Adobe Commerce su cloud, on-premise o Adobe Commerce as a Cloud Service, consulta la seguente documentazione:

   - [Guida a Catalog Service](overview.md)
   - [Riferimento API GraphQL di Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Guida dell&#39;amministratore di Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Guida di Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Guida di Adobe Commerce su Cloud](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- Per i progetti che utilizzano **Adobe Commerce Optimizer** o **Adobe Commerce Optimizer Connector**, consulta la seguente documentazione:

   - [Guida per gli sviluppatori di Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/)
   - [Riferimento API di GraphQL per merchandising](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Guida di Adobe Commerce Optimizer](../optimizer/overview.md)
