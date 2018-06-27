---
title: 'Verificare la connettività per messaggistica unificata ai gateway VoIP e PBX: Exchange 2013 Help'
TOCTitle: Verificare la connettività per messaggistica unificata ai gateway VoIP e PBX
ms:assetid: 2aca8631-a99a-4e29-aff0-e462385f03b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996906(v=EXCHG.150)
ms:contentKeyID: 56269830
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Verificare la connettività per messaggistica unificata ai gateway VoIP e PBX

 

_**Si applica a:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2014-09-17_

È possibile verificare il funzionamento della messaggistica unificata e delle relative apparecchiature telefoniche connesse. Quando si esegue la procedura riportata di seguito, i server Accesso client e Cassette postali verificano l'intero funzionamento end-to-end del sistema di segreteria telefonica. Sono inclusi i componenti telefonici connessi ai server Accesso client e Cassette postali, tra cui i gateway VoIP, i sistemi PBX (Private Branch eXchanges) e IP PBX e i cavi.

Per altre attività di gestione relative alla risoluzione dei problemi di messaggistica unificata, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Informazioni preliminari

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere le voci "Server Cassette postali (servizio di messaggistica unificata)" e "Server Accesso client (servizio di routing delle chiamate di messaggistica unificata)" dell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Per eseguire le procedure riportate di seguito, è necessario accedere al server Cassette postali utilizzando un account membro del gruppo Administrators locale.

  - Verificare che il server Cassette postali sia installato nello stesso computer del server Accesso client o in un computer diverso.

  - Verificare che il server Accesso client sia installato nello stesso computer del server Cassette postali o in un computer diverso.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di Shell per verificare il funzionamento dei componenti telefonici e della messaggistica unificata

In questo esempio viene verificata l'abilità del gateway IP di messaggistica unificata per l'ascolto delle richieste SIP in ingresso sulla porta TCP 5060.

    Test-UMConnectivity -ListenPort 5060 -UMIPGateway MyIPGateway

In questo esempio viene verificata la capacità del server Cassette postali locale di utilizzare una connessione TCP non protetta al posto di una connessione TLS reciproca protetta per effettuare una chiamata tramite il gateway IP di messaggistica unificata denominato `MyUMIPGateway` utilizzando il numero di telefono 56780.

    Test-UMConnectivity -UMIPGateway MyUMIPGateway -Phone 56780 -Secured $false

In questo esempio viene verificato il numero di Outlook Voice Access in un dial plan mediante un URI SIP. È possibile utilizzare l'esempio in un ambiente che include Lync Server.

    Test-UMConnectivity -UMIPGateway OCSGateway1 -Phone "sip:SIPdialplan.contoso.com@contoso.com"


> [!NOTE]
> È possibile impostare il parametro <CODE>-Timeout</CODE> con un valore inferiore a 5 secondi. Tuttavia, si consiglia di configurarlo sempre con un valore pari o superiore a 5 secondi. Utilizzare la modalità 2 quando il parametro <CODE>&shy;UMIPGateway</CODE> viene specificato nella sintassi della riga di comando.


