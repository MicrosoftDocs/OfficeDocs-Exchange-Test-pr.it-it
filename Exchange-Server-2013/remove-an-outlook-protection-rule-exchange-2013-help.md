---
title: 'Rimuovere una regola di protezione di Outlook: Exchange 2013 Help'
TOCTitle: Rimuovere una regola di protezione di Outlook
ms:assetid: 569fc3be-b269-43f5-8797-73ab0691e685
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633467(v=EXCHG.150)
ms:contentKeyID: 50480637
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere una regola di protezione di Outlook

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Utilizzo di regole di protezione di Microsoft Outlook, è possibile proteggere i messaggi con Information Rights Management (IRM) applicando un modello di [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) in Outlook 2010 prima che i messaggi vengono inviati. Per impedire l'applicazione di una regola di protezione Outlook, è possibile disabilitare la regola. Rimozione di una regola di protezione Outlook rimuove la definizione della regola da Active Directory.

Per le attività di gestione aggiuntive correlate a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Protezione dei diritti" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per rimuovere le regole di protezione di Outlook. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Rimozione di una regola di protezione di Outlook tramite Shell

In questo esempio viene rimossa la regola di protezione di Outlook OPR-DG-Finance.

    Remove-OutlookProtectionRule -Identity "OPR-DG-Finance"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-OutlookProtectionRule](https://technet.microsoft.com/it-it/library/dd297961\(v=exchg.150\)).

## Rimozione di tutte le regole di protezione di Outlook tramite Shell

In questo esempio vengono rimosse tutte le regole di protezione di Outlook nell'organizzazione Exchange.

    Get-OutlookProtectionRule | Remove-OutlookProtectionRule

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-OutlookProtectionRule](https://technet.microsoft.com/it-it/library/dd298004\(v=exchg.150\)) e [Remove-OutlookProtectionRule](https://technet.microsoft.com/it-it/library/dd297961\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver correttamente rimosso una regola di protezione di Outlook, utilizzare il cmdlet [Get-OutlookProtectionRule](https://technet.microsoft.com/it-it/library/dd298004\(v=exchg.150\)) per visualizzare le regole di protezione di Outlook. Per un esempio di come visualizzare le regole di protezione di Outlook, vedere [Examples](https://technet.microsoft.com/it-it/dd298004\(exchg.150\)#examples) in **Get-OutlookProtectionRule**.

