---
title: Verifica e distribuisci l'evasione dell'archivio
description: Piano di test per verificare la funzionalità Evasione punto vendita. I test coprono l'API di sincronizzazione dell'inventario, il flusso di lavoro di esecuzione end-to-end per gli ordini annullati, la gestione degli utenti dell'app Store Fulfillment e l'esperienza di archiviazione del cliente.
role: User, Admin
level: Intermediate
feature: Shipping/Delivery, User Account, Roles/Permissions
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 0%

---

# Test e distribuzione del completamento dell’archivio per Adobe Commerce

Dopo aver completato il processo di onboarding nell’ambiente di sviluppo, puoi avviare il processo per testare e distribuire la soluzione Store Fulfillment nell’ambiente di produzione.

**Prerequisiti**

Prima di eseguire il test o la sincronizzazione di informazioni, archivi o ordini, verificare di aver completato le seguenti attività:

- Completata la [configurazione generale](enable-general.md) per i servizi di distribuzione archivio.

- [Aggiungi e convalida le credenziali dell’account e i dettagli di connessione per gli ambienti sandbox e di produzione](connect-set-up-service.md#configure-store-fulfillment-account-credentials)

- Conferma che l&#39;[Integrazione Adobe Commerce](connect-set-up-service.md#configure-store-fulfillment-account-credentials) per la soluzione Store Fulfillment sia disponibile e autorizzata.

## Preparazione per il test

La configurazione della connessione deve essere completata prima di poter creare ordini di test o eseguire test di integrazione. Prima di eseguire il test, è necessario verificare che i dati dell’archivio siano sincronizzati.

1. Sincronizza origini di evasione archivio.

   - Vai a **[!UICONTROL Stores > Sources]**.

   - Selezionare **[!UICONTROL Synchronize Store Fulfillment Sources]**.

1. Dalla griglia dell&#39;archivio verificare che gli archivi siano stati contrassegnati come `Synced` prima di creare gli ordini di test.

## Piano di prova di esempio

I rivenditori convalidano le funzionalità di base della soluzione Store Fulfillment durante le fasi di configurazione e di test di una distribuzione. Questo piano di test di esempio fornisce un punto di partenza per il test. Aggiungi altri scenari in base alle tue esigenze.

>[!NOTE]
>
>Dopo aver completato l’onboarding iniziale per la soluzione Store Fulfillment o aver aggiornato un’installazione esistente, testa sempre l’applicazione in un ambiente non di produzione prima di implementarla in produzione.

Il presente piano di prova di esempio riguarda le seguenti aree funzionali:

| Area funzionale | Funzione | Ruolo |
|-------------------------------------|------------------------------------------|----------------------------------|
| Sincronizzazione di magazzino e ordini | Sincronizzazione API inventario | Amministratore Adobe Commerce |
| End-to-End | Flussi di lavoro per annullamento ordine | Cliente, Amministratore, Associate store |
| Amministratore | Autorizzazioni app di esecuzione store | Amministratore |
| Adobe Commerce Frontend | Tipi di prodotto | Cliente, Amministratore |
| Estrazione front-end</br>Modulo di archiviazione | Esperienza di check-in | Cliente, Amministratore |
| App assistenza store | Ordine</br>Prelievo</br>Fase</br>e handoff | Associa store |

### Sincronizzazione API inventario

Questa sezione del piano di test riguarda la sincronizzazione di inventario e ordine per verificare che gli aggiornamenti alle origini di prelievo e alle scorte siano sincronizzati correttamente tra Adobe Commerce e la soluzione di evasione dello store.

**Area funzionale**: Sincronizzazione inventario e ordine</br>
**Ruolo:** Amministratore</br>
**Tipo di test:** Tutti positivi

<table>
<thead>
<tr>
<th>Funzione</th>
<th>Scenario di prova</th>
<th>Risultati previsti</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Aggiungi origine scorte di prelievo</strong></td>
<td>Salvare una nuova origine di materiale di prelievo.</td>
<td>La sincronizzazione in tempo reale invia i dettagli dell'origine al servizio Walmart GIF entro 5 minuti.</td>
</tr>
<tr>
<td><strong>Aggiorna origine scorte di prelievo esistente</strong></td>
<td>Salvare gli aggiornamenti a un'origine di prelievo esistente.</td>
<td>L'operazione di sincronizzazione in tempo reale invia i dettagli a Walmart GIF entro 5 minuti</td>
</tr>
<tr>
<td><strong>Stato origine scorte di ritiro</br><code>Is Synced</code></strong></td>
<td>Salvare gli aggiornamenti a un'origine di prelievo esistente.</td>
<td>Dopo un'operazione riuscita, la colonna <code>Is Synced</code> della pagina Gestisci Source viene aggiornata da <code>No</code> a <code>Yes</code>.</td>
</tr>
<tr>
<td><strong>Processo di prenotazione scorte modificate</strong></td>
<td>Crea e invia un nuovo ordine per un prodotto.</td>
<td>La quantità vendibile per il prodotto diminuisce di conseguenza.</td>
</tr>
<tr>
<td><strong>Push per nuovo ordine, sincronizzazione API: ordine cliente</strong></td>
<td>Il cliente invia un ordine di prelievo del negozio.</td>
<td><ul><li>Nella visualizzazione Ordine amministratore, un <strong>utente amministratore di Adobe Commerce</strong> vede che lo stato di sincronizzazione ordini è stato aggiornato a <code>Sent</code></li><li>Il registro dei dettagli dell’ordine include il messaggio <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Push per nuovo ordine, sincronizzazione API: l'amministratore invia l'ordine</strong></td>
<td>Un <strong>amministratore</strong> di Adobe Commerce invia un ordine di prelievo.</td>
<td><ul><li>Nella visualizzazione Ordine amministratore, lo stato di sincronizzazione ordini viene aggiornato a <code>Sent</code>.</li><li>Il registro dei dettagli dell’ordine include il messaggio <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Push nuovo ordine, coda eccezioni<strong></td>
<td>Identifica diversi prodotti virtuali e scaricabili nell’amministratore di Adobe Commerce che possono essere soddisfatti tramite Adobe Commerce senza richiedere l’interazione con il servizio di evasione (FaaS).</td>
<td>Questi prodotti sono rimossi o contrassegnati in modo appropriato nell'esportazione per evitare un conflitto a valle con le FAAS.</td>
</tr>
</tbody>
</table>

### Flussi di lavoro per annullamento ordine

Questa sezione del piano di test include scenari per testare il flusso di lavoro end-to-end per gli ordini annullati tramite Adobe Commerce.

**Area funzionale:** Amministratore Adobe Commerce</br>
**Ruolo:** End-to-End (Amministratore, Associato Store, Cliente)</br>
**Tipo di risultato del test:** positivo per tutti gli scenari

<table style="table-layout:fixed">
<tr>
<th>Funzione</th>
<th>Scenario</th>
<th>Risultati previsti</th>
</tr>
<tr>
<td><strong>Annullamento completo dell’ordine</strong></td>
<td><ol>
<li>Ordinate.</li>
<li>Attendi che l’ordine venga sincronizzato.</li>
<li>Verificare la ricezione dell'e-mail della fattura (se si autorizza e si acquisisce).</li>
<li>Creare una nota di credito con tutti i prodotti ordinati dalla vista Fattura.</li>
</ol>
</td>
<td>
<ul>
<li>Cronologia ordini aggiornata con <code>We refunded $X online. Transaction ID: transactionID</code> e <code>Received Cancel acknowledgment from the BOPIS solution.</code></li>
<li>Stato ordine: <code>Closed</code>. (Abbiamo impostato PAYMENT REVIEW adesso.)</li>
<li>Nota di credito creata in Adobe Commerce. (Attendere che il cron funzioni).</li>
<li>Se vengono selezionati tutti gli elementi, l'indirizzo e-mail di prelievo <code>DISPLAY COMMENT HISTORY</code> mostra <code>Order is ready for pickup</code> (<code>CUSTOMER NOTIFIED</code> flag è <code>true</code>).</li>
<li>Se non vengono prelevati tutti gli elementi, vengono visualizzati i messaggi e-mail di annullamento e VISUALIZZA CRONOLOGIA COMMENTI <code>Order has been canceled - all items were not available</code></li>
<li><code>CUSTOMER NOTIFIED</code> il contrassegno è <code>true</code>.)</li>
</ul>
</td>
</tr>
<tr><td><strong>Annullamento parziale dell'ordine<strong></td>
<td>
<ol>
<li>Effettuare l'ordine con almeno due prodotti.</li>
<li>Attendi che l’ordine venga sincronizzato.</li>
<li>Verificare che la fattura sia stata creata (se si autorizza e si acquisisce) e che sia stata ricevuta un'e-mail di fattura.</li>
<li>Attendere due ore per la liquidazione della transazione.</li>
<li>Creare una nota di credito con solo una parte dei prodotti ordinati dalla vista Fattura.</li>
</td>
<td>
<ul>
<li>Aggiornamento cronologia ordini: <code>We refunded $X online. Transaction ID: transactionID</code></li>
<li>Aggiornamento cronologia ordini: <code>Order notified as partly canceled at: Date and Hour</code></li>
<li>Ricevuta e-mail di rimborso ordine: <code>$x amount was refunded</code></li>
<li>Stato ordine: <code>Processing</code>.</li>
<li>Nota di credito creata in Adobe Commerce (attendi che cron funzioni).</li>
<li>Se alcuni elementi non sono stati prelevati, verificare che venga visualizzata l'e-mail [!UICONTROL Ready for Pickup] con la sezione prelievo o rimborso pari a zero. <code>DISPLAY COMMENT HISTORY</code> mostra <code>Order is ready for pickup, but some items not available.</code>.</li>
<li><code>CUSTOMER NOTIFIED</code> il flag è <code>true</code>.</li>
</ul>
</td>
</tr>
<td><strong>Pronto per il ritiro</br></br>Annullamento completo</br>(tutti i prodotti sono impostati come prelevati con quantità pari a 0)</strong></td>
<td>
<ol>
<li>Effettua l’ordine.</li>
<li>Attendi che l’ordine venga sincronizzato.</li>
<li>Verificare che la fattura sia stata creata (se si autorizza e si acquisisce) e che sia stata ricevuta un'e-mail di fattura.</li>
<li>Andare al Postman ed eseguire la richiesta Ready for Pickup con tutti i prodotti impostati come <code>picked</code> con <code>0 qty</code>.</li>
</ol>
</td>
<td>
<ul>
<li>Cronologia ordini aggiornata: <code>We refunded $X offline</code></li>
<li>Lo stato dell'ordine è <code>CLOSED</code>.
<li>Viene creata la nota di credito. (Attendere che il cron funzioni).</li>
<li>E-mail di rimborso ricevuta: <code>$x amount was refunded</code></li>
<li>E-mail di annullamento ordine inviata.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Pronto per il ritiro - Annullamento parziale</strong></br></br><strong>(Alcuni prodotti sono stati prelevati e altri con <code>0 qty</code>)</strong>
</td>
<td>
<ol>
<li>Effettua l’ordine.</li>
<li>Attendi che l’ordine venga sincronizzato.</li>
<li>Verificare che la fattura sia stata creata (se si autorizza e si acquisisce) e che sia stata ricevuta un'e-mail di fattura.</li>
<li>Vai al Postman ed esegui la richiesta Pronto per il ritiro con parte dei prodotti impostati come prelevati con 0 qtà e il resto prelevato.</li>
</ol>
</td>
<td>
<ul>
<li><code>Your order is ready for pickup</code> con [!UICONTROL Ready for Pickup Items] e [!UICONTROL Canceled Items] tabelle. </li>
<li>Lo stato dell'ordine è PRONTO PER IL RITIRO. </li>
<li>Cronologia ordini aggiornata: <code>We refunded $X offline.</code>
<li>Cronologia ordini aggiornata: <code>Order notified as partly canceled at: Date and hour</code>
<li>E-mail di rimborso ricevuta: <code>$x amount was refunded</code>
<li>Viene creata la nota di credito. (Attendere che il cron funzioni).</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Pronto per il ritiro - Annullamento parziale</br></br>Alcuni prodotti sono stati prelevati, altri con <code>0 qty</code>)</strong>
</td>
<td><ol>
<li>Effettua l’ordine.</li>
<li>Attendi che l’ordine venga sincronizzato.</li>
<li>Verificare che la fattura sia stata creata (se si autorizza e si acquisisce) e che sia stata ricevuta un'e-mail di fattura.</li>
<li>Vai al Postman ed esegui la richiesta Pronto per il ritiro con parte dei prodotti impostati come prelevati con 0 qtà e il resto prelevato.</li>
</ol>
</td>
<td><ul>
<li><code>Your order is ready for pickup</code> con [!UICONTROL Ready for Pickup Items] e [!UICONTROL Canceled Items] tabelle. </li>
<li>Lo stato dell'ordine è PRONTO PER IL RITIRO. </li>
<li>Cronologia ordini aggiornata: <code>We refunded $X offline.</code>
<li>Cronologia ordini aggiornata: <code>Order notified as partly canceled at: Date and hour</code>
<li>E-mail di rimborso ricevuta: <code>$x amount was refunded</code>
<li>Viene creata la nota di credito. (Attendere che il cron funzioni).</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Erogato (durante la dispensazione) </br></br>Annullamento completo (tutti i prodotti sono impostati come rifiutati)</strong>
</td>
<td>
<ol>
<li>Effettua l’ordine.</li>
<li>Attendi che l’ordine venga sincronizzato.</li>
<li>Verificare che la fattura sia stata creata (se si autorizza e si acquisisce) e che sia stata ricevuta un'e-mail di fattura.</li>
<li>Vai al Postman ed esegui la richiesta Pronto per il ritiro con tutti i prodotti impostati come prelevati.</li>
<li>Apri la cassetta postale, individua l’e-mail Pronto per il ritiro. Quindi fare clic su **[!UICONTROL Confirm Arrival]**.</li>
<li>Archivia.</li>
<li>Vai a Postman ed esegui la richiesta Dispensed con tutti i prodotti impostati come rifiutati.</li>
</ol>
<td><ul>
<li>Cronologia ordini aggiornata: <code>We refunded $X offline.</code></li>
<li>E-mail di rimborso ricevuta: <code>$x amount was refunded</code></li>
<li>Stato impostato su <code>CLOSED</code>.</li>
<li>Nota di credito creata. (Attendere che il cron funzioni).</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Erogati (durante la dispensazione)</br></br>Annullamento parziale</br>(Alcuni prodotti vengono distribuiti; alcuni rifiutati)</strong>
</td>
<td>
<ol>
<li>Effettua l’ordine.</li>
<li>Attendi che l’ordine venga sincronizzato.</li>
<li>Verificare che la fattura sia stata creata (se si autorizza e si acquisisce) e che sia stata ricevuta un'e-mail di fattura.</li>
<li>Vai a Postman ed esegui la richiesta Pronto per il ritiro con tutti i prodotti impostati come prelevati.</li>
<li>Apri la cassetta postale. Trovare l'e-mail pronta per il ritiro e selezionare <code>Confirm Arrival</code>.</li>
<li>Archivia.</li>
<li>Andare al Postman ed eseguire la richiesta dispensata con alcuni prodotti impostati per la dispensazione e alcuni impostati per il rifiuto</li>
</ol>
</td>
<td>
<li>Cronologia ordini aggiornata: <code>We refunded $X offline</code></li>
<li><code>Order notified as partly canceled at: Date and Hour</code>
<li>E-mail di rimborso ricevuta: <code>$x amount was refunded</code>
<li>Stato ordine impostato su <code>Ready for pickup Dispensed</code>
<li>Nota di credito creata. (Attendere che il cron funzioni).</li>
</td>
</tr>
<tr>
<td> <strong>Nuova RMA dopo il ritorno (completo)</strong>
</td>
<td>
<ol>
<li>Effettua l’ordine.</li>
<li>Attendi che l’ordine venga sincronizzato.</li>
<li>Se l'opzione Autorizza e acquisisci è configurata, verificare che la fattura sia stata creata e che il cliente abbia ricevuto l'e-mail della fattura.</li>
<li>Scegli tutti i prodotti con Postman.</li>
<li>Archivia.</li>
<li>Fai una dispensa.</li>
<li>Vai all'ordine e seleziona <strong>[!UICONTROL Create returns]=
<li>Creare la RMA.</li>
</ol>
</td>
<td>
<ul>
<li>La RMA è stata creata ed è visualizzata sotto la scheda <strong>[!UICONTROL Returns]</b> nella visualizzazione Ordine.</li>
<li>Il cliente ha ricevuto l’e-mail di conferma RMA.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Nuova RMA dopo la restituzione - Parziale</strong>
</td>
<td>
<ol>
<li>Effettua l’ordine.</li>
<li>Attendi che l’ordine venga sincronizzato.</li>
<li>Verificare che la fattura sia stata creata (se si autorizza e si acquisisce) e che sia stata ricevuta un'e-mail di fattura.</li>
<li>Scegli tutti i prodotti con Postman.</li>
<li>Archivia.</li>
<li>Fai una dispensa.</li>
<li>Vai all’ordine e seleziona  <strong>[!UICONTROL Create returns]</strong></li>
<li>Creare la RMA con parte dei prodotti ordinati.</li>
</ol>
<td>
<ul>
<li>RMA creato e visualizzato sotto la scheda <strong>[!UICONTROL Returns]</strong> nella visualizzazione Ordine.</li>
<li>Il cliente ha ricevuto l’e-mail di conferma RMA.</li>
<li>Dopo aver creato RMA, ottenere l'autorizzazione RMA: dall'amministratore, passare a <strong>[!UICONTROL Sales > Returns]</strong>. Selezionare la RMA creata e autorizzarla.</li>
<li>Verificare che il cliente abbia ricevuto l'e-mail di conferma dell'autorizzazione RMA.</li>
<li>Verificare che il rimborso sia stato aggiunto alla cronologia transazioni e ordini.</li>
</ul>
</td>
</tr>
</table>


### Autorizzazioni app di esecuzione store

Questa sezione del piano di test tratta la gestione dell’account per gli utenti dell’app Store Fulfillment.

- Conferma che un Associate store possa eseguire l’autenticazione con un nuovo account utente creato dall’Amministratore Adobe Commerce.
- Conferma che gli aggiornamenti agli account esistenti siano stati applicati correttamente.

**Area funzionale:** Amministratore Adobe Commerce</br>
**Ruolo:** Amministratore, Associato archivio</br>
**Tipo di test:** Tutti positivi

<table style="table-layout:auto">
<tr>
<th>Funzione</th>
<th>Scenario</th>
<th>Risultati previsti</th>
</tr>
<tr>
<td><strong>Gestione account utente - Crea account</strong></br></br>
</td>
<td>
<ol>
<li><strong>Amministratore</strong> — Accedi all'amministratore Adobe Commerce</li>
<li>Vai a <strong>[!UICONTROL System] &gt; Autorizzazioni app di esecuzione store &gt; Tutti gli utenti app di esecuzione store</strong></li>
<li><strong>Aggiungi nuovo utente.</strong></li>
</ol>
<td>
<ul>
<li>Account creato correttamente.</li>
<li>Il nuovo account utente viene visualizzato nel dashboard [!UICONTROL Store Fulfillment Users].</li>
<li><strong>Associate store</strong> accedi all'app Store Assist con il nuovo account utente.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Gestione account utente - Aggiorna account utente esistente</strong>
</td>
<td>
<ol>
<li>Accedi ad Adobe Commerce Admin con l’account utente Admin.</li>
<li>Vai a <strong>[!UICONTROL System] &gt; Autorizzazioni app di esecuzione store &gt; Tutti gli utenti app di esecuzione store</strong>.</li>
<li>Nell'elenco Account utente aprire un account utente attivo esistente selezionando <strong>[!UICONTROL Edit]</strong>.
<li>Disattivare l'account modificando <strong>[!UICONTROL Is Active]</strong> in <strong>No</strong>.</li>
</ol>
</td>
<td>
<ul>
<li>Nel dashboard <strong>[!UICONTROL Store Fulfillment App Users]</strong> lo stato dell'account aggiornato è cambiato in <strong>[!UICONTROL Inactive]</strong>.</li>
<li>Associate store: impossibile accedere all'app Store Assist con le credenziali dell'account inattive.</li>
</ul>
</td>
</tr>
</table>

## Tipi di prodotti Adobe Commerce

Gli scenari di test per i tipi di prodotto Adobe Commerce verificano che i clienti visualizzino le informazioni corrette su prodotto, scorte e metodo di consegna per i diversi tipi di prodotto:

- [!UICONTROL Configurable]
- [!UICONTROL Grouped]
- [!UICONTROL Virtual]
- [!UICONTROL Bundle products] nella vetrina di Adobe Commerce.

**Area funzionale:** Adobe Commerce Frontend</br>
**Ruolo:** Utente App Di Assistenza Store (Associato Store)</br>
**Tipo di test:** Tutti positivi

<table style="table-layout:auto">
<tr>
<th>Funzione</th>
<th>Scenario</th>
<th>Commenti</th>
</tr>
<tr>
<td><strong>Prodotti configurabili</strong>
</td>
<td>
<ul>
<li>Verificare che l'utente sia in grado di visualizzare solo le opzioni configurabili, che l'origine sia abilitata, che il materiale sia assegnato e che vi siano alcuni articoli in magazzino. Controllare i prodotti secondari.</li>
<li>Verifica che, quando selezioni un archivio diverso, le opzioni non disponibili vengano visualizzate come barrate.</li>
<li>Verifica che, se l’utente seleziona un archivio diverso, le opzioni configurabili non siano selezionate.</li>
<li>Verifica che, se un prodotto configurabile è già nel carrello e un utente seleziona un altro store, il prodotto venga visualizzato come esaurito.</li>
</ul>
</td>
<td></td>
</td>
</tr>
<tr>
<td><strong>Prodotti raggruppati</strong>
</td>
<td>
<ul>
<li>Verificare che i metodi di consegna e il pulsante [!UICONTROL Add to cart] siano disabilitati per il cliente quando tutti i prodotti secondari hanno
<code>qty</code> impostato su <code>0</code>.</li>
<li>Verificare che i metodi di consegna siano abilitati per il cliente quando almeno uno dei prodotti secondari ha <code>qty</code> impostato su <code>0.</code></li>
<li>Verificare che il metodo [!UICONTROL Store Pickup Delivery] sia visibile e attivo solo per i prodotti in cui è abilitato [!UICONTROL Available for Store Pickup]. (Controlla prodotto secondario).</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td><strong>Prodotti virtuali</strong>
</td>
<td>
Verificare che i prodotti virtuali non offrano il metodo di consegna [!UICONTROL In-store Pickup].
<td></td>
</td>
</tr>
<tr>
<td><strong>Prodotti del bundle</strong>
</td>
<td>
<ul>
<li>Verificare che se almeno un prodotto secondario ha disabilitato [!UICONTROL Available for Store Pickup], l'opzione di consegna Ritiro da store non sia disponibile per il cliente.</li>
<li>Verificare che se almeno un prodotto secondario ha disabilitato [!UICONTROL Available for Home Delivery], l'opzione Consegna a domicilio non sia disponibile per il cliente.</li>
<li>Verifica se almeno uno dei prodotti secondari in un bundle è esaurito; viene visualizzato anche il bundle (prodotto principale)
come [!UICONTROL Out of stock].</li>
</ul>
</td>
<td></td>
</tr>
<tbody>
</table>

## Esperienza di check-in

Questa sezione del piano di test riguarda l&#39;esperienza di check-in per gli ordini di ritiro dal negozio per le seguenti funzionalità:

- Contatto di prelievo alternativo: verificare il flusso di lavoro per l&#39;aggiunta di un [!UICONTROL Alternate Pickup Contact] e la selezione di un [!UICONTROL Preferred Contact] negli ordini di ritiro dello store.

- Modulo di check-in: verificare il flusso di lavoro per l&#39;invio di una richiesta di check-in per gli ordini di prelievo del Negozio.

**Aree funzionali:** Cart Checkout, Modulo di check-in per ordini di ritiro dal magazzino</br>
**Ruolo:** Amministratore, Cliente, Associato Store</br>
**Tipo di test:** Tutti positivi

### Contatto di ritiro alternativo


**Area funzionale:** Cart Checkout</br>
**Ruolo:** Cliente</br>
**Tipo di test:** Tutti positivi

<table style="table-layout:auto">
<tr>
<th>Funzione</th>
<th>Scenario</th>
<th>Risultati previsti</th>
</tr>
<tr>
<td><strong>Contatto ritiro alternativo</br>
Check-in<strong>
</td>
<td>
Un cliente invia un ordine con l’opzione di ritiro in-store.</td>
<td>Durante il processo di pagamento, il cliente visualizza l'opzione [!UICONTROL Alternate Pickup Contact] nella fase di spedizione.
</td>
</tr>
<tr>
<td><strong>Contatto preferito per ritiro alternativo, Archivia</strong>
<td>
Un cliente invia un ordine con l’opzione di ritiro in-store. Durante il pagamento, il cliente aggiunge un [!UICONTROL Alternate Pickup Contact].</td>
<td>Durante il processo di pagamento, il cliente visualizza l'opzione [!UICONTROL Preferred Contact] nella fase di spedizione.</td>
</td>
</tr>
<tr>
<td><strong>Dettagli di contatto per il ritiro alternativo, Archivia</strong>
</td>
<td>
Un cliente invia un ordine con l’opzione di ritiro in-store. Durante il pagamento, il cliente seleziona [!UICONTROL Alternate Pickup Contact] nella fase di spedizione.
</td>
<td>Il cliente visualizza le opzioni di input per immettere i dettagli di contatto: [!UICONTROL First name], [!UICONTROL Last name], [!UICONTROL Phone] e [!UICONTROL Email].</td>
</tr>
<tr>
<td><strong>Ritiro alternativo, Archivia e-mail</strong>
</td>
<td>Un cliente invia un ordine con l’opzione di ritiro in-store. Durante il pagamento, il cliente seleziona [!UICONTROL Alternate Pickup Contact] nella fase di spedizione, aggiunge i dettagli di contatto e invia l'ordine.</td>
<td>Sia il cliente che il contatto alternativo ricevono un'e-mail di check-in per l'ordine.</td>
</tr>
<td><strong>Prelievo alternativo, dettagli ordine</strong></td>
<td>Un cliente invia un ordine con l’opzione di ritiro in-store. Durante il pagamento, il cliente seleziona [!UICONTROL Alternate Pickup Contact] nella fase di spedizione, aggiunge i dettagli di contatto e invia l'ordine.</td>
<td>L’amministratore visualizza le informazioni di contatto aggiuntive sull’ordine salvato.</td>
</tr>
<tr>
<td><strong>Contatto di ritiro alternativo, visualizzazione ordine associato archivio</strong>
</td>
<td>Un cliente invia un ordine con l’opzione di ritiro in-store. Durante il pagamento, il cliente seleziona [!UICONTROL Alternate Pickup Contact] nella fase di spedizione, aggiunge i dettagli di contatto e invia l'ordine.</td>
<td>L’Associate store può visualizzare le informazioni di contatto aggiuntive sull’ordine in FaaS/ChaaS.</td>
</td>
</tr>
</tbody>
</table>

### Modulo di archiviazione


**Area funzionale:** Modulo di archiviazione</br>
**Ruolo:** Cliente</br>
**Tipo di test:** Tutti positivi

<table style="table-layout:auto">
<tr>
<th>Funzione</th>
<th>Scenario</th>
<th>Risultati previsti</th>
</tr>
<tr>
<td><strong>Archivia azione - Invia richiesta</strong>
</td>
<td>Nel modulo di archiviazione, il cliente compila tutti i campi obbligatori e invia la richiesta.</td>
<td>Il cliente riceve una risposta di successo.</td>
</tr>
<tr>
<td><strong>Azione check-in: visualizza i dettagli della richiesta</strong></td>
<td>Un cliente invia correttamente una richiesta di archiviazione.</td>
<td>Gli aggiornamenti dello stato dell’ordine nel sistema FaaS e l’Associato store possono visualizzare i dettagli della richiesta di archiviazione nel FaaS.
</td>
</tr>
<tr>
<td><strong>Azione Check-in: invia richiesta una sola volta</strong></td>
<td>Dopo aver inviato una richiesta di check-in per un ordine, il cliente seleziona nuovamente il link per il check-in.</td>
<td>Nel modulo di archiviazione, il cliente non visualizza un'opzione per modificare o inviare nuovamente il modulo.</td>
</tr>
<tr>
<td><strong>Azione check-in: conferma arrivo</strong></td>
<td>Un ordine di prelievo in-store è contrassegnato come pronto per il prelievo nella FaaS. Il cliente riceve un'e-mail pronta per il ritiro e seleziona [!UICONTROL Confirm Arrival].</td>
<td>Il cliente visualizza il modulo di check-in per l'ordine.</td>
</tr>
</tbody>
</table>

## App Store Assist

Questa sezione del piano di test descrive gli scenari per i flussi di lavoro di verifica ordine, prelievo e handoff nell’app Store Assist.

**Area funzionale:** app di assistenza per lo store</br>
**Ruolo:** Associato archivio</br>
**Tipo di test:** Tutti positivi

<table style="table-layout:auto">
<tr>
<th>Funzione</th>
<th>Scenario</th>
<th>Risultati previsti</th>
</tr>
<tr>
<td>
<strong>Prelievo singolo ordine—percorso felice, prelievo a bordo strada</strong></td>
<td>Selezionare articoli singoli e con più quantità. Nessun prelievo nullo e prelievo a bordo campo (con staging).
</td>
<td>
</td>
</tr>
<tr>
<td><strong>Prelievo di più ordini: percorso felice, prelievo a bordo strada</strong></td>
<td>Articoli singoli e multi-quantità. Nessun prelievo nullo e prelievo a bordo campo (con staging)</td>
<td></td>
</tr>
<tr>
<td><strong>Ritiro per singolo ordine: prelievo in negozio percorso felice</strong></td>
<td>Articoli singoli e multi-quantità. Nessun prelievo nulla e ritiro in negozio (con staging)</td>
<td>
</td>
</tr>
<tr>
<td><strong>Prelievo di più ordini: percorso felice, prelievo in negozio</strong></td>
<td>Selezionare articoli singoli e con più quantità. Nessun prelievo nullo e prelievo a bordo campo (con staging).</td>
<td></td>
</tr>
<tr>
<td><strong>Prelievo di un singolo ordine: percorso non felice, prelievo in negozio</strong></td>
<td>Prelievo di articoli in quantità singola e multipla con prelievo parziale e nilpick e in-store (con staging)</td>
</td>
<td></td>
</tr>
<td><strong>Prelievo di più ordini: prelievo a terra non felice</strong></td>
<td>Prelievo di articoli in quantità singola e multipla con prelievo parziale e nilpick e in-store (con staging)</td>
<td></td>
</tr>
<td><strong>Prelievo ordine singolo: percorso non felice, prelievo a bordo strada</strong></td>
<td>Prelievo di articoli singoli e di più quantità con prelievo parziale e nilpick e a blocchi (con staging)</strong></td>
</td>
<td></td>
</tr>
<tr><td><strong>Ordine effettuato - Annullato prima del prelievo</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Ordine effettuato - Annullato prima della consegna</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Ordine effettuato: ricerca nel modulo dell’ordine</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Ordine effettuato: ricerca e check-in manuale per il trasferimento</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Ordine effettuato: tutti gli articoli prelevati in modo non corretto o non disponibili contrassegnati dal selettore</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Ordine effettuato con articoli bundle - prelievo e handoff</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Ordine effettuato - Mano spenta con rifiuto</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Ordine effettuato - Mano a mano con rifiuto di tutti gli articoli</strong></td>
<td></td>
<td></td></tr>
</tbody>
</table>

## Distribuisci

Dopo aver verificato che la soluzione sia stata configurata e testata in base alle specifiche, puoi procedere alla distribuzione dalla staging alla produzione.

L’implementazione e i test variano a seconda dell’infrastruttura e delle funzionalità.

>[!TIP]
>
>Per le linee guida per la distribuzione, gli elenchi di controllo e le best practice per Adobe Commerce sui progetti di infrastruttura cloud, consulta [Distribuire l&#39;archivio](https://experienceleague.adobe.com/it/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production) nella documentazione per sviluppatori di Adobe Commerce.
