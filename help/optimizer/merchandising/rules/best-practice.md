---
title: Best practice per le regole di merchandising
description: Scopri le best practice per implementare le regole di merchandising per le pagine di ricerca, inserzioni predefinite e categorie.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: cc8d0879-c253-4ad4-8e7d-e066dff9112d
TQID: https://experienceleague.adobe.com/DrdrBBXeMyqQr16h1LrlSoet3F6ihn57LBmPFBUXmTs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 841e772971e7ec18d37fa8ba137b27b8950fc569
workflow-type: tm+mt
source-wordcount: 404
ht-degree: 0%

---

# Best practice per le regole di merchandising

Per ottimizzare la conversione e i ricavi, implementa **regole di ricerca** efficaci, una **regola di elenco predefinita** avanzata e **[regole di categoria](add.md#rule-types)** (versione beta). Regola le classificazioni utilizzando dati di vendita, azioni, promozioni e [classificazione intelligente](add.md#intelligent-ranking).

È fondamentale stabilire una regola **predefinita** ben ponderata. La [regola predefinita](overview.md#default-rule) determina il modo in cui i risultati della ricerca vengono inizialmente ordinati quando non si applica alcuna regola di ricerca più specifica, migliorando così l&#39;individuazione e la probabilità di acquisto. Esamina regolarmente in modo da tenere il passo con le esigenze e le campagne dei clienti.

## Suggerimenti per ottimizzare le regole di ricerca

- Aggiungi o incrementa prodotti con elevati volumi di vendita o attività di vendita recenti.
- Dai priorità ai prodotti con valutazioni elevate e recensioni positive.
- Assicurati che gli articoli in magazzino abbiano una classificazione più alta.
- Dare leggermente priorità ai prodotti con margini di profitto più elevati senza compromettere la rilevanza.
- Evidenzia i prodotti in vendita o inclusi nelle promozioni speciali.
- Impostare automaticamente le regole di ricerca durante i periodi di promozione o di vendita utilizzando l&#39;intervallo di date durante il periodo di promozione.
- Personalizza i risultati della ricerca in base al comportamento dei singoli acquirenti utilizzando [classificazione intelligente](add.md#intelligent-ranking), ad esempio &quot;consigliato per te&quot;, &quot;più visualizzato&quot; e così via.
- Quando è selezionata una strategia intelligente diversa da **Nessuno**, sintonizza **[Aumento classificazione intelligente](add.md#intelligent-ranking-boost)** per regola e convalida in **Verifica la regola** prima di pubblicare.
- Utilizza sempre il pannello &quot;Test della regola&quot; per visualizzare in anteprima come la tua strategia di classificazione intelligente influisce sui risultati effettivi della ricerca per query diverse.

## Suggerimenti per le regole di categoria

>[!IMPORTANT]
>
>Le regole di categoria sono in versione beta.

- Utilizza [regole di categoria](add.md#rule-types) nelle **pagine di categoria** con traffico elevato o margine elevato in cui l&#39;ordine curato è importante quanto la ricerca, ad esempio raccolte stagionali o reparti in primo piano.
- Allinea **classificazione intelligente** (ad esempio, di tendenza, più visualizzato) al modo in cui gli acquirenti sfogliano tale categoria; le pagine delle categorie non utilizzano il testo delle query di ricerca come fanno le regole di ricerca. Vedi [Classificazione intelligente](add.md#intelligent-ranking). Per i metodi intelligenti diversi da **Nessuno**, utilizza **[Incremento classificazione intelligente](add.md#intelligent-ranking-boost)** e anteprima categoria per ottimizzare la forza comportamentale per la regola di categoria.
- Applica **pin**, **boost** e **bury** in modo coerente con il piano della campagna; ricorda che le posizioni manuali di solito si applicano solo quando l&#39;acquirente utilizza l&#39;**ordinamento predefinito** per l&#39;inserzione. Vedi [Classificazione manuale](add.md#manual-ranking).
- Anteprima nel flusso di regole **categoria** nell&#39;editor e convalida nella vetrina dopo la pubblicazione, stessa disciplina utilizzata per il pannello &quot;Test della regola&quot; durante la ricerca.
