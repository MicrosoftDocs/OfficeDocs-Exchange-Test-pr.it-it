---
title: "Configurazione dell'Assistente cartelle gestite: Exchange 2013 Help"
TOCTitle: Configurazione dell'Assistente cartelle gestite
ms:assetid: 9fcfb9b6-bd24-4218-a163-bc599cd5476a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123958(v=EXCHG.150)
ms:contentKeyID: 50481287
ms.date: 01/08/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurazione dell'Assistente cartelle gestite

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-10-01_

L'*Assistente cartelle gestite* è un assistente per le cassette postali di MicrosoftExchange che applica le impostazioni di conservazione dei messaggi configurate nei criteri di conservazione.

Per altre attività di gestione relative a Gestione record di messaggistica, vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange (EAC) per configurare l'Assistente cartelle gestite. È necessario utilizzare Shell

  - In Exchange 2013, l'Assistente cartelle gestite è un assistente basato sulle limitazioni. Gli assistenti basati sulla limitazione sono sempre in esecuzione e non è necessario programmarli. Le risorse del sistema che consumano sono limitate. È possibile configurare l'Assistente cartelle gestite per elaborare tutte le cassette postali su un server Cassette postali entro un certo periodo di tempo (noto come *ciclo di lavoro*). Il ciclo di lavoro è impostato su un giorno per impostazione predefinita.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare Shell per configurare l'Assistente cartelle gestite

Questo esempio configura l'Assistente cartelle gestite per elaborare tutte le cassette postali in un solo giorno.

```powershell
Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-MailboxServer](https://technet.microsoft.com/it-it/library/aa998651\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta configurazione dell'Assistente cartelle gestite, utilizzare il cmdlet [Get-MailboxServer](https://technet.microsoft.com/it-it/library/bb123539\(v=exchg.150\)) per controllare il parametro *ManagedFolderWorkCycle*.

Questo comando recupera tutti i server Cassette postali nell'organizzazione e genera in output da ogni server le proprietà del ciclo di lavoro dell'Assistente cartelle gestite, utilizzando un formato tabella. L'opzione *Auto* è utilizzata per adattare automaticamente la larghezza delle colonne.

    Get-MailboxServer | Format-Table Name,ManagedFolderWorkCycle* -Auto

## Utilizzare Shell per avviare l'Assistente cartelle gestite

In questo esempio l'Assistente cartelle gestite viene impostato in modo che elabori immediatamente la cassetta postale di Morris Cornejo.

```powershell
Start-ManagedFolderAssistant -Identity morris.cornejo@contoso.com
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Start-ManagedFolderAssistant](https://technet.microsoft.com/it-it/library/aa998864\(v=exchg.150\)).

