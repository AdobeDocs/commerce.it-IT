---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%
---
I sinonimi unidirezionali e bidirezionali ampliano la definizione di parole chiave. Alcuni sono intercambiabili con la parola chiave, mentre altri rappresentano un sottoinsieme della parola chiave.

## Bidirezionale

I sinonimi bidirezionali hanno lo stesso significato e restituiscono gli stessi risultati di ricerca. Nell&#39;esempio seguente, la prima parola visualizzata in grassetto è la parola chiave utilizzata nel catalogo, seguita da parole che hanno lo stesso significato della parola chiave originale. È possibile creare una semplice coppia di sinonimi bidirezionali o una catena di più sinonimi bidirezionali per la stessa parola chiave.

**giacca** ![Cappotto selettore bidirezionale](/help/assets/ccdm-shared/synonyms/two-way.png)
**pantaloni** ![Selettore bidirezionale](/help/assets/ccdm-shared/synonyms/two-way.png) slack ![Selettore bidirezionale](/help/assets/ccdm-shared/synonyms/two-way.png) pantaloni

## Unidirezionale

Un sinonimo unidirezionale è un sottoinsieme di una parola chiave, ma con un significato più specifico. Ad esempio, i capri e i pantaloni corti sono pantaloni, ma non tutti i pantaloni sono capri o pantaloncini corti. La ricerca di pantaloni include capsule e pantaloncini. Tuttavia, la ricerca di pantaloncini non restituisce capris.

**felpa** ![selettore unidirezionale](/help/assets/ccdm-shared/synonyms/one-way.png) felpa con cappuccio
**pantaloni** ![Selettore unidirezionale](/help/assets/ccdm-shared/synonyms/one-way.png) capri ![Selettore unidirezionale](/help/assets/ccdm-shared/synonyms/one-way.png) vitello-lunghezza-pantaloni ![Selettore unidirezionale](/help/assets/ccdm-shared/synonyms/one-way.png) pedinatori

## Comportamento sinonimo di più parole

Per i sinonimi composti da più parole, il sistema considera il sinonimo come una frase. Ad esempio, se crei un sinonimo bidirezionale **tavolo da pranzo** ![Selettore bidirezionale](/help/assets/ccdm-shared/synonyms/two-way.png) **tavolo da cucina** ![Selettore bidirezionale](/help/assets/ccdm-shared/synonyms/two-way.png) **tavolo da pranzo**, il sistema esegue la ricerca in tutti i campi impostati per ricercare l&#39;occorrenza di **tavolo da pranzo** o **tavolo da cucina** o **tavolo da pranzo**.

Se non viene creato alcun sinonimo e un acquirente cerca **la tabella della cucina**, il sistema cerca i termini ovunque nei campi ricercabili, anche tra campi diversi, ad esempio **la tabella** nel campo del nome e **la cucina** nella parola chiave meta.

Dopo aver creato un sinonimo, il comportamento di ricerca cambia per cercare la frase esatta **tabella cucina**. Questo potrebbe ridurre il numero di risultati, perché verranno visualizzati solo i prodotti con la frase esatta.

Se desideri cercare i termini separatamente come prima, puoi [creare un ticket di supporto](https://experienceleague.adobe.com/it/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide).
