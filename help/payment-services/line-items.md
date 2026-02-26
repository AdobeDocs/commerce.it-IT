---
title: Elementi riga per  [!DNL Payment Services]
description: Scopri gli elementi riga per  [!DNL Payment Services]  e come visualizzare gli elementi riga nel dashboard esercente.
feature: Payments, Paas, Saas
role: User
exl-id: f690ff94-f83d-4525-9d52-1dea25a71060
source-git-commit: 6727102c54e0ac81df289ecd66ec61156662b8b9
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Elementi riga per [!DNL Payment Services]

Gli elementi riga per [!DNL Payment Services] sono gli elementi inclusi in un ordine. Queste voci forniscono informazioni quali:

* Dettagli prodotto
* Quantità
* Prezzo (comprese tasse, sconti e altre informazioni rilevanti)

Queste informazioni sono utili per il servizio clienti, la gestione degli ordini e la fatturazione corretta.

## Configurare gli elementi riga

Gli elementi riga sono abilitati per impostazione predefinita per [!DNL Payment Services]. Per configurare:

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.

1. Vai a **[!UICONTROL Sales]** e seleziona **[!UICONTROL Payment Methods]**.

1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.

1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione&#x200B;_[!UICONTROL Line Items]_.

1. Per **[!UICONTROL Line Items Enabled]**, selezionare `Yes` per abilitare (impostazione predefinita) o `No` per disabilitare gli elementi riga.

1. Fai clic su **[!UICONTROL Save Config]** per salvare le modifiche.

>[!IMPORTANT]
>
> Se disponi di estensioni di terze parti che aggiungono agli ordini tariffe personalizzate (come le tariffe di gestione), potresti dover disabilitare le voci. [!DNL Payment Services] calcola gli articoli linea in base ai componenti ordine standard di Commerce (articoli, imposte, spedizione e sconti). Le commissioni di terze parti non riconosciute da [!DNL Payment Services] possono causare una mancata corrispondenza tra il totale della riga e il totale dell&#39;ordine, che potrebbe impedire il completamento dell&#39;estrazione.

## Visualizza righe

Per visualizzare gli elementi riga:

1. Passa alla [dashboard esercente PayPal](https://www.paypal.com/merchant/){target=_blank}.

1. Fai clic su **Attività** > **Tutte le transazioni**.

1. Seleziona l’ordine desiderato e visualizzane gli elementi:

   > Esempio di elementi riga nella vista del dashboard acquirente

   ![Visualizzazione elementi riga](assets/paypal-shopper-dashboard-line-items-view.png){width="500" zoomable="yes"}

## Attributi degli elementi riga

Le voci vengono generate quando l&#39;ordine viene effettuato tramite Adobe Commerce e le informazioni vengono inviate a PayPal, con i seguenti attributi:

| Attributo | Tipo di dati | Descrizione |
| --- | --- | --- |
| `name` | Stringa! | Il nome dell&#39;elemento. Se un articolo ha più di una linea a causa di quantità multiple o di un problema di arrotondamento delle imposte, il nome dell&#39;articolo rimane invariato per tutte le linee, ma il prezzo visualizzato può variare leggermente a causa dell&#39;arrotondamento. |
| `unit_amount` | Oggetto! | Il prezzo o il tasso unitario dell&#39;articolo. Include i seguenti attributi: `currency_code` e `value`. |
| `tax` | Oggetto | Imposta sull&#39;articolo per ogni unità. Include i seguenti attributi: `currency_code` e `value`. |
| `quantity` | Stringa! | Quantità dell&#39;articolo. Sarà un numero intero. |
| `description` | Stringa | Descrizione dettagliata dell&#39;articolo. |
| `sku` | Stringa | L&#39;unità di gestione delle scorte (o SKU) dell&#39;articolo. |
| `url` | Stringa | `URL` per l&#39;elemento da acquistare. Visibile all&#39;acquirente e utilizzato nelle esperienze dell&#39;acquirente. |
| `upc` | Oggetto | Codice universale del prodotto (o UPC) dell’articolo. |
| `category` | Stringa | Tipo di categoria dell&#39;articolo. |

### Attributi `unit_amount`

L&#39;oggetto `unit_amount` contiene i seguenti attributi:

| Attributo | Tipo di dati | Descrizione |
| --- | --- | --- |
| `currency_code` | Stringa! | Codice valuta ISO-4217 di [tre caratteri](https://developer.paypal.com/api/rest/reference/currency-codes/) che identifica la valuta. |
| `value` | Stringa! | Indica il valore dell&#39;elemento. `currency_code` determina il numero richiesto di cifre decimali, se presenti. |

### Attributi `tax`

L&#39;oggetto `tax` contiene i seguenti attributi:

| Attributo | Tipo di dati | Descrizione |
| --- | --- | --- |
| `currency_code` | Stringa! | Codice valuta ISO-4217 di [tre caratteri](https://developer.paypal.com/api/rest/reference/currency-codes/) che identifica la valuta. |
| `value` | Stringa! | Indica il valore dell&#39;elemento. Dipende da ogni `currency_code` per il numero richiesto di cifre decimali. |

### Attributi `upc`

L&#39;oggetto `upc` contiene i seguenti attributi:

| Attributo | Tipo di dati | Descrizione |
| --- | --- | --- |
| `type` | stringa! | Il tipo di UPC. |
| `code` | stringa! | Il codice prodotto UPC dell’articolo. |

+++Esempio di elementi riga

```json
{
    "name": "Crown Summit Backpack - 1",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD"
        "value": "3.13"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
},
{
    "name": "Crown Summit Backpack - 2",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD",
        "value": "3.14"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
}
```

+++

Per ulteriori informazioni su questi campi e sulle relative limitazioni, consulta la [documentazione per gli sviluppatori di PayPal sulle righe](https://developer.paypal.com/docs/api/orders/v2/#definition-line_item){target=_blank}.

## Gestisci righe

Adobe Commerce [calcola l&#39;imposta in base all&#39;importo totale per ogni riga](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/site-store/taxes/taxes#warning-messages){target=_blank}. Ciò può causare problemi di arrotondamento se vengono ordinate più quantità dello stesso articolo o se nel catalogo vengono visualizzati prezzi comprensivi di imposte. In questi casi, la quantità totale può essere divisa in due righe, ma la quantità sarà uguale al totale degli articoli ordinati.

> Esempio di elementi riga con problemi di arrotondamento nella vista dashboard esercente

![Visualizzazione elementi riga](assets/line-items-example.png){width="600" zoomable="yes"}

+++Come Adobe Commerce calcola un problema di arrotondamento nelle righe

Gli elementi riga per [!DNL Payment Services] bilanciano questo problema di arrotondamento in modo che il valore `unit_amount` o `unit_tax` corrisponda all&#39;importo totale per l&#39;ordine. Per risolvere il problema di arrotondamento, un elemento può essere diviso in due righe:

* Quando il problema di arrotondamento viene visualizzato su `unit_amount`, l&#39;esercente dovrebbe notare una differenza nel prezzo di questa linea aggiuntiva.
* Quando il problema di arrotondamento viene visualizzato su `unit_tax`, non verrà visualizzata alcuna differenza sui singoli elementi di riga perché `tax` non è visualizzato nella griglia, ma solo come totale nella parte inferiore.

+++
