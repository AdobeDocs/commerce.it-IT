---
title: Visualizzazioni catalogo privato
description: Scopri in che modo le visualizzazioni del catalogo privato limitano l’accesso ai dati del catalogo, vengono create automaticamente per i cataloghi condivisi B2B o vengono configurate manualmente con Catalog Protection.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e [!DNL Adobe Commerce Optimizer] (infrastruttura SaaS gestita da Adobe)."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%
---
# Visualizzazioni di cataloghi privati

Per impostazione predefinita, una [visualizzazione catalogo](catalog-view.md) è pubblica. Limita l’accesso a una vista catalogo in modo che solo le richieste con un token firmato valido possano recuperare i relativi dati.

Una vista catalogo diventa privata in uno dei due modi seguenti:

- [!BADGE Private Beta]{type=Caution tooltip="Richiede l’estensione B2B del connettore Adobe Commerce Optimizer, attualmente in versione beta privata."} **Automaticamente, per i cataloghi condivisi B2B**. Per le distribuzioni Commerce che utilizzano l&#39;integrazione [!DNL Adobe Commerce Optimizer Connector] con l&#39;estensione B2B, le visualizzazioni del catalogo privato vengono create e configurate automaticamente, in base alla configurazione del catalogo condiviso in [!DNL Adobe Commerce]. Vedi [Visualizzazioni automatiche di cataloghi privati per cataloghi condivisi B2B](#automatic-private-catalog-views-for-b2b-shared-catalogs).

- **Manualmente, per qualsiasi vista catalogo**. Per limitare l&#39;accesso a una vista catalogo che sarebbe altrimenti pubblica, inclusa una vista catalogo B2C, seguire la procedura descritta in [Proteggere una vista catalogo](#protect-a-catalog-view). Consulta [Casi d&#39;uso con chiave di accesso limitato](restricted-access-keys.md#restricted-access-key-use-cases) per esempi, come portali per partner e anteprime pre-release.

La protezione del catalogo si applica solo alla vista catalogo selezionata. Non modifica i criteri o i livelli della vista. La visualizzazione è limitata a un singolo listino prezzi dedicato. Vedere [Limitazione del listino prezzi dedicato alle visualizzazioni di cataloghi privati](#price-book-restriction-on-private-catalog-views).

## Comprendere il limite di protezione

La protezione del catalogo si applica solo alla visualizzazione del catalogo in cui è abilitata. Protegge le richieste di cataloghi e di ricerca ma non modifica i criteri o i livelli della visualizzazione, non protegge altre visualizzazioni di catalogo né protegge le operazioni di carrello, pagamento o ordine.

Il back-end Commerce connesso deve applicare in modo indipendente l’idoneità all’acquisto.

## Limitazione del listino prezzi dedicato alle visualizzazioni di cataloghi privati

Una vista catalogo privata può fare riferimento a un solo listino prezzi dedicato. Questo differisce da una vista catalogo pubblica, che può utilizzare più listini prezzi.

Quando [!UICONTROL Catalog Protection] è abilitato, il selettore del listino prezzi nel modulo di visualizzazione catalogo passa da un controllo a selezione multipla a un controllo a selezione singola (pulsante di opzione).

![Limitazione del listino prezzi della visualizzazione catalogo privato](../assets/catalog-view-private-pricebook-restrictions.png)

- Se si abilita [!UICONTROL Catalog Protection] in una visualizzazione catalogo a cui sono assegnati più listini prezzi, non sarà possibile salvare la visualizzazione fino a quando non si rimuove tutti i listini prezzi tranne uno.
- Se in precedenza è stata salvata una vista catalogo privata con più assegnazioni del listino prezzi dedicato prima dell&#39;esistenza di questa restrizione, la configurazione della vista catalogo non viene modificata automaticamente. Tuttavia, alla successiva modifica della vista, è necessario rimuovere tutti i listini prezzi tranne uno prima di poter salvare gli aggiornamenti.

In ciascuno di questi casi, [!DNL Adobe Commerce Optimizer] visualizza il seguente messaggio di convalida: `A protected catalog view can use only one price book. Select 'Single price book only' to continue.`

Le visualizzazioni del catalogo pubblico non sono interessate da questa restrizione e possono continuare a fare riferimento a più listini prezzi.

## Visualizzazioni automatiche di cataloghi privati per cataloghi condivisi B2B

[!BADGE Private Beta]{type=Caution tooltip="Richiede l’estensione B2B del connettore Adobe Commerce Optimizer, attualmente in versione beta privata."}

Per le distribuzioni integrate con [!DNL Adobe Commerce Optimizer Connector for B2B] per il supporto di cataloghi condivisi, l&#39;estensione crea e configura automaticamente le visualizzazioni del catalogo privato, in base alla configurazione del catalogo condiviso in [!DNL Adobe Commerce]. Questa configurazione include la vista catalogo, il criterio, una chiave di accesso con restrizioni iniziale e un riferimento al listino prezzi dedicato. Con questa configurazione, puoi gestire le chiavi di accesso con restrizioni dalla pagina Amministratore Commerce **Chiavi di accesso con restrizioni** (**Sistema** > **Trasferimento dati**). Per informazioni dettagliate, vedere [Modifiche al catalogo condiviso B2B](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes) nella Guida all&#39;integrazione *[!DNL Adobe Commerce Optimizer Connector]*.

Se non si utilizzano cataloghi condivisi B2B, ad esempio per proteggere una visualizzazione di catalogo per un portale partner o per l&#39;anteprima pre-release, utilizzare le istruzioni in [Proteggi una visualizzazione di catalogo](#protect-a-catalog-view) per configurarne manualmente una.

## Proteggere una vista catalogo

>[!NOTE]
>
>Ignorare questa procedura per le visualizzazioni catalogo associate ai cataloghi condivisi B2B gestiti da [!DNL Adobe Commerce Optimizer Connector for B2B]. Vedi [Visualizzazioni automatiche di cataloghi privati per cataloghi condivisi B2B](#automatic-private-catalog-views-for-b2b-shared-catalogs).

Prima di iniziare, [crea una chiave ad accesso limitato](restricted-access-keys.md) dalla chiave pubblica generata dall&#39;applicazione client.

1. Nella visualizzazione del catalogo creare o modificare il modulo, impostare **[!UICONTROL Catalog Protection]** su **[!UICONTROL Enabled]**.

1. In **[!UICONTROL Restricted Access Keys]**, selezionare fino a tre [chiavi di accesso con restrizioni](restricted-access-keys.md) da assegnare a questa visualizzazione catalogo.

   ![Protezione catalogo abilitata nel modulo di modifica della visualizzazione catalogo, con una chiave di accesso con restrizioni assegnata](../assets/catalog-view-protected.png){width="70%" zoomable="yes"}

1. Fare clic su **[!UICONTROL Save catalog view]**.

   La vista catalogo è ora protetta. Solo le richieste contenenti un token firmato valido da una chiave assegnata possono recuperarne i dati.

   >[!NOTE]
   >
   >Attendere fino a cinque minuti per rendere effettive le modifiche alla configurazione di Protezione catalogo.

## Verificare che l’accesso sia applicato

Per confermare che una vista del catalogo privato rifiuta le richieste non autorizzate, chiama il relativo [endpoint GraphQL](../get-started.md#get-instance-details) con e senza un token firmato, utilizzando le intestazioni seguenti:

| Intestazione | Finalità |
| --- | --- |
| `AC-View-ID` | Vista catalogo da interrogare. |
| `AC-Price-Book-ID` | Il listino prezzi da applicare. |
| `AC-Catalog-View-Access-Token` | L’autorizzazione per la verifica JWT firmata per la vista catalogo. |

Una richiesta senza un token valido restituisce un errore GraphQL invece dei dati di catalogo, ad esempio:

```json
{
  "errors": [
    {
      "message": "Access key validation failed: Missing token",
      "extensions": { "x-commerce-exception": "access-key-invalid" }
    }
  ]
}
```

Una richiesta con un token firmato da una chiave assegnata e non scaduta restituisce i dati del catalogo come previsto. Per informazioni dettagliate sulla firma di un JWT e sulla chiamata all&#39;API Merchandising, consulta la [documentazione per gli sviluppatori](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication).

## Gestire le chiavi di accesso con restrizioni

Se [!UICONTROL Catalog Protection] è abilitato e tutte le chiavi assegnate scadono, la visualizzazione del catalogo diventa inaccessibile. Gli storefront che si basano su questa vista catalogo non possono fornire dati da essa. Assegna una nuova chiave non scaduta per ripristinare l’accesso. Per istruzioni, vedere [Ruotare le chiavi](restricted-access-keys.md#rotate-a-key).

>[!NOTE]
>
>Per le distribuzioni integrate con l&#39;estensione [!DNL Adobe Commerce Optimizer Connector for B2B], è possibile gestire le chiavi di accesso dalla pagina **Chiavi di accesso limitate** dell&#39;amministratore di Commerce (**Sistema** > **Trasferimento dati**). Per informazioni dettagliate, vedere [Gestione delle chiavi di accesso con restrizioni](../../aco-connector/restricted-access-keys.md) nella Guida all&#39;integrazione di *[!DNL Adobe Commerce Optimizer Connector]*.

## Altri argomenti correlati

- [Visualizzazioni catalogo](catalog-view.md): scopri come le visualizzazioni catalogo organizzano il catalogo prodotti per struttura aziendale, criteri e prezzi.
- [Chiavi di accesso limitate](restricted-access-keys.md)—Creare, assegnare e ruotare le chiavi utilizzate per firmare i token per la protezione del catalogo.
