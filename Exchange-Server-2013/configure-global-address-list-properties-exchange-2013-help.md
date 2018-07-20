---
title: "Configurare la proprietà dell'elenco indirizzi globale: Exchange 2013 Help"
TOCTitle: Configurare la proprietà dell'elenco indirizzi globale
ms:assetid: 5fd2c96f-fe93-4b5a-8495-70c450511a37
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232068(v=EXCHG.150)
ms:contentKeyID: 50480785
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la proprietà dell'elenco indirizzi globale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-12-16_

In questo argomento viene spiegato come modificare le impostazioni di un elenco indirizzi globale.

Per altre attività di gestione relative agli elenchi di indirizzi, vedere [Procedure dell'elenco indirizzi](address-list-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Elenchi indirizzi" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Non è possibile modificare le impostazioni dell'elenco indirizzi globale predefinito.

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione delle proprietà dell'elenco indirizzi globale tramite Shell

In questo esempio viene assegnato un nuovo nome, FourthCoffee, all'elenco indirizzi globale con GUID 96d0c505-eba8-4103-ad4f-577a1bf4ad7b.

    Set-GlobalAddressList -Identity 96d0c505-eba8-4103-ad4f-577a1bf4ad7b -Name FourthCoffee


> [!NOTE]
> Se si utilizzano le proprietà del filtro condizionale predefinito, il valore del parametro <EM>IncludedRecipients</EM> non può essere vuoto.



In questo esempio vengono modificati i destinatari che verranno compresi nell'elenco indirizzi globale Fourth Coffee insieme a quelli la cui società è impostata su Fourth Coffee.

    Set-GlobalAddressList -Identity Fourth Coffee -RecipientFilter {Company -eq "Fourth Coffee"}

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-GlobalAddressList](https://technet.microsoft.com/it-it/library/bb123877\(v=exchg.150\)).

