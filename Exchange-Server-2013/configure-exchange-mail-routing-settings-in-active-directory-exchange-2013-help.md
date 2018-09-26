---
title: 'Config. imp. routing posta Exchange-Active Directory: Exchange 2013 Help'
TOCTitle: Configurare impostazioni di routing della posta di Exchange in Active Directory
ms:assetid: d01f8545-c201-4a96-be39-ed4c7008afcf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ674705(v=EXCHG.150)
ms:contentKeyID: 50481709
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare impostazioni di routing della posta di Exchange in Active Directory

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Per impostazione predefinita Microsoft Exchange Server 2013 fa riferimento agli oggetti collegamento del sito IP in Active Directory per facilitare la determinazione del percorso di routing più conveniente. Se tuttavia si ritiene che i costi del collegamento del sito IP di Active Directory e i modelli di flusso di traffico non siano ottimali per il routing della posta in Exchange, è possibile configurare le impostazioni in Active Directory che verranno utilizzate soltanto da Exchange per ottimizzare il flusso della posta.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Sito di Active Directory e gestione del collegamento al sito" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Configurazione di un costo specifico di Exchange su un collegamento del sito IP di Active Directory tramite Shell

Determinare il nome del collegamento del sito IP di Active Directory per cui si desidera impostare un costo di Exchange. Un costo inferiore indica una route preferibile. È possibile esaminare il contenuto dei registri della tabella di routing e visualizzare i dati nella sezione **ADTopologyPath ID** per visualizzare i dettagli sul percorso di routing meno costoso calcolato tra due siti di Active Directory.

Per impostare un costo specifico per Exchange in un collegamento del sito di Active Directory, eseguire il comando riportato di seguito:

```powershell 
 Set-AdSiteLink <ADSiteLinkIdentity> -ExchangeCost <Integer | $null>
```

Con questo esempio viene impostato un costo specifico di Exchange pari a 10 per il collegamento del sito IP denominato IPSiteLinkAB.

```powershell
Set-AdSiteLink IPSiteLinkAB -ExchangeCost 10
```

Con questo esempio viene eliminato il costo specifico di Exchange dal collegamento del sito IP denominato IPSiteLinkAB.

```powershell
Set-AdSiteLink IPSiteLinkAB -ExchangeCost $null
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare l'impostazione corretta del costo per Exchange su un collegamento del sito di Active Directory, effettuare le operazioni seguenti:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
    Get-AdSiteLink | Format-List Name,ExchangeCost
    ```

2.  Verificare che il costo di Exchange sia configurato sul collegamento del sito di Active Directory.

## Configurazione di un sito di Active Directory come sito hub tramite Shell

Se il sito hub è presente lungo il percorso di routing più conveniente, il messaggio deve essere instradato attraverso il sito hub. Esaminare il contenuto dei registri della tabella di routing e visualizzare i dati nella sezione **ADTopologyPath ID** per verificare l'esistenza del sito selezionato lungo il percorso di routing più conveniente tra due siti di Active Directory. Se il risultato è negativo, è necessario assegnare costi specifici per Exchange ai collegamenti del sito IP per stabilire il percorso di routing più conveniente tra i siti selezionati.

Per configurare un sito di Active Directory come sito hub, eseguire il comando riportato di seguito:

```powershell
Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true
```

Con questo esempio il sito di Active Directory denominato Site A viene configurato come sito hub.

```powershell
Set-AdSite "Site A" -HubSiteEnabled $true
```

Con questo esempio viene rimosso l'attributo del sito hub dal sito di Active Directory denominato Site B.

```powershell
Set-AdSite "Site B" -HubSiteEnabled $false
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la configurazione corretta di un sito di Active Directory come sito hub, effettuare le operazioni seguenti:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
    Get-AdSite | Format-List Name,HubSiteEnabled
    ```

2.  Verificare che il valore *HubSiteEnabled* sia `True` per il sito di Active Directory.

