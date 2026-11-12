---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%
---
Utilizza l&#39;area di lavoro *Impostazioni* per configurare la ricerca e l&#39;individuazione dei prodotti per la vetrina. Sono disponibili le seguenti schede:

- **Facet**—Configura i gruppi di intervalli di prezzo e gli intervalli utilizzati come filtri di ricerca.
- **Lingua** - Imposta la lingua del catalogo utilizzata per l&#39;indicizzazione e la ricerca.
- **Ricerca avanzata**: abilita la ricerca semantica e la ricerca fuzzy e regola le soglie di incremento semantico e similarità.

## Accedere all’area di lavoro Impostazioni

La modalità di apertura dell&#39;area di lavoro *Impostazioni* dipende dal prodotto utilizzato:

- **Amministratore Adobe Commerce** (Adobe Commerce as a Cloud Service)—Seleziona *Merchandising* > **Impostazioni merchandising**.
- **Adobe Commerce Optimizer Studio**—Seleziona *Merchandising* > **Impostazioni**.

>[!BEGINTABS]

>[!TAB Facet di prezzo]

## Facet di prezzo {#price-facets}

È possibile specificare il numero di gruppi di intervalli di prezzi e il modo in cui i valori di prezzo vengono distribuiti tra di essi. Ogni fascia di prezzo si sovrappone al gruppo precedente di uno. Ad esempio, cinque gruppi con un intervallo di 20 creano intervalli di prezzi: 0-20, 20-40, 40-60, 60-80 e >80. Se il catalogo non contiene un numero di prodotti sufficiente per riempire tutti gli intervalli definiti, la visualizzazione dei gruppi disponibili viene regolata di conseguenza. Ad esempio: 0-20, 60-80, >80.

**Per configurare i facet di prezzo:**

1. Dall&#39;area di lavoro **Impostazioni**, selezionare **[!UICONTROL Facets]**.
1. Nella sezione **Facet prezzo** eseguire le operazioni seguenti:
   - Immettere **[!UICONTROL Number of selections]** o i gruppi di prezzi da rendere disponibili. È possibile definire fino a 100 raggruppamenti di prezzi.
   - Immettere **[!UICONTROL Interval value]** o l&#39;intervallo di prezzi per ogni gruppo. Il valore massimo è 40.000.000.
1. Fare clic su **[!UICONTROL Save]**.

   La disponibilità delle impostazioni aggiornate nella vetrina richiede circa 15 minuti.

### Descrizioni dei campi facet di prezzo

| Campo | Descrizione |
| --- | --- |
| Numero di selezioni | Specifica il numero di raggruppamenti di intervalli di prezzi che possono essere utilizzati come filtri di ricerca nella vetrina. Valore predefinito: 8, valore massimo: 100 |
| Valore intervallo | Specifica l&#39;intervallo di prezzo per ogni gruppo. Ad esempio, cinque selezioni con un valore di intervallo di 20 raggruppamenti di rendimento di 0-20, 20-40, 40-60, 60-80 e >80. Valore predefinito: 5, valore massimo: 40.000.000 |

>[!TAB Lingua]

## Lingua {#language}

L’impostazione Lingua indica al sistema la lingua da prevedere durante la lettura del catalogo e la scrittura dell’indice.

Le lingue hanno diversi insiemi di regole per la grammatica: come le parole vengono separate, tempi dei verbi e forme delle parole, ad esempio.
L’impostazione Lingua assicura che al meccanismo di indicizzazione venga applicato l’insieme corretto di regole.

Impostare l&#39;impostazione Lingua sulla lingua principale del catalogo. La modifica della lingua dell&#39;indice richiede da 5 a 60 minuti per essere visualizzata nella vetrina, a seconda delle dimensioni e della complessità del catalogo.

| Lingua | Codice |
|----|----|
| Arabo | ar |
| Armeno | hy |
| Basco | eu |
| Bengalese | bn |
| Brasiliano | pt-br |
| Bulgaro | bg |
| Catalano | ca |
| Cinese (semplificato) | zh-cn |
| Cinese (tradizionale) | zh-tw |
| Ceco | cs |
| Danese | da |
| Olandese | nl |
| Inglese | it |
| Estone | et |
| Finlandese | fi |
| Francese | fr |
| Galiziano | gl |
| Tedesco | de |
| Greco | el |
| Hindi | ciao |
| Ungherese | hu |
| Indonesiano | id |
| Irlandese | ga |
| Italiano | it |
| Giapponese (Katakana) | ja |
| Coreano | ko |
| Lettone | lv |
| Lituano | lt |
| Norvegese | no |
| Persiano | fa |
| Portoghese | pt |
| Rumeno | ro |
| Russo | ru |
| Sorani | ku |
| Spagnolo | es |
| Svedese | sv |
| Turco | tr |
| Thailandese | th |

>[!TAB Ricerca avanzata]

## Ricerca avanzata {#advanced-search}

Utilizzare la scheda **[!UICONTROL Advanced search]** per gestire la ricerca in un&#39;unica posizione. Il sistema offre un’esperienza di ricerca unificata nella vetrina; non puoi configurare separatamente la ricerca per parole chiave e la ricerca semantica per gli acquirenti. **[!UICONTROL Enable semantic search]** è **abilitato per impostazione predefinita** per i cataloghi inglesi idonei. La ricerca semantica funziona insieme alla configurazione esistente; [regole di merchandising](./merchandising/rules/overview.md), [sinonimi](./merchandising/synonyms/overview.md), [facet](./merchandising/facets/overview.md), aumenti e filtri continuano ad essere applicati. Il sistema utilizza automaticamente gli attributi predefiniti del catalogo: non è possibile selezionare o assegnare priorità agli attributi in Impostazioni. Non sono richieste modifiche a vetrina o sviluppatori.

![Impostazioni di ricerca avanzate](/help/assets/ccdm-shared/advanced-search.png)

**Per gestire la ricerca semantica:**

1. Nell&#39;area di lavoro **Impostazioni** selezionare la scheda **[!UICONTROL Advanced search]**.
1. In **[!UICONTROL Enable semantic search]**, confermare che la ricerca semantica sia abilitata o disabilitarla se non si desidera una corrispondenza semantica.
1. Fare clic su **[!UICONTROL Save]** se si modificano i controlli di attivazione/disattivazione.

   I risultati della ricerca vengono aggiornati al termine dell’indicizzazione. Per un catalogo di medie dimensioni, l’indicizzazione può richiedere fino a 30 minuti. Per cataloghi di grandi dimensioni con milioni di prodotti, può richiedere alcune ore.

### Sintonizzazione opzionale

Dopo aver abilitato la ricerca semantica, nella stessa scheda puoi regolare quanto segue:

- **[!UICONTROL Semantic boost]** - Per assegnare la priorità ai risultati rilevanti dal punto di vista semantico nella classificazione, applica un incremento. Aumentare il valore quando le corrispondenze semantiche dovrebbero pesare di più nel set di risultati; abbassarlo quando i risultati si sentono troppo ampi.
- **[!UICONTROL Similarity threshold]** - Imposta il punteggio di somiglianza minimo (come percentuale) per una corrispondenza semantica. I valori più bassi restituiscono più risultati (richiamo più elevato), ma possono includere corrispondenze più deboli. I valori più alti restituiscono un numero minore di corrispondenze più strette (maggiore precisione).
- **[!UICONTROL Fuzzy search]** - Per trovare corrispondenze vicine per le query di ricerca e correggere errori di battitura e varianti minori, attivare **2}.**
- **[!UICONTROL Fuzzy search similarity threshold]** - Imposta la somiglianza minima (come percentuale) necessaria per la visualizzazione delle corrispondenze fuzzy. Le soglie inferiori restituiscono corrispondenze più approssimative; aumenta la soglia se i risultati sfocati si sentono troppo ampi.

>[!NOTE]
>
> La ricerca semantica è supportata solo per **cataloghi inglesi**. Se si seleziona un&#39;altra lingua nella scheda **[!UICONTROL Language]**, **[!UICONTROL Enable semantic search]** verrà disabilitato.

Per i vantaggi, le indicazioni sulla convalida, le best practice, la risoluzione dei problemi e le limitazioni, vedere [Ricerca semantica](/help/optimizer/setup/semantic-search.md).

### Descrizioni dei campi di ricerca avanzate

| Controllo | Descrizione |
| --- | --- |
| Abilita ricerca semantica | Quando è abilitata, la ricerca utilizza significato e contesto insieme alla corrispondenza delle parole chiave. Gli attributi di catalogo predefiniti vengono utilizzati automaticamente; in Impostazioni non è richiesta alcuna impostazione di attributi. Abilitato per impostazione predefinita. |
| Incremento semantico | Incremento applicato per assegnare la priorità ai risultati semanticamente rilevanti nella classificazione. |
| Soglia di somiglianza | Punteggio di somiglianza minimo (percentuale) per una corrispondenza semantica. I valori più bassi favoriscono il richiamo; i valori più alti favoriscono la precisione. |
| Ricerca fuzzy | Quando **su**, la ricerca trova corrispondenze vicine per le query (ad esempio, varianti minori). |
| Soglia di somiglianza ricerca fuzzy | Le corrispondenze fuzzy di somiglianza minima (percentuale) devono soddisfare per apparire nei risultati. |

>[!ENDTABS]
