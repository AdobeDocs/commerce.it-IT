---
title: Filtra prodotti
description: Definisci le condizioni che includono o escludono l’utilizzo dei prodotti come consigli.
exl-id: 140bf047-4f6a-48da-b536-d96e78ae3d17
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Filtra prodotti

Adobe Commerce applica automaticamente filtri predefiniti non configurabili alle unità di consigli. Se in una pagina sono distribuite più unità di consigli, Adobe Commerce filtra tutti i prodotti ripetuti in tali unità. Viene utilizzato solo il primo riferimento a un prodotto ripetuto, per fare spazio ad altri prodotti da consigliare. Adobe Commerce filtra anche eventuali prodotti acquistati in precedenza e quelli presenti nel carrello.

Quando [crei](create.md) un&#39;unità di consigli, puoi definire filtri che controllano quali prodotti possono essere visualizzati nei consigli. Questi filtri si basano su un set di condizioni di inclusione o esclusione definite dall’utente. Solo i prodotti che corrispondono a tutte le condizioni di inclusione vengono visualizzati nei consigli. Non sono consigliati i prodotti che soddisfano una qualsiasi delle condizioni di esclusione.

Per configurare più filtri e abilitarli solo quelli desiderati, seleziona l’opzione (Attiva/Disattiva) in ogni pagina del filtro. Ciò consente di creare bozze di filtri da utilizzare in futuro. Il numero di filtri attivati viene visualizzato in ogni scheda.

## Condizioni

Le condizioni possono essere statiche o dinamiche.

- Una condizione statica utilizza gli attributi di prodotto esistenti per determinare quali prodotti possono comparire nell’unità. Ad esempio, è possibile specificare che solo i prodotti in magazzino con un prezzo superiore a 25 $ vengano visualizzati nell&#39;unità. Le condizioni statiche sono disponibili su tutti i tipi di pagina.

- Una condizione dinamica chiave del contesto corrente di un acquirente, ad esempio la categoria o il prodotto attualmente visualizzato. Ad esempio, quando crei un consiglio di prodotto da distribuire nelle pagine dei dettagli del prodotto, puoi creare una condizione per consigliare solo i prodotti che rientrano in un intervallo di prezzo relativo del prodotto attualmente visualizzato. Le condizioni dinamiche sono disponibili su ogni tipo di pagina, eccetto la Home page, e sulle pagine con consigli inseriti con Page Builder.

### Operatori logici

Gli operatori logici `AND` e `OR` vengono utilizzati per unire più condizioni. Se utilizzi sia i filtri di inclusione che i filtri di esclusione, le inclusioni vengono valutate per prime per determinare tutti i possibili prodotti che possono essere consigliati, quindi i prodotti che corrispondono a eventuali filtri di esclusione vengono rimossi dall’elenco.

- `AND` - Unisce due condizioni di filtro di inclusione
- `OR` - Unisce due condizioni di filtro di esclusione

>[!NOTE]
>
> I filtri di inclusione ed esclusione sostituiscono le esclusioni di categoria legacy nelle versioni 3.2.2 e successive del modulo `magento/product-recommendations`. Per ulteriori informazioni sulle versioni di Adobe Commerce, consulta le [note sulla versione](release-notes.md).

## Tipi di filtri {#filtertypes}

![Filtri](assets/rec-conditions.png)

### Categoria

Filtra i prodotti in base alla loro categoria. Il filtro categoria utilizza assegnazioni di categoria dirette e le relative sottocategorie. Se ad esempio si abilita una condizione di esclusione per la categoria `Gear`, verranno esclusi i prodotti assegnati a `Gear` e tutte le relative sottocategorie, ad esempio `Gear/Bags` o `Gear/Fitness Equipment`. Lo stesso vale per un filtro di inclusione per una categoria. Ad esempio, l&#39;abilitazione di una condizione di inclusione per la categoria `Gear` include i prodotti assegnati a `Gear` e a tutte le relative sottocategorie, ad esempio `Gear/Bags` o `Gear/Fitness Equipment`.

Nel campo categoria vengono visualizzate le categorie che appartengono alla visualizzazione dello store corrente.

>[!NOTE]
>
>Per i commercianti B2B, il filtro Categoria aderisce a qualsiasi [categoria di prodotto specifica per il cliente](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html) configurata.

Adobe Commerce consiglia di utilizzare la seguente configurazione del filtro categorie quando distribuisci i consigli ai tipi di pagina:

| Pagina | Filtra per |
|---|---|
| Home | Non filtrare i prodotti. |
| Categoria | Filtra i prodotti nella categoria specifica. |
| Dettagli prodotto | Filtra i prodotti nelle stesse categorie. |
| Carrello | Filtra le categorie di prodotti nel carrello. |
| Conferma ordine | Filtra le categorie di prodotti acquistati. |

### Prodotto

I filtri dei prodotti specificano quali prodotti specifici sono idonei, o non idonei, per la visualizzazione nei consigli. Non puoi selezionare prodotti disabilitati o non visibili singolarmente, in quanto tali prodotti non possono mai essere visualizzati nei consigli.

>[!NOTE]
>
>I prodotti secondari di un prodotto configurabile non vengono visualizzati in un&#39;unità di consigli perché tali prodotti secondari hanno la visibilità di _Non visibile singolarmente_.

### Tipo

Un filtro basato sul tipo di prodotto include o esclude tutti i prodotti di un tipo specifico. I tipi supportati sono _simple_, _configurable_, _virtual_, _downloadable_ o _gift card_. _I tipi di prodotto_, _raggruppati_ e personalizzati non sono supportati.

### Visibilità

Filtra i prodotti in base alla visibilità, ad esempio: _Catalogo_, _Ricerca_ o entrambi.

### Prezzo

Un filtro basato sul prezzo del prodotto utilizza il prezzo finale per eseguire il confronto. Il prezzo finale include eventuali sconti o prezzi speciali disponibili per gli acquirenti anonimi. Per i commercianti B2B, il prezzo visualizzato riflette i [prezzi di gruppo specifici per il cliente](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) che hai configurato.

### Stato del magazzino

I seguenti filtri di esclusione possono essere utilizzati per filtrare i prodotti in base allo stato delle scorte:

- Esaurito - (solo esclusione) esclude i prodotti esauriti.
- Magazzino basso: (solo esclusione) esclude i prodotti con scorte limitate. Lo stato scorte basse si basa sul valore _Solo X Soglia sinistra_ nella [Configurazione inventario](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/inventory.html).
