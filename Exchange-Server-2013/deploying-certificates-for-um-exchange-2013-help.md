---
title: 'Distribuzione dei certificati per la messaggistica unificata: Exchange 2013 Help'
TOCTitle: Distribuzione dei certificati per la messaggistica unificata
ms:assetid: 95658f6f-eac2-4674-90e7-f2d3f25c5242
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee681661(v=EXCHG.150)
ms:contentKeyID: 52063086
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuzione dei certificati per la messaggistica unificata

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-04-29_

È possibile utilizzare TLS (Transport Layer Security) reciproca per abilitare Messaggistica unificata per crittografare i dati inviati tra server Microsoft Exchange 2013 e gateway VoIP, IP PBX, session border controller (SBC) e Microsoft Lync Server. I certificati associano l'identità del proprietario del certificato a una coppia di chiavi elettroniche (pubblica e privata) utilizzate per crittografare e firmare le informazioni con firma digitale.

Se si utilizzano dial plan protetti con SIP o protetti nell'organizzazione Exchange 2010, sarà necessario importare i certificati utilizzati nei server Accesso client di Exchange 2013 che eseguono il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e i server Cassette postali che eseguono il servizio Messaggistica unificata di Microsoft Exchange. È possibile utilizzare uno dei seguenti certificati per i servizi Messaggistica unificata e routing delle chiamate di messaggistica unificata:

  - Certificato (Exchange) autofirmato

  - Certificato di infrastruttura a chiave pubblica (PKI) interna

  - Certificato commerciale di terze parti

Per impostazione predefinita, durante l'installazione di Messaggistica unificata, viene creato un certificato autofirmato, che può essere utilizzato con gateway VoIP, IP PBX e SBC, ma non durante l'integrazione della messaggistica unificata con Lync Server. Se si distribuiscono certificati da utilizzare con Lync Server, è necessario eseguire la procedura guidata relativa al certificato Exchange o il cmdlet **New-ExchangeCertificate** per ottenere un certificato emesso da un'autorità di certificazione (CA) interna o PKI oppure è necessario acquistare un certificato di terze parti o commerciale che sia riconosciuto come trusted sia da Messaggistica unificata sia da Lync Server.

## Distribuzione di certificati per gateway VoIP, IP PBX e SBC

Per abilitare Messaggistica unificata a crittografare i dati inviati tra gateway VoIP, IP PBX e SBC, è necessario procedere come segue:

  - Utilizzare il certificato di messaggistica unificata autofirmato, creare la richiesta per un nuovo certificato di Exchange e ottenere un certificato PKI interno oppure acquistare un certificato commerciale di terze parti che sia possibile utilizzare per TLS reciproco tra Messaggistica unificata e gateway VoIP, IP PBX e SBC.

  - Importare il certificato che verrà utilizzato su tutti i server cassette postali e Accesso client nell'organizzazione.

  - Abilitare il certificato che verrà utilizzato dai servizi di messaggistica unificata.

  - Importare il certificato su gateway VoIP, IP PBX e SBC

  - Configurare il dial plan di messaggistica unificata come dial plan SIP con protezione o protetto.

  - Configurare la modalità di avvio della messaggistica unificata sui server Accesso client e Cassette postali nell'organizzazione.

  - Creare i gateway IP di messaggistica unificata richiesti con un nome di dominio completo (FQDN, fully qualified domain name).

  - Configurare la porta di attesa sui gateway IP di messaggistica unificata per utilizzare la porta TLS 5061.

  - Riavviare il servizio routing delle chiamate di messaggistica unificata su tutti i server Accesso client e riavviare il servizio Messaggistica unificata di Microsoft Exchange su tutti i server Cassette postali.

## Distribuzione di certificati per Lync Server

Per crittografare i dati inviati tra Messaggistica unificata e Lync Server, è necessario:

  - Creare la richiesta per un nuovo certificato di Exchange e ottenere un certificato PKI interno oppure acquistare un certificato commerciale di terze parti, che sia riconosciuto come trusted sia da Messaggistica unificata sia da Lync Server.

  - Importare il certificato che verrà utilizzato su tutti i server cassette postali e Accesso client nell'organizzazione.

  - Abilitare il certificato che verrà utilizzato dai servizi di messaggistica unificata.

  - Importare il certificato su computer che eseguono Lync Server.

  - Configurare il dial plan di messaggistica unificata SIP URI come SIP con protezione o protetto.

  - Configurare la modalità di avvio della messaggistica unificata sui server Accesso client e Cassette postali nell'organizzazione.

  - Eseguire OcsUmUtil.exe da un computer Lync Server.

  - Riavviare il servizio routing delle chiamate di messaggistica unificata su tutti i server Accesso client e riavviare il servizio Messaggistica unificata di Microsoft Exchange su tutti i server Cassette postali nell'organizzazione. Per dettagli, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

  - Riavviare il servizio Lync Server Front-End su tutti i Lync Server che fanno parte di un pool Front End di Enterprise Edition oppure riavviare i server Front End di Standard Edition. È possibile utilizzare il cmdlet **Stop-CsWindowsService** per interrompere i servizi Lync Server e il cmdlet **Start-CsWindowsService** per avviare i servizi Lync Server.
    
    I cmdlet **Start-CsWindowsService** e **Stop-CsWindowsService** sono analoghi a quelli generici di Windows PowerShell **Start-Service** e **Stop-Service**. Se lo si desidera, è possibile utilizzare i cmdlet **Start-Service** o **Stop-Service** per avviare e arrestare un servizio Lync Server. Tuttavia, i cmdlet **Start-CsWindowsServiceStop-CsWindowsService** includono un parametro *ComputerName* che facilita l'arresto e l'avvio di un servizio Lync Server su un computer remoto. A tal fine, includere il parametro *ComputerName* seguito dal nome di dominio completo (FQDN) del computer remoto. I cmdlet **Start-Service** e **Stop-Service** non dispongono di un parametro simile.
    

    > [!NOTE]
    > Per l'integrazione completa di Messaggistica unificata e Lync Server, è inoltre necessario eseguire lo script ExchUcUtil.ps1 su ciascun server Cassette postali o Accesso client nell'organizzazione.


