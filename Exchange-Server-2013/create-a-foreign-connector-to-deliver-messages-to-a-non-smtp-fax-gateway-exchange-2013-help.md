---
title: 'Crea connett. est. recapito messaggi gateway fax non SMTP: Exchange 2013 Help'
TOCTitle: Creare un connettore esterno per il recapito di messaggi a un gateway fax non SMTP
ms:assetid: 589db487-3c4c-409a-92e3-c78dd8f639b6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ710163(v=EXCHG.150)
ms:contentKeyID: 50480711
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare un connettore esterno per il recapito di messaggi a un gateway fax non SMTP

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-17_

È possibile che si operi in uno scenario in cui si desidera inviare e ricevere messaggi di posta elettronica da un server gateway fax che non utilizza SMTP come meccanismo di trasporto principale. Seguire i passi di questa procedura per creare un connettore esterno che possa recapitare e ricevere i messaggi dal sistema esterno.


> [!TIP]
> Nella maggior parte dei casi in cui è necessario recapitare i messaggi in uscita a un sistema non SMTP, è consigliabile utilizzare i connettori agente di recapito perché, tra l'altro, consentono di gestire le code di messaggi e non è necessario scrivere i messaggi nel file system. Per ulteriori dettagli, vedere l'argomento <A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">Agenti di recapito e connettori agente di recapito</A>.



Ulteriori informazioni sugli scenari in cui si utilizza questa procedura Vedere i seguenti argomenti:

  - [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 30 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori esterni" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Utilizzare Shell per creare un connettore esterno che invii i messaggi a un server gateway non SMTP

1.  Utilizzare il seguente comando per creare il connettore esterno:
    
        New-ForeignConnector -Name "Contoso Foreign Connector" -AddressSpaces "X400:c=US;a=Fabrikam;P=Contoso;5" -SourceTransportServers Hub01,Hub02
    
    In questo esempio, Hub01 e Hub02 sono i server di origine nell'organizzazione scelti per recapitare i messaggi al sistema esterno. L'utilizzo di più server di origine determina la tolleranza di errore.

Una volta creato il connettore esterno, è possibile configurare le directory di destinazione, di prelievo e di riesecuzione, in base ai requisiti dell'organizzazione.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il connettore esterno sia stato creato correttamente, utilizzare il seguente comando:

```powershell
Get-ForeignConnector | Format-List Name
```

Verificare che sia visualizzato il nome del connettore esterno creato.

## Passaggio 2: Utilizzare Shell per configurare la directory di destinazione per un server Cassette postali su cui è in esecuzione il servizio di trasporto

La directory di destinazione per un server Cassette postali su cui è in esecuzione il servizio di trasporto viene utilizzata per recapitare i messaggi in uscita dal connettore esterno.

Creare una directory da utilizzare come directory di destinazione sul file system locale. È anche possibile utilizzare una directory su una condivisione file di rete.

1.  Utilizzare il seguente script per specificare la directory di destinazione per il connettore esterno (impostare il parametro *DropDirectory* sul percorso appropriato nel proprio ambiente):
    
    ```powershell
Set-ForeignConnector "Contoso Foreign Connector" -DropDirectory "C:\Drop Directory"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la directory di destinazione sia stata impostata correttamente, utilizzare il seguente script di cmdlet e controllare il valore del parametro *DropDirectory*:

```powershell
Get-ForeignConnector "Contoso Foreign Connector" | Format-List
```

Una volta creato il connettore esterno e specificata la directory di destinazione, è possibile inviare un messaggio utilizzando il server Cassette postali in cui è stato creato il connettore esterno e verificare che il file venga recapitato nella directory di destinazione.

## Passaggio 3: Utilizzare Shell per configurare la directory di prelievo per il servizio di trasporto su un server Cassette postali

La directory di prelievo per il servizio di trasporto su un server Cassette postali viene utilizzata per raccogliere i messaggi generati da sistemi non SMTP. Utilizzare questa procedura se si desidera raccogliere i messaggi generati da un sistema non SMTP, quale un server gateway fax, tramite il trasferimento file.

Per istruzioni dettagliate sulla configurazione della directory di prelievo, vedere [Configurare la directory di prelievo e la directory di riesecuzione](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la directory di prelievo sia stata impostata correttamente, utilizzare il seguente comando e controllare il valore del parametro *PickupDirectoryPath*:

```powershell
Get-TransportService | Format-List PickupDirectoryPath
```

## Passaggio 4: Utilizzare Shell per configurare la directory di riesecuzione per il servizio di trasporto su un server Cassette postali

La directory di riesecuzione per il servizio di trasporto su un server Cassette postali viene utilizzata per raccogliere i messaggi generati da sistemi non SMTP. Utilizzare questa procedura per configurare la directory di riesecuzione se si desidera reinviare i messaggi di posta elettronica, generalmente da un server gateway esterno non SMTP, generati nell'ambiente Exchange ed esportati dal trasporto Exchange.

Per istruzioni dettagliate sulla configurazione della directory di prelievo, vedere [Configurare la directory di prelievo e la directory di riesecuzione](configure-the-pickup-directory-and-the-replay-directory-exchange-2013-help.md).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la directory di riesecuzione sia stata impostata correttamente, utilizzare il seguente comando e controllare il valore del parametro *ReplayDirectoryPath*:

```powershell
Get-TransportService | Format-List ReplayDirectoryPath
```

## Ulteriori informazioni

[Connettori esterni](foreign-connectors-exchange-2013-help.md)

[Agenti di recapito e connettori agente di recapito](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

