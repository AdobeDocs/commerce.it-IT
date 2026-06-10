---
title: Pipeline di sincronizzazione catalogo
description: Scopri come funziona la pipeline di sincronizzazione  [!DNL Adobe Commerce Optimizer Connector] , inclusa la trasformazione dei feed, le pianificazioni cron, il controllo dell'ambito e la gestione degli errori.
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T16:21:52.214Z'
TQID: 'https://experienceleague.adobe.com/EXUQzAd0I6Hnq4twzhaBZZnv0jLjeGBuTx-QgQz-5MA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 625
ht-degree: 1%

---

# Pipeline di sincronizzazione del connettore

Basato su [[!DNL SaaS Data Export]](https://experienceleague.adobe.com/it/docs/commerce/saas-data-export/overview), **[!DNL Adobe Commerce Optimizer Connector]** associa i dati raccolti dagli indicizzatori [!DNL SaaS Data Export] al formato richiesto da [!DNL Adobe Commerce Optimizer] [!DNL Catalog Data Ingestion API] e gestisce l&#39;autenticazione, l&#39;invio in batch e il controllo di sincronizzazione basato sull&#39;ambito. Le sezioni seguenti descrivono come funziona tale sincronizzazione.

Contesto correlato:

- Scopri il valore aziendale, le funzionalità chiave e l&#39;architettura dell&#39;integrazione nell&#39;argomento [[!DNL Commerce Optimizer Connector] panoramica](overview.md).

- Per i nomi dei pacchetti modulo, gli endpoint API di feed e i percorsi delle chiavi di configurazione, vedi [Riferimento connettore](reference/connector-reference.md)

## Funzionamento della sincronizzazione

Il diagramma seguente mostra la sincronizzazione dei dati da [!DNL Adobe Commerce] a [!DNL Commerce Optimizer] tramite [!DNL Adobe I/O Gateway].

![Diagramma di sincronizzazione di alto livello del connettore Commerce Optimizer](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

Quando i dati del catalogo cambiano in [!DNL Adobe Commerce], la sincronizzazione si sposta attraverso queste fasi.

1. **Rilevamento modifiche entità** — (ogni 1 minuto) Un processo cron (`indexer_reindex_all_invalid`) rileva [!DNL Adobe Commerce] modifiche entità e attiva [!DNL SaaS Data Export], che assembla gli elementi feed e ne tiene traccia dello stato.
1. **Trasformazione**: [!DNL Commerce Optimizer Connector] seleziona i feed assemblati, mappa le entità e gli ambiti [!DNL Adobe Commerce] ai formati richiesti dall&#39;API [!DNL Commerce Optimizer] e prepara il payload per la trasmissione.
1. **Trasmissione**: i dati trasformati vengono inviati tramite HTTP POST (`/v1/catalog/<feed name>`) tramite [!DNL Adobe I/O Gateway] a [!DNL Commerce Optimizer], che convalida e mantiene i feed in ingresso.
1. **Nuovo tentativo non riuscito** (ogni 5 minuti). Un processo cron separato (`*_resend_failed_items`) rileva eventuali elementi di feed non riusciti e li invia nuovamente tramite la stessa pipeline.

### Processi cron pianificati

Due gruppi di cron automatizzano la pipeline secondo una pianificazione fissa.

| Gruppo Cron | Finalità | Pianificazione |
| ---------- | ------- | -------- |
| `indexer_reindex_all_invalid` | Ascolta aggiornamenti di entità, assembla elementi feed, persiste stato feed | Ogni 1 minuto |
| `*_resend_failed_items` | Controlla gli elementi di feed non riusciti e li invia nuovamente a [!DNL Commerce Optimizer] | Ogni 5 minuti |

L&#39;estensione **[!DNL SaaS Data Export]** gestisce la raccolta di feed e il tracciamento dello stato. Il livello del connettore mappa entità e ambiti nel formato richiesto dall&#39;API [!DNL Commerce Optimizer] e li invia tramite `POST /v1/catalog/<feed name>`.

#### Requisiti

- [Commerce cron deve essere in esecuzione](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues){target="_blank"}.
- Gli indicizzatori dei feed devono utilizzare la modalità **[!UICONTROL Update by Schedule]**. Vedere [Verifica configurazione applicazione Commerce](../data-export/data-synchronization.md#verify-commerce-application-configuration){target="_blank"}.

## Controllo sincronizzazione basato su ambito

Il modulo `CommerceOptimizerScopeMapper` legge le impostazioni di esportazione per sito Web e per visualizzazione store e le applica durante la raccolta e l&#39;invio dei feed.

- **Ambiti abilitati** esportano dati secondo la normale pianificazione delta.
- **Gli ambiti disattivati** sono esclusi dalla pipeline.
Le entità sincronizzate in precedenza vengono rimosse da [!DNL Commerce Optimizer] alla successiva esecuzione cron.

Se i problemi di sincronizzazione interessano una sola origine catalogo o un listino prezzi dedicato, vedere [Dati non sincronizzati](troubleshooting.md#data-not-syncing).

Per informazioni dettagliate sulla personalizzazione dell&#39;ambito di sincronizzazione, vedere [Personalizzare la configurazione di esportazione degli ambiti di Commerce](get-started.md#customize-the-commerce-scopes-export-configuration).

## Tempistica e monitoraggio

| Scenario | Tempistica tipica |
| -------- | -------------- |
| Aggiornamenti catalogo di routine | 1-2 cicli di sincronizzazione delta (~1-2 minuti per l&#39;indicizzazione, più invio) |
| Errori transitori | Riprovato ogni 5 minuti |
| Sincronizzazione completa o cataloghi di grandi dimensioni | Da minuti a ore |

Monitorare lo stato per feed dalla pagina [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) nell&#39;amministrazione di Commerce. Vedere [Verificare che la sincronizzazione dei dati funzioni](./get-started.md#verify-that-the-data-sync-is-working).

## Invio di feed e gestione degli errori

Il processo `FeedSubmitter` gestisce [!DNL Catalog Data Ingestion API] chiamate.

1. Separa gli elementi di aggiornamento dagli elementi di eliminazione (endpoint API diversi).
1. Le chiamate aggiornano ed eliminano gli endpoint in modo indipendente.
1. Unisce i risultati dello stato per elemento in un’unica risposta.

### Unione del codice di stato HTTP

Quando le chiamate di aggiornamento ed eliminazione restituiscono codici di stato diversi, `FeedSubmitter` combina i risultati come segue.

| Risultato aggiornamenti | Elimina il risultato | Risultato finale |
| --------------- | --------------- | ------------- |
| 200 | 200 o nessuno | 200 operazione riuscita |
| 200 | 400 | 200 con errori di eliminazione |
| 400 | 400 | 400 errori uniti |
| altro | altro | RIUTILIZZABILE |

| Tipo di errore | Comportamento |
| ---------- | -------- |
| **400** | Gli elementi elencati nel campo `errors` della risposta vengono visualizzati nell&#39;amministratore e richiedono attenzione. Gli altri elementi del batch vengono ritentati. |
| **5xx** | Tentativi eseguiti dai processi cron `*_feed_resend_failed_items` specifici del feed nel gruppo `resync_failed_feeds_data_exporter`. |

>[!MORELIKETHIS]
>
> - [Panoramica del connettore](overview.md): apprendere il contesto aziendale e la mappatura dell&#39;ambito
> - [Riferimento connettore](reference/connector-reference.md) - Rivedi moduli, endpoint API e chiavi di configurazione
> - [Personalizzare la configurazione di esportazione degli ambiti di Commerce](./get-started.md#customize-the-commerce-scopes-export-configuration): configurare i feed per livello di ambito, abilitare e disabilitare il comportamento e i passaggi dell&#39;amministratore
> - [Risoluzione dei problemi](troubleshooting.md) — Diagnostica errori di sincronizzazione
