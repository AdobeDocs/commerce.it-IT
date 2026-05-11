---
title: Creare e gestire i sinonimi
description: Scopri come creare e gestire i sinonimi per  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: d2982a0b-e7df-44e6-b3c9-9b4328635d38
TQID: https://experienceleague.adobe.com/YtlgC9okQYDboZg-A0bcnLUVFRH4IVEeBLMeshGad4s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: b5520579-b31f-4df7-9281-f0d9f91e2edc
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 606
ht-degree: 0%

---

# Crea sinonimi

Aumenta il coinvolgimento dei clienti aggiungendo il tuo elenco curato di [!DNL Adobe Commerce Optimizer] sinonimi. Puoi aggiungere fino a 200 sinonimi per origine di catalogo.

![Sinonimo Di Workspace](../../assets/synonym-workspace.png)

## Passaggio 1: aggiungere un sinonimo

1. Dalla barra a sinistra, vai a _Merchandising_ > **Sinonimi**.
1. Fare clic sul pulsante **[!UICONTROL Create synonyms]**.

## Passaggio 2: definire il sinonimo per tipo

Segui le istruzioni per il [tipo di sinonimo](type.md) che desideri creare.

### Sinonimo bidirezionale

1. Immettere il termine o la frase **Parola chiave** da trovare.
1. Immettere i **Espansione** termini che si desidera aggiungere come sinonimi per la parola chiave. Separa più termini con una virgola.
In questo esempio, la parola chiave da associare è &quot;pantaloni&quot; e l&#39;insieme dei termini di espansione sono &quot;pantaloni, slacks&quot;.

   ![Sinonimo bidirezionale](../../assets/synonym-add-two-way.png)

1. Al termine, fare clic su **Salva**.

   Il set di sinonimi viene visualizzato nell&#39;elenco con una freccia bidirezionale tra ciascun termine, il che significa che i termini sono intercambiabili.

   ![Esempio di sinonimo bidirezionale](../../assets/synonym-add-two-way-example.png)

### Sinonimo unidirezionale

1. Fare clic sul tipo di sinonimo **unidirezionale**.

1. Immetti i termini **Parola chiave** e **Espansione**. Separa più termini con una virgola.

   ![Sinonimo unidirezionale](../../assets/synonym-add-one-way.png)

   In questo esempio, la parola chiave è &quot;pantaloni&quot; e i termini di espansione unidirezionale &quot;capris, peddle-pushers&quot; sono ciascuno un sottoinsieme di &quot;pantaloni&quot;, ma con un significato specifico.

1. Al termine, fare clic su **Salva**.

   Il set di sinonimi viene visualizzato nell&#39;elenco con una freccia unidirezionale che punta dai termini di espansione alla parola chiave per indicare che i termini sono sottoinsiemi della parola chiave. Un segno più separa ogni termine di espansione.

   ![Esempio di sinonimo unidirezionale](../../assets/synonym-add-one-way-example.png)

## Passaggio 3: Pubblicare le modifiche

1. Al termine dei sinonimi, fare clic su **Pubblica**.
1. Attendi fino a due ore prima che gli aggiornamenti diventino disponibili nella vetrina.

## Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| [Tipo](type.md) | Determina se i sinonimi hanno lo stesso significato della parola chiave o sono un sottoinsieme della parola chiave. Opzioni:<br />Bidirezionale (impostazione predefinita) - Termini che hanno lo stesso significato della parola chiave e restituiscono gli stessi risultati di ricerca<br />Unidirezionale - Termini che sono un sottoinsieme della parola chiave. I sinonimi unidirezionali restituiscono un elenco più ristretto di prodotti specifici. |
| Parola chiave | Parola comunemente associata a una selezione di prodotti nel catalogo. |
| Espansione | Termini aggiuntivi che hanno lo stesso significato o un significato simile della parola chiave. |

## Gestire i sinonimi

Segui queste istruzioni per gestire [!DNL Adobe Commerce Optimizer] [sinonimi](overview.md) esistenti.

## Trova sinonimo

Per facilitare la ricerca di un sinonimo, è possibile filtrare l&#39;elenco per tipo e cercare per parola chiave o termine di espansione. Questi metodi possono essere utilizzati singolarmente o insieme.

1. Per filtrare l&#39;elenco, impostare **Type** su uno dei seguenti:

   - Tutti
   - Unidirezionale
   - Bidirezionale

1. Per cercare una parola chiave o un termine di espansione, immettere almeno tre caratteri nella casella **[!UICONTROL Search]**.

## Modifica sinonimo

1. Trovare il sinonimo da modificare e fare clic su **Altro** (...) opzioni.

1. Fai clic su **Modifica**.
La parola chiave è il primo termine dell&#39;elenco e ogni termine è separato da una virgola. È possibile aggiornare la parola chiave e i termini di espansione, ma non è possibile modificare il tipo di sinonimo.
1. Fare clic sull&#39;elemento da modificare. Quindi, aggiorna il testo in base alle esigenze.

1. Al termine, fare clic su **Salva**.

## Elimina sinonimo

1. Trovare il sinonimo da eliminare nell&#39;elenco e fare clic su **Altro** (...) opzioni.
1. Fare clic su **Elimina**.
1. Quando richiesto, fare clic su **Elimina sinonimo** per confermare.

## Pubblica modifiche

Per completare il processo, le modifiche salvate devono essere pubblicate nella vetrina. La pubblicazione degli aggiornamenti può richiedere fino a due ore.

1. Fai clic su **Pubblica**.
1. Cerca il messaggio nella parte superiore della pagina che conferma la pubblicazione delle modifiche.
