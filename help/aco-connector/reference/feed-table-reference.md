---
title: Riferimento schema tabella feed
description: Scopri lo schema della tabella di feed utilizzato da  [!DNL Adobe Commerce Optimizer Connector]  per tenere traccia dello stato dell'elemento di feed, dello stato di esportazione e dei dettagli dell'errore.
autotag-review: '2026-06-23T00:00:00.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 0%

---


# Riferimento schema tabella feed

Ogni feed dispone di una tabella MySQL dedicata nel database [!DNL Adobe Commerce]. Tutte le tabelle di feed condividono la stessa struttura di colonne.

## Feed supportati

Per l&#39;elenco completo dei feed supportati con endpoint API, limiti batch, nomi di indicizzatore e nomi di tabelle di feed, vedere [Moduli connettore ed endpoint di feed](connector-reference.md#supported-feeds).

## Schema

| Colonna | Tipo | Descrizione |
| --- | --- | ---------------- |
| `id` | INT (PK) | Incremento automatico chiave primaria |
| `source_entity_id` | INTERO | ID entità dalla tabella di origine di Commerce (ad esempio, `catalog_product_entity.entity_id`) |
| `feed_id` | VARCHAR | Identificatore univoco di un elemento del feed. Calcolato come hash dei campi di identità dell&#39;elemento (ad esempio, `sku + storeViewCode`), non come valore di incremento automatico. |
| `feed_data` | JSON | Payload di feed per questo elemento. Vengono compilate solo informazioni minime come identificatore di entità e ambito. Quando è impostato `PERSIST_EXPORTED_FEED=1`, viene archiviato il payload completo. |
| `feed_hash` | VARCHAR | Hash di contenuto utilizzato per il rilevamento delle modifiche. Calcolato dal payload, esclusi i timestamp (`modifiedAt`, `updatedAt`). Se l&#39;hash corrisponde all&#39;esportazione precedente, l&#39;elemento non viene inviato nuovamente. |
| `is_deleted` | TINYINT | Marcatore di eliminazione temporanea. Impostato su `1` quando l&#39;entità viene eliminata in Commerce. |
| `modified_at` | TIMESTAMP | L’ultima volta che questo elemento del feed è stato modificato |
| `status` | INTERO | Codice di stato dell’invio dall’ultimo tentativo di esportazione. Consulta [Invio di feed e gestione degli errori](../connector-sync-pipeline.md#feed-submission-and-error-handling). |
| `errors` | TESTO | Dettagli dell&#39;errore con codifica JSON restituiti dall&#39;API [!DNL Commerce Optimizer] per questo elemento |
| `metadata` | JSON | Flag di sincronizzazione interni e informazioni sui metadati di blocco utilizzati dal framework di esportazione |

## Query diagnostiche comuni

Utilizzare le query SQL seguenti per verificare direttamente lo stato della tabella dei feed. La colonna `feed_data` memorizza i dati in formato API [!DNL Adobe Commerce Optimizer]. Sostituire i valori segnaposto come `<SKU>`, `<ATTRIBUTE_CODE>`, `<SLUG>` e `<PRICE_BOOK_ID>` con i valori effettivi dell&#39;ambiente.

**Feed prodotti - per SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Feed attributi prodotto - per codice attributo:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.code') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.code') IN ('<ATTRIBUTE CODE>');
```

**Feed categorie - per percorso URL:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.slug') AS 'slug',
    JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.slug') IN ('<SLUG>');
```

**Feed prezzi - per SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Feed dei listini prezzi per ID listino prezzi dedicato:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
    JSON_EXTRACT(f.feed_data, '$.name') AS 'name',
    JSON_EXTRACT(f.feed_data, '$.parentId') AS 'parent price book ID',
    JSON_EXTRACT(f.feed_data, '$.currency') AS 'currency',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_price_books_feed f
WHERE JSON_UNQUOTE(JSON_EXTRACT(f.feed_data, '$.priceBookId'))  IN ('<PRICE_BOOK_ID>');
```

>[!MORELIKETHIS]
>
>- [Moduli connettore ed endpoint di feed](connector-reference.md)
>- [Pipeline di sincronizzazione del connettore](../connector-sync-pipeline.md)
>- [Gestisci sincronizzazione](../data-sync-manage.md)
>- [Mappatura campi per feed connettore](field-mapping.md)
