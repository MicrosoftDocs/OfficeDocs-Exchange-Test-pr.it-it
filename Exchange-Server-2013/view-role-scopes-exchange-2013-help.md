---
title: 'Ruolo Visualizza ambiti: Exchange 2013 Help'
TOCTitle: Ruolo Visualizza ambiti
ms:assetid: 0bb3a434-6651-473a-94eb-4eb9a34e6f70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335084(v=EXCHG.150)
ms:contentKeyID: 50480007
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ruolo Visualizza ambiti

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Gli ambiti del ruolo di gestione consentono di determinare gli oggetti disponibili, in modo che l'utente possa modificarli utilizzando i cmdlet e i parametri relativi. È possibile visualizzare gli ambiti per determinare gli ambiti aggiunti all'organizzazione, la configurazione di uno specifico ambito o gli ambiti orfani.

Per ulteriori informazioni sugli ambiti del ruolo di gestione in Microsoft Exchange Server 2013, vedere [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative agli ambiti di ruolo, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ambiti di gestione" nell'argomento[Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Questo argomento utilizza il pipelining e il cmdlet **Format-List**. Per ulteriori informazioni su questi concetti, vedere i seguenti argomenti:
    
      - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))
    
      - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Visualizzazione di uno specifico ambito

È possibile visualizzare i dettagli di un ambito eseguendo il piping dell'output del cmdlet **Get-ManagementScope** al cmdlet **Format-List**.

Per visualizzare i dettagli di uno specifico ambito, utilizzare la seguente sintassi.

```powershell
Get-ManagementScope <scope name> | Format-List
```

In questo esempio vengono recuperati i dettagli dell'ambito Seattle Servers.

```powershell
Get-ManagementScope "Seattle Servers" | Format-List
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementScope](https://technet.microsoft.com/it-it/library/dd298180\(v=exchg.150\)).

## Elenco di tutti gli ambiti

In questo esempio viene recuperato un elenco degli ambiti nell'organizzazione.

```powershell
Get-ManagementScope
```

Questo cmdlet consente di recuperare gli ambiti esclusivi e regolari. Per la restituzione solo degli ambiti esclusivi o solo degli ambiti regolari, vedere "Elenco solo degli ambiti esclusivi o solo di quelli regolari" in questo argomento.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementScope](https://technet.microsoft.com/it-it/library/dd298180\(v=exchg.150\)).

## Elenco di tutti gli ambiti orfani

*Ambiti orfani* indicano gli ambiti non associati ad alcuna assegnazione del ruolo di gestione.

In questo esempio viene recuperato un elenco di ambiti orfani.

```powershell
Get-ManagementScope -Orphan
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementScope](https://technet.microsoft.com/it-it/library/dd298180\(v=exchg.150\)).

## Elenco solo degli ambiti esclusivi o solo di quelli regolari

Per impostazione predefinita, il cmdlet **Get-ManagementScope** consente di restituire un elenco di ambiti contenente gli ambiti esclusivi e regolari. Se si desidera restituire solo gli ambiti esclusivi o solo quelli regolari, utilizzare la seguente sintassi.

```powershell
Get-ManagementScope -Exclusive < $true | $false >
```

In questo esempio vengono restituiti solo gli ambiti esclusivi.

```powershell
Get-ManagementScope -Exclusive $true
```

In questo esempio viene restituito un elenco solo degli ambiti regolari.

```powershell
Get-ManagementScope -Exclusive $false
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementScope](https://technet.microsoft.com/it-it/library/dd298180\(v=exchg.150\)).

