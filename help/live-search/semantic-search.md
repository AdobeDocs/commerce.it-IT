---
title: Ricerca semantica
description: Abilita la ricerca semantica AI per  [!DNL Live Search]  dalle impostazioni. Non è richiesta alcuna modifica alla configurazione degli attributi o alla vetrina.
role: Admin
recommendations: noCatalog
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 0%

---

# Ricerca semantica

La ricerca semantica utilizza l&#39;intelligenza artificiale per capire cosa significano gli acquirenti, non solo le parole esatte che digitano. Query come &quot;abito per un matrimonio in spiaggia&quot; o &quot;scarpe comode per stare in piedi tutto il giorno&quot; possono restituire prodotti rilevanti anche quando il catalogo non utilizza quelle frasi esatte.

[!DNL Live Search] combina la corrispondenza delle parole chiave e la corrispondenza semantica in un&#39;unica esperienza di ricerca. Non è possibile gestire modalità separate per parole chiave e semantiche nella vetrina. [!DNL Live Search] non offre controlli semantici avanzati (ad esempio cursori di incremento o similarità) in Admin. Puoi abilitare o disabilitare la ricerca semantica.

## Abilitazione tramite distribuzione

La ricerca semantica è gestita dall&#39;area di lavoro **Impostazioni** nell&#39;amministratore [!DNL Live Search] (**Marketing** > *SEO e ricerca* > **[!DNL Live Search]**). [!DNL Adobe Commerce as a Cloud Service] utilizza la stessa interfaccia [!DNL Live Search] dei commercianti PaaS.

## Vantaggi

- **Meno ricerche con zero risultati**: gli acquirenti trovano i prodotti quando il testo non corrisponde esattamente al testo del catalogo.
- **Risultati più rilevanti** - Le query naturali e descrittive restituiscono corrispondenze utili in base al significato e al contesto.
- **Meno manutenzione sinonimi** — Varianti comuni delle parole (ad esempio, divano e divano) vengono spesso gestite senza elenchi di sinonimi manuali.
- **Nessuna vetrina o lavoro per sviluppatori** - La ricerca semantica non richiede modifiche al codice tema, al widget o all&#39;API. Gli esercenti PaaS lo abilitano nelle Impostazioni; [!DNL Adobe Commerce as a Cloud Service] clienti lo ricevono per impostazione predefinita.

## Come funziona

Quando la ricerca semantica è abilitata, [!DNL Live Search] utilizza attributi di catalogo predefiniti scelti dal sistema (ad esempio il nome e la descrizione del prodotto) per interpretare il significato della query insieme alla ricerca tradizionale per parole chiave. Non selezionare o assegnare la priorità agli attributi nell’amministratore.

Ad esempio:

- Una ricerca per &quot;divano in pelle&quot; può restituire prodotti etichettati &quot;divano in pelle&quot;.
- &quot;Spring dress&quot; può far emergere gli abiti stagionali anche quando &quot;spring&quot; non è nel nome del prodotto.
- &quot;Scarpe da corsa&quot; può abbinare prodotti descritti come calzature da fuoristrada o da trekking.

## Cosa succede quando si abilita la ricerca semantica

La ricerca semantica funziona insieme alla configurazione [!DNL Live Search] esistente. Non si sostituisce la ricerca per parola chiave né si riconfigura la vetrina.

Quando la ricerca semantica è attiva:

- Le tue [regole di ricerca](rules.md), [sinonimi](synonyms.md), [facet](facets.md), potenziamenti e [impostazioni di merchandising di categoria](category-merch.md) esistenti continuano ad essere applicate.
- La ricerca semantica aggiunge una comprensione basata sull’intelligenza artificiale dell’intento del cliente di migliorare la rilevanza dei risultati insieme alla corrispondenza delle parole chiave.
- Gli attributi predefiniti del catalogo vengono indicizzati automaticamente. Non selezionare attributi né pubblicare una configurazione separata.

## Gestire la ricerca semantica nell’amministratore

Vai all&#39;area di lavoro [Impostazioni](settings.md#semantic-search) per visualizzare o modificare l&#39;interruttore **[!UICONTROL Semantic search]**.

>[!NOTE]
>
> La ricerca semantica è disponibile solo per **cataloghi inglesi**. Se modifichi **Lingua** in un catalogo non inglese nell&#39;area di lavoro **Impostazioni**, **[!UICONTROL Semantic search]** viene disabilitato automaticamente.

### Per gli esercenti PaaS

I commercianti on-premise e Adobe Commerce on-premise devono abilitare manualmente la ricerca semantica:

1. In Amministrazione, vai a **Marketing** > *SEO &amp; Search* > **[!DNL Live Search]**.
1. Nell&#39;area di lavoro **Impostazioni**, abilita **[!UICONTROL Semantic search]**.

   Quando è abilitata, la ricerca associa i prodotti in base al significato e al contesto, in modo da produrre risultati più rilevanti, ridurre il numero di ricerche con risultati pari a zero e migliorare la conversione.

1. Fare clic su **[!UICONTROL Save]**.

   I risultati della ricerca vengono aggiornati al termine dell’indicizzazione. Per un catalogo di medie dimensioni, l’indicizzazione può richiedere fino a mezz’ora. Per cataloghi di grandi dimensioni con milioni di prodotti, può richiedere alcune ore.

### Per i clienti ACS

I clienti [!DNL Adobe Commerce as a Cloud Service] utilizzano la stessa area di lavoro **Impostazioni** nell&#39;amministratore [!DNL Live Search]. La ricerca semantica è **abilitata per impostazione predefinita** per i cataloghi inglesi idonei. Confermare che **[!UICONTROL Semantic search]** è abilitato o disabilitarlo se non si desidera una corrispondenza semantica nella vetrina.

Dopo aver salvato una modifica, non è necessario un passaggio di pubblicazione o una configurazione della vetrina separati.

## Convalida dopo l’abilitazione

Al termine dell’indicizzazione e dopo l’attivazione della ricerca semantica, Adobe consiglia di convalidare le prestazioni della ricerca. Utilizza l&#39;area di lavoro [Prestazioni](performance.md) per esaminare le metriche e testare le query rilevanti per la tua azienda. Ciò vale sia che la ricerca semantica sia stata attivata per impostazione predefinita sia che sia stata attivata manualmente.

1. Controlla i termini più cercati nel rapporto **Ricerche univoche**.
1. Verifica le query a zero risultati cronologiche dal report **Zero results** nella vetrina.
1. Confronta i risultati della ricerca per le stesse query prima e dopo l’abilitazione.
1. Monitora la conversione della ricerca e le metriche di coinvolgimento, tra cui il tasso di click-through, il tasso di conversione e il tasso di zero risultati.

## Best practice

- Utilizza nomi e descrizioni di prodotti chiari e descrittivi (idealmente 50-100 parole) in modo che sia la corrispondenza semantica che quella delle parole chiave abbiano un testo di catalogo forte con cui lavorare.
- Mantieni [sinonimi](synonyms.md) specifici del brand o altamente tecnici, in cui la ricerca semantica potrebbe non includere termini specializzati.

## Risoluzione dei problemi

| Problema | Cosa fare |
| --- | --- |
| Nessuna modifica nella vetrina subito dopo il salvataggio | Attendere il completamento dell&#39;indicizzazione. I cataloghi di grandi dimensioni possono richiedere più tempo. |
| La ricerca semantica non è disponibile o è disabilitata automaticamente | Conferma **Lingua** nell&#39;area di lavoro **Impostazioni** impostata su **Inglese**. |
| I risultati mancano ancora dei termini comuni | Aggiungere [sinonimi](synonyms.md) per i termini del marchio o del settore. La ricerca semantica potrebbe non essere risolta. |

## Limitazioni {#semantic-search-limitations}

- **Lingua del catalogo:** La ricerca semantica è disponibile solo per **cataloghi in lingua inglese**.
- **Controlli di amministrazione:** [!DNL Live Search] fornisce solo un controllo di attivazione/disattivazione. Non è possibile regolare l&#39;incremento semantico, la soglia di similarità o la ricerca fuzzy dall&#39;area di lavoro **Impostazioni**.

## Ulteriori informazioni su questo argomento

- [Impostazioni](settings.md#semantic-search)
- [Sinonimi](synonyms.md)
- [Prestazioni](performance.md)
