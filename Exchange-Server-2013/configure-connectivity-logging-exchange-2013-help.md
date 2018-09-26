---
title: 'Configurare la registrazione di integrazione applicativa: Exchange 2013 Help'
TOCTitle: Configurare la registrazione di integrazione applicativa
ms:assetid: 24e46a79-33ea-44e9-b03c-549db1c86a6f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996827(v=EXCHG.150)
ms:contentKeyID: 50480184
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la registrazione di integrazione applicativa

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-18_

La registrazione della connettività registra l'attività di connessione in uscita utilizzata per trasmettere i messaggi da un servizio di trasporto su un server Exchange. La registrazione della connettività registra l'origine della connessione, la destinazione, il numero di messaggi e byte trasmessi e le informazioni su eventuali errori di connessione.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Servizio di trasporto", "Servizio di trasporto Front End" e "Servizio di trasporto alle cassette postali" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare l'interfaccia di amministrazione di Exchange per abilitare o disabilitare la registrazione della connettività oppure impostare il percorso del registro solo per il servizio di trasporto. Per tutte le altre opzioni per la registrazione della connettività negli altri servizi di trasporto, utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la configurazione della registrazione della connettività nel servizio di trasporto

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Selezionare il server Cassette postali da configurare, quindi scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **Registro di trasporto**.

4.  Nella sezione **Registro di connettività**, modificare uno dei seguenti valori:
    
      - **Abilita il registro delle connessioni**   Per disabilitare la registrazione della connettività sul server, deselezionare la casella di controllo. Per abilitare la registrazione della connettività sul server, selezionare la casella di controllo.
    
      - **Percorso del registro di connettività**   Il valore specificato deve essere presente sul server Exchange locale. Se la cartella non esiste, verrà creata quando si fa clic su **Salva**.
    
    Al termine, fare clic su **Save**.

## Utilizzo di Shell per la configurazione della registrazione della connettività

Per configurare la registrazione della connettività, utilizzare il seguente comando:
```powershell
    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ConnectivityLogEnabled <$true | $false> -ConnectivityLogMaxAge <dd.hh:mm:ss> -ConnectivityLogMaxDirectorySize <Size> -ConnectivityLogMaxFileSize <Size> -ConnectivityLogPath <LocalFilePath>
```

In questo esempio vengono definite le impostazioni per il registro della connettività nel servizio di trasporto sul server Cassette postali Mailbox01:

  -  Imposta il percorso dei file di registro della connettività su D:\\Hub Connectivity Log. Notare che se la cartella non esiste, verrà creata automaticamente.

  -  Imposta la dimensione massima di un file di registro della connettività su 20 MB.

  -  Imposta la dimensione massima della directory del registro della connettività su 1,5 GB.

  -  Imposta la durata massima di un file di registro della connettività su 45 giorni.

<!-- end list -->
```powershell
    Set-TransportService Mailbox01 -ConnectivityLogPath "D:\Hub Connectivity Log" -ConnectivityLogMaxFileSize 20MB -ConnectivityLogMaxDirectorySize 1.5GB -ConnectivityLogMaxAge 45.00:00:00
```

> [!NOTE]
> <UL>
> <LI>
> <P>Per configurare le impostazioni del registro della connettività nel servizio di trasporto alle cassette postali su un server Cassette postali, utilizzare il cmdlet <STRONG>Set-MailboxTransportService</STRONG>. Per configurare le impostazioni del registro della connettività nel servizio di trasporto alle cassette postali su un server Cassette postali, utilizzare il cmdlet <STRONG>Set-FrontEndTransportService</STRONG>.</P>
> <LI>
> <P>Impostare il valore del parametro <EM>ConnectivityLogPath</EM> su <CODE>$null</CODE> disabilita la registrazione della connettività. Se però il valore del parametro <EM>ConnectivityLogEnabled</EM> è <CODE>$true</CODE>, vengono generati gli errori nel registro eventi.</P>
> <LI>
> <P>Se il parametro <EM>ConnectivityLogMaxAge</EM> viene impostato su <CODE>00:00:00</CODE>, si evita che i file di registro della connettività vengano rimossi automaticamente dopo un determinato periodo di tempo.</P></LI></UL>



## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente configurato la registrazione della connettività, fare quanto segue:

1.  In Shell, utilizzare il seguente comando:
    ```powershell
        <Get-TransportService | Get-FrontEndTransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List ConnectivityLog*
    ```
2.  Verificare che i valori visualizzati siano quelli configurati.

