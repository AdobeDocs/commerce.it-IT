---
title: Sicurezza e conformità
description: Verifica i requisiti di sicurezza e conformità per il sito.
exl-id: 083c5a12-1d78-48b5-b9e3-612b104ce7e0
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security.html?lang=it
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Sicurezza e conformità

La sicurezza è la preoccupazione principale di [!DNL Payment Services] e non vengono trasmesse informazioni private o regolamentate dal settore delle carte di pagamento (PCI) a [!DNL Payment Services].

## Sicurezza di Commerce

[!DNL Adobe Commerce] e [!DNL Magento Open Source] includono il supporto per diverse funzionalità di sicurezza.

Consulta [Sicurezza](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/security/security){target="_blank"} nella guida utente di base per rivedere le best practice sulla sicurezza e scoprire come gestire le sessioni e le credenziali dell&#39;amministratore, implementare CAPTCHA e gestire le restrizioni per i siti Web.

## Conformità PCI

Il settore delle carte di pagamento (Payment Card Industry, PCI) ha stabilito una serie di requisiti per le imprese che accettano il pagamento tramite carta di credito su Internet. Oltre a mantenere un ambiente sicuro, i commercianti che gestiscono le informazioni della carta di credito del cliente sono responsabili del rispetto di alcune linee guida standard.

Per ulteriori informazioni, vedere [Linee guida per la conformità PCI](https://experienceleague.adobe.com/it/docs/commerce-admin/start/compliance/payments/compliance-pci){target="_blank"}.

Gli esercenti possono completare un [questionario di autovalutazione (SAQ)](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"}, che è uno strumento di auto-convalida per valutare la sicurezza dei dati dei titolari della carta.

### Campi carta di credito

Con i campi della carta di credito, non vengono trasmessi dati regolamentati PCI ai servizi. Non è necessario archiviare o mantenere tali dati, il che riduce notevolmente i problemi di conformità PCI.

### 3DS

PCI 3-D Secure (3DS) consente l&#39;autenticazione dell&#39;acquirente con l&#39;emittente della carta di credito quando si effettuano acquisti online con carta di credito. Questo ulteriore livello di sicurezza contribuisce a prevenire le frodi online ed è richiesto come parte delle normative di conformità dell&#39;Unione europea (UE).

[!UICONTROL Payment Services] fornisce funzionalità 3DS per consentire ai commercianti di rispettare le normative UE e proteggere clienti e commercianti da attività fraudolente nei loro negozi.

Se sei un commerciante all&#39;interno dell&#39;UE o della Gran Bretagna in cui è richiesta la conformità 3DS, devi attivare manualmente 3DS (è `Off` per impostazione predefinita) nel [Amministratore configurazione](configure-admin.md#credit-card-fields).

>[!IMPORTANT]
>
>Il requisito 3DS si applica alle operazioni in cui la banca dell&#39;impresa e del titolare della carta si trova nello [Spazio economico europeo](https://www.efta.int/eea) (SEE) e in Gran Bretagna. I commercianti degli Stati Uniti non richiedono 3DS, ma possono abilitarlo per le loro transazioni se lo desiderano.

Gli ordini effettuati per l&#39;acquirente dal personale del commerciante/negozio non sono configurati con le misure di conformità 3DS.

>[!MORELIKETHIS]
>
> * Per ulteriori informazioni, vedere [3DS nelle impostazioni](configure-admin.md#3ds).
> * Per ulteriori informazioni sulle carte di credito specifiche per i test 3DS, consulta le [schede di test](https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/test/) nella documentazione per gli sviluppatori di PayPal.

### Vaulting delle carte

Quando un acquirente [archivia, o &quot;salva&quot;, le informazioni sulla sua carta di credito](vaulting.md) per acquisti futuri nei tuoi negozi, le informazioni minime sulla carta di credito vengono condivise con l&#39;acquirente (ultime quattro cifre, data di scadenza della carta e marchio della carta). Le informazioni relative alla carta di credito vengono memorizzate presso il fornitore dei servizi di pagamento. Quando una carta scade, o non hanno più bisogno delle informazioni salvate, possono eliminare quel token in modo che le informazioni non vengano più memorizzate dal provider di pagamenti.

Per ulteriori informazioni, vedere [Archivio carte di credito](vaulting.md).

### Pulsanti di pagamento PayPal

Con i pulsanti di pagamento PayPal non vengono trasmessi dati regolamentati PCI ai servizi. Non è necessario archiviare o mantenere tali dati, il che riduce notevolmente i problemi di conformità PCI.

Per motivi di sicurezza, PayPal non passa l&#39;indirizzo di fatturazione durante il pagamento: paese, e-mail e nome sono le uniche informazioni di fatturazione utilizzate. Facoltativamente, puoi abilitare l&#39;estrazione PayPal del tuo sito per restituire l&#39;indirizzo di fatturazione completo contattando PayPal e completando un processo di verifica.

PayPal ha anche la protezione integrata contro le frodi che utilizza l&#39;apprendimento automatico per aiutarti a combattere le frodi. Per ulteriori informazioni, consulta la [documentazione sulla protezione del venditore](https://www.paypal.com/us/webapps/mpp/security/seller-protection) di PayPal.

## Protezione dalle frodi

Con l&#39;estensione [Signifyd](https://commercemarketplace.adobe.com/signifyd-module-connect.html) è possibile abilitare la protezione antifrode automatizzata per Payment Services. Per ulteriori informazioni, vedere [Protezione antifrode Signifyd](fraud-protection.md).

PayPal fornisce altre opzioni per la [protezione dalle frodi](https://www.paypal.com/us/cshelp/article/what-is-fraud-protection-help1014){target=_blank} nella documentazione per gli sviluppatori:

* Per ulteriori informazioni, vedere [Protezione antifrode avanzata](https://www.paypal.com/us/enterprise/fraud-protection-advanced#fraud-protection-advanced){target=_blank}.
* Per ulteriori informazioni, vedere [Protezione chargeback](https://www.paypal.com/us/cshelp/article/what-is-chargeback-protection-help608){target=_blank}.
