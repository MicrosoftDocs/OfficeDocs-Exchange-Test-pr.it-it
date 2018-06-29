---
title: 'Installazione dello strumento di risoluzione dei problemi di messaggistica unificata di Exchange: Exchange 2013 Help'
TOCTitle: Installazione dello strumento di risoluzione dei problemi di messaggistica unificata di Exchange
ms:assetid: 84223af0-a717-49ee-add6-86313bb30d17
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff844714(v=EXCHG.150)
ms:contentKeyID: 56269835
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installazione dello strumento di risoluzione dei problemi di messaggistica unificata di Exchange

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Lo strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010 è un cmdlet di Exchange Management Shell denominato **Test-ExchangeUMCallFlow**. Questo cmdlet può essere utilizzato per diagnosticare gli errori di configurazione specifici degli scenari di ricezione chiamate e per verificare se il sistema di caselle vocali funziona correttamente sia nelle distribuzioni locali che in quelle cross-premise del servizio di messaggistica unificata di Microsoft Exchange Server 2010 Service Pack 1 (SP1) o versione successiva. È possibile utilizzare questo cmdlet nelle distribuzioni con Microsoft Office o Microsoft Lync Server 2010 o versioni successive oppure nelle distribuzioni del servizio di messaggistica unificata con gateway VO IP, PBX IP o session border controller (SBC).

È possibile installare lo strumento di risoluzione dei problemi di messaggistica unificata su un server Messaggistica unificata locale, su un server Cassette postali di Exchange 2013 o su un altro computer a 64 bit.

## Informazioni preliminari

  - Tempo stimato per il completamento: 3 minuti

  - Prima di procedere con l'installazione dello strumento di risoluzione dei problemi di messaggistica unificata, è necessario installare i componenti indicati di seguito su un computer con Windows Vista, Windows 7, Windows 8 o l'edizione a 64 bit di Windows Server 2008 oppure Windows Server 2012 o versioni successive:
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1) vedere [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    
      - Se lo strumento verrà eseguito su un computer Windows Vista o Windows Server 2008, vedere [aggiornamento Microsoft .NET Framework 3.5 per Windows Server 2008 x64 e Windows Vista x64,](https://go.microsoft.com/fwlink/p/?linkid=178998).
    
      - Windows Gestione remota Windows (WinRM) 2.0 e Windows PowerShell V2 (Windows6.0-KB968930.msu). Vedere l'articolo 968930 della Microsoft Knowledge Base [Pacchetto Windows Management Framework Core (Windows PowerShell 2.0 e Gestione remota Windows 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930).
    
      - Microsoft Unified Communications Managed API 2.0 Core Runtime (Ucmaruntimewebdownloadx64). Vedere [Unified Communications Managed API 2.0, Core Runtime (64 bit)](https://go.microsoft.com/fwlink/p/?linkid=198175).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Installazione dello strumento di risoluzione dei problemi di messaggistica unificata

1.  Scaricare il Messaging Troubleshooting strumento unificato dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625)e quindi fare doppio clic sulla cartella di installazione Microsoftexchange2010umtroubleshootingtool.

2.  Nella pagina **Installazione guidata dello strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010** fare clic su **Avanti**.

3.  Nella pagina **Contratto di licenza** verificare le condizioni di licenza relative al software e, se si intende accettarle, fare clic su **Accetto i termini del contratto di licenza**. Quindi, fare clic su **Avanti**.

4.  Nella pagina **Seleziona cartella di installazione** verificare il percorso della cartella di installazione e fare clic su **Avanti**.

5.  Nella pagina **Conferma installazione** fare clic su **Avanti** per avviare l'installazione.

6.  Nella pagina **Installazione completata** fare clic su **Chiudi**.

