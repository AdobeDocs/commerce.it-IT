---
title: Prestazioni
description: L'area di lavoro Prestazioni di  [!DNL Live Search]  fornisce ad insight i termini di ricerca utilizzati dagli acquirenti.
exl-id: 07a63df8-b981-4913-841a-7e81ec634281
source-git-commit: 5978a400d985e3099962af8bcefdd6f29f687d67
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Prestazioni

L&#39;area di lavoro *Performance* fornisce ad insight i termini di ricerca utilizzati dagli acquirenti. Le informazioni possono essere utilizzate per identificare le tendenze, aumentare il click-through e migliorare il tasso di conversione. L’area di lavoro Prestazioni fornisce un’istantanea delle metriche di ricerca per un intervallo di date specifico e include i seguenti rapporti:

* Ricerche univoche
* Nessun risultato
* Risultati comuni

![Prestazioni](assets/performance-unique-searches.png)

Per ulteriori informazioni sulla sincronizzazione dei dati, è inoltre possibile fare riferimento a [Dashboard di gestione dati](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html).

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

| Dati snapshot | Descrizione | Esempio di calcolo |
|--- |--- |--- |
| Ricerche univoche | Numero totale di ricerche univoche per l’intervallo di date specificato. Le ricerche multiple dello stesso acquirente, anche se per la stessa query, sono considerate univoche se inviate a più di un&#39;ora di distanza. | **Esempio:**<br /> Ricerche:<br />- &quot;pantaloni&quot; alle 10:00<br />- &quot;pantaloni&quot; alle 10:30 AM (entro 1 ora → non univoco)<br />- &quot;pantaloni&quot; alle 12:00 PM (dopo 1 ora → univoco)<br />- &quot;camicia&quot; alle 1:00<br /><br />**Ricerche univoche totali = 3** |
| Tasso di click-through | La percentuale di ricerche che si concludono con il cliente che fa clic su un prodotto. Ad esempio, il tasso di click-through è del 50% se l’acquirente cerca &quot;pantaloni&quot; e &quot;camicia&quot; e poi fa clic su un risultato nella ricerca &quot;camicia&quot;. | **Formula:**<br /> Percentuale di click-through = Ricerche con clic ≥1 ÷ Totale ricerche univoche <br /><br />**Esempio:**<br /> Totale ricerche univoche = 4<br />Ricerche con almeno un clic = 2<br /><br />CTR = 2 ÷ 4 = **50%** |
| Tasso di conversione | La percentuale di prodotti acquistati dal cliente rispetto al numero di prodotti su cui il cliente fa clic per l’intervallo di date specificato. Ad esempio, il tasso di conversione dell’interazione è del 100% se l’acquirente visualizza sei prodotti nella finestra a comparsa, fa clic su uno e effettua un acquisto. <br /><br />Il tasso di conversione non è influenzato dal numero di visualizzazioni di un determinato prodotto. Ad esempio, il tasso di conversione rimane lo stesso se l’acquirente utilizza la ricerca, ma non fa clic su alcun prodotto. | **Formula:**<br /> Tasso di conversione = Prodotti acquistati ÷ Totale prodotti selezionati <br /><br />**Esempio 1:**<br /> Prodotti selezionati = 5<br />Prodotti acquistati = 2<br /><br />CVR = 2 ÷ 5 = **40%**<br /><br />**Esempio 2 (aggregazione di 5 ore):**<br /> Clic per ora: 4, 5, 6, 10, 2<br />Acquisti per ora: 1, 3, 0, 4, 1<br /><br />Clic totali = 4 + 5 + 6 + 10 + 2 = 27<br />Acquisti totali = 1 + 3 + 0 + 4 + 9<br /><br />CVR = 9 ÷ 27 = **33,33%** |
| Percentuale risultati zero | Percentuale di ricerche univoche che non restituisce alcun risultato per l’intervallo di date specificato. Ad esempio, il tasso di risultati zero è 66,67% se il cliente cerca &quot;fjjajfjfjf&quot; due volte (senza risultati) e &quot;pantaloni&quot; una volta (con risultati). | **Formula:**<br /> Percentuale zero risultati = Ricerche univoche con zero risultati ÷ Totale ricerche univoche <br /><br />**Esempio:**<br /> Totale ricerche univoche = 3<br />Ricerche con zero risultati = 2<br /><br />Percentuale zero risultati = 2 ÷ 3 = **66,67%** |
| Media posizione clic | Posizione relativa del tasso medio di click-through basato su ricerche univoche per l’intervallo di date specificato. | **Formula:**<br /> Posizione media clic = Somma delle posizioni di clic ÷ Clic totali <br /><br />**Esempio:**<br /> Clic nelle posizioni: 1, 3, 2<br /><br />Posizione media clic = (1 + 3 + 2) ÷ 3 = **2** |

| Rapporti | Descrizione |
|--- |--- |
| Ricerche univoche | Elenca le query di ricerca univoche utilizzate durante l’intervallo di date specificato. I dati del report vengono calcolati nello stesso modo dei dati univoci dello snapshot di ricerca. Se un acquirente digita la stessa query di ricerca due volte, ma a più di un’ora di distanza, la ricerca viene considerata come due ricerche univoche. <br />**Limite rapporto:** primi 500 termini durante la generazione del file CSV. |
| Nessun risultato | Elenca le query di ricerca che non restituiscono risultati e il numero di volte in cui vengono utilizzate durante l’intervallo di date specificato. <br />**Limite rapporto:** primi 500 termini durante la generazione del file CSV. |
| Risultati comuni | Elenca i nomi dei prodotti che hanno ricevuto il maggior numero di visualizzazioni durante l’intervallo di date specificato. I risultati più comuni vengono calcolati solo in base alle impression e non sono influenzati dal numero di clic o ricavi generati. <br />**Limite rapporto:** primi 500 termini durante la generazione del file CSV. |
