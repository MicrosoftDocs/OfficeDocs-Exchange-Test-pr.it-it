---
title: 'Prerequisiti di Exchange 2013: Exchange 2013 Help'
TOCTitle: Prerequisiti di Exchange 2013
ms:assetid: e21cf744-7813-48b3-9293-5cecd89a6c25
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb691354(v=EXCHG.150)
ms:contentKeyID: 50481883
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Prerequisiti di Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-03-20_

In questo argomento viene descritta la procedura di installazione dei necessari prerequisiti del sistema operativo Windows Server 2012 R2, Windows Server 2012 and Windows Server 2008 R2 con Service Pack 1 (SP1) per i ruoli del server Cassette postali, Accesso client e Trasporto Edge di Microsoft Exchange 2013. Vengono inoltre indicati i prerequisiti indispensabili per l'installazione degli strumenti di gestione di Exchange 2013 nei computer client Windows 8, Windows 8.1 e Windows 7.

  - Che cosa è necessario sapere prima di iniziare

  - Preparazione di Active Directory

  - Prerequisiti di Windows Server 2012 R2 e Windows Server 2012
    
      - Ruoli server Accesso client o Cassette postali
    
      - Ruolo del server Trasporto Edge

  - Prerequisiti di Windows Server 2008 R2 SP1
    
      - Ruoli server Accesso client o Cassette postali
    
      - Ruolo del server Trasporto Edge

  - Prerequisiti di Windows 7 (solo strumenti di amministrazione) (solo strumenti di amministrazione)

  - Prerequisiti di Windows 8 e Windows 8.1 (solo strumenti di amministrazione) (solo strumenti di amministrazione)

## Che cosa è necessario sapere prima di iniziare

  - Le informazioni contenute in questo argomento sono applicabili al Service Pack 1 e alle versioni successive di Exchange 2013.

  - Il ruolo del server Trasporto Edge è disponibile a partire da Exchange 2013 SP1.

  - Assicurarsi che il livello di funzionalità della foresta sia almeno Windows Server 2003 e che Master Schema esegua Windows Server 2003 con Service Pack 2 o versione successiva. Per ulteriori informazioni sul livello di funzionalità di Windows, vedere [Gestire domini e foreste](https://go.microsoft.com/fwlink/p/?linkid=137037).

  - L'opzione di installazione completa di Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2 SP1 deve essere utilizzata per tutti i server che eseguono ruoli del server o strumenti di gestione di Exchange 2013.

  - È necessario innanzitutto aggiungere il computer alla foresta e al dominio interni di Active Directory appropriati.

  - Alcuni prerequisiti richiedono il riavvio del server per completare l'installazione.

  - Installare nel computer in uso gli aggiornamenti di Windows più recenti. Per ulteriori informazioni, vedere [Checklist della distribuzione di protezione](deployment-security-checklist-exchange-2013-help.md).
    

    > [!NOTE]
    > Se si sta installando il ruolo del server Cassette postali e il server deve essere membro di un gruppo di disponibilità del database (DAG), è necessario che sia in esecuzione Windows Server 2012 R2 Standard o Datacenter Edition, Windows Server 2012 Standard o Datacenter Edition oppure Windows Server 2008 R2 SP1 Enterprise Edition. Windows Server 2008 R2 SP 1 Standard Edition non supporta le funzionalità necessarie per i gruppi di disponibilità del database.<BR>Non è possibile eseguire l'aggiornamento di Windows se sul server è installato Exchange.<BR>Per eseguire l'aggiornamento a Microsoft Unified Communications Managed API (UCMA) 4.0, è necessario in primo luogo disinstallare le precedenti versioni di UCMA installate tramite <STRONG>Installazione appplicazioni</STRONG>.




> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Preparazione di Active Directory

Il computer utilizzato per preparare Active Directory a Exchange 2013 deve soddisfare determinati prerequisiti.

Installare, nell'ordine visualizzato, il software seguente nel computer che verrà utilizzato per preparare Active Directory:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (incluso con Windows Server 2012 R2)

Una volta installato il software indicato in precedenza, completare i seguenti passaggi per installare Remote Tools Administration Pack. Dopo avere installato Remote Tools Administration Pack sarà possibile utilizzare il computer per preparare Active Directory. Per ulteriori informazioni sulla preparazione di Active Directory, vedere [Preparazione di Active Directory e dei domini](prepare-active-directory-and-domains-exchange-2013-help.md).

1.  Aprire Windows PowerShell.

2.  Installazione di Remote Tools Administration Pack.
    
      - In un computer con Windows Server 2012 R2 o Windows Server 2012, eseguire il comando seguente.
        
            Install-WindowsFeature RSAT-ADDS
    
      - In un computer con Windows Server 2008 R2 SP1, eseguire il comando seguente.
        
            Add-WindowsFeature RSAT-ADDS

## Prerequisiti di Windows Server 2012 R2 e Windows Server 2012

I prerequisiti necessari per installare Exchange 2013 in un computer con Windows Server 2012 R2 o Windows Server 2012 dipendono da quali ruoli di Exchange si desidera installare. Leggere la sezione seguente corrispondente ai ruoli che si desidera installare.

## Ruoli server Accesso client o Cassette postali

Seguire le istruzioni riportate in questa sezione per installare i prerequisiti nei computer Windows Server 2012 R2 o Windows Server 2012 in cui si intende effettuare una delle seguenti operazioni:

  - Installare solo il ruolo del server Cassette postali in un computer.

  - Installare solo il ruolo del server Accesso client in un computer.

  - Installare sia il ruolo del server Cassette postali che Accesso clienti nello stesso computer.

Eseguire le operazioni seguenti per installare le funzionalità e i ruoli di Windows necessari:

1.  Aprire Windows PowerShell.

2.  Eseguire il comando seguente per installare i componenti di Windows necessari.
    
        Install-WindowsFeature AS-HTTP-Activation, Desktop-Experience, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS

Dopo aver installato i ruoli e le funzionalità del sistema operativo, installare il software seguente nell’ordine indicato:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 e versioni successive <STRONG>richiede</STRONG> .NET Framework 4.6.2. Aggiornare i server a .NET Framework 4.6.2 prima di installare Exchange 2013 CU16 o si riceverà un errore. Se .NET Framework 4.5.2 è installato sui server di Exchange, aggiornare i server a Exchange 2013 CU15 prima di installare .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (incluso con Windows Server 2012 R2)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Ruolo del server Trasporto Edge

Seguire le istruzioni riportate in questa sezione per installare i prerequisiti nei computer Windows Server 2012 R2 o Windows Server 2012 in cui si intende installare solo il ruolo server Trasporto Edge in un computer.

Eseguire le operazioni seguenti per installare le funzionalità e i ruoli di Windows necessari:

1.  Aprire Windows PowerShell.

2.  Eseguire il comando seguente per installare i componenti di Windows necessari.
    
        Install-WindowsFeature ADLDS

Installare la versione di Microsoft .NET Framework che corrisponde alla versione di Exchange 2013 che si sta installando:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 e versioni successive <STRONG>richiede</STRONG> .NET Framework 4.6.2. Aggiornare i server a .NET Framework 4.6.2 prima di installare Exchange 2013 CU16 o si riceverà un errore. Se .NET Framework 4.5.2 è installato sui server di Exchange, aggiornare i server a Exchange 2013 CU15 prima di installare .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234) (incluso con Windows Server 2012 R2)

## Prerequisiti di Windows Server 2008 R2 SP1

I prerequisiti necessari per installare Exchange 2013 in un computer con Windows Server 2008 R2 SP1 dipendono da quali ruoli di Exchange si desidera installare. Leggere la sezione seguente corrispondente ai ruoli che si desidera installare.

## Ruoli server Accesso client o Cassette postali

Seguire le istruzioni riportate in questa sezione per installare i prerequisiti nei computer Windows Server 2008 R2 SP1 in cui si intende effettuare una delle seguenti operazioni:

  - Installare solo il ruolo del server Cassette postali in un computer.

  - Installare solo il ruolo del server Accesso client in un computer.

  - Installare sia il ruolo del server Cassette postali che Accesso clienti nello stesso computer.

Eseguire le operazioni seguenti per installare le funzionalità e i ruoli di Windows necessari:

1.  Aprire Windows PowerShell.

2.  Eseguire il comando seguente per caricare il modulo Server Manager.
    
        Import-Module ServerManager

3.  Eseguire il comando seguente per installare i componenti di Windows necessari.
    
        Add-WindowsFeature Desktop-Experience, NET-Framework, NET-HTTP-Activation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Web-Server, WAS-Process-Model, Web-Asp-Net, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, RSAT-ADDS

Dopo aver installato i ruoli e le funzionalità del sistema operativo, installare il software seguente nell’ordine indicato:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 e versioni successive <STRONG>richiede</STRONG> .NET Framework 4.6.2. Aggiornare i server a .NET Framework 4.6.2 prima di installare Exchange 2013 CU16 o si riceverà un errore. Se .NET Framework 4.5.2 è installato sui server di Exchange, aggiornare i server a Exchange 2013 CU15 prima di installare .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://go.microsoft.com/fwlink/p/?linkid=258269)

4.  [Articolo della Microsoft Knowledge Base KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

5.  [Articolo della Knowledge Base KB2619234 (È disponibile il cookie/GUID per l’associazione utilizzato da RPC su HTTP che deve essere utilizzato anche al livello RPC in Windows 7 e in Windows Server 2008 R2)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2619234)

6.  [Articolo della Knowledge Base KB2533623 (Possibile esecuzione di codice remoto durante un caricamento della libreria non protetto)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2533623)
    

    > [!NOTE]
    > Questo hotfix può essere stato già installato se Windows Update è stato configurato per installare gli aggiornamenti di sicurezza nel computer.



## Ruolo del server Trasporto Edge

Seguire le istruzioni riportate in questa sezione per installare i prerequisiti nei computer Windows Server 2008 R2 SP1 in cui si intende installare solo il ruolo server Trasporto Edge in un computer.

Eseguire le operazioni seguenti per installare le funzionalità e i ruoli di Windows necessari:

1.  Aprire Windows PowerShell.

2.  Eseguire il comando seguente per caricare il modulo Server Manager.
    
        Import-Module ServerManager

3.  Eseguire il comando seguente per installare i componenti di Windows necessari.
    
        Add-WindowsFeature NET-Framework, ADLDS

Dopo aver installato i ruoli e le funzionalità del sistema operativo, installare il software seguente nell’ordine indicato:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16 e versioni successive <STRONG>richiede</STRONG> .NET Framework 4.6.2. Aggiornare i server a .NET Framework 4.6.2 prima di installare Exchange 2013 CU16 o si riceverà un errore. Se .NET Framework 4.5.2 è installato sui server di Exchange, aggiornare i server a Exchange 2013 CU15 prima di installare .NET Framework 4.6.2.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64-bit](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Prerequisiti di Windows 7 (solo strumenti di amministrazione)

Seguire le istruzioni riportate in questa sezione per installare i prerequisiti nei computer Windows 7 a 64 bit aggiunti al dominio in cui si desidera installare gli strumenti di gestione Exchange.

1.  Aprire il **Pannello di controllo** e selezionare **Programmi**.

2.  Fare clic su **Attivazione o disattivazione delle funzionalità Windows**.

3.  Passare a **Internet Information Services** \> **Strumenti di gestione Web** \> **Compatibilità di gestione con IIS 6**.

4.  Selezionare la casella di controllo per **Console di gestione IIS 6**, quindi fare clic su **OK**.

Dopo aver installato le funzionalità del sistema operativo, installare il software seguente nell’ordine indicato:

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Articolo della Knowledge Base KB974405 (Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

## Prerequisiti di Windows 8 e Windows 8.1 (solo strumenti di amministrazione)

[.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

