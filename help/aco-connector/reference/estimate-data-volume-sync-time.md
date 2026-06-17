---
title: Stimare il volume dei dati e il tempo di sincronizzazione
description: Scopri come stimare il volume dei dati e il tempo di sincronizzazione per  [!DNL Adobe Commerce Optimizer Connector] feed per pianificare le sincronizzazioni dei cataloghi ed evitare interruzioni.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 0%

---


# Stimare il volume dei dati e il tempo di sincronizzazione

Adobe consiglia di stimare il volume dei dati e il tempo di sincronizzazione prima di avviare qualsiasi sincronizzazione dei feed per garantire una pianificazione fluida ed evitare interruzioni nelle operazioni del sito. Ciò è particolarmente importante quando si pianificano sincronizzazioni iniziali o aggiornamenti del catalogo su larga scala, ad esempio modifiche di prezzo di massa.

Per impostazione predefinita, il connettore elabora i feed in modalità a thread singolo. Non esiste alcuna parallelizzazione del processo di invio dei feed. L’API di acquisizione accetta fino a 2 richieste al secondo. Tuttavia, l&#39;allocazione di base per il tasso di acquisizione [!DNL Adobe Commerce Optimizer] limita la velocità effettiva a:

- Fino a 1.000 prodotti al minuto (un prodotto è una SKU con attributi in una visualizzazione store specifica). Vedi [Limiti e limiti](../../optimizer/boundaries-limits.md) per i dettagli di allocazione di base.
- Fino a 50.000 prezzi al minuto

## Fattori che influiscono sul tempo di sincronizzazione

Le stime che seguono presuppongono le seguenti condizioni:

- Conteggio thread: 1 (impostazione predefinita)
- Tasso di accettazione feed: 2 richieste al secondo (0,5 secondi per richiesta)
- Tutti i prodotti vengono assegnati a tutti i siti Web esistenti

La velocità di trasmissione effettiva varia a seconda delle dimensioni del payload della richiesta e del carico corrente sul server applicazioni Commerce.

## Calcola il tempo di sincronizzazione per feed

Utilizza la tabella seguente per stimare il numero di record, richieste e tempo di sincronizzazione per ciascun feed del connettore. I valori delle dimensioni del batch riflettono i limiti definiti nel riferimento a [feed supportati](connector-reference.md#supported-feeds).

>[!NOTE]
>
>Il tempo di sincronizzazione dei prodotti è basato sul limite di allocazione di base di 1.000 prodotti al minuto. Per gli altri feed, i calcoli si basano su una velocità di trasmissione di 2 richieste al secondo. La velocità effettiva dipende dalle dimensioni del payload e dal carico del server.
>
>La stima dei prezzi presuppone che tutti i gruppi di clienti abbiano prezzi univoci.

| Feed | Esempio di dati | Formula | Richieste previste | Tempo di sincronizzazione previsto |
| ---- | ------------ | ------- | ------------------ | ------------------- |
| Prodotti | Prodotti (P): 10.000, Viste store (SV): 4 | P × SV = 40.000 record | 40.000 ÷ dimensione batch (100) = 400 | 40.000 ÷ 1.000 record/min = **40 min** |
| Categorie | Categorie (C): 500, Viste store (SV): 4 | C × SV = 2.000 record | 2.000 ÷ dimensione batch (100) = 20 | (20 × 0,5 s) ÷ 60 = **~10 s** |
| Attributi del prodotto | Attributi (A): 200, Viste archivio (SV): 4 | A × SV = 800 record | Dimensione batch 800 ÷ (100) = 8 | (8 × 0,5 s) ÷ 60 = **~4 s** |
| Prezzi | Prodotti (P): 10.000, siti Web (WS): 2, gruppi di clienti (CG): 6 | P × WS × CG = 120.000 record | 120.000 ÷ dimensione batch (500) = 240 | (240 × 0,5 s) ÷ 60 = **2 min** |
| Listino prezzi | Siti Web (WS): 2, Gruppi di clienti (CG): 6 | WS × CG = 12 record | 12 ÷ dimensione batch (500) = 1 | (1 × 0,5 s) ÷ 60 = **&lt; 1 s** |

>[!MORELIKETHIS]
>
> - [Moduli connettore ed endpoint di feed](connector-reference.md) - Revisione dei limiti batch e dei feed supportati
> - [Gestisci sincronizzazione](../data-sync-manage.md) - Controlla lo stato di sincronizzazione e attiva le risincronizzazioni manuali
> - [Pipeline di sincronizzazione del connettore](../connector-sync-pipeline.md) - Comprendere come funzionano le pianificazioni cron e la sincronizzazione automatica
