---
title: Impostazioni
description: Configura le impostazioni per  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: 6ac223de-8e03-4842-8b67-92ce321d323d
TQID: https://experienceleague.adobe.com/9-BMXoWad0bbvsnwgHQrs19ZC9ngGrVE9J7PszcX4Zc
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: 867
ht-degree: 0%

---

# Impostazioni

Utilizza l&#39;area di lavoro *Impostazioni* per configurare la ricerca e l&#39;individuazione dei prodotti per la vetrina. Sono disponibili le seguenti schede:

- **Facet di prezzo** — Configura i gruppi di intervalli di prezzi e gli intervalli utilizzati come filtri di ricerca.
- **Lingua**: impostare la lingua del catalogo utilizzata per l&#39;indicizzazione e la ricerca.
- **Ricerca avanzata**: abilita la ricerca semantica e la ricerca fuzzy e regola le soglie di incremento semantico e similarità.

>[!BEGINTABS]

>[!TAB Facet di prezzo]

## Facet di prezzo {#price-facets}

È possibile specificare il numero di gruppi di intervalli di prezzi e il modo in cui i valori di prezzo vengono distribuiti tra di essi. Ogni fascia di prezzo si sovrappone al gruppo precedente di uno. Ad esempio, quando si utilizzano cinque gruppi con un intervallo di 20, si ottengono intervalli di prezzi come 0-20, 20-40, 40-60, 60-80 e >80. Se il catalogo non contiene un numero di prodotti sufficiente per riempire tutti gli intervalli definiti, la visualizzazione dei gruppi disponibili viene regolata di conseguenza. Ad esempio: 0-20, 60-80, >80.

**Per configurare i facet di prezzo:**

1. Nell&#39;area di lavoro **Impostazioni**, selezionare **[!UICONTROL Facets]**.
1. Nella sezione **Facet prezzo** eseguire le operazioni seguenti:
   - Immettere **[!UICONTROL Number of selections]** o i gruppi di prezzi da rendere disponibili. È possibile definire fino a 100 raggruppamenti di prezzi.
   - Immettere **[!UICONTROL Interval value]** o l&#39;intervallo di prezzi per ogni gruppo. Il valore massimo è 40.000.000.
1. Fare clic su **[!UICONTROL Save]**.

   La disponibilità delle impostazioni aggiornate nella vetrina richiede circa 15 minuti.

### Descrizioni dei campi

| Campo | Descrizione |
| --- | --- |
| Numero di selezioni | Specifica il numero di raggruppamenti di intervalli di prezzi che possono essere utilizzati come filtri di ricerca nella vetrina. Valore predefinito: 8, valore massimo: 100 |
| Valore intervallo | Specifica l&#39;intervallo di prezzo per ogni gruppo. Ad esempio, cinque selezioni con un valore di intervallo di 20 raggruppamenti di rendimento di 0-20, 20-40, 40-60, 60-80 e >80. Valore predefinito: 5, valore massimo: 40.000.000 |

>[!TAB Lingua]

## Lingua {#language}

L&#39;impostazione della lingua indica a [!DNL Adobe Commerce Optimizer] quale lingua aspettarsi durante la lettura del catalogo e la scrittura dell&#39;indice.

Le lingue hanno diversi insiemi di regole per la grammatica: come le parole vengono separate, tempi dei verbi e forme delle parole, ad esempio.
L’impostazione Lingua assicura che al meccanismo di indicizzazione venga applicato l’insieme corretto di regole.

Impostare l&#39;impostazione Lingua sulla lingua principale del catalogo. Quando modifichi la lingua dell’indice, la visualizzazione della modifica nella vetrina può richiedere da 5 a 60 minuti, a seconda delle dimensioni e della complessità del catalogo.

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

Utilizzare la scheda **[!UICONTROL Advanced search]** per gestire la ricerca in un&#39;unica posizione. [!DNL Adobe Commerce Optimizer] offre un&#39;esperienza di ricerca unificata nella vetrina; non è possibile configurare separatamente la ricerca per parole chiave e la ricerca semantica per gli acquirenti. **[!UICONTROL Enable semantic search]** è **abilitato per impostazione predefinita** per i cataloghi inglesi idonei. La ricerca semantica funziona insieme alla configurazione esistente; [regole di merchandising](./merchandising/rules/overview.md), [sinonimi](./merchandising/synonyms/overview.md), [facet](./merchandising/facets/overview.md), aumenti e filtri continuano ad essere applicati. Il sistema utilizza automaticamente gli attributi predefiniti del catalogo: non è possibile selezionare o assegnare priorità agli attributi nell&#39;amministratore. Non sono richieste modifiche a vetrina o sviluppatori.

![Impostazioni di ricerca avanzate](./assets/advanced-search.png)

**Per gestire la ricerca semantica:**

1. Nell&#39;area di lavoro **Impostazioni** selezionare la scheda **[!UICONTROL Advanced search]**.
1. In **[!UICONTROL Enable semantic search]**, confermare che la ricerca semantica sia abilitata o disabilitarla se non si desidera una corrispondenza semantica.
1. Fare clic su **[!UICONTROL Save]** se si modificano i controlli di attivazione/disattivazione.

   I risultati della ricerca vengono aggiornati al termine dell’indicizzazione. Per un catalogo di medie dimensioni, l’indicizzazione può richiedere fino a mezz’ora. Per cataloghi di grandi dimensioni con milioni di prodotti, può richiedere alcune ore.

### Sintonizzazione opzionale

Dopo aver abilitato la ricerca semantica, nella stessa scheda puoi regolare quanto segue:

- **[!UICONTROL Semantic boost]** — Applica un incremento per assegnare la priorità ai risultati semanticamente rilevanti nella classificazione. Aumentare il valore quando le corrispondenze semantiche dovrebbero pesare di più nel set di risultati; abbassarlo quando i risultati si sentono troppo ampi.
- **[!UICONTROL Similarity threshold]** — Imposta il punteggio di somiglianza minimo (come percentuale) per una corrispondenza semantica. I valori più bassi restituiscono più risultati (richiamo più elevato), ma possono includere corrispondenze più deboli. I valori più alti restituiscono un numero minore di corrispondenze più strette (maggiore precisione).

  >[!NOTE]
  >
  > La ricerca semantica è supportata solo per **cataloghi inglesi**. Se si seleziona un&#39;altra lingua nella scheda **[Lingua](#language)**, **[!UICONTROL Enable semantic search]** verrà disabilitato.

- **[!UICONTROL Fuzzy search]** — Attiva **2} per trovare corrispondenze vicine per le query di ricerca, in modo da correggere errori di battitura e variazioni minori.**
- **[!UICONTROL Fuzzy search similarity threshold]** — Imposta la somiglianza minima (come percentuale) necessaria per la visualizzazione delle corrispondenze fuzzy. Le soglie inferiori restituiscono corrispondenze più approssimative; aumenta la soglia se i risultati sfocati si sentono troppo ampi.

Per i vantaggi, le indicazioni sulla convalida, le best practice, la risoluzione dei problemi e le limitazioni, vedere [Ricerca semantica](setup/semantic-search.md).

### Descrizioni dei campi

| Controllo | Descrizione |
| --- | --- |
| Abilita ricerca semantica | Quando è abilitata, la ricerca utilizza significato e contesto insieme alla corrispondenza delle parole chiave. Gli attributi di catalogo predefiniti vengono utilizzati automaticamente; l’amministratore non richiede alcuna impostazione di attributi. Abilitato per impostazione predefinita per [!DNL Adobe Commerce Optimizer] clienti. |
| Incremento semantico | Incremento applicato per assegnare la priorità ai risultati semanticamente rilevanti nella classificazione. |
| Soglia di somiglianza | Punteggio di somiglianza minimo (percentuale) per una corrispondenza semantica. I valori più bassi favoriscono il richiamo; i valori più alti favoriscono la precisione. |
| Ricerca fuzzy | Quando **su**, la ricerca trova corrispondenze vicine per le query (ad esempio, varianti minori). |
| Soglia di somiglianza ricerca fuzzy | Le corrispondenze fuzzy di somiglianza minima (percentuale) devono soddisfare per apparire nei risultati. |

>[!ENDTABS]
