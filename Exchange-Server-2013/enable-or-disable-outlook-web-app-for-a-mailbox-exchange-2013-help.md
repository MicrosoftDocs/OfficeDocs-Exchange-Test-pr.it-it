---
title: 'Att./dis. Outlook Web App per cassetta postale: Exchange 2013 Help'
TOCTitle: Attivare o disattivare Outlook Web App per una cassetta postale
ms:assetid: abc19646-6211-4f18-a060-e347452dcc53
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124124(v=EXCHG.150)
ms:contentKeyID: 50555659
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Attivare o disattivare Outlook Web App per una cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-14_

È possibile utilizzare EAC o Shell per abilitare o disabilitare Outlook Web App per la cassetta postale utente. Quando Outlook Web App è abilitato, l'utente può utilizzare Outlook Web App per l'invio e la ricezione della posta elettronica. Quando Outlook Web App è disabilitato, la cassetta postale continuerà a ricevere messaggi di posta elettronica e l'utente vi potrà accedere per inviare e ricevere messaggi utilizzando un client MAPI, quale Microsoft Outlook o un client di posta elettronica POP o IMAP, presupponendo che la cassetta postale sia abilitata a supportare l'accesso da tali client.


> [!NOTE]
> Il supporto per Outlook Web App e MAPI, POP3 e client di posta elettronica IMAP4 è abilitato per impostazione predefinita al momento della creazione di un utente.



Per ulteriori attività di gestione correlate alla gestione dell'accesso client di posta elettronica a una cassetta postale, vedere i seguenti argomenti:

  - [Abilitazione o disabilitazione della rete MAPI per una cassetta postale](enable-or-disable-mapi-for-a-mailbox-exchange-online-help.md)

  - [Abilitazione o disabilitazione dell'accesso IMAP4 per un utente](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Abilitare o disabilitare l'accesso POP3 per un utente](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni utente di Accesso client" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Abilitazione o disabilitazione di Outlook Web App tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale che si desidera abilitare o disabilitare a Outlook Web App, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

4.  In **Connettività posta elettronica** effettuare una delle seguenti operazioni:
    
      - Per disabilitare Outlook Web App, sotto **Outlook Web App: Abilitato**, fare clic su **Disabilita**.
        
        Viene visualizzato un messaggio di avviso che richiede all'utente di confermare la disabilitazione di Outlook Web App. Fare clic su **Sì**.
    
      - Per abilitare Outlook Web App, sotto **Outlook Web App: Disabilitato**, fare clic su **Abilita**.

5.  Fare clic su **Salva** per salvare la modifica.


> [!NOTE]
> È possibile abilitare e disabilitare Outlook Web App per più cassette postali utente tramite la funzionalità di modifica in blocco di EAC. Per ulteriori informazioni su come eseguire questa operazione, vedere la sezione "Modifica in blocco delle cassette postali utente" in <A href="manage-user-mailboxes-exchange-2013-help.md">Gestire le cassette postali degli utenti</A>.



## Abilitazione o disabilitazione di Outlook Web App tramite Shell

Con questo esempio viene disabilitato Outlook Web App per la cassetta postale di Yan Li.

    Set-CASMailbox -Identity "Yan Li" -OWAEnabled $false

Con questo esempio viene abilitato Outlook Web App per la cassetta postale di Elly Nkya.

    Set-CASMailbox -Identity Ellyn@contoso.com -OWAEnabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta abilitazione o disabilitazione di Outlook Web App per la cassetta postale utente, effettuare una delle seguenti operazioni:

  - In EAC accedere a **Destinatari** \> **Cassette postali**, fare clic sulla cassetta postale, quindi su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

  - Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

  - Sotto **Connettività posta elettronica**, verificare se Outlook Web App è abilitato o disabilitato.

Oppure

  - Eseguire il seguente comando in Shell.
    
        Get-CASMailbox <identity>
    
    Se Outlook Web App è abilitato, il valore della proprietà *OWAEnabled* è `True`. Se Outlook Web App è disabilitato, il valore è `False`.

