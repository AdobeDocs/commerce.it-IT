---
title: Elenco di controllo preparazione cliente
description: Scopri come prepararti per una migrazione in massa dei dati ad Adobe Commerce as a Cloud Service con una lista di controllo di idoneità che includa coinvolgimento, computer, origine e destinazione.
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:18.443Z'
TQID: 'https://experienceleague.adobe.com/728hkK-dzIPzyuBhuNyOqEE9FxlVGdVc9R2wIRcXobk'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c32adafa-ed01-4b31-997e-2413013911b0id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 1171
ht-degree: 0%

---

# Lista di controllo preparazione cliente

{{bulk-data-early-access}}

Utilizzare questo elenco di controllo per preparare una migrazione dei dati da un&#39;istanza [!DNL Adobe Commerce on Cloud] o locale a [!DNL Adobe Commerce as a Cloud Service] utilizzando lo strumento di migrazione dei dati in blocco.

Lo strumento di migrazione viene distribuito come parte del processo di coinvolgimento Commerce Deployed Engineering (CDE). L’accesso allo strumento viene gestito in base a un contratto CDE firmato e non è disponibile pubblicamente.

Questo elenco di controllo descrive ciò che è necessario disporre prima che lo strumento venga condiviso ([Fase 1](#stage-1-before-tool-access)) e ciò che è necessario per iniziare la configurazione e l&#39;esecuzione una volta che si dispone dello strumento ([Fase 2](#stage-2-before-running-the-migration)). Rivedi questo elenco di controllo con il tuo team Adobe in anticipo, perché alcuni elementi richiedono il coordinamento di Adobe.

## Fase 1: prima dell&#39;accesso all&#39;utensile

Completa o conferma quanto segue prima di fornire lo strumento di migrazione e la relativa documentazione.

- **Coinvolgimento CDE**: è necessario che sia stato stipulato un contratto Commerce Deployed Engineering firmato. L&#39;accesso allo strumento viene concesso nella fase di firma dell&#39;offerta del ciclo di vita del CDE. Coordinati con il tuo team Adobe.
- **Questionario di ambito completato**: durante l&#39;individuazione CDE viene completato un questionario di ambito per verificare la fattibilità della migrazione con le attuali funzionalità dello strumento e per valutare l&#39;ingombro e la complessità dei dati. Prima di procedere, assicurati di averlo completato con il tuo team Adobe.
- **Nessun dato HIPAA confermato**. L&#39;istanza di origine non deve contenere dati regolamentati HIPAA. Conferma prima di procedere.
- **Indirizzi IP forniti** — Fornisci al team di Adobe l&#39;elenco degli indirizzi IP statici da cui verrà eseguito lo strumento di migrazione. Questa opzione è necessaria per configurare l’accesso alla rete sul lato Adobe.
- **Provisioning dell&#39;istanza di destinazione eseguito**. È necessario eseguire il provisioning dell&#39;istanza di destinazione [!DNL Adobe Commerce as a Cloud Service] prima dell&#39;inizio della migrazione. Coordinati con il tuo team Adobe per confermare che l’istanza è pronta.

## Fase 2: prima di eseguire la migrazione

Dopo aver effettuato l&#39;accesso allo strumento, preparare i seguenti elementi prima di iniziare la configurazione e l&#39;esecuzione.

### Computer di migrazione

Lo strumento di migrazione viene eseguito su una macchina controllata, ad esempio un jump box dedicato. Questa macchina deve soddisfare i seguenti requisiti.

- Installazione di **[!DNL Docker]e [!DNL Docker Compose] completata**. Lo strumento è basato su [!DNL Docker]. Sia `docker` che `docker compose` (o la versione precedente di `docker-compose`) devono essere installati e funzionanti nel computer di migrazione.
- **[!DNL Docker]autorizzazioni di esecuzione** — L&#39;utente che esegue la migrazione deve essere autorizzato a eseguire [!DNL Docker] comandi. Il [!DNL Linux], l&#39;utente deve essere nel gruppo `docker`. In [!DNL macOS] e [!DNL Windows], [!DNL Docker Desktop] deve essere in esecuzione e accessibile.
- **Directory di lavoro scrivibile**: la directory in cui è estratto lo strumento di migrazione deve essere completamente scrivibile dall&#39;utente di migrazione. Lo strumento scrive registri, cache, [!DNL Composer] dipendenze e file generati durante l&#39;esecuzione.
- **Spazio su disco sufficiente** - Verificare che lo spazio su disco sia sufficiente per i dati estratti, le immagini [!DNL Docker] e l&#39;output del registro. I requisiti di spazio variano a seconda delle dimensioni del database di origine.
- **Origini locali: connessione diretta al database dal computer di migrazione**. Per le istanze di origine locali, il computer di migrazione deve avere accesso diretto alla rete del database di origine. Lo strumento non stabilisce automaticamente la connettività del database locale. Prima di eseguire qualsiasi comando di migrazione, verificare che l&#39;host, la porta e le credenziali siano raggiungibili dal computer di migrazione.
- **Cloud CLI installato e chiave SSH registrata**. Per [!DNL Adobe Commerce on Cloud] istanze di origine, [Cloud CLI](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) deve essere installato nel computer di migrazione. La chiave pubblica SSH deve essere registrata anche nel tuo account. Per istruzioni, consulta la [Guida alle connessioni sicure](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections).

### istanza Source

- **API archivio Source accessibili**: le API REST e GraphQL dell&#39;archivio di origine devono essere accessibili dal computer di migrazione. Assicurati che nessuna restrizione di rete o autenticazione di base HTTP blocchi il traffico API all’URL di origine.
- **Credenziali OAuth Source**: lo strumento di migrazione utilizza OAuth per l&#39;autenticazione con l&#39;archivio di origine. Crea o conferma un&#39;integrazione nell&#39;origine [!UICONTROL **Admin**] ([!UICONTROL **System**] > [!UICONTROL **Extensions**] > [!UICONTROL Integrations]) e la chiave consumer, il segreto consumer, il token di accesso e il segreto del token di accesso sono pronti.
- **Origini PaaS: token API di Magento Cloud** — Genera un token API [!DNL Cloud] dalle [Impostazioni account cloud](https://accounts.magento.cloud) in [!UICONTROL **Impostazioni account**] > [!UICONTROL **Token API**]. Obbligatorio solo quando l&#39;origine è un&#39;istanza [!DNL Adobe Commerce on Cloud].
- **Credenziali database Source** - (solo locale) I dettagli della connessione al database [!DNL MySQL] di origine sono pronti per la configurazione: `host`, `port`, `user`, `password` e il nome `database`.
- **Possibilità di mettere in pausa cron**. Per evitare scritture simultanee, è necessario arrestare cron nell&#39;istanza di origine per la durata dell&#39;estrazione dei dati.
- **Possibilità di sospendere le integrazioni e i processi in background**. Qualsiasi integrazione di terze parti (ERP, OMS, PIM), processo pianificato o processo in background che scrive nel database di origine deve essere sospesa per la finestra di estrazione.
- **Possibilità di attivare e disattivare la modalità di manutenzione** — (solo migrazione per fasi) Se si esegue una migrazione per fasi con una finestra di manutenzione, è necessario abilitare e disabilitare la modalità di manutenzione nell&#39;istanza di origine.

### Istanza di destinazione

- **ID tenant e ID organizzazione confermati**. Ottieni `TARGET_TENANT_ID` e `TARGET_ORG_ID` dal tuo team Adobe prima della configurazione.
- **Credenziali server-to-server OAuth IMS** - Necessarie per l&#39;autenticazione dello strumento di migrazione con la destinazione. Generato tramite [Adobe Developer Console](https://developer.adobe.com/console/). È necessario l&#39;accesso [!UICONTROL Developer] o [!UICONTROL Admin] all&#39;organizzazione Adobe, perché l&#39;accesso utente di base non è sufficiente per creare le credenziali. Coordinati con il tuo team Adobe per selezionare il profilo di prodotto corretto e preparare l&#39;ID client (`ADOBE_IMS_CLIENT_ID`) e il segreto client (`ADOBE_IMS_CLIENT_SECRET`).
- **URL endpoint CDMS** — fornito dal team Adobe. Non tentare di dedurre questo valore. È necessario sia l’endpoint di pre-produzione per le migrazioni sandbox e di test che l’endpoint di produzione per le migrazioni live cutover.
- **Configurazione di base allineata tra origine e destinazione**. I dati di configurazione di base, ad esempio le impostazioni dell&#39;archivio e la configurazione del sistema, non vengono migrati dallo strumento. Impostala manualmente sulla destinazione in modo che corrisponda all’origine prima della migrazione.
- **Archivi B2B: funzionalità B2B configurate in modo coerente**. Se l&#39;origine è un archivio abilitato B2B, verificare che le impostazioni B2B [!UICONTROL Admin] pertinenti siano configurate in modo coerente sia sull&#39;origine che sulla destinazione prima della migrazione. Per informazioni sulle impostazioni specifiche necessarie, consultare la [guida alla migrazione](migration-guide.md).

### Pianificazione della migrazione

- **Approccio di migrazione deciso** — Determina quale approccio si adatta al tuo caso d&#39;uso prima di iniziare.
  - Migrazione monofase: nessuna modalità di manutenzione richiesta. Si adatta a esecuzioni di prova, ambienti di sviluppo o sandbox o a qualsiasi migrazione in cui l’origine può rimanere attiva durante l’estrazione.
  - Migrazione multifase: è necessaria la modalità di manutenzione. È necessaria una migrazione multifase per le migrazioni di produzione in cui l’origine deve essere congelata durante l’estrazione per garantire la coerenza dei dati.
- **Intervallo di manutenzione pianificato** - Si applica solo alle migrazioni multifase. Pianifica e comunica in anticipo la finestra di manutenzione. L’istanza sorgente non è disponibile per gli utenti finali per la durata delle fasi di estrazione e caricamento.
- **Codice visualizzazione archivio confermato** — Identificare il codice della visualizzazione archivio (`STORE_CODE`) nell&#39;istanza di origine. Il valore predefinito è `default` ma deve corrispondere al codice effettivo in [!UICONTROL Admin] > [!UICONTROL Stores] > [!UICONTROL All Stores]. Un codice di archivio errato può influire sulle operazioni dei dati durante la migrazione.

Dopo aver confermato tutti gli elementi, è possibile verificare l&#39;accesso al servizio con la [guida all&#39;accesso al servizio di migrazione](cdms-access.md) e quindi avviare i passaggi di configurazione ed esecuzione nella [guida alla migrazione](migration-guide.md).
