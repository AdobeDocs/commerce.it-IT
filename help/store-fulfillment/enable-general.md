---
title: Configurazione generale
description: Configura le impostazioni generali per abilitare  [!DNL Store Fulfillment]  per il tuo archivio. Configura le impostazioni globali dell'estensione, le impostazioni di sistema per la registrazione, la sincronizzazione dei dati e la sicurezza. Fornisci dati chiave per abilitare l’integrazione tra Adobe Commerce e i servizi di Store Fulfillment.
role: Admin
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 0%

---

# Servizio store e configurazione vendite

Abilita l&#39;estensione [!DNL Store Fulfillment] dall&#39;amministratore [!DNL Commerce] configurando le impostazioni dell&#39;estensione, le impostazioni di sicurezza per gli utenti dell&#39;app Store Assist e le opzioni del metodo di consegna.

>[!IMPORTANT]
>
>La configurazione del servizio Store Fulfillment viene applicata solo dopo la connessione dell&#39;istanza di Adobe Commerce e dell&#39;app [!DNL Store Fulfillment]. Vedi [Connessione a esecuzione archivio](connect-set-up-service.md).

## Gestisci impostazioni servizi di evasione negozio

Consente di gestire le impostazioni per i servizi di Store Fulfillment dal menu [!DNL Commerce Admin Store Configuration].

- Abilitare l&#39;estensione, configurare le impostazioni globali e specificare le opzioni di protezione per le connessioni e gli account utente dell&#39;app Store Assist selezionando **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**.

  ![Configurazione servizi archivio di amministrazione per il completamento dell&#39;archivio](assets/store-services-admin-sf-config.png)

- Configurare i metodi di consegna selezionando **[!UICONTROL Store > Configuration > Sales > Delivery Methods > In-Store Pickup]**.

  ![Configurazione vendite archivio amministrazione per il completamento dello store](assets/store-sales-admin-sf-deliver-config.png)

## Impostazioni di base

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Price]</strong></td>
<td>Il prezzo addebitato al cliente per il ritiro in negozio. Il valore predefinito è zero.</td>
<td>Sito Web</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Search Radius]</strong></td>
<td>Il raggio, in chilometri, da utilizzare quando un acquirente cerca un punto di ritiro nel negozio checkout. I risultati della ricerca restituiscono solo gli archivi che si trovano entro il raggio di ricerca specificato.</td>
<td>Sito Web</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Displayed error message]</strong></td>
<td>Messaggio visualizzato quando un cliente seleziona un prelievo in-store per un articolo non disponibile per il prelievo in-store. Se necessario, è possibile personalizzare il testo predefinito.
</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</tbody>
</table>

>[!NOTE]
>
>L&#39;impostazione [!UICONTROL Search Radius] viene utilizzata solo se hai configurato l&#39;impostazione [percorso archivio e mappatura](store-location-map-provider-setup.md) per Adobe Commerce.

## Abilitare la soluzione di evasione del punto vendita

Abilita la soluzione [!DNL Store Fulfillment] per aggiungere le funzionalità di prelievo in-store e curbside alle esperienze di acquisto e pagamento nella tua vetrina Adobe Commerce.

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enabled]</strong></td>
<td>Attiva o disattiva la soluzione. Quando è abilitata, configura e utilizza le funzionalità di Store Fulfillment e stabilisce la connessione tra il tuo archivio Adobe Commerce e i servizi [!DNL Store Fulfillment]. Quando è disabilitata, tutte le funzioni di Store Fulfillment sono disabilitate e non vi è alcuna comunicazione tra Adobe Commerce e i servizi di Store Fulfillment. Impossibile elaborare o ricevere informazioni sull'ordine.</td>
<td>Sito Web</td>
<td>Sì</td>
</tr>
</tbody>
</table>

## Aggiungi credenziali account

<table>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Environment]</strong></td>
<td>Selezionare <i>[!UICONTROL Sandbox]</i> o <i>[!UICONTROL Production]</i><br></br>Selezionando [!UICONTROL Sandbox] si abilita la comunicazione con i servizi di evasione in un ambiente di test.<br></br>Selezionando [!UICONTROL Production] si abilita la comunicazione con i servizi di evasione in un ambiente live.<br></br>È stato assegnato un set di credenziali per ogni ambiente ed è possibile gestire entrambi i set nella stessa installazione. <br></br>Salvare le credenziali prima di convalidare la connessione.</td>
<td>Globale</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL API Server URL]</strong></td>
<td>URL dell'endpoint API di evasione del negozio Walmart. Il valore deve essere l’URL completo fornito durante il processo di onboarding. I clienti Store Fulfillment ricevono sia un URL sandbox che un URL di produzione. Quando aggiungi i valori, accertati di copiare e incollare l’URL completo, inclusa la barra "/" finale.</td>
<td>Globale</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Token Auth Server URL]</strong></td>
<td>L'URL dell'endpoint di autenticazione di evasione del negozio Walmart. Il valore deve essere l’URL completo fornito durante il processo di onboarding. Ricevi sia una sandbox che un URL di produzione. Quando aggiungi i valori, accertati di copiare e incollare l’URL completo, inclusa la barra "/" finale.</td>
<td>Globale</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Merchant Id]</strong></td>
<td>L’ID univoco del venditore (tenant) fornito durante il processo di onboarding. Questo ID viene utilizzato per instradare gli ordini in modo che i negozi di esercenti li ricevano.</td>
<td>Globale</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Id]</strong></td>
<td>ID di integrazione univoco fornito durante il processo di onboarding. Questo ID viene utilizzato per autenticare tutte le comunicazioni tra Adobe Commerce e i servizi di evasione store</td>
<td>Globale</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Secret]</strong></td>
<td>Chiave di integrazione univoca fornita durante il processo di onboarding. Questa chiave viene utilizzata per autenticare tutte le comunicazioni tra Adobe Commerce e il servizio di evasione store.</td>
<td>Globale</td>
<td>Sì</td>
</tr>
</table>

Dopo aver configurato [!UICONTROL Account Credentials], selezionare <strong>[!UICONTROL Validate Credentials]</strong> per verificare e stabilire una connessione al servizio di evasione dell&#39;archivio per la prima volta.

## Configurare la registrazione

I registri per i servizi di evasione archivi sono disponibili nel file di registro `var/log/walmart-bopis.log`.

Chiedere all&#39;amministratore di sistema di configurare gli ambienti per consentire la gestione delle eccezioni in modo che le eccezioni relative alle API possano essere acquisite tramite il firewall o la cache.

Poiché il file di registro dell&#39;applicazione può crescere rapidamente, abilitare la registrazione per l&#39;applicazione solo per un breve periodo di tempo quando necessario, ad esempio durante la risoluzione dei problemi di evasione dell&#39;archivio per un ordine [!DNL Commerce]. Questa configurazione evita problemi di tempo di risposta negli ambienti di produzione causati da file di registro di grandi dimensioni.

>[!TIP]
>
>Per le installazioni locali di Adobe Commerce, chiedere all&#39;amministratore di sistema di impostare la rotazione del registro per il file `var/log/walmart-bopis.log` per ridurre al minimo le dimensioni. Per le installazioni locali di Adobe Commerce, vedere [Rotazione del registro](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings) nella _Guida all&#39;installazione di Adobe Commerce_. Per i progetti Adobe Commerce su infrastrutture cloud, consulta [Visualizzare e gestire i registri](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html).

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Debug Mode]</strong></td>
<td>La modalità di debug viene utilizzata per aumentare l’attività registrata all’interno dell’integrazione. Se l'opzione è disabilitata, non vengono registrate informazioni di debug. Quando questa opzione è attivata, tutte le informazioni di debug vengono registrate <br></br>Tutti i dati registrati si trovano nel file: <pre>var/log/walmart-bopis.log</pre>
<td>Globale</td>
<td>No</td>
</tr>
</tbody>
</table>

## Gestire la sincronizzazione degli ordini

Configura le impostazioni per gestire la gestione degli errori per la sincronizzazione degli ordini, gli attributi del catalogo da utilizzare per la scansione del codice a barre durante il prelievo degli ordini e configura le dimensioni dei batch di ordini per la coda di evasione del punto vendita.

È possibile visualizzare i dettagli relativi alle operazioni di sincronizzazione degli ordini dal dashboard Gestione coda evasione archivio in Amministrazione (
<strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong>).

### Gestione degli errori di sincronizzazione

<table>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Retry Critical Error]</strong></td>
<td>Specifica i nuovi tentativi per un'operazione di sincronizzazione dei record dopo un errore critico.<br></br>Gli errori critici si verificano ogni volta che l'integrazione non riceve una risposta positiva dal servizio di evasione. Questi problemi si verificano quando il servizio è inattivo o quando si verifica un errore nell’invio dei dati dell’ordine.<br></br>Quando viene raggiunta la soglia dei tentativi, l'elemento rimane in coda ma non viene elaborato di nuovo. Visualizza tutti gli elementi con errori della gestione <strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong> nell'amministratore. Per risolvere i problemi relativi agli elementi con errori sistematici, contatta il tuo Account Manager.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Error Notification Email]</strong></td>
<td>Abilita le notifiche di errore per ricevere un'e-mail quando viene raggiunto [!UICONTROL Retry Critical Error Threshold] per un ordine. La notifica include tutti i dettagli disponibili sull’errore.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Send Error Notification Email To]</strong></td>
<td>Un elenco delimitato da virgole di indirizzi e-mail dei destinatari per le notifiche di errore.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Order Sync Exception Email Template]</strong></td>
<td>Specifica il modello e-mail utilizzato per notificare ai destinatari gli errori di sincronizzazione degli ordini. Viene fornito un modello predefinito. Non supporta la personalizzazione.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</table>

### Sincronizzazione ordine

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Barcode Source]</strong></td>
<td>Attributo del catalogo che memorizza il codice analizzabile per gli elementi corrispondenti nelle posizioni dell'esercente.<br></br>Se disponi di una sola località per esercenti, è probabile che tu utilizzi codici UPC, mentre il tuo canale di e-commerce identifica i prodotti in base allo SKU. In questo scenario, seleziona l’attributo di catalogo contenente il codice UPC.<br></br>Questa impostazione garantisce che gli ordini inviati ai tuoi negozi elencino le voci con l'identificatore corretto, in modo che i soci del negozio possano analizzare con precisione le voci durante il processo di prelievo.<br></br>Se non si è sicuri, rivolgersi ai responsabili evasione nel reparto Spedizione e prelievo per determinare l'attributo da inviare. Se l’attributo non è attualmente incluso nel database, puoi aggiungerlo al set di attributi del prodotto Adobe Commerce.</td>
<td>Sito Web</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Barcode Type]</strong></td>
<td>Attributo di catalogo che memorizza l'origine del codice a barre per gli articoli corrispondenti nelle posizioni dell'esercente.<br></br>Questa impostazione garantisce che gli ordini inviati ai tuoi negozi elencino le voci con l'identificatore corretto, in modo che i soci del negozio possano analizzare con precisione le voci durante il processo di prelievo. Le opzioni includono: SKU, UPC, GTIN, UPCA, EAN13, UPCE0, DISA, UAB, CODABAR, Price Embedded UPC.<br></br>In caso di dubbi, selezionare l'opzione che assomiglia maggiormente ai valori contenuti nell'attributo [!UICONTROL Barcode Source]. Gli assegnatari del Negozio possono comunque far corrispondere gli articoli manualmente dalla lista di prelievo.</td>
<td>Sito Web</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Max Number of Items]</strong></td>
<td>Numero massimo di elementi da inviare dalla coda di evasione dell'archivio contemporaneamente.<br></br>Gli ordini BOPIS vengono inviati al servizio di evasione in batch, a intervalli regolari. Questa impostazione consente di controllare le dimensioni del batch.<br></br>Il valore predefinito è 100 elementi. A seconda del volume e della capacità dell’ordine, puoi aumentare o diminuire il valore massimo.</td>
<td>Globale</td>
<td>No</td>
</tr>
</tbody>
</table>

## Abilita opzioni di spedizione evasione negozio

Configura le opzioni di spedizione Store Fulfillment che determinano la disponibilità delle opzioni di ritiro in-store e consegna a domicilio per i tuoi store Adobe Commerce.

### Spedisci al negozio

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship To Store]</strong></td>
<td>L'impostazione di spedizione al punto vendita si basa sulle funzionalità di spedizione al punto vendita esistenti. Se utilizzi Inventory management, o se puoi accettare ed evadere ordini presso sedi di esercenti senza scorte tramite trasferimenti di scorte da negozio a negozio, imposta questa opzione su "Sì".<br></br>Se non è possibile supportare l'opzione di spedizione allo store o non si desidera offrirla, impostare su 'No'. Se l'opzione è disabilitata, gli articoli del catalogo con inventario pari a zero per un punto vendita o quelli al di sotto di [!DNL Out of Stock Threshold] per tale ubicazione non vengono offerti con le opzioni di prelievo in-store.<br></br>È possibile regolare il valore di questa impostazione in base alla posizione dell'esercente.</td>
<td>Globale</td>
<td>No</td>
</tr>
</tbody>
</table>

### Spedisci da store

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></td>
<td>Abilita o disabilita l’opzione Consegna a domicilio nei negozi dei tuoi esercenti. Se questa opzione è abilitata, le posizioni dei negozi di esercenti vengono considerate in forma aggregata con altre origini assegnate nelle scorte associate al sito Web.<br></br>Nei servizi Inventory management standard, l'opzione [!DNL Ship from Store] è intrinseca e non può essere disabilitata. Con la soluzione Store Fulfillment è possibile attivarla o disattivarla.<br></br>È possibile regolare questa impostazione in base alla posizione e al prodotto dell'esercente.</td>
<td>Globale</td>
<td>No</td>
</tr>
</tbody>
</table>


## Gestione account e autorizzazioni di utilizzo dell&#39;app Store Fulfillment

Configura le impostazioni per l’account utente e la sicurezza della password dell’app Store Fulfillment e per l’autenticazione a due fattori.

### Sicurezza delle app

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL User Session Lifetime]</strong></td>
<td>Intervallo di tempo, in secondi, in cui una sessione utente associata all'archivio rimane attiva prima della disconnessione automatica. I valori validi sono compresi tra 60 e 31536000.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Maximum Login Failures to Lockout Account]</strong></td>
<td>Specifica il numero di tentativi di accesso non riusciti consentiti prima che un associato archivio venga bloccato dal proprio account.<br></br>Per disattivare il blocco account, impostare il valore su 0.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Lockout Time (minutes)]</strong></td>
<td>Numero di minuti per bloccare un account dopo un errore di accesso.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Force Password Change]</strong></td>
<td><em>[!UICONTROL Yes]</em>: richiedi all’utente di modificare la password dopo la configurazione dell’account.<br></br><em>[!UICONTROL No]</em>: consiglia all'utente di modificare la password dopo la configurazione dell'account.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Password Lifetime]</strong></td>
<td>Il numero di giorni in cui una password rimane valida prima della modifica richiesta. Lascia vuoto per disabilitare questa opzione.</td>
<td>Globale</td>
<td>No</td>
</tr>
</tbody>
</table>

## Metodi di consegna

Store Fulfillment funziona estendendo le funzionalità native di Adobe Commerce [!DNL In-Store Delivery]. Dopo aver installato l’estensione, puoi configurare i metodi di consegna in-store utilizzando le seguenti impostazioni estese aggiunte all’amministratore.

- **Ritiro in negozio**—Opzioni di offerta per la consegna in negozio durante il processo di pagamento
Queste impostazioni configurano gli scenari di consegna più comuni per gli ordini BOPIS.

- **[!UICONTROL Curbside pick up]** - Opzioni di offerta per i clienti per parcheggiare in un punto vendita e far consegnare l&#39;ordine da un associato del negozio.

Configurare queste impostazioni dall&#39;amministratore selezionando <strong>[!UICONTROL Stores > Configuration > Sales > Delivery Methods > In-Store Pickup]</strong>.

>[!NOTE]
>
>Per ulteriori informazioni sulla configurazione delle opzioni di consegna in-store, vedi [Consegna in-store](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/basic-methods/shipping-in-store-delivery) nella _Guida utente di Adobe Commerce_.


### Configurazione dei metodi di consegna

Con il metodo di consegna in-store, il cliente può selezionare un’origine da utilizzare come luogo di prelievo durante il pagamento.

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrizione</strong></td>
<td><strong>Ambito</strong></td>
<td><strong>Obbligatorio</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enable In-Store Pickup]</strong></td>
<td>Attiva o disattiva l'opzione di prelievo in negozio disponibile durante il pagamento per i clienti che scelgono il prelievo in negozio. Quando il ritiro in-store è disattivato, l’opzione non viene visualizzata.<br></br>Questa impostazione globale si applica a tutte le posizioni del punto vendita al dettaglio. Se questa opzione è abilitata, puoi disabilitarla selettivamente nel punto vendita al dettaglio.</td>
<td>Sito Web</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Curbside Pickup]</strong></td>
<td>Abilita o disabilita l'opzione di ritiro a blocchi durante il processo di pagamento per i clienti che scelgono il ritiro dal negozio.<br></br>Questa impostazione globale si applica a tutte le posizioni del punto vendita al dettaglio. Se questa opzione è abilitata, puoi disabilitarla selettivamente nel punto vendita al dettaglio.</td>
<td>Sito Web</td>
<td>No</td>
</tr>
</tbody>
</table>

### Configurazione del titolo del metodo di consegna

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrizione</strong></th>
<th><strong>Ambito</strong></th>
<th><strong>Obbligatorio</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Titolo consegna a domicilio</strong></td>
<td>Specifica il titolo da visualizzare per l’opzione Consegna a domicilio nelle aree prodotto, carrello e pagamento. La consegna a domicilio si riferisce alle funzionalità di spedizione standard di Adobe Commerce, da un magazzino, da un vettore o direttamente all’indirizzo di spedizione fornito dal cliente. </br></br>Questa etichetta non influisce sulle etichette del metodo di spedizione per il vettore di spedizione selezionato.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Descrizione consegna a domicilio</strong></td>
<td>Una descrizione facoltativa che viene visualizzata ogni volta che il Titolo consegna Home viene mostrato ai clienti. Nella maggior parte dei casi, la descrizione è un messaggio statico per comunicare le promesse di consegna. Alcuni esempi:</br><code>Same-day shipping on orders by 4</code></br></br><code>Ships within 2 business days</code></td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Titolo ritiro store</strong></td>
<td>Quando a un cliente vengono presentate le opzioni di consegna e il ritiro in-store è disponibile, viene mostrata questa etichetta. </br></br>Puoi personalizzare questa etichetta, che viene visualizzata nelle aree prodotto, carrello e pagamento.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<td><strong>Descrizione ritiro store</strong></td>
<td>Ovunque sia visualizzato il Titolo ritiro dal negozio, puoi facoltativamente includere una descrizione. Questo messaggio statico consente di migliorare le comunicazioni con i clienti relative all’esperienza di ritiro dal negozio. Alcuni esempi:</br></br><code>Get it today for free!</code></br></br><code>Ready for pickup in an hour!</code></td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Titolo ritiro in-store</strong></td>
<td>Quando In-Store Pickup è abilitato, questo titolo viene mostrato ai clienti come opzione di consegna Pickup store. Puoi personalizzarne l’etichetta.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<tr>
<td><strong>Titolo per ritiro Curbside</strong></td>
<td>Quando Curbside Pickup è abilitato, l’opzione viene mostrata ai clienti come un tipo di opzione di consegna Pickup store. Puoi personalizzarne l’etichetta qui.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Istruzioni per il ritiro in-store</strong></td>
<td>Quando un ordine è pronto per essere ritirato presso i punti vendita, il cliente riceve una notifica via e-mail. Se il cliente ha selezionato [!DNL In-Store Pickup] durante il pagamento, è possibile personalizzare le istruzioni di prelievo qui. </br></br>Queste istruzioni sono impostate a livello globale e si applicano a tutte le posizioni dei negozi al dettaglio. È inoltre possibile personalizzare le istruzioni a livello di punto vendita al dettaglio.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Istruzioni per il ritiro di Curbside</strong></td>
<td>Specifica le istruzioni personalizzate di prelievo degli ordini da includere nelle notifiche e-mail dei clienti per gli ordini di prelievo a blocchi. </br></br>Queste istruzioni sono impostate a livello globale e si applicano a tutte le posizioni dei negozi al dettaglio. È inoltre possibile personalizzare le istruzioni a livello di punto vendita al dettaglio.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Lead time di prelievo stimato</strong></td>
<td>Il numero di minuti necessari prima che un ordine venga ricevuto, evaso e pronto per essere ritirato. Queste informazioni vengono mostrate al cliente quando si seleziona un punto vendita al dettaglio per l'opzione di consegna Ritiro dal negozio. Questa impostazione si applica a tutte le posizioni del punto vendita al dettaglio. Puoi anche personalizzare il lead time a livello di punto vendita al dettaglio.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Etichetta tempo di ritiro stimato</strong></td>
<td>Visualizza il tempo stimato fino al momento in cui un ordine è disponibile per il prelievo del cliente. Queste informazioni vengono mostrate ai clienti quando selezionano una posizione del negozio al dettaglio per l'opzione di consegna [!DNL In-Store Pickup]. </br></br>Quando si personalizza questa etichetta, è possibile utilizzare il codice <code>%1</code> per inserire il <strong>lead time di prelievo stimato</strong>. Ad esempio:</br></br><code>Ready for Pickup in %1 minutes.</code></br></br>Questa impostazione si applica a tutte le posizioni del punto vendita al dettaglio. Puoi anche personalizzare il lead time a livello di punto vendita al dettaglio.</td>
<td>Visualizzazione store</td>
<td>No</td>
<tr>
<td><strong>Esclusione di responsabilità per tempo di prelievo</strong></td>
<td>Il contenuto visualizzato nella pagina del prodotto nella descrizione comando che elenca le ore del negozio, le festività, le chiusure impreviste e così via</td>
<td>Visualizzazione store
</td>
<td>No
</td>
</tr>
</tbody></table>

### Configurazione titoli disponibilità Stock

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrizione</strong></th>
<th><strong>Ambito</strong></th>
<th><strong>Obbligatorio</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>In magazzino</strong></td>
<td>Quando un cliente utilizza la collocazione del punto vendita al dettaglio, per ogni ubicazione viene visualizzata la disponibilità di magazzino per gli articoli correnti. </br></br>È possibile personalizzare l'etichetta di stato <em>[!UICONTROL in-stock]</em> qui.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Esaurito</strong></td>
<td>Quando un cliente utilizza la collocazione del punto vendita al dettaglio, per ogni ubicazione viene visualizzata la disponibilità di magazzino per gli articoli correnti.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Parzialmente in magazzino</strong></td>
<td>Quando un cliente utilizza la collocazione del punto vendita al dettaglio, viene visualizzata la disponibilità di magazzino per tutti gli articoli correnti per ogni ubicazione. </br></br>È possibile personalizzare l'etichetta di stato <em>[!UICONTROL partially in-stock]</em> qui.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</tbody></table>

