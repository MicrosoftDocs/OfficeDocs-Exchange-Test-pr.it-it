---
title: 'Dial plan di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Dial plan di messaggistica unificata
ms:assetid: ed7afc03-94af-4b23-8745-6a61f203c149
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125151(v=EXCHG.150)
ms:contentKeyID: 50481990
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dial plan di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

I dial plan di messaggistica unificata sono i componenti principali della messaggistica unificata e sono necessari per una corretta distribuzione della messaggistica unificata nella rete. Nelle seguenti sezioni vengono descritti i dial plan di messaggistica unificata e il loro utilizzo nella distribuzione.

## Informazioni generali sui dial plan di messaggistica unificata

I dial plan di messaggistica unificata rappresentano un insieme di sistemi PBX (Private Branch eXchange) o IP PBX che condividono i numeri di interno comuni degli utenti. Gli interni di tutti gli utenti ospitati su PBX o IP PBX all'interno di un dial plan contengono lo stesso numero di cifre. Gli utenti possono chiamarsi digitando il numero dell'interno senza aggiungere un numero particolare o digitare un numero di telefono completo.

Un dial plan di messaggistica unificata riflette un dial plan di telefonia. Un dial plan di telefonia viene configurato su PBX o IP PBX.

Nella messaggistica unificata possono essere presenti le seguenti topologie di dial plan di messaggistica unificata:

  - Un singolo dial plan che rappresenta un sottoinsieme di interni o tutti gli interni di un'organizzazione che dispone di un singolo PBX o IP PBX.

  - Un singolo dial plan che rappresenta un sottoinsieme di interni o tutti gli interni di un'organizzazione che dispone di più PBX o IP PBX in rete.

  - Più dial plan che rappresentano un sottoinsieme di interni o tutti gli interni di un'organizzazione che dispone di un singolo PBX o IP PBX.

  - Più dial plan che rappresentano un sottoinsieme di interni o tutti gli interni di un'organizzazione che dispone di più PBX o IP PBX.

Gli utenti che appartengono allo stesso dial plan presentano le seguenti caratteristiche:

  - Un numero di interno che identifica in maniera univoca la cassetta postale dell'utente nel dial plan.

  - La possibilità di chiamare o inviare messaggi vocali ad altri membri del dial plan utilizzando solo il numero di interno.

Per ulteriori informazioni sulle modalità di abilitazione di un utente alla messaggistica unificata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

I dial plan di messaggistica unificata vengono utilizzati nella messaggistica unificata per garantire che i numeri di interno degli utenti siano univoci. In alcune reti di telefonia possono esistere più PBX o IP PBX. In tali reti di telefonia possono essere presenti due utenti il cui numero di interno telefonico è identico. I dial plan di messaggistica unificata consentono di risolvere una situazione simile. L'inserimento di due utenti in due dial plan di messaggistica unificata separati rende univoci i loro numeri di interno.

## Funzionamento dei dial plan

Quando una rete di telefonia viene integrata nella messaggistica unificata, è necessario che siano presenti uno o più dispositivi hardware denominati gateway VoIP (Voice over IP) o IP PBX che consentono di connettere la rete di telefonia alla rete a commutazione di pacchetto basata su IP. I gateway VoIP convertono i protocolli a commutazione di circuito da un sistema PBX che si trova in una rete di telefonia in un protocollo a commutazione di dati come IP. I sistemi IP PBX convertono anche i protocolli a commutazione di circuito in un protocollo a commutazione di dati. I session border controller (SBC) consentono di connettere due reti basate su IP in una rete WAN pubblica o privata e sono presenti nelle distribuzioni di messaggistica unificata online o ibride. Ciascun gateway VoIP, PBX IP o session border controller (SBC) nell'organizzazione è rappresentato da un gateway IP di messaggistica unificata. Per ulteriori informazioni sui gateway IP di messaggistica unificata, vedere [Gateway IP di messaggistica unificata](um-ip-gateways-exchange-2013-help.md).

La messaggistica unificata richiede la creazione di almeno un dial plan di messaggistica unificata. Che si creino uno o più dial plan, tutti i server Exchange dell'organizzazione risponderanno alle chiamate in arrivo. Devono essere presenti anche uno o più gateway IP di messaggistica unificata associati al dial plan. Nelle distribuzioni locale e ibride, dopo aver installato i server Exchange e associato un gateway IP di messaggistica unificata, tutti i server Exchange risponderanno alle chiamate in arrivo per tutti i dial plan. Tuttavia, per le distribuzioni locali e ibride, quando si integrano Exchange e Lync Server, è necessario creare dial plan SIP URI.


> [!IMPORTANT]
> Ogni volta che viene creato un dial plan di messaggistica unificata, viene creato anche un criterio cassetta postale di messaggistica unificata. Il criterio cassetta postale di messaggistica unificata viene chiamato Criterio predefinito &lt;<EM>nome dial plan</EM>&gt;. Questo criterio cassetta postale di messaggistica unificata può essere eliminato o configurato in modo diverso.



Se si specifica un dial plan di messaggistica unificata quando si crea il primo gateway IP di messaggistica unificata, viene creato anche un gruppo di risposta di messaggistica unificata predefinito. La creazione di tali componenti consente ai server Exchange di ricevere chiamate da un gateway VoIP, IP PBX o SBC e quindi di elaborare tali chiamate in arrivo per gli utenti associati al dial plan di messaggistica unificata. Nelle distribuzioni locali o ibride, quando il gateway VoIP, il PBX IP o l'SBC riceve una chiamata, la inoltra a un server Accesso client. Il server Accesso client inoltra quindi la chiamata a un server Cassette postali, che cerca una corrispondenza tra il numero di interno dell'utente e il dial plan di messaggistica unificata associato.

## Tipi di dial plan

Un URI (Uniform Resource Identifier) è una stringa di caratteri (numerici o alfabetici) utilizzata per identificare una risorsa o assegnarle un nome. Nella messaggistica unificata, lo scopo principale di un URI è consentire ai dispositivi VoIP di comunicare con altri dispositivi tramite protocolli specifici. Un URI definisce il formato di numerazione e di denominazione oppure lo schema utilizzato per le informazioni relative alle parti chiamante e chiamata contenute all'interno di un'intestazione SIP (Session Initiation Protocol) per una chiamata in arrivo o in uscita.

I tipi di dial plan di messaggistica unificata creati dipendono dai tipi di URI supportati dai gateway VoIP, o IP PBX dell'organizzazione. Il tipo di URI è il tipo di stringa inviata dal gateway PBX o IP PBX. Quando si crea un dial plan, è necessario conoscere gli specifici tipi di URI supportati dai PBX o dagli IP PBX. Esistono tre formati o tipi di URI che possono essere configurati nei dial plan di messaggistica unificata:

  - Interno (TeleExtn)

  - URI SIP

  - E.164

Nella messaggistica unificata, ogni volta che viene creato un dial plan, questo utilizza per impostazione predefinita il tipo di formato URI per l'interno telefonico. Dopo aver creato un dial plan non è più possibile modificare il tipo di URI. È necessario eliminare il dial plan esistente e crearne un altro con il tipo di URI corretto.

## Tipo di URI dell'interno telefonico

Il tipo di URI Interno telefonico è il tipo di dial plan di messaggistica unificata più comune ed è utilizzato con i gateway IP PBX e PBX. Quando si configura un dial plan Interno telefonico (TelExtn), i gateway VoIP, PBX e IP PBX utilizzati devono supportare il tipo di URI TelExtn. Attualmente la maggior parte dei PBX e IP PBX supportano questo tipo di URI.

Quando una chiamata viene ricevuta da un PBX e l'utente abilitato alla messaggistica unificata non è disponibile per rispondere alla chiamata, il PBX inoltrerà la chiamata al gateway VoIP. Il gateway VoIP o IP PBX utilizzato convertirà la chiamata da un protocollo basato su circuito a un protocollo basato su IP. Nell'intestazione relativa al pacchetto SIP ricevuto dal gateway VoIP o dall'IP PBX, le informazioni relative alle parti chiamante e chiamata sono elencate in uno dei seguenti formati:

  - Tel:512345

  - 512345@\<*Indirizzo IP*\>

Il formato Interno telefonico (TelExtn) utilizzato è basato sulla configurazione del gateway VoIP o IP PBX.

## Tipo URI SIP

SIP (Session Initiation Protocol) è un protocollo standard utilizzato per avviare le sessioni utente interattive che includono elementi multimediali quali video, voce, chat e giochi. SIP è un protocollo basato sulla richiesta alla risposta, che risponde alle richieste dei client e alle risposte dei server. I client vengono identificati dagli URI SIP. Le richieste possono essere inviate tramite qualsiasi protocollo di trasporto, ad esempio UDP o TCP. SIP determina l'endpoint che deve essere utilizzato per la sessione selezionando i supporti di comunicazione e i parametri dei supporti.

Quando si crea un nuovo dial plan, è possibile scegliere di creare un dial plan URI SIP se nell'ambiente è stato distribuito Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. È possibile anche creare un dial plan URI SIP se l'organizzazione dispone di gateway IP PBX o PBX abilitati per SIP. Nel secondo caso, l'organizzazione deve anche supportare gli URI SIP e il routing SIP.

Un URI SIP è il numero di telefono SIP di un utente. L'URI SIP è simile a un indirizzo di posta elettronica ed è scritto nel seguente formato: sip*:\<nome utente\>@\<dominio o indirizzo IP\>*:*Porta*. Quando viene utilizzato un IP PBX o PBX abilitato a SIP per inviare una chiamata ai server Exchange, il dispositivo invierà solo l'URI SIP per le parti chiamante e chiamata nell'intestazione SIP e non includerà i numeri di interno.

## Tipo di URI E.164

E.164 è un formato di numerazione standard che definisce il piano di numerazione internazionale per le telecomunicazioni pubbliche utilizzato nella rete PSTN (Public Switched Telephone Network) e in alcune reti di dati. E.164 definisce il formato dei numeri di telefono. I numeri E.164 possono avere un massimo di 15 cifre e sono solitamente scritti con un segno più (+) che precede le cifre del numero di telefono. Per comporre un numero di telefono in formato E.164 da un telefono, è necessario includere nel numero che viene composto l'appropriato prefisso per le chiamate internazionali. In un piano di numerazione E.164 per i sistemi telefonici pubblici, ciascun numero assegnato include un codice di paese (CC), un codice di destinazione nazionale (NDC) e un numero del sottoscrittore (SN).

Quando si crea un nuovo dial plan, è possibile creare un dial plan E.164. Tuttavia, se si crea e configura un dial plan E.164, i PBX e gli IP PBX devono supportate il routing E.164. L'intestazione SIP ricevuta dal gateway VoIP associato a un dial plan E.164 includerà il numero di telefono in formato E.164 e le informazioni relative a parti chiamante e chiamata e verrà riportata nel seguente formato: Tel:+14255550123. Per le distribuzioni di Exchange Online con la messaggistica unificata di Exchange e Lync Server, è necessario utilizzare i numeri E.164 formattati per Outlook Voice Access e i numeri degli operatori automatici.

## Protezione VoIP

I server Messaggistica unificata comunicano con i gateway IP, i PBX IP e altri computer Exchange in modalità non protetta, SIP con protezione o protetta a seconda della modalità di configurazione del dial plan di messaggistica unificata. Nelle distribuzioni locali e ibride, i server Accesso client e Cassette postali possono operare in qualsiasi modalità configurata in un dial plan, dato che i server attendono le richieste non protette sulla porta TCP 5060 e le richieste protette sulla porta TCP 5061 contemporaneamente se sono configurati per l'avvio in modalità doppia. I server Accesso client e Cassette postali rispondono a tutte le chiamate in arrivo per tutti i dial plan di messaggistica unificata, ma tali dial plan possono avere impostazioni di protezione VoIP diverse.

Nelle distribuzioni locali e ibride, per impostazione predefinita quando si crea un dial plan di messaggistica unificata le comunicazioni avvengono in modalità non protetta e i server Accesso client e Cassette postali inviano e ricevono i dati dai gateway VoIP, IP PBX e SBC senza utilizzare la crittografia. Nella modalità non protetta, le informazioni relative al canale di supporto RTP e alla segnalazione SIP non vengono crittografate. Il cmdlet **Get-UMDialPlan** in Shell consente di determinare le impostazioni di protezione per uno specifico dial plan di messaggistica unificata.

Nelle distribuzioni locali e ibride, è possibile configurare un server Accesso client e Cassette postali per utilizzare MTLS (Mutual Transport Layer Security) per crittografare il traffico SIP e RTP inviato e ricevuto da altri server o dispositivi. Quando si seleziona il dial plan per l'utilizzo della modalità SIP con protezione, viene crittografato solo il traffico della segnalazione SIP e i canali di supporto RTP utilizzano sempre il protocollo TCP, non crittografato. Tuttavia, quando si configura il dial plan per l'utilizzo della modalità protetta, il traffico della segnalazione SIP e i canali di supporto RTP sono entrambi crittografati. Un canale dei supporti di segnalazione crittografato che utilizza il protocollo SRTP (Secure Realtime Transport Protocol) utilizza anche MTLS per crittografare i dati VoIP.

È possibile configurare la modalità di protezione VoIP sia quando si crea un nuovo dial plan sia dopo la sua creazione, utilizzando EAC o il cmdlet **Set-UMDialPlan** in Shell. Se si configura il dial plan di messaggistica unificata per l'utilizzo delle modalità protetta o SIP protetta, i server Accesso client e Cassette postali utilizzeranno la crittografia per il traffico di segnalazione SIP, per i canali di supporto RTP o per entrambi. Tuttavia, per essere in grado di inviare i dati crittografati a/da server Exchange, è necessario configurare correttamente il dial plan di messaggistica unificata e i dispositivi VoIP quali gateway VoIP, IP PBX e SBC per il supporto di MTLS.

## Outlook Voice Access

Due tipi di chiamanti hanno accesso al sistema di caselle vocali tramite il numero di Outlook Voice Access configurato in un dial plan di messaggistica unificata: i chiamanti non autenticati e i chiamanti autenticati. Quando un chiamante compone un numero di Outlook Voice Access configurato in un dial plan, viene considerato anonimo o non autenticato fino a quando non fornisce alcune informazioni, tra cui l'interno del sistema di caselle vocali e il PIN. L'unica opzione disponibile per i chiamanti anonimi o non autenticati è la funzionalità di ricerca nella directory. Una volta immessi l'interno del sistema di caselle vocali e il PIN, il chiamante viene autenticato e può accedere alla propria cassetta postale. Dopo aver effettuato l'accesso al sistema di caselle vocali, il chiamante utilizza Outlook Voice Access.

Outlook Voice Access consiste in una serie di prompt vocali che consentono al chiamante di accedere alla posta elettronica, alla posta vocale, al calendario e ad altre informazioni. Outlook Voice Access consente ai chiamanti autenticati di spostarsi tra le informazioni personali della cassetta postale, eseguire chiamate o individuare gli utenti utilizzando gli input del segnale multifrequenza DTMF (definiti anche composizione a toni) o gli input vocali.

## Numeri di Outlook Voice Access

Dopo aver creato un dial plan di messaggistica unificata, è necessario aggiungere almeno un numero di Outlook Voice Access. I numeri di Outlook Voice Access sono anche chiamati numeri pilota del dial plan. Questo numero è utilizzato dagli utenti di Outlook Voice Access per accedere alle loro cassette postali e per eseguire ricerche nella directory.

Per impostazione predefinita, quando si crea un dial plan di messaggistica unificata, non viene configurato alcun numero di Outlook Voice Access. Per consentire agli utenti di utilizzare la funzionalità Outlook Voice Access, è necessario configurare almeno un numero di telefono o di interno. Il numero di caratteri alfanumerici nel numero di Outlook Voice Access non può superare il limite di 20. Dopo aver configurato questo numero nel dial plan, il numero viene visualizzato nelle opzioni di posta vocale in Microsoft Outlook e in Outlook Web App.

È possibile utilizzare la casella **Numeri di Outlook Voice Access** nel dial plan di messaggistica unificata per aggiungere il numero di telefono o di interno che l'utente chiamerà per accedere al sistema di caselle vocali mediante Outlook Voice Access. Nella maggior parte dei casi, è sufficiente immettere un numero di interno o un numero di telefono esterno. Tuttavia, poiché questo campo accetta caratteri alfanumerici, è possibile utilizzare un URI SIP con IP PBX, PBX abilitato per SIP, Office Communications Server 2007 R2 o Microsoft Lync Server.

In base alle esigenze dell'organizzazione, è opportuno configurare uno o più numeri di Outlook Voice Access. È possibile configurare uno o più numeri di Outlook Voice Access su un singolo dial plan di messaggistica unificata, ma non è possibile creare un singolo numero di Outlook Voice Access relativo a più dial plan di messaggistica unificata.

