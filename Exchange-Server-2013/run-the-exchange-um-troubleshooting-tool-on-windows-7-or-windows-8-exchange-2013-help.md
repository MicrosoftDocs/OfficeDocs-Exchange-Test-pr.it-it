---
title: 'Esecuzione dello strumento di risoluzione dei problemi di messaggistica unificata in Windows 7 o Windows 8: Exchange 2013 Help'
TOCTitle: Esecuzione dello strumento di risoluzione dei problemi di messaggistica unificata in Windows 7 o Windows 8
ms:assetid: 98d6869d-ee4a-4088-849d-ef75b0f5d932
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff851872(v=EXCHG.150)
ms:contentKeyID: 56269836
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esecuzione dello strumento di risoluzione dei problemi di messaggistica unificata in Windows 7 o Windows 8

 

_**Si applica a:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Lo strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010 è un cmdlet di Exchange Management Shell denominato **Test-ExchangeUMCallFlow**. Questo cmdlet può essere utilizzato per diagnosticare gli errori di configurazione specifici degli scenari di ricezione chiamate e per verificare se il sistema di caselle vocali funziona correttamente sia nelle distribuzioni locali che in quelle cross-premise del servizio di messaggistica unificata di Microsoft Exchange Server 2010 Service Pack 1 (SP1) o versione successiva. È possibile utilizzare questo cmdlet nelle distribuzioni con Microsoft Office o Microsoft Lync Server 2010 o versioni successive oppure nelle distribuzioni del servizio di messaggistica unificata con gateway VO IP, PBX IP o session border controller (SBC).

## Informazioni preliminari

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Messaggistica UNIFICATA" o "servizi di messaggistica UNIFICATA? voce nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md) .

  - Verificare che il Exchange 2010 o l'organizzazione di Exchange 2013 soddisfi i requisiti seguenti:
    
      - È stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).
    
      - È stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).
    
      - È stato creato un gateway IP di messaggistica unificata. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).
    
      - Un server Messaggistica UNIFICATA di Exchange 2010 è stato aggiunto al dial plan di messaggistica UNIFICATA. Se si utilizza Exchange 2013 con Lync Server, aggiungere tutti accesso Client e server cassette postali per il dial plan URI SIP. Per ulteriori informazioni, vedere [Add un Server messaggistica UNIFICATA a un Dial Plan](https://go.microsoft.com/fwlink/p/?linkid=313051) o [Aggiungere server cassette postali e accesso Client a un dial plan URI SIP](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md).

  - Se è in esecuzione dello strumento Risoluzione dei problemi di messaggistica UNIFICATA su un server Messaggistica UNIFICATA locale con Exchange 2010 SP1 o versione successiva o in un server cassette postali di Exchange 2013 potrebbe non è necessario installare tutti i prerequisiti elencati di seguito. Può sono già stati installati con il ruolo del server Messaggistica UNIFICATA. Tuttavia, se si sta installando dello strumento Risoluzione dei problemi di messaggistica UNIFICATA in un computer a 64 bit diverso da un server che esegue il ruolo del server Messaggistica UNIFICATA, è necessario installare i componenti seguenti:
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1). Vedere [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    
      - Se lo strumento verrà eseguito su un computer con Vista o Windows Server 2008Windows, vedere [aggiornamento Microsoft .NET Framework 3.5 per Windows Server 2008 x64 e Windows Vista x64,](https://go.microsoft.com/fwlink/p/?linkid=178998).
    
      - Windows Gestione remota Windows (WinRM) 2.0 e Windows PowerShell V2 (Windows6.0-KB968930.msu). Vedere l'articolo 968930 della Microsoft Knowledge Base [Pacchetto Windows Management Framework Core (Windows PowerShell 2.0 e Gestione remota Windows 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930).
    
      - Microsoft Unified Communications Managed API 2.0 Core Runtime (Ucmaruntimewebdownloadx64). Vedere [Unified Communications Managed API 2.0, Core Runtime (64 bit)](https://go.microsoft.com/fwlink/p/?linkid=198175).

  - Scaricare e installare lo strumento di risoluzione dei problemi di messaggistica unificata.
    
      - Download [dello strumento di risoluzione dei problemi di messaggistica unificata](https://go.microsoft.com/fwlink/p/?linkid=182625) dall'area Download Microsoft.
    
      - Installare lo strumento. Per i dettagli, vedere [Installazione dello strumento di risoluzione dei problemi di messaggistica unificata di Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).
        

        > [!IMPORTANT]
        > Se si utilizzerà la risoluzione dei problemi di strumento di messaggistica UNIFICATA in modalità <CODE>SIPClient</CODE> , esistono diversi altri Office Communications Server 2007 R2 o Microsoft requisiti di Lync Server e i prerequisiti che devono essere soddisfatti. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=311961">Checklist: distribuzione di Office Communications Server 2007 R2 e la messaggistica unificata di Exchange 2010</A>.



  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Esecuzione dello lo strumento di risoluzione dei problemi di messaggistica unificata in Windows Vista, Windows 7 o Windows 8

1.  Fare clic su **Start** \> **Tutti i programmi** \> **Accessori** \> **Windows PowerShell**.

2.  Fare clic con il pulsante destro del mouse su **Windows PowerShell** e, nel menu visualizzato, selezionare **Esegui come amministratore**.

3.  Al prompt dei comandi di Windows PowerShell, accedere alla cartella di installazione dello strumento di risoluzione dei problemi di messaggistica unificata ed eseguire il comando riportato di seguito.
    
        C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -psconsolefile .\Microsoft.Exchange.UM.TroubleshootingToolsnapin.psc1 -noexit -command ". '.\Microsoft.Exchange.UM.TroubleshootingTool.ps1' "

4.  Se si sta eseguendo lo strumento di risoluzione dei problemi di messaggistica unificata in Windows Vista, Windows 7 o Windows 8, al prompt dei comandi di Windows PowerShell eseguire il comando riportato di seguito.
    
        Set-ExecutionPolicy RemoteSigned

5.  Aprire lo **strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010** dal menu **Start**.

6.  Nella finestra dello **strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010**, nel prompt, digitare il seguente comando e premere Invio.
    
        $cred=Get-Credential

7.  Nella finestra **Richiesta credenziali di Windows PowerShell** digitare dominio\\nome utente e password, quindi fare clic su **OK**.

8.  Nella finestra dello **strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010**, specificare i parametri del cmdlet necessari per verificare il flusso delle chiamate. Ad esempio:
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

