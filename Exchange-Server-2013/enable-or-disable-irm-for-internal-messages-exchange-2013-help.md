---
title: 'Abilita/disabilita IRM per messaggi interni: Exchange 2013 Help'
TOCTitle: Abilitazione o disabilitazione di IRM per i messaggi interni
ms:assetid: a6a17f57-5304-41f1-954d-7301857d54a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124077(v=EXCHG.150)
ms:contentKeyID: 50481362
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitazione o disabilitazione di IRM per i messaggi interni

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-12_

In Microsoft Exchange Server 2013, Information Rights Management (IRM) è abilitato ai messaggi interni per impostazione predefinita. In tal modo sarà possibile creare le regole di protezione del trasporto e le regole di protezione di Microsoft Outlook per i messaggi protetti da IRM nel trasporto e nei client Microsoft Outlook 2010 e versioni successive. L'abilitazione di IRM per i messaggi interni è un prerequisito per tutte le altre funzionalità IRM di Exchange Server 2013, come la decrittografia del trasporto, la decrittografia della regola del journal, IRM in Microsoft Office Outlook Web App e IRM in Microsoft Exchange ActiveSync.


> [!WARNING]
> Disabilitando IRM per i messaggi interni verranno disabilitate tutte le funzionalità IRM nell'organizzazione di Exchange. Le funzionalità IRM lato client di Outlook, ad esempio la possibilità di leggere, rispondere, inoltrare e creare messaggi protetti da IRM utilizzando un server Active Directory Rights Management Services (AD&nbsp;RMS) non saranno interessate.



Per le attività di gestione aggiuntive correlate a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Protezione dei diritti" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange (EAC) per abilitare o disabilitare IRM per i messaggi interni. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo della shell per l'abilitazione di IRM per i messaggi interni

In questo esempio, IRM viene abilitato per i messaggi interni per l'organizzazione di Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $true

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Utilizzo della shell per la disabilitazione di IRM per i messaggi interni

Questo esempio disabilita IRM per i messaggi interni per l'organizzazione di Exchange.

    Set-IRMConfiguration -InternalLicensingEnabled $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione di IRM per i messaggi interni, utilizzare il cmdlet [Get-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd776120\(v=exchg.150\)) per controllare la configurazione.

