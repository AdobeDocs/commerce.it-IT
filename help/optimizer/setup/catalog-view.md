---
title: Vista catalogo
description: Scopri cosa sono le visualizzazioni catalogo e come crearle per organizzare il catalogo dei prodotti in base alla struttura aziendale, alle politiche e ai prezzi.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
source-git-commit: f67a5327b742338655b0f7ffa4076a174219f711
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---


# Visualizzazioni catalogo per servizi di merchandising

Le visualizzazioni catalogo sono alla base di Adobe Commerce Optimizer Merchandising Services e consentono di organizzare il catalogo dei prodotti in base alla struttura aziendale, alle politiche e ai prezzi. Questo modello dati flessibile supporta scenari multi-brand, multi-business unit e multi-lingue, mantenendo al contempo l’efficienza operativa.

## Cosa sono le visualizzazioni catalogo?

Le visualizzazioni catalogo definiscono il modo in cui il catalogo dei prodotti viene organizzato e visualizzato. Agiscono come filtri che determinano:

- **Quali prodotti sono visibili** in base alla struttura aziendale (marchi, aree geografiche, rivenditori)
- **Prezzi visualizzati** tramite listini prezzi collegati
- **Come vengono filtrati i prodotti** utilizzando i criteri (attributi come marchio, modello, categoria)
- **Origine del catalogo utilizzata** in base ad attributi quali le impostazioni locali

Considera le viste catalogo come diversi &quot;obiettivi&quot; attraverso i quali i clienti vedono il tuo catalogo. Ad esempio:

- La vista del catalogo del dealer mostra solo i prodotti disponibili per quel dealer specifico
- Una vista del catalogo regionale potrebbe mostrare prodotti e prezzi specifici per un’area geografica
- Una vista catalogo marchio può mostrare solo i prodotti di una particolare marca

## Creare una vista catalogo

In questa sezione, puoi creare una visualizzazione catalogo, selezionare un [criterio](policies.md) e un [listino prezzi dedicato](pricebooks.md).

Prima di creare una vista catalogo, assicurati di disporre di:

- [Criteri creati](policies.md) per definire i filtri dei prodotti

- [Imposta i listini prezzi](pricebooks.md) per i prezzi

1. Dal menu a sinistra, vai a _Configurazione archivio_ e fai clic su **[!UICONTROL Catalog views]**.

1. Fare clic su **[!UICONTROL Create catalog view]**. &#x200B;

1. Configura i dettagli di visualizzazione del catalogo:

   - **Nome** - Immettere il nome della visualizzazione del catalogo, ad esempio `Celport`. &#x200B;
   - **Origini del catalogo** - Aggiungere l&#39;origine del catalogo (impostazioni locali), ad esempio `en-US`. Premere **Invio**.
   - **Criteri**: utilizzare il menu a discesa per selezionare i criteri rilevanti. Ad esempio, &quot;Marchio&quot;, &quot;Modello&quot;. &#x200B;Assicurarsi di avere già [creato un criterio](policies.md).

1. Selezionare il listino prezzi dedicato da collegare alla vista catalogo.

1. Fare clic su **[!UICONTROL Add]** per creare la visualizzazione catalogo con il listino prezzi dedicato e i criteri collegati.

   Se il pulsante **[!UICONTROL Add]** non è attivo, assicurati che l&#39;origine del catalogo sia aggiunta correttamente posizionando il cursore nel campo Origini del catalogo e premendo **Invio**. &#x200B;

La pagina Visualizzazioni catalogo viene aggiornata per visualizzare la nuova visualizzazione del catalogo.&#x200B;

Dopo aver completato questi passaggi, la vista catalogo viene ora configurata per visualizzare prodotti e prezzi in base alle origini e ai criteri selezionati.

## Panoramica dell’architettura

Le visualizzazioni catalogo fanno parte del framework dei servizi di merchandising che sostituisce il framework per siti web, store e store view utilizzato nelle fondazioni di Adobe Commerce con un modello più flessibile:

Architettura ![[!DNL Merchandising Services]](../assets/merchandising-svcs-architecture.png)

### Come funziona

**1. Acquisizione dei dati**
I dati del catalogo da PIM, ERP e altri sistemi vengono acquisiti nel framework dei servizi di merchandising. Ogni SKU contiene informazioni sulle impostazioni internazionali e attributi di prodotto associati a viste catalogo, criteri e impostazioni internazionali. Per ulteriori informazioni sull&#39;acquisizione dei dati, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog).

**2. Catalogo base unificato**
I dati acquisiti creano un catalogo di base unificato nella pipeline di dati di Catalog Service. Questa fonte singola elimina la duplicazione dei dati tra le unità aziendali.

**3. Visualizzazioni catalogo**
Più visualizzazioni catalogo rappresentano diverse unità aziendali (ad esempio, &quot;Texas Retail&quot;, &quot;Texas Retail Seasonal&quot;). Le impostazioni internazionali, le policy e i listini prezzi possono essere condivisi tra le diverse viste di catalogo per garantire flessibilità.

**4. Consegna multicanale**
I dati del catalogo filtrati vengono consegnati a varie destinazioni, tra cui vetrine Edge Delivery Services, marketplace, piattaforme pubblicitarie e micro-vetrine personalizzate. Per ulteriori informazioni sulla distribuzione dei dati del catalogo, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog).

### Componenti chiave

| Componente | Finalità | Esempio |
|---|---|---|
| **Visualizzazione catalogo** | Business unit o canale di distribuzione | Dealer network, negozio di zona |
| **Criterio** | Filtro prodotti basato su attributi | Marchio, modello, categoria |
| **Impostazioni locali** | Impostazione della lingua | en-US, fr-CA, es-MX |
| **Listino prezzi** | Struttura dei prezzi | Commercio al dettaglio, commercio all&#39;ingrosso, dipendente |

### Flusso di dati

1. **Acquisisci** - Dati prodotto da sistemi PIM/ERP
2. **Processo** - Applica visualizzazioni catalogo, criteri e determinazione prezzi
3. **Consegna** - Distribuisci il catalogo filtrato a vetrine, marketplace, ecc.

## Funzioni principali

| Funzionalità | Beneficio |
|---|---|
| **Catalogo base singolo** | Eliminazione della duplicazione dei dati tra le unità aziendali |
| **Prezzo flessibile** | Più listini prezzi per SKU per diversi segmenti di clienti |
| **Scalabile** | Gestione efficiente di oltre 200 milioni di SKU |
| **Multicanale** | Distribuisci cataloghi su vetrine, mercati e piattaforme pubblicitarie |
| **Aggiornamenti in tempo reale** | Aggiornamento rapido dei dati del catalogo per promozioni e campagne |

## Casi d’uso

### Conglomerato multimarca

**Sfida**: gestisci più marchi, paesi e lingue<br>
**Soluzione**: catalogo singolo con visualizzazioni catalogo per ogni combinazione di marchio/area geografica

### Dealer di componenti per automobili

**Sfida**: 3.000 dealer con gli stessi prodotti ma prezzi diversi<br>
**Soluzione**: un catalogo con viste catalogo e listini prezzi specifici per i dealer

### Retailer multi-posizione

**Sfida**: prezzi e scorte diversi per ubicazione<br>
**Soluzione**: viste catalogo basate sulla posizione con criteri specifici per l&#39;area geografica

>[!INFO]
>
>Per informazioni dettagliate sull&#39;acquisizione e la consegna dei dati del catalogo, consulta la [documentazione per gli sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog).
