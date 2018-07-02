---
title: 'Test e risoluzione dei problemi con la risoluzione dei problemi di strumento di messaggistica UNIFICATA: Exchange 2013 Help'
TOCTitle: Test e risoluzione dei problemi con la risoluzione dei problemi di strumento di messaggistica UNIFICATA
ms:assetid: 1fab2e52-bd2d-4e46-b222-53fee9d34cba
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg621148(v=EXCHG.150)
ms:contentKeyID: 56269829
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Test e risoluzione dei problemi con la risoluzione dei problemi di strumento di messaggistica UNIFICATA

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Lo strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010 è un cmdlet di Exchange Management Shell denominato **Test-ExchangeUMCallFlow**. Questo cmdlet può essere utilizzato per diagnosticare gli errori di configurazione specifici degli scenari di ricezione chiamate e per verificare se il sistema di caselle vocali funziona correttamente sia nelle distribuzioni locali che in quelle cross-premise del servizio di messaggistica unificata di Microsoft Exchange Server 2010 Service Pack 1 (SP1) o versione successiva. È possibile utilizzare questo cmdlet nelle distribuzioni con Microsoft Office o Microsoft Lync Server 2010 o versioni successive oppure nelle distribuzioni del servizio di messaggistica unificata con gateway VO IP, PBX IP o session border controller (SBC).

## Panoramica

Questo cmdlet emula le chiamate e viene eseguita una serie di test diagnostici che consentono agli amministratori locale per identificare gli errori di configurazione in apparecchiature telefoniche, Exchange 2010 SP1 o versioni successive impostazioni messaggistica unificata e problemi di connettività tra locali e distribuzioni tra locali di Exchange 2010 SP1 o versioni successive la messaggistica unificata.

Quando viene eseguito, il cmdlet restituisce la causa e le possibili soluzioni dei problemi rilevati. Restituisce inoltre le metriche per la qualità audio per rilevare problemi audio relativi alla connettività di rete, ad esempio perdita media dei pacchetti e instabilità. Il cmdlet **Test-ExchangeUMCallFlow** supporta la verifica dei componenti di messaggistica unificata nelle chiamate `Secured`, `SIP Secured` e `Unsecured` e può essere eseguito in modalità `Gateway` o `SIPClient`.

Per impostazione predefinita, quando si esegue la risoluzione dei problemi di strumento di messaggistica UNIFICATA, utilizza le credenziali utilizzati quando si accede al computer. Le credenziali utilizzate sono quelli specificati per il chiamante. Deve impostare o specificare le credenziali da utilizzare quando è in esecuzione dello strumento Risoluzione dei problemi di messaggistica UNIFICATA in modalità `SIPClient` . Tuttavia, non è necessario impostare le credenziali durante l'esecuzione dello strumento Risoluzione dei problemi di messaggistica UNIFICATA in modalità `Gateway` . Se si utilizzerà la risoluzione dei problemi di strumento di messaggistica UNIFICATA in modalità `SIPClient` , è necessario soddisfare requisiti diversi altri Office Communications Server 2007 R2 o Lync Server e i prerequisiti. Per ulteriori informazioni, vedere [Checklist: distribuzione di Office Communications Server 2007 R2 e la messaggistica unificata di Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=311961) o [Elenco di controllo: Integrazione di messaggistica UNIFICATA di Exchange 2013 con Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).


> [!IMPORTANT]
> Il cmdlet <STRONG>Test-ExchangeUMCallFlow</STRONG> deve essere utilizzato per testare solo le funzionalità della segreteria telefonica di un Microsoft Exchange Server 2010 server Messaggistica unificata con Exchange&nbsp;2010 Service Pack 1 (SP1) o Microsoft Exchange 2013.



Il cmdlet **Test-ExchangeUMCallFlow** può essere installato in un server Messaggistica unificata locale di Exchange 2010, in un server Cassette postali di Exchange 2013 o in un altro computer a 64 bit che esegue:

  - Il sistema operativo Windows 7 o Windows 8

  - Il sistema operativo Windows Server 2008 o Windows Server 2008 R2

  - Il sistema operativo Windows Server 2012 o Windows Server 2012 R2

Prima dell'installazione del cmdlet **Test-ExchangeUMCallFlow**, è necessario installare i seguenti componenti in un computer a 64 bit che esegue Windows 7, Windows 8, Windows Server 2008 o Windows Server 2012:

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1). Per scaricare il service pack, vedere [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).

  - Microsoft .NET Framework 3.5 aggiornamento per Windows Vista x64 e Windows Server 2008 x64 Aggiorna se lo strumento verrà eseguito su un computer Windows Vista o Windows Server 2008. Per scaricare l'aggiornamento, vedere [aggiornamento Microsoft .NET Framework 3.5 per Windows Server 2008 x64 e Windows Vista x64,](https://go.microsoft.com/fwlink/p/?linkid=178998).

  - Windows Remote Management (WinRM) 2.0 e Windows PowerShell V2 (Windows6.0-KB968930.msu). Per ulteriori informazioni, vedere l'articolo 968930 della Microsoft Knowledge Base, [Pacchetto di Windows Management Framework Core (Windows PowerShell 2.0 e Gestione remota Windows 2.0)](http://go.microsoft.com/fwlink/?linkid=3052%26kbid=968930).

  - Microsoft Unified Communications Managed AP1 2.0, Core Runtime (64 bit). Per scaricare il file di programma Ucmaruntimewebdownloadx64, vedere [Unified Communications Managed API 2.0, Core Runtime (64 bit)](https://go.microsoft.com/fwlink/p/?linkid=198175).

Il cmdlet **Test-ExchangeUMCallFlow** non è incluso nel Exchange 2010 DVD SP1, il download Exchange 2010 solo SP1 o supporto di installazione di Exchange 2013. Tuttavia, è possibile scaricare il cmdlet dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Test-ExchangeUMCallFlow](https://technet.microsoft.com/it-it/library/ff630913\(v=exchg.150\)).

