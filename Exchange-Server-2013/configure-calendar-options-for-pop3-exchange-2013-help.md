---
title: 'Configurare le opzioni di calendario per POP3: Exchange 2013 Help'
TOCTitle: Configurare le opzioni di calendario per POP3
ms:assetid: ac3d60a0-8697-4c06-9e93-f8d2c4b157b6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124133(v=EXCHG.150)
ms:contentKeyID: 50555656
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le opzioni di calendario per POP3

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-27_

È possibile utilizzare Shell per configurare le impostazioni di accesso di calendario per gli utenti che connettono le proprie cassette postali tramite connessioni POP3. Le impostazioni specificate determinano la modalità di accesso degli utenti di POP3 al calendario e di scambio delle informazioni di calendario (ad esempio, inviare o rispondere a una richiesta di riunione) con altri utenti.

Per ulteriori informazioni correlate a POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni POP3" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Impostazione delle opzioni di calendario per POP3 tramite Shell

Con questo esempio vengono abilitati gli utenti di POP3 all'utilizzo di iCalendar standard, uno standard per lo scambio delle informazioni di calendario.

```powershell
Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

Con questo esempio agli utenti POP3 viene consentito l'accesso alle informazioni di calendario interne da un server interno.
```powershell
    Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 
```
Con questo esempio agli utenti POP3 viene consentito l'accesso alle informazioni di calendario da Internet o da un server esterno.

```powershell
Set-PopSettings -CalendarItemRetrievalOption InternetUrl
```

Con questo esempio agli utenti POP3 viene consentito l'accesso alle informazioni di calendario tramite l'URL Outlook Web App diretto. Se si utilizza `Custom`, specificare l'URL di Outlook Web App utilizzando il parametro *OWAServerUrl*.

```powershell
Set-PopSettings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

Una volta specificate le opzioni del calendario per POP3, è necessario riavviare i servizi POP3. Per informazioni su come riavviare i servizi POP3, vedere [Avviare e arrestare i servizi POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-PopSettings](https://technet.microsoft.com/it-it/library/aa997154\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver impostato correttamente le opzioni di calendario, effettuare le operazioni seguenti:

Eseguire il seguente comando in Shell.

```powershell
Get-PopSettings | format-list
```

Verificare che le impostazioni di calendario siano corrette.

## Ulteriori informazioni

Dopo aver impostato le opzioni di calendario per POP3, è possibile anche:

[Configurare opzioni di formato per il recupero messaggi POP3 e IMAP4](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[Impostare limiti di timeout di connessione per POP3](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

