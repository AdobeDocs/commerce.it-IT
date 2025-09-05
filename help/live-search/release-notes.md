---
title: Note sulla versione [!DNL Live Search]
description: Informazioni aggiornate sulla versione di  [!DNL Live Search]  da Adobe Commerce.
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: a7fecafe005c68c58a3491a2aad206d16d6d621b
workflow-type: tm+mt
source-wordcount: '2577'
ht-degree: 0%

---

# Note sulla versione [!DNL Live Search]

Queste note sulla versione descrivono le versioni più recenti di [!DNL Live Search].
È disponibile il supporto per la versione principale rilasciata corrente. Vengono fornite a titolo di riferimento le note sulla versione per le versioni precedenti.
Gli aggiornamenti includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Correzioni](../assets/fix.svg) correzioni e miglioramenti
![Bug](../assets/bug.svg) problemi noti

## Aggiornamenti dei servizi in hosting

Queste note descrivono gli aggiornamenti pubblicati al di fuori di una versione con versione o i miglioramenti al servizio ospitato.

_29 aprile 2025_

![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale il rapporto **Esporta in CSV** nella scheda [**Prestazioni**](./performance.md) non includeva tutti i dati specificati nell&#39;intervallo di date.
![Correzione](../assets/fix.svg) è stato risolto un problema che impediva il salvataggio di una [regola di merchandising](./rules.md) se era stato utilizzato il filtro di query di ricerca.
![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale [prodotti bloccati](./facets-manage.md#pinunpin-facet) non erano elencati nella parte superiore della pagina dei risultati.

_21 aprile 2025_

![Correzione](../assets/fix.svg) è stato risolto un problema relativo al filtro di intervallo per i prezzi in modo che i prodotti uguali all&#39;intervallo superiore non vengano inclusi nei risultati. Questa modifica è in linea con il modo in cui gli intervalli di prezzi vengono definiti per i facet.

_3 aprile 2025_

![Correzione](../assets/fix.svg) Aggiornamento dell&#39;estensione SaaS Data Export per rimuovere la &quot;Categoria principale da assegnare ai prodotti&quot; [limitazione](boundaries-limits.md#b2b-and-category-permissions) per i commercianti B2B. Consulta [Gestire l&#39;estensione per l&#39;esportazione dei dati](../data-export/manage-extension.md) per scoprire come aggiornare l&#39;estensione per l&#39;esportazione dei dati SaaS alla versione 103.4.0+.

_20 febbraio 2025_

![New](../assets/new.svg) Commerce supporta i sinonimi con più parole. [Ulteriori informazioni](synonyms-type.md#multi-word-synonym-behavior). Il supporto per i sinonimi composti da più parole è disponibile solo dopo la data di rilascio del 20 febbraio. Qualsiasi sinonimo di più parole esistente richiede una reindicizzazione completa per funzionare, che puoi richiedere [creando un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

_31 gennaio 2025_

![Nuovo](../assets/new.svg) Nell&#39;ambiente di test è presente un nuovo criterio di conservazione dei dati per i dati del catalogo non interrogati. [Ulteriori informazioni](overview.md#catalog-data-retention-policy).

_19 settembre 2024_

![Nuovo](../assets/new.svg) È stata rilasciata una versione beta che supporta tre nuove funzionalità di ricerca: con livelli, inizia con e contiene. [Ulteriori informazioni](install.md#install-the-live-search-beta).

_4 settembre 2024_

![Correzione](../assets/fix.svg) aumentato il numero massimo di bucket che possono essere restituiti [all&#39;interno di un facet](boundaries-limits.md#facets) a 100.

_7 agosto 2024_

![Correzione](../assets/fix.svg): il valore massimo dell&#39;intervallo o dell&#39;intervallo di prezzo per [price faceting](settings.md#price-faceting) è stato aumentato da 10.000 a 40.000.000.

_13 febbraio 2024_

![Nuovo](../assets/new.svg) [!DNL Live Search] ora supporta l&#39;impostazione di una regola predefinita per [Search Merchandising](rules.md).

_12 ottobre 2023_

![New](../assets/new.svg) Gli amministratori di Commerce ora possono specificare la lingua dell&#39;indice per [!DNL Live Search]. Vedi [Impostazioni](settings.md).
![Correzione](../assets/fix.svg) La scheda &quot;Regole di ricerca&quot; è stata rinominata &quot;Ricerca merchandising&quot;.

_13 giugno 2023_

![Correzione](../assets/fix.svg) è stato risolto un problema che causava problemi di classificazione per alcuni caratteri, ad esempio virgolette o apostrofi. La reindicizzazione risolve questi problemi.

_25 aprile 2023_

I clienti ![New](../assets/new.svg) [!DNL Live Search] ora possono sfruttare il nuovo [indicizzatore di prezzo SaaS](../price-index/price-indexing.md).

### Widget PLP

_22 maggio 2025_

![Correzione](../assets/fix.svg) è stato risolto un problema per cui il pulsante Aggiungi al carrello rimaneva in inglese quando le impostazioni locali venivano modificate in francese, tedesco, italiano o spagnolo.
![Correzione](../assets/fix.svg) è stato risolto un problema che causava la visualizzazione del pulsante Aggiungi al carrello per i prodotti esauriti.

_31 maggio 2024_

![Nuovo](../assets/new.svg) È stata rilasciata la versione 2.0.0 del widget PLP, che aggiunge il supporto per le seguenti funzionalità:

- Pulsanti Aggiungi al carrello - Disponibile solo per prodotti semplici.
- Più immagini per prodotto: l’immagine può cambiare quando si sceglie un colore diverso per un prodotto configurabile.

_27 ottobre 2023_

![Nuovo](../assets/new.svg) Il widget PLP [!DNL Live Search] ora supporta i campioni colore.

## [!DNL Live Search] 4.5.0

_5 settembre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) Live Search ora rispetta completamente la [modalità di restrizione dei cookie](install.md#cookies) impedendo la raccolta e l&#39;archiviazione dei dati nei cookie/nell&#39;archiviazione locale quando le restrizioni sono abilitate.

## [!DNL Live Search] 4.4.1

_11 agosto 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) dell&#39;endpoint del servizio di catalogo corretto per gli ambienti sandbox.

## [!DNL Live Search] 4.4.0

_14 luglio 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) ha aumentato il limite di [raggruppamento prezzi](./settings.md#price-faceting) da 50 a 100.

## [!DNL Live Search] 4.3.0

_11 marzo 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) [!DNL Live Search] ora supporta PHP 8.4 per le installazioni che eseguono Adobe Commerce 2.4.8-beta2.
![Correzione](../assets/fix.svg) è stato risolto un problema che impediva la compatibilità della scheda di ricerca con `psr/http-message:2.0`.

## [!DNL Live Search] 4.2.3

_13 febbraio 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale nella pagina dei dettagli dell&#39;ordine mancavano il numero dell&#39;ordine, la data e il pulsante **[!UICONTROL Reorder]**.

## [!DNL Live Search] 4.2.2

_6 gennaio 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) è stato risolto un problema che causava un errore con la query GraphqL `categoryList` in Adobe Commerce versione 2.4.5 e precedenti.

## [!DNL Live Search] 4.2.1

_31 luglio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) è stato risolto un problema che impediva il caricamento di alcuni script nella pagina di estrazione.
![Correzione](../assets/fix.svg) è stata corretta una versione di dipendenza nel file `composer.json`.

## [!DNL Live Search] 4.2.0

_31 maggio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) Aggiornamento dell&#39;estensione Live Search per l&#39;utilizzo dei widget PLP versione 2.0.0.

## [!DNL Live Search] 4.1.2

_16 maggio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

### Aggiornamenti

![Correzione](../assets/fix.svg) La query GraphQL [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-by-categories) è stata corretta per filtrare in base a `categoryPath` e `categoryList` per le categorie.

## [!DNL Live Search] 4.1.1

_19 marzo 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

### Nuove funzioni

![Nuovo](../assets/new.svg) Aggiunto supporto lingua per polacco.
![Nuovo](../assets/new.svg) [!DNL Live Search] ora supporta PHP 8.3 per le installazioni con Adobe Commerce 2.4.4.

## [!DNL Live Search] 4.1.0

_22 febbraio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

### Nuove funzioni

![Nuovo](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) è ora disponibile. Questo dashboard rinnovato fornisce informazioni approfondite sui flussi di dati per [!DNL Product Recommendations], [!DNL Live Search] e [!DNL Catalog Service].

### Aggiornamenti

![Correzione](../assets/fix.svg) è stato risolto un problema che causava un errore quando gli utenti ospiti aggiungevano prodotti al carrello in visualizzazioni store non predefinite.
![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale il popover di ricerca visualizzava sempre il simbolo di valuta davanti al valore del prezzo, indipendentemente dalle impostazioni internazionali.
![Correzione](../assets/fix.svg) Sono state rimosse le definizioni dei tipi non necessarie per i plug-in di base disabilitati per risolvere i problemi di compatibilità durante l&#39;installazione.

## [!DNL Live Search] 4.0.0

_13 novembre 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

### Nuove funzioni

![Nuovo](../assets/new.svg) [!DNL Live Search] ora supporta i campioni colore nel widget PLP.
![Nuovo](../assets/new.svg) [!DNL Live Search] ora visualizza il nome della categoria anziché l&#39;ID della categoria.
![Nuovo](../assets/new.svg) [!DNL Live Search] ora supporta i prezzi barrati nel widget PLP.
![New](../assets/new.svg) ha introdotto il pulsante &quot;Nascondi filtri&quot; per nascondere il pannello dei filtri.


### Aggiornamenti

![Correzione](../assets/fix.svg) Il widget PLP [!DNL Live Search] è ora abilitato per impostazione predefinita per le nuove installazioni.
![Correzione](../assets/fix.svg) La scheda di ricerca è obsoleta. In futuro, l&#39;adattatore di ricerca verrà aggiornato solo per risolvere i problemi di sicurezza.
![Correggi](../assets/fix.svg) Stili CSS riconfigurati per isolare meglio le classi widget.
![Correzione](../assets/fix.svg) correzioni di bug minori

Dopo aver installato la versione 3.1.1 o successiva, abilita i nuovi indicizzatori:

- Feed prezzi prodotto
- Feed dati del sito Web degli ambiti
- Ambiti feed dati di gruppi di clienti

Dopo l&#39;upgrade, verifica la configurazione aggiornata in QA o Staging prima di eseguire il push delle modifiche in produzione.

+++3.1.1 e precedenti

### [!DNL Live Search] 3.1.1

_15 settembre 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuova](../assets/new.svg) è stata aggiunta una nuova scheda di merchandising per categorie. Gli utenti possono ora aggiungere classificazioni intelligenti e classificazioni manuali (pin, boost, bury, hide) per categoria
![Nuovi](../assets/new.svg) utenti possono aggiungere una singola regola di categoria con classificazione intelligente o manuale
![Nuovi](../assets/new.svg) utenti possono ora aggiungere regole di classificazione intelligente alle sottocategorie
![Nuovo](../assets/new.svg) Vengono fornite informazioni dettagliate per l&#39;eliminazione di sottocategorie con classificazione intelligente
![Nuovo](../assets/new.svg) è stata aggiunta la possibilità di eliminare le regole per le strategie di classificazione ereditate
![Nuovo](../assets/new.svg) aggiunta la possibilità di eliminare le regole per una singola categoria
![Nuovi](../assets/new.svg) Gli utenti possono ora eseguire ricerche per nome di categoria quando aggiungono una regola
![Nuovo](../assets/new.svg) Nella struttura ad albero delle categorie gli utenti possono ora visualizzare la categoria a cui sono applicate le regole.
![Nuovo](../assets/new.svg) nell&#39;anteprima categoria viene visualizzata solo la categoria selezionata.
![Nuovi](../assets/new.svg) componenti di AEM CIF [widget popover](https://github.com/adobe/aem-cif-guides-venia/pull/319) e [widget PLP](https://github.com/adobe/aem-cif-guides-venia/pull/320) consentono ai siti AEM di sfruttare [!DNL Live Search].

#### Aggiornamenti

![Correzione](../assets/fix.svg) La dimensione della tabella dei prodotti e dei feed di prezzo è stata notevolmente ridotta. Nelle tabelle `catalog_data_exporter_products` e `catalog_data_exporter_product_prices` dovrebbe verificarsi una riduzione sostanziale delle dimensioni.
![Correzione](../assets/fix.svg) La scheda &quot;Regole&quot; è stata rinominata &quot;Regole di ricerca&quot;
![Correzione](../assets/fix.svg) Quando si classifica per &#39;tendenza&#39;, ora è possibile scegliere tra:
- 3 giorni (impostazione predefinita)
- 14 giorni
- 30 giorni
![Correzione](../assets/fix.svg) &#39;Eventi&#39; (Boost/Pin/Bury/Hide) è stato rinominato in &#39;Classifica manuale&#39;
![Correzione](../assets/fix.svg) &#39;Tipo di classificazione&#39; è stato rinominato in &#39;Classificazione intelligente&#39;
![Correzione](../assets/fix.svg) correzioni di bug minori

### [!DNL Live Search] 3.1.0

_1 settembre 2023_

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

#### Aggiornamenti

![Correzione](../assets/fix.svg) Il widget Elenco prodotti è stato aggiornato per utilizzare l&#39;API [Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/).

### [!DNL Live Search] 3.0.2

_7 agosto 2023_

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

#### Nuove funzioni

![Nuovo](../assets/new.svg) I seguenti valori sono stati aggiunti all&#39;oggetto `storeDetails`:

- &quot;Consenti tutti i prodotti per pagina&quot;
- Tasso di cambio
- &quot;Prodotti per pagina sulla griglia valori consentiti&quot;
- &quot;Prodotti per pagina sulla griglia Valore predefinito&quot;
- Lingua archivio

#### Aggiornamenti

![Correzione](../assets/fix.svg) moduli Catalog Service aggiunti al metapacchetto per supportare il recupero avanzato dei dati.
![Correzione](../assets/fix.svg) La navigazione della pagina **Account personale** non scompare più quando si utilizza il widget Pagina elenco prodotti.

Per accedere a queste funzioni, i commercianti devono aggiornare la versione dell&#39;estensione [!DNL Live Search] >= 3.0.2.

Si consiglia di eseguire l’aggiornamento e il test prima di passare alla produzione. Dopo aver verificato i risultati dell’ambiente di test, è consigliabile aggiornare l’ambiente di produzione nelle ore di minore utilizzo.

#### Limitazioni

L’utilizzo del widget Pagina di elenco prodotti di Live Search genera un errore in Google Tag Manager. Se è necessario Google Tag Manager, utilizzare l&#39;adattatore di ricerca predefinito.

### [!DNL Live Search] 3.0.1

_14 marzo 2023_

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

#### Nuove funzioni

![Nuova](../assets/new.svg) scheda elemento prodotto nell&#39;anteprima delle regole
![Nuovo](../assets/new.svg) [Widget pagina elenco prodotti](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-storefront/plp-styling)
![Nuovo](../assets/new.svg) [Opzioni filtro categorie](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#facets)
![Nuovo](../assets/new.svg) Aggiunta la possibilità di trascinare e rilasciare per creare eventi di fissaggio
![Nuove](../assets/new.svg) nuove azioni pin:
- Fissa in un punto - Fissa il pulsante per creare l’evento Fissa con un clic
- Fissa in alto - Posiziona il prodotto in prima posizione
- Fissa in basso - Posiziona il prodotto in fondo ai risultati
- Sbloccare un evento con un clic
![Nuovo](../assets/new.svg) [Classificazione intelligente per le regole](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add)
![New](../assets/new.svg) [!DNL Live Search] ora supporta le funzionalità complete di [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) in Commerce (in precedenza noto come inventario Multi-Source o MSI). Per abilitare il supporto completo, è necessario [aggiornare](install.md#update) il modulo di dipendenza `commerce-data-export` alla versione 102.2.0+.

#### Aggiornamenti

![Correggi](../assets/fix.svg) Configura regole ora ordina automaticamente le posizioni in modo univoco
![Correzione](../assets/fix.svg) L&#39;eliminazione di un evento esistente comporta l&#39;aggiornamento dell&#39;anteprima
![Correggi](../assets/fix.svg) le regole senza eventi possono essere salvate
![Correggi](../assets/fix.svg) Rimuovi il selettore &quot;Seleziona tipo&quot; di faceting
![Correzione](../assets/fix.svg) aggiunto nuovo stato &quot;Modifica&quot; per le regole non salvate

#### Correzioni

![Correzione](../assets/fix.svg) dell&#39;errore del server corretto quando si verifica un evento non completato durante il salvataggio
![Correzione](../assets/fix.svg) è stata corretta l&#39;eliminazione di un evento specifico in presenza di più eventi
![Correzione](../assets/fix.svg) è stato corretto un evento di regola esistente che non veniva aggiornato quando veniva aggiunto un nuovo evento
![Correzione](../assets/fix.svg) corretta al secondo clic &quot;Modifica&quot; dai dettagli, [!DNL Live Search] pagina da ricaricare
![Correzione](../assets/fix.svg) Sinonimi: è stato risolto un problema che impediva all&#39;utente di uscire dall&#39;input e di riportare lo stato attivo sul campo
![Correzione](../assets/fix.svg) di altre correzioni di bug minori e aggiornamenti delle prestazioni
![Bug](../assets/bug.svg) - La classificazione per &quot;Consigliato per te&quot; è supportata solo all&#39;interno dei widget Live Search. Non è supportato con la funzionalità di ricerca Luma e PWA predefinita.
![Bug](../assets/bug.svg) - I facet degli attributi di prezzo personalizzati non vengono visualizzati correttamente in Luma, ma l&#39;API li filtra correttamente.

I commercianti devono aggiornare la versione dell&#39;estensione [!DNL Live Search] >= 3.0.1 per accedere a queste funzioni.

Si consiglia di eseguire l’aggiornamento e il test prima di passare alla produzione. Dopo aver verificato i risultati dell’ambiente di test, è consigliabile aggiornare l’ambiente di produzione nelle ore di minore utilizzo.

### [!DNL Live Search] 2.0.5

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) - Live Search genererebbe un errore quando le risorse SDK non erano disponibili a causa di problemi di rete. Questo bug è stato corretto.

Per accedere a queste funzioni, i commercianti devono aggiornare la versione dell’estensione Live Search >= 2.0.5.

Si consiglia di eseguire l’aggiornamento e il test prima di passare alla produzione. Dopo aver verificato i risultati dell’ambiente di test, è consigliabile aggiornare l’ambiente di produzione nelle ore di minore utilizzo.

### [!DNL Live Search] 2.0.4

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) Live Search ora supporta il filtro in base all&#39;impostazione &#39;Visualizza prodotti esauriti&#39; nell&#39;amministratore. Se &#39;Visualizza prodotti esauriti&#39; è impostato su false, `inStock = true` verrà aggiunto al filtro.
![Correzione](../assets/fix.svg) Per migliorare le prestazioni, il blocco &quot;Suggestions&quot; è stato rimosso dal popup di Live Search. I dati vengono comunque trasmessi tramite GraphQL, nel caso in cui desideri sostituire la funzione.
![Correzione](../assets/fix.svg) `categories` e `categoryPath` hanno sostituito `categoryIds` per il filtro delle categorie. Ulteriori informazioni sono disponibili nell&#39;argomento [productSearch](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/).
![Correzione](../assets/fix.svg) In precedenza, un utente associato a un&#39;azienda B2B riceveva un codice gruppo clienti errato durante le ricerche. Live Search ora restituisce il valore corretto.
![Correzione](../assets/fix.svg) In precedenza, durante la ricerca di un termine inesistente, Live Search restituiva un errore. Questo bug è ora corretto.

Per accedere a queste funzioni, i commercianti devono aggiornare la versione dell&#39;estensione [!DNL Live Search] >= 2.0.4.

Si consiglia agli utenti di eseguire l’aggiornamento e il test prima di passare alla produzione. Dopo aver verificato i risultati dell’ambiente di test, è consigliabile aggiornare l’ambiente di produzione nelle ore di minore utilizzo.

### [!DNL Live Search] 2.0.3

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) Live Search ora supporta le funzionalità B2B rispettando le autorizzazioni delle categorie, i cataloghi condivisi e i prezzi specifici del gruppo di clienti.

Per accedere a queste funzioni, i commercianti devono aggiornare la versione dell&#39;estensione [!DNL Live Search] >= 2.0.3.

Si consiglia agli utenti di eseguire l’aggiornamento e il test prima di passare alla produzione. Dopo aver verificato i risultati dell’ambiente di test, è consigliabile aggiornare l’ambiente di produzione nelle ore di minore utilizzo.

### [!DNL Live Search] 2.0

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

Le installazioni di [!DNL Live Search] esistenti devono essere aggiornate a [!DNL Live Search] 2.0.0 per sfruttare le nuove funzioni, le correzioni e i miglioramenti seguenti:

![Nuovo](../assets/new.svg) [!DNL Live Search] ora supporta PHP 8.1 per le installazioni con Adobe Commerce 2.4.4.
![Nuovo](../assets/new.svg) Il modulo `Magento_ElasticsearchCatalogPermissionsGraphQl` viene aggiunto all&#39;elenco dei moduli disabilitati durante l&#39;installazione.
![Nuovo](../assets/new.svg) Il numero di righe disponibili in [[!DNL storefront popover]](overview.md) può essere configurato da *Amministratore*.
![Nuovo](../assets/new.svg) Beta [PWA](https://developer.adobe.com/commerce/pwa-studio/) supportato per [!DNL Live Search].
![Nuovo](../assets/new.svg) Il processo di installazione di [!DNL Live Search] è stato aggiornato con modifiche avanzate.
![Correzione](../assets/fix.svg) [Collegamento Ricerca avanzata](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) rimosso dal piè di pagina della vetrina.
![Bug](../assets/bug.svg) I seguenti attributi di prodotto non sono supportati da [Commerce GraphQL API](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) se utilizzati in relazione alla versione beta di PWA: `description`, `name`, `short_description`
![Bug](../assets/bug.svg) La versione beta di PWA per [!DNL Live Search] non supporta [gestione eventi](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/).

### [!DNL Live Search] 1.3.1

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Correzione](../assets/fix.svg) [L&#39;attributo di prezzo personalizzato](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) non restituisce più un errore se configurato come [facet](facets-add.md).
![Correzione](../assets/fix.svg) è stato risolto un problema che causava un errore se non era disponibile alcun [simbolo di valuta](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) (`data-currency-symbol`).
![Correzione](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) ora mostra il [Prezzo speciale](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) (prezzo finale minimo) quando disponibile.

### [!DNL Live Search] 1.3.0

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) [Performance](performance.md) il dashboard di reporting fornisce ad insight i termini di ricerca utilizzati dagli acquirenti.
![Nuovo](../assets/new.svg) [!DNL Live Search] [Eventi Storefront SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) fornisce l&#39;accesso a un livello dati comune con i servizi di pubblicazione e sottoscrizione degli eventi e le metriche.
![Correzione](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) ha una nuova classe `active` per il contenitore `.search-autocomplete` che controlla la visibilità.
![Correzione](../assets/fix.svg) Nella vetrina, il collegamento a piè di pagina [Termini di ricerca](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) è stato rimosso e la relativa cache è disabilitata per le installazioni di [!DNL Live Search].
![Bug](../assets/bug.svg) La patch per l&#39;adattatore di ricerca gestisce i prodotti duplicati.
![Bug](../assets/bug.svg) [!DNL Live Search] supporta [ubicazioni di inventario a origine singola](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage) (fisico) con più [scorte](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage) (virtuali). Al momento non sono supportate più origini inventario.

### [!DNL Live Search] 1.2.0

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md) visualizza i prodotti suggeriti e le miniature dei risultati di ricerca principali mentre gli acquirenti digitano query nella casella Ricerca.
![Nuovo](../assets/new.svg) Commerce *La sessione dell&#39;amministratore* rimane aperta durante periodi prolungati di inattività della tastiera
![New](../assets/new.svg) [!DNL Live Search] viene abilitato automaticamente dopo l&#39;onboarding
![Correzione](../assets/fix.svg) Il tempo di indicizzazione iniziale è inferiore a un&#39;ora
![Correzione](../assets/fix.svg) degli aggiornamenti incrementali del prodotto quasi in tempo reale (dopo l&#39;installazione e l&#39;installazione)
![Correggi](../assets/fix.svg) colonne ordinabili nell&#39;editor sinonimo
![Correzione](../assets/fix.svg) [!DNL Live Search] non genera più un errore se i criteri di ricerca contengono un valore di ordinamento vuoto
![Correzione](../assets/fix.svg) Il filtro dell&#39;intervallo non si interrompe più se i codici attributo contengono stringhe &quot;a&quot; o &quot;da&quot;

### [!DNL Live Search] 1.1.0

[!BADGE Supportato]{type="Informative" tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Bug](../assets/bug.svg) Il servizio [!DNL Live Search] supporta solo la [valuta di base](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration) dell&#39;installazione di Adobe Commerce.
![Bug](../assets/bug.svg) Quando si aggiunge un facet, il feed degli attributi del prodotto non viene aggiornato correttamente se impostato su `Update on Save`. Per evitare questo problema, passare a [Gestione indice](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) e impostare il feed attributi prodotto su `Update by Schedule`.
![Bug](../assets/bug.svg) [!DNL Live Search] sinonimi definiti per visualizzazione archivio, ma attualmente memorizzati per sito Web e identificati con una combinazione di `environmentId` e `storeViewCode`. Di conseguenza, tutti i siti web e le visualizzazioni dello store all’interno dell’installazione di Adobe Commerce condividono i sinonimi. Il set di sinonimi creato più di recente per la visualizzazione Store ha la precedenza.
![Bug](../assets/bug.svg) Se un sinonimo contiene più parole, ogni parola viene considerata come un sinonimo separato. Ad esempio, se definisci &quot;pezzo orario&quot; come sinonimo di &quot;orologio&quot;, sia &quot;tempo&quot; che &quot;pezzo&quot; vengono trattati come sinonimi di orologio.

+++

## Documentazione

Per ulteriori informazioni:

- [Documentazione per gli sviluppatori di Adobe Commerce](https://developer.adobe.com/commerce/docs)
- [Guida utente di Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce)
- [[!DNL Live Search] sul Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html)
