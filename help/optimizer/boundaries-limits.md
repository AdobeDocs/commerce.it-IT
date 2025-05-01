---
title: Limiti e limiti
description: Scopri i limiti e le limitazioni di  [!DNL Adobe Commerce Optimizer]  per garantire che soddisfi le esigenze della tua azienda.
role: Admin, Developer
source-git-commit: 45a43fe2ada206515c512a04aa6e9072e08844cc
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Limiti e limiti

>[!NOTE]
>
>Questa documentazione descrive i limiti e i limiti per lo sviluppo di accesso anticipato e non riflette tutte le funzionalità previste per la disponibilità generale.

Di seguito sono riportati limiti e limiti per Adobe Commerce Optimizer.

## Catalogo

- Il tasso garantito di inserimento nel catalogo è: 1000 prodotti/minuto e 5000 prezzi/minuto
- Il numero base di aggiornamenti di prodotto al giorno è 1.000.000.
- Il numero totale di SKU consentiti in una singola istanza è di 250.000. 
- Il numero massimo di ambiti è 50.
- Il numero di varianti per prodotto è 10.000.
- La dimensione del prodotto non può superare i 200 kb.

## Prezzi

- Il numero massimo di listini prezzi è 30.000. Il numero di listini prezzi di base non può superare 100 e deve seguire la regola in cui (il numero di listini prezzi) x (il numero di canali) deve essere minore o uguale a 100.
- Il tasso di acquisizione feed a prezzo garantito è di 5000 record al minuto.
- Un singolo record di prezzo non può avere più di 10 sconti.
- Il numero base di aggiornamenti del prezzo al giorno è 5.000.000.

## Ricerca e vetrina

- Un’unica richiesta di ricerca può restituire 100 prodotti.
- Il numero massimo di attributi filtrabili è 200
- Il numero massimo di attributi ricercabili è 200
- Il numero massimo di attributi ordinabili è 50
- Il numero massimo di facet è 100. Tutti i facet devono essere attributi filtrabili.
- Il numero massimo di opzioni restituite da un singolo facet cat è 100, che può essere aumentato per richiesta di supporto.

## Canali e criteri

- Il numero massimo di canali per tenant è 1000.
- Il numero massimo di criteri assegnati a un canale è 10.
- Il numero massimo di valori di attributo utilizzati in un criterio è 100. 

## Individuazione dei prodotti e raccomandazioni

- Per l’individuazione del prodotto, le impostazioni di merchandising e prezzo basate su attributi non sono supportate.
- Per i consigli:

   - ACO supporta il tipo di consiglio _Visualizzato di recente_ per EA
   - Non sono supportate inclusioni o esclusioni di categorie o attributi.
   - Impossibile visualizzare l&#39;anteprima dei consigli in [!DNL Adobe Commerce Optimizer].
