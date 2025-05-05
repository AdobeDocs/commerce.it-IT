---
title: Cerca in Merchandising Workspace
description: Scopri come utilizzare l’area di lavoro Search Merchandising.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---

# Cerca in Merchandising Workspace

L&#39;area di lavoro *Ricerca merchandising* elenca la selezione corrente di regole e il relativo stato e fornisce l&#39;accesso agli strumenti necessari per creare e gestire le regole. Dall’area di lavoro puoi:

* Cerca regole
* Visualizza dettagli regola
* Attiva/disattiva regole
* Elimina regole
* Accedere all’editor di regole

![Cerca in Workspace di merchandising](assets/rules-workspace.png)

## Impostare l&#39;ambito

Se l&#39;installazione di Adobe Commerce include più visualizzazioni dello store, impostare **Ambito** sulla [visualizzazione dello store](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=it#scope-settings) in cui si applicano le regole.

## Mostra/nascondi colonne

1. Nell&#39;angolo superiore destro fare clic su **Mostra/nascondi** ![Selettore colonna](assets/btn-show-hide-columns.png) colonne.
Le colonne visibili presentano un segno di spunta blu nel menu delle opzioni. Il nome della regola è l&#39;unica colonna che non può essere nascosta.

1. Nel menu, effettuate una delle seguenti operazioni:

   * Per visualizzare una colonna nascosta, fare clic sul nome di una colonna senza segno di spunta.
   * Per nascondere una colonna visibile, fare clic su un nome di colonna con un segno di spunta.

## Filtra regole per stato

1. Se il tuo archivio ha molte regole, puoi filtrarle per stato per ridurre l’elenco. Per impostazione predefinita, nell&#39;elenco Regole vengono visualizzate tutte le regole.

1. Per elencare solo le regole con un&#39;impostazione di stato specifica, impostare **Stato** su una delle seguenti opzioni:

   * Tutti
   * Attivo
   * Inattivo
   * Pianificato

## Trova regole di ricerca per nome

Inizia a digitare il nome della regola o qualsiasi parola nel nome della regola.
La ricerca trova le regole corrispondenti durante la digitazione. La stringa di caratteri corrispondenti viene evidenziata nel nome di ogni regola trovata.

![Regole - trova per nome](assets/rules-workspace-search-name.png)

## Visualizza dettagli

Il pannello dei dettagli mostra il nome della regola, lo stato, le condizioni e gli eventi, la data di inizio e di fine, la descrizione e la data dell’ultima modifica. Le regole possono essere abilitate, modificate ed eliminate dal pannello dei dettagli.

1. Nell&#39;area di lavoro *Ricerca merchandising*, individuare la regola nella griglia che si desidera visualizzare e fare clic su **Altro** (...).
1. Fare clic su **Visualizza dettagli**.
Dal pannello Visualizza dettagli potete effettuare una delle seguenti operazioni:

   * Modifica regola
   * Elimina regola
   * Attiva/Disattiva regola

1. Per chiudere il pannello *Visualizza dettagli*, fare clic su **Chiudi** (X) nell&#39;angolo superiore destro.

   ![Regola - dettagli](assets/rules-workspace-details.png)

## Descrizioni delle colonne

| Colonna | Descrizione |
|--- |--- |
| Nome | Nome della regola. |
| Ultimo aggiornamento | Data dell’ultimo aggiornamento della regola. |
| Data di inizio | Data di inizio di una regola pianificata. |
| Data di fine | Data di fine di una regola pianificata. |
| Stato | Lo stato con codice colore indica lo stato corrente della regola. Utilizzare il controllo Stato sopra la griglia per filtrare le regole per stato. Valori:<br />Tutti gli stati - Visualizza tutte le regole indipendentemente dallo stato.<br />Attivo (blu): visualizza solo le regole attive.<br />Pianificato (arancione): visualizza solo le regole pianificate.<br />Inattivo (grigio): visualizza solo le regole inattive. |

## Controlli

| Controllo | Descrizione |
|--- |--- |
| Aggiungi regola | Apre l&#39;[editor regole](rules-add.md). |
| Stato | Filtra l’elenco delle regole in base allo stato. Opzioni: Tutti, Attivo, Inattivo, Pianificato |
| ![Selettore colonna](assets/btn-show-hide-columns.png) | Specifica le colonne visibili nella griglia. Opzioni: Ultimo aggiornamento, Data inizio, Data fine, Stato |
| Ricerca | Cerca una regola per nome completo o per corrispondenza parziale. |
| ![Altro selettore](assets/btn-more.png) | Visualizza un menu di altre azioni che possono essere applicate alla regola selezionata. Opzioni: Modifica, Visualizza dettagli, Elimina |

## Dettagli regola

| Campo | Descrizione |
|--- |--- |
| Stato | Stato corrente della regola. |
| Condizioni | Query di ricerca che descrive le condizioni associate alla regola. |
| Data di inizio | Data in cui la regola entra in vigore, se pianificata. |
| Data di fine | Data di scadenza della regola, se pianificata. |
| Descrizione | Breve descrizione della regola. |
| Ultimo aggiornamento | Data e ora dell’ultimo aggiornamento della regola. |
| Abilitato | Controllo che modifica lo stato della regola. Opzioni: Abilitato / Disabilitato |
