---
title: Impostazioni
description: Configura le impostazioni per  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: 6ac223de-8e03-4842-8b67-92ce321d323d
TQID: https://experienceleague.adobe.com/9-BMXoWad0bbvsnwgHQrs19ZC9ngGrVE9J7PszcX4Zc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 471
ht-degree: 0%

---

# Impostazioni

Utilizza l&#39;area di lavoro *Impostazioni* per configurare gli intervalli e gli intervalli del facet di prezzo e la lingua predefinita per l&#39;individuazione del prodotto.

Fatturazione prezzo specifica il numero di gruppi di intervalli di prezzi e il modo in cui i valori di prezzo vengono distribuiti tra di essi.

L&#39;impostazione **Lingua** indica a [!DNL Adobe Commerce Optimizer] quale lingua aspettarsi durante la scrittura dell&#39;indice.

## Fatturazione del prezzo

È possibile specificare il numero di gruppi di intervalli di prezzi e il modo in cui i valori di prezzo vengono distribuiti tra di essi. Ogni fascia di prezzo si sovrappone al gruppo precedente di uno. Ad esempio, cinque gruppi con un intervallo di 20 creano le seguenti fasce di prezzo: 0-20, 20-40, 40-60, 60-80 e >80. Se il catalogo non contiene un numero di prodotti sufficiente per riempire tutti gli intervalli definiti, la visualizzazione dei gruppi disponibili viene regolata di conseguenza. Ad esempio: 0-20, 60-80, >80.

1. Nell&#39;area di lavoro **Impostazioni**, selezionare **[!UICONTROL Search]**, quindi in **Fatturazione prezzo**, eseguire le operazioni seguenti:
   - Immetti il **numero di selezioni** o i raggruppamenti di prezzi da rendere disponibili. È possibile definire fino a 100 raggruppamenti di prezzi.
   - Immettere il valore **Intervallo** o l&#39;intervallo di prezzi per ogni gruppo. Il valore massimo è 40.000.000.
1. Fai clic su **Salva**.

   La disponibilità delle impostazioni aggiornate nella vetrina richiede circa 15 minuti.

### Descrizioni dei campi

| Campo | Descrizione |
|--- |--- |
| Numero di selezioni | Specifica il numero di raggruppamenti di intervalli di prezzi che possono essere utilizzati come filtri di ricerca nella vetrina. Valore predefinito: 8, valore massimo: 100 |
| Valore intervallo | Specifica l&#39;intervallo di prezzo per ogni gruppo. Ad esempio, cinque selezioni con un valore di intervallo pari a 20 creano cinque raggruppamenti di 0-20, 20-40, 40-60, 60-80 e >80. Valore predefinito: 5, valore massimo: 40.000.000 |

## Lingua

L&#39;impostazione della lingua indica a [!DNL Adobe Commerce Optimizer] quale lingua aspettarsi durante la lettura del catalogo e la scrittura dell&#39;indice.

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
