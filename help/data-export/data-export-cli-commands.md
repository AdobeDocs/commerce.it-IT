---
title: Interfaccia della riga di comando per l'esportazione dei dati SaaS
description: Scopri come utilizzare i comandi dell’interfaccia della riga di comando per gestire feed e processi per  [!DNL data export extension]  per i servizi SaaS di Adobe Commerce.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Riferimento all&#39;interfaccia della riga di comando per l&#39;esportazione di dati SaaS

Gli sviluppatori e gli amministratori di sistema possono gestire le operazioni di sincronizzazione per l&#39;esportazione di dati SaaS utilizzando lo strumento da riga di comando [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI). Il comando `saas:resync` è incluso nel pacchetto `magento/saas-export`.

Adobe sconsiglia di utilizzare il comando `saas:resync` regolarmente. Gli scenari tipici per l’utilizzo del comando sono:

- Sincronizzazione iniziale
- L&#39;ID dello spazio dati [SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) è stato modificato ed è necessario sincronizzare i dati con il nuovo spazio dati.
- Risoluzione dei problemi

## Sincronizzazione iniziale

>[!NOTE]
>Se utilizzi Live Search o Product Recommendations, non è necessario eseguire la sincronizzazione iniziale. Il processo viene avviato automaticamente dopo la connessione del servizio all’istanza di Commerce.

Quando si attiva `saas:resync` dalla riga di comando, a seconda delle dimensioni del catalogo, l&#39;aggiornamento dei dati può richiedere da alcuni minuti ad alcune ore.

Per la sincronizzazione iniziale, Adobe consiglia di eseguire i comandi nel seguente ordine:

```bash
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

## Esempi di comandi

Prima di utilizzare i comandi `saas:resync`, controlla le [descrizioni delle opzioni](#command-options).

- Eseguire una risincronizzazione completa per un feed di entità.

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  I feed già esportati non vengono risincronizzati.

- Risincronizzazione completa del feed specificato e dei dati di pulizia

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  Utilizzare solo dopo l&#39;esecuzione di un&#39;operazione [!DNL Data Space ID Cleanup].

- Per i feed di esportazione immediati, invia nuovamente tutti i dati ai servizi Commerce connessi senza troncare i dati di indice nella tabella dei feed

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- Elenca i comandi e le opzioni disponibili con le relative descrizioni.

  ```
  bin/magento saas:resync --help
  ```

## Opzioni di comando

Le opzioni seguenti sono disponibili per la gestione di `saas:resync` operazioni.

>[!NOTE]
>
>Il comando `saas:resync` supporta inoltre opzioni avanzate per migliorare i comandi di esportazione dei dati aumentando le dimensioni del batch e aggiungendo l&#39;elaborazione multi-thread. Vedi [Personalizzare l&#39;elaborazione dell&#39;esportazione](customize-export-processing.md).

### `feed`

Questa opzione obbligatoria specifica l&#39;entità feed da risincronizzare, ad esempio `products`.

Il valore dell&#39;opzione `feed` può includere qualsiasi feed di entità disponibile:

- `products`: feed dati prodotto
- `productAttributes`: feed dati attributi prodotto
- `categories`: feed dati categorie
- `variants`: feed dati varianti prodotto configurabili
- `prices`: feed dati prezzi prodotto
- `categoryPermissions`: feed dati per autorizzazioni categoria
- `productOverrides`: feed dati delle autorizzazioni del prodotto
- `inventoryStockStatus`: feed dati stato scorte
- `scopesWebsite`: siti Web con feed di dati di visualizzazioni store e store
- `scopesCustomerGroup`: feed dati per gruppi di clienti
- `orders`: feed dati ordini cliente

A seconda dei [Servizi Commerce](../landing/saas.md) installati, è possibile che sia disponibile un diverso set di feed per il comando `saas:resync`.

### `no-reindex`

Questa opzione invia nuovamente i dati del catalogo esistenti a [!DNL Commerce Services] senza reindicizzazione. Se questa opzione non è specificata, il comando esegue una reindicizzazione completa prima di sincronizzare i dati.

Il comportamento di questa opzione dipende dal fatto che il feed sia esportato in [modalità di esportazione legacy o immediata](data-synchronization.md#synchronization-modes)

- Per i feed di esportazione legacy, il processo di sincronizzazione non tronca i dati indicizzati nella tabella dei feed. Al contrario, invia nuovamente tutti i dati al servizio Adobe Commerce.
- Per i feed di esportazione immediati, questa opzione viene ignorata se specificata. Per questi feed, il processo di risincronizzazione non troncerà l&#39;indice e risincronizza solo gli aggiornamenti o gli elementi con errori precedenti.

### `cleanup`

Questa opzione consente di pulire la tabella dell’indicizzatore del feed prima di una sincronizzazione. Se specificato, l&#39;esportazione dei dati SaaS esegue una risincronizzazione completa per il feed specificato e pulisce tutti i dati esistenti nella tabella dei feed.

Adobe consiglia di utilizzare questo comando solo dopo aver eseguito l&#39;operazione [!DNL Data Space ID Cleanup].

>[!WARNING]
>
>**Non utilizzare questa opzione regolarmente**. Può causare problemi di sincronizzazione dei dati nei servizi Adobe Commerce. `delete product event` potrebbe ad esempio non propagarsi al servizio Adobe Commerce se si utilizza l&#39;opzione `cleanup`.

## Risoluzione dei problemi

Se non vengono visualizzati i dati previsti nei servizi Commerce connessi, risolvere i problemi verificando i registri degli errori di esportazione dei dati e utilizzando il comando `saas:resync` con variabili di ambiente per rivedere i payload e i dati del profiler. Consulta [Esaminare i registri e risolvere i problemi](troubleshooting-logging.md).
