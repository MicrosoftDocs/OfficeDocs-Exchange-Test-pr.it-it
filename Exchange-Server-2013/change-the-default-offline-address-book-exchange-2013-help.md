---
title: 'Modificare la Rubrica offline predefinita: Exchange 2013 Help'
TOCTitle: Modificare la Rubrica offline predefinita
ms:assetid: 61abf78e-2543-4431-acc8-839e3c7a4548
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998569(v=EXCHG.150)
ms:contentKeyID: 50480747
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare la Rubrica offline predefinita

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-12-16_

Per impostazione predefinita, quando si installa il ruolo del server Cassette postali, viene creata una Rubrica offline predefinita basata su Web denominata Rubrica offline predefinita. È possibile impostare come predefinita qualsiasi Rubrica offline nella propria organizzazione Exchange. La nuova Rubrica offline predefinita viene associata a tutti i nuovi database delle cassette postali creati. Nella propria organizzazione è possibile disporre di un'unica Rubrica offline predefinita. Se si elimina la Rubrica offline predefinita, MicrosoftExchange non assegna automaticamente un'altra Rubrica offline come predefinita. Pertanto, è necessario impostare manualmente una nuova Rubrica offline come predefinita.

Per altre attività di gestione relative alle rubriche offline, vedere [Procedure della Rubrica fuori rete](offline-address-book-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Rubriche offline" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, in Exchange Online il ruolo Elenco di indirizzi non è assegnato ad alcun gruppo di ruoli. Per utilizzare cmdlet che richiedono il ruolo Elenco di indirizzi, è necessario aggiungere il ruolo a un gruppo di ruoli. Per ulteriori informazioni, vedere la sezione "Aggiungere un ruolo a un gruppo di ruoli" nell'argomento [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Modifica della rubrica offline predefinita tramite Shell

In questo esempio viene impostata la Rubrica offline denominata My OAB come Rubrica offline predefinita.

    Set-OfflineAddressBook -Identity "My OAB" -IsDefault $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-OfflineAddressBook](https://technet.microsoft.com/it-it/library/aa996330\(v=exchg.150\)).

