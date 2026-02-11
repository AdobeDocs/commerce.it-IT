---
title: Limiti e limiti
description: Scopri i limiti e le limitazioni di  [!DNL Product Recommendations]  per garantire che soddisfi le esigenze della tua azienda.
role: Admin, Developer
source-git-commit: 66830c9d950a27269aca1bda0dcc7d0d86f05647
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Limiti e limiti

Rivedi i limiti e le limitazioni seguenti per garantire che [!DNL Product Recommendations] soddisfi le esigenze della tua azienda. Comprendere questi vincoli ti aiuta a pianificare l’implementazione, configurare i filtri ed evitare problemi comuni.

## Generale

- **Tipi di prodotto** - I tipi di prodotto supportati includono _simple_, _configurable_, _virtual_, _downloadable_ e _gift card_. _I tipi di prodotto_, _raggruppati_ e personalizzati non sono supportati. Se il catalogo contiene un numero elevato di tipi di prodotto non supportati, il [punteggio di preparazione](create.md#readiness-indicators) sarà basso. Vedi [Filtro per tipo di prodotto](filters.md#type).
- **SKU con spazi** - Gli SKU contenenti spazi possono ridurre la rilevanza dei consigli e devono essere evitati quando possibile.
- **Pagina carrello** - I consigli di prodotto non sono supportati nella pagina del carrello quando lo store è configurato per [visualizzare la pagina del carrello subito dopo aver aggiunto un prodotto al carrello](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration). Consulta [Creare consigli](create.md).
- **Prodotti secondari** - I prodotti secondari di un prodotto configurabile (visibilità _Non visibile singolarmente_) non vengono visualizzati in un&#39;unità di consigli. Può essere visualizzato solo il prodotto configurabile (padre). Vedi [Filtra prodotti](filters.md#product).
- **Prodotti disabilitati o non visibili** - I prodotti disabilitati o non visibili singolarmente non possono mai essere visualizzati nei consigli e non possono essere selezionati nei filtri dei prodotti.
- **Prezzi speciali** - [I prezzi speciali](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) con date di inizio e fine non sono supportati nelle unità di consigli. Un prodotto con un prezzo speciale può essere visualizzato nei consigli, ma l’unità non visualizza il prezzo speciale, la data di inizio o la data di fine. Gli acquirenti vedono il prezzo regolare (o altri dati sui prezzi forniti dal catalogo/feed dei prezzi) fino a quando non aprono la pagina del prodotto.

## Unità consigli

- **Unità attive per tipo di pagina** - È possibile creare fino a 50 unità di consigli attive per ogni tipo di pagina (Home, Categoria, Dettagli prodotto, Carrello, Conferma). Al raggiungimento del limite, il tipo di pagina è disattivato nel flusso di creazione.
- **Prodotti per unità** - Il numero di prodotti visualizzati in un&#39;unità di consigli può essere impostato da 5 (impostazione predefinita) a un massimo di 20.
- **Stato bozza** - Dopo aver salvato un consiglio come bozza, non è possibile modificare il tipo di pagina o il tipo di consiglio per tale unità. Prima dell&#39;attivazione è possibile modificare altre impostazioni.

## Filtri e condizioni

- **Condizioni dinamiche** - Le condizioni dinamiche (ad esempio &quot;prodotti nella stessa categoria del prodotto corrente&quot; o &quot;fascia di prezzo relativa&quot;) sono disponibili su ogni tipo di pagina ad eccezione della home page. Inoltre, non sono disponibili nelle pagine in cui i consigli vengono inseriti con Page Builder. Vedi [Condizioni](filters.md#conditions).

## Ambienti di anteprima e non di produzione

- **Anteprima visualizzata di recente** - Il tipo di consiglio _Visualizzato di recente_ non può essere visualizzato in anteprima nell&#39;amministratore perché i dati si basano sulla cronologia del browser e non sono disponibili nel contesto amministratore. Consulta [Anteprima raccomandazioni](create.md#preview).
- **Consigli da un altro spazio dati** - Quando [recuperi i consigli da un altro spazio dati SaaS](settings.md) (ad esempio, produzione) in una vetrina non di produzione, puoi visualizzare i consigli ma non puoi passare alle relative pagine di prodotto. Questa funzione è progettata per l’anteprima e il test.
- **GraphQL e spazio dati alternativo** - Quando si utilizzano i consigli di prodotto tramite [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/), il parametro `alternateEnvironmentId` (utilizzato per recuperare i consigli da un altro spazio dati) non è disponibile. Utilizza l’API REST o le Impostazioni amministratore per cambiare l’origine dei consigli in non produzione.

## API e configurazione

- **Chiavi API (4.x e versioni successive)** - È necessario fornire chiavi API pubbliche e private sia per gli ambienti sandbox che per quelli di produzione. Se non fornisci entrambe le coppie di chiavi API, non puoi accedere alla funzione Consigli di prodotto in Amministrazione. La raccolta dei dati sulla vetrina e i consigli esistenti continuano a funzionare. Vedi [Installa e configura](install-configure.md).

## Limitazioni per i cookie

- Quando la modalità di restrizione dei cookie [1&rbrace; è attivata e gli acquirenti non hanno accettato i cookie, alcuni tipi di consigli che si basano su dati comportamentali potrebbero non essere visualizzati o mostrare risultati limitati.](setting-cookie.md)
- I tipi di consigli che non si basano su dati comportamentali (ad esempio, _Più visualizzati_, _Somiglianza visiva_) continuano a funzionare quando le restrizioni dei cookie sono abilitate.
- Quando le restrizioni sui cookie sono abilitate, la funzione Consigli di prodotto non raccoglie né memorizza i dati comportamentali nei cookie o nell’archiviazione locale fino a quando l’acquirente non acconsente.

## Page Builder

- **Metriche e viste archivio** - Le metriche per le unità di consigli di Page Builder vengono visualizzate solo nella vista archivio predefinita nell&#39;area di lavoro Consigli di prodotto. Per visualizzare le metriche dei consigli di Page Builder in una visualizzazione archivio non predefinita, è necessario aprire e [modificare](edit.md) l&#39;unità di consigli di Page Builder in tale visualizzazione archivio e salvarla. Le metriche verranno quindi visualizzate per tale visualizzazione archivio. Consulta [Integrazione di Page Builder](page-builder.md).

## B2B

- La funzione Consigli di prodotto rispetta [le autorizzazioni per la categoria](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions.html), [i cataloghi condivisi](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) e i prezzi specifici del gruppo di clienti. Gli acquirenti vedono solo i consigli per i prodotti a cui possono accedere in base al segmento e all’assegnazione del catalogo. Consulta [Onboarding](onboarding.md).

## Dati e preparazione

- **Dati comportamentali** - Molti tipi di consigli richiedono dati comportamentali sufficienti nella vetrina (visualizzazioni, componenti aggiuntivi al carrello, acquisti). Nuovi store o store a basso traffico possono vedere risultati limitati o inesistenti per questi tipi fino a quando non vengono raccolti dati adeguati. Monitora [gli indicatori di preparazione](create.md#readiness-indicators) nell&#39;amministratore.
- **Gestione temporanea senza dati di produzione** - In un ambiente non di produzione senza dati comportamentali, l&#39;unico tipo di consiglio che è possibile testare senza recuperare dalla produzione è _Altro tipo simile a questo_, che utilizza solo somiglianza basata su catalogo. Consulta [Ambiente di staging](staging-environment.md).

## Risoluzione dei problemi

Per informazioni sulla sincronizzazione del catalogo, sulla mancata visualizzazione dei consigli o su altri problemi comuni, eseguire una ricerca nella [Knowledge Base di Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) o contattare il [supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
