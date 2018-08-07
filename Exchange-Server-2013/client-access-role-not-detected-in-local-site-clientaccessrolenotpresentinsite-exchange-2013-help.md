---
title: 'Acc. client non ril. site_ClientAccessRoleNotPresentInSite: Exchange 2013 Help'
TOCTitle: Ruolo accesso client non rilevato in site_ClientAccessRoleNotPresentInSite locale
ms:assetid: b5bfc6af-9c55-46c0-a293-6078b64e87dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.clientaccessrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50481477
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ruolo accesso client non rilevato in site\_ClientAccessRoleNotPresentInSite locale

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Il programma di installazione di Microsoft® Exchange Server 2007 visualizzato questo avviso perché Impossibile rilevare un ruolo Accesso Client esistente nel sito del servizio di directory Active Directory® locale.

Si è scelto di installare il Server cassette postali ruolo prima di un'istanza del ruolo Accesso Client sia installato nel sito di Active Directory.

Il ruolo del server Accesso Client accetta le connessioni al server Exchange 2007 da svariati client. Software client, ad esempio Microsoft Outlook Express ed Eudora utilizzare connessioni POP3 o IMAP4 per comunicare con Exchange server. Client di hardware, ad esempio i dispositivi mobili, utilizzare ActiveSync, POP3 o IMAP4 per comunicare con Exchange server.

Se gli utenti accedono posta in arrivo utilizzando qualsiasi client diversi da Microsoft Office Outlook®, è necessario installare il ruolo del server Accesso Client nell'organizzazione di Exchange.

Gli utenti saranno in grado di eseguire l'accesso alle cassette postali con Outlook, ma non sarà in grado di utilizzare dispositivi mobili o Outlook Web Access con la stessa cassetta postale fino a quando non è presente nel sito Active Directory locale il ruolo Accesso Client.

