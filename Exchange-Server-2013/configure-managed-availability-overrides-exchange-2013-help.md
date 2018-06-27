---
title: 'Configurare le sostituzioni di disponibilità gestita: Exchange 2013 Help'
TOCTitle: Configurare le sostituzioni di disponibilità gestita
ms:assetid: c8f315b3-1d5e-4ad9-8bea-9c3a4a13ebfc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn482055(v=EXCHG.150)
ms:contentKeyID: 59890031
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le sostituzioni di disponibilità gestita

 

_**Si applica a:**Exchange Online, Exchange Server 2013 SP1_

_**Ultima modifica dell'argomento:**2015-11-30_

La disponibilità gestita esegue continuamente il probe per individuare possibili problemi con i componenti di Exchange o le relative dipendenze ed esegue azioni di ripristino per garantire che l'esperienza dell'utente finale non sia influenzata da problemi con nessuno di questi componenti. Tuttavia, potrebbero esistere scenari in cui le impostazioni predefinite non siano adatte all'ambiente dell'utente. Probe, strumenti di monitoraggio e risponditori della disponibilità gestita possono essere personalizzati mediante la creazione di una sostituzione.

Esistono due tipi di sostituzioni: locale e globale. Come indicato dai relativi nomi, una sostituzione locale è disponibile solo nel server in cui viene creato e una sostituzione globale viene utilizzata per applicare un override a più server. Per un determinato periodo di tempo o per una versione specifica di Exchange, ma non entrambi contemporaneamente, è possono creare entrambi i tipi di sostituzione.


> [!NOTE]
> Quando si crea un override, non hanno effetto immediato. Microsoft Exchange servizio di gestione dello stato verifica la presenza di modifiche alla configurazione ogni 10 minuti e carica le modifiche di configurazione rilevato. Se non si desidera di attesa, è possibile riavviare il servizio.



Per altre attività di gestione relative alla disponibilità gestita, vedere [Gestire i set di integrità e lo stato dei server](manage-health-sets-and-server-health-exchange-2013-help.md).

## Informazioni preliminari

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - È possibile utilizzare solo Shell per eseguire questa procedura. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Esegue l'override di utilizzare Exchange Management Shell per creare locale

Per creare una sostituzione locale per un determinato periodo, utilizzare la sintassi seguente.

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Duration <dd.hh:mm:ss>

Per creare una sostituzione locale per una versione specifica di Exchange, utilizzare la sintassi seguente.

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Version <15.01.xxxx.xxx>


> [!NOTE]
> Quando si crea l'override, i valori utilizzati nel parametro <EM>Identity</EM> sono tra maiuscole e minuscole.



In questo esempio viene aggiunta una sostituzione locale che disabilita il responder `ActiveDirectoryConnectivityConfigDCServerReboot` sul server denominato EXCH03 per 20 giorni.

    Add-ServerMonitoringOverride -Server EXCH03 -Identity "AD\ActiveDirectoryConnectivityConfigDCServerReboot" -ItemType Responder -PropertyName Enabled -PropertyValue 0 -Duration 20.00:00:00

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che è stata creata correttamente una sostituzione locale, utilizzare il cmdlet **Get-ServerMonitoringOverride** per visualizzare l'elenco delle sostituzioni locali:

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

La sostituzione deve essere visualizzata nell'elenco.

## Esegue l'override di utilizzare Exchange Management Shell per rimuovere locale

Per rimuovere una sostituzione locale, utilizzare la sintassi seguente.

    Remove-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <PropertytoRemove>

In questo esempio consente di rimuovere la sostituzione locale esistente del risponditore `ActiveDirectoryConnectivityConfigDCServerReboot` integrità Exchange dal server EXCH01.

    Remove-ServerMonitoringOverride -Server EXCH01 -Identity Exchange\ActiveDirectoryConnectivityConfigDCServerReboot -ItemType Responder -PropertyName Enabled

## Verifica dell'esito positivo dell'operazione

Per verificare che sia stata rimossa correttamente una sostituzione locale, utilizzare il cmdlet **Get-ServerMonitoringOverride** per visualizzare l'elenco delle sostituzioni locali:

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

La sostituzione rimossa non dovrà essere visualizzata nell'elenco.

## Utilizzare Exchange Management Shell per creare globale gli override

Per creare una sostituzione globale per un determinato periodo, utilizzare la sintassi seguente.

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -Duration <dd.hh:mm:ss>

Per creare una sostituzione globale per una versione specifica di Exchange, utilizzare la sintassi seguente.

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -ApplyVersion <15.01.xxxx.xxx>


> [!NOTE]
> Quando si crea l'override, i valori utilizzati nel parametro <EM>Identity</EM> sono tra maiuscole e minuscole.



In questo esempio viene aggiunta una sostituzione globale che disabilita il probe `OnPremisesInboundProxy` per 30 giorni.

    Add-GlobalMonitoringOverride -Identity "FrontendTransport\OnPremisesInboundProxy" -ItemType Probe -PropertyName Enabled -PropertyValue 0 -Duration 30.00:00:00

In questo esempio viene aggiunta una sostituzione globale che disabilita il responder `StorageLogicalDriveSpaceEscalate` per tutti i server che eseguono la versione Exchange 15.01.0225.042.

    Add-GlobalMonitoringOverride -Identity "MailboxSpace\StorageLogicalDriveSpaceEscalate" -PropertyName Enabled -PropertyValue 0 -ItemType Responder -ApplyVersion "15.01.0225.042"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver creato correttamente una sostituzione globale, utilizzare il cmdlet **Get-GlobalMonitoringOverride** per visualizzare l'elenco delle sostituzioni globali:

    Get-GlobalMonitoringOverride

La sostituzione deve essere visualizzata nell'elenco.

## Utilizzare Exchange Management Shell per rimuovere globale gli override

Per rimuovere una sostituzione globale, utilizzare la sintassi seguente.

    Remove-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <OverriddenProperty>

In questo esempio viene rimossa la sostituzione globale esistente della proprietà `ExtensionAttributes` del probe `OnPremisesInboundProxy` nel set di integrità `FrontEndTransport` .

    Remove-GlobalMonitoringOverride -Identity FrontEndTransport\OnPremisesInboundProxy -ItemType Probe -PropertyName ExtensionAttributes

## Verifica dell'esito positivo dell'operazione

Per verificare di aver rimosso correttamente una sostituzione globale, utilizzare il cmdlet **Get-GlobalMonitoringOverride** per visualizzare l'elenco delle sostituzioni globali:

    Get-GlobalMonitoringOverride

La sostituzione rimossa non dovrà essere visualizzata nell'elenco.

