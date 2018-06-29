---
title: 'Rimuovere un elenco indirizzi globale: Exchange 2013 Help'
TOCTitle: Rimuovere un elenco indirizzi globale
ms:assetid: 65d75b69-641b-4a37-a63c-47cf018f5f22
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232077(v=EXCHG.150)
ms:contentKeyID: 50480781
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un elenco indirizzi globale

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-12-16_

L'elenco indirizzi globale (GAL, Global Address List) è una directory contenente voci per ogni gruppo, utente e contatto all'interno di un'organizzazione di Exchange.

Per altre attività di gestione relative agli elenchi di indirizzi, vedere [Procedure dell'elenco indirizzi](address-list-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Elenchi indirizzi" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Non è possibile rimuovere l'elenco indirizzi globale predefinito.

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Eliminazione di un elenco indirizzi globale tramite Shell

In questo esempio, l'elenco indirizzi globale per la società Fourth Coffee viene rimosso dal controller di dominio ad-server.fourthcoffee.com.

    Remove-GlobalAddressList -Identity "Fourth Coffee" -DomainController ad-server.fourthcoffee.com

Digitare **S** per confermare la rimozione dell'elenco indirizzi globale, quindi premere INVIO.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-GlobalAddressList](https://technet.microsoft.com/it-it/library/bb124368\(v=exchg.150\)).

