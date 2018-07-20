---
title: 'Configurare IRM per la ricerca di Exchange e In-Place eDiscovery: Exchange 2013 Help'
TOCTitle: Configurare IRM per la ricerca di Exchange e In-Place eDiscovery
ms:assetid: d96790e9-93ad-4a56-b90f-2dbfa2f2073c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg588319(v=EXCHG.150)
ms:contentKeyID: 50481822
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare IRM per la ricerca di Exchange e In-Place eDiscovery

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-16_

In Microsoft Exchange Server 2013, si può configurare IRM (Information Rights Management) in modo che il servizio di ricerca di Exchange può indicizzare i contenuti dei messaggi protetti tramite IRM.

Quando i membri del gruppo di ruoli Gestione individuazione eseguono una ricerca [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md), i messaggi protetti tramite IRM vengono inclusi nei risultati della ricerca e copiati nella cassetta postale di individuazione specificata nella ricerca. Inoltre, i membri del gruppo di ruoli Gestione individuazione possono utilizzare Outlook Web App per accedere ai messaggi protetti tramite IRM che sono stati copiati nella cassetta postale di individuazione come risultato della ricerca di individuazione.


> [!NOTE]
> I membri del gruppo di ruoli Gestione individuazione non possono accedere ai messaggi protetti tramite IRM esportati da una cassetta postale di individuazione in un'altra cassetta postale o in un file .pst. Si può accedere ai messaggi protetti tramite IRM in una cassetta postale di individuazione solo utilizzando Outlook Web App.



Per le attività di gestione aggiuntive correlate a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Protezione dei diritti" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - IRM deve essere configurato nell'organizzazione di Exchange 2013. Per ulteriori informazioni, vedere [Abilitazione o disabilitazione di IRM per i messaggi interni](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - La cassetta postale federata deve essere aggiunta al gruppo di utenti con privilegi avanzati in Active Directory Rights Management Services (AD RMS). Per ulteriori informazioni, vedere [Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per configurare IRM per Exchange Search e eDiscovery in locale. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Configurazione di IRM per il servizio Ricerca di Exchange tramite Shell

In questo esempio si configura IRM per consentire al servizio di ricerca di Exchange di indicizzare i messaggi protetti tramite IRM.


> [!NOTE]
> Per impostazione predefinita, il parametro <EM>SearchEnabled</EM> è impostato su <CODE>$true</CODE>. Per disabilitare l'indicizzazione dei messaggi protetti tramite IRM, impostarlo su <CODE>$false</CODE>. Disabilitando l'indicizzazione dei messaggi protetti tramite IRM, si impedisce che vengano inclusi nei risultati della ricerca quando un utente effettua una ricerca nella propria cassetta postale o quando un gestore di individuazione utilizza eDiscovery in locale.



    Set-IRMConfiguration -SearchEnabled $true

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Configurazione di IRM per eDiscovery in locale tramite Shell

Con questo esempio viene consentito ai membri del gruppo di ruoli Gestione di individuazione di accedere ai messaggi protetti tramite IRM che risiedono nella cassetta postale di individuazione.


> [!NOTE]
> Per impostazione predefinita, il parametro <EM>EDiscoverySuperUserEnabled</EM> è impostato su <CODE>$true</CODE>. Per disabilitare l'accesso ai messaggi protetti tramite IRM da parte dei membri del gruppo di ruoli Gestione di individuazione, impostarlo su <CODE>$false</CODE>.



    Set-IRMConfiguration -EDiscoverySuperUserEnabled $true

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che IRM sia stato configurato correttamente per Exchange Search e eDiscovery in locale, utilizzare il cmdlet **Get-IRMConfigurtaion** per recuperare le informazioni sulla configurazione di IRM. Per un esempio delle modalità di recupero della configurazione IRM, vedere [Examples](https://technet.microsoft.com/it-it/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) in **Get-IRMConfiguration**.

