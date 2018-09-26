---
title: 'Gestire imp. mess. unificata su server Accesso Client: Exchange 2013 Help'
TOCTitle: Gestire le impostazioni di messaggistica unificata su un server Accesso Client
ms:assetid: 08667911-fa86-404e-84b1-65cedd94d579
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673507(v=EXCHG.150)
ms:contentKeyID: 50555535
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire le impostazioni di messaggistica unificata su un server Accesso Client

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-09_

Dopo aver installato un server Accesso client su cui è in esecuzione il servizio Router delle chiamate di messaggistica unificata di Microsoft Exchange, è possibile configurare diverse opzioni tra cui il numero di chiamate contemporanee, le porte di ascolto TCP e TLS, lo stato e la modalità di avvio.


> [!NOTE]
> Non è necessario che i server Accesso client vengano aggiunti a un dial plan di messaggistica unificata prima di poter elaborare le chiamate per la messaggistica unificata, a meno che non si stia integrando la messaggistica unificata e Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. Per impostazione predefinita, tutti i server Accesso client nell'organizzazione sono disponibili per rispondere alle chiamate.



Per informazioni sulle altre attività relative ai server Accesso client e alla messaggistica unificata, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Informazioni necessarie prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Accesso client (servizio di routing delle chiamate di messaggistica unificata)" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare che il server Accesso client sia installato nello stesso computer del server Cassette postali o su un altro computer.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Configurazione delle proprietà della messaggistica unificata su un server Accesso client tramite Shell

In questo esempio, il server Accesso client denominato `MyClientAccessServer` viene rimosso da tutti i dial plan SIP.

```powershell
Set-UMCallRouterSettings -DialPlans $null - Server MyClientAccessServer
```

In questo esempio viene aggiunto un server Accesso client denominato `MyClientAccessServer` a un dial plan SIP denominato `MySIPDialPlan` e viene impostato il numero massimo di chiamate vocali in ingresso.

```powershell
Set-UMCallRouterSettings -DialPlans MySIPDialPlan -MaxCalls 150 -Server MyClientAccessServer
```

In questo esempio la porta di ascolto TCP SIP viene impostata su 5077 e la modalità di avvio su Doppio su un server Accesso client denominato `MyClientAccessServer`.
```powershell
    Set-UMCallRouterSettings  -Server MyClientAccessServer-SipTCPListeningPort 5077 -UMStartUpMode -Dual 
```
## Visualizzazione delle proprietà del server Accesso client tramite Shell

In questo esempio viene visualizzato un elenco di tutti i server Accesso client.

```powershell
Get-UMCallRouterSettings
```

In questo esempio viene visualizzato un elenco formattato delle proprietà per il server Accesso client.

```powershell
Get-UMCallRouterSettings | Format-List
```

