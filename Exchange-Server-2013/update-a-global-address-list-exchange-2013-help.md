---
title: 'Aggiornamento di un elenco indirizzi globale: Exchange 2013 Help'
TOCTitle: Aggiornamento di un elenco indirizzi globale
ms:assetid: 236e8530-62dd-4c43-8a5d-8465623252e6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb266966(v=EXCHG.150)
ms:contentKeyID: 50480160
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Aggiornamento di un elenco indirizzi globale

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-12-16_

È possibile utilizzare Shell per aggiornare un elenco di indirizzi globale. Un elenco di indirizzi globale è una directory che contiene voci per ogni gruppo, utente e contatto che fa parte dell'implementazione di Microsoft Exchange nell'organizzazione.

Per altre attività di gestione relative agli elenchi di indirizzi, vedere [Procedure dell'elenco indirizzi](address-list-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Elenchi indirizzi" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Aggiornamento di un elenco di indirizzi globale tramite Shell

In questo esempio, viene aggiornato un elenco di indirizzi globale per la società Fourth Coffee.


> [!NOTE]
> Eseguendo questo comando, ci si limita ad avviare il processo di aggiornamento. L'aggiornamento dell'elenco indirizzi globale può richiedere diverse ore.



    Update-GlobalAddressList -Identity "Fourth Coffee"

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Update-GlobalAddressList](https://technet.microsoft.com/it-it/library/aa998806\(v=exchg.150\)).

