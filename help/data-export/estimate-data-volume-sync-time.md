---
title: Stima del volume dei dati e del tempo di trasmissione
description: Scopri come stimare il volume di dati e il tempo di trasmissione necessari affinché lo strumento  [!DNL data export]  sincronizzi i dati dei feed tra Adobe Commerce e i servizi connessi.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 787d05d6-fc2f-4f23-8ea7-ef54330e1f37
TQID: https://experienceleague.adobe.com/nhVfGHgrsvqIjUcWfsVDcriEFwUhRQa9D-4xAU-cAnU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 585
ht-degree: 0%

---

# Stimare il volume dei dati e il tempo di trasmissione per la sincronizzazione dei dati

Adobe consiglia di stimare il volume dei dati e il tempo di sincronizzazione prima di avviare qualsiasi sincronizzazione dei feed di dati per garantire una pianificazione fluida ed evitare interruzioni nelle operazioni del sito. Questa stima è importante quando si pianificano sincronizzazioni iniziali o aggiornamenti di cataloghi su larga scala, ad esempio le variazioni dei prezzi di massa.

>[!NOTE]
>
>Per le distribuzioni di [!DNL Adobe Commerce Optimizer Connector], controlla i feed supportati specifici del connettore e i limiti batch in [Moduli connettore ed endpoint di feed](../aco-connector/reference/connector-reference.md#supported-feeds).

Per impostazione predefinita, lo strumento di esportazione dei dati elabora i dati in modalità a thread singolo con una dimensione batch predefinita. Con la configurazione predefinita, non esiste alcuna parallelizzazione del processo di invio dei feed. Questo componente accetta anche le richieste al secondo (RPS), il che si traduce nel modo seguente:

- Fino a 10.000 prodotti al minuto in cui un prodotto è una SKU con attributi in una visualizzazione dello store specifica
- Fino a 50.000 prezzi al minuto

I seguenti fattori influiscono sul tempo di trasmissione dei dati durante la sincronizzazione.

- Il conteggio dei thread è impostato su 1 (per impostazione predefinita)
- La dimensione del batch è impostata su _100_ per tutti i feed ad eccezione del feed `prices`, dove è impostata su _500_.
- Il tasso di accettazione dei feed è di 2 richieste al secondo.
- Tutti i prodotti vengono assegnati a tutti i siti Web esistenti
- Per gli scenari di calcolo dei prezzi, a tutti i prodotti vengono assegnati prezzi speciali e raggruppati


## Calcolare la trasmissione dei dati per feed

Utilizzare i valori e le formule della tabella seguente per calcolare il volume di dati e il tempo di sincronizzazione per ogni feed di dati.

>[!NOTE]
>
>Questi calcoli si basano su una velocità di trasmissione di 2 richieste al secondo. La velocità si basa sul tempo necessario per la raccolta e l’invio dei dati. La velocità di trasmissione effettiva varia a seconda delle dimensioni del payload della richiesta e del carico corrente sul server applicazioni Commerce.

| Feed | Esempio di dati | Formula per il calcolo dei record | Conteggio richieste previsto | Tempo di risincronizzazione previsto |
| --- | --- | --- | --- | --- |
| Prodotti | Prodotti (P): 10000, Viste store (SV): 4 | P * SV = 40000 | 40000/Dimensione batch (100) = 400 richieste | (400 richieste * 0,5 secondi per richiesta) / 60 = 3,3 minuti |
| Categorie | Categorie (C): 500, Viste store (SV): 4 | C * SV = 2000 | 2000 / Dimensione batch (100) = 20 richieste | (20 richieste * 0,5 secondi per richiesta) / 60 = 0,1 minuti (4 secondi) |
| Prezzi | Prodotti (P): 10000, Gruppi di clienti (CG): 6 (ad esempio, prezzo univoco nel catalogo condiviso), Siti Web (WS): 2 | P \* WS * CG = 120000 | 120000/Dimensione batch (500) = 240 richieste | (240 richieste * 0,5 secondi per richiesta) / 60 = 2 minuti |
| Sostituzioni prodotto | Prodotti con autorizzazioni o in catalogo condiviso (P): 10000, Gruppi di clienti interessati (CG): 5, Siti Web assegnati WS: 2 | P \* WS * CG = 100000 | 100000/Dimensione batch (100) = 1000 richieste | (1000 richieste * 0,5 secondi per richiesta) / 60 = 8,3 minuti |
| Varianti prodotto | Varianti (prodotti secondari) assegnate a prodotti configurabili (PV): 100000 | PV = 100000 | 100000/Dimensione batch (100) = 1000 richieste | (1000 richieste * 0,5 secondi per richiesta) / 60 = 8,3 minuti |
| Autorizzazioni categoria | Numero di tutte le autorizzazioni per categoria + 4 record di fallback (CP): 10000 | CP = 10000 | 10000/Dimensione batch (100) = 100 richieste | (100 richieste * 0,5 secondi per richiesta) / 60 = 0,8 minuti (50 secondi) |
| Stato scorte | Prodotti (P): 10000, Scorte prodotti assegnati a (S): 5 (supponendo che ogni prodotto sia assegnato a ogni scorta) | P * S = 50000 | 50000/Dimensione batch (100) = 500 richieste | (500 richieste * 0,5 secondi per richiesta) / 60 = 4,2 minuti |
| Ordini di vendita | Tutti i record ordine (comprese fatture, spedizioni e così via) (SO): 10000 | SO = 10000 | 10000/Dimensione batch (100) = 100 richieste | (100 richieste * 0,5 secondi per richiesta) / 60 = 0,8 minuti (50 secondi) |

>[!MORELIKETHIS]
>
> - [Migliorare le prestazioni di esportazione dei dati](customize-export-processing.md)
> - [Gestisci sincronizzazione](data-sync-manage.md)
> - [Funzionamento della sincronizzazione](sync-overview.md)
