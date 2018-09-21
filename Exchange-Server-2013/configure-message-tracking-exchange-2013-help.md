---
title: 'Configurazione della verifica messaggi: Exchange 2013 Help'
TOCTitle: Configurazione della verifica messaggi
ms:assetid: 50eb5213-cf27-4179-b427-38d751ee4a70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997984(v=EXCHG.150)
ms:contentKeyID: 51407362
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione della verifica messaggi

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-18_

La verifica dei messaggi registra l'attività di trasporto SMTP di tutti i messaggi che vengono trasferiti da e verso il servizio di trasporto o le cassette postali su un server Cassette postali di Exchange Server 2013 Microsoft. I registri di verifica dei messaggi possono essere utilizzati per le indagini sui messaggi, l'analisi del flusso di posta, le segnalazioni e la risoluzione dei problemi.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Servizio di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md) oppure "Configurazione server Cassette postali" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - È possibile utilizzare l'interfaccia di amministrazione di Exchange per abilitare o disabilitare la verifica dei messaggi o configurare il percorso del registro della verifica dei messaggi. Per tutte le altre opzioni di verifica dei messaggi, è necessario utilizzare Exchange Management Shell.

  - Sul server Cassette postali di Exchange 2013, è possibile utilizzare sia il cmdlet **Set-TransportService** che il cmdlet **Set-MailboxServer** per configurare le opzioni di verifica dei messaggi. Nelle procedure di questo argomento viene utilizzato il cmdlet **Set-TransportService**.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare l'interfaccia di amministrazione di Exchange per configurare la verifica dei messaggi sui server Cassette postali

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Selezionare il server Cassette postali da configurare, quindi scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **Registro di trasporto**.

4.  Nella sezione **Registro verifica messaggi**, modificare uno dei seguenti valori:
    
      - **Abilita registro verifica messaggi**   Per disabilitare la verifica dei messaggi sul server, deselezionare la casella di controllo. Per abilitare la verifica dei messaggi sul server, selezionare la casella di controllo.
    
      - **Percorso del registro di verifica messaggi**   Il valore specificato deve essere presente sul server Exchange locale. Se la cartella non esiste, verrà creata quando si fa clic su **Salva**.

5.  Fare clic su **Salva**.

## Utilizzo di Shell per la configurazione della verifica dei messaggi

Per configurare la verifica dei messaggi, eseguire il comando seguente:

    Set-TransportService <ServerIdentity> -MessageTrackingLogEnabled <$true | $false> -MessageTrackingLogMaxAge <dd.hh:mm:ss> -MessageTrackingLogMaxDirectorySize <Size> -MessageTrackingLogMaxFileSize <Size> -MessageTrackingLogPath <LocalFilePath> -MessageTrackingLogSubjectLoggingEnabled <$true|$false>

In questo esempio vengono configurate le seguenti impostazioni del registro di verifica dei messaggi sul server Cassette postali Mailbox01:

  -  Configurare il percorso del file di registro di verifica dei messaggi su D:\\Message Tracking Log. Notare che se la cartella non esiste, verrà creata automaticamente.

  -  Impostare la dimensione massima del file di registro di verifica dei messaggi su 20 MB.

  -  Impostare la dimensione massima della directory del registro di verifica dei messaggi su 1,5 GB.

  -  Impostare la durata massima di un file di registro di verifica dei messaggi su 45 giorni.

<!-- end list -->

    Set-TransportService Mailbox01 -MessageTrackingLogPath "D:\Hub Message Tracking Log" -MessageTrackingLogMaxFileSize 20MB -MessageTrackingLogMaxDirectorySize 1.5GB -MessageTrackingLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>L'impostazione del parametro <EM>MessageTrackingLogPath</EM> sul valore <CODE>$null</CODE>, disabilita la verifica dei messaggi. Se però il valore del parametro <EM>MessageTrackingLogEnabled</EM> è <CODE>$true</CODE>, vengono generati gli errori nel registro eventi.</P>
> <LI>
> <P>L'impostazione del parametro <EM>MessageTrackingLogMaxAge</EM> sul valore <CODE>00:00:00</CODE> impedisce la rimozione automatica dei file di registro di verifica dei messaggi che hanno superato il limite di validità.</P>
> <LI>
> <P>Sui server Cassette postali di Exchange 2013 la dimensione massima della directory del registro di verifica dei messaggi è tre volte superiore rispetto al valore del parametro <EM>MessageTrackingLogMaxDirectorySize</EM>. Nonostante i file di registro di verifica dei messaggi vengano generati da quattro servizi differenti che hanno quattro diversi prefissi nel nome, la quantità e la frequenza di dati scritta sui file di registro <STRONG>MSGTRKMA</STRONG> vengono confrontati in modo irrilevante con gli altri tre prefissi del file di registro. Per ulteriori informazioni, vedere la sezione "Struttura dei file di registro della verifica messaggi" nell'argomento <A href="message-tracking-exchange-2013-help.md">Verifica messaggi</A>.</P></LI></UL>



In questo esempio viene disabilitata la registrazione dell'oggetto del messaggio nel registro di verifica dei messaggi sul server Cassette postali Mailbox01:

```powershell
Set-TransportService Mailbox01 -MessageTrackingLogSubjectLoggingEnabled $false
```

In questo esempio viene disabilitata la verifica dei messaggi sul server Cassette postali Mailbox01.

```powershell
Set-TransportService Mailbox01 -MessageTrackingLogEnabled $false
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione della verifica dei messaggi, effettuare le seguenti operazioni:

1.  In Shell, utilizzare il seguente comando:
    
        Get-TransportService <ServerIdentity> | Format-List MessageTrackingLog*

2.  Verificare che i valori visualizzati siano quelli configurati.

