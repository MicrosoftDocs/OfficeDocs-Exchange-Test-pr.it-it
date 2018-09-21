---
title: 'Imposta cred. mess. unificata strum. risol. prob. Exchange: Exchange 2013 Help'
TOCTitle: Impostare le credenziali da utilizzare con la messaggistica UNIFICATA di risoluzione dei problemi di strumento di Exchange
ms:assetid: 542b7718-9345-40cc-bcb2-e307e70a1fa2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff630916(v=EXCHG.150)
ms:contentKeyID: 56269833
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare le credenziali da utilizzare con la messaggistica UNIFICATA di risoluzione dei problemi di strumento di Exchange

 

_**Si applica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Lo strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010 è un cmdlet di Exchange Management Shell denominato **Test-ExchangeUMCallFlow**. Questo cmdlet può essere utilizzato per diagnosticare gli errori di configurazione specifici degli scenari di ricezione chiamate e per verificare se il sistema di caselle vocali funziona correttamente sia nelle distribuzioni locali che in quelle cross-premise del servizio di messaggistica unificata di Microsoft Exchange Server 2010 Service Pack 1 (SP1) o versione successiva. È possibile utilizzare questo cmdlet nelle distribuzioni con Microsoft Office o Microsoft Lync Server 2010 o versioni successive oppure nelle distribuzioni del servizio di messaggistica unificata con gateway VO IP, PBX IP o session border controller (SBC).

Per impostazione predefinita, quando si utilizza lo strumento di risoluzione dei problemi di messaggistica unificata, vengono utilizzate le credenziali di accesso al computer. Le credenziali utilizzate sono quelle specificate per la parte chiamante. È necessario impostare o specificare le credenziali da utilizzare quando si esegue lo strumento di risoluzione dei problemi di messaggistica unificata in modalità `SIPClient`. Tuttavia, non è necessario impostare le credenziali quando si esegue lo strumento di risoluzione dei problemi di messaggistica unificata in modalità `Gateway`.

## Informazioni preliminari

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Messaggistica UNIFICATA" o "servizi di messaggistica UNIFICATA? voce nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md) .

  - Verificare che il Exchange 2010 o l'organizzazione di Exchange 2013 soddisfi i requisiti seguenti:
    
      - È stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).
    
      - È stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy).
    
      - È stato creato un gateway IP di messaggistica unificata. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway).
    
      - Un server Messaggistica UNIFICATA di Exchange 2010 è stato aggiunto al dial plan di messaggistica UNIFICATA. Se si utilizza Exchange 2013 con Lync Server, aggiungere tutti i server cassette postali e accesso Client per il dial plan URI SIP. Per ulteriori informazioni, vedere [Add un Server messaggistica UNIFICATA a un Dial Plan](https://go.microsoft.com/fwlink/p/?linkid=313051) o [Aggiungere server cassette postali e accesso Client a un dial plan URI SIP](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md).

  - Installare lo strumento di risoluzione dei problemi di messaggistica unificata. Per la procedura dettagliata, vedere [Installazione dello strumento di risoluzione dei problemi di messaggistica unificata di Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Se si utilizzerà la risoluzione dei problemi di strumento di messaggistica UNIFICATA in modalità <CODE>SIPClient</CODE> , esistono requisiti diversi altri Office Communications Server 2007 R2 o Microsoft Lync Server e i prerequisiti. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=311961">Checklist: distribuzione di Office Communications Server 2007 R2 e la messaggistica unificata di Exchange 2010</A> o <A href="checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md">Elenco di controllo: Integrazione di messaggistica UNIFICATA di Exchange 2013 con Lync Server</A>.



  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Impostazione delle credenziali da utilizzare con lo strumento di risoluzione dei problemi di messaggistica unificata

1.  Aprire lo **strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010** dal menu **Start**.

2.  Nella finestra dello **strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010**, nel prompt, digitare il seguente comando e premere Invio.
    
    ```powershell
$cred=Get-Credential
```

3.  Nella finestra **Richiesta credenziali di Windows PowerShell** digitare dominio\\nome utente e password, quindi fare clic su **OK**.

4.  Nella finestra dello **strumento di risoluzione dei problemi di messaggistica unificata di Microsoft Exchange 2010**, specificare i parametri del cmdlet necessari per verificare il flusso delle chiamate. Ad esempio:
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

