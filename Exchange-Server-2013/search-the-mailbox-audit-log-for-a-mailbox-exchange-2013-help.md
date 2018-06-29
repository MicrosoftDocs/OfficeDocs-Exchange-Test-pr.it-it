---
title: 'Il Registro di controllo delle cassette postali per una cassetta postale di ricerca: Exchange 2013 Help'
TOCTitle: Il Registro di controllo delle cassette postali per una cassetta postale di ricerca
ms:assetid: 5b518a08-3b51-4ba3-bfbd-0e35cc5ff374
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff461930(v=EXCHG.150)
ms:contentKeyID: 50480757
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Il Registro di controllo delle cassette postali per una cassetta postale di ricerca

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-03_

È possibile ricercare in modo sincrono voci del registro di controllo delle cassette postali per una cassetta postale e visualizzare i risultati della ricerca in Shell.

Se si desidera eseguire una ricerca nei registri di controllo delle cassette postali per più cassette postali e inviare i risultati tramite posta elettronica a un determinato indirizzo, è necessario creare una ricerca nel registro di controllo delle cassette postali. Per ulteriori informazioni, vedere [Creare una ricerca dei registri di controllo delle cassette postali](create-a-mailbox-audit-log-search-exchange-2013-help.md).

Per altre attività di gestione relative alla registrazione di controllo delle cassette postali, vedere [Procedure di registrazione di controllo delle cassette postali](mailbox-audit-logging-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo delle cassette postali" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per impostazione predefinita, la registrazione di controllo delle cassette postali è disabilitata per tutte le cassette postali. Per ciascuna cassetta postale in cui si desidera eseguire il controllo, è necessario abilitare la registrazione di controllo e specificare le azioni del proprietario, del delegato o dell'amministratore della cassetta postale che si desidera controllare. Per ulteriori informazioni, vedere [Abilitare o disabilitare la registrazione per una cassetta postale di controllo delle cassette postali](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per cercare una cassetta postale nel registro di controllo delle cassette postali. Tuttavia, è possibile utilizzare l'interfaccia di amministrazione di Exchange per creare un rapporto degli accessi alla cassetta postale da parte di utenti diversi dai proprietari oppure cercare nel rapporto ed esportare i risultati.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Ricerca del registro di controllo delle cassette postali per una cassetta postale tramite Shell

Per esempi su come utilizzare Shell per cercare una cassetta postale nel registro di controllo delle cassette postali, vedere [Examples](https://technet.microsoft.com/it-it/ff522360\(exchg.150\)#examples) in [Search-MailboxAuditLog](https://technet.microsoft.com/it-it/library/ff522360\(v=exchg.150\)).

