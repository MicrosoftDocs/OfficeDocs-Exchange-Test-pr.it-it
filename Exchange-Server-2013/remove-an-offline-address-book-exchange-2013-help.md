---
title: 'Rimuovere una Rubrica fuori rete: Exchange 2013 Help'
TOCTitle: Rimuovere una Rubrica fuori rete
ms:assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124744(v=EXCHG.150)
ms:contentKeyID: 50481785
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere una Rubrica fuori rete

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-12-16_

In questo argomento viene descritto come rimuovere una rubrica offline.

Per altre attività di gestione relative alle rubriche offline, vedere [Procedure della Rubrica fuori rete](offline-address-book-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Rubriche offline" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Dopo aver eliminato una Rubrica offline collegata a un utente o a un database delle cassette postali, il destinatario dovrà scaricare la Rubrica offline predefinita fino a quando a tale utente non verrà assegnata una nuova Rubrica offline. Se si elimina la Rubrica offline, è necessario assegnare una Rubrica offline diversa come predefinita. Per le istruzioni su come modificare la Rubrica offline predefinita, vedere [Modificare la Rubrica offline predefinita](change-the-default-offline-address-book-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Rimozione di una rubrica offline tramite Shell

Con questo esempio viene rimossa una Rubrica offline denominata My OAB.

    Remove-OfflineAddressBook -Identity "My OAB"

Digitare **Y** per confermare l'eliminazione della Rubrica offline, quindi premere INVIO.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Remove-OfflineAddressBook](https://technet.microsoft.com/it-it/library/bb123594\(v=exchg.150\)).

