---
title: Endpoint REST per conto gift card
description: Scopri come utilizzare le API REST per account gift card per creare, aggiornare, eliminare ed eseguire query sugli account gift card a livello di programmazione in [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer
level: Experienced
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# API account gift card

{{accs-sandbox-experimental}}

Gli endpoint REST del conto gift card forniscono la gestione programmatica degli account gift card a livello di account, non a livello di carrello o preventivo. Utilizza questa API per creare, recuperare, aggiornare ed eliminare account gift card o per eseguire il provisioning di account gift card in blocco tramite l’endpoint di importazione JSON.

Questi endpoint sono progettati per:

* Amministratori che gestiscono i programmi gift card
* Integrazioni di terze parti che forniscono gift card da sistemi esterni, come ERP, CRM e piattaforme di marketing
* Flussi di lavoro automatizzati per la creazione in blocco di gift card

## Autenticazione

Tutti gli endpoint richiedono un token Bearer amministratore o di integrazione. Il token deve essere associato a un ruolo che include la risorsa Elenco di controllo di accesso (ACL) `Magento_GiftCardAccount::giftcardaccount`.

Per le operazioni di importazione in blocco, il ruolo deve includere anche la risorsa ACL `Magento_ImportExport::import_api`.

## Contesto del sito web e dello store

I valori delle visualizzazioni del sito web e dell’archivio vengono risolti dalle intestazioni delle richieste HTTP e non dal corpo della richiesta. Passa una delle seguenti intestazioni a ogni richiesta:

* `Store: <store_view_code>`
* `Magento-Website-Code: <website_code>`

L’API risolve automaticamente il sito web da queste intestazioni. Non includere `website_id` nel payload della richiesta REST.

>[!NOTE]
>
>L’endpoint per l’importazione in blocco è un’eccezione. Poiché l&#39;importazione funziona in blocco e può essere destinata a siti Web specifici, ogni riga nel payload di importazione richiede un valore `website_id` esplicito.

## Riferimento API REST

L&#39;API espone le seguenti operazioni in `/V1/giftcardaccounts`, tutte protette dalla risorsa ACL `Magento_GiftCardAccount::giftcardaccount`:

| Metodo | URL | Descrizione |
|--------|-----|-------------|
| POST | `/rest/V1/giftcardaccounts` | Creare un conto gift card |
| GET | `/rest/V1/giftcardaccounts` | Elenca account (supporta searchCriteria) |
| GET | `/rest/V1/giftcardaccounts/:id` | Ottieni account per ID |
| GET | `/rest/V1/giftcardaccounts/code/:code` | Ottieni account per codice |
| PUT | `/rest/V1/giftcardaccounts/:id` | Aggiorna account (semantica unione) |
| DELETE | `/rest/V1/giftcardaccounts/:id` | Elimina account |

### Riferimento campo

| Campo | Tipo | Valori validi | Creazione REST | Importa |
|---|---|---|---|---|
| `code` | stringa | Massimo 255 caratteri | Obbligatorio | Obbligatorio |
| `balance` | galleggiare | >= 0 | Obbligatorio | Obbligatorio |
| `status` | int | `0` (disabilitato), `1` (abilitato) | Facoltativo, impostazione predefinita: `1` | Facoltativo, impostazione predefinita: `1` |
| `state` | int | `0` (disponibile), `1` (utilizzato), `2` (riscattato), `3` (scaduto) | Facoltativo, impostazione predefinita: `0` | Facoltativo, impostazione predefinita: `0` |
| `is_redeemable` | int | `0` o `1` | Facoltativo, impostazione predefinita: `1` | Facoltativo, impostazione predefinita: `1` |
| `date_expires` | stringa | `YYYY-MM-DD` o null | Facoltativo | Facoltativo |
| `date_created` | stringa | `YYYY-MM-DD` | Impostazione automatica | Facoltativo, impostazione automatica se omesso |
| `website_id` | int | ID sito Web valido | Non accettato (risoluzione automatica dalle intestazioni) | Obbligatorio |

### Creare un conto gift card

Crea un nuovo conto gift card con rilevamento codice duplicato.

| Elemento | Valore |
|---|---|
| **Metodo** | `POST` |
| **URL** | `/V1/giftcardaccounts` |

**Corpo richiesta:**

```json
{
  "giftcardAccount": {
    "code": "GIFT-1234-ABCD",
    "balance": 100.00,
    "status": 1,
    "state": 0,
    "is_redeemable": 1,
    "date_expires": "2027-12-31"
  }
}
```

**Risposta (200):**

```json
{
  "account_id": 42,
  "code": "GIFT-1234-ABCD",
  "balance": 100,
  "status": 1,
  "state": 0,
  "is_redeemable": 1,
  "date_expires": "2027-12-31",
  "date_created": "2026-03-12"
}
```

### Recuperare un conto gift card per ID

| Elemento | Valore |
|---|---|
| **Metodo** | `GET` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Risposta (200):**

Restituisce un singolo oggetto conto gift card.

### Recuperare un conto gift card in base al codice

| Elemento | Valore |
|---|---|
| **Metodo** | `GET` |
| **URL** | `/V1/giftcardaccounts/code/:code` |

>[!IMPORTANT]
>
>Se un codice gift card è puramente numerico (ad esempio, `12345`), una richiesta a `/V1/giftcardaccounts/12345` corrisponde alla route ID, non alla route codice. Utilizzare sempre `/V1/giftcardaccounts/code/12345` per ricerche basate su codice quando il codice potrebbe essere numerico.

**Risposta (200):**

Restituisce un singolo oggetto conto gift card.

### Elenca account gift card con criteri di ricerca

| Elemento | Valore |
|---|---|
| **Metodo** | `GET` |
| **URL** | `/V1/giftcardaccounts` |

Passa i criteri di ricerca come parametri di query. Nell&#39;esempio seguente vengono restituiti gli account gift card in cui `status` è uguale a `1` (abilitato):

```text
GET /V1/giftcardaccounts?searchCriteria[filterGroups][0][filters][0][field]=status&searchCriteria[filterGroups][0][filters][0][value]=1&searchCriteria[pageSize]=10&searchCriteria[currentPage]=1
```

**Risposta (200):**

```json
{
  "items": [
    {
      "account_id": 42,
      "code": "GIFT-1234-ABCD",
      "balance": 100,
      "status": 1,
      "state": 0,
      "is_redeemable": 1,
      "date_expires": "2027-12-31",
      "date_created": "2026-03-12"
    }
  ],
  "search_criteria": { ... },
  "total_count": 1
}
```

### Aggiornare un conto gift card

Aggiorna un account gift card esistente utilizzando la semantica di unione. Nella richiesta vengono applicati solo campi non nulli. Il campo `code` non è modificabile. Il passaggio di un codice diverso restituisce un errore di convalida.

| Elemento | Valore |
|---|---|
| **Metodo** | `PUT` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Corpo richiesta:**

```json
{
  "giftcardAccount": {
    "balance": 75.00,
    "status": 1
  }
}
```

**Risposta (200):**

Restituisce l&#39;oggetto account gift card aggiornato.

### Eliminare un conto gift card

| Elemento | Valore |
|---|---|
| **Metodo** | `DELETE` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Risposta (200):**

```json
true
```

## Importazione in blocco tramite JSON

È possibile eseguire il provisioning in blocco degli account gift card utilizzando `POST /V1/import/json` con tipo di entità `giftcardaccount`. Questo endpoint richiede la risorsa dell&#39;elenco di controllo di accesso (ACL) `Magento_ImportJsonApi::import_api` oltre all&#39;ACL dell&#39;account gift card.

### Comportamenti supportati

| Comportamento | Descrizione |
|---|---|
| `append` | Crea nuovi account gift card. Se esiste già un codice, la riga non riesce e l’importazione continua con le righe rimanenti. |
| `replace` | Aggiorna e inserisce gli account gift card in base al codice. Crea l&#39;account se il codice non esiste e lo sostituisce in caso affermativo. |
| `delete` | Rimuove gli account gift card per codice. |

### Esempio di richiesta

```json
{
  "source": {
    "entity": "giftcardaccount",
    "behavior": "append",
    "validation_strategy": "validation-stop-on-errors",
    "allowed_error_count": "10",
    "items": [
      {
        "code": "BULK-001",
        "balance": 50.00,
        "website_id": 1,
        "status": 1,
        "state": 0,
        "is_redeemable": 1,
        "date_expires": "2027-06-30"
      },
      {
        "code": "BULK-002",
        "balance": 25.00,
        "website_id": 1
      }
    ]
  }
}
```

### Dettagli del comportamento di importazione

* Ogni riga nel payload di importazione richiede un `website_id` esplicito, a differenza degli endpoint REST che derivano il sito web dalle intestazioni delle richieste.
* Ogni riga viene convalidata in modo indipendente. Le righe non valide generano errori per riga senza influire sulle righe valide nello stesso batch.
* I codici duplicati all’interno dello stesso batch vengono rilevati e segnalati come errori per riga, anziché causare un rollback della transazione.
* L&#39;importazione scrive direttamente nel database per le prestazioni e ignora il ciclo di vita di salvataggio del modello del fornitore. Le voci della cronologia di modifica del saldo non vengono create durante l&#39;importazione.
* Le operazioni di creazione REST rifiutano le date di scadenza passate. L’importazione accetta le date di scadenza precedenti per progettazione, per supportare la migrazione dei dati storici.

## Gestione degli errori

L’API restituisce i codici di stato HTTP standard:

| Codice di stato | Condizione |
|---|---|
| `400` | Errore di convalida. Campi obbligatori mancanti, valori non validi o data di scadenza passata durante la creazione REST. |
| `401` | Token bearer mancante o non valido. |
| `403` | Nel token manca la risorsa ACL richiesta. |
| `404` | Conto gift card non trovato. |
| `409` | Codice gift card duplicato. |

La convalida dell&#39;input copre i campi obbligatori, gli intervalli di valori (lo stato deve essere `0` o `1`, lo stato deve essere `0`-`3`, il saldo deve essere non negativo), il formato della data e la sicurezza del tipo. I valori non numerici per i campi numerici vengono rifiutati.
