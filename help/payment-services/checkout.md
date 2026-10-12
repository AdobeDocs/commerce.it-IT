---
title: Estrai in [!DNL Payment Services]
description: Personalizza l'estrazione di [!DNL Payment Services] in base alle esigenze del cliente.
feature: Payments, Checkout, Paas, Saas
exl-id: 47df165f-2145-4e0e-b272-54b8e768cf19
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%
---

# Estrai in [!DNL Payment Services]

È possibile configurare l&#39;estrazione per Adobe Commerce [!DNL Payment Services] in base alle proprie esigenze. Funzionalità quali [svuotamento automatico dell&#39;ordine](#order-auto-voided-if-error) e [vaulting di carte di credito](#credit-card-vaulting) garantiscono agli acquirenti un&#39;esperienza utente fluida.

## Ordine annullato automaticamente in caso di errore

Se si verifica un errore durante l&#39;estrazione, [!DNL Payment Services] annulla/annulla automaticamente l&#39;ordine.

Nella pagina di pagamento viene visualizzato un messaggio di errore per l’acquirente. Il messaggio può variare.

![Errore durante l&#39;estrazione](assets/user-checkout-error.png "Errore durante l&#39;estrazione"){width="600" zoomable="yes"}

Un commento relativo all&#39;ordine annullato viene visualizzato anche nell&#39;amministratore per un [ordine](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/order-management/orders/orders?lang=en) specifico.

![Commento ordine annullato in Admin per ordine](assets/admin-checkout-error.png "Commento ordine annullato in Admin per ordine"){width="600" zoomable="yes"}

Se un acquirente ottiene l&#39;autorizzazione per un ordine, ma l&#39;ordine non è stato creato e convertito in `Capture`, l&#39;ordine viene annullato automaticamente. Questo processo assicura che non venga riservato alcun credito sulla carta di credito dell&#39;acquirente ed evita la commissione che si verifica quando l&#39;autorizzazione viene annullata al termine del periodo standard di 29 giorni.

>[!NOTE]
>
>L&#39;annullamento automatico dell&#39;ordine si verifica solo quando il cliente utilizza un metodo di pagamento impostato sulla modalità `Authorize` e non sulla modalità `Authorize and Capture`.

## Ritira dalla pagina del prodotto

Quando un cliente effettua il check-out direttamente dalla pagina del prodotto utilizzando i pulsanti PayPal o [!DNL Pay Later], viene acquistato solo l&#39;articolo rappresentato nella pagina del prodotto corrente. Gli articoli già presenti nel carrello del cliente non vengono aggiunti al flusso di pagamento e non vengono acquistati.

Questa funzione consente al cliente di acquistare rapidamente l’articolo che sta visualizzando, mantenendo gli articoli precedentemente aggiunti al carrello.
Se il cliente annulla l’ordine, l’articolo nella pagina del prodotto corrente viene aggiunto al carrello del cliente.

Quando un cliente accede al flusso di pagamento dalla pagina del prodotto, la pagina di pagamento viene semplificata: la visualizzazione mostra solo i dati e le opzioni relativi all’ordine.

## Vaulting con carta di credito

Gli acquirenti possono vagliare, o &quot;salvare&quot;, le informazioni sulla loro carta di credito per acquisti futuri a livello del sito web (qualsiasi negozio all&#39;interno dello stesso account del commerciante).

Per ulteriori informazioni, consulta [Vaulting carta di credito](vaulting.md)
