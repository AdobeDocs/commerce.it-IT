---
title: Revisione dei registri e risoluzione dei problemi
description: Scopri come risolvere i problemi di  [!DNL data export]  errori utilizzando i registri di esportazione dei dati e saas.
feature: Services
exl-id: d022756f-6e75-4c2a-9601-31958698dc43
source-git-commit: 22c74c12ddfccdb4e6c4e02c3a15557e1020d5ef
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# Revisione dei registri e risoluzione dei problemi

L&#39;estensione [!DNL data export] fornisce i registri per tenere traccia dei processi di raccolta e sincronizzazione dei dati.

## Registri

I registri sono disponibili nella directory `var/log` nel server applicazioni Commerce.

| nome registro | nome file | descrizione |
|-----------------| ----------| -------------|
| Registro esportazione dati SaaS | `commerce-data-export.log` | Fornisce informazioni sulle attività di esportazione dei dati, come eventi di entità e trigger di risincronizzazione completa.  Ogni record di registro ha una struttura specifica e fornisce informazioni sul feed, sull’operazione, sullo stato, sul tempo trascorso, sull’ID processo e sul chiamante. |
| Registro errori esportazione dati SaaS | `data-export-errors.log` | Fornisce messaggi di errore e tracce dello stack per gli errori che si verificano durante il processo di sincronizzazione dei dati. |
| Registro di esportazione SaaS | `saas-export.log` | Fornisce informazioni sui dati inviati ai servizi SaaS di Commerce. |
| Registro errori esportazione SaaS | `saas-export-errors.log` | Fornisce informazioni sugli errori che si verificano durante l’invio di dati ai servizi SaaS di Commerce. |

Se non visualizzi i dati previsti per un servizio Adobe Commerce, utilizza i registri di errore per l’estensione di esportazione dei dati per determinare dove si è verificato il problema. Inoltre, puoi estendere i registri con dati aggiuntivi per il tracciamento e la risoluzione dei problemi. Vedi [Registrazione estesa](#extended-logging).

### Formato registro

Ogni record di registro ha la seguente struttura.

```
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elapsed from script run>",
   "pid": "<process id that executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>La stringa basata su JSON è ottimizzata per una migliore leggibilità.

Nella tabella seguente sono descritti i tipi di operazioni che è possibile registrare nei registri.

| Operazione | Descrizione | Esempio chiamante |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| sincronizzazione completa | Raccoglie e invia tutti i dati all’SaaS per un determinato feed. | `bin/magento saas:resync --feed=products` |
| reindicizzazione parziale | Raccoglie e invia dati a SaaS solo per entità aggiornate in un determinato feed. Questo registro è presente solo se esistono entità aggiornate. | `bin/magento cron:run --group=index` |
| riprova elementi non riusciti | Inviare nuovamente gli elementi per un determinato feed a SaaS se l&#39;operazione di sincronizzazione precedente non è riuscita a causa di un errore dell&#39;applicazione Commerce o del server. Questo registro è presente solo se sono presenti elementi non riusciti. | `bin/magento cron:run --group=saas_data_exporter` (qualsiasi gruppo cron &quot;*_data_exporter&quot;) |
| sincronizzazione completa (legacy) | Raccoglie e invia tutti i dati a SaaS per un determinato feed in modalità di esportazione legacy. | `bin/magento saas:resync --feed=categories` |
| reindicizzazione parziale (legacy) | Invia entità aggiornate a SaaS per un determinato feed in modalità di esportazione legacy. Questo registro è presente solo se esistono entità aggiornate. | `bin/magento cron:run --group=index` |
| sincronizzazione parziale (legacy) | Invia entità aggiornate a SaaS per un determinato feed in modalità di esportazione legacy. Questo registro è presente solo se esistono entità aggiornate. | `bin/magento cron:run --group=saas_data_exporter` (qualsiasi gruppo cron &quot;*_data_exporter&quot;) |


### Esempi di registrazione

Durante una risincronizzazione completa, l&#39;avanzamento viene tracciato e registrato ogni 30 secondi per impostazione predefinita. Di seguito è riportato un esempio di voce di registro.

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

In questo esempio, i valori `status` forniscono informazioni sull&#39;operazione di sincronizzazione:

- **`"Progress 2/5"`** indica che 2 delle 5 iterazioni sono state completate. Il numero di iterazioni dipende dal numero di entità esportate.
- **`"processed: 200"`** indica che sono stati elaborati 200 elementi.
- **`"synced: 100"`** indica che 100 elementi sono stati inviati a SaaS. `"synced"` non è uguale a `"processed"`. Ecco un esempio:
   - **`"synced" < "processed"`** significa che la tabella di feed non ha rilevato alcuna modifica nell&#39;elemento rispetto alla versione sincronizzata in precedenza. Tali elementi vengono ignorati durante l&#39;operazione di sincronizzazione.
   - **`"synced" > "processed"`** lo stesso id entità (ad esempio, `Product ID`) può avere più valori in ambiti diversi. Ad esempio, un prodotto può essere assegnato a cinque siti web. In questo caso, potresti avere &quot;1 elemento elaborato&quot; e &quot;5 elementi sincronizzati&quot;.

+++ **Esempio: log di risincronizzazione completo per il feed di prezzo**

```
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## Visualizzare e risolvere i problemi dei registri con New Relic

Se archivi i registri di Adobe Commerce in New Relic, puoi aggiungere regole di analisi per migliorare la leggibilità e l’esperienza di query.

1. Accedi a New Relic.

1. Vai a `Logs => Parsing`.

1. Fare clic su `Create parsing rule`.

1. Configura la regola di analisi aggiungendo i seguenti valori.

   - **Filtra i registri in base a NRQL**

     `filePath LIKE '%commerce-data-export%.log'`

   - **Regola di analisi**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel} %{GREEDYDATA:feed:json}`

In questo esempio viene aggiunta una regola che consente di eseguire query sui registri di New Relic per tipo di feed, operazione e così via.

**Esempio di stringa di query**—`feed.feed:"products" and feed.status:"Complete"`

## Risoluzione dei problemi

Se i dati mancano o sono errati nei servizi Commerce, controlla i registri per individuare eventuali messaggi di errore che si sono verificati durante la sincronizzazione da Adobe Commerce alla piattaforma dei servizi Commerce. Se necessario, utilizza la registrazione estesa per aggiungere ulteriori informazioni ai registri per la risoluzione dei problemi.

- Il log degli errori di esportazione dei dati (`commerce-data-export-errors.log`) acquisisce gli errori che si verificano durante la fase di raccolta.
- Il log degli errori di esportazione SaaS (`saas-export-errors.log`) acquisisce gli errori che si verificano durante la fase di trasmissione.

Se vengono visualizzati errori non correlati alla configurazione o alle estensioni di terze parti, invia un [ticket di supporto](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) con il maggior numero di informazioni possibile.

### Risolvi problemi di sincronizzazione catalogo {#resolvesync}

Quando attivi una risincronizzazione dei dati, l’aggiornamento dei dati può richiedere fino a un’ora e può essere incluso nei componenti dell’interfaccia utente, ad esempio le unità per la ricerca live e per la generazione di consigli. Se riscontri ancora delle discrepanze tra il catalogo e i dati nella vetrina di Commerce, o se la sincronizzazione del catalogo non è riuscita, fai riferimento a quanto segue:

#### Discrepanza dei dati

1. Visualizzare la visualizzazione dettagliata del prodotto in questione nei risultati della ricerca.
1. Copiare l&#39;output JSON e verificare che il contenuto corrisponda a quello presente nel catalogo [!DNL Commerce].
1. Se il contenuto non corrisponde, apporta una piccola modifica al prodotto nel catalogo, ad esempio aggiungendo uno spazio o un punto.
1. Attendere la risincronizzazione o [attivare una risincronizzazione manuale](#resync).

#### Sincronizzazione non in esecuzione

Se la sincronizzazione non è in esecuzione su una pianificazione o non è stato sincronizzato nulla, vedere questo articolo [KnowledgeBase](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce).

#### Sincronizzazione non riuscita

Se lo stato della sincronizzazione del catalogo è **Non riuscito**, inviare un [ticket di supporto](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

## Registrazione estesa

Utilizza le variabili di ambiente per estendere i registri con dati aggiuntivi per il tracciamento e la risoluzione dei problemi. Aggiungi la variabile di ambiente alla riga di comando quando esegui i comandi CLI di esportazione dei dati, come mostrato negli esempi seguenti.

### Verifica il payload del feed

Includere il payload del feed nel registro di esportazione SaaS aggiungendo la variabile di ambiente `EXPORTER_EXTENDED_LOG=1` quando si sincronizza nuovamente il feed.

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

Al termine dell&#39;operazione, il payload del feed è disponibile per la revisione nel registro di esportazione SaaS (`var/.log/saas-export.log`).

### Mantieni payload nella tabella dell’indice del feed

Per l&#39;estensione di esportazione dei dati Commerce SaaS (`magento/module-data-exporter`) 103.3.0 e versioni successive, i feed di esportazione immediati mantengono solo i dati minimi richiesti nella tabella dell&#39;indice. I feed includono tutti i feed dello stato delle scorte di magazzino e di catalogo.

La conservazione dei dati di payload nella tabella di indice non è consigliata negli ambienti di produzione, ma può essere utile in un ambiente di sviluppo. Includere il payload del feed nell&#39;indice aggiungendo la variabile di ambiente `PERSIST_EXPORTED_FEED=1` quando si risincronizza il feed.

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### Esegui il profiler per risolvere i problemi di prestazioni lente

Se il processo di reindicizzazione di un feed specifico richiede un tempo eccessivo, eseguire il profiler per raccogliere dati aggiuntivi che potrebbero essere utili per il team di supporto.

Eseguire il profiler aggiungendo la variabile di ambiente `EXPORTER_PROFILER=1` quando si esegue il comando reindex.

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

I dati del profiler vengono memorizzati nel log di esportazione dei dati (`var/log/commerce-data-export.log`) nel seguente formato:

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
