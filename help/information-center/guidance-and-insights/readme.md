---
title: Governance di approfondimenti e linee guida
description: Scopri il modello di governance interna per approfondimenti e indicazioni. Non pubblicato in Experience League.
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%
---

# Governance di approfondimenti e indicazioni

Questo è un riferimento interno per il team di documentazione. Non è elencato in `TOC.md`, pertanto non è stato generato o pubblicato in Experience League. Tienilo qui in modo che rimanga vicino al contenuto che governa. Per informazioni sulla gestione del Centro informazioni nel suo complesso, consulta [governance.md](../governance.md).

## Proprietà

Gli articoli di approfondimento e guida sono di proprietà dell’autore o del team di pubblicazione che è responsabile del mantenimento della precisione e della valuta dell’articolo. Questi articoli sono attualmente ospitati nell&#39;archivio `commerce.en`. Il team della documentazione di Commerce fornisce assistenza per garantire la qualità dei contenuti e pubblicare l’articolo in produzione.

## Cosa appartiene a Insights e guide

- **Appartiene qui**: guida strategica e white paper per le soluzioni Commerce che descrivono le linee guida di implementazione in base a scenari reali. Includi i collegamenti alle pagine della documentazione di Commerce rilevanti per il supporto.

- **Appartiene al repository del prodotto**: configurazione dettagliata, tutorial, materiale di riferimento (riferimento API/CLI/config) e risoluzione dei problemi. Se un post inizia ad accumulare quel tipo di dettagli, spostalo nella guida del prodotto pertinente e collegalo ad esso.

## Aggiunta di nuovi contenuti

Creare un ticket COMDOX JIRA per l’articolo da pubblicare. Copiare `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)` nella descrizione del ticket e compilarla. Richiede al richiedente di identificare il pubblico, segnalare se il contenuto è temporaneo (con una data di scadenza) e confermare che appartiene a Insights and guidance e non alla documentazione del prodotto Commerce.

Una volta definito l&#39;ambito del ticket, avviare l&#39;articolo da un modello in `templates/` (`whitepaper-template.md`, `security-guidance-template.md`, `insight-perspective-template.md`, non pubblicato, copiare l&#39;articolo pertinente nel file di destinazione ed eliminare i commenti del segnaposto frontmatter del modello). Aggiungi una voce a `help/information-center/TOC.md` in Approfondimenti e linee guida quando il contenuto sarà pronto per la pubblicazione.

- **La nuova sezione principale** (ad esempio, Approfondimenti > Gestione catalogo) richiede una revisione IA prima di aggiungerla, poiché modifica la forma di navigazione della guida. Eseguire il loop in chi possiede Commerce IA review per la storia o l&#39;attività.

- **Aggiungi al sommario**: aggiungi il nuovo argomento al sommario prima di pubblicarlo. Se necessario, nascondi i metadati per pubblicare un articolo nascosto accessibile solo agli utenti che dispongono del collegamento. Vedi [Nascondere il contenuto](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files) nella Guida dell&#39;autore ExL.

## Frequenza di revisione

Rivedi il contenuto dell&#39;articolo quando le nuove soluzioni Commerce vengono rinominate o aggiornate o le informazioni non sono più rilevanti.
