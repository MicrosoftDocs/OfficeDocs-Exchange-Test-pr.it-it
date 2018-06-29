---
title: 'Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali: Exchange 2013 Help'
TOCTitle: Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali
ms:assetid: 59d22c5e-64bc-4879-8ad1-364862b6ba11
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201691(v=EXCHG.150)
ms:contentKeyID: 50480720
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-01-23_

In Microsoft Exchange Server 2013, nel servizio di trasporto sui server Cassette postali sono disponibili, ma non installati per impostazione predefinita, i seguenti agenti di protezione da posta indesiderata:

  - Agente filtro contenuto

  - Agente ID mittente

  - Agente filtro mittente

  - Agente di analisi protocollo per reputazione mittente

Tuttavia, è possibile installare questi agenti su un server Cassette postali utilizzando uno script in Exchange Management Shell. Generalmente, gli agenti di protezione da posta indesiderata vengono installati su un server Cassette postali solo se l'organizzazione accetta tutta la posta in ingresso senza applicare preventivamente alcun filtro di protezione da posta indesiderata.


> [!NOTE]
> Anche se l'agente filtro destinatari è disponibile nei server Cassette postali, non deve essere configurato. Quando il filtro destinatari in un server Cassette postali rileva un destinatario non valido o bloccato in un messaggio contenente altri destinatari validi, il messaggio viene rifiutato. Anche se l'agente filtro destinatari viene attivato per impostazione predefinita, non è configurato per bloccare destinatari. Per ulteriori informazioni, vedere <A href="manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md">Gestire il filtro destinatari nei server Trasporto Edge</A>.



Può capitare, però, che gli agenti di protezione da posta indesiderata disponibili vengano installati nel servizio di trasporto su un server Cassette postali, ma che, prima di raggiungere il server Cassette postali, sul messaggio agiscano altri agenti di protezione da posta indesiderata di Exchange. È il caso, ad esempio, di una rete perimetrale in cui un server Trasporto Edge. Gli agenti di protezione da posta indesiderata sul server Cassette postali riconoscono i valori X-Header di protezione da posta indesiderata aggiunti ai messaggi da altri agenti di Exchange e i messaggi che contengono questi valori vengono lasciati passare senza essere nuovamente esaminati. Tuttavia, le ricerche dei destinatari da parte dell'agente Filtro destinatario vengono eseguite nuovamente sul server Cassette postali.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Configurazione di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Gli agenti Filtro connessioni e Filtro allegati non sono disponibili sui server Cassette postali. Sono disponibili solo sul server Trasporto Edge. Tuttavia, l'agente Malware è installato e abilitato per impostazione predefinita sul server Cassette postali. Per ulteriori informazioni, vedere [Protezione antimalware](anti-malware-protection-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Utilizzare Shell per eseguire lo script Install-AntispamAgents.ps1

Eseguire il comando indicato di seguito:

    & $env:ExchangeInstallPath\Scripts\Install-AntiSpamAgents.ps1

## Come verificare se l'operazione ha avuto esito positivo

Questa operazione è stata eseguita correttamente se lo script viene eseguito senza errori e chiede di riavviare il servizio di trasporto di Microsoft Exchange.

## Passaggio 2: Utilizzare Shell per riavviare il servizio di trasporto di Microsoft Exchange

Eseguire il comando indicato di seguito:

    Restart-Service MSExchangeTransport

## Come verificare se l'operazione ha avuto esito positivo

Questa operazione è stata eseguita correttamente se il servizio di trasporto di Microsoft Exchange viene riavviato senza errori.

## Passaggio 3: Utilizza Shell per specificare i server SMTP interni dell'organizzazione

È necessario specificare gli indirizzi IP degli eventuali server SMTP interni che devono essere ignorati dall'agente ID mittente. È necessario specificare l'indirizzo IP di almeno un server SMTP interno. Se il server Cassette postali su cui sono in esecuzione gli agenti di protezione da posta indesiderata è l'unico server SMTP dell'organizzazione, specificare l'indirizzo IP di quel computer.

Per aggiungere gli indirizzi IP dei server SMTP interni senza modificare i valori esistenti, utilizzare il seguente comando:

    Set-TransportConfig -InternalSMTPServers @{Add="<ip address1>","<ip address2>"...}

In questo esempio, gli indirizzi del server SMTP interno 10.0.1.10 e 10.0.1.11 vengono aggiunti alla configurazione di trasporto dell'organizzazione.

    Set-TransportConfig -InternalSMTPServers @{Add="10.0.1.10","10.0.1.11"}

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente specificato l'indirizzo IP di almeno un server SMTP interno, fare quanto segue:

1.  Eseguire il comando indicato di seguito:
    
        Get-TransportConfig | Format-List InternalSMTPServers

2.  Verificare che sia visualizzato l'indirizzo IP di almeno un server SMTP interno valido.

