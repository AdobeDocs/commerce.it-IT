---
title: Prestazioni
description: L'area di lavoro Prestazioni  [!DNL Live Search]  fornisce informazioni approfondite sui termini di ricerca utilizzati dagli acquirenti.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Prestazioni

L&#39;area di lavoro *Performance* fornisce informazioni approfondite sui termini di ricerca utilizzati dagli acquirenti. Le informazioni possono essere utilizzate per identificare le tendenze, aumentare il click-through e migliorare il tasso di conversione. L’area di lavoro Prestazioni fornisce un’istantanea delle metriche di ricerca per un intervallo di date specifico e include i seguenti rapporti:

* Ricerche univoche
* Nessun risultato
* Risultati comuni

![Prestazioni](assets/performance-unique-searches.png)

Per ulteriori informazioni sulla sincronizzazione dei dati, è inoltre possibile fare riferimento a [Dashboard di gestione dati](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html?lang=it).

>[!NOTE]
>
>L’area di lavoro delle prestazioni viene aggiornata ogni 12 ore.

## Visualizzare un rapporto

1. Per immettere l&#39;**intervallo di date**, fare clic sul calendario (![Calendario](assets/btn-calendar.png)) ed eseguire una delle operazioni seguenti:

   * Per specificare una singola data, fare doppio clic sulla data nel calendario.
   * Per specificare un intervallo di date, fare clic sulla prima e sull&#39;ultima data del calendario.

>[!NOTE]
>
>L’intervallo di date non può superare un anno.

## Descrizioni dei campi

| Dati snapshot | Descrizione |
|--- |--- |
| Ricerche univoche | Numero totale di ricerche univoche per l’intervallo di date specificato. Le ricerche multiple dello stesso acquirente, anche se per la stessa query, sono considerate univoche se inviate a più di un&#39;ora di distanza. |
| Percentuale di click-through | La percentuale di ricerche che si concludono con il cliente che fa clic su un prodotto. Ad esempio, il tasso di click-through è del 50% se l’acquirente cerca &quot;pantaloni&quot; e &quot;camicia&quot; e poi fa clic su un risultato nella ricerca &quot;camicia&quot;. |
| Tasso di conversione | La percentuale di prodotti acquistati dal cliente rispetto al numero di prodotti su cui il cliente fa clic per l’intervallo di date specificato. Ad esempio, il tasso di conversione dell’interazione è del 100% se l’acquirente visualizza sei prodotti nella finestra a comparsa, fa clic su uno e effettua un acquisto. <br /><br />Il tasso di conversione non è influenzato dal numero di visualizzazioni di un determinato prodotto. Ad esempio, il tasso di conversione rimane lo stesso se l’acquirente utilizza la ricerca, ma non fa clic su alcun prodotto. |
| Percentuale risultati zero | Percentuale di ricerche univoche che non restituisce alcun risultato per l’intervallo di date specificato. Ad esempio, il tasso di risultati zero è 66,67% se il cliente cerca &quot;fjjajfjfjf&quot; due volte (senza risultati) e &quot;pantaloni&quot; una volta (con risultati). |
| Media posizione clic | Posizione relativa del tasso medio di click-through basato su ricerche univoche per l’intervallo di date specificato. |

| Rapporti | Descrizione |
|--- |--- |
| Ricerche univoche | Elenca le query di ricerca univoche utilizzate durante l’intervallo di date specificato. I dati del report vengono calcolati nello stesso modo dei dati univoci dello snapshot di ricerca. Se un acquirente digita la stessa query di ricerca due volte, ma a più di un’ora di distanza, la ricerca viene considerata come due ricerche univoche. Limite rapporto: primi 500 termini |
| Nessun risultato | Elenca le query di ricerca che non restituiscono risultati e il numero di volte in cui vengono utilizzate durante l’intervallo di date specificato. Limite rapporto: primi 500 termini |
| Risultati comuni | Elenca i nomi dei prodotti che hanno ricevuto il maggior numero di visualizzazioni durante l’intervallo di date specificato. I risultati più comuni vengono calcolati solo in base alle impression e non sono influenzati dal numero di clic o ricavi generati. Limite rapporto: primi 500 termini |
