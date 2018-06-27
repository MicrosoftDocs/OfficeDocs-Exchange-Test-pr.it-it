---
title: 'Gestire gli agenti di estensione cmdlet: Exchange 2013 Help'
TOCTitle: Gestire gli agenti di estensione cmdlet
ms:assetid: 9141b3cb-ad13-4415-be2f-aa89f91445f5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298143(v=EXCHG.150)
ms:contentKeyID: 50555630
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire gli agenti di estensione cmdlet

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-11-19_

In questo argomento vengono illustrate le procedure per abilitare, disabilitare, visualizzare e modificare la priorità degli agenti di estensione cmdlet in Microsoft Exchange Server 2013. Per ulteriori informazioni sugli agenti di estensione cmdlet in Exchange 2013, vedere [Agenti di estensione di cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: meno di 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Agenti di estensione cmdlet" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Prima di abilitare `Scripting Agent`, è necessario verificare che sia configurato correttamente. Per ulteriori informazioni su `Scripting Agent`, vedere [Agenti di estensione di cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Abilitazione di un agente di estensione cmdlet

Quando si abilita un agente di estensione cmdlet in Exchange 2013, l'agente viene eseguito su tutti i server Exchange 2013 dell'organizzazione. Quando un agente viene abilitato, i cmdlet possono utilizzarlo°per eseguire ulteriori operazioni.


> [!WARNING]
> Prima di abilitare un agente, accertarsi di essere a conoscenza del funzionamento dell'agente e dell'impatto che l'agente avrà sull'organizzazione.



In questo esempio viene abilitato un agente di estensione cmdlet utilizzando il cmdlet **Enable-CmdletExtensionAgent**. È necessario specificare il nome dell'agente che si desidera abilitare quando si esegue il cmdlet. Prima di abilitare `Scripting Agent`, è necessario verificare che sia stato distribuito il file di configurazione `ScriptingAgentConfig.xml` a tutti i server nell'organizzazione. Se prima non si distribuisce il file di configurazione e si abilita `Scripting``Agent`, tutti i cmdlet non-**Get** avranno esito negativo quando verranno eseguiti. In questo esempio viene abilitato `Scripting Agent`.

    Enable-CmdletExtensionAgent "Scripting Agent"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Enable-CmdletExtensionAgent](https://technet.microsoft.com/it-it/library/dd335192\(v=exchg.150\)).

## Disabilitazione di un agente di estensione cmdlet

Quando si disabilita un agente di estensione cmdlet in Exchange 2013, l'agente viene disabilitato su tutti i server Exchange 2013 dell'organizzazione. Quando un agente è disattivato, non è più disponibile per i cmdlet. I cmdlet non possono più utilizzare l'agente per eseguire operazioni aggiuntive.


> [!WARNING]
> Prima di disabilitare un agente, accertarsi di essere a conoscenza del funzionamento dell'agente e dell'impatto che la sua disabilitazione avrà sull'organizzazione.



Per disabilitare un agente di estensione cmdlet, utilizzare il cmdlet **Disable-CmdletExtensionAgent**. Specificare il nome dell'agente da disabilitare in fase di esecuzione del cmdlet. Con questo esempio viene disabilitato `Scripting Agent`.

    Disable-CmdletExtensionAgent "Scripting Agent"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Disable-CmdletExtensionAgent](https://technet.microsoft.com/it-it/library/dd298132\(v=exchg.150\)).

## Visualizzazione degli agenti di estensione cmdlet esistenti

La visualizzazione degli agenti di estensione cmdlet consente di individuare gli agenti eseguiti per primi e gli agenti abilitati in un'organizzazione Exchange 2013. Per ulteriori informazioni sul pipelining e il cmdlet **Format-Table**, vedere i seguenti argomenti:

  - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))

  - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

In questo esempio si ottengono i dettagli di uno specifico agente di estensione cmdlet utilizzando il cmdlet **Get-CmdletExtensionAgent**. In questo esempio vengono restituiti i dettagli di `Mailbox Permissions Agent`.

    Get-CmdletExtensionAgent "Mailbox Permissions Agent"

In questo esempio si ottengono più agenti di estensione cmdlet utilizzando il cmdlet **Get-CmdletExtensionAgent** e viene eseguito il piping dell'output al cmdlet **Format-Table**. In questo esempio viene visualizzato un elenco di tutti gli agenti di estensione cmdlet dell'organizzazione e, utilizzando il cmdlet **Format-Table**, in una tabella vengono visualizzate le proprietà **Name**, **Enabled** e **Priority** di ciascun agente.

    Get-CmdletExtensionAgent | Format-Table Name, Enabled, Priority

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-CmdletExtensionAgent](https://technet.microsoft.com/it-it/library/dd297946\(v=exchg.150\)).

## Modifica della priorità di un agente di estensione cmdlet

La possibilità di modificare la priorità di un agente di estensione cmdlet in Exchange 2013 è utile quando si desidera che un determinato agente venga chiamato da un cmdlet prima di un altro agente. Ciò è utile specialmente se si crea uno script personalizzato in esecuzione in `Scripting Agent` e si desidera che lo script abbia la precedenza su un agente incorporato. Per ulteriori informazioni su `Scripting Agent`, vedere [Agenti di estensione di cmdlet](cmdlet-extension-agents-exchange-2013-help.md).


> [!WARNING]
> La modifica della priorità o la sostituzione della funzionalità di un agente incorporato è un'operazione avanzata. Assicurarsi di essere pienamente consapevoli delle modifiche che verranno apportate.



Gli agenti vengono ordinati da zero al numero massimo di agenti. Più l'agente è vicino allo zero, più alta sarà la priorità. Vengono chiamati per primi gli agenti con la priorità più alta. Per ulteriori informazioni sulle priorità degli agenti, vedere [Agenti di estensione di cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

In questo esempio viene modificata la priorità di un agente di estensione cmdlet utilizzando il cmdlet **Set-CmdletExtensionAgent**. In questo esempio, la priorità di `Scripting Agent` viene modificata su 3.

    Set-CmdletExtensionAgent "Scripting Agent" -Priority 3

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-CmdletExtensionAgent](https://technet.microsoft.com/it-it/library/dd335175\(v=exchg.150\)).

