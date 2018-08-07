---
title: 'Abilita/disabilita rete MAPI per cassetta postale: Exchange 2013 Help'
TOCTitle: Abilitazione o disabilitazione della rete MAPI per una cassetta postale
ms:assetid: c2c6718c-a2c0-4ed2-b4ed-364c3cb1f592
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124497(v=EXCHG.150)
ms:contentKeyID: 50555678
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Abilitazione o disabilitazione della rete MAPI per una cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-12-31_

È possibile utilizzare Interfaccia di amministrazione di Exchange o Exchange Management Shell per abilitare o disabilitare MAPI per la cassetta postale utente. Quando MAPI è abilitato, la cassetta postale utente può essere accessibile da Outlook o altri client di posta elettronica MAPI. Quando MAPI è disabilitato, non può essere accessibile da Outlook o da altri client MAPI. La cassetta postale continuerà tuttavia a ricevere messaggi di posta elettronica e l'utente vi potrà accedere per inviare e ricevere messaggi utilizzando Outlook Web App, un client di posta elettronica POP o IMAP, presupponendo che la cassetta postale sia abilitata a supportare l'accesso da tali client.


> [!NOTE]
> Il supporto per Outlook Web App e MAPI, POP3 e client di posta elettronica IMAP4 è abilitato per impostazione predefinita al momento della creazione di un utente.



Per ulteriori attività di gestione correlate alla gestione dell'accesso client di posta elettronica a una cassetta postale, vedere i seguenti argomenti:

  - [Attivare o disattivare Outlook Web App per una cassetta postale](enable-or-disable-outlook-web-app-for-a-mailbox-exchange-2013-help.md)

  - [Abilitazione o disabilitazione dell'accesso IMAP4 per un utente](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Abilitare o disabilitare l'accesso POP3 per un utente](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni utente di Accesso client" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Abilitazione o disabilitazione di MAPI tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale per cui si desidera abilitare o disabilitare MAPI, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

4.  In **Connettività posta elettronica** effettuare una delle seguenti operazioni.
    
      - Per disabilitare MAPI, sotto **MAPI: Abilitato**, fare clic su **Disabilita**.
        
        Viene visualizzato un messaggio di avviso che richiede all'utente di confermare la disabilitazione di MAPI. Fare clic su **Sì**.
    
      - Per abilitare MAPI, sotto **MAPI: Disabilitato**, fare clic su **Abilita**.

5.  Fare clic su **Salva** per salvare la modifica.

## Per utilizzare Exchange Management Shell per abilitare o disabilitare MAPI

Con questo esempio viene disabilitato MAPI per la cassetta postale di Ken Sanchez.

    Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $false

Con questo esempio viene abilitato MAPI per la cassetta postale di Esther Valle.

    Set-CASMailbox -Identity "Esther Valle" -MAPIEnabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta abilitazione o disabilitazione di MAPI per la cassetta postale utente, effettuare una delle seguenti operazioni:

  - In EAC accedere a **Destinatari** \> **Cassette postali**, fare clic sulla cassetta postale, quindi su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

  - Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

  - Sotto **Connettività posta elettronica**, verificare se MAPI è abilitato o disabilitato.

Oppure

  - Eseguire il comando riportato di seguito in Exchange Management Shell.
    
        Get-CASMailbox <identity>
    
    Se MAPI è abilitato, il valore della proprietà *MapiEnabled* è `True`. Se MAPI è disabilitato, il valore è `False`.

