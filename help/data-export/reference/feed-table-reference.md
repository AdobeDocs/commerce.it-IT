---
title: Riferimento schema tabella feed
description: Scopri lo schema della tabella dei feed utilizzato da [!DNL SaaS Data Export] per tenere traccia dello stato dell'elemento del feed, dello stato di esportazione e dei dettagli dell'errore.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 416
ht-degree: 0%

---


# Riferimento schema tabella feed

Ogni feed dispone di una tabella MySQL dedicata nel database [!DNL Adobe Commerce]. Tutte le tabelle di feed condividono la stessa struttura di colonne. La tabella seguente elenca ogni feed con il relativo nome di feed CLI, l’ID dell’indicizzatore e il nome della tabella di feed.

## Feed supportati

L&#39;elenco effettivo dei feed dipende dal pacchetto [!DNL SaaS Data Export] installato.


| Feed (`--feed`) | Finalità | ID indicizzatore | Tabella feed | Modalità di esportazione |
| --- | ------------------------------------------------------------------- | --- | --- | --- |
| `products` | Catalogo dei prodotti (attributi, categorie, immagini, ecc.) | `catalog_data_exporter_products` | `cde_products_feed` | Immediato |
| `productAttributes` | Definizioni degli attributi e metadati. Utilizzato per definire lo schema di ricerca. | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` | Immediato |
| `categories` | Dati delle categorie | `catalog_data_exporter_categories` | `cde_categories_feed` | Immediato |
| `prices` | Prezzi dei prodotti con prezzi dei gruppi di clienti e prezzi dei livelli | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` | Immediato |
| `variants` | Varianti di prodotto configurabili | `catalog_data_exporter_product_variants` | `cde_product_variants_feed` | Immediato |
| `scopesWebsite` | Sito Web con codici di visualizzazione negozio | `scopes_website_data_exporter` | `scopes_website_data_exporter` | Legacy |
| `scopesCustomerGroup` | Definizioni dei gruppi di clienti | `scopes_customergroup_data_exporter` | `scopes_customergroup_data_exporter` | Legacy |
| `productOverrides` | Autorizzazioni calcolate per il prodotto | `catalog_data_exporter_product_overrides` | `cde_product_overrides_feed` | Immediato |
| `categoryPermissions` *(EE)* | Dati delle autorizzazioni delle categorie non elaborati | `catalog_data_exporter_category_permissions` | `cde_category_permissions_feed` | Immediato |
| `orders` | Stato ordini cliente | `sales_order_data_exporter_v2` | `sales_data_exporter_orders_v2` | Legacy |

La colonna **Modalità di esportazione** indica il modo in cui ogni feed raccoglie e invia i dati:

- **Feed in modalità immediata**: raccolta dati, salto di elementi non modificati tramite hash di contenuto (deduplicazione hash) e invio di aggiornamenti nella stessa esecuzione dell&#39;indicizzatore.
- **Feed in modalità legacy** (`scopesWebsite`, `scopesCustomerGroup`, `orders`) - Archivia prima i dati assemblati nella tabella di feed e inviali tramite un processo cron separato.

Vedere [Modalità di sincronizzazione](../sync-overview.md#synchronization-modes).

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
| `status` | INTERO | Codice di stato dell’invio dall’ultimo tentativo di esportazione. Consulta [Invio di feed e gestione degli errori HTTP](../sync-overview.md#feed-submission-and-http-error-handling). |
| `errors` | TESTO | Dettagli dell’errore con codifica JSON restituiti dal servizio SaaS per questo elemento |
| `metadata` | JSON | Flag di sincronizzazione interni e informazioni sui metadati di blocco utilizzati dal framework di esportazione |

## Query diagnostiche comuni

Utilizzare le query SQL seguenti per verificare direttamente lo stato della tabella dei feed. Sostituire `cde_products_feed` con la tabella per il feed che si sta esaminando. Consulta [Feed supportati](#supported-feeds) per l&#39;elenco completo dei nomi di tabella.

**Trovare tutti gli elementi che non sono stati esportati correttamente:**

```sql
SELECT source_entity_id, status, errors, modified_at
FROM cde_products_feed
WHERE status != 200
ORDER BY modified_at DESC
LIMIT 50;
```

**Verifica lo stato di esportazione per uno SKU specifico in tutti gli ambiti:**

```sql
SELECT p.sku, f.status, f.modified_at, f.is_deleted, f.feed_data, f.errors
FROM catalog_product_entity p
LEFT JOIN cde_products_feed f ON f.source_entity_id = p.entity_id
WHERE p.sku = 'ADB295';
```


>[!MORELIKETHIS]
>
>- [Sincronizzare i dati con l&#39;esportazione dei dati SaaS](../sync-overview.md)
>- [Visualizza e gestisci sincronizzazione](../data-sync-manage.md)
>- [Sincronizzare i feed utilizzando Commerce CLI](../data-export-cli-commands.md)
