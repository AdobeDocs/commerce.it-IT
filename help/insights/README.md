---
title: Governance della documentazione Commerce
description: 'Scopri il modello di governance interno per Commerce Insights. Non pubblicato in Experience League: mantenuto fuori da TOC.md intenzionalmente.'
source-git-commit: 1da6d9753acbeadf3a0df5fae86a9386643c6d6d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Governance della documentazione Commerce

Questo è un riferimento interno per il team di documentazione. Non è elencato in `TOC.md`, pertanto non è stato generato o pubblicato in Experience League. Tienilo qui in modo che rimanga vicino al contenuto che governa.

## Proprietà

Gli articoli di Commerce Insights sono di proprietà dell’autore o del team di pubblicazione che è responsabile della precisione e della valuta dell’articolo. Questi articoli sono attualmente ospitati nell&#39;archivio `commerce.en`. Il team della documentazione di Commerce fornisce assistenza per garantire la qualità dei contenuti e pubblicare l’articolo in produzione.

## Cosa appartiene a Commerce Insights

- **Appartiene qui**: guida strategica e white paper per le soluzioni Commerce che descrivono le linee guida per l&#39;implementazione in base a scenari reali. Includi i collegamenti alle pagine della documentazione di Commerce rilevanti per il supporto.

- **Appartiene al repository del prodotto**: configurazione dettagliata, tutorial, materiale di riferimento (riferimento API/CLI/config) e risoluzione dei problemi. Se un post inizia ad accumulare quel tipo di dettagli, spostalo nella guida del prodotto pertinente e collegalo ad esso.

## Aggiunta di nuovi contenuti

Creare un ticket COMDOX JIRA per l’articolo da pubblicare. Copiare `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)` nella descrizione del ticket e compilarla. Il richiedente dovrà identificare il pubblico, segnalare se il contenuto è temporaneo (con una data di scadenza) e confermare che appartiene alla Guida di Insights e non alla documentazione di Commerce.

Una volta definito l&#39;ambito del ticket, avviare l&#39;articolo da un modello in `templates/` (`whitepaper-template.md`, `security-guidance-template.md`, `insight-perspective-template.md`, non pubblicato, copiare l&#39;articolo pertinente nel file di destinazione ed eliminare i commenti del segnaposto frontmatter del modello). Aggiungi una voce `TOC.md` quando il contenuto è pronto per la pubblicazione.

- **La nuova sezione principale** (ad esempio, Approfondimenti > Gestione catalogo) richiede una revisione IA prima di aggiungerla, poiché modifica la forma di navigazione della guida. Eseguire il loop in chi possiede Commerce IA review per la storia o l&#39;attività.

- **Aggiungi al sommario** - Aggiungi un nuovo argomento al sommario prima della pubblicazione. Se necessario, nascondi i metadati per pubblicare un articolo nascosto accessibile solo agli utenti che dispongono del collegamento. Vedi [Nascondere il contenuto](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files) nella Guida dell&#39;autore ExL.

## Frequenza di revisione

Rivedi il contenuto dell&#39;articolo quando le nuove soluzioni Commerce vengono rinominate o aggiornate o le informazioni non sono più rilevanti.
