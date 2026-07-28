---
title: Eseguire una migrazione dati in blocco
description: Scopri come configurare ed eseguire una migrazione di dati in blocco da un’istanza Adobe Commerce PaaS o on-premise ad Adobe Commerce as a Cloud Service con CLI.
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:07.600Z'
TQID: 'https://experienceleague.adobe.com/z9659Vnf2JLxJ4U5p3tEEjurj5Mg3bfKj68Gheq2AXY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 2802
ht-degree: 0%

---

# Eseguire una migrazione dati in blocco

{{bulk-data-early-access}}

Questa guida è un riferimento operativo dettagliato per l&#39;esecuzione di una migrazione dati da un&#39;installazione locale o PaaS [!DNL Adobe Commerce] a [!DNL Adobe Commerce as a Cloud Service] tramite lo strumento di migrazione dati in blocco. I valori di configurazione effettivi e i dettagli specifici dell’ambiente variano a seconda della configurazione.

Prima di iniziare, verifica di aver completato ogni elemento nella [Lista di controllo preparazione cliente](readiness-checklist.md) e di aver verificato l&#39;accesso API con la [Guida all&#39;accesso al servizio di migrazione](cdms-access.md).

>[!NOTE]
>
>Il pacchetto di distribuzione dello strumento include una documentazione tecnica completa relativa all&#39;architettura dello strumento, alla progettazione interna, al framework di trasformazione dei dati e al framework di test di integrità.

## Prerequisiti

- **[!DNL Docker]** e **[!DNL Docker Compose]** devono essere installati nel computer in cui si esegue la migrazione.
- L&#39;utente che esegue la migrazione deve disporre dell&#39;autorizzazione per eseguire i comandi `docker` e `docker compose` (o `docker-compose` legacy). Il [!DNL Linux], l&#39;utente deve essere nel gruppo `docker`. In [!DNL macOS] e [!DNL Windows], [!DNL Docker Desktop] deve essere in esecuzione e accessibile. L&#39;interfaccia CLI di migrazione richiama [!DNL Docker] ripetutamente e gli errori di autorizzazione in questo punto bloccano l&#39;esecuzione.
- Prima di eseguire la migrazione, la configurazione di base deve essere coerente tra origine e destinazione. I dati di configurazione di base, ad esempio le impostazioni dell&#39;archivio e la configurazione del sistema, non vengono migrati da questo strumento. Impostala sulla destinazione in modo indipendente e allinearla all’origine prima della migrazione.

## Configurare il pacchetto di strumenti

Configurare l’ambiente per la migrazione in blocco dei dati:

>[!VIDEO](https://video.tv.adobe.com/v/3496128?captions=ita)

1. Estrarre il contenuto di `ccsaas-migration-tools.tar.gz`.

1. Esegui tutti i comandi dalla cartella `ccsaas-migration-tools` estratta, in cui risiede `bin/console`.

1. Verificare che la cartella sia scrivibile per i registri, la cache, [!DNL Composer] e i file generati.

   Cambia la proprietà di tutti i file e le sottocartelle presenti in tale directory all&#39;utente del sistema operativo che esegue la migrazione, in modo che lo strumento sia in grado di leggere e scrivere in modo coerente. Ad esempio, il [!DNL Linux]: `chown -R <user>:<group> <project-root>`.

1. Creare i file `.env` e `.my.cnf` nella directory principale del progetto copiando i file di esempio (`.example.env` in `.env` e `.my.cnf.example` in `.my.cnf`), quindi immettere i valori descritti nelle sezioni seguenti.

### Esempio di file di configurazione

I file `.example.env` e `.my.cnf.example` nella directory principale dell&#39;archivio sono il punto di partenza per la configurazione. Copiare ogni file con il relativo nome di lavoro e inserire i valori richiesti.

| Esempio di file | Copia in | Cosa copre |
| --- | --- | --- |
| `.example.env` | `.env` | Elenco annotato di tutte le variabili di ambiente supportate: prestazioni, CDMS, IMS, SaaS di destinazione, autenticazione URL di origine, OAuth e valori PaaS facoltativi (`MAGENTO_CLOUD_CLI_TOKEN` quando `id=` è impostato in `.my.cnf`). Elenco completo delle variabili disponibile nel file `.env`. |
| `.my.cnf.example` | `.my.cnf` | `[section]` layout di riferimento per [!DNL MySQL] locale e PaaS (`id=project:environment`). Il nome `[section]` deve corrispondere a `SOURCE_CONNECTION_NAME` in `.env`. I campi includono `user`, `password`, `host`, `port`, `database` e `id=` per PaaS. |

## Configurare il file di ambiente

Il file `.env` nella directory principale del progetto è la configurazione di migrazione ed estrazione. Gestisce la pipeline CLI, inclusi gli URL di origine e di destinazione, OAuth, la connessione CDMS remota, l’autenticazione SaaS e IMS e altri switch.

>[!NOTE]
>
>Non includere barre finali negli URL. Utilizzare ad esempio `https://example.com` anziché `https://example.com/`.

Modificare il file `.env` e impostare correttamente almeno i valori seguenti. Per l&#39;elenco completo delle variabili supportate, fare riferimento alle annotazioni in linea in `.example.env`.

```shell-session
SOURCE_INSTANCE_URL=https://<source-host>
SOURCE_INSTANCE_GRAPHQL_URL=https://<source-host>/graphql
SOURCE_INSTANCE_REST_URL=https://<source-host>/rest
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Configurare le credenziali OAuth di origine

>[!VIDEO](https://video.tv.adobe.com/v/3496148?captions=ita)

Questi quattro valori firmano le richieste dallo strumento di migrazione alle API dell’archivio di origine. Per ottenerle, apri l&#39;origine [!UICONTROL Admin] e passa a [!UICONTROL **Sistema**] > [!UICONTROL **Estensioni**] > [!UICONTROL **Integrazioni**]. Creare o aprire un&#39;integrazione, quindi copiare i valori in `.env`:

```shell-session
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Impostare il token CLI cloud

>[!NOTE]
>
>Applicabile solo a [!DNL Adobe Commerce on Cloud] istanze di origine. Lo strumento rileva automaticamente il tipo di origine da `.my.cnf`. Se la sezione `SOURCE_CONNECTION_NAME` contiene una riga `id=` (ad esempio, `id=project:production`), l&#39;origine è [!DNL Adobe Commerce on Cloud] e `MAGENTO_CLOUD_CLI_TOKEN` è obbligatorio. Per le origini locali senza `id=`, questo token non è necessario e la configurazione del tunnel è stata ignorata.

1. Vai a `https://accounts.magento.cloud` e accedi.

1. Fai clic sull&#39;immagine del tuo profilo e seleziona [!UICONTROL **Impostazioni account**].

1. Vai alla sezione [!UICONTROL **Token API**].

1. Selezionare [!UICONTROL **Crea un token API**], assegnargli un nome descrittivo e copiare il token generato.

1. Imposta il token in `.env`:

   ```text
   MAGENTO_CLOUD_CLI_TOKEN=<your_magento_cloud_api_token>
   ```

>[!NOTE]
>
>Se utilizzi per la prima volta Cloud CLI, devi aggiungere anche la chiave pubblica SSH al tuo account. Per istruzioni, consulta la [Guida alle connessioni sicure](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/develop/secure-connections).

### Allinea impostazioni amministratore Commerce

Prima della migrazione, assicurati che le seguenti impostazioni siano coerenti tra l’origine e la destinazione.

>[!NOTE]
>
>Per garantire una migrazione senza problemi, [!DNL Adobe] consiglia di rendere tutte le configurazioni di base nell&#39;istanza di destinazione coerenti con l&#39;origine.

### Configurare le credenziali SaaS e IMS di destinazione

>[!VIDEO](https://video.tv.adobe.com/v/3496173?captions=ita)

Queste sono le impostazioni IMS e API di [!DNL Adobe Commerce as a Cloud Service] per la destinazione. È necessario disporre dell’ID tenant, dell’ID organizzazione, delle credenziali server-to-server di IMS OAuth e dell’host IMS corretto per l’ambiente. Coordina con il tuo team di Adobe per l’accesso a organizzazione, tenant e profilo. Non tentare di dedurre o stimare valori sensibili.

#### Genera credenziali IMS

Utilizza [Adobe Developer Console](https://developer.adobe.com/console/). Per creare i progetti è necessario l&#39;accesso [!UICONTROL Developer] o [!UICONTROL Admin] nell&#39;organizzazione Adobe. Un accesso utente di base non è sufficiente per aggiungere le API.

1. Creare un progetto o aprirne uno esistente, quindi selezionare [!UICONTROL Add API].

1. Scegli [!UICONTROL **Adobe Commerce as a Cloud Service**] e continua.

1. Seleziona [!UICONTROL **OAuth Server-to-Server**] come tipo di autenticazione e continua.

1. Seleziona il profilo di prodotto previsto dal team di Adobe per questo tenant, quindi seleziona [!UICONTROL **Salva API configurata**].

1. Nella barra laterale del progetto, apri [!UICONTROL **OAuth Server-to-Server**] (o [!UICONTROL **Credenziali**]), quindi copia l&#39;ID client e il segreto client in `.env` come `ADOBE_IMS_CLIENT_ID` e `ADOBE_IMS_CLIENT_SECRET`.

L&#39;endpoint del token IMS (`ADOBE_IMS_URL`) deve corrispondere all&#39;ambiente delle credenziali.

| Livello | `ADOBE_IMS_URL` tipico |
| --- | --- |
| Controllo qualità o gestione temporanea | `https://ims-na1-stg1.adobelogin.com` |
| Pre-produzione o produzione | `https://ims-na1.adobelogin.com` |

>[!NOTE]
>
>`na1` in questi URL rappresenta l&#39;area in cui è stato eseguito il provisioning dell&#39;istanza di destinazione. Sostituiscilo con l’identificatore di regione appropriato se il provisioning dell’istanza viene eseguito in un’area diversa.

`ADOBE_IMS_META_SCOPES` deve corrispondere agli ambiti per i quali è stato eseguito il provisioning in tale credenziale. Il file `.example.env` include come riferimento la stringa completa dell&#39;ambito separato da virgole. Modificala solo se Adobe ti indica di farlo.

#### Mappare le credenziali [!DNL Adobe I/O] al file di ambiente

In [!DNL Developer Console], i valori server-to-server OAuth vengono presentati come un ID client e un segreto client, corrispondenti alla seguente struttura JSON:

```json
{
  "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

Mappare in `.env` (segnaposto di esempio):

```shell-session
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
```

Gli host API SaaS differiscono tra pre-produzione e produzione. `TARGET_INSTANCE_REST_URL` e `TARGET_INSTANCE_GRAPHQL_URL` devono utilizzare lo stesso ambiente API Commerce della migrazione, sia di pre-produzione che di produzione. Non combinare un livello con il CDMS o tenant dell’altro livello.

| Ambiente | Host tipico in `TARGET_INSTANCE_*_URL` |
| --- | --- |
| Pre-produzione o sandbox | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}` |
| Produzione | `https://na1.api.commerce.adobe.com/{tenantId}` |

>[!NOTE]
>
>`na1` in questi URL rappresenta l&#39;area in cui è stato eseguito il provisioning dell&#39;istanza di destinazione. Sostituiscilo con l’identificatore di regione appropriato se il provisioning dell’istanza viene eseguito in un’area diversa.

```shell-session
TARGET_TENANT_ID=<tenant_id>
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=<client_id>
ADOBE_IMS_CLIENT_SECRET=<client_secret>
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
TARGET_INSTANCE_REST_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}
TARGET_INSTANCE_GRAPHQL_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

Per gli host SaaS di produzione, sostituire `na1-sandbox` con `na1` in entrambi gli URL `TARGET_INSTANCE_*`. Utilizzare `ADOBE_IMS_URL` corrispondente per il livello, come illustrato nella tabella precedente.

### Impostare l’endpoint CDMS

Puntare lo strumento di migrazione sull’host dell’API CDMS che corrisponde all’ambiente in cui si sta eseguendo la migrazione. Imposta `CDMS_HOST` (e in genere `CDMS_PORT=443`) in `.env`. Utilizzare un host, di pre-produzione o di produzione, non entrambi.

| Ambiente | Quando utilizzare | `CDMS_HOST` |
| --- | --- | --- |
| Pre-produzione | Esecuzioni in pre-produzione o in stile sandbox, CDMS non di produzione | `https://commerce-data-migration-service-preprod-external.adobe.io` |
| Produzione | Migrazione o cutover della produzione live | `https://commerce-data-migration-service-prod-external.adobe.io` |

Imposta o rimuovi il commento dal blocco corrispondente all’esecuzione:

```shell-session
# Pre-production CDMS
CDMS_HOST=https://commerce-data-migration-service-preprod-external.adobe.io
CDMS_PORT=443

# Production CDMS (use for prod cutover only)
# CDMS_HOST=https://na1.api.commerce.adobe.com
# CDMS_PORT=443
```

### Imposta il codice store

`STORE_CODE` è il codice della vista archivio utilizzato dallo strumento di migrazione per le chiamate API REST dell&#39;istanza sorgente, per la creazione di clienti di test sintetici e per la pulizia dei dati. Viene inviato anche come intestazione `x-store-code` durante la fase di caricamento.

`STORE_CODE` utilizza `default` come impostazione predefinita in `.example.env`. Verifica che corrisponda al codice predefinito della vista archivio dell’istanza sorgente. Per verificare, nell&#39;origine [!UICONTROL Admin] vai a [!UICONTROL **Archivi**] > [!UICONTROL **Tutti gli archivi**] e controlla la colonna [!UICONTROL **Codice**] per la visualizzazione archivio da utilizzare. Se il codice mostrato non è `default`, aggiornare `STORE_CODE` in `.env` per farla corrispondere.

## Configurare il file di connessione al database

>[!VIDEO](https://video.tv.adobe.com/v/3496163?captions=ita)

Il file `.my.cnf` fornisce le impostazioni di connessione [!DNL MySQL] per il lato di estrazione dello strumento di migrazione. Per crearlo, copia `.my.cnf.example` in `.my.cnf` nella directory principale del progetto. Il nome della sezione deve corrispondere a `SOURCE_CONNECTION_NAME` in `.env`.

Per un’origine locale o self-hosted:

```ini
[<connection-name>]
user=<db_user>
password='<db_password>'
host=<db_host>
port=3306
database=<db_name>
```

>[!NOTE]
>
>Il computer che esegue lo strumento di migrazione deve avere accesso diretto alla rete del database di origine. Lo strumento non stabilisce o verifica automaticamente la connettività locale. Prima di eseguire qualsiasi comando di migrazione, verificare che l&#39;host, la porta e le credenziali siano raggiungibili dal computer di migrazione.

Per un&#39;origine [!DNL Adobe Commerce on Cloud]:

```ini
[<connection-name>]
id=<project_id>:<environment>
```

Il campo `id=` indica allo strumento che l&#39;origine è PaaS e attiva la configurazione del tunnel utilizzando `MAGENTO_CLOUD_CLI_TOKEN`. I valori `project_id` e `environment` sono disponibili in [!DNL Cloud Console] o tramite i comandi `magento-cloud project:list` e `magento-cloud environment:list`.

## Preparare la rete e le istanze

L’autenticazione di base HTTP davanti all’archivio può bloccare il traffico di API e strumenti. Assicurati che sia disabilitato per l’URL di origine utilizzato dalla migrazione o che i percorsi dello strumento siano consentiti, in modo che le richieste REST e GraphQL possano raggiungere l’archivio.

### Mantenere la stabilità del database di origine durante l&#39;estrazione

Mentre lo strumento estrae i dati dal database di origine, nessun altro processo deve scrivervi. Le scritture simultanee possono causare uno snapshot incoerente.

- Arrestare cron sull&#39;origine e qualsiasi utilità di pianificazione del sistema operativo che esegua `bin/magento` o altri processi di scrittura per la finestra di estrazione oppure assicurarsi che non possano essere eseguiti durante l&#39;estrazione.
- Rivedi altre integrazioni, come ERP, OMS, PIM, processi personalizzati e API di terze parti che scrivono nello stesso database. Metti in pausa o blocca le scritture per la finestra di estrazione, quindi nulla muta le tabelle durante l’esecuzione dell’estrazione.
- Questa funzionalità integra la modalità di manutenzione e l&#39;accesso al tunnel o al database. Insieme, riducono il traffico della vetrina e quello dell’API. Le integrazioni Cron e sono origini separate di scritture che è necessario controllare esplicitamente.

### Target

Se il catalogo di destinazione deve essere cancellato prima della migrazione, eliminare i prodotti in [!UICONTROL Admin] in piccoli batch, ad esempio 200 alla volta, per evitare conflitti di catalogo duplicati e timeout di eliminazione in blocco.

## Creare ed eseguire la migrazione

Lavora dalla directory del progetto estratto con accesso in scrittura.

### Mantieni la sessione attiva tramite SSH

Se ti connetti tramite SSH, una rete rilasciata può uccidere la shell e interrompere una migrazione lunga. Il comando GNU `screen` mantiene la sessione attiva sul server:

```bash
screen -S migration          # new session named "migration"
# run ./bin/console commands here; when you want to disconnect without stopping work:
# press Ctrl+A, release, then press d   # detach
screen -ls                   # list sessions
screen -x migration          # reattach to "migration"
```

È inoltre possibile utilizzare `tmux` se disponibile nel server.

### Creare l’immagine Docker

Genera l&#39;immagine [!DNL Docker] utilizzata da `bin/console`, che contiene PHP, CLI e dipendenze. Eseguire questa operazione prima della prima esecuzione o dopo la modifica di Dockerfile o immagine di base.

```bash
./bin/console build
```

### Avvia i servizi di backup

Avviare i servizi di backup [!DNL Docker Compose] per lo strumento, ad esempio il database di test locale e, se abilitati in `.env`, i servizi locali facoltativi. I servizi esatti dipendono dalla configurazione. Esegui questa operazione dopo una build corretta e prima dei comandi della shell, della migrazione o della fase.

```bash
./bin/console start
```

### Inizializzare il contenitore CLI

Avviare una volta il contenitore CLI in modo che il punto di ingresso possa completare l&#39;installazione, ad esempio un&#39;installazione di [!DNL Composer] se necessaria, rispetto al progetto montato. Esegui questa operazione una volta prima della prima migrazione eseguita in un nuovo ambiente.

```bash
./bin/console shell
exit
```

### Eseguire la migrazione

Lo strumento supporta due approcci di migrazione. Scegli quello adatto al tuo caso d’uso.

#### Migrazione monofase

Non è richiesta alcuna modalità di manutenzione nell’istanza sorgente. Esegui la pipeline di migrazione completa con un singolo comando:

```bash
./bin/console migration
```

Il comando esegue automaticamente tutti i passaggi della pipeline, end-to-end, nell’ordine seguente.

1. **Controllo configurazione**: convalida le variabili di ambiente e la configurazione dello strumento.
1. **Inizializzazione dell&#39;ambiente** — avvia [!DNL Docker] servizi, apre i tunnel cloud (se applicabili) ed esegue unit test.
1. **Integration test e inizializzazione CDMS**: esegue gli integration test e inizializza la connessione API CDMS.
1. **Crea migrazione**: registra la migrazione con CDMS e attende l&#39;analisi dello schema di destinazione. ID migrazione salvato in `.migration_id`.
1. **Test funzionali e generazione dei dati di test**: esegue test funzionali e genera dati di test sintetici sull&#39;origine per la verifica dell&#39;integrità (se abilitata).
1. **Estrazione dati**: estrae i dati dall&#39;istanza di origine.
1. **Carica nella destinazione** — carica i dati estratti nell&#39;istanza di destinazione [!DNL Adobe Commerce as a Cloud Service]. Le viste di staging vengono pulite nell’origine e i dati dei test di origine vengono rimossi tramite REST in parallelo al caricamento.
1. **Verifica integrità dati**: attiva la verifica del checksum ed esegue i test di verifica API locali. I risultati vengono registrati e gli errori non arrestano la pipeline.
1. **Pulizia dei dati di test sulla destinazione** — rimuove i dati di test sintetici dall&#39;istanza di destinazione.
1. **Risultati processo**: genera un riepilogo della migrazione e, facoltativamente, scarica gli artefatti dall&#39;archivio.

Utilizza questa opzione quando non è necessaria alcuna finestra di manutenzione, tipica per esecuzioni di prova end-to-end, ambienti di sviluppo o sandbox o qualsiasi migrazione in cui l’origine può rimanere attiva durante l’estrazione.

>[!WARNING]
>
>Non utilizzare questa opzione quando è necessaria un’origine congelata, ad esempio qualsiasi migrazione di produzione in cui non devono verificarsi nuovi ordini o modifiche ai dati durante l’estrazione. Utilizza invece la migrazione graduale. Non utilizzare questo comando come passaggio all’interno del flusso di lavoro di manutenzione graduale.

#### Migrazione multifase con modalità di manutenzione

È necessaria una modalità di manutenzione nell’istanza sorgente per garantire la coerenza dei dati durante l’estrazione. La migrazione è suddivisa in fasi distinte che devono essere eseguite in ordine.

>[!NOTE]
>
>Sono coinvolte due diverse CLI. I comandi `./bin/console` vengono eseguiti dalla directory principale del progetto dello strumento di migrazione. I comandi `bin/magento maintenance:*` vengono eseguiti nel server applicazioni [!DNL Adobe Commerce] di origine, tramite SSH nella directory principale di installazione o tramite [!UICONTROL Admin]. Lo strumento non emette comandi di manutenzione [!DNL Magento] per tuo conto.

| Fase | Chi lo gestisce | Stato Source |
| --- | --- | --- |
| 1. `migration:before-maintenance` | Strumento | Live — non abilitare ancora la manutenzione |
| &#x200B;2. Abilita modalità di manutenzione | Manuale | Transizione verso il congelamento |
| 3. `migration:during-maintenance` | Strumento | Congelato: non disattivare la manutenzione durante questa fase |
| &#x200B;4. Disattiva modalità di manutenzione | Manuale (condizionale) | Torna alla versione live dell’istanza sorgente di transizione |
| &#x200B;5. `migration:cleanup` (facoltativo) | Strumento | Live — deve essere fuori manutenzione |

**Fase 1 — Prima della manutenzione (l&#39;origine è attiva)**

Esegui mentre l’istanza sorgente è attiva e accetta il traffico. L’accesso REST e GraphQL all’origine deve essere completamente disponibile. Non attivare la modalità di manutenzione prima del completamento di questa fase.

Torna alla directory principale del server ed esegui:

```bash
./bin/console migration:before-maintenance
```

1. **Controllo configurazione**: convalida le variabili di ambiente e la configurazione dello strumento.
1. **Inizializzazione dell&#39;ambiente** — avvia [!DNL Docker] servizi, apre i tunnel cloud PaaS (se applicabile) ed esegue unit test.
1. **Integration test e inizializzazione CDMS**: esegue gli integration test e inizializza la connessione API CDMS.
1. **Crea migrazione**: registra la migrazione con CDMS e attende l&#39;analisi dello schema di destinazione. ID migrazione salvato in `.migration_id`.
1. **Test funzionali**: esegue test funzionali per l&#39;origine attiva.
1. **Generazione dati di test**: crea clienti e ordini di test sintetici nell&#39;origine per la verifica dell&#39;integrità (se abilitata).

**Fase 2 - Abilitare la modalità di manutenzione (manuale)**

Abilita la modalità di manutenzione nell’origine e sospendi tutte le attività che scrivono nel database o che hanno un impatto su di esso, inclusi i processi pianificati, le integrazioni di terze parti, l’elaborazione degli ordini e la sincronizzazione delle risorse multimediali.

Sul server Commerce di origine (directory principale di installazione), eseguire:

```bash
bin/magento maintenance:enable
```

**Fase 3 — Durante la manutenzione (l&#39;origine è bloccata)**

Esegui con l’istanza sorgente in modalità manutenzione. L&#39;origine deve rimanere bloccata per l&#39;intera durata di questa fase. Non disattivare la modalità di manutenzione fino al completamento della **fase 3**.

```bash
./bin/console migration:during-maintenance
```

1. **Configurazione del tunnel cloud**. Per [!DNL Adobe Commerce on Cloud] istanze di origine, riapre i tunnel cloud e verifica la connettività del database. Ignorato automaticamente per le istanze locali.
1. **Estrazione dati**: estrae i dati dall&#39;istanza di origine bloccata.
1. **Pulizia visualizzazione di gestione temporanea** — rimuove le visualizzazioni di gestione temporanea dall&#39;origine utilizzando una connessione di database diretta (sicura in modalità di manutenzione).
1. **Carica nella destinazione** — carica i dati estratti nell&#39;istanza di destinazione [!DNL Adobe Commerce as a Cloud Service] e attende il completamento.
1. **Verifica integrità dati**: attiva la verifica del checksum CDMS ed esegue i test di verifica API locali. I risultati vengono registrati e gli errori non arrestano la pipeline.
1. **Pulizia dei dati di test sulla destinazione** — rimuove i dati di test sintetici dall&#39;istanza di destinazione.
1. **Risultati processo**: genera un riepilogo della migrazione e, facoltativamente, scarica gli artefatti dall&#39;archivio.

**Fase 4 — Disattivazione della modalità di manutenzione (manuale, condizionale)**

Questa fase disattiva la modalità di manutenzione, riabilitando il traffico verso l’istanza sorgente. Questo passaggio è necessario prima di eseguire la fase di pulizia perché la pulizia comunica con l&#39;origine tramite REST e non riesce con `HTTP 503` se la modalità di manutenzione è ancora attiva.

Nel server Commerce di origine eseguire:

```bash
bin/magento maintenance:disable
```

**Fase 5 — Pulizia (facoltativa, l&#39;origine deve essere attiva)**

Rimuovere i clienti e gli ordini del test sintetico creati in **Fase 1** dall&#39;istanza di origine tramite REST. Questa fase può essere eseguita solo dopo la disattivazione della modalità di manutenzione.

>[!NOTE]
>
>Ignora questa fase se `SKIP_TEST_DATA_CREATION=true` è impostato in `.env`, perché non sono stati creati dati di test.

Torna alla directory principale del server ed esegui:

```bash
./bin/console migration:cleanup
```

1. **Configurazione connessione al database**. Per [!DNL Adobe Commerce on Cloud] istanze di origine, riapre i tunnel cloud. Per le istanze locali, stabilisce e verifica la connettività diretta del database.
1. **Pulizia REST di Source**: rimuove i clienti e gli ordini dei test sintetici dall&#39;origine tramite l&#39;API REST.

## Riprendere o eseguire nuovamente una migrazione

Lo strumento di migrazione tiene traccia dell&#39;avanzamento utilizzando un file `.migration_id` nella directory principale del progetto. Questo file viene creato automaticamente all’avvio di una nuova migrazione e registra l’identificatore di migrazione corrente.

### Riprendi dopo un errore

Se un’esecuzione della migrazione non riesce o viene interrotta, esegui nuovamente lo stesso comando per riprendere dall’ultimo passaggio riuscito (estrazione, caricamento o verifica) anziché riavviare il sistema da zero. I passaggi già completati vengono saltati automaticamente.

>[!IMPORTANT]
>
>Quando si riprende la fase `migration:during-maintenance`, l&#39;origine deve rimanere in modalità di manutenzione per tutto. Se l’origine è stata rimossa dalla manutenzione o i dati sono stati modificati tra un’esecuzione e l’altra, la ripresa della migrazione può produrre risultati incoerenti.

### Avvia una nuova migrazione

Per ignorare un&#39;esecuzione precedente e avviare una migrazione completamente nuova, eliminare il file `.migration_id` prima di avviare la migrazione successiva:

```bash
rm .migration_id
```

Se `.migration_id` esiste e la migrazione precedente è già stata completata, lo strumento stampa un messaggio che indica che la migrazione è già stata eseguita e consiglia di eliminare il file.

## Revisione dei registri e debug

Tutti i registri di migrazione vengono scritti nella directory `logs/` nella directory principale del progetto e sono organizzati in sottodirectory con marca temporale:

```text
logs/
  2026-03-23_14-30-00/     ← one directory per run
    index.log              ← main pipeline log (start here)
    ...
```

- `index.log` è il registro principale di orchestrazione della pipeline. Se un passaggio non è riuscito, viene visualizzato lo script terminato con un codice diverso da zero e il motivo per cui è stato eseguito.
- I registri per passaggio, ad esempio `09b_run_load.log` e `11_verify_data_integrity_local.log`, contengono un output dettagliato per ogni fase.
