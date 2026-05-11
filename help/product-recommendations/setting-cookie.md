---
title: Gestire le restrizioni dei cookie
description: Scopri come i consigli di prodotto gestiscono le restrizioni sui cookie e la conformità alla privacy.
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
TQID: https://experienceleague.adobe.com/qqgwO4KI4koSBcYu9mdrjb6AQFW4guxk6dfLDBEwVb8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 454
ht-degree: 0%

---

# Gestire le restrizioni dei cookie

Sia Adobe Commerce che Magento Open Source richiedono il consenso prima che i dati vengano memorizzati nei cookie del browser. Per ulteriori informazioni, vedere [Modalità di restrizione cookie](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html).

## Gestione delle restrizioni relative ai cookie da parte di Product Recommendations

Quando distribuisci il modulo `magento/product-recommendations` in produzione, inizia a raccogliere gli eventi di interazione dell&#39;acquirente nella vetrina. Questi dati possono essere memorizzati nei cookie del browser o nell’archiviazione locale per alimentare gli algoritmi di raccomandazioni.

>[!IMPORTANT]
>
>La funzione Consigli di prodotto ora rispetta la modalità di restrizione dei cookie non raccogliendo o memorizzando dati nei cookie o nell’archiviazione locale quando le restrizioni dei cookie sono abilitate. Ciò include i dati comportamentali utilizzati per i consigli personalizzati.

### Dati interessati da restrizioni relative ai cookie

I seguenti dati di Product Recommendations non vengono raccolti quando è abilitata la modalità di restrizione dei cookie:

- **Dati comportamentali**: visualizzazioni di prodotti, azioni di aggiunta al carrello, acquisti e altre interazioni con gli acquirenti.
- **Dati sessione**: informazioni sulla sessione acquirente e interazioni con l&#39;unità di consigli.
- **Dati Personalization**: dati utilizzati per tipi di consigli come &quot;Visualizzati di recente&quot; e &quot;Più acquistati&quot;.

### Impatto sui tipi di consigli

Quando la modalità di restrizione dei cookie è abilitata e gli acquirenti non hanno accettato i cookie, alcuni tipi di consigli potrebbero non essere visualizzati o mostrare risultati limitati:

- **Prodotti visualizzati di recente**: richiede dati di sessione memorizzati nei cookie/nell&#39;archivio locale.
- **Consigliato**: richiede dati comportamentali per la personalizzazione.
- **Ha acquistato questo/a, ha acquistato quello**: richiede i dati della cronologia acquisti.

>[!NOTE]
>
>I tipi di consigli che non si basano su dati comportamentali, come &quot;Più visualizzati&quot; e &quot;Somiglianza visiva&quot;, continueranno a funzionare normalmente anche con le restrizioni sui cookie abilitate.

## Soluzioni di consenso dei cookie di terze parti

La funzione Consigli sui prodotti non può integrarsi automaticamente con soluzioni di terze parti basate sul consenso dei cookie. È responsabilità del commerciante garantire che la raccolta dei dati sia conforme alle leggi e alle normative sulla privacy applicabili.

Se utilizzi una soluzione di consenso dei cookie personalizzata, puoi implementare il meccanismo dei cookie do-not-track per controllare la raccolta dei dati.

### Implementazione dei cookie do-not-track

È possibile utilizzare il cookie `mg_dnt` per controllare a livello di programmazione la raccolta dati:

#### Nome cookie

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### Disattiva raccolta dati

Imposta il cookie do-not-track quando gli utenti rifiutano i cookie:

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### Abilita raccolta dati

Cancella il cookie do-not-track quando gli utenti accettano i cookie:

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## Verifica della modalità di restrizione dei cookie

Per verificare il comportamento dei consigli di prodotto con le restrizioni sui cookie:

1. Abilita la modalità di restrizione dei cookie nella configurazione di Adobe Commerce.
1. Visita la vetrina senza accettare i cookie.
1. Verifica che le unità di consigli visualizzino il contenuto di fallback appropriato.
1. Accetta i cookie e verifica che i consigli inizino a raccogliere dati.

## Rispetto della privacy

La raccolta dati di Consigli di prodotto non include informazioni personali (PII, personally identifiable information). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono anonimi. Per ulteriori informazioni, vedere l&#39;[Informativa sulla privacy di Adobe](https://www.adobe.com/privacy/policy.html).

>[!TIP]
>
>Per i clienti del settore sanitario che utilizzano l’estensione HIPAA per Data Services, potrebbe essere necessaria una configurazione aggiuntiva. Per ulteriori informazioni, vedere [Preparazione HIPAA](../data-connection/hipaa-readiness.md).
