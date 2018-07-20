---
title: 'Ripristino di un server Exchange: Exchange 2013 Help'
TOCTitle: Ripristino di un server Exchange
ms:assetid: 46e9a1cf-b64c-43c3-a898-6171176da761
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876880(v=EXCHG.150)
ms:contentKeyID: 50480568
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ripristino di un server Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile ripristinare un server perso utilizzando l'opzione **Setup /m:RecoverServer** in Microsoft Exchange Server 2013. La maggior parte delle impostazioni per un computer che esegue Exchange 2013 viene archiviata in Active Directory. L'opzione */m:RecoverServer* ricrea un server Exchange con lo stesso nome utilizzando impostazioni e altre informazioni archiviate in Active Directory.

Il ripristino di un server perso Exchange spesso viene eseguito utilizzando un nuovo hardware. Tuttavia, è possibile utilizzare anche un server esistente.

In questo argomento viene descritto come ripristinare un server perso Exchange 2013 che non è un membro del gruppo di disponibilità del database (DAG). Per informazioni dettagliate relative al ripristino di un server membro di un gruppo di disponibilità del database, vedere [Ripristinare un server membro di database availability group](recover-a-database-availability-group-member-server-exchange-2013-help.md).


> [!NOTE]
> Se Exchange è installato in un percorso diverso da quello predefinito, è necessario utilizzare l'opzione <EM>/TargetDir</EM> per specificare il percorso dei file binari di Exchange. Se non si utilizza l'opzione <EM>/TargetDir</EM>, i file di Exchange verranno installati nel percorso predefinito (%programfiles%\Microsoft\Exchange Server\V15).<BR>Per determinare il percorso di installazione, procedere come segue: 
> <OL>
> <LI>
> <P>Aprire ADSIEDIT.MSC o LDP.EXE.</P>
> <LI>
> <P>Accedere al percorso seguente: <STRONG>CN=ExServerName,CN=Servers,CN=First Administrative Group,CN=Administrative Groups,CN=ExOrg Name,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=DomainName,CN=Com</STRONG></P>
> <LI>
> <P>Fare clic con il pulsante destro del mouse sull'oggetto server Exchange, quindi scegliere <STRONG>Proprietà</STRONG>.</P>
> <LI>
> <P>Individuare l'attributo <STRONG>msExchInstallPath</STRONG>. in cui è memorizzato il percorso di installazione corrente.</P></LI></OL>



Per informazioni sulle altre attività di gestione relative al backup e al recupero dei dati? vedere [Backup, ripristino e ripristino di emergenza](backup-restore-and-disaster-recovery-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 20 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni infrastruttura Exchange" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Sul server su cui viene eseguito il ripristino deve essere installato lo stesso sistema operativo del server perso. Ad esempio, non è possibile ripristinare un server su cui è installato Exchange 2013 e Windows Server 2008 R2 su un server su cui è installato Windows Server 2012 o viceversa. Ad esempio, non è possibile ripristinare un server su cui era installato Exchange 2013 Windows Server 2012 in un server su cui è installato Windows Server 2012 R2 o viceversa.

  - Sul server su cui si è verificato l'errore e sul server su cui si sta eseguendo il ripristino devono essere presenti le stesse lettere per le unità disco dei database montati.

  - Il server su cui si esegue il ripristino deve avere le stesse caratteristiche delle prestazioni e la stessa configurazione hardware del server perso.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Ripristino di un server Exchange perso

1.  Reimpostare l'account computer del server perso. Per ulteriori informazioni, vedere [reimpostare un Account Computer](https://go.microsoft.com/fwlink/p/?linkid=165388).

2.  Installare il sistema operativo corretto ed assegnare al nuovo server lo stesso nome del server perso. Il ripristino non viene eseguito se il server non ha lo stesso nome del server perso.

3.  Aggiungere il server allo stesso dominio del server perso.

4.  Installare i prerequisiti necessari e i componenti del sistema operativo. Per ulteriori informazioni, vedere [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md) e [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

5.  Accedere al server in fase di ripristino e aprire un prompt dei comandi.

6.  Passare ai file di installazione di Exchange 2013 e utilizzare il seguente comando.
    
        Setup /m:RecoverServer /IAcceptExchangeServerLicenseTerms

7.  Una volta completata l'installazione, ma prima di rimettere in funzione il server ripristinato, riconfigurare qualsiasi impostazione che era presente sul server in precedenza, quindi riavviare il server.

## Come verificare se l'operazione ha avuto esito positivo?

Il completamento dell'installazione è l'elemento principale che indica che il ripristino è riuscito. Come ulteriore verifica del corretto ripristino del server, fare quanto segue:

  - Aprire lo strumento Servizi Windows (services.msc) e verificare che i servizi di Microsoft Exchange siano stati installati e siano in esecuzione.

