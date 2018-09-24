---
title: 'Gestire il filtro connessioni su server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Gestire il filtro connessioni su server Trasporto Edge
ms:assetid: baebc865-ec3e-48ca-ac48-7aac8b34c003
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124376(v=EXCHG.150)
ms:contentKeyID: 60829842
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire il filtro connessioni su server Trasporto Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Il filtro delle connessioni è una funzionalità di protezione da posta indesiderata che viene fornita dall'agente Filtro connessioni e che è disponibile solo sui server Trasporto Edge in Microsoft Exchange 2013. Il filtro delle connessioni abilita le seguenti funzionalità:

  - Elenco Blocca indirizzi IP

  - Provider dell'elenco indirizzi IP bloccati

  - Elenco Consenti indirizzi IP

  - Provider dell'elenco indirizzi IP consentiti

Ciascuna di queste funzionalità può essere abilitata o disabilitata separatamente.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione da posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione del filtro connessioni tramite Shell

Per abilitare o disabilitare completamente il filtro connessioni, è necessario abilitare o disabilitare l'agente Filtro connessioni. La modifica viene applicata al riavvio del servizio Trasporto di Microsoft Exchange. Quando si riavvia il servizio Trasporto di Microsoft Exchange in un server Trasporto Edge, il flusso di posta sul server viene interrotto temporaneamente.

Per disabilitare il filtro connessioni, eseguire il seguente comando:

```powershell
Disable-TransportAgent "Connection Filtering Agent"
```

Per abilitare il filtro connessioni, eseguire il seguente comando:

```powershell
Enable-TransportAgent "Connection Filtering Agent"
```

Per rendere effettiva la modifica, riavviare il servizio Trasporto di Microsoft Exchange eseguendo il seguente comando:

```powershell
Restart-Service MSExchangeTransport
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione del filtro connessioni, eseguire il seguente comando e verificare che il valore visualizzato sia il valore che era stato configurato.

```powershell
Get-TransportAgent "Connection Filtering Agent" | Format-List Enabled
```

## Procedure dell'elenco indirizzi IP bloccati

Le seguenti procedure si applicano all'elenco indirizzi IP bloccati che viene configurato manualmente. Non si applicano ai provider dell'elenco indirizzi IP bloccati.

Utilizzare i cmdlet **IPBlockListConfig** per visualizzare e configurare il modo in cui il filtro connessioni utilizza l'elenco indirizzi IP bloccati. Utilizzare i cmdlet **IPBlockListEntry** per visualizzare e configurare gli indirizzi IP dell'elenco indirizzi IP bloccati.

## Utilizzo della Shell per visualizzare la configurazione dell'elenco indirizzi IP bloccati

Per visualizzare la configurazione dell'elenco indirizzi IP bloccati, eseguire il seguente comando:
```powershell
    Get-IPBlockListConfig | Format-List *Enabled,*Response
```
## Utilizzo della Shell per abilitare o disabilitare l'elenco indirizzi IP bloccati

Per disabilitare l'elenco indirizzi IP bloccati, eseguire il seguente comando:

```powershell
Set-IPBlockListConfig -Enabled $false
```

Per abilitare l'elenco indirizzi IP bloccati, eseguire il seguente comando:

```powershell
Set-IPBlockListConfig -Enabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione dell'elenco indirizzi IP bloccati, eseguire il seguente comando e verificare che il valore visualizzato sia il valore che era stato configurato.

```powershell
Get-IPBlockListConfig | Format-List Enabled
```

## Utilizzo della Shell per configurare l'elenco indirizzi IP bloccati

Per configurare l'elenco indirizzi IP bloccati, utilizzare la sintassi di seguito:
```powershell
    Set-IPBlockListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false> -MachineEntryRejectionResponse "<Custom response text>"] [-StaticEntryRejectionResponse "<Custom response text>"]
```
In questo esempio viene configurato l'elenco indirizzi IP bloccati con le relative impostazioni, come indicato di seguito:

  - L'elenco indirizzi IP bloccati filtra le connessioni in ingresso dai server di posta interni ed esterni. Per impostazione predefinita, le connessioni vengono filtrate unicamente dai server di posta esterni (il parametro *ExternalMailEnabled* è impostato su `$true` e il parametro *InternalMailEnabled* è impostato su `$false`). Le connessioni non autenticate e autenticate dai partner esterni vengono considerate esterne.

  - Il testo della risposta personalizzata per le connessioni filtrate dagli indirizzi IP aggiunti automaticamente all'elenco indirizzi IP bloccati dalla funzionalità di reputazione del mittente dell'agente di analisi protocollo è impostata sul valore "Connessione dall'indirizzo IP {0} rifiutata in base alla reputazione del mittente".

  - Il testo della risposta personalizzata per le connessioni filtrate mediante gli indirizzi IP aggiunti manualmente all'elenco indirizzi IP bloccati è impostato sul valore "Connessione dall'indirizzo IP {0} rifiutata in base al filtro connessioni".

<!-- end list -->
```powershell
    Set-IPBlockListConfig -InternalMailEnabled $true -MachineEntryRejectionResponse "Connection from IP address {0} was rejected by sender reputation." -StaticEntryRejectionResponse "Connection from IP address {0} was rejected by connection filtering."
```
## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione dell'elenco indirizzi IP bloccati, eseguire il seguente comando e verificare che i valori visualizzati siano quelli che erano stati configurati.
```powershell
    Get-IPBlockListConfig | Format-List *MailEnabled,*Response
```
## Utilizzo della Shell per visualizzare le voci dell'elenco indirizzi IP bloccati

Per visualizzare tutte le voci dell'elenco indirizzi IP bloccati, eseguire il seguente comando:

```powershell
Get-IPBlockListEntry
```

Ciascuna voce dell'elenco indirizzi IP bloccati è identificata da un valore intero. L'intero dell'identità viene assegnato in ordine crescente quando si aggiungono le voci all'elenco indirizzi IP bloccati e all'elenco indirizzi IP consentiti.

Per visualizzare una voce specifica dell'elenco indirizzi IP bloccati, utilizzare la sintassi seguente:

```powershell
Get-IPBlockListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

Ad esempio, per visualizzare la voce dell'elenco indirizzi IP bloccati che contiene l'indirizzo IP 192.168.1.13, eseguire il seguente comando:

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.13
```


> [!NOTE]
> Quando si utilizza il parametro <EM>IPAddress</EM>, la voce risultante dell'elenco indirizzi IP bloccati può essere un singolo indirizzo IP, un intervallo di indirizzi IP oppure un IP CIDR (Classless InterDomain Routing). Per utilizzare il parametro <EM>Identity</EM>, viene specificato il valore intero assegnato alla voce dell'elenco indirizzi IP bloccati.



## Utilizzo della Shell per aggiungere voci dell'elenco indirizzi IP bloccati

Per aggiungere voci all'elenco indirizzi IP bloccati, utilizzare la sintassi di seguito:
```powershell
    Add-IPBlockListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-comment "<Descriptive Comment>"]
```
L'esempio seguente consente di aggiungere la voce dell'elenco indirizzi IP bloccati per l'intervallo di indirizzi IP da 192.168.1.10 a 192.168.1.15 e configurare la scadenza dell'elenco indirizzi IP bloccati al 4 luglio 2014 alle ore 15:00.

```powershell
Add-IPBlockListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che una voce sia stata aggiunta correttamente all'elenco indirizzi IP bloccati, eseguire il seguente comando e verificare che la nuova voce dell'elenco indirizzi IP bloccati sia visualizzata.

```powershell
Get-IPBlockListEntry
```

## Utilizzo della Shell per rimuovere voci dell'elenco indirizzi IP bloccati

Per rimuovere voci dall'elenco indirizzi IP bloccati, utilizzare la sintassi di seguito:

```powershell
Remove-IPBlockListEntry <IdentityInteger>
```

L'esempio seguente consente di rimuovere la voce dell'elenco indirizzi IP bloccati con il parametro *Identity* di valore 3.

```powershell
Remove-IPBlockListEntry 3
```

L'esempio seguente consente di rimuovere la voce dell'elenco indirizzi IP bloccati contenente l'indirizzo IP 192.168.1.12 senza utilizzare il valore intero del parametro *Identity*. La voce dell'elenco indirizzi IP bloccati può essere costituita da un singolo indirizzo IP oppure da un intervallo di indirizzi IP.

```powershell
Get-IPBlockListEntry -IPAddress 192.168.1.12 | Remove-IPBlockListEntry
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che una voce sia stata rimossa correttamente dall'elenco indirizzi IP bloccati, eseguire il seguente comando e verificare che la voce rimossa dall'elenco indirizzi IP bloccati non sia più presente.

```powershell
Get-IPBlockListEntry
```

## Procedure del provider dell'elenco indirizzi IP bloccati

Le seguenti procedure si applicano ai provider dell'elenco indirizzi IP bloccati. Non si applicano all'elenco indirizzi IP bloccati.

Utilizzare i cmdlet **IPBlockListProvidersConfig** per visualizzare e configurare il modo in cui il filtro connessioni utilizza i provider dell'elenco indirizzi IP bloccati. Utilizzare i cmdlet **IPBlockListProvider** per visualizzare, configurare e verificare i provider dell'elenco indirizzi IP bloccati.

## Utilizzo della Shell per visualizzare la configurazione di tutti i provider dell'elenco indirizzi IP bloccati

Per visualizzare in che modo il filtro connessioni utilizza tutti i provider dell'elenco indirizzi IP bloccati, eseguire il seguente comando:
```powershell
    Get-IPBlockListProvidersConfig | Format-List *Enabled,Bypassed*
```
## Utilizzo della Shell per abilitare o disabilitare tutti i provider dell'elenco indirizzi IP bloccati

Per disabilitare tutti i provider dell'elenco indirizzi IP bloccati, eseguire il seguente comando:

```powershell
Set-IPBlockListProvidersConfig -Enabled $false
```

Per abilitare tutti i provider dell'elenco indirizzi IP bloccati, eseguire il seguente comando:

```powershell
Set-IPBlockListProvidersConfig -Enabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione di tutti i provider dell'elenco indirizzi IP bloccati, eseguire il seguente comando e verificare che il valore visualizzato sia il valore che era stato configurato.

```powershell
Get-IPBlockListProvidersConfig | Format-List Enabled
```

## Utilizzo della Shell per configurare tutti i provider dell'elenco indirizzi IP bloccati

Per configurare in che modo il filtro connessioni utilizza tutti i provider dell'elenco indirizzi IP bloccati, utilizzare la sintassi seguente:
```powershell
    Set-IPBlockListProvidersConfig [-BypassedRecipients <recipient1,recipient2...>] [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]
```
L'esempio seguente consente di configurare tutti i provider dell'elenco indirizzi IP bloccati con le seguenti impostazioni:

  - I provider dell'elenco indirizzi IP bloccati filtrano le connessioni in ingresso dai server di posta interni ed esterni. Per impostazione predefinita, le connessioni vengono filtrate unicamente dai server di posta esterni (il parametro *ExternalMailEnabled* è impostato su `$true` e il parametro *InternalMailEnabled* è impostato su `$false`). Le connessioni non autenticate e autenticate dai partner esterni vengono considerate esterne.

  - I messaggi inviati ai destinatari interni chris@fabrikam.com e michelle@fabrikam.com sono esclusi dal filtro mediante i provider dell'elenco indirizzi IP bloccati. Se si desidera aggiungere destinatari all'elenco senza influire sui destinatari esistenti, utilizzare la sintassi `@{Add="<recipient1>","<recipient2>"...}`.

<!-- end list -->
```powershell
    Set-IPBlockListProvidersConfig -BypassedRecipients chris@fabrikam.com,michelle@fabrikam.com -InternalMailEnabled $true
```
Per ulteriori informazioni, vedere [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/it-it/library/aa998543\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione di tutti i provider dell'elenco indirizzi IP bloccati, eseguire il seguente comando e verificare che i valori visualizzati siano quelli che erano stati configurati.
```powershell
    Get-IPBlockListProvidersConfig | Format-List *MailEnabled,Bypassed*
```
## Utilizzo della Shell per visualizzare i provider dell'elenco indirizzi IP bloccati

Per visualizzare l'elenco di riepilogo di tutti i provider dell'elenco indirizzi IP bloccati, eseguire il seguente comando:

```powershell
Get-IPBlockListProvider
```

Per visualizzare i dettagli di un provider specifico, utilizzare la seguente sintassi:

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity>
```

L'esempio seguente consente di visualizzare i dettagli del provider denominato Contoso IP Block List Provider.
```powershell
    Get-IPBlockListProvider "Contoso IP Block List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match,*Response
```
## Utilizzo della Shell per aggiungere un provider dell'elenco indirizzi IP bloccati

Per aggiungere un provider dell'elenco indirizzi IP bloccati, utilizzare la sintassi di seguito:
```powershell
    Add-IPBlockListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]
```
Questo esempio consente di creare un provider dell'elenco indirizzi IP bloccati denominato "Contoso IP Block List Provider" con le seguenti opzioni:

  - **FQDN per l'utilizzo del porvider**   rbl.contoso.com

  - **Codice maschera di bit che deve essere utilizzato dal provider**   127.0.0.1

<!-- end list -->
```powershell
    Add-IPBlockListProvider -Name "Contoso IP Block List Provider" -LookupDomain rbl.contoso.com -BitmaskMatch 127.0.0.1
```

> [!NOTE]
> Quando si aggiunge un nuovo provider dell'elenco indirizzi IP bloccati, questo viene abilitato per impostazione predefinita (il valore del parametro <EM>Enabled</EM> è <CODE>$true</CODE>), e il valore di priorità viene incrementato (la prima voce ha il valore <EM>Priority</EM> 1).



Per ulteriori informazioni, vedere [Add-IPBlockListProvider](https://technet.microsoft.com/it-it/library/bb124358\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che un provider dell'elenco indirizzi IP bloccati sia stato aggiunto correttamente, eseguire il seguente comando e verificare che il nuovo provider dell'elenco indirizzi IP bloccati sia visualizzato.

```powershell
Get-IPBlockListProvider
```

## Utilizzo della Shell per abilitare o disabilitare un provider dell'elenco indirizzi IP bloccati

Per abilitare o disabilitare uno specifico provider dell'elenco indirizzi IP bloccati, utilizzare la sintassi seguente:

```powershell
Set-IPBlockListProvider <IPBlockListProviderIdentity> -Enabled <$true | $false>
```

L'esempio seguente consente di disabilitare il provider denominato Contoso IP Block List Provider.

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $false
```

L'esempio seguente consente di abilitare il provider denominato Contoso IP Block List Provider.

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione del provider dell'elenco indirizzi IP bloccati, eseguire il seguente comando e verificare che il valore visualizzato sia il valore che era stato configurato.

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List Enabled
```

## Utilizzo della Shell per configurare un provider dell'elenco indirizzi IP bloccati

Le opzioni di configurazione disponibili nel cmdlet **Set-IPBlockListProvider** sono identiche a quelle nel cmdlet **New-IPBlockListProvider**.

Per configurare un provider dell'elenco indirizzi IP bloccati esistente, utilizzare la sintassi di seguito:
```powershell
    Set-IPBlockListProvider <IPBlockListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]
```
Ad esempio, per aggiungere il codice di stato dell'indirizzo IP 127.0.0.1 all'elenco dei codici di stato esistenti per il provider denominato Contoso IP Block List Provider, eseguire il seguente comando:

```powershell
Set-IPBlockListProvider "Contoso IP Block List Provider" -IPAddressesMatch @{Add="127.0.0.1"}
```

Per ulteriori informazioni, vedere [Set-IPBlockListProvider](https://technet.microsoft.com/it-it/library/bb124979\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione di un provider dell'elenco indirizzi IP bloccati, eseguire il seguente comando e verificare che i valori visualizzati siano quelli che erano stati configurati.

```powershell
Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List
```

## Utilizzo della Shell per verificare un provider dell'elenco indirizzi IP bloccati

Per verificare un provider dell'elenco indirizzi IP bloccati, utilizzare la sintassi di seguito.

```powershell
Test-IPBlockListProvider <IPBlockListProviderIdentity> -IPAddress <IPAddressToTest>
```

L'esempio seguente consente di verificare il provider denominato Contoso IP Block List Provider cercando l'indirizzo IP 192.168.1.1.

```powershell
Test-IPBlockListProvider "Contoso IP Block List Provider" -IPAddress 192.168.1.1
```

## Utilizzo della Shell per rimuovere un provider dell'elenco indirizzi IP bloccati

Per rimuovere un provider dell'elenco indirizzi IP bloccati, utilizzare la sintassi di seguito:

```powershell
Remove-IPBlockListProvider <IPBlockListProviderIdentity>
```

L'esempio seguente consente di rimuovere il provider dell'elenco indirizzi IP bloccati denominato Contoso IP Block List Provider.

```powershell
Remove-IPBlockListProvider "Contoso IP Block list Provider"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che un provider dell'elenco indirizzi IP bloccati sia stato rimosso correttamente, eseguire il seguente comando e verificare che il provider dell'elenco indirizzi IP rimosso non sia più presente.

```powershell
Get-IPBlockListProvider
```

## Procedure dell'elenco indirizzi IP consentiti

Le seguenti procedure si applicano all'elenco indirizzi IP consentiti che viene configurato manualmente. Non si applicano ai provider dell'elenco indirizzi IP consentiti.

Utilizzare i cmdlet **IPAllowListConfig** per visualizzare e configurare il modo in cui il filtro connessioni utilizza l'elenco indirizzi IP consentiti. Utilizzare i cmdlet **IPAllowListEntry** per visualizzare e configurare gli indirizzi IP dell'elenco indirizzi IP consentiti.

## Utilizzo della Shell per visualizzare la configurazione dell'elenco indirizzi IP consentiti

Per visualizzare la configurazione dell'elenco indirizzi IP consentiti, eseguire il seguente comando:

    Get-IPAllowListConfig | Format-List *Enabled

## Utilizzo della Shell per abilitare o disabilitare l'elenco indirizzi IP consentiti

Per disabilitare l'elenco indirizzi IP consentiti, eseguire il seguente comando:

```powershell
Set-IPAllowListConfig -Enabled $false
```

Per abilitare l'elenco indirizzi IP consentiti, eseguire il seguente comando:

```powershell
Set-IPAllowListConfig -Enabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione dell'elenco indirizzi IP consentiti, eseguire il seguente comando e verificare che il valore visualizzato sia il valore che era stato configurato.

```powershell
Get-IPAllowListConfig | Format-List *Enabled
```

## Utilizzo della Shell per configurare l'elenco indirizzi IP consentiti

Per configurare l'elenco indirizzi IP consentiti, utilizzare la sintassi di seguito:
```powershell
    Set-IPAllowListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>
```
Questo esempio consente di configurare l'elenco indirizzi IP consentiti in modo da filtrare le connessioni in ingresso dai server di posta interni ed esterni. Per impostazione predefinita, le connessioni vengono filtrate unicamente dai server di posta esterni (il parametro *ExternalMailEnabled* è impostato su `$true` e il parametro *InternalMailEnabled* è impostato su `$false`). Le connessioni non autenticate e autenticate dai partner esterni vengono considerate esterne.

```powershell
Set-IPAllowListConfig -InternalMailEnabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione dell'elenco indirizzi IP consentiti, eseguire il seguente comando e verificare che i valori visualizzati siano quelli che erano stati configurati.
```powershell
    Get-IPAllowListConfig | Format-List *MailEnabled
```
## Utilizzo della Shell per visualizzare le voci dell'elenco indirizzi IP consentiti

Per visualizzare tutte le voci dell'elenco indirizzi IP consentiti, eseguire il seguente comando:

```powershell
Get-IPAllowListEntry
```

Ciascuna voce dell'elenco indirizzi IP consentiti è identificata da un valore intero. L'intero dell'identità viene assegnato in ordine crescente quando si aggiungono le voci all'elenco indirizzi IP bloccati e all'elenco indirizzi IP consentiti.

Per visualizzare una voce specifica dell'elenco indirizzi IP consentiti, utilizzare la sintassi seguente:

```powershell
Get-IPAllowListEntry <-Identity IdentityInteger | -IPAddress IPAddress>
```

Ad esempio, per visualizzare la voce dell'elenco indirizzi IP consentiti che contiene l'indirizzo IP 192.168.1.13, eseguire il seguente comando:

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.13
```


> [!NOTE]
> Quando si utilizza il parametro <EM>IPAddress</EM>, la voce risultante dell'elenco indirizzi IP consentiti può essere un singolo indirizzo IP, un intervallo di indirizzi IP oppure un IP CIDR (Classless InterDomain Routing). Per utilizzare il parametro <EM>Identity</EM>, viene specificato il valore intero assegnato alla voce dell'elenco indirizzi IP consentiti.



## Utilizzo della Shell per aggiungere voci dell'elenco indirizzi IP consentiti

Per aggiungere voci all'elenco indirizzi IP consentiti, utilizzare la sintassi di seguito:
```powershell
    Add-IPAllowListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-Comment "<Descriptive Comment>"]
```
L'esempio seguente consente di aggiungere la voce dell'elenco indirizzi IP consentiti per l'intervallo di indirizzi IP da 192.168.1.10 a 192.168.1.15 e di configurare la scadenza dell'elenco indirizzi IP consentiti al 4 luglio 2014 alle ore 15:00.

```powershell
Add-IPAllowListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che una voce sia stata aggiunta correttamente all'elenco indirizzi IP consentiti, eseguire il seguente comando e verificare che la nuova voce dell'elenco indirizzi IP consentiti sia visualizzata.

```powershell
Get-IPAllowListEntry
```

## Utilizzo della Shell per rimuovere voci dell'elenco indirizzi IP consentiti

Per rimuovere voci dall'elenco indirizzi IP consentiti, utilizzare la sintassi di seguito:

```powershell
Remove-IPAllowListEntry <IdentityInteger>
```

L'esempio seguente consente di rimuovere la voce dell'elenco indirizzi IP consentiti con il parametro *Identity* di valore 3.

```powershell
Remove-IPAllowListEntry 3
```

L'esempio seguente consente di rimuovere la voce dell'elenco indirizzi IP consentiti contenente l'indirizzo IP 192.168.1.12 senza utilizzare il valore intero del parametro *Identity*. La voce dell'elenco indirizzi IP consentiti può essere costituita da un singolo indirizzo IP oppure da un intervallo di indirizzi IP.

```powershell
Get-IPAllowListEntry -IPAddress 192.168.1.12 | Remove-IPAllowListEntry
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che una voce sia stata rimossa correttamente dall'elenco indirizzi IP consentiti, eseguire il seguente comando e verificare che la voce rimossa dall'elenco indirizzi IP consentiti non sia più presente.

```powershell
Get-IPAllowListEntry
```

## Procedure del provider dell'elenco indirizzi IP consentiti

Le seguenti procedure si applicano ai provider dell'elenco indirizzi IP consentiti. Non si applicano all'elenco indirizzi IP consentiti.

Utilizzare i cmdlet **IPAllowListProvidersConfig** per visualizzare e configurare il modo in cui il filtro connessioni utilizza i provider dell'elenco indirizzi IP consentiti. Utilizzare i cmdlet **IPAllowListProvider** per visualizzare, configurare e verificare i provider dell'elenco indirizzi IP consentiti.

## Utilizzo della Shell per visualizzare la configurazione di tutti i provider dell'elenco indirizzi IP consentiti

Per visualizzare in che modo il filtro connessioni utilizza tutti i provider dell'elenco indirizzi IP consentiti, eseguire il seguente comando:
```powershell
    Get-IPAllowListProvidersConfig | Format-List *Enabled
```
## Utilizzo della Shell per abilitare o disabilitare tutti i provider dell'elenco indirizzi IP consentiti

Per disabilitare tutti i provider dell'elenco indirizzi IP consentiti, eseguire il seguente comando:

```powershell
Set-IPAllowListProvidersConfig -Enabled $false
```

Per abilitare tutti i provider dell'elenco indirizzi IP consentiti, eseguire il seguente comando:

```powershell
Set-IPAllowListProvidersConfig -Enabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione di tutti i provider dell'elenco indirizzi IP consentiti, eseguire il seguente comando e verificare che il valore visualizzato sia il valore che era stato configurato.

```powershell
Get-IPAllowListProvidersConfig | Format-List Enabled
```

## Utilizzo della Shell per configurare tutti i provider dell'elenco indirizzi IP consentiti

Per configurare in che modo il filtro connessioni utilizza tutti i provider dell'elenco indirizzi IP consentiti, utilizzare la sintassi seguente:
```powershell
    Set-IPAllowListProvidersConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]
```
Questo esempio consente di configurare tutti i provider dell'elenco indirizzi IP consentiti in modo da filtrare le connessioni in ingresso dai server di posta interni ed esterni. Per impostazione predefinita, le connessioni vengono filtrate unicamente dai server di posta esterni (il parametro *ExternalMailEnabled* è impostato su `$true` e il parametro *InternalMailEnabled* è impostato su `$false`). Le connessioni non autenticate e autenticate dai partner esterni vengono considerate esterne.

```powershell
Set-IPAllowListProvidersConfig -InternalMailEnabled $true
```

Per ulteriori informazioni, vedere [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/it-it/library/aa998543\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione di tutti i provider dell'elenco indirizzi IP consentiti, eseguire il seguente comando e verificare che i valori visualizzati siano quelli che erano stati configurati.
```powershell
    Get-IPAllowListProvidersConfig | Format-List *MailEnabled
```
## Utilizzo della Shell per visualizzare i provider dell'elenco indirizzi IP consentiti

Per visualizzare l'elenco di riepilogo di tutti i provider dell'elenco indirizzi IP consentiti, eseguire il seguente comando.

```powershell
Get-IPAllowListProvider
```

Per visualizzare i dettagli di un provider specifico, utilizzare la seguente sintassi.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity>
```

L'esempio seguente consente di visualizzare i dettagli del provider denominato Contoso IP Allow List Provider.
```powershell
    Get-IPAllowListProvider "Contoso IP Allow List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match
```
## Utilizzo della Shell per aggiungere un provider dell'elenco indirizzi IP consentiti

Per aggiungere un provider dell'elenco indirizzi IP consentiti, utilizzare la sintassi di seguito:
```powershell
    Add-IPAllowListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]
```
Questo esempio consente di creare un provider dell'elenco indirizzi IP consentiti denominato "Contoso IP Allow List Provider" con le seguenti opzioni:

  - **FQDN per l'utilizzo del porvider**   allow.contoso.com

  - **Codice maschera di bit che deve essere utilizzato dal provider**   127.0.0.1

<!-- end list -->
```powershell
    Add-IPAllowListProvider -Name "Contoso IP Allow List Provider" -LookupDomain allow.contoso.com -BitmaskMatch 127.0.0.1
```

> [!NOTE]
> Quando si aggiunge un nuovo provider dell'elenco indirizzi IP consentiti, questo viene abilitato per impostazione predefinita (il valore del parametro <EM>Enabled</EM> è <CODE>$true</CODE>), e il valore di priorità viene incrementato (la prima voce ha il valore <EM>Priority</EM> 1).



Per ulteriori informazioni, vedere [Add-IPBlockListProvider](https://technet.microsoft.com/it-it/library/bb124358\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che un provider dell'elenco indirizzi IP consentiti sia stato aggiunto correttamente, eseguire il seguente comando e verificare che il nuovo provider dell'elenco indirizzi IP consentiti sia visualizzato.

```powershell
Get-IPAllowListProvider
```

## Utilizzo della Shell per abilitare o disabilitare un provider dell'elenco indirizzi IP consentiti

Per abilitare o disabilitare uno specifico provider dell'elenco indirizzi IP consentiti, utilizzare la sintassi seguente.

```powershell
Set-IPAllowListProvider <IPAllowListProviderIdentity> -Enabled <$true | $false>
```

L'esempio seguente consente di disabilitare il provider denominato Contoso IP Allow List Provider.

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $false
```

L'esempio seguente consente di abilitare il provider denominato Contoso IP Allow List Provider.

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione del provider dell'elenco indirizzi IP consentiti, eseguire il seguente comando e verificare che il valore visualizzato sia il valore che era stato configurato.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List Enabled
```

## Utilizzo della Shell per configurare un provider dell'elenco indirizzi IP consentiti

Le opzioni di configurazione disponibili nel cmdlet **Set-IPAllowListProvider** sono identiche a quelle nel cmdlet **New-IPAllowListProvider**.

Per configurare un provider dell'elenco indirizzi IP consentiti esistente, utilizzare la sintassi di seguito:
```powershell
    Set-IPAllowListProvider <IPAllowListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]
```
Ad esempio, per aggiungere il codice di stato dell'indirizzo IP 127.0.0.1 all'elenco dei codici di stato esistenti per il provider denominato Contoso IP Allow List Provider, eseguire il seguente comando:

```powershell
Set-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddressesMatch @{Add="127.0.0.1"}
```

Per ulteriori informazioni, vedere [Set-IPBlockListProvider](https://technet.microsoft.com/it-it/library/bb124979\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione di un provider dell'elenco indirizzi IP consentiti, eseguire il seguente comando e verificare che i valori visualizzati siano quelli che erano stati configurati.

```powershell
Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List
```

## Utilizzo della Shell per verificare un provider dell'elenco indirizzi IP consentiti

Per verificare un provider dell'elenco indirizzi IP consentiti, utilizzare la sintassi di seguito:

```powershell
Test-IPAllowListProvider <IPAllowListProviderIdentity> -IPAddress <IPAddressToTest>
```

L'esempio seguente consente di verificare il provider denominato Contoso IP Allow List Provider cercando l'indirizzo IP 192.168.1.1.

```powershell
Test-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddress 192.168.1.1
```

## Utilizzo della Shell per rimuovere un provider dell'elenco indirizzi IP consentiti

Per rimuovere un provider dell'elenco indirizzi IP consentiti, utilizzare la sintassi di seguito:

```powershell
Remove-IPAllowListProvider <IPAllowListProviderIdentity>
```

L'esempio seguente consente di rimuovere il provider dell'elenco indirizzi IP consentiti denominato Contoso IP Allow List Provider.

```powershell
Remove-IPAllowListProvider "Contoso IP Allow List Provider"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che un provider dell'elenco indirizzi IP consentiti sia stato rimosso correttamente, eseguire il seguente comando e verificare che il provider dell'elenco indirizzi IP consentiti rimosso non sia più presente.

```powershell
Get-IPAllowListProvider
```

