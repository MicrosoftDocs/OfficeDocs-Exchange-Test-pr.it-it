---
title: 'Creare un elenco di indirizzi utilizzando filtri destinatario: Exchange 2013 Help'
TOCTitle: Creare un elenco di indirizzi utilizzando filtri destinatario
ms:assetid: 8eabea64-97c6-40af-b61c-9b6a125cbdf1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123718(v=EXCHG.150)
ms:contentKeyID: 50481158
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un elenco di indirizzi utilizzando filtri destinatario

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-12-16_

In questo argomento è spiegato come creare un elenco indirizzi con i filtri destinatari. Per ulteriori informazioni sugli elenchi di indirizzi, vedere [Elenchi indirizzi](address-lists-exchange-2013-help.md).

Per altre attività di gestione relative agli elenchi di indirizzi, vedere [Procedure dell'elenco indirizzi](address-list-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Elenchi indirizzi" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Per utilizzare il parametro *RecipientFilter* per creare un filtro personalizzato, è necessario specificare una stringa per il filtro. Shell utilizza OPATH per la sintassi del filtro. OPATH è un linguaggio di query progettato per eseguire query sulle origini dati degli oggetti.

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Creazione di un elenco di indirizzi con i filtri destinatari tramite Shell

In questo esempio viene creato un elenco di indirizzi per tutti gli utenti con cassette postali Exchange in Oregon o nello stato di Washington.

    New-AddressList -Name "Pacific Northwest Mailboxes" -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

In questo esempio viene creato un elenco di indirizzi per tutti gli utenti con cassette postali di Exchange il cui parametro *CustomAttribute15* ha valore `AgencyB`.

    New-AddressList -Name "AgencyB" -RecipientFilter {(RecipientType -eq 'UserMailbox') -and (CustomAttribute15 -like *AgencyB*)}

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-AddressList](https://technet.microsoft.com/it-it/library/aa996912\(v=exchg.150\)).

