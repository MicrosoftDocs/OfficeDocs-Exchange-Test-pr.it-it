---
title: 'Creare un elenco indirizzi globale: Exchange 2013 Help'
TOCTitle: Creare un elenco indirizzi globale
ms:assetid: 59e4955a-8999-4d17-be9f-23a41a23b929
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232063(v=EXCHG.150)
ms:contentKeyID: 50480721
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un elenco indirizzi globale

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-12-16_

L'elenco indirizzi globale (GAL, Global Address List) è una directory contenente voci per ogni gruppo, utente e contatto all'interno dell'implementazione di un'organizzazione Microsoft Exchange. Se nell'organizzazione vengono utilizzati criteri per le rubriche, è consigliabile creare ulteriori Elenchi indirizzi globali. Per ulteriori informazioni, vedere [Criteri delle rubriche](address-book-policies-exchange-2013-help.md).

Per altre attività di gestione relative agli elenchi di indirizzi, vedere [Procedure dell'elenco indirizzi](address-list-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Elenchi indirizzi" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare la shell per creare un Elenco indirizzi globale utilizzando le proprietà del filtro condizionale

In questo esempio viene creato un Elenco indirizzi globale di nome GAL\_Contoso per i destinatari costituiti da utenti di cassette postali appartenenti alla società Contoso.

    New-GlobalAddressList -Name "GAL_Contoso" -IncludedRecipients MailboxUsers -ConditionalCompany Contoso


> [!NOTE]
> Se si utilizzano le proprietà del filtro condizionale predefinite, il parametro <EM>IncludedRecipients</EM> non può risultare vuoto.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-GlobalAddressList](https://technet.microsoft.com/it-it/library/bb123785\(v=exchg.150\)).

## Utilizzare la shell per creare un Elenco indirizzi globale utilizzando un filtro destinatari

In questo esempio viene creato un Elenco indirizzi globale di nome GAL\_AgencyA, che include destinatari per cui il parametro *CustomAttribute15* ha valore `AgencyA`.

    New-GlobalAddressList -Name "GAL_AgencyA" -RecipientFilter {CustomAttribute15 -like "AgencyA"}

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-GlobalAddressList](https://technet.microsoft.com/it-it/library/bb123785\(v=exchg.150\)).

