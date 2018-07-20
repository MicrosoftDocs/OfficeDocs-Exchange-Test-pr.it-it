---
title: 'Come consentire agli utenti finali di visualizzare le impostazioni dei server POP3, IMAP4 e SMTP in Outlook Web App: Exchange 2013 Help'
TOCTitle: Come consentire agli utenti finali di visualizzare le impostazioni dei server POP3, IMAP4 e SMTP in Outlook Web App
ms:assetid: bd22bf7e-3bf7-45e6-8790-919b780166f6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg298947(v=EXCHG.150)
ms:contentKeyID: 50555673
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Come consentire agli utenti finali di visualizzare le impostazioni dei server POP3, IMAP4 e SMTP in Outlook Web App

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-28_

Se alcuni utenti utilizzano POP3 o IMAP4 per collegarsi alle proprie cassette postali di Microsoft Exchange Server 2013, dovrebbero conoscere le impostazioni corrette del server per il collegamento. Dopo l'installazione predefinita di Exchange 2013, gli utenti non possono controllare le impostazioni del server POP3 o IMAP4 in arrivo oppure le impostazioni del server SMTP in uscita. È tuttavia possibile configurare Exchange in modo che gli utenti possano controllare le proprie impostazioni utilizzando MicrosoftOutlook Web App.

Dopo l'esecuzione di queste procedure gli utenti finali possono controllare le proprie impostazioni del server in Outlook Web App, come segue:

1.  In Outlook Web App, fare clic su **Impostazioni** \> **Opzioni**.

2.  In **Opzioni** fare clic su **Account** \> **Account personale** \> **Impostazioni per l'accesso POP o IMAP**.

Per ulteriori informazioni su POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzare Shell per consentire agli utenti di POP3 e IMAP4 di visualizzare le impostazioni di POP3 e IMAP4 in arrivo in Outlook Web App

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni POP3" e "Impostazioni IMAP4" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

In questo esempio si consente agli utenti finali di visualizzare le impostazioni del server POP3 esterno.

    Set-PopSettings -ExternalConnectionSettings {Dublin01.Contoso.com:995:SSL}

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-PopSettings](https://technet.microsoft.com/it-it/library/aa997154\(v=exchg.150\)).

In questo esempio si consente agli utenti finali di visualizzare le impostazioni del server IMAP4 esterno.

    Set-ImapSettings -ExternalConnectionSettings {Dublin01.Contoso.com:993:SSL}

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ImapSettings](https://technet.microsoft.com/it-it/library/aa998252\(v=exchg.150\)).

Per applicare queste modifiche, è necessario riavviare IIS. Non è necessario riavviare i servizi POP3. Per riavviare IIS, da un prompt dei comandi, digitare quanto segue:

    iisreset

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver configurato Exchange per consentire agli utenti di visualizzare le impostazioni del server POP3:

1.  Eseguire il seguente comando in Shell.
    
        Get-PopSettings | format-list

2.  Verificare che sia impostata la proprietà *ExternalConnectionSettings*.

Per verificare di aver configurato Exchange per consentire agli utenti di visualizzare le impostazioni del server IMAP4:

1.  Eseguire il seguente comando in Shell.
    
        Get-ImapSettings | format-list

2.  Verificare che sia impostata la proprietà *ExternalConnectionSettings*.

## Utilizzare Shell per consentire agli utenti di POP3 e IMAP4 di visualizzare le impostazioni di SMTP in uscita in Outlook Web App

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di ricezione" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

Con questo esempio viene consentito agli utenti finali di visualizzare le impostazioni del server SMTP interno ed esterno utilizzando Outlook Web App.

    Get-ReceiveConnector "*Client Frontend*" | Set-ReceiveConnector -Fqdn Server.Contoso.com -AdvertiseClientSettings $true 

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125140\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver configurato Exchange per consentire agli utenti di visualizzare le impostazioni del server SMTP:

1.  Eseguire il seguente comando in Shell.
    
        Get-ReceiveConnector | format-list

2.  Se la proprietà *AdvertiseClientSettings* è impostata su `true`, gli utenti possono visualizzare le impostazioni del server SMTP in Outlook Web App. Se *AdvertiseClientSettings* è impostata su `false`, gli utenti non possono visualizzare le impostazioni del server SMTP in Outlook Web App.

## Ulteriori informazioni

Dopo aver reso possibile agli utenti finali la visualizzazione delle proprie impostazioni POP3, IMAP4, e SMTP, è anche possibile:

[Abilitare o disabilitare l'accesso POP3 per un utente](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[Abilitazione o disabilitazione dell'accesso IMAP4 per un utente](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

