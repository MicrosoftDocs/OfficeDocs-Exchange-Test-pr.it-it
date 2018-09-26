---
title: 'Scaricare gli aggiornamenti al motore e alle definizioni: Exchange 2013 Help'
TOCTitle: Scaricare gli aggiornamenti al motore e alle definizioni
ms:assetid: 8f2ca383-e463-4df0-aa5d-29afe2f81aaf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657471(v=EXCHG.150)
ms:contentKeyID: 50481162
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Scaricare gli aggiornamenti al motore e alle definizioni

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Microsoft gli amministratori Exchange Server 2013 possono scaricare manualmente motore antimalware e gli aggiornamenti delle definizioni (firma). Si consiglia di scaricare il motore e alle definizioni degli aggiornamenti nel server Exchange prima dell'immissione nell'ambiente di produzione.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti

  - È possibile utilizzare solo Shell per eseguire questa procedura. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).

  - Per scaricare gli aggiornamenti, il computer deve essere in grado di accedere a Internet e di stabilire una connessione alla porta TCP 80 (HTTP). Se l'organizzazione utilizza un server proxy per l'accesso a Internet, vedere la sezione utilizzo di Shell per configurare le impostazioni del server proxy per gli aggiornamenti di anti-malware in questo argomento.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Protezione dal malware? voce nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) .

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare Shell per scaricare manualmente gli aggiornamenti al motore e alle definizioni

Per scaricare gli aggiornamenti al motore e alle definizioni, eseguire il seguente comando:
```powershell
    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity <FQDN of server>
```

In questo esempio vengono scaricati manualmente gli aggiornamenti motore e alle definizioni sul server Exchange denominato mailbox01. contoso.com:
```powershell
    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com
```

Facoltativamente, è possibile utilizzare il parametro *EngineUpdatePath* per scaricare gli aggiornamenti di in una posizione diversa il percorso predefinito dei `http://forefrontdl.microsoft.com/server/scanengineupdate`. È possibile utilizzare questo parametro per specificare un indirizzo HTTP alternativo o un percorso UNC. Se si specifica un percorso UNC, il servizio di rete deve avere accesso al percorso.

In questo esempio vengono scaricati manualmente motore e alle definizioni degli aggiornamenti nel server Exchange denominato mailbox01. contoso.com dal percorso UNC `\\FileServer01\Data\MalwareUpdates`:
```powershell
    & $env:ExchangeInstallPath\Scripts\Update-MalwareFilteringServer.ps1 -Identity mailbox01.contoso.com -EngineUpdatePath \\FileServer01\Data\MalwareUpdates
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare il corretto download degli aggiornamenti, è necessario accedere a Visualizzatore eventi e visualizzare il registro eventi. È consigliabile applicare un filtro per vedere solo gli eventi FIPFS, come spiegato nella procedura seguente.

1.  Dal menu **Start**, scegliere **Tutti i programmi** \> **Strumenti di amministrazione** \> **Visualizzatore eventi**.

2.  Nel Visualizzatore eventi, espandere **Registri di Windows** e fare clic su **Applicazione**.

3.  Scegliere **Filtro registro corrente** dal menu **Azioni**.

4.  Nella finestra di dialogo **Filtro registro corrente**, selezionare la casella di controllo **FIPFS** dall'elenco a discesa **Origini eventi** e fare clic su **OK**.

Se gli aggiornamenti del motore sono stati scaricati correttamente sarà visibile l'ID evento 6033, molto simile al seguente:

`MS Filtering Engine Update process performed a successful scan engine update.`

`Scan Engine: Microsoft`

`Update Path: http://forefrontdl.microsoft.com/server/scanengineupdate`

`Last Update time: ‎2012‎-‎08‎-‎16T13:22:17.000Z`

`Engine Version: 1.1.8601.0`

`Signature Version: 1.131.2169.0`

## Utilizzo della Shell per configurare le impostazioni del server proxy per gli aggiornamenti di anti-malware

Se l'organizzazione utilizza un server proxy per controllare l'accesso a Internet, è necessario identificare il server proxy in modo che il motore antimalware e gli aggiornamenti delle definizioni possono essere scaricati correttamente. Impostazioni del server proxy che sono disponibili tramite lo strumento **Netsh.exe** , le impostazioni di connessione Internet Explorer e il parametro *InternetWebProxy* nel cmdlet **Set-ExchangeServer** non influisce sulla modalità anti-malware aggiornamenti vengono scaricati.

Per configurare le impostazioni del server proxy per gli aggiornamenti di anti-malware, eseguire la procedura seguente.

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
        Add-PsSnapin Microsoft.Forefront.Filtering.Management.Powershell
    ```

2.  Utilizzare i cmdlet **Get-ProxySettings** e **Set-ProxySettings** per visualizzare e configurare le impostazioni del server proxy che vengono utilizzati per scaricare gli aggiornamenti di anti-malware. Il cmdlet **Set-ProxySettings** utilizza la sintassi seguente:
    ```powershell
        Set-ProxySettings -Enabled <$true | $false> -Server <Name or IP address of proxy server> -Port <TCP port of proxy server>
    ```
    Ad esempio, per configurare gli aggiornamenti di anti-malware per utilizzare il server proxy all'indirizzo 172.17.17.10 sulla porta TCP 80, eseguire il comando seguente.
    
    ```powershell
    Set-ProxySettings -Enabled $true -Server 172.17.17.10 -Port 80
    ```
    
    Per verificare le impostazioni del server proxy, eseguire il cmdlet **Get-ProxySettings** .

## Ulteriori informazioni

[Configurare i criteri antimalware](configure-anti-malware-policies-exchange-2013-help.md)

