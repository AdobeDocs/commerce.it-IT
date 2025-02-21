---
title: Elaborazione di livello 2 e livello 3
description: Livelli di elaborazione dei pagamenti con carta all'interno di  [!DNL Payment Services]  transazioni.
role: Admin
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Elaborazione di livello 2 e livello 3

Sono disponibili tre livelli di elaborazione della scheda tramite [!DNL Payment Services]:

* Il livello 1 è il più comune, richiede meno informazioni e pertanto è soggetto generalmente a commissioni di interscambio più elevate rispetto alle operazioni trattate con dati di livello 2 o 3, che sono solitamente collegate alle carte di credito aziendali e di acquisto.

* Con i livelli 2 e 3, [!DNL Payment Services] clienti con interchange plus (IC++) che accettano molte transazioni con carta di acquisto o con carta aziendale possono potenzialmente ricevere una velocità di elaborazione inferiore consentendo a [!DNL Payment Services] di inviare ulteriori informazioni su una transazione. Se l&#39;operazione soddisfa i requisiti di rete della carta, l&#39;esercente può ricevere una velocità di elaborazione inferiore per una determinata operazione.

>[!NOTE]
>
>I prezzi di livello 2 e 3 si applicano solo alle transazioni Visa e MasterCard. American Express offre solo prezzi di livello 2. Discover non offre prezzi di livello 2 né di livello 3. Per ulteriori informazioni, consulta [elaborazione dei pagamenti](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} nella documentazione per gli sviluppatori di PayPal.

Vedere [Che cos&#39;è IC++?](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank} nella documentazione per gli sviluppatori di PayPal per ulteriori informazioni.

I dati di elaborazione di livello 2 e 3 consentono agli esercenti di ridurre il prezzo IC++ se forniscono ulteriori dettagli sull&#39;acquisto che riducono il rischio del processore e forniscono vantaggi:

* Fornendo questi dati di elaborazione, i grandi clienti pagheranno meno.

* I clienti hanno meno probabilità di trovarsi in situazioni fraudolente, in quanto gli ordini hanno più informazioni.

Tuttavia, le reti di carte, come Visa e Mastercard, determinano in ultima analisi se una transazione si qualifica per l&#39;elaborazione di livello 2 o 3:

* I dati di livello 2 contengono informazioni aggiuntive, ad esempio l&#39;importo dell&#39;imposta per l&#39;ordine, il codice cliente o il numero OA.

* I dati di livello 3 contengono informazioni più dettagliate sulla vendita; ciò consente di ottenere tassi di interscambio ancora più bassi rispetto al livello 2. I dati di livello 3 contengono informazioni quali una descrizione dell&#39;articolo acquistato, la quantità di unità acquistate, l&#39;unità di misura per gli articoli ordinati e altri dettagli specifici.

[!DNL Payment Services] raccoglie questi dati e fornisce rapporti dettagliati sulle transazioni di pagamento.

## Transazioni di pagamento con carta di livello 2 e 3 in [!DNL Payment Services]

Per essere classificate nei livelli 2 o 3, le informazioni precedentemente trasmesse devono essere inviate dagli esercenti, sebbene siano le reti di carte a determinare, in ultima analisi, il livello al quale un&#39;operazione si qualifica per l&#39;elaborazione.

Per ulteriori informazioni, consulta le [Domande frequenti sull&#39;elaborazione dei pagamenti](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank} nella documentazione per gli sviluppatori di PayPal.

L&#39;elaborazione dei livelli 2 e 3 è disabilitata per impostazione predefinita per [!DNL Payment Services] commercianti a livello di store.

L&#39;elaborazione di livello 2 e livello 3 è disponibile se si utilizza già la determinazione prezzi IC++. Per abilitare questa funzionalità è possibile eseguire questa operazione tramite l&#39;interfaccia della riga di comando [CLI](configure-cli.md).

>[!IMPORTANT]
>
>In caso di domande, contattare l&#39;account manager [!DNL Payment Services].
