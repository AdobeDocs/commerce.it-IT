---
title: Miglioramento delle prestazioni di esportazione dei dati SaaS
description: Scopri come migliorare le prestazioni di esportazione dei dati SaaS per i servizi Commerce utilizzando una modalità di esportazione dei dati con più thread.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 7151118c-5e30-44d0-b515-5801a73e44ec
TQID: https://experienceleague.adobe.com/k-gizR-v-zQjQiN5IZm1Mv87J6j9eMsxH8vl-K1Co2M
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 669
ht-degree: 0%

---

# Miglioramento delle prestazioni di esportazione dei dati SaaS

**La modalità di esportazione dei dati multi-thread** accelera il processo di esportazione dividendo i dati di feed in batch ed elaborandoli simultaneamente.

Gli sviluppatori o gli integratori di sistemi possono migliorare le prestazioni utilizzando la modalità di esportazione dati multi-thread invece della modalità single-thread predefinita. Nella modalità a thread singolo, non esiste alcuna parallelizzazione del processo di invio del feed. Inoltre, a causa dei limiti predefiniti impostati, tutti i client possono utilizzare un solo thread. Nella maggior parte dei casi, la personalizzazione della configurazione non è necessaria.

## Considerazioni per l’utilizzo della modalità multi-thread

Quando si lavora con i servizi di esportazione dei dati, è necessario ottimizzare le prestazioni garantendo al contempo una sincronizzazione accurata.
Adobe consiglia di utilizzare la configurazione predefinita per l’acquisizione dei dati, che in genere soddisfa i requisiti di sincronizzazione per gli esercenti Commerce. Tuttavia, in alcuni scenari la personalizzazione può velocizzare i tempi di elaborazione.

Quando decidi se personalizzare la configurazione di esportazione dei dati, considera i seguenti fattori chiave:

- **Sincronizzazione iniziale**-Valutare il numero di prodotti e [stimare il volume di dati e il tempo di trasmissione](estimate-data-volume-sync-time.md) in base alla configurazione predefinita. Chiediti: puoi attendere questa sincronizzazione iniziale dei dati dopo aver effettuato l’onboarding di un servizio Commerce?

- **Aggiunta di nuove visualizzazioni dello store o siti Web** - Se si prevede di aggiungere visualizzazioni dello store o siti Web con lo stesso numero di prodotti dopo la pubblicazione, stimare il volume di dati e il tempo di trasmissione. Determina se il tempo di sincronizzazione è accettabile con la configurazione predefinita o se è necessaria l’elaborazione multi-thread.

- **Importazioni regolari**-Anticipa le importazioni regolari, ad esempio gli aggiornamenti dei prezzi o le modifiche dello stato delle scorte. Valuta se questi aggiornamenti possono essere applicati entro un intervallo di tempo accettabile o se è necessaria un’elaborazione più rapida.

- **Peso prodotto**-Valuta se i tuoi prodotti sono leggeri o pesanti. Regolare di conseguenza la dimensione del batch se le descrizioni o gli attributi del prodotto aumentano la dimensione del prodotto.

Tenere presente che una pianificazione attenta, che includa la stima del volume dei dati e del tempo di sincronizzazione, può spesso eliminare la necessità di personalizzazione. Pianifica le operazioni di acquisizione dei feed in base a queste stime per ottenere risultati ottimali.

>[!NOTE]
>
>Adobe consiglia di prestare attenzione quando si utilizza l’elaborazione con più thread. Se configuri il multi-threading per prestazioni più veloci, puoi attivare i guardrail dei servizi Adobe Commerce inclusi per evitare l’uso improprio del sistema durante l’acquisizione dei dati. Questi guardrail impediscono inoltre agli utenti di attivare le modifiche di sincronizzazione che possono sovraccaricare il sistema. Quando vengono attivate le protezioni, le richieste vengono bloccate e il sistema restituisce 429 errori. Se si verificano questi errori, regolare la configurazione e inviare un ticket di supporto per assistenza.

## Configurare il multithreading

La modalità multithread è supportata per tutti i [metodi di sincronizzazione](sync-overview.md#synchronization-types): sincronizzazione completa, sincronizzazione parziale e sincronizzazione elementi non riuscita. Per configurare il multithreading, specificare il numero di thread e la dimensione del batch da utilizzare durante la sincronizzazione.

- `thread-count` è il numero di thread attivati per elaborare le entità. Il valore predefinito `thread-count` è `1`.
- `batch-size` è il numero di entità elaborate in un&#39;iterazione. Il valore predefinito `batch-size` è `100` record per tutti i feed ad eccezione del feed di prezzo. Per il feed di prezzo, il valore predefinito è `500` record.

>[!NOTE]
>
>Per le distribuzioni di [!DNL Adobe Commerce Optimizer Connector], controlla i feed supportati specifici del connettore e i limiti batch in [Moduli connettore ed endpoint di feed](../aco-connector/reference/connector-reference.md#supported-feeds).

È possibile configurare il multithreading come opzione temporanea durante l&#39;esecuzione di un comando di risincronizzazione oppure aggiungendo la configurazione del multithread alla configurazione dell&#39;applicazione Adobe Commerce.

>[!NOTE]
>
>Assicurati di allineare le prestazioni dell’esportazione di dati SaaS con il limite di velocità definito per un client sul lato consumer.

### Configurare il multithreading in fase di runtime

Quando si esegue un comando di sincronizzazione completa dalla riga di comando, specificare l&#39;elaborazione multi-thread aggiungendo le opzioni `thread-count` e `batch-size` al comando CLI.

```shell
bin/magento saas:resync --feed=products --thread-count=2 --batch-size=200
```

Le opzioni specificate nella riga di comando sovrascrivono la configurazione di esportazione dei dati specificata nel file dell&#39;applicazione Adobe Commerce `config.php`.

### Aggiungere il multithreading alla configurazione di Commerce

Per elaborare tutte le operazioni di esportazione dei dati utilizzando il multithreading, gli integratori di sistemi o gli sviluppatori possono modificare il numero di thread e la dimensione batch per ogni feed nella configurazione dell’applicazione Commerce.

Queste modifiche possono essere applicate aggiungendo valori personalizzati alla [sezione di sistema](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/files/config-reference-configphp#system) del file di configurazione, `app/etc/config.php`.

**Esempio: configurazione del multithreading per prodotti e prezzi**

```php
<?php
return [
    'system' => [
        'default' => [
            'commerce_data_export' => [
                'feeds' => [
                    'products' => [
                        'batch_size' => 100,
                        'thread_count' => 2,
                    ],
                    'prices' => [
                        'batch_size' => 400,
                        'thread_count' => 4,
                    ]
                ]
            ],
//   ...
```

>[!MORELIKETHIS]
>
> - [Stimare il volume dei dati e il tempo di trasmissione](estimate-data-volume-sync-time.md)
> - [Funzionamento della sincronizzazione](sync-overview.md)
> - [Schema tabella feed](reference/feed-table-reference.md)
