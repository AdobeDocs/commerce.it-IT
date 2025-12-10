---
title: Sincronizzare i feed utilizzando Commerce CLI
description: Scopri come utilizzare i comandi dell’interfaccia della riga di comando per gestire feed e processi per  [!DNL data export extension]  per i servizi SaaS di Adobe Commerce.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Sincronizzare i feed utilizzando Commerce CLI

Il comando `saas:resync` nel pacchetto `magento/saas-export` consente di gestire la sincronizzazione dei dati per i servizi SaaS di Adobe Commerce.

Adobe sconsiglia di utilizzare il comando `saas:resync` regolarmente. Gli scenari tipici per l’utilizzo del comando sono:

- Sincronizzazione iniziale
- Sincronizza i dati con un nuovo spazio dati dopo aver modificato l&#39;[ID spazio dati SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Risoluzione dei problemi

Monitorare le operazioni di sincronizzazione nel file `var/log/saas-export.log`.

## Sincronizzazione iniziale

>[!NOTE]
>
>La sincronizzazione iniziale viene eseguita automaticamente quando sono abilitati Live Search o Product Recommendations. Non sono necessari comandi manuali.

Quando si attiva `saas:resync` dalla riga di comando, a seconda delle dimensioni del catalogo, l&#39;aggiornamento dei dati può richiedere da alcuni minuti ad alcune ore.

Per la sincronizzazione iniziale, Adobe consiglia di eseguire i comandi nel seguente ordine:

```shell
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

## Sincronizza con i comandi CLI

Il comando `saas:resync` supporta diverse operazioni di sincronizzazione:

- Sincronizzazione parziale con SKU
- Riprendi sincronizzazioni interrotte
- Convalida dei dati senza sincronizzazione

Visualizza tutte le opzioni disponibili:

```shell
bin/magento saas:resync --help
```

Per la descrizione delle opzioni con esempi, consulta le sezioni seguenti.


>[!NOTE]
>
>Per le opzioni avanzate per gestire l&#39;elaborazione dell&#39;esportazione, vedere [Personalizzare l&#39;elaborazione dell&#39;esportazione](customize-export-processing.md).

## `--by-ids`

Risincronizza parzialmente entità specifiche in base ai loro ID. Supporta `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` e `categoryPermissions` feed.

Per impostazione predefinita, quando si utilizza l&#39;opzione `--by-ids` si specificano valori utilizzando i valori SKU del prodotto. Per utilizzare gli ID prodotto, aggiungere l&#39;opzione `--id-type=ProductID`.

**Esempi:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

Pulisci la tabella dell’indicizzatore del feed prima della reindicizzazione e dell’invio dei dati a SaaS. Supportato solo per `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` e `categoryPermissions`.

Se utilizzata con l&#39;opzione `--dry-run`, l&#39;operazione esegue un&#39;operazione di risincronizzazione a secco per tutti gli elementi.

>[!IMPORTANT]
>
>Usare solo dopo la pulizia dell&#39;ambiente o con l&#39;opzione `--dry-run`. Se utilizzata in altri casi, l’operazione di pulizia può causare la perdita di dati e problemi di sincronizzazione dei dati.

**Esempio:**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

Riprende un&#39;operazione di risincronizzazione interrotta. Supportato solo per `products`, `productAttributes` e `productOverrides` feed.

**Esempio:**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

Esegue il processo di reindicizzazione del feed senza inviare il feed a SaaS e senza salvarlo nella tabella del feed. Questa opzione è utile per identificare eventuali problemi con il set di dati.

Aggiungi la variabile di ambiente `EXPORTER_EXTENDED_LOG=1` per salvare il payload in `var/log/saas-export.log`.

**Esempio:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### Verifica elementi di feed specifici

Verificare elementi di feed specifici aggiungendo l&#39;opzione `--by-ids` con la raccolta di registri estesi per visualizzare il payload generato nel file `var/log/saas-export.log`.

**Esempio:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### Test di tutti gli elementi feed

Per impostazione predefinita, il feed inviato durante un&#39;operazione `resync --dry-run` include solo i nuovi elementi o gli elementi che non è stato possibile esportare in precedenza. Per includere tutti gli elementi nel feed da elaborare, utilizzare l&#39;opzione `--cleanup-feed`.

**Esempio**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--feed`

Obbligatorio. Specifica l&#39;entità feed da risincronizzare.

Feed disponibili:

- `categories`
- `categoryPermissions`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

>[!NOTE]
>
>I feed disponibili nell’ambiente potrebbero essere diversi a seconda dei moduli installati nell’ambiente Adobe Commerce.

**Esempio:**

```shell
bin/magento saas:resync --feed products
```

## `--no-reindex`

Invia nuovamente i dati del catalogo esistenti a [!DNL Commerce Services] senza reindicizzazione. Non supportato per feed relativi a prodotti.

Il comportamento varia in base alla [modalità di esportazione](data-synchronization.md#synchronization-modes):

- Modalità legacy: invia nuovamente tutti i dati senza troncarli.
- Modalità immediata: l’opzione viene ignorata, sincronizza solo gli aggiornamenti/errori.

**Esempio:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

## `--id-type=ProductId`

Per impostazione predefinita, le entità specificate quando si utilizza il comando `saas:resync feed` con l&#39;opzione `--by-ids` vengono specificate per SKU prodotto. Utilizzare l&#39;opzione `--id-type=ProductId` per specificare le entità in base all&#39;ID prodotto.

```shell
bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

**Esempio:**

## Risoluzione dei problemi

Se non vengono visualizzati i dati previsti nei servizi Commerce connessi, risolvere i problemi verificando i registri degli errori di esportazione dei dati e utilizzando il comando `saas:resync` con variabili di ambiente per rivedere i payload e i dati del profiler. Consulta [Esaminare i registri e risolvere i problemi](troubleshooting-logging.md).
