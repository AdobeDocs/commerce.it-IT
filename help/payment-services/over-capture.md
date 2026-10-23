---
title: Overcapture
description: Scopri i requisiti di overcapture e la configurazione per l’estensione Payment Services.
role: Admin, User
level: Intermediate
feature: Payments, Paas
source-git-commit: d2bcc58f34af50f26d4a4f082e5b3fc30089ab58
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%
---
# Overcapture

L&#39;overcapture consente ai commercianti idonei con un contratto di overcapture PayPal di acquisire più dell&#39;importo originariamente autorizzato quando fatturano un ordine. Ad esempio, l&#39;importo finale potrebbe aumentare a causa di adeguamenti basati sul peso o di modifiche nei costi dei materiali tra l&#39;autorizzazione e l&#39;evasione.

PayPal determina il limite di overcapture per ogni account esercente. L&#39;abilitazione dell&#39;overcapture in [!DNL Payment Services] non stabilisce un accordo o non aumenta il limite approvato da PayPal.

>[!NOTE]
>
>In questo argomento viene descritta l&#39;overcapture nell&#39;estensione [!DNL Payment Services]. Per [!DNL Adobe Commerce as a Cloud Service], vedere [Quantità di acquisizione personalizzate](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) per i requisiti di disponibilità e abilitazione separati.

## Prerequisiti

Prima di abilitare l&#39;overcapture:

* L&#39;overcapture è disponibile solo in [!DNL Payment Services] 2.17.0 o versione successiva.
* L&#39;overcapture è disponibile solo per le aziende con sede negli Stati Uniti. I [requisiti di overcapture di PayPal (PSD2)](https://www.paypal.com/us/cshelp/article/overcapture-requirements-psd2-help954) si applicano anche ai commercianti con sede negli Stati Uniti che vendono ad acquirenti PayPal nello Spazio economico europeo (SEE).
* L&#39;overcapture non è disponibile per i metodi di pagamento alternativi (APM).
* Ottieni un accordo di overcapture con PayPal e conferma il limite approvato per il tuo account esercente con il tuo responsabile di PayPal.
* Impostare **[!UICONTROL Payment Action]** del metodo di pagamento su `Authorize`. L&#39;overcapture si applica agli ordini autorizzati acquisiti successivamente durante la fatturazione, non agli ordini acquisiti automaticamente con `Authorize and Capture`. Vedi [Imposta [!DNL Payment Services] come metodo di pagamento](production.md#set-payment-services-as-payment-method).

## Abilita overcapture

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Nel pannello a sinistra, espandi **[!UICONTROL Sales]** e scegli **[!UICONTROL Payment Methods]**.
1. Seleziona il sito web da configurare utilizzando il selettore dell’ambito di archiviazione.
1. Espandere la sezione _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Nella sezione _[!UICONTROL Payment Services]_, espandere la sezione&#x200B;_[!UICONTROL General Configuration]_.
1. Imposta **[!UICONTROL Over Capture Enabled]** su `Yes`.
1. Fai clic su **[!UICONTROL Save Config]** per salvare le modifiche.
1. Passare a **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, quindi fare clic su **[!UICONTROL Flush Cache]** per aggiornare tutte le cache non valide.

## Acquisire un pagamento autorizzato

L&#39;overcapture avviene durante la fatturazione nell&#39;amministratore. L&#39;importo di acquisizione richiesto deve essere compreso nel limite approvato da PayPal per il tuo account esercente. Vedere [Creare una fattura](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice) per il flusso di lavoro di fatturazione standard.

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. Apri un ordine con un pagamento autorizzato che non è ancora stato acquisito.
1. Fare clic su **[!UICONTROL Invoice]**.
1. Nel campo Importo acquisizione personalizzata immettere l&#39;importo totale da acquisire. Ad esempio, se l&#39;importo autorizzato è USD 100 e l&#39;addebito finale concordato è USD 110, immettere `110` e non `10`. L&#39;importo richiesto deve essere compreso nel limite approvato da PayPal.
1. Selezionare l&#39;acquisizione in linea per la fattura per richiedere il pagamento tramite il provider di servizi di pagamento.
1. Esaminare la fattura e fare clic su **[!UICONTROL Submit Invoice]**.

### Acquisire utilizzando l’API Fattura

Utilizza l&#39;endpoint standard [Crea una fattura](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-create-invoice):

```http
POST /rest/<store_code>/V1/order/<orderId>/invoice
```

Utilizza il codice store per l’ordine e l’ID interno dell’ordine. Eseguire l&#39;autenticazione con un token di integrazione o amministratore autorizzato e impostare `Content-Type: application/json`.

Il payload di esempio seguente richiede una fattura completa con acquisizione online di USD 110 per un ordine autorizzato per USD 100, a condizione che il contratto PayPal del commerciante consenta tale importo:

```json
{
  "capture": true,
  "notify": false,
  "arguments": {
    "extension_attributes": {
      "custom_capture_amount": 110
    }
  }
}
```

In questo esempio:

1. `capture` richiede l&#39;acquisizione online.
1. `notify` controlla se Commerce invia l&#39;e-mail di notifica della fattura.
1. `custom_capture_amount` è l&#39;importo finale da acquisire, non l&#39;aumento rispetto all&#39;importo autorizzato.

## Risolvere i problemi relativi a un&#39;acquisizione rifiutata

Se PayPal rifiuta una richiesta di overcapture:

* Conferma che sia attivo un contratto di recupero in eccesso per il conto PayPal utilizzato per il pagamento.
* Verifica che l’importo richiesto rientri nel limite approvato. Se supera il limite, richiedi un importo inferiore o contatta il tuo account manager PayPal per discutere di un aumento.
