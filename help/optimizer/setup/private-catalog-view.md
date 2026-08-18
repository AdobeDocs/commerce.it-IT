---
title: Visualizzazioni catalogo privato
description: Scopri come creare una visualizzazione di catalogo privata abilitando Catalog Protection in modo che solo le richieste con un token firmato valido possano recuperare i dati relativi ai prodotti e ai prezzi.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 16e3405e1500dfd39603b1e300f4625e5a57cf02
workflow-type: tm+mt
source-wordcount: 642
ht-degree: 0%

---

# Visualizzazioni di cataloghi privati

Per impostazione predefinita, una [visualizzazione catalogo](catalog-view.md) è pubblica. Abilita la protezione del catalogo in una visualizzazione catalogo per limitare l’accesso alle richieste che includono un token firmato valido.

La protezione del catalogo si applica solo alla vista catalogo selezionata. Non modifica i criteri o i livelli della vista. La visualizzazione è limitata a un singolo listino prezzi dedicato. Vedere [Limitazione del listino prezzi dedicato alle visualizzazioni di cataloghi privati](#price-book-restriction-on-private-catalog-views).

Consulta i [Casi d&#39;uso per le chiavi di accesso con restrizioni](restricted-access-keys.md#restricted-access-key-use-cases) per esempi su quando proteggere una vista catalogo.

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

## Proteggere una vista catalogo

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

Se [!UICONTROL Catalog Protection] è abilitato e tutte le chiavi assegnate scadono, la vista catalogo diventa inaccessibile. Gli storefront che si basano su questa vista catalogo non possono servire i dati da essa. Assegna una nuova chiave non scaduta per ripristinare l’accesso. Per istruzioni, vedere [Ruotare le chiavi](restricted-access-keys.md#rotate-a-key).

>[!IMPORTANT]
>
>La creazione e la gestione automatica delle chiavi tramite Adobe Commerce e il connettore Adobe Commerce Optimizer non sono ancora disponibili.

## Altri argomenti correlati

- [Visualizzazioni catalogo](catalog-view.md): scopri come le visualizzazioni catalogo organizzano il catalogo prodotti per struttura aziendale, criteri e prezzi.
- [Chiavi di accesso limitate](restricted-access-keys.md)—Creare, assegnare e ruotare le chiavi utilizzate per firmare i token per la protezione del catalogo.
