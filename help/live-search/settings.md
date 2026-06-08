---
title: Impostazioni
description: Configurare la ricerca semantica, gli intervalli di facet di prezzo e il linguaggio di indicizzazione predefinito per il servizio  [!DNL Live Search] .
exl-id: 6387a365-7e23-4023-95ac-27908164d81c
TQID: https://experienceleague.adobe.com/Dn4x8Boo-1F5RQgMXVx6Dpt7iYWFIlqOlO5QwhJrjVU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: 650
ht-degree: 0%

---

# Impostazioni

Utilizza l&#39;area di lavoro **Impostazioni** per configurare la ricerca semantica, gli intervalli e gli intervalli dei facet di prezzo e la lingua predefinita per l&#39;indice.

![Impostazioni](assets/settings.png)

## Ricerca semantica {#semantic-search}

La ricerca semantica utilizza l’intelligenza artificiale per far corrispondere i prodotti in base al significato e al contesto, non solo alle parole chiave esatte. Quando **[!UICONTROL Semantic search]** è abilitato, gli acquirenti che utilizzano un linguaggio naturale o un testo che non corrisponde al testo del catalogo possono comunque trovare prodotti rilevanti. [!DNL Live Search] offre la corrispondenza semantica e parola chiave in un&#39;unica esperienza di ricerca unificata nella vetrina. La ricerca semantica funziona insieme alla configurazione esistente. [regole di ricerca](rules.md), [sinonimi](synonyms.md), [facet](facets.md), aumenti e [merchandising categoria](category-merch.md) continuano ad essere applicati.

**Per abilitare la ricerca semantica (solo PaaS):**

1. In Amministrazione, vai a **Marketing** > *SEO &amp; Search* > **[!DNL Live Search]**.
1. Nell&#39;area di lavoro **Impostazioni**, abilita **[!UICONTROL Semantic search]**.

   Se abilitata, la ricerca associa i prodotti in base al significato e al contesto, dando luogo a risultati più rilevanti, a meno ricerche con risultati pari a zero e a una conversione migliore.

1. Fare clic su **[!UICONTROL Save]**.

   I risultati della ricerca vengono aggiornati al termine dell’indicizzazione. Per un catalogo di medie dimensioni, l’indicizzazione può richiedere fino a mezz’ora. Per cataloghi di grandi dimensioni con milioni di prodotti, può richiedere alcune ore.

>[!NOTE]
>
> La ricerca semantica è disponibile solo per **cataloghi inglesi**. Se si imposta **Lingua** su un catalogo non inglese (vedere [Lingua](#language)), **[!UICONTROL Semantic search]** viene disabilitato automaticamente.

Per i vantaggi, le indicazioni sulla convalida, le best practice, la risoluzione dei problemi e le limitazioni, vedere [Ricerca semantica](semantic-search.md).

### Descrizioni dei campi

| Campo | Descrizione |
| --- | --- |
| Ricerca semantica | Quando è abilitato, [!DNL Live Search] utilizza il significato e il contesto insieme alla corrispondenza delle parole chiave. Gli attributi di catalogo predefiniti vengono utilizzati automaticamente; l’amministratore non richiede alcuna impostazione di attributi. Abilitato per impostazione predefinita per [!DNL Adobe Commerce as a Cloud Service]; abilitato manualmente dai venditori PaaS. |

## Fatturazione del prezzo {#price-faceting}

È possibile specificare il numero di gruppi di intervalli di prezzi e il modo in cui i valori di prezzo vengono distribuiti tra di essi. Ogni fascia di prezzo si sovrappone al gruppo precedente di uno. Ad esempio, cinque gruppi con un intervallo di 20 creano le seguenti fasce di prezzo: 0-20, 20-40, 40-60, 60-80 e >80. Se il catalogo non contiene un numero di prodotti sufficiente per riempire tutti gli intervalli definiti, la visualizzazione dei gruppi disponibili viene regolata di conseguenza. Ad esempio: 0-20, 60-80, >80.

**Per configurare il faceting dei prezzi:**

1. In Amministrazione, vai a **Marketing** > *SEO &amp; Search* > **[!DNL Live Search]**.
1. Nell&#39;area di lavoro **Settings** in *Price faceting*, eseguire le operazioni seguenti:
   * Immetti il **numero di selezioni** o i raggruppamenti di prezzi da rendere disponibili. Con [!DNL Live Search] 4.4.0 è possibile definire fino a 100 raggruppamenti di prezzi. Le versioni precedenti consentivano 50 raggruppamenti di prezzi.
   * Immettere il valore **Intervallo** o l&#39;intervallo di prezzi per ogni gruppo. Il valore massimo è 40.000.000.
1. Fare clic su **[!UICONTROL Save]**.

   La disponibilità delle impostazioni aggiornate nella vetrina richiede circa 15 minuti.

### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Numero di selezioni | Specifica il numero di raggruppamenti di intervalli di prezzi che possono essere utilizzati come filtri di ricerca nella vetrina. Valore predefinito: 8, valore massimo: 100 (al [!DNL Live Search] 4.4.0) |
| Valore intervallo | Specifica l&#39;intervallo di prezzo per ogni gruppo. Ad esempio, cinque selezioni con un valore di intervallo pari a 20 creano cinque raggruppamenti di 0-20, 20-40, 40-60, 60-80 e >80. Valore predefinito: 5, valore massimo: 40.000.000 |

## Lingua {#language}

L&#39;impostazione della lingua indica a [!DNL Live Search] quale lingua aspettarsi durante la lettura del catalogo e la scrittura dell&#39;indice.

Le lingue hanno diversi insiemi di regole per la grammatica: come le parole vengono separate, tempi dei verbi e forme delle parole, ad esempio.
L’impostazione Lingua assicura che al meccanismo di indicizzazione venga applicato l’insieme corretto di regole.

Impostare l&#39;impostazione Lingua sulla lingua principale del catalogo. Quando si modifica la lingua dell’indice, possono essere necessari da 5 a 60 minuti per riflettere la modifica nella vetrina, a seconda delle dimensioni e della complessità del catalogo.

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
