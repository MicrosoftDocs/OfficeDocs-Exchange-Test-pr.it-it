---
title: 'Configurare le opzioni di calendario per IMAP4: Exchange 2013 Help'
TOCTitle: Configurare le opzioni di calendario per IMAP4
ms:assetid: 6679c8b2-3f0f-449a-a17c-a7b30001538c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998606(v=EXCHG.150)
ms:contentKeyID: 50555608
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le opzioni di calendario per IMAP4

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-27_

È possibile utilizzare Shell per configurare le impostazioni di accesso al calendario per gli utenti che si connettono alla loro cassetta postale tramite una connessione IMAP4. Dalle impostazioni specificate dipende il modo in cui gli utenti di IMAP4 possono accedere al loro calendario e scambiare informazioni su di esso con altri utenti (ad esempio, inviando o rispondendo a una convocazione di riunione).

Per ulteriori informazioni su IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni IMAP4" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di Shell per impostare le opzioni di calendario per IMAP4

In questo esempio, viene abilitato l'utilizzo da parte degli utenti di IMAP4 dello standard iCalendar che permette di scambiare le informazioni sul calendario.

```powershell
Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

In questo esempio, agli utenti di IMAP4 viene consentito l'accesso alle informazioni sul calendario da un server interno.
```powershell
    Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 
```

In questo esempio viene consentito agli utenti di IMAP4 l'accesso alle informazioni di calendario da Internet su un server interno.

```powershell
Set-ImapSettings -CalendarItemRetrievalOption InternetUrl
```

In questo esempio, agli utenti di IMAP4 viene consentito l'accesso alle informazioni sul calendario tramite un URL di Outlook Web App diretto. Se si utilizza `Custom`, è necessario specificare un URL di Outlook Web App tramite il parametro *OWAServerUrl*.

```powershell
Set-Imap4Settings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

Dopo avere specificato le opzioni di calendario per IMAP4, è necessario riavviare i servizi IMAP4. Per informazioni su come riavviare i servizi IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ImapSettings](https://technet.microsoft.com/it-it/library/aa998252\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver impostato correttamente le opzioni del calendario, fare quanto segue:

Eseguire il seguente comando in Shell.

```powershell
Get-ImapSettings | format-list
```

Verificare che le impostazioni del calendario siano corrette.

## Ulteriori informazioni

Una volta impostate le opzioni di calendario per IMAP4, è possibile anche effettuare le seguenti operazioni:

[Configurare opzioni di formato per il recupero messaggi POP3 e IMAP4](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[Impostare limiti di timeout di connessione per IMAP4](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

