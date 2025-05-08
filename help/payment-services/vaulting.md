---
title: Vaulting con carta di credito
description: Gli acquirenti possono archiviare (salvare) i dati della carta di credito per acquisti futuri.
exl-id: b4060307-ffcd-41cb-9b9d-a2fef02f23bd
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Vaulting con carta di credito

Convertire i clienti occasionali in clienti fedeli con il vaulting delle carte di credito. I clienti che hanno effettuato l’accesso possono salvare, o &quot;vaultare&quot;, le credenziali della carta di credito da utilizzare in un acquisto successivo per lo stesso o un altro negozio all’interno dello stesso account esercente.

## Abilita vaulting

Gli esercenti possono abilitare il vaulting delle carte di credito per i loro negozi nelle [!DNL Payment Services] [Impostazioni](settings.md#card-vaulting).

1. Nella barra laterale _Admin_, passa a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

1. Fare clic su **[!UICONTROL Settings]**.

1. Attiva/disattiva il selettore **[!UICONTROL Vault enabled]**. Per ulteriori informazioni, vedere [Abilita [!DNL Payment Services]](settings.md#enable-payment-services).

## Vaulting senza acquisto

I clienti connessi possono archiviare un metodo di pagamento nel dashboard **Il mio account**:

1. Accesso a **Il mio account** nella vetrina.

1. Passa a **[!UICONTROL Stored Payment Methods]** nella barra di navigazione a sinistra per visualizzare tutti i metodi di pagamento memorizzati.

   Per ulteriori informazioni, vedere [Metodi di pagamento memorizzati](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/stored-payment-methods).

1. Il cliente fa clic su **[!UICONTROL Add New Card]** per memorizzare una nuova scheda.

   ![Aggiungi nuova scheda](assets/add-new-card.png){width="400" zoomable="yes"}

   Il cliente deve fornire tutti i dettagli richiesti, come le informazioni sulla carta e sulla fatturazione, per archiviare il metodo di pagamento.
Tutti i metodi di pagamento con vaulting utilizzano la serie di indirizzi di fatturazione durante il vaulting della carta, che nel conto PayPal del cliente. Il cliente potrebbe visualizzare un indirizzo di fatturazione diverso da quello visualizzato in Commerce.

1. Fai clic su **[!UICONTROL Save New Card]**

   ![Metodi di pagamento memorizzati nel mio account](assets/stored-payment-methods.png){width="400" zoomable="yes"}

Le schede memorizzate possono essere utilizzate quando si effettua un ordine:

![Usa credenziali archiviate per acquisti futuri](assets/use-stored-card.png){width="400" zoomable="yes"}

### Elimina un metodo di pagamento memorizzato

I clienti possono eliminare facilmente le carte di credito archiviate da **Metodi di pagamento archiviati** in **Il mio account** facendo clic su **Elimina** per una carta specifica.

## Vaulting di un metodo di pagamento durante il pagamento

I clienti che hanno effettuato l’accesso possono effettuare il vaulting di una carta di credito durante il pagamento per utilizzarla in acquisti successivi nel negozio corrente o in altri negozi all’interno dello stesso account esercente:

![Archivia la carta di credito per un uso successivo](assets/save-card-for-later.png){width="400" zoomable="yes"}

Commerce memorizza un token che consente ai clienti di completare i pagamenti futuri recuperando le informazioni salvate sulla carta di credito. Il vaulting di una carta dal conto del cliente o durante il pagamento si tradurrà in token di pagamento diversi.

>[!WARNING]
>
> PayPal può attualmente memorizzare un massimo di cinque carte a pagamento.

## Utilizzare il vaulting in Amministrazione

Se un cliente dispone di una carta di credito precedentemente archiviata, un esercente può creare un ordine successivo per quel cliente nell&#39;Amministratore utilizzando uno di questi metodi di pagamento archiviato.

Puoi usare le carte ad archivio nell&#39;Amministratore solo se il cliente ha un account esistente e un token valido memorizzato nel sistema da un pagamento completato in precedenza.

Per creare un ordine nell’amministratore per un cliente utilizzando la sua carta di credito archiviata:

1. [Crea un ordine e aggiungi prodotti](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order.html).
1. In _[!UICONTROL Payment & Shipping Information]_, selezionare **[!UICONTROL Stored Cards]**&#x200B;come metodo di pagamento.
1. Seleziona il metodo di pagamento con carta di credito archiviata desiderato.
1. Dopo aver completato tutti gli altri passaggi necessari per l&#39;ordine, [invialo](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order.html?lang=en#step-3%3A-submit-the-order).

   ![Utilizza carta di credito archiviata in Amministratore per il cliente](assets/admin-vaultedcard.png){width="600" zoomable="yes"}

## Sicurezza

Le informazioni minime sulla carta di credito vengono condivise con l&#39;acquirente, che visualizza solo le ultime quattro cifre, la data di scadenza e il marchio della carta di credito archiviata. Le informazioni sulla carta di credito vengono archiviate con il provider di pagamenti per soddisfare gli standard di conformità [PCI](security.md#PCI-compliance).
