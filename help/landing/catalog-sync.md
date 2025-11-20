---
title: Sincronizzazione catalogo
description: Scopri come esportare i dati di prodotto dal server  [!DNL Commerce]  a  [!DNL Commerce Services].
feature: Catalog Management, Data Import/Export, Catalog Service
exl-id: 99f96b93-b036-490c-8c57-40463a0de365
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Sincronizzazione catalogo

>[!NOTE]
>
> Il Dashboard di sincronizzazione del catalogo è ora il Dashboard di gestione dati. Questo dashboard rinnovato ora supporta [[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0+, [[!DNL Live Search]](../live-search/overview.md) v4.1.0+ e [[!DNL Catalog Service]](../catalog-service/overview.md) v1.17+. I clienti possono ottenere Data Management Dashboard aggiornando all’ultima versione di uno di questi servizi. Ulteriori informazioni sono disponibili nella documentazione di [Data Management Dashboard](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=it). Questo argomento corrente rimane valido per gli utenti che devono ancora effettuare l’aggiornamento e che dispongono ancora della dashboard Sincronizzazione catalogo.

Adobe Commerce utilizza gli indicizzatori per compilare i dati del catalogo nelle tabelle. Il processo viene attivato automaticamente da [eventi](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html?lang=it#events-that-trigger-full-reindexing), ad esempio una modifica al prezzo di un prodotto o al livello di inventario.

Il servizio Catalog Sync sposta i dati del prodotto da un&#39;istanza [!DNL Adobe Commerce] alla piattaforma [!DNL Commerce Services] su base continuativa per mantenere aggiornati i dati. Ad esempio, [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) richiede le informazioni del catalogo corrente per restituire con precisione i consigli con nomi, prezzi e disponibilità corretti. Utilizzare il dashboard _Sincronizzazione catalogo_ per osservare e gestire il processo di sincronizzazione o l&#39;interfaccia della riga di comando per attivare una sincronizzazione del catalogo e reindicizzare i dati del prodotto per l&#39;utilizzo da parte di [!DNL Commerce Services]. Vedi [Riferimento interfaccia riga di comando](../data-export/data-export-cli-commands.md) nella _Guida all&#39;esportazione dati SaaS_.

## Accesso al dashboard di sincronizzazione del catalogo

Per accedere al dashboard di sincronizzazione catalogo, seleziona **Sistema** > _Trasferimento dati_ > **Sincronizzazione catalogo**.

Con il dashboard **Sincronizzazione catalogo** puoi:

- Visualizza lo stato di sincronizzazione (**In corso**, **Completato**, **Non riuscito**)
- Visualizza il numero totale di prodotti sincronizzati
- Cerca i prodotti sincronizzati per visualizzarne lo stato corrente
- Cerca nel catalogo del negozio per nome, SKU, ecc.
- Visualizza i dettagli del prodotto sincronizzato in JSON per diagnosticare una discrepanza di sincronizzazione
- Riavvia il processo di sincronizzazione

### Ultima sincronizzazione

Segnala uno stato di sincronizzazione di:

- **Operazione completata** - Visualizza la data e l&#39;ora di completamento della sincronizzazione e il numero di prodotti aggiornati
- **Non riuscito** - Visualizza la data e l&#39;ora del tentativo di sincronizzazione
- **In corso** - Visualizza la data e l&#39;ora dell&#39;ultima sincronizzazione completata

Il processo di sincronizzazione del catalogo viene eseguito automaticamente ogni ora. Se nella vetrina non sono visualizzati i prodotti previsti o se i prodotti non riflettono le modifiche recenti apportate, è possibile risolvere [problemi di sincronizzazione del catalogo](#resolvesync).

### Prodotti sincronizzati

Visualizza il numero totale di prodotti sincronizzati dal catalogo [!DNL Commerce]. Dopo la sincronizzazione iniziale, solo i prodotti modificati devono essere sincronizzati.

## Risincronizza {#resync}

Se è necessario avviare una risincronizzazione del catalogo prima che venga eseguita la sincronizzazione oraria pianificata, è possibile forzare una risincronizzazione.

>[!NOTE]
>
> L&#39;imposizione di una risincronizzazione attiva una risincronizzazione dell&#39;intero catalogo prodotti, che può aumentare il carico sulle risorse hardware.

1. Dal dashboard _Sincronizzazione catalogo_, selezionare **Impostazioni**.

   Viene visualizzata la pagina _Impostazioni sincronizzazione catalogo_.

1. Nella sezione _Risincronizza dati_ fare clic su [!UICONTROL Resync].

   [!DNL Commerce] sincronizza il catalogo durante la prossima finestra di sincronizzazione pianificata. A seconda delle dimensioni del catalogo, questa operazione può richiedere molto tempo.

## Prodotti catalogo sincronizzati

Nella tabella **Prodotti catalogo sincronizzati** vengono visualizzate le informazioni seguenti.

| Campo | Descrizione |
|---|---|
| ID | Identificatore univoco del prodotto |
| Nome | Nome vetrina del prodotto |
| Tipo | Identifica il tipo di prodotto, ad esempio semplice, configurabile o scaricabile |
| Ultima esportazione | Data dell’ultima esportazione del prodotto dal catalogo |
| Ultima modifica | Data dell’ultima modifica del prodotto nel catalogo |
| SKU | Visualizza l&#39;unità di gestione delle scorte per il prodotto |
| Prezzo | Prezzo del prodotto |
| Visibilità | Impostazione di visibilità di un prodotto come definito nel catalogo [!DNL Commerce] |

## Risolvi problemi di sincronizzazione catalogo {#resolvesync}

Consulta [Registri e risoluzione dei problemi](../data-export/troubleshooting-logging.md#troubleshooting) nella _Guida all&#39;esportazione dei dati SaaS_.
