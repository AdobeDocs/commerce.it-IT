---
title: Sincronizzare i feed utilizzando Commerce CLI
description: Scopri come utilizzare i comandi CLI di Commerce per gestire i feed e sincronizzare i processi per  [!DNL data export extension]  nei servizi SaaS di Adobe Commerce.
autotag-review: '2026-06-17T15:08:59.000Z'
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
TQID: 'https://experienceleague.adobe.com/Vi8hMKOBjTPkSQp0t8DCkjZsJ8s3Q5GSbSXyX2gmWRo'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: ef1a9efc579d8d21c145e6981235489a2e4ea203
workflow-type: tm+mt
source-wordcount: 728
ht-degree: 0%

---

# Sincronizzare i feed utilizzando Commerce CLI

Il comando `saas:resync` nel pacchetto `magento/saas-export` consente di gestire la sincronizzazione dei dati per i servizi SaaS [!DNL Adobe Commerce].

>[!NOTE]
>
>Il comando `saas:resync` si applica anche a [!DNL Adobe Commerce Optimizer Connector] feed come `products`, `categories` e `priceBooks`. Per l&#39;elenco completo dei feed dei connettori e dei nomi degli indicizzatori, vedere [Feed supportati](../aco-connector/reference/connector-reference.md#supported-feeds).

Adobe sconsiglia di utilizzare il comando `saas:resync` regolarmente. Gli scenari tipici per l’utilizzo del comando sono:

- Sincronizzazione iniziale
- Sincronizza i dati con un nuovo spazio dati dopo aver modificato l&#39;[ID spazio dati SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Risoluzione dei problemi

Monitorare le operazioni di sincronizzazione nel file `var/log/saas-export.log`.

## Sincronizzazione iniziale

>[!NOTE]
>
>La sincronizzazione iniziale viene eseguita automaticamente quando sono abilitati Live Search o Product Recommendations. Non sono necessari comandi manuali.
>
>Per le distribuzioni di [!DNL Adobe Commerce Optimizer Connector], il comando `aco:config:init` pianifica la sincronizzazione completa iniziale invalidando tutti gli indicizzatori del feed del connettore. Vedi [Abilitare l&#39;integrazione [!DNL Commerce Optimizer] ](../aco-connector/get-started.md#enable-the-adobe-commerce-optimizer-integration) e [Gestire la sincronizzazione in [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md).

Quando si attiva `saas:resync` dalla riga di comando, a seconda delle dimensioni del catalogo, l&#39;aggiornamento dei dati può richiedere da alcuni minuti ad alcune ore.

Le sincronizzazioni dei feed possono essere eseguite in qualsiasi ordine, non esistono dipendenze rigide tra di esse. La sequenza seguente inizia con i dati di ambito, che è un punto di partenza logico poiché gli ambiti definiscono le viste archivio a cui fanno riferimento gli altri feed.

```shell
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed productAttributes
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed products
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed productoverrides
```

>[!NOTE]
>
>L’ambiente potrebbe non includere tutti i feed in questa sequenza. Consulta [Feed supportati](reference/feed-table-reference.md#supported-feeds) per l&#39;elenco completo dei feed, i nomi dei feed CLI e i requisiti dei moduli.

## Opzioni di comando

Il comando `saas:resync` supporta diverse operazioni di sincronizzazione:

- Sincronizzazione parziale con SKU
- Riprendi sincronizzazioni interrotte
- Convalida dei dati senza sincronizzazione

Visualizza tutte le opzioni di comando e i flag:

```shell
bin/magento saas:resync --help
```

Per la descrizione delle opzioni con esempi, consulta le sezioni seguenti.

>[!NOTE]
>
>Per le opzioni avanzate per gestire l&#39;elaborazione dell&#39;esportazione, vedere [Personalizzare l&#39;elaborazione dell&#39;esportazione](customize-export-processing.md).

## `--feed`

Obbligatorio. Specifica l&#39;entità feed da risincronizzare.

`bin/magento saas:resync --help` documenta le opzioni e i flag del comando. Non elenca tutti i feed disponibili nell’ambiente. Per l&#39;elenco completo dei feed con nomi di feed CLI, ID di indicizzatore e tabelle di feed, vedere [Feed supportati](reference/feed-table-reference.md#supported-feeds).

>[!NOTE]
>
>I moduli installati determinano i feed da risincronizzare. `productOverrides` richiede ad esempio [!DNL Adobe Commerce] nel cloud, nei locali o Commerce as a Cloud Service e `orders` richiede il modulo Ordini di vendita.

>[!NOTE]
>
>Il comando `saas:resync` trasmette solo i nuovi elementi, gli elementi aggiornati e gli elementi che in precedenza non erano stati esportati. Gli elementi il cui hash di contenuto non è stato modificato dall&#39;ultima esportazione vengono ignorati.

**Esempio:**

```shell
bin/magento saas:resync --feed products
```

## `--by-ids`

Risincronizza parzialmente entità specifiche in base ai loro ID. Supporta `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` e `categoryPermissions` feed.

Per impostazione predefinita, quando si utilizza l&#39;opzione `--by-ids` si specificano valori utilizzando i valori SKU del prodotto. Per utilizzare gli ID prodotto, aggiungere l&#39;opzione `--id-type=productId`.

>[!NOTE]
>
>A differenza di una risincronizzazione standard, `--by-ids` ignora la verifica hash e forza l&#39;invio delle entità specificate ai servizi Commerce connessi indipendentemente dal fatto che il contenuto sia stato modificato dopo l&#39;ultima esportazione.

**Esempi:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

## `--cleanup-feed`

Pulisci la tabella dell’indicizzatore del feed prima della reindicizzazione e dell’invio dei dati a SaaS. Supportato solo per `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` e `categoryPermissions`.

Se utilizzata con l&#39;opzione `--dry-run`, l&#39;operazione esegue un&#39;operazione di risincronizzazione a secco per tutti gli elementi.

>[!WARNING]
>
>L&#39;utilizzo del comando di risincronizzazione con l&#39;opzione `cleanup-feed` cancella lo stato di esportazione del feed locale e può causare una sincronizzazione incompleta. È possibile, ad esempio, che le eliminazioni di entità in [!DNL Adobe Commerce] non vengano applicate ai servizi Commerce connessi o che entità non aggiornate rimangano negli indici remoti di Commerce Services anche se sono state eliminate o aggiornate in [!DNL Adobe Commerce]. Utilizza questa opzione solo per le ricompilazioni complete dell’ambiente, ad esempio dopo una pulizia dello spazio dati SaaS.

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

**Esempio:**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--no-reindex`

Invia nuovamente i dati del catalogo esistenti a [!DNL Commerce Services] senza reindicizzazione. Non supportato per feed relativi a prodotti.

Il comportamento varia in base alla [modalità di esportazione](sync-overview.md#synchronization-modes):

- Modalità legacy: invia nuovamente tutti i dati senza troncarli.
- Modalità immediata: l’opzione viene ignorata, sincronizza solo gli aggiornamenti/errori.

**Esempio:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

>[!MORELIKETHIS]
>
> - [Esaminare i registri e risolvere i problemi](troubleshooting/logging.md) — Eseguire la diagnostica degli errori di esportazione dei dati e SaaS.
> - [Risoluzione dei problemi di scenari](troubleshooting/troubleshooting-scenarios.md) — Risoluzione dei problemi di configurazione errata e dei risultati di sincronizzazione imprevisti.
> - [Funzionamento della sincronizzazione](sync-overview.md): informazioni sulle modalità di sincronizzazione e sul comportamento dei tentativi.
