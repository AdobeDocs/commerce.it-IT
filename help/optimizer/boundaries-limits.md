---
title: Limiti e limiti
description: Scopri i limiti e le limitazioni di  [!DNL Adobe Commerce Optimizer]  per garantire che soddisfi le esigenze della tua azienda.
role: Admin, Developer
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 149b87fc822e5d07eed36f3d6a38c80e7b493214
workflow-type: tm+mt
source-wordcount: '270'
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

- Il numero massimo di listini prezzi è 1.000.

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

   - [!DNL Adobe Commerce Optimizer] supporta il tipo di consiglio _Visualizzato di recente_ per l&#39;accesso anticipato.
   - Non sono supportate inclusioni o esclusioni di categorie o attributi.
   - Impossibile visualizzare l&#39;anteprima dei consigli in [!DNL Adobe Commerce Optimizer].
