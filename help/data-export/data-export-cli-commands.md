---
title: Sincronizzare i feed utilizzando Commerce CLI
description: Scopri come utilizzare i comandi dell’interfaccia della riga di comando per gestire feed e processi per  [!DNL data export extension]  per i servizi SaaS di Adobe Commerce.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 086a571b69e8ad76a912c339895409b0037642b9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# Sincronizzare i feed utilizzando Commerce CLI

Il comando `saas:resync` nel pacchetto `magento/saas-export` consente di gestire la sincronizzazione dei dati per i servizi SaaS di Adobe Commerce.

Adobe sconsiglia di utilizzare il comando `saas:resync` regolarmente. Gli scenari tipici per l’utilizzo del comando sono:

- Sincronizzazione iniziale
- Sincronizza i dati con il nuovo spazio dati dopo aver modificato l&#39;[ID spazio dati SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
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

Risincronizza parzialmente entità specifiche in base ai loro ID. Supporta `products`, `productAttributes` e `productOverrides` feed.

Per impostazione predefinita, le entità sono specificate per SKU prodotto. Utilizza `--id-type=ProductID` per utilizzare gli ID prodotto.

**Esempi:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<SKU-1>,<SKU-2>,<SKU-3>'

bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<ID-1>,<ID-2>,<ID-3>' --id-type='productId'
```

## `--cleanup-feed`

Pulisce la tabella dell&#39;indicizzatore del feed prima della reindicizzazione e dell&#39;invio dei dati a SaaS. Supportato solo per `products`, `productOverrides` e `prices` feed.

>[!IMPORTANT]
>
>Da utilizzare solo dopo la pulizia dell’ambiente. Può causare problemi di sincronizzazione dei dati nei servizi Commerce.

**Esempio:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --cleanup-feed
```

## `--continue-resync`

Riprende un&#39;operazione di risincronizzazione interrotta. Supportato solo per `products`, `productAttributes` e `productOverrides` feed.

**Esempio:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --continue-resync
```

## `--dry-run`

Esegue il processo di reindicizzazione del feed senza inviarlo a SaaS o salvarlo nella tabella di feed. Utilizza per convalidare i dati.

Aggiungi la variabile di ambiente `EXPORTER_EXTENDED_LOG=1` per salvare il payload in `var/log/saas-export.log`.

**Esempio:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed='<FEED_NAME>' --dry-run
```

## `--feed`

Obbligatorio. Specifica l&#39;entità feed da risincronizzare.

Feed disponibili:

- `categories`
- `categoryPermissions`
- `inventoryStockStatus`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

**Esempio:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>'
```

## `--no-reindex`

Invia nuovamente i dati del catalogo esistenti a [!DNL Commerce Services] senza reindicizzazione. Non supportato per feed relativi a prodotti.

Il comportamento varia in base alla [modalità di esportazione](data-synchronization.md#synchronization-modes):

- Modalità legacy: invia nuovamente tutti i dati senza troncarli.
- Modalità immediata: l’opzione viene ignorata, sincronizza solo gli aggiornamenti/errori.

**Esempio:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --no-reindex
```

## Risoluzione dei problemi

Se non vengono visualizzati i dati previsti nei servizi Commerce connessi, risolvere i problemi verificando i registri degli errori di esportazione dei dati e utilizzando il comando `saas:resync` con variabili di ambiente per rivedere i payload e i dati del profiler. Consulta [Esaminare i registri e risolvere i problemi](troubleshooting-logging.md).
