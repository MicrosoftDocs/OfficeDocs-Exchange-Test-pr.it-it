---
title: 'Configurare la registrazione agente di protezione da posta indesiderata: Exchange 2013 Help'
TOCTitle: Configurare la registrazione agente di protezione da posta indesiderata
ms:assetid: df157ca3-ad8e-4302-acbc-5fbb8570c21d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb691337(v=EXCHG.150)
ms:contentKeyID: 50481876
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la registrazione agente di protezione da posta indesiderata

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

La registrazione agente consente di registrare le azioni eseguite da specifici agenti di protezione dalla posta indesiderata di Exchange. Le informazioni inserite nel registro dipendono dall'agente, dall'evento SMTP e dall'azione eseguita sul messaggio.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Servizio Trasporto" e "Server Trasporto Edge" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per impostazione predefinita le funzionalità di protezione da posta indesiderata non sono abilitate nel servizio di trasporto in un server Cassette postali. Le funzionalità di protezione da posta indesiderata in un server Cassette postali vengono solitamente abilitate se l'organizzazione di Exchange non prevede filtri preventivi di protezione da posta indesiderata prima di accettare i messaggi in arrivo. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione della registrazione degli agenti di protezione da posta indesiderata tramite Shell

Eseguire il comando indicato di seguito:

    Set-TransportService <ServerIdentity> -AgentLogEnabled <$true | $false> -AgentLogMaxAge <dd.hh:mm:ss> -AgentLogMaxDirectorySize <Size> -AgentLogMaxFileSize <Size> -AgentLogPath <LocalFilePath>

In questo esempio vengono realizzate le seguenti impostazioni dei registri degli agenti sul server Cassette postali Mailbox01:

  -  Il percorso dei file di registro degli agenti viene impostato su D:\\Anti-Spam Agente Log. Notare che se la cartella non esiste, verrà creata automaticamente.

  -  La dimensione massima di un file di registro degli agenti viene impostata su 20 MB.

  -  La dimensione massima della directory con i registri degli agenti viene impostata su 400 MB.

  -  Il limite massimo di validità dei file di registro degli agenti viene impostato su 14 giorni.

<!-- end list -->

    Set-TransportService Mailbox01 -AgentLogPath "D:\Anti-Spam Agent Log" -AgentLogMaxFileSize 20MB -AgentLogMaxDirectorySize 400MB -AgentLogMaxAge 14.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>Se si imposta il parametro <EM>AgentLogPath</EM> sul valore <CODE>$null</CODE>, la registrazione agente viene disabilitata. Tuttavia, se si imposta <EM>AgentLogPath</EM> su <CODE>$null</CODE> quando il valore del parametro è <EM>AgentLogEnabled</EM><CODE>$true</CODE>, vengono generati errori nel registro eventi. Per disabilitare la registrazione agente nel modo migliore, è consigliabile impostare <EM>AgentLogEnabled</EM> su <CODE>$false</CODE>.</P>
> <LI>
> <P>L'impostazione del parametro <EM>AgentLogMaxAge</EM> sul valore <CODE>00:00:00</CODE> impedisce la rimozione automatica dei file di registro degli agenti che hanno superato il limite di validità.</P></LI></UL>



Per informazioni dettagliate sulla sintassi e sui parametri, vedere i parametri *AgentLog* in [Set-TransportService](https://technet.microsoft.com/it-it/library/jj215682\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la registrazione degli agenti di protezione dalla posta indesiderata sia stata configurata correttamente, procedere come segue:

1.  In Shell, utilizzare il seguente comando:
    
        Get-TransportService <ServerIdentity> | Format-List AgentLog*

2.  Verificare che i valori visualizzati siano quelli configurati.

