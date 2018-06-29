---
title: 'Configurare il flusso della posta Internet tramite un server Trasporto Edge senza utilizzare EdgeSync: Exchange 2013 Help'
TOCTitle: Configurare il flusso della posta Internet tramite un server Trasporto Edge senza utilizzare EdgeSync
ms:assetid: 6bb98d10-6f12-4b08-a58e-36375f605d65
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232082(v=EXCHG.150)
ms:contentKeyID: 61183409
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il flusso della posta Internet tramite un server Trasporto Edge senza utilizzare EdgeSync

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-01-23_

Si consiglia di utilizzare il processo sottoscrizione di Edge per stabilire il flusso di posta tra l'organizzazione Exchange e il server Trasporto Edge. Tuttavia, alcune situazioni possono impedire la sottoscrizione al server di Trasporto Edge all'organizzazione Exchange utilizzando il processo di Trasporto Edge. Per stabilire manualmente il flusso di posta tra l'organizzazione di Exchange e un server Trasporto Edge, è necessario creare e configurare i connettori di invio e di ricezione sul server Trasporto Edge e sui server cassette postali dell'organizzazione di Exchange.

## Informazioni preliminari

  - Tempo stimato per il completamento di questa attività: 30 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Le voci "Connettori di invio", "Connettori di invio - Trasporto Edge" e "Connettori di ricezione - Trasporto Edge" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - In questa procedura viene utilizzata l'autenticazione di base tramite TLS (Transport Layer Security) per fornire la crittografia e l'autenticazione. Se si utilizza questo metodo di autenticazione, è necessario che nel server di ricezione sia installato un certificato server X.509 SSL (Secure Sockets Layer). Il valore del nome di dominio completo (FQDN, Fully Qualified Domain Name) configurato sul connettore di ricezione deve corrispondere al nome di dominio completo riportato nel certificato server SSL. Per impostazione predefinita, il valore del nome di dominio completo nel connettore di ricezione corrisponde a quello del server in cui si trova il connettore.

  - Inoltre, è possibile utilizzare il metodo di autenticazione Protetto esternamente. Tuttavia, in questo caso, la comunicazione tra il server Trasporto Edge e il server cassette postali non vengono autenticati o crittografati da Exchange. Si consiglia di utilizzare il metodo di autenticazione Protetto esternamente sono quando viene utilizzato anche un metodo di crittografia aggiuntivo. Il metodo di crittografia può essere un'associazione IPsec (Internet Protocol security) o una connessione VPN (Virtual Private Network).

  - Un server Trasporto Edge, in genere, è *multihomed*. Questo significa che il server Trasporto Edge dispone di schede di rete collegate a più segmenti di rete. Ciascuna di queste schede di rete presenta una configurazione IP univoca. È necessario configurare la scheda di rete collegata al segmento di rete esterno o pubblico per l'utilizzo di un server DNS (Domain Name System) pubblico per la risoluzione dei nomi. Questo consente al server di risolvere i nomi di dominio SMPT per i record di risorsa MX e di instradare la posta a Internet. È necessario configurare la scheda di rete collegata al segmento di rete interno o privato per l'utilizzo di un server DNS nella rete perimetrale o disporre di un file Host disponibile.

  - È necessario creare un account utente in Active Directory e aggiungerlo al gruppo di protezione universale nel computer Exchange Server. Tale account verrà utilizzato dal connettore di invio sul server di Trasporto Edge per autenticare il server cassette postali di destinazione nell'organizzazione di Exchange.
    

    > [!IMPORTANT]
    > A questo account vengono concesse le autorizzazioni assegnate ai computer che eseguono Exchange Server. Si consiglia di prestare particolare attenzione alla salvaguardia delle credenziali dell'account per impedirne un utilizzo non appropriato. L'account può essere configurato per consentire l'accesso solo a computer specifici.



## Procedure del server Trasporto Edge

Sul server Trasporto Edge sono necessari i connettori seguenti:

  - Un connettore di invio configurato per inviare messaggi a Internet

  - Un connettore di invio configurato per inviare messaggi ai server cassette postali nell'organizzazione Exchange

  - Un connettore di ricezione configurato per ricevere messaggi solo dai server cassette postali nell'organizzazione Exchange

  - Un connettore di ricezione configurato per accettare messaggi solo da Internet

Per impostazione predefinita, viene creato un singolo connettore di ricezione durante l'installazione del ruolo del server Trasporto Edge. Tale connettore può essere utilizzato sia per i messaggi Internet in arrivo che per quelli in uscita dai server cassette postali. In genere, durante il processo di sottoscrizione di Edge vengono configurate automaticamente l'autenticazione e le autorizzazioni corrette sul server di ricezione predefinito. Se non viene utilizzato questo processo, si consiglia di modificare il connettore di ricezione predefinito sul server Trasporto Edge in modo che accetti solo i messaggi provenienti da Internet. È quindi necessario creare un connettore di ricezione sul server Trasporto Edge configurato per accettare solo i messaggi dai server cassette postali interni.

Le seguenti sezioni forniscono una guida alla procedura di configurazione necessaria alla preparazione del server Trasporto Edge per comunicare con l'organizzazione Exchange.


> [!NOTE]
> È possibile utilizzare solo la Shell per eseguire tali procedure nei server Trasporto Edge.



## Passo 1: creare un connettore di invio configurato per l'invio dei messaggi a Internet

Il connettore di invio richiede la seguente configurazione:

  - **Nome** Per Internet (o qualsiasi nome descrittivo)

  - **Tipo di utilizzo**   Internet

  - **Spazi indirizzo**   "\*" (tutti i domini)

  - **Impostazioni di rete**   Utilizzare i record DNS MX per instradare automaticamente la posta. A seconda della configurazione di rete, è anche possibile instradare la posta attraverso uno SmartHost. Lo SmartHost instrada quindi la posta in Internet.

Per creare un connettore di invio configurato per l'invio di messaggi a Internet, eseguire il seguente comando.

    New-SendConnector -Name "To Internet" -AddressSpaces * -Usage Internet -DNSRoutingEnabled $true

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-SendConnector](https://technet.microsoft.com/it-it/library/aa998936\(v=exchg.150\)).

## Passo 2: creare un connettore di invio configurato per l'invio di messaggi all'organizzazione Exchange

Utilizzare il cmdlet **New-SendConnector** per creare un connettore di invio.


> [!NOTE]
> Prima di creare il connettore di invio, è necessario eseguire il comando <STRONG>Get-Credential</STRONG> per salvare il nome utente e la password che verranno utilizzati in una variabile temporanea. Questa operazione è necessaria, in quanto il cmdlet <STRONG>New-SendConnector</STRONG> non accetta le credenziali utente in testo normale.



Il connettore di invio richiede la seguente configurazione:

  - **Nome** All'organizzazione interna (o qualsiasi nome descrittivo)

  - **Tipo di utilizzo**   Interno

  - **Spazi indirizzo**   Tutti i domini accettati per l'organizzazione Exchange. Esempio, \*.contoso.com.

  - Routing DNS disabilitato (routing smart host abilitato)

  - **Smarthost** FQDN di uno o più server di cassette postali come Smarthost. Ad esempio, mbxserver01.contoso.com e mbxserver02.contoso.com.

  - **Metodi di autenticazione SmartHost**   Autenticazione di base su TLS

  - **Credenziali di autenticazione Smart host** Credenziali per l'account utente nel dominio interno. È necessario innanzitutto salvare nome utente e password in una variabile temporale, perché il cmdlet **New-SendConnector** non accetterà le credenziali utente nel testo normale.

Per creare un connettore di invio configurato per l'invio di messaggi all'organizzazione di Exchange, eseguire i seguenti comandi.

    $MailboxCredentials = Get-Credential
    New-SendConnector -Name "To Internal Org" -Usage Internal -AddressSpaces *.contoso.com -DNSRoutingEnabled $false -SmartHosts mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $MailboxCredentials

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-SendConnector](https://technet.microsoft.com/it-it/library/aa998936\(v=exchg.150\)).

## Passo 3: modificare il connettore di ricezione predefinito per accettare solo i messaggi provenienti da Internet

È necessario apportare le seguenti modifiche di configurazione al connettore di ricezione predefinito:

  - Modificare il nome in modo da utilizzare il connettore esclusivamente per ricevere la posta elettronica da Internet. Il nome del connettore di ricezione predefinito è "Connettore di ricezione interno predefinito \<nome server Trasporto Edge\>".

  - Modificare i binding di rete per accettare solo i messaggi provenienti dalla scheda di rete accessibile da Internet. Ad esempio, 10.1.1.1 e il valore della porta standard SMTP TCP pari a 25.

Per modificare il connettore di ricezione predefinito solo per accettare messaggi da Internet, eseguire il seguente comando.

    Set-ReceiveConnector "Default internal Receive connector Edge01" -Name "From Internet" -Bindings 10.1.1.1:25

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125140\(v=exchg.150\)).

## Passo 4: creare un connettore di ricezione configurato per accettare solo i messaggi provenienti dall'organizzazione Exchange

Nel connettore di ricezione è necessario impostare la seguente configurazione:

  - **Nome** Dall'organizzazione interna (o qualsiasi nome descrittivo)

  - **Tipo di utilizzo**   Interno

  - **Binding della rete locale**   Scheda di rete con connessione Internet diretta. Ad esempio, 10.1.1.2 e il valore della porta standard SMTP TCP pari a 25.

  - **Impostazioni della rete remota**   Indirizzo IP di uno o più server cassette postali nell'organizzazione Exchange. Ad esempio, 192.168.5.10 e 192.168.5.20.

  - **Metodi di autenticazione** TLS, autenticazione di base, autenticazione di base tramite TLS e autenticazione di Exchange Server.

Per creare un connettore di ricezione configurato per la sola accettazione di messaggi all'organizzazione di Exchange, eseguire i seguenti comandi.

    New-ReceiveConnector -Name "From Internal Org" -Usage Internal -AuthMechanism TLS,BasicAuth,BasicAuthRequireTLS,ExchangeServer -Bindings 10.1.1.2:25 -RemoteIPRanges 192.168.5.10,192.168.5.20

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125139\(v=exchg.150\)).

## Come verificare se la procedura ha avuto esito positivo?

Per verificare di aver configurato correttamente i connettori di invio e ricezione richiesti, eseguire i seguenti comandi sul server di Trasporto Edge e verificare che i valori visualizzati siano uguali a quelli configurati.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,SourceTransportServers,DSNRoutingEnabled,SmartHosts,SmartHostAuthMechanism
    Get-ReceiveConnector | Format-List Name,Usage,AuthMechanism,Bindings,RemoteIPRanges

## Procedure del server cassette postali

I server cassette postali nell'organizzazione, richiedono un connettore di invio configurato per l'invio di messaggi al server Trasporto Edge per l'inoltro su Internet.

Per impostazione predefinita, vengono creati due connettori di ricezione durante l'installazione del ruolo del server cassette postali. Il connettore denominato Client *nomeserver* è configurato per accettare messaggi da tutti i client di messaggistica POP3 e IMAP. Il connettore denominato *nomeserver* predefinito è configurato per accettare i messaggi da un server Trasporto Edge. Non è richiesta alcuna modifica su questi connettori.

## Passaggio 5: Creazione di un connettore di invio configurato per inviare i messaggi in uscita al server Trasporto Edge

Il connettore di invio richiede la seguente configurazione:

  - **Nome** A Edge (o qualsiasi nome descrittivo)

  - **Tipo di utilizzo**   Interno

  - **Spazi indirizzo**   "\*" (tutti i domini)

  - Routing DNS disabilitato (routing smart host abilitato)

  - **Smarthost**   Indirizzo IP o FQDN del server di Trasporto Edge. Ad esempio, edge01.contoso.net.

  - **Server cassette postali di origine** FQDN di uno o più server cassette postali. Ad esempio, mbxserver01.contoso.com e mbxserver02.contoso.com.

  - **Metodo di autenticazione SmartHost**   Autenticazione di base su TLS.

  - **Credenziali di autenticazione Smarthost** Credenziali per l'account utente del server Trasporto Edge. È necessario innanzitutto salvare nome utente e password in una variabile temporale, perché il cmdlet **New-SendConnector** non accetterà le credenziali utente nel testo normale.

Per creare un connettore di invio configurato per l'invio di messaggi in uscita al server di Trasporto Edge, eseguire i seguenti comandi.

    $EdgeCredentials = Get-Credential
    New-SendConnector -Name "To Edge" -Usage Internal -AddressSpaces * -DNSRoutingEnabled $false -SmartHosts edge01.contoso.com -SourceTransportServers mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $EdgeCredentials

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-SendConnector](https://technet.microsoft.com/it-it/library/aa998936\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver correttamente creato un connettore di invio configurato per l'invio di messaggi in uscita al server di Trasporto Edge, eseguire il seguente comando su un server cassette postali e verificare che i valori visualizzati siano uguali a quelli configurati.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,DSNRoutingEnabled,SmartHosts,SourceTransportServers,SmartHostAuthMechanism

