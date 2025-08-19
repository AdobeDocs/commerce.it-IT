---
title: Configurazione della riga di comando
description: Dopo l'installazione, è possibile configurare  [!DNL Payment Services] utilizzando l'interfaccia CLI (Command-Line Interface).
role: Admin, Developer
level: Intermediate
exl-id: 265ab1be-fe52-41f3-85cb-addbc2ddfb17
feature: Payments, Checkout, Configuration, Integration, Paas
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Configurazione della riga di comando

Dopo aver installato [!DNL Payment Services], è possibile configurarlo facilmente da [nella home](payments-home.md) o tramite l&#39;interfaccia della riga di comando (CLI).

## Configurare l’esportazione dei dati

[!DNL Payment Services] combina i dati degli ordini esportati da [!DNL Magento Open Source] e [!DNL Adobe Commerce] con i dati di pagamento aggregati dei fornitori di servizi di pagamento per creare report utili. L&#39;estensione [!DNL Payment Services] utilizza gli indicizzatori per raccogliere in modo efficiente tutti i dati necessari per i report.

Per informazioni sui dati utilizzati nel reporting di [!DNL Payment Services], vedere [Rapporto sullo stato dei pagamenti degli ordini](order-payment-status.md#data-used-in-the-report).

### Configura cron su [!DNL Magento Open Source]

Se si desidera utilizzare la modalità indice `BY SCHEDULE` in [!DNL Magento Open Source], è necessario configurare cron. Vedere [Configurare ed eseguire cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs).

### Imposta indici

I dati dell&#39;ordine vengono esportati e memorizzati nel servizio di pagamento utilizzando una delle due modalità di indice: `ON SAVE` (impostazione predefinita) o `BY SCHEDULE` (scelta consigliata).

I seguenti indici sono per [!DNL Payment Services]:

| Codice | Nome | Descrizione |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | Feed ordine di vendita | Genera l&#39;indice dei dati dell&#39;ordine |
| `sales_order_status_data_exporter` | Feed stati ordini di vendita | Genera l&#39;indice dei dati relativi agli stati degli ordini cliente |
| `store_data_exporter` | Feed store | Genera l&#39;indice dei dati dell&#39;archivio |

Per modificare la modalità dell&#39;indice per tutti e tre gli indicizzatori, eseguire:

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>Se non si specifica alcun indicizzatore nel comando, tutti gli indicizzatori verranno aggiornati allo stesso valore. Se si desidera modificare un indicizzatore specifico, è necessario elencarlo nel comando.

Per ulteriori informazioni sulla modifica manuale della modalità di un indicizzatore, vedere [Configurare gli indicizzatori](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"} nella documentazione per gli sviluppatori. Per informazioni su come modificarlo nell&#39;amministratore, vedere [Gestione indice](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"} nella guida utente di base.

### Reindicizzare manualmente i dati

È possibile reindicizzare manualmente i dati, anziché attenderne l&#39;esecuzione automatica. Per ulteriori informazioni, vedere [Reindicizza](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex){target="_blank"} in [Gestione degli indicizzatori](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"}.

Quando è impostata la modalità `BY SCHEDULE`, il sistema tiene traccia delle entità modificate e il processo cron aggiorna l&#39;indice in base a una pianificazione impostata. Vedere [Esegui cron dalla riga di comando](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run) in [Configura ed esegui cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)) per informazioni su come attivare manualmente l&#39;indicizzazione utilizzando i processi cron.

### Invia dati reindicizzati al servizio di pagamento

Dopo l&#39;indicizzazione, i dati verranno inviati automaticamente a [!DNL Payment Services]. Puoi anche attivare manualmente il processo di invio dei dati indicizzati con questo comando:

```bash
bin/magento saas:resync --feed [feedName]
```

Utilizza le seguenti opzioni di comando:

| Comando | Descrizione |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | Esegue una reindicizzazione del feed specificato e lo invia al servizio corrispondente |
| `bin/magento saas:resync --no-reindex` | Ignora l&#39;indicizzazione e invia dati non sincronizzati dagli indici |

Il parametro `--feed` consente di specificare il feed da inviare:

| Feed | Descrizione |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | Feed ordini in modalità Produzione |
| `paymentServicesOrdersSandbox` | Feed ordini in modalità Sandbox |
| `paymentServicesOrderStatusesProduction` | Stati degli ordini in modalità Produzione |
| `paymentServicesOrderStatusesSandbox` | Ordinare gli stati in modalità Sandbox |
| `paymentServicesStoresProduction` | Archivi in modalità Produzione |
| `paymentServicesStoresSandbox` | Memorizza in modalità Sandbox |

Tutti i dati necessari per i report vengono inviati automaticamente a [!DNL Payment Services] se cron è configurato e installato. È inoltre possibile attivare manualmente il processo di invio dei dati cron a [!DNL Payment Services].

```bash
bin/magento cron:run --group payment_services_data_export
```

Per ulteriori informazioni sulla reindicizzazione e sugli indicizzatori, vedere l&#39;argomento [Gestione degli indicizzatori](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) nella documentazione per gli sviluppatori.

## Configurare l’ambito tramite CLI

[!DNL Payment Services] consente ai commercianti di utilizzare [più account PayPal](configure-admin.md#use-multiple-paypal-accounts). Ora è possibile modificare gli ambiti di questi account tramite CLI.

Per impostare l&#39;ambito al livello `website`, eseguire:

```bash
bin/magento config:set payment/payment_services/mba_scoping_level website
```

Per impostare l&#39;ambito al livello `store`, utilizzare:

```bash
bin/magento config:set payment/payment_services/mba_scoping_level store
```

>[!TIP]
>
> Se si desidera modificare l&#39;ambito a livello di archivio, contattare il rappresentante commerciale [!DNL Payment Services].

Dopo aver modificato l’ambito, svuota la cache per visualizzare le modifiche:

```bash
bin/magento cache:clean:payment_services_merchant_scopes
```

## Configurare l’elaborazione L2/L3

[!DNL Payment Services] può elaborare dati di livello 2 e 3 da transazioni di pagamento con carta per fornire informazioni aggiuntive agli esercenti.

>[!WARNING]
>
> L&#39;integrazione con l&#39;elaborazione di livello 2 e livello 3 con PayPal è disponibile solo per gli esercenti statunitensi. Per ulteriori informazioni, consulta [elaborazione dei pagamenti](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} nella documentazione per gli sviluppatori di PayPal.

Se desideri utilizzare i dati di elaborazione L2/L3 per [!DNL Payment Services] o se hai domande, contatta il tuo account manager [!DNL Payment Services].

Per informazioni sull&#39;elaborazione L2 e L3 utilizzata in [!DNL Payment Services], vedere [Elaborazione livello 2 e livello 3](levels-card-payment-transactions.md).
