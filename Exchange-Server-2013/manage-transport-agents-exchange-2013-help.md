---
title: 'Gestire gli agenti di trasporto: Exchange 2013 Help'
TOCTitle: Gestire gli agenti di trasporto
ms:assetid: f15ab7e4-015d-45b1-9c10-f733d7cd2a36
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125175(v=EXCHG.150)
ms:contentKeyID: 50482027
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire gli agenti di trasporto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Gli agenti di trasporto utilizzano gli eventi SMTP per eseguire operazioni sui messaggi durante il passaggio nella pipeline di trasporto. La maggior parte degli agenti di trasporto predefiniti inclusi in Microsoft Exchange Server 2013 sono invisibili e non gestibili. Tuttavia, è possibile installare e configurare agenti di trasporto di terze parti nei server Exchange dell'organizzazione. Per ulteriori informazioni sugli agenti di trasporto, vedere [Agenti di trasporto](transport-agents-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Agenti di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Il supporto per agenti di trasporto legacy non è abilitato per impostazione predefinita, tuttavia è possibile abilitarlo. Per istruzioni, vedere [Attivare il supporto per gli agenti di trasporto legacy](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Informazioni sulle procedure per gli agenti di trasporto nel servizio di trasporto front-end sui server Accesso client

Non è possibile utilizzare Exchange Management Shell per gestire l'agente di trasporto nel servizio di trasporto front-end su un server Accesso client. È necessario invece aprire Windows PowerShell sul server Accesso client e importare i cmdlet di Exchange nella sessione Windows PowerShell.


> [!WARNING]
> L'esecuzione di cmdlet di Exchange in Windows PowerShell per attività diverse dalla gestione degli agenti di trasporto nel servizio di trasporto front-end non è supportata. Potrebbero verificarsi gravi conseguenza se si ignora Exchange Management Shell e il controllo dell'accesso basato sui ruoli (RBAC) eseguendo i cmdlet Exchange in Windows PowerShell. È sempre consigliabile eseguire i cmdlet di Exchange in Exchange Management Shell. Per ulteriori informazioni, vedere <A href="release-notes-for-exchange-2013-exchange-2013-help.md">Note sulla versione di Exchange 2013</A>.



Per eseguire una o più procedure dell'agente di trasporto descritte in questo argomento nel servizio di trasporto front-end, è necessario effettuare i seguenti passaggi aggiuntivi:

1.  Sul server Accesso client aprire Windows PowerShell ed eseguire il comando riportato di seguito:
    
    ```powershell
Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
```

2.  Eseguire il comando come indicato, ma aggiungere il seguente valore al comando: `-TransportService FrontEnd`.
    
    Ad esempio, per visualizzare gli agenti di trasporto nel servizio di trasporto front-end su un server Accesso client, eseguire il comando riportato di seguito:
    
    ```powershell
Get-TransportAgent -TransportService FrontEnd
```

## Installazione di un agente di trasporto tramite Shell

Quando si installa un agente di trasporto, Exchange registra solamente le DLL associate all'agente di trasporto. Verificare che tutti i file, le chiavi di registro e gli altri oggetti da cui l'agente di trasporto dipende siano installati e configurati correttamente. Una volta caricate le DLL, Exchange continuerà a fare riferimento alle DLL dopo il completamento del comando.

Gli agenti di trasporto dispongono dell'accesso completo a tutti i messaggi di posta elettronica rilevati. In Exchange non sono previste limitazioni sul comportamento di un agente di trasporto. Gli agenti di trasporto instabili o contenenti difetti nel sistema di protezione possono incidere sulla stabilità e sulla protezione di Exchange. Pertanto, è necessario installare soltanto gli agenti di trasporto completamente attendibili e già sperimentati in un ambiente di prova.

Gli agenti di trasporto vengono installati in stato disabilitato, per garantire che il flusso di posta non venga influenzato dagli agenti di trasporto non ancora configurati. Pertanto, dopo aver configurato correttamente un agente di trasporto, è necessario abilitarlo.

Per installare un agente di trasporto, utilizzare la seguente sintassi.

    Install-TransportAgent -Name <TransportAgentIdentity> -TransportAgentFactory <"TransportAgentFactory"> -AssemblyPath <"FilePath">

In questo esempio viene installato un agente di trasporto fittizio denominato Contoso Transport Agent nel servizio di trasporto su un server Cassette postali.

    Install-TransportAgent -Name "Contoso Transport Agent" -TransportAgentFactory "vendor.exchange.ContosoTransportAgentfactory" -AssemblyPath "C:\Program Files\Vendor\TransportAgent\ContosoTransportAgentFactory.dll"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'agente di trasporto sia stato installato correttamente, eseguire il comando `Get-TransportAgent` e verificare che l'agente di trasporto sia incluso nell'elenco.

## Abilitazione di un agente di trasporto tramite Shell

Per abilitare un agente di trasporto, utilizzare la seguente sintassi.

```powershell
Enable-TransportAgent <TransportAgentIdentity>
```

In questo esempio viene abilitato l'agente di trasporto fittizio denominato Contoso Transport Agent nel servizio di trasporto su un server Cassette postali.

```powershell
Enable-TransportAgent "Contoso Transport Agent"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'agente di trasporto sia stato abilitato correttamente, eseguire il comando `Get-TransportAgent | Format-List Name,Enabled` e verificare che l'agente di trasporto sia abilitato.

## Disabilitazione di un agente di trasporto tramite Shell

Per disabilitare un agente di trasporto, utilizzare la seguente sintassi.

```powershell
Disable-TransportAgent <TransportAgentIdentity>
```

In questo esempio viene disabilitato l'agente di trasporto denominato Fabrikam Transport Agent nel servizio di trasporto su un server Cassette postali.

```powershell
Disable-TransportAgent "Fabrikam Transport Agent"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'agente di trasporto sia stato disabilitato correttamente, eseguire il comando `Get-TransportAgent | Format-List Name,Enabled` e verificare che l'agente di trasporto sia disabilitato.

## Visualizzazione degli agenti di trasporto tramite Shell

Per visualizzare un elenco di riepilogo di tutti gli agenti di trasporto, eseguire il comando riportato di seguito:

```powershell
Get-TransportAgent
```

Per visualizzare la configurazione dettagliata per un agente di trasporto specifico, eseguire il comando riportato di seguito:

```powershell
Get-TransportAgent <TransportAgentIdentity> | Format-List
```

In questo esempio viene fornita la configurazione dettagliata dell'agente di trasporto denominato Transport Rule Agent.

```powershell
Get-TransportAgent "Transport Rule Agent" | Format-List
```

## Configurazione della priorità di un agente di trasporto tramite Shell

Gli agenti di trasporto con la priorità più vicina a 0 elaborano per primi i messaggi di posta elettronica. Tuttavia, a causa dell'evento SMTP nella pipeline di trasporto in cui è registrato l'agente, sul messaggio potrebbe agire prima un agente con priorità più bassa, anziché un agente con priorità più alta.

Per modificare la priorità di un agente di trasporto esistente, utilizzare il comando riportato di seguito.

```powershell
Set-TransportAgent <TransportAgentIdentity> -Priority <Integer>
```

In questo esempio viene impostato il valore 3 per la priorità dell'agente relativa all'agente di trasporto Contoso Transport Agent nel servizio di trasporto su un server Cassette postali.

```powershell
Set-TransportAgent "Contoso Transport Agent" -Priority 3
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la priorità di un agente di trasporto sia stata configurata correttamente, eseguire il comando `Get-TransportAgent | Format-List Name,Priority` e verificare il valore della priorità dell'agente di trasporto.

## Disinstallazione di un agente di trasporto tramite Shell

Quando l'agente di trasporto viene disinstallato, Exchange non registra i file DLL utilizzati con l'agente. Non verranno rimossi file, chiavi del Registro di sistema o altri oggetti aggiunti al momento dell'installazione dell'agente di trasporto.

Per disinstallare un agente di trasporto, eseguire il comando riportato di seguito:

```powershell
Uninstall-TransportAgent <TransportAgentIdentity>
```

In questo esempio viene disinstallato l'agente di trasporto denominato Fabirkam Transport Agent dal servizio di trasporto su un server Cassette postali.

```powershell
Uninstall-TransportAgent "Fabrikam Transport Agent"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'agente di trasporto sia stato disinstallato correttamente, eseguire il comando `Get-TransportAgent` e verificare che l'agente di trasporto sia incluso nell'elenco.

