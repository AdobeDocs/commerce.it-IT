---
title: Tipi di sinonimo
description: Informazioni sui diversi tipi di sinonimi in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: a74e48ea-e069-4ccc-a67f-2f85be251fb5
TQID: https://experienceleague.adobe.com/23kmFWLruZeFMxIjKZJKbs0y9q10DDtbFG8ioLC5U-o
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# Tipi di sinonimi

I sinonimi unidirezionali e bidirezionali ampliano la definizione di parole chiave. Alcuni sono intercambiabili con la parola chiave, mentre altri rappresentano un sottoinsieme della parola chiave.

## Bidirezionale

I sinonimi bidirezionali hanno lo stesso significato e restituiscono gli stessi risultati di ricerca. Nell&#39;esempio seguente, la prima parola visualizzata in grassetto è la parola chiave utilizzata nel catalogo, seguita da parole che hanno lo stesso significato della parola chiave originale. È possibile creare una semplice coppia di sinonimi bidirezionali o una catena di più sinonimi bidirezionali per la stessa parola chiave.

**giacca** ![Cappotto selettore bidirezionale](../../assets/two-way.png)
**pantaloni** ![Selettore bidirezionale](../../assets/two-way.png) slack ![Selettore bidirezionale](../../assets/two-way.png) pantaloni

## Unidirezionale

Un sinonimo unidirezionale è un sottoinsieme di una parola chiave, ma con un significato più specifico. Ad esempio, i capri e i pantaloni corti sono pantaloni, ma non tutti i pantaloni sono capri o pantaloncini corti. La ricerca di pantaloni include capsule e pantaloncini. Tuttavia, la ricerca di pantaloncini non restituisce capris.

**felpa** ![selettore unidirezionale](../../assets/one-way.png) felpa con cappuccio
**pantaloni** ![Selettore unidirezionale](../../assets/one-way.png) capri ![Selettore unidirezionale](../../assets/one-way.png) vitello-lunghezza-pantaloni ![Selettore unidirezionale](../../assets/one-way.png) pedinatori

## Comportamento sinonimo di più parole

Per i sinonimi composti da più parole, [!DNL Adobe Commerce Optimizer] considera il sinonimo come una frase. Ad esempio, se crei un sinonimo bidirezionale **tavolo da pranzo** ![Selettore bidirezionale](../../assets/two-way.png) **tavolo da cucina** ![Selettore bidirezionale](../../assets/two-way.png) **tavolo da pranzo**, [!DNL Adobe Commerce Optimizer] esegue ricerche in tutti i campi impostati per ricercare l&#39;occorrenza di **tavolo da pranzo** o **tavolo da cucina** o **tavolo da pranzo**.

Se non viene creato alcun sinonimo e un acquirente cerca **la tabella della cucina**, [!DNL Adobe Commerce Optimizer] cerca i termini in qualsiasi punto dei campi ricercabili, anche tra campi diversi, ad esempio **la tabella** nel campo del nome e **la cucina** nella parola chiave meta.

Dopo aver creato un sinonimo, il comportamento di ricerca cambia per cercare la frase esatta **tabella cucina**. Questo potrebbe ridurre il numero di risultati, perché verranno visualizzati solo i prodotti con la frase esatta.

Se desideri cercare i termini separatamente come prima, puoi [creare un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Se la domanda è sufficiente, [!DNL Adobe Commerce Optimizer] prenderà in considerazione l&#39;aggiunta di questa funzionalità al prodotto in una versione futura.
