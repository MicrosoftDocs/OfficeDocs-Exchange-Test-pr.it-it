---
title: 'Gestione di reputazione mittente: Exchange 2013 Help'
TOCTitle: Gestione di reputazione mittente
ms:assetid: f2716bd9-e3ac-46d9-9264-4e3dabfa0f38
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125186(v=EXCHG.150)
ms:contentKeyID: 50482030
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione di reputazione mittente

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Reputazione mittente è fornita dall'agente di analisi del protocollo. Reputazione mittente consente di bloccare i messaggi in base alle diverse caratteristiche del mittente. La reputazione mittente si basa su dati permanenti relativi al mittente per determinare l'eventuale azione da eseguire su un messaggio in arrivo.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione da posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per impostazione predefinita le funzionalità di protezione da posta indesiderata non sono abilitate nel servizio di trasporto in un server Cassette postali. Le funzionalità di protezione da posta indesiderata in un server Cassette postali vengono solitamente abilitate se l'organizzazione di Exchange non prevede filtri preventivi di protezione da posta indesiderata prima di accettare i messaggi in arrivo. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - L'agente di analisi del protocollo è l'agente che si occupa della funzionalità di reputazione mittente. Quando si disattiva la reputazione del mittente, l'agente di analisi del protocollo risulta ancora abilitato.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione della reputazione mittente tramite Shell

Con questo esempio viene disabilitata la reputazione mittente.

```powershell
Set-SenderReputationConfig -Enabled $false
```

Con questo esempio viene abilitata la reputazione mittente.

```powershell
Set-SenderReputationConfig -Enabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la reputazione mittente sia stata abilitato o disabilitata correttamente, procedere come segue:

1.  Per verificare che l'agente di analisi del protocollo sia stato installato e abilitato, eseguire il comando riportato di seguito:
    
    ```powershell
        Get-TransportAgent
    ```

2.  Verificare i valori di reputazione mittente configurati eseguendo il comando riportato di seguito:
    ```powershell
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled
    ```
## Abilitazione o disabilitazione della reputazione mittente per messaggi interni o esterni tramite Shell

Per impostazione predefinita, la reputazione mittente è abilitata per i messaggi esterni e disabilitata per quelli interni. Un messaggio è considerato esterno se proviene da una connessione non autenticata esterna all'organizzazione Exchange. Un messaggio è considerato interno se proviene da una connessione non autenticata e se il dominio del mittente è configurato come dominio autorevole nell'organizzazione Exchange.

Per disabilitare la reputazione mittente per i messaggi esterni, eseguire il seguente comando:

```powershell
Set-SenderReputationConfig -ExternalMailEnabled $false
```

Per abilitare la reputazione mittente per i messaggi esterni, eseguire il seguente comando:

```powershell
Set-SenderReputationConfig -ExternalMailEnabled $true
```

Per disabilitare la reputazione mittente per i messaggi interni, eseguire il seguente comando:

```powershell
Set-SenderReputationConfig -InternalMailEnabled $false
```

Per abilitare la reputazione mittente per i messaggi interni, eseguire il seguente comando:

```powershell
Set-SenderReputationConfig -InternalMailEnabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la reputazione mittente sia stata abilitato o disabilitata correttamente per i messaggi interni ed esterni, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    ```powershell
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled
    ```
2.  Verificare che i valori visualizzati corrispondano a quelli configurati.

## Configurazione delle proprietà della reputazione mittente tramite Shell

Per configurare le proprietà della reputazione mittente, eseguire il comando riportato di seguito:

```powershell
Set-SenderReputationConfig -SrlBlockThreshold <Value> -SenderBlockingPeriod <Hours>
```

In questo esempio la soglia di blocco del livello di reputazione mittente (SRL) è impostata su 6 e la reputazione mittente viene configurata per aggiungere mittenti pericolosi all'elenco di indirizzi IP bloccati per 36 ore:

```powershell
Set-SenderReputationConfig -SrlBlockThreshold 6 -SenderBlockingPeriod 36
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che le proprietà della reputazione mittente siano state configurate correttamente, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
        Get-SenderReputationConfig
    ```

2.  Verificare che i valori visualizzati corrispondano a quelli configurati.

## Configurazione dell'accesso in uscita per il rilevamento di server proxy aperti tramite Shell

Potrebbe essere necessario eseguire ulteriori passaggi per consentire alla reputazione mittente di attraversare i firewall posti tra Internet e il server Exchange su cui è in esecuzione l'agente di analisi del protocollo. Nella seguente tabella sono elencate le porte in uscita necessarie per la reputazione mittente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocolli</th>
<th>Porte</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SOCKS4, SOCKS5</p></td>
<td><p>1081, 1080</p></td>
</tr>
<tr class="even">
<td><p>Wingate, Telnet, Cisco</p></td>
<td><p>23</p></td>
</tr>
<tr class="odd">
<td><p>HTTP CONNECT, POST HTTP</p></td>
<td><p>6588, 3128, 80</p></td>
</tr>
</tbody>
</table>


Per configurare l'accesso in uscita per il rilevamento di server proxy aperti, eseguire il comando riportato di seguito.
```powershell
    Set-SenderReputationConfig -ProxyServerName <String> -ProxyServerPort <Port> -ProxyServerType <String>
```
In questo esempio la reputazione mittente viene configurata per l'utilizzo del server proxy aperto denominato SERVER01 che utilizza il protocollo HTTP CONNECT sulla porta 80.
```powershell
    Set-SenderReputationConfig - ProxyServerName SERVER01 -ProxyServerPort 80 -ProxyServerType HttpConnect
```
## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'accesso in uscita per il rilevamento dei server proxy aperti sia stato configurato correttamente, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    ```powershell
        Get-SenderReputationConfig | Format-List ProxyServer*
    ```
2.  Verificare che i valori visualizzati siano quelli configurati.

