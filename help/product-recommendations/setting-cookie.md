---
title: Gestire le restrizioni dei cookie
description: Scopri come i consigli di prodotto gestiscono le restrizioni dei cookie.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Gestire le restrizioni dei cookie

Sia Adobe Commerce che Magento Open Source richiedono il consenso prima che i dati vengano memorizzati nei cookie del browser. Per ulteriori informazioni, vedere [Modalità di restrizione cookie](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html).

Quando distribuisci il modulo `magento/product-recommendations` in produzione, inizia a raccogliere gli eventi di interazione dell&#39;acquirente nella vetrina. Poiché i dati per questi eventi possono essere memorizzati nei cookie del browser o nell’archiviazione locale, la funzione supporta la modalità di restrizione dei cookie in quanto non raccoglie gli eventi fino a quando l’acquirente non ha fornito il consenso ai cookie.

Questo potrebbe non funzionare con le soluzioni di consenso dei cookie di terze parti. È responsabilità di ogni commerciante garantire che la raccolta dei dati non avvenga prima che sia stato fornito il consenso ai cookie, come spesso richiesto dalla legge. Se gestisci il consenso dei cookie con il codice personalizzato, puoi utilizzare un cookie do-not-track denominato `mg_dnt` per limitare la raccolta di dati.

- Nome del cookie:

  ```text
  `const DNT_COOKIE = "mg_dnt";`
  ```

- Imposta il cookie do-not-track per disabilitare la raccolta dati:

  ```text
  `$.mage.cookies.set(DNT_COOKIE, true);`
  ```

- Per cancellare il cookie quando l&#39;utente accetta i cookie:

  ```text
  `$.mage.cookies.clear(DNT_COOKIE);`
  ```
