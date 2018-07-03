---
title: 'Configurare la registrazione del protocollo: Exchange 2013 Help'
TOCTitle: Configurare la registrazione del protocollo
ms:assetid: c81cac9c-b990-492a-b899-5be8d08a6068
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124531(v=EXCHG.150)
ms:contentKeyID: 50481650
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la registrazione del protocollo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-03-15_

Con la registrazione protocollo vengono registrate le conversazioni SMTP che si verificano sui connettori di invio e ricezione come parte del recapito di un messaggio.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Servizio di trasporto", "Servizio Trasporto front-end", "Servizio Trasporto cassette postali", "Connettori di ricezione" e "Connettori di invio" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare l'interfaccia di amministrazione di Exchange (EAC) per abilitare o disabilitare la registrazione di protocollo per i connettori di invio e ricezione nel servizio di trasporto sui server Cassette postali e per i connettori di ricezione nel servizio Trasporto front-end sui server Accesso client. È inoltre possibile utilizzare EAC per configurare i percorsi dei registri dei protocolli solo per il servizio di trasporto. Per tutte le altre opzioni di registrazione protocollo è necessario utilizzare Shell.

  - La registrazione del protocollo viene abilitata o disabilitata su ciascun connettore. Tutti i connettori di ricezione sul server Exchange condividono gli stessi file e le stesse opzioni di registrazione protocollo. Tali impostazioni sono separate dai file e dalle opzioni di registrazione protocollo che si trovano sullo stesso server.

  - UNRESOLVED\_TOKENBLOCK\_VAL(ALERT\_Do eseguire questa nel server Edge sottoscritto)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Configurazione della registrazione di protocollo tramite EAC

Per utilizzare EAC per abilitare o disabilitare la registrazione di protocollo su un connettore di invio o ricezione nel servizio di trasporto su un server Cassette postali oppure su un connettore di ricezione nel servizio Trasporto front-end su un server Accesso client, effettuare le operazioni seguenti:

1.  In EAC, accedere a **Flusso di posta** \> **Connettori di invio** o **Flusso di posta** \> **Connettori di ricezione**.

2.  Selezionare il connettore da configurare, quindi scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella sezione **Livello di registrazione protocollo** della scheda **Generale** selezionare una delle seguenti opzioni:
    
      - **Nessuna**   Registrazione protocollo disabilitata sul connettore.
    
      - **Verbose**   Registrazione protocollo abilitata sul connettore.
    
    Al termine, fare clic su **Salva**.

Per utilizzare EAC per configurare i percorsi dei registri di protocollo per i connettori di invio e ricezione nel servizio di trasporto su un server Cassette postali, effettuare le operazioni seguenti:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Selezionare il server Cassette postali da configurare, quindi scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server fare clic su **Registri di trasporto**.

4.  Nella sezione **Registro di protocollo** modificare una delle impostazioni seguenti:
    
      - **Percorso registro di protocollo di invio**   Il valore specificato deve trovarsi sul server Exchange locale. Se la cartella non esiste, verrà creata quando si fa clic su **Salva**.
    
      - **Percorso registro di protocollo di ricezione**   Il valore specificato deve trovarsi sul server Exchange locale. Se la cartella non esiste, verrà creata quando si fa clic su **Salva**.
    
    Al termine, fare clic su **Salva**.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver utilizzato correttamente EAC per configurare le impostazioni di registrazione protocollo, effettuare le operazioni seguenti:

1.  Accedere al percorso specificato per i registri di protocollo del connettore di invio e ricezione.

2.  Se è attivata la registrazione protocollo, verificare che venga creato un file di registro. Se si disabilita la registrazione protocollo, verificare che il file di registro più recente non venga più aggiornato.

## Abilitazione o disabilitazione della registrazione protocollo su un connettore di invio o ricezione tramite Shell

Per abilitare o disabilitare la registrazione protocollo su un connettore di invio o ricezione, utilizzare il comando seguente:

    <Set-SendConnector |Set-ReceiveConnector> <ConnectorIdentity> -ProtocolLoggingLevel <Verbose | None>

Con questo esempio viene abilitata la registrazione protocollo per il connettore di ricezione denominato Connection da Contoso.com.

    Set-ReceiveConnector "Connection from Contoso.com" -ProtocolLoggingLevel Verbose

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver abilitato o disabilitato correttamente la registrazione protocollo, procedere come segue:

1.  In Shell, utilizzare il seguente comando:
    
        <Get-SendConnector |Get-ReceiveConnector> | Format-List Name,ProtocolLoggingLevel

2.  Verificare che i valori visualizzati siano quelli configurati.

## Utilizzo di Shell per abilitare o disabilitare la registrazione protocollo sul connettore di invio tra organizzazioni

Per abilitare o disabilitare la registrazione protocollo sul connettore di invio implicito e invisibile tra organizzazioni presente nel servizio di trasporto su un server Cassette postali e nel servizio DI Torto front-end su un server Accesso client, utilizzare il comando seguente:

    <Set-TransportService | Set-FrontEndTransportService> -IntraOrgConnectorProtocolLoggingLevel <Verbose | None>

Con questo esempio viene abilitata la registrazione protocollo sul connettore di invio tra organizzazioni nel servizio di trasporto su un server Cassette postali denominato Mailbox01.

    Set-TransportService Mailbox01 -IntraOrgConnectorProtocolLoggingLevel Verbose

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver abilitato o disabilitato correttamente la registrazione protocollo sul connettore di invio tra organizzazioni, procedere come segue:

1.  In Shell, utilizzare il seguente comando:
    
        <Get-TransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List IntraOrgConnectorProtocolLoggingLevel

2.  Verificare che il valore visualizzato sia quello configurato.

## Utilizzo di Shell per abilitare o disabilitare la registrazione protocollo sul connettore di invio per il recapito delle cassette postali

Per abilitare o disabilitare la registrazione protocollo sul connettore di invio per il recapito delle cassette postali implicito e invisibile presente nel servizio di trasporto cassette postali su un server Cassette postali, utilizzare il comando seguente:

    Set-MailboxTransportService -MailboxDeliveryConnectorProtocolLoggingLevel <Verbose | None>

Con questo esempio viene abilitata la registrazione protocollo sul connettore di ricezione per il recapito delle cassette postali nel servizio di trasporto cassette postali su un server Cassette postali denominato Mailbox01.

    Set-MailboxTransportService Mailbox01 -MailboxDeliveryConnectorProtocolLoggingLevel Verbose

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver abilitato o disabilitato correttamente la registrazione protocollo sul connettore di recapito delle cassette postali, procedere come segue:

1.  In Shell, utilizzare il seguente comando:
    
        Get-MailboxTransportService <ServerIdentity> | Format-List MailboxDeliveryConnectorProtocolLoggingLevel

2.  Verificare che il valore visualizzato sia quello configurato.

## Configurazione delle impostazioni di registrazione protocollo tramite Shell

Per configurare le impostazioni di registrazione protocollo, utilizzare il comando seguente:

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ReceiveProtocolLogPath <LocalFilePath> -SendProtocolLogPath <LocalFilePath> -ReceiveProtocolLogMaxFileSize <Size> -SendProtocolLogMaxFileSize <Size> -ReceiveProtocolLogMaxDirectorySize <Size> -SendProtocolLogMaxDirectorySize <Size> -ReceiveProtocolLogMaxAge <dd.hh:mm:ss> -SendProtocolLogMaxAge <dd.hh:mm:ss>

Con questo esempio vengono configurate le impostazioni del registro di protocollo seguenti nel servizio di trasporto sul server Cassette postali denominato Mailbox01:

  -  Imposta il percorso di tutti i registri di protocollo dei connettori di ricezione su D:\\Hub Receive SMTP Log e tutti i registri di protocollo dei connettori di invio su D:\\Hub Send SMTP Log. Notare che se la cartella non esiste, verrà creata automaticamente.

  -  Imposta la dimensione massima di un file di registro di protocollo del connettore di ricezione e di invio su 20 MB.

  -  Imposta la dimensione massima di una cartella di registro di protocollo del connettore di ricezione e di invio su 400 MB.

  -  Imposta la validità massima di un file di registro di protocollo del connettore di ricezione e di invio su 45 giorni.

<!-- end list -->

    Set-TransportService Mailbox01 -ReceiveProtocolLogPath "D:\Hub Receive SMTP Log" -SendProtocolLogPath "D:\Hub Send SMTP Log" -ReceiveProtocolLogMaxFileSize 20MB -SendProtocolLogMaxFileSize 20MB -ReceiveProtocolLogMaxDirectorySize 400MB -SendProtocolLogMaxDirectorySize 400MB -ReceiveProtocolLogMaxAge 45.00:00:00 -SendProtocolLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>Per configurare le impostazioni di registrazione protocollo nel servizio Trasporto cassette postali su un server Cassette postali, utilizzare il cmdlet <STRONG>Set-MailboxTransportService</STRONG>. Per configurare le impostazioni di registrazione protocollo nel servizio Trasporto front-end su un server Accesso client, utilizzare il cmdlet <STRONG>Set-FrontEndTransportService</STRONG>.</P>
> <LI>
> <P>L'impostazione del valore del parametro <EM>SendProtocolLogPath</EM> o del parametro <EM>ReceiveProtocolLogPath</EM> su <CODE>$null</CODE> consente di disabilitare in maniera efficace la registrazione protocollo per tutti i connettori di invio o di ricezione sul server. Tuttavia, impostando tali parametri su <CODE>$null</CODE> quando la registrazione protocollo è abilitata per qualsiasi connettore di invio sul server, compreso il connettore di invio tra organizzazioni o il connettore di invio per il recapito delle cassette postali, vengono generati errori nel registro eventi.</P>
> <LI>
> <P>L'impostazione del parametro <EM>ReceiveProtocolLogMaxAge</EM> o <EM>SendProtocolLogMaxAge</EM> sul valore <CODE>00:00:00</CODE> impedisce la rimozione automatica dei file di registrazione protocollo a causa del periodo di validità.</P></LI></UL>



## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver configurato correttamente le impostazioni dei registri di protocollo, effettuare le operazioni seguenti:

1.  In Shell, utilizzare il seguente comando:
    
        <Get-TransportService | Get-MailboxTransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List SendConnectorProtocolLog*,ReceiveConnectorProtocolLog*

2.  Verificare che i valori visualizzati siano quelli configurati.

