---
title: "Abilitazione o disabilitazione dell'accesso IMAP4 per un utente: Exchange 2013 Help"
TOCTitle: Abilitazione o disabilitazione dell'accesso IMAP4 per un utente
ms:assetid: a685fae4-b6f1-42fe-8bdc-5f99f9617799
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb676481(v=EXCHG.150)
ms:contentKeyID: 50481361
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitazione o disabilitazione dell'accesso IMAP4 per un utente

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-01-18_

È possibile abilitare o disabilitare IMAP4 per un utente.


> [!NOTE]
> Dopo aver abilitato o disabilitato IMAP4 per un utente, è necessario riavviare il servizio IMAP4 di Microsoft Exchange e il servizio Back-end IMAP4 di Microsoft Exchange. Per ulteriori informazioni su come riavviare il servizio IMAP4, vedere <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Avviare e arrestare i servizi IMAP4</A>.



Per ulteriori informazioni relative alla gestione delle cassette postali utente, vedere [Gestire le cassette postali degli utenti](manage-user-mailboxes-exchange-2013-help.md).

Per ulteriori informazioni su POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per abilitare o disabilitare IMAP4 per un utente

1.  In EAC, selezionare **Destinatari** \> **Cassette postali**.

2.  Nel riquadro dei risultati, selezionare l'utente per il quale si desidera abilitare o disabilitare IMAP4 e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella finestra di dialogo **Cassetta postale utente**, nell'albero della console, fare clic su **Funzionalità delle cassette postali**.
    
    Nel riquadro dei risultati, in **Connessione posta elettronica**, effettuare una delle seguenti operazioni:
    
      - Per disabilitare IMAP4 per l'utente, in **IMAP4: Abilitato**, fare clic su **Disabilita**.
    
      - Per abilitare IMAP4 per l'utente, in **IMAP4: Disabilitato**, fare clic su **Abilita**.

4.  Fare clic su **Salva**.

## Abilitazione o disabilitazione di IMAP4 per la cassetta postale di un utente tramite Shell

Con questo esempio viene abilitato IMAP4 per l'utente John Smith.

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $true

Con questo esempio viene disabilitato IMAP4 per l'utente John Smith.

    Set-CASMailbox -Identity "John Smith" -IMAPEnabled $false

## Come verificare se l'operazione ha avuto esito positivo

1.  In EAC, selezionare **Destinatari** \> **Cassette postali**.

2.  Nel riquadro dei risultati, selezionare l'utente per il quale si desidera abilitare o disabilitare IMAP4 e quindi fare clic su **Modifica**.

3.  Nella finestra di dialogo **Cassetta postale utente**, nell'albero della console, fare clic su **Funzionalità delle cassette postali**.
    
    Nel riquadro dei risultati, esaminare le voci in **Connessione posta elettronica**.
    
      - Se IMAP4 è abilitato per l'utente, sarà indicato **IMAP4: Abilitato**.
    
      - Se IMAP4 non è abilitato per l'utente, sarà indicato **IMAP4: Disabilitato**.

4.  Fare clic su **Salva**.

