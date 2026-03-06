---
title: Tipi di sinonimo
description: Informazioni sui diversi tipi di sinonimi in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: a74e48ea-e069-4ccc-a67f-2f85be251fb5
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Tipi di sinonimi

I sinonimi unidirezionali e bidirezionali ampliano la definizione di parole chiave. Alcuni sono intercambiabili con la parola chiave, mentre altri rappresentano un sottoinsieme della parola chiave.

## Bidirezionale

I sinonimi bidirezionali hanno lo stesso significato e restituiscono gli stessi risultati di ricerca. Nell&#39;esempio seguente, la prima parola visualizzata in grassetto è la parola chiave utilizzata nel catalogo, seguita da parole che hanno lo stesso significato della parola chiave originale. È possibile creare una semplice coppia di sinonimi bidirezionali o una catena di più sinonimi bidirezionali per la stessa parola chiave.

**giacca** ![Cappotto selettore bidirezionale](../../assets/two-way.png)
**pantaloni** ![Selettore bidirezionale](../../assets/two-way.png) pantaloni ![Selettore bidirezionale](../../assets/two-way.png) pantaloni

## Unidirezionale

Un sinonimo unidirezionale è un sottoinsieme di una parola chiave, ma con un significato più specifico. Ad esempio, i capri e i pantaloni corti sono pantaloni, ma non tutti i pantaloni sono capri o pantaloncini corti. La ricerca di pantaloni include capsule e pantaloncini. Tuttavia, la ricerca di pantaloncini non restituisce capris.

**felpa** ![selettore unidirezionale](../../assets/one-way.png) felpa con cappuccio
**pantaloni** ![Selettore unidirezionale](../../assets/one-way.png) capri ![Selettore unidirezionale](../../assets/one-way.png) vitello-lunghezza-pantaloni ![Selettore unidirezionale](../../assets/one-way.png) pedinatori

## Comportamento sinonimo di più parole

Per i sinonimi composti da più parole, [!DNL Adobe Commerce Optimizer] considera il sinonimo come una frase. Ad esempio, se crei un sinonimo bidirezionale **tavolo da pranzo** ![Selettore bidirezionale](../../assets/two-way.png) **tavolo da cucina** ![Selettore bidirezionale](../../assets/two-way.png) **tavolo da pranzo**, [!DNL Adobe Commerce Optimizer] esegue ricerche in tutti i campi impostati per ricercare l&#39;occorrenza di **tavolo da pranzo** o **tavolo da cucina** o **tavolo da pranzo**.

Se non viene creato alcun sinonimo e un acquirente cerca **la tabella della cucina**, [!DNL Adobe Commerce Optimizer] cerca i termini in qualsiasi punto dei campi ricercabili, anche tra campi diversi, ad esempio **la tabella** nel campo del nome e **la cucina** nella parola chiave meta.

Dopo aver creato un sinonimo, il comportamento di ricerca cambia per cercare la frase esatta **tabella cucina**. Questo potrebbe ridurre il numero di risultati, perché verranno visualizzati solo i prodotti con la frase esatta.

Se desideri cercare i termini separatamente come prima, puoi [creare un ticket di supporto](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Se la domanda è sufficiente, [!DNL Adobe Commerce Optimizer] prenderà in considerazione l&#39;aggiunta di questa funzionalità al prodotto in una versione futura.
