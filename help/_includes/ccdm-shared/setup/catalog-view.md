---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
<!--This shared include file contains the conceptual and architecture overview of catalog views for Adobe Merchandising Services-->

Una vista catalogo definisce i prodotti e i prezzi che un cliente può recuperare. Combina origini di catalogo, livelli di catalogo, criteri e listini prezzi per supportare diversi marchi, aree geografiche, business unit o canali.

## Cosa sono le visualizzazioni catalogo?

Le visualizzazioni catalogo definiscono il modo in cui il catalogo dei prodotti viene organizzato e visualizzato. Agiscono come filtri che determinano:

- **Quali prodotti sono visibili** in base alla struttura aziendale (marchi, aree geografiche, rivenditori)
- **Prezzi visualizzati** tramite listini prezzi collegati
- **Come vengono filtrati i prodotti** utilizzando i criteri (attributi come marchio, modello, categoria)
- **Che cosa viene utilizzata [l&#39;origine del catalogo](/help/optimizer/setup/catalog-sources.md)** in base ad attributi come le impostazioni locali
- **Chi può accedere ai dati della visualizzazione** tramite [Catalog Protection](private-catalog-view.md) e [chiavi di accesso con restrizioni](restricted-access-keys.md)

Ad esempio, puoi creare visualizzazioni catalogo separate per:

- Un marchio o una business unit
- Un’area geografica
- Un canale dealer o partner
- Un segmento di clienti con prezzi specifici

## Panoramica dell’architettura

Le visualizzazioni catalogo fanno parte del framework dei servizi Adobe Merchandising che sostituisce il framework di siti web, store e storeview utilizzato nelle fondazioni di Adobe Commerce con un modello più flessibile:

Architettura ![[!DNL Merchandising Services]](/help/assets/ccdm-shared/setup/merchandising-svcs-architecture.png)

### Come funziona

**1. Acquisizione dei dati**
I dati del catalogo provenienti da un backend di Adobe Commerce o da un altro backend di terze parti (ad esempio, PIM o ERP) e da altri sistemi vengono acquisiti nel livello dati di Adobe Merchandising Services. Ogni SKU contiene informazioni sulle impostazioni internazionali e attributi di prodotto associati a viste catalogo, criteri e impostazioni internazionali. Il processo di acquisizione dei dati dipende dal sistema di origine e dal metodo di integrazione:

- **Backend di Adobe Commerce**: il sistema esporta i feed del catalogo di Commerce, li mappa nel formato previsto dall&#39;API REST per l&#39;acquisizione dei dati e sincronizza i dati dei feed con il livello dati di Adobe Merchandising Services. In questo modello, Adobe Commerce gestisce la sincronizzazione iniziale e gli aggiornamenti successivi. I feed includono prodotti, categorie, attributi di prodotto, prezzi e listini prezzi.

- **Sistema di back-end o di origine di terze parti**. Un connettore o un servizio di integrazione recupera i dati del catalogo dall&#39;origine tramite API, eventi o feed di esportazione, quindi li mappa e li convalida in base allo schema del modello dati del catalogo componibile (CCDM) e li sincronizza con il livello Servizi di Adobe Merchandising utilizzando l&#39;API REST per l&#39;acquisizione dei dati. L’integrazione è responsabile del caricamento iniziale e dell’invio delle modifiche successive. Un connettore specifico della piattaforma, ad esempio il [connettore Salesforce Commerce](https://experienceleague.adobe.com/en/docs/commerce/optimizer/developer/salesforce-connector) di Adobe, può fornire un punto di partenza.

**2. Catalogo base unificato**
I dati acquisiti creano un catalogo di base unificato nella pipeline di dati di Catalog Service. Questa fonte singola elimina la duplicazione dei dati tra le unità aziendali.

**3. Visualizzazioni catalogo**
Più visualizzazioni catalogo rappresentano diverse unità aziendali (ad esempio, &quot;Texas Retail&quot;, &quot;Texas Retail Seasonal&quot;). Le impostazioni internazionali, le policy e i listini prezzi possono essere condivisi tra le diverse viste di catalogo per garantire flessibilità.

**4. Consegna multicanale**
I dati di catalogo filtrati vengono inviati a destinazioni come Edge Delivery Services, marketplace, piattaforme pubblicitarie e micro-vetrine personalizzate. Per ulteriori informazioni sulla distribuzione dei dati del catalogo, consulta la [documentazione per gli sviluppatori](https://developer.adobe.com/commerce/services/optimizer/).

Quando è abilitato **[!UICONTROL Catalog Protection]** in una visualizzazione catalogo, la consegna a tale destinazione richiede un token firmato valido da una [chiave di accesso con restrizioni](restricted-access-keys.md) assegnata; le richieste non autorizzate vengono negate invece di ricevere i dati del catalogo.

### Componenti chiave

| Componente | Finalità | Esempio |
|---|---|---|
| **Visualizzazione catalogo** | Business unit o canale di distribuzione | Dealer network, negozio di zona |
| **Criterio** | Filtro prodotti basato su attributi | Marchio, modello, categoria |
| **Impostazioni locali** | Impostazione della lingua | en-US, fr-CA, es-MX |
| **Listino prezzi** | Struttura dei prezzi | Commercio al dettaglio, commercio all&#39;ingrosso, dipendente |
| **Chiave di accesso limitata** | Credenziali token firmato che consentono di accedere a una visualizzazione di catalogo protetta | Chiave portale partner, chiave di prezzo B2B |

### Flusso di dati

1. **Acquisisci** - dati catalogo dal backend Adobe Commerce
2. **Processo** - Applica visualizzazioni catalogo, criteri e determinazione prezzi
3. **Consegna** - Distribuisci catalogo filtrato a vetrine, marketplace e così via

## Funzioni principali

| Funzionalità | Beneficio |
|---|---|
| **Catalogo base singolo** | Eliminazione della duplicazione dei dati tra le unità aziendali |
| **Prezzo flessibile** | Più listini prezzi per SKU per diversi segmenti di clienti |
| **Scalabile** | Gestione efficiente di oltre 200 milioni di SKU |
| **Multicanale** | Distribuisci cataloghi su vetrine, mercati e piattaforme pubblicitarie |
| **Aggiornamenti in tempo reale** | Aggiornamento rapido dei dati del catalogo per promozioni e campagne |
| **Visualizzazioni catalogo privato** | Limitare la visualizzazione di un catalogo ai client autorizzati mediante la convalida del token firmato |

## Casi d’uso

### Conglomerato multimarca

**Sfida**: gestisci più marchi, paesi e lingue<br>
**Soluzione**: catalogo singolo con visualizzazioni catalogo per ogni combinazione di marchio/area geografica

### Rivenditore di componenti per automobili

**Sfida**: 3.000 dealer con gli stessi prodotti ma prezzi diversi<br>
**Soluzione**: un catalogo con viste catalogo e listini prezzi specifici per i dealer

### Retailer multisito

**Sfida**: prezzi e scorte diversi per ubicazione<br>
**Soluzione**: viste catalogo basate sulla posizione con criteri specifici per l&#39;area geografica

>[!NOTE]
>
>Per informazioni dettagliate sull&#39;acquisizione e la consegna dei dati del catalogo, consulta la [documentazione per gli sviluppatori](https://developer.adobe.com/commerce/services/optimizer/).
