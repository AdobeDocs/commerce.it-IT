---
title: Estrai in [!DNL Payment Services]
description: Personalizza [!DNL Payment Services] l'estrazione in base alle esigenze del cliente.
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Estrai in [!DNL Payment Services]

È possibile configurare l&#39;estrazione per Adobe Commerce [!DNL Payment Services] in base alle proprie esigenze. Funzionalità quali [svuotamento automatico dell&#39;ordine](#order-auto-voided-if-error) e [vaulting di carte di credito](#credit-card-vaulting) garantiscono agli acquirenti un&#39;esperienza utente fluida.

## Ordine annullato automaticamente in caso di errore

Se si verifica un errore durante l&#39;estrazione, [!DNL Payment Services] annulla/annulla automaticamente l&#39;ordine.

Nella pagina di pagamento viene visualizzato un messaggio di errore per l’acquirente. Il messaggio può variare.

![Errore durante l&#39;estrazione](assets/user-checkout-error.png "Errore durante l&#39;estrazione"){width="600" zoomable="yes"}

Un commento relativo all&#39;ordine annullato viene visualizzato anche nell&#39;amministratore per un [ordine](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/orders.html?lang=en) specifico.

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
