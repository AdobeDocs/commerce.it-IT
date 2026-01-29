---
title: Migrazione dalla scheda di ricerca al widget PLP
description: Scopri come migrare dalla scheda di ricerca obsoleta al widget per pagina elenco prodotti  [!DNL Live Search] .
source-git-commit: 8811f0f271928fbc827e5a0164542da473c57224
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 0%

---

# Migrazione dall&#39;adattatore di ricerca al widget PLP

La scheda di ricerca è stata [obsoleta](release-notes.md#live-search-400) a partire da [!DNL Live Search] 4.0.0 e riceverà solo gli aggiornamenti di sicurezza. Il widget [Product Listing Page (PLP)](plp-styling.md) è la soluzione supportata per tutte le [!DNL Live Search] implementazioni successive. Questa guida ti aiuta a capire quando la migrazione è semplice e quando è necessario un lavoro aggiuntivo.

## Prerequisiti

Prima di iniziare il processo di migrazione, assicurati che l’ambiente soddisfi questi requisiti.

Prima di avviare la migrazione:

**Requisiti tecnici**:

- Adobe Commerce 2.4.4 o versione successiva.
- Estensione [!DNL Live Search] installata.
- Accesso alla riga di comando (CLI).
- Accedi all’amministratore di Commerce.
- Ambiente di staging o controllo qualità per il test.

**Backup e preparazione**:

1. Eseguire il backup del database e del codice.
1. Documenta le personalizzazioni correnti.
1. Rivedi [Limiti e limiti](boundaries-limits.md) per assicurarti che il widget PLP soddisfi le tue esigenze.
1. Pianifica la migrazione durante un periodo di traffico ridotto.
1. Informa le parti interessate di potenziali modifiche al comportamento della vetrina.

**Verifica l&#39;implementazione corrente**:

- Verifica la versione [!DNL Live Search] corrente.
- Documenta i facet in uso e la relativa configurazione.
- Verifica tutte le funzionalità di ricerca e documenta i comportamenti previsti.
- Acquisisci schermate della presentazione corrente dei risultati di ricerca.

**Compatibilità versione**:

- Esecuzione di Adobe Commerce 2.4.4 o versione successiva.
- Aggiornamento a [!DNL Live Search] 4.0.0 o versione successiva.

## Scenari di migrazione

### Migrazione semplice (non richiede lavoro aggiuntivo)

Puoi eseguire direttamente la migrazione al widget PLP se l’implementazione soddisfa TUTTI i seguenti criteri:

**Vetrina standard basata su Luma**:

- Stai utilizzando il tema Luma o un tema che eredita da Luma con personalizzazioni minime.
- Non sono state apportate modifiche personalizzate ai layout o ai modelli PLP.
- Non sono state create estensioni JavaScript personalizzate che interagiscono con i risultati della ricerca.

**Catalogo prodotti standard**:

- Tutti gli attributi del prodotto utilizzano modelli sorgente standard (non modelli sorgente personalizzati).
- Non esistono tipi di prodotto personalizzati che richiedono una logica di rendering speciale.
- Il catalogo utilizza solo facet standard e filtri.

**Integrazioni standard**:

- Non utilizzi Google Tag Manager (GTM) per l’analisi.
- Non utilizzi estensioni di terze parti che modificano il comportamento di ricerca.

Se l&#39;implementazione soddisfa questi criteri, passare ai [passaggi di migrazione standard](#standard-migration-steps).

### Migrazione che richiede lavoro aggiuntivo

È necessario un lavoro aggiuntivo se l’implementazione presenta una delle seguenti caratteristiche:

**Modifiche tema personalizzato**:

- Layout PLP personalizzati che sostituiscono i modelli Luma.
- CSS o JavaScript personalizzato che esegue il targeting di elementi specifici dell&#39;adattatore di ricerca.
- Modifiche al modello personalizzato apportate a PLP o a file correlati.
- Il tema non eredita da Luma (ad esempio, il tema personalizzato viene creato da zero).

**Attributi di prodotto personalizzati**:

- Attributi del prodotto con modelli di origine personalizzati utilizzati come facet.
- Tipi di prodotto personalizzati con requisiti di visualizzazione speciali.
- Attributi programmatici con `"is_user_defined": false`.

**Integrazioni avanzate**:

- Google Tag Manager (GTM) viene utilizzato attivamente per il tracciamento.
- Strumenti di analisi o personalizzazione di terze parti integrati con la ricerca.
- Tracciamento degli eventi personalizzato o implementazione del livello dati.
- Integrazione con motori di ricerca o consigli esterni.

**Implementazioni headless o PWA**:

- Utilizzo di un’architettura headless (ad esempio, PWA Studio, Vue Storefront).
- Framework front-end personalizzato (React, Vue, Angular).
- Utilizzo di GraphQL esclusivamente per le query di catalogo.
- Implementazione di eventi storefront personalizzati.

**Codice widget personalizzato**:

- Il codice dell&#39;adattatore di ricerca è stato personalizzato in precedenza.
- Hosting di versioni personalizzate dei widget sulla tua rete CDN.
- Estensioni JavaScript personalizzate per la funzionalità di ricerca.

Se l&#39;implementazione ha uno di questi scenari, vedi [Scenari di migrazione complessi](#complex-migration-scenarios).

## Passaggi di migrazione standard

Per le implementazioni senza personalizzazioni speciali, segui questi passaggi:

### Passaggio 1: aggiornare [!DNL Live Search]

Aggiorna l&#39;estensione [!DNL Live Search] alla versione 4.0 o successiva per accedere al widget PLP.

**Ruolo**: commerciante o partner

1. Verifica la versione [!DNL Live Search] corrente:

   ```bash
   composer show magento/live-search | grep version
   ```

1. Se nella versione 3.x o precedente, abilitare il modulo AdvancedSearch prima dell&#39;aggiornamento:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

1. Aggiorna `composer.json` per richiedere [!DNL Live Search] versione 4.0 o successiva:

   ```json
   "require": {
      "magento/live-search": "^4.0"
   }
   ```

1. Esegui l’aggiornamento:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Eseguire l&#39;aggiornamento del programma di installazione e ricompilare:

   ```bash
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   ```

1. Se necessario, distribuire contenuto statico:

   ```bash
   bin/magento setup:static-content:deploy
   ```

### Passaggio 2: abilitare il widget PLP

Configurate il widget PLP in Commerce Admin.

**Ruolo**: commerciante

Il widget PLP è abilitato per impostazione predefinita per le nuove installazioni di [!DNL Live Search] 4.0.0+. Se si esegue l’aggiornamento da una versione precedente:

1. Vai a **[!UICONTROL Stores]** > Impostazioni > **[!UICONTROL Configuration]**.
1. Passa a **[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**.
1. Espandere la sezione **[!UICONTROL Storefront Features]**.
1. Imposta **[!UICONTROL Enable Product Listing Widgets]** su **Sì**.
1. Fare clic su **[!UICONTROL Save Config]**.
1. Svuota la cache: **[!UICONTROL System]** > Strumenti > **[!UICONTROL Cache Management]** > **[!UICONTROL Flush Magento Cache]**.

### Passaggio 3: test sullo staging

Convalida la migrazione in un ambiente non di produzione prima di andare &quot;live&quot;.

**Ruolo**: commerciante/partner

Prima di implementare in produzione, verifica accuratamente la funzionalità di ricerca:

**Test funzionali**:

- Verifica che i risultati della ricerca vengano visualizzati correttamente.
- Verifica tutti i facet configurati.
- Verifica il funzionamento della navigazione tra categorie.
- Verifica la paginazione tramite i risultati.
- Verificare che le opzioni di ordinamento funzionino come previsto.
- Test della funzionalità aggiuntiva al carrello per prodotti semplici.

**Test visivi**:

- Verificare che le immagini del prodotto siano visualizzate correttamente.
- Verifica che i nomi dei prodotti e i prezzi siano visualizzati correttamente.
- Campioni colore di prova (se utilizzati).
- Verifica il comportamento reattivo sui dispositivi mobili.
- Verifica che lo stile corrisponda al tuo marchio.

**Test delle prestazioni**:

- Misura i tempi di caricamento delle pagine.
- Verifica con dimensioni di catalogo realistiche.
- Monitorare l&#39;utilizzo delle risorse del server.
- Controlla la console del browser per verificare la presenza di errori JavaScript.

### Passaggio 4: distribuire in produzione

Sposta la configurazione convalidata nella vetrina.

**Ruolo**: commerciante/partner

1. Se possibile, pianifica la distribuzione durante la finestra di manutenzione.
1. Segui il processo di distribuzione standard.
1. Abilitare il widget PLP in produzione utilizzando [Passaggio 2: abilitare il widget PLP](#step-2-enable-the-plp-widget).
1. Monitora eventuali problemi subito dopo la distribuzione.
1. Disponi di un piano di rollback pronto in caso di problemi critici.

### Passaggio 5: Convalida e monitoraggio

Monitora le prestazioni di ricerca e l’esperienza del cliente dopo la migrazione.

**Ruolo**: commerciante

Dopo la distribuzione, monitora le metriche chiave:

- Percentuale di ricerca con risultati zero
- Tasso di conversione da ricerca a carrello
- Prestazioni di caricamento pagina
- Feedback o ticket di supporto del cliente
- Errori JavaScript nella console del browser

## Scenari di migrazione complessi

I seguenti scenari richiedono pianificazione aggiuntiva, sviluppo personalizzato o supporto specializzato oltre i passaggi di migrazione standard.

### Tema personalizzato con modifiche al layout

In questo scenario, sono presenti modelli o layout personalizzati che sostituiscono il comportamento predefinito dell’elenco di prodotti.

**Ruolo**: Sviluppatore/Partner

1. **Personalizzazioni di controllo**:
   - Documenta tutti i file XML di layout personalizzati nel tema.
   - Esamina eventuali modifiche apportate al modello personalizzato nelle pagine di elenco dei prodotti o nei file correlati.
   - Identifica le classi CSS personalizzate utilizzate per lo stile.
   - Documenta le interazioni JavaScript personalizzate.

1. **Migrare a personalizzazioni basate su CSS**:
   - Il widget PLP utilizza classi CSS specifiche (vedere [Guida allo stile PLP](plp-styling.md)).
   - Ricrea personalizzazioni visive utilizzando le classi CSS del widget PLP.
   - Verifica che gli stili personalizzati siano applicati correttamente.

1. **Rimuovi personalizzazioni in conflitto**:
   - Rimuovi l’XML di layout che modifica la struttura dell’elenco di prodotti.
   - Pulire JavaScript che esegue il targeting di elementi specifici della scheda di ricerca.
   - Aggiorna le sostituzioni del modello in conflitto con il rendering del widget.

1. **Verifica completa**:
   - Verificare che tutte le personalizzazioni visive funzionino con il widget PLP.
   - Assicurati che non vi siano conflitti di layout.
   - Esegui il test su tutti i punti di interruzione e i dispositivi.

### Attributi del prodotto con modelli di origine personalizzati

In questo scenario, sono presenti facet che utilizzano attributi di prodotto con modelli di origine personalizzati non supportati dall&#39;adattatore di ricerca ma SUPPORTATI dal widget PLP.

**Ruolo**: commerciante (configurazione amministratore)

1. **Identificare gli attributi interessati**:
   - Rivedi gli attributi del prodotto utilizzati come facet.
   - Identifica quali utilizzano i modelli di origine personalizzati.
   - Documenta la configurazione facet corrente.

1. **Aggiornare e abilitare il widget PLP**:
   - Segui [Passaggi di migrazione standard](#standard-migration-steps).
   - Il widget PLP supporta gli attributi del modello di origine personalizzato.

1. **Riconfigura facet**:
   - Vai a **[!UICONTROL Marketing]** > SEO e cerca > **[!UICONTROL Live Search]**.
   - Verifica la configurazione del facet per gli attributi interessati.
   - I facet di test funzionano correttamente con i modelli di origine personalizzati.

1. **Convalida**:
   - Test del filtro con facet del modello di origine personalizzati.
   - Verificare che tutti i valori degli attributi vengano visualizzati correttamente.
   - Assicurati che le prestazioni siano accettabili.

### Integrazione con Google Tag Manager (GTM)

In questo scenario, esiste un problema noto in cui l’abilitazione del widget PLP può causare il mancato funzionamento di GTM.

**Ruolo**: Sviluppatore/Partner + Ingegneria del Cliente

**Opzione 1: continuare con la scheda di ricerca (solo provvisoria)**

- Mantieni la scheda di ricerca abilitata se GTM è business-critical.
- Comprendere che riceverai solo aggiornamenti di sicurezza.
- Pianifica la migrazione quando viene risolta la compatibilità GTM.
- Contatta il supporto Adobe per aggiornamenti sulla compatibilità GTM.

**Opzione 2: migrazione del tracciamento GTM a un approccio alternativo**

1. **Implementare una raccolta di eventi personalizzata**:

   - Utilizza [Eventi Storefront SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/).
   - Acquisisci eventi di ricerca e interazione del prodotto.
   - Invia manualmente gli eventi al livello dati GTM.

1. **Completare i passaggi seguenti**:

   - Verifica i requisiti di tracciamento GTM correnti.
   - Mappa gli eventi GTM a Storefront Events.
   - Implementare listener di eventi personalizzati.
   - Flusso dei dati di prova in GTM.
   - Convalidare i rapporti di analisi.

**Opzione 3: sostituire GTM con Adobe Analytics**

- Valuta se eseguire la migrazione a [Adobe Analytics](https://business.adobe.com/products/adobe-analytics.html), se applicabile.
- Contatta il team di progettazione clienti per assistenza.

**Chi contattare**: invia un ticket di supporto per aggiornamenti sulla compatibilità GTM o assistenza tecnica clienti.

### Scenario: implementazione headless o PWA

In questo scenario, si dispone di una vetrina headless o PWA che richiede la raccolta di eventi personalizzati e non può utilizzare l’interfaccia utente standard del widget PLP.

**Ruolo**: Sviluppatore/Partner

1. **Verifica implementazioni di riferimento**:
   - Esaminare il codice sorgente del widget [PLP](https://github.com/adobe/storefront-product-listing-page).
   - Consulta la documentazione API per [[!DNL Live Search] GraphQL](graphql.md).
   - Comprendere le [query di Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).

1. **Implementare un&#39;interfaccia utente personalizzata**:
   - Utilizza l&#39;API GraphQL [!DNL Live Search] per le query.
   - Creare componenti personalizzati per l’elenco dei prodotti.
   - Implementa l’interfaccia utente per il faceting.
   - Gestisci impaginazione e ordinamento.

1. **Implementa raccolta eventi**:
   - Consulta la [documentazione sugli eventi storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search).
   - Implementa gli eventi richiesti:
      - `search-request-sent`
      - `search-response-received`
      - `search-results-view`
      - `product-page-view`
      - `add-to-cart`
   - I dati dell’evento di test fluiscono in Adobe Commerce.

1. **Configura ordinamento facet**:
   - Per le implementazioni headless, i facet possono essere ordinati in base al conteggio.
   - Configurare nell&#39;area di lavoro **[!UICONTROL Live Search]** > **[!UICONTROL Facets]**.
   - Impostare **[!UICONTROL Sort Type]** su **Count** per una migliore interfaccia utente.

1. **Verifica e convalida**:
   - Verifica la precisione dei risultati della ricerca.
   - Funzionalità facet di test.
   - Verifica che gli eventi siano tracciati correttamente.
   - Monitorare le metriche delle prestazioni.
   - Convalidare il funzionamento delle funzioni di merchandising intelligenti.

### Scenario: modifiche al codice widget personalizzato

In questo scenario, hai personalizzato in precedenza l’adattatore di ricerca o il codice del widget e devi migrare le personalizzazioni.

**Ruolo**: Sviluppatore/Partner

1. **Documenta personalizzazioni esistenti**:
   - Elenca tutte le personalizzazioni apportate all&#39;adattatore di ricerca.
   - Identifica i requisiti aziendali alla base di ogni personalizzazione.
   - Determina se le personalizzazioni sono ancora necessarie.

1. **Verifica se le funzionalità integrate soddisfano le tue esigenze**:
   - Rivedi [funzionalità widget PLP](plp-styling.md#widget-features).
   - Verifica se la personalizzazione basata su CSS è sufficiente.
   - Verifica il comportamento predefinito del widget PLP.

1. **Se il codice personalizzato è ancora necessario**:
   - Clona l&#39;archivio widget [PLP](https://github.com/adobe/storefront-product-listing-page).
   - Implementare le personalizzazioni.
   - Ospita sulla tua rete CDN.
   - Aggiorna la configurazione di Commerce per utilizzare il widget personalizzato.

   >[!WARNING]
   >
   >Se personalizzi il widget PLP utilizzando il codice dell’archivio, sei responsabile della manutenzione e degli aggiornamenti. Le nuove funzioni dei widget PLP di Adobe potrebbero essere incompatibili con le personalizzazioni.

1. **Verifica completa**:
   - Verifica tutte le funzionalità personalizzate.
   - Verifica che gli aggiornamenti di Commerce non interrompano le personalizzazioni.
   - Documenta l’implementazione personalizzata.
   - Pianifica la manutenzione in corso.

## Limitazioni note e casi limite

Presta attenzione a queste limitazioni durante la migrazione:

**Limitazioni del widget PLP**:

- **Direzione ordinamento**: quando il widget PLP è abilitato, non è possibile modificare la direzione ordinamento nelle pagine di elenco prodotti (crescente/decrescente).
- **Aggiungi al carrello**: i pulsanti Aggiungi al carrello sono disponibili solo per i prodotti semplici nel widget.
- **Prezzo di livello**: non supportato nel widget PLP.
- **Visualizzazione IVA**: i prezzi includono l&#39;IVA, ma l&#39;IVA non può essere visualizzata come valore separato.

**Differenze di funzionalità rispetto alla scheda di ricerca**:

- **Campioni colore**: l&#39;attributo `color` deve essere scritto esattamente come `color` (non come &quot;colore&quot; o nomi personalizzati) per il corretto funzionamento dei campioni.
- **Stile tema**: le classi tema personalizzate non vengono ereditate dal widget. È necessario impostare come destinazione le classi CSS specifiche del widget.
- **Tipi di prodotto personalizzati**: non supportati nel widget.

**Considerazioni sulle prestazioni**:

- I cataloghi di grandi dimensioni (oltre 50.000 prodotti) possono presentare caricamenti di pagina iniziali più lunghi.
- Più facet con molti valori possono influire sulle prestazioni.
- Le prestazioni del dispositivo mobile possono variare in base alle dimensioni del catalogo.

**Problemi di compatibilità**:

- Problema di compatibilità con Google Tag Manager (vedi [Scenario GTM](#google-tag-manager-gtm-integration)).
- Alcune estensioni di terze parti possono entrare in conflitto con il widget PLP.
- Le estensioni di estrazione personalizzate potrebbero richiedere aggiornamenti.

## Ottenere aiuto

Contatta la risorsa appropriata in base alle tue esigenze specifiche.

**Il supporto Adobe** può fornire assistenza per:

- Procedure di migrazione di Standard Live Search
- Problemi di configurazione del widget PLP
- Problemi di indicizzazione dei facet o degli attributi
- Problemi di prestazioni con le implementazioni predefinite
- Errori di aggiornamento

**Contattare i partner di sviluppo/integratori di sistemi** per:

- Modifiche tema personalizzate
- Implementazioni di codice widget personalizzato
- Compatibilità di estensioni di terze parti
- Implementazioni headless o PWA
- Tracciamento degli eventi personalizzati

Per contattare il supporto Adobe, consulta la [Guida utente del Centro assistenza](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

## Domande frequenti

Risposte alle domande frequenti sulla migrazione dalla scheda di ricerca al widget PLP.

**Q: la scheda di ricerca riceverà correzioni di bug o aggiornamenti di funzionalità?**

R: No. L&#39;adattatore di ricerca è obsoleto e riceverà solo gli aggiornamenti di protezione. Correzioni di bug, miglioramenti delle prestazioni e nuove funzioni sono disponibili solo nel widget PLP. In caso di problemi con la scheda di ricerca, la soluzione consigliata è la migrazione al widget PLP.

**Q: la migrazione interromperà la mia vetrina?**

R: se segui le procedure di test corrette nella gestione temporanea, la migrazione dovrebbe essere perfetta. Disponi di un piano di rollback pronto per la distribuzione in produzione.

**Q: quanto tempo richiede la migrazione?**

R: per implementazioni standard: 1-2 ore. Per le implementazioni personalizzate: 1-4 settimane a seconda della complessità.

**D: le regole di merchandising per la ricerca funzioneranno ancora?**

R: Sì, tutte le regole di merchandising di ricerca, i sinonimi e i facet configurati nell&#39;area di lavoro [!DNL Live Search] continuano a funzionare con il widget PLP.

**Q: è necessario riconfigurare i facet?**

R: In genere no, ma se gli attributi del modello di origine personalizzato erano limitati dall’adattatore di ricerca, ora puoi utilizzarli con il widget PLP.

**Q: cosa dire del CSS personalizzato?**

R: È necessario aggiornare CSS per eseguire il targeting delle classi di widget PLP. Vedi il riferimento alle [classi CSS](plp-styling.md#css-classes).

**Q: questo influirà sulle prestazioni di ricerca?**

R: Il widget PLP è progettato per essere performante. La maggior parte dei commercianti vede prestazioni uguali o migliori. I cataloghi di grandi dimensioni devono essere testati nella staging.
