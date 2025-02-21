---
title: Aggiungi facet
description: Scopri come aggiungere attributi di prodotto filtrabili come  [!DNL Live Search] facet.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Aggiungi facet

Qualsiasi attributo di prodotto filtrabile può essere utilizzato come facet. Il pannello *Aggiungi facet* elenca i facet correnti e semplifica l&#39;assegnazione di attributi di prodotto aggiuntivi come facet. Durante questo processo in tre fasi, viene scelto un attributo da utilizzare come facet, le proprietà vengono modificate se necessario e le modifiche pubblicate nella vetrina.

![Aggiungi facet](assets/facets-add.png)

## Passaggio 1: aggiungere un facet

1. In Amministrazione, vai a **Marketing** > SEO &amp; Search > **[!DNL Live Search]**.
1. Nella scheda *Faceting*, fare clic su **Aggiungi facet**.
1. Nell&#39;elenco *Aggiungi facet*, ogni attributo disponibile ha un ![pulsante Aggiungi](assets/btn-add.png) separato. Completa una delle seguenti operazioni:

   * Nell&#39;elenco *Attributi faceting*, scegliere l&#39;attributo prodotto che si desidera utilizzare come facet e fare clic su **Aggiungi**.
   * Per trovare un attributo di prodotto specifico, immettere i primi caratteri del nome dell&#39;attributo nella casella *Cerca*. Quindi fare clic su **Aggiungi**.

     Per configurare intervalli e raggruppamenti di price faceting, fare riferimento a [Impostazioni](settings.md). Per ulteriori informazioni, vai a [Tipi di facet](facets-type.md).
Il facet viene aggiunto nella parte inferiore dell&#39;elenco *Facet dinamici* e il pulsante *Pubblica modifiche* diventa disponibile.

1. Se il facet che desideri aggiungere non viene trovato, vai a **Archivi** > Attributi > **Prodotto** e verifica che l&#39;attributo abbia le [proprietà richieste](facets.md) da utilizzare come facet. Se necessario, aggiorna le seguenti proprietà della vetrina dell’attributo:

   * Usa nella ricerca - `Yes`
   * Utilizzo in navigazione a livelli dei risultati di ricerca - `Yes`
   * Usa in navigazione a livelli - `Filterable (with results)`

1. Quando richiesto, aggiorna la cache.

   Il facet diventa disponibile nella vetrina alla successiva sincronizzazione del catalogo con [!DNL Live Search]. Se il facet non è disponibile dopo due ore, vedere [Sincronizzare i dati del catalogo](install.md#synchronize-catalog-data).

## Passaggio 2: modificare le proprietà del facet (facoltativo)

1. Per modificare le proprietà del facet, fare clic su **Altre** (![Altro selettore](assets/btn-more.png)) opzioni nella colonna a destra.
1. Scegliere **Modifica** dal menu. Quindi, regola le seguenti proprietà in base alle esigenze.

   * Etichetta - ([Solo headless](facets-type.md)) Immettere l&#39;etichetta facet che si desidera utilizzare.
   * Tipo di ordinamento: i facet sono ordinati alfabeticamente per tutti i [!DNL Commerce] storefront. Per le implementazioni headless, i facet possono essere ordinati alfabeticamente o per conteggio. Opzioni: Alfabetico, Conteggio (solo headless)
   * Valore massimo: immettere il numero massimo di valori di facet visualizzati nella vetrina. Voci valide: 0 - 100; valore predefinito: 8

1. Al termine, fare clic su **Salva**.

   ![Modifica facet](assets/facet-edit.png)

1. Per fissare il facet all&#39;inizio dell&#39;elenco *Filtri*, fare clic sul puntino grigio (![Selettore pin](assets/btn-pin-gray.png)).
1. Per modificare l&#39;ordine del facet bloccato, fare clic sull&#39;icona **Sposta** (![Sposta selettore](assets/btn-move.png)) e trascinare la riga in una nuova posizione nella sezione *Facet bloccati*.

## Passaggio 3: Pubblicare le modifiche

1. Una volta completato il facet, fare clic su **Pubblica modifiche**.
1. Attendere che il facet venga visualizzato nell&#39;archivio.
Se il facet non è disponibile dopo due ore, vedere [Verifica esportazione](install.md#synchronize-catalog-data) nelle istruzioni di installazione.

## Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Etichetta | ([Solo headless](facets-type.md)) L&#39;[etichetta facet](facets-type.md) visibile nella vetrina può essere modificata per coerenza con il tuo marchio. |
| Tipo di ordinamento | Metodo utilizzato per [ordinare](facets-type.md) facet. Tutti i [!DNL Commerce] storefront ordinano i facet in ordine alfabetico. Anche le implementazioni headless possono essere ordinate per `Count`. Opzioni:<br />Alfabetico - Ordina alfabeticamente i facet.<br />Conteggio - (solo headless) Ordina i facet in base al numero di corrispondenze trovate. |
| Valore massimo | Il numero massimo di valori che possono essere visualizzati nella vetrina per ogni facet. I facet che rappresentano un intervallo di valori vengono distribuiti in modo uniforme. Voci valide: 0 - 100; valore predefinito: 8 |

### Controlli

| Controllo | Descrizione |
|--- |--- |
| ![Selettore pin](assets/btn-pin-blue.png) | Aggiunge o rimuove un facet all&#39;inizio dell&#39;elenco *Filtri*. |
| ![Altro selettore](assets/btn-more.png) | Visualizza un menu di ulteriori azioni che possono essere applicate al facet selezionato. Opzioni: Modifica, Elimina |
| ![Sposta selettore](assets/btn-move.png) | Utilizza l&#39;icona *Sposta* per trascinare un facet bloccato in un&#39;altra posizione nella sezione *Facet bloccati*. |
