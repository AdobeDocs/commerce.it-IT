---
title: Flussi di lavoro per l'evasione di assistenza al negozio
description: Scopri i moduli Prelievo, Staging, Mano-Fuori e Ordini disponibili nell’app Assist per store. Questi moduli consentono il flusso di lavoro di evasione del punto vendita end-to-end per gli ordini BOPIS. Gli associati al negozio utilizzano questi moduli per gestire e consegnare gli ordini di prelievo del negozio ai clienti.
role: Leader, Admin, User
level: Intermediate
feature: Shipping/Delivery, Tools and External Services, Customer Service
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---

# Flussi di lavoro per l&#39;evasione di assistenza al negozio

L&#39;app Store Assist fornisce a Store Associates quattro moduli per gestire il processo di evasione in-store per gli ordini di acquisto online e ritiro in store:

- **[Prelievo](#pick-module)**: ottieni la piena visibilità di tutti gli articoli ordinati e degli strumenti per assicurarti che vengano prelevati gli articoli e le quantità corrette. Gli associati al negozio possono scegliere uno o più ordini contemporaneamente per una maggiore efficienza.

- **[Fase](#stage-module)** - Immettere il luogo in cui vengono effettuati gli ordini mentre i clienti si recano al negozio, in modo che gli associati al negozio possano trovare e consegnare gli ordini più rapidamente.

- **[Mano spenta](#hand-off-module)** - Ricevi notifiche in tempo reale dopo l&#39;arrivo dei clienti allo store per ridurre al minimo il tempo di attesa e gli ordini di trasferimento.

- **[Ordini](#orders-module)**: visualizza un elenco di tutti gli ordini effettuati per un negozio in modo che tutti conoscano il numero di ordini e lo stato di ciascun ordine.

>[!NOTE]
>
>Prima che gli Store Associates possano usare l&#39;app Store Assist, un amministratore deve completare il [processo di configurazione dell&#39;app](app-setup.md).

## Scegli modulo

Il modulo Scegli aiuta i soci del negozio a trovare e analizzare gli articoli ordinati dal cliente e a confezionarli per il ritiro. Puoi vedere quanti ordini sono scaduti e iniziare a sceglierli immediatamente. È inoltre possibile scegliere prima altri ordini. Gli ordini vengono ordinati in base al tempo di scadenza della consegna, a partire dagli ordini scaduti. Gli assegnatari del Negozio possono selezionare gli ordini da prelevare in base all&#39;ordine richiesto per le operazioni.

I dipendenti possono inoltre scegliere di scegliere di scegliere un ordine alla volta o più ordini contemporaneamente.

Durante il prelievo, gli associati al negozio visualizzano un elenco di tutti gli articoli da prelevare per ciascun ordine, le relative quantità, il prezzo e la descrizione del prodotto dal catalogo. Viene visualizzata una barra di avanzamento che consente di spostarsi all&#39;interno di Store Assist durante il prelievo degli ordini.

Una volta che gli associati iniziano il prelievo e selezionano gli articoli da prelevare, vengono presentate tutte le informazioni rilevanti per l&#39;articolo, ad esempio: dimensioni, colore, quantità, prezzo, descrizione, adattamento e SKU/UPC. Gli associati dispongono di due azioni per il prelievo degli ordini:

- Indica che l&#39;articolo non è stato trovato e attiva un rimborso.
- Analizzare il codice a barre sull&#39;elemento. Lo scopo della scansione è quello di verificare che hanno scelto l&#39;articolo corretto. Nel caso in cui la fotocamera non riesca a leggere il codice a barre, i soci del negozio devono immettere manualmente lo SKU dell&#39;articolo che hanno scelto.

Se gli associati non riescono a trovare un elemento, possono saltarlo e tornare in un secondo momento.  Il rimborso di cui sopra viene emesso solo una volta che completano la loro fase di pick walk l&#39;ordine.

## Modulo stage

Il modulo Stage mostra dove viene effettuato l&#39;ordine in batch fino a quando il cliente non arriva per ritirarlo. L&#39;impostazione di questa ubicazione è un passo fondamentale per evitare la perdita di ordini quando gli associati al negozio finiscono il turno prima dell&#39;arrivo del cliente o se sono presenti molti ordini. In entrambi i casi, è stato progettato per aiutarti a trovare rapidamente l&#39;ordine giusto con tutte le informazioni rilevanti.

È possibile utilizzare una barra di testo in formato libero per indicare la posizione dell&#39;ordine: sotto il bancone, nel retro o nella posizione B3, in base alle operazioni eseguite.

Puoi anche aggiornare facilmente la posizione di staging nell&#39;app, se i tuoi associati dovevano metterla altrove.

## Modulo Mano spento

Il modulo [!UICONTROL Hand Off] mostra quali clienti hanno effettuato il check-in per ritirare i loro ordini, dove i loro ordini sono posizionati nell&#39;area intermedia e li attendono. I clienti possono ritirare gli ordini sia nel negozio o nel parcheggio fuori/sul marciapiede. Le informazioni sulla loro esatta posizione vengono presentate in questo modulo dopo il check-in.

Dopo aver selezionato un ordine pronto per il trasferimento del cliente. Tutti possono visualizzare le informazioni sull&#39;ordine, inclusi eventuali articoli non trovati, l&#39;ubicazione di attesa del cliente, il tempo di attesa, la posizione in cui l&#39;ordine è posizionato nell&#39;area intermedia e il numero di telefono del cliente, se disponibile.

Il cliente potrebbe aver scelto una persona alternativa per ritirare l&#39;ordine. In questo caso, vengono visualizzati il nome e le informazioni di contatto della persona che deve scegliere l&#39;ordine.

Al momento della consegna dell&#39;ordine al cliente, l&#39;Associato al negozio deve accettare l&#39;ordine o rifiutare determinati articoli. Una volta soddisfatto, il cliente deve firmare per l&#39;ordine sul dispositivo del proprio associato, se una firma richiede una firma per la società.

Se i clienti arrivano senza aver effettuato il check-in, i dipendenti possono effettuare il check-in manualmente.

## Modulo Ordini

Nel modulo Ordini vengono visualizzati tutti gli ordini esistenti e il relativo stato. Quando un cliente chiama per controllare il proprio ordine, gli associati al negozio possono trovare rapidamente le informazioni ricercando il numero o eseguendo una ricerca dal modulo Ordini.

Gli associati allo store possono anche annullare gli ordini dalla pagina Ordini dell’app Assistenza allo store.
