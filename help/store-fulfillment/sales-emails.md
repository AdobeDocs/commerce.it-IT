---
title: Modelli e-mail vendita
description: Configura i modelli e-mail transazionali per comunicare con i clienti e gli amministratori del negozio durante il processo di evasione degli ordini di ritiro dal negozio.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Communications, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---


# Modelli e-mail vendita

Store Fulfillment offre un set esteso di modelli e-mail transazionali per supportare i flussi di lavoro di ordine e evasione. Offrono comunicazioni e messaggi coerenti e automatizzati su tutti i canali, notificando agli amministratori di clienti e negozi le modifiche dello stato degli ordini, le istruzioni per gli ordini di prelievo in negozio e altro ancora.

I modelli e-mail per il completamento dell’archivio sono configurati con messaggi e impostazioni predefiniti. Gli amministratori di esercenti di Adobe Commerce possono gestire e modificare le configurazioni e selezionare i modelli e-mail per comunicare con i clienti in scenari diversi. Gli amministratori possono configurare e personalizzare anche i modelli.

Configurare i modelli e-mail per le vendite dall&#39;amministratore: **[!UICONTROL Stores > Configuration > Sales > Sales Emails]**.

## E-mail - Impostazioni generali

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrizione</strong></th>
<th><strong>Ambito</strong></th>
<th><strong>Obbligatorio</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Invio asincrono</strong></td>
<td>Determina se le e-mail di vendita vengono inviate in modo asincrono. Opzioni: <br/>**`Disabilita`** - (Predefinito) Le e-mail di vendita vengono inviate quando attivate da un evento. Utilizza l’impostazione predefinita per ottenere i tempi di comunicazione e risposta più rapidi per il ritiro dello store. <br/>**`Abilita`** - L'abilitazione di questa opzione consente di spostare in background i processi che gestiscono le notifiche di pagamento e di elaborazione dell'ordine in modo che vengano inviati a intervalli regolari predeterminati.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</tbody></table>

## Ordina pronto per il ritiro nello store

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrizione</strong></th>
<th><strong>Ambito</strong></th>
<th><strong>Obbligatorio</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Abilitato</strong></td>
<td>Questa e-mail viene inviata al cliente quando il responsabile del negozio ha completato il prelievo dell'ordine. Imposta su "No" per disabilitare la notifica e-mail. Se il modello e-mail è disattivato, ciò non impedisce al partner del negozio di prelevare un ordine.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Ordina pronto per il mittente dell'e-mail di ritiro</strong></td>
<td>L’identità del mittente utilizzata per inviare la notifica e-mail.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Ordine pronto per il modello di e-mail di ritiro</strong></td>
<td>Il modello di messaggio e-mail utilizzato per notificare i clienti registrati. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<td><strong>Ordine pronto per il modello di e-mail di ritiro per l'ospite</strong></td>
<td>Modello di messaggio e-mail utilizzato per inviare una notifica ai clienti guest. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Ordine pronto per il modello di e-mail di ritiro per il contatto di ritiro alternativo</strong></td>
<td>Il modello di messaggio e-mail utilizzato per notificare ulteriori contatti denominati nell’ordine. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Invia Ordine Pronto Per Il Ritiro Della Copia E-Mail A</strong></td>
<td>Un elenco delimitato da virgole di indirizzi e-mail per inviare una copia di ogni notifica.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Metodo Invia ordine pronto per la copia e-mail di ritiro</strong></td>
<td>Il metodo di copia delle e-mail, ovvero la copia carbone, da utilizzare.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</tbody></table>


## L&#39;ordine è stato ritirato nello Store

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrizione</strong></th>
<th><strong>Ambito</strong></th>
<th><strong>Obbligatorio</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Abilitato</strong></td>
<td>Questa e-mail viene inviata al cliente quando per confermare di aver ritirato l'ordine dal negozio. Imposta su "No" per disabilitare la notifica e-mail. Se il modello e-mail è disabilitato, non impedisce al cliente di ritirare un ordine.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>L'Ordine È Stato Ritirato Mittente E-Mail</strong></td>
<td>L’identità del mittente utilizzata per inviare la notifica e-mail.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>L'Ordine È Stato Ritirato Modello E-Mail</strong></td>
<td>Il modello di messaggio e-mail utilizzato per notificare i clienti registrati. Con l’integrazione viene fornito un modello predefinito</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<td><strong>L'ordine è stato ritirato Modello di Email per Ospite</strong></td>
<td>Modello di messaggio e-mail utilizzato per inviare una notifica ai clienti guest. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Invia È Stata Ritirata La Copia E-Mail A</strong></td>
<td>Un elenco delimitato da virgole di indirizzi e-mail per inviare una copia di ogni notifica.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Invia è stato selezionato metodo di copia e-mail</strong></td>
<td>Il metodo di copia delle e-mail, ovvero la copia carbone, da utilizzare.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</tbody></table>

## Ordine ritardato

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrizione</strong></th>
<th><strong>Ambito</strong></th>
<th><strong>Obbligatorio</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Abilitato</strong></td>
<td>Questa e-mail viene inviata al cliente per informarlo di un ritardo nell’elaborazione o nel prelievo dell’ordine presso il negozio di merchant. Imposta su "No" per disabilitare la notifica e-mail. Se il modello e-mail è disabilitato, la funzione non impedisce il ritardo di un ordine.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Ordina mittente e-mail ritardato
</strong></td>
<td>L’identità del mittente utilizzata per inviare la notifica e-mail.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Modello e-mail per ordine ritardato</strong></td>
<td>Il modello di messaggio e-mail utilizzato per notificare i clienti registrati. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<td><strong>Ordinare il modello di e-mail posticipato per l'ospite</strong></td>
<td>Modello di messaggio e-mail utilizzato per inviare una notifica ai clienti guest. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Invia Copia E-Mail Ritardata Dell’Ordine A</strong></td>
<td>Un elenco delimitato da virgole di indirizzi e-mail per inviare una copia di ogni notifica.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Metodo di invio della copia ritardata dell'ordine</strong></td>
<td>Il metodo di copia delle e-mail, ovvero la copia carbone, da utilizzare.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</tbody></table>



## Ordine annullato

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrizione</strong></th>
<th><strong>Ambito</strong></th>
<th><strong>Obbligatorio</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Abilitato</strong></td>
<td>Questa e-mail viene inviata al cliente per informarlo che il suo ordine è stato annullato presso il negozio di vendita. Impostare su <code>No</code> per disabilitare la notifica e-mail. Se il modello e-mail è disabilitato, questa funzione non impedisce l’annullamento di un ordine.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Mittente e-mail annullato dall'ordine
</strong></td>
<td>L’identità del mittente utilizzata per inviare la notifica e-mail.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Modello e-mail per ordine annullato</strong></td>
<td>Il modello di messaggio e-mail utilizzato per notificare i clienti registrati. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<td><strong>Ordine annullato per ospite</strong></td>
<td>Modello di messaggio e-mail utilizzato per inviare una notifica ai clienti guest. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Invia la copia e-mail annullata dell'ordine a</strong></td>
<td>Un elenco delimitato da virgole di indirizzi e-mail per inviare una copia di ogni notifica.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Metodo di copia annullata dell'ordine di invio</strong></td>
<td>Il metodo di copia delle e-mail, ovvero la copia carbone, da utilizzare.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</tbody></table>


## Ordine parzialmente annullato

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrizione</strong></th>
<th><strong>Ambito</strong></th>
<th><strong>Obbligatorio</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Abilitato</strong></td>
<td>Questa e-mail viene inviata al cliente per informarlo che parte dell’ordine è stato annullato presso il negozio di alimentari. Impostare su <code>No</code> per disabilitare la notifica e-mail. Se il modello e-mail è disabilitato, ciò non impedisce che un ordine venga parzialmente annullato.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Mittente e-mail parzialmente annullato dall'ordine
</strong></td>
<td>L’identità del mittente utilizzata per inviare la notifica e-mail.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Modello e-mail parzialmente annullato dall'ordine</strong></td>
<td>Il modello di messaggio e-mail utilizzato per notificare i clienti registrati. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<td><strong>Modello e-mail parzialmente annullato dall'ordine per contatto di ritiro alternativo</strong></td>
<td>Il modello di messaggio e-mail utilizzato per notificare ulteriori contatti denominati nell’ordine. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Ordine parzialmente annullato per l'ospite</strong></td>
<td>Modello di messaggio e-mail utilizzato per inviare una notifica ai clienti guest. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Invia copia e-mail parzialmente annullata a</strong></td>
<td>Un elenco delimitato da virgole di indirizzi e-mail per inviare una copia di ogni notifica.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Metodo di copia annullata parzialmente dell'ordine di invio</strong></td>
<td>Il metodo di copia delle e-mail, ovvero la copia carbone, da utilizzare.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</tbody></table>

## Spedisci al negozio

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrizione</strong></th>
<th><strong>Ambito</strong></th>
<th><strong>Obbligatorio</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>L'ordine ha il mittente dell'e-mail per i prodotti del Negozio</strong></td>
<td>E-mail inviata a personale commerciante specificato come rapporto aggregato di tutti gli ordini aperti che non possono essere prelevati in un negozio commerciale finché il loro inventario non è disponibile. </br></br> I commercianti possono utilizzare questo rapporto per avviare e gestire trasferimenti o rifornimenti di magazzino da punto di vendita. </br></br>Questa notifica si applica solo quando le funzionalità di [!DNL Ship-to-Store] sono abilitate.
</br></br>Questa etichetta non influisce sul vettore di spedizione selezionato o sulle relative etichette disponibili per il metodo di spedizione.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Destinatari e-mail del Negozio di spedizione</strong></td>
<td>Un elenco delimitato da virgole di indirizzi e-mail per inviare una copia di ogni notifica.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
<tr>
<td><strong>Modello e-mail</strong></td>
<td>Modello di messaggio e-mail utilizzato per notificare i destinatari. Con l’integrazione viene fornito un modello predefinito.</td>
<td>Visualizzazione store</td>
<td>No</td>
</tr>
</tbody></table>

>[!NOTE]
>
>Se consenti ordini inevasi, devi fornire un indirizzo e-mail di amministratore per ricevere notifiche su questi ordini. Aggiungere l&#39;indirizzo alle impostazioni di configurazione seguenti: **[!UICONTROL Send Order Delayed Email Copy To]** nel modello [Ritardo ordine](#order-delayed) e [!UICONTROL Ship To Store Email Recipients] nel modello [Spedisci all&#39;archivio](#ship-to-store).



