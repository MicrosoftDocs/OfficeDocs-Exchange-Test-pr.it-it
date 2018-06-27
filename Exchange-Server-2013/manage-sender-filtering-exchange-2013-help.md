---
title: 'Gestire il filtro mittente: Exchange 2013 Help'
TOCTitle: Gestire il filtro mittente
ms:assetid: a7f4b3e1-2970-45ad-911e-a9f46d880d3d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124087(v=EXCHG.150)
ms:contentKeyID: 50481387
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire il filtro mittente

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-08_

Il filtro mittente è fornito dall'agente filtro mittente. L'agente Filtro mittente si basa sull'intestazione **MAIL FROM:** Intestazione SMTP per determinare l'eventuale azione da intraprendere per un messaggio di posta elettronica in ingresso.

Quando è abilitata su un server di Exchange, la funzionalità del filtro mittente filtra tutti i messaggi che passano attraverso i connettori di ricezione di quel computer.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione da posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per impostazione predefinita le funzionalità di protezione da posta indesiderata non sono abilitate nel servizio di trasporto in un server Cassette postali. Le funzionalità di protezione da posta indesiderata in un server Cassette postali vengono solitamente abilitate se l'organizzazione di Exchange non prevede filtri preventivi di protezione da posta indesiderata prima di accettare i messaggi in arrivo. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare Shell per abilitare o disabilitare il filtro mittente

Per abilitare il filtro mittenti, eseguire il seguente comando:

    Set-SenderFilterConfig -Enabled $false

Per abilitare il filtro mittente, eseguire il seguente comando:

    Set-SenderFilterConfig -Enabled $true


> [!NOTE]
> Se si disabilita il filtro mittente, l'agente Filtro mittente sottostante è ancora abilitato. Per disabilitare l'agente Filtro mittente, eseguire il comando riportato di seguito: <CODE>Disable-TransportAgent "Sender Filter Agent"</CODE>.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione del filtro mittente, attenersi alla procedura seguente:

1.  Eseguire il comando indicato di seguito:
    
        Get-SenderFilterConfig | Format-List Enabled

2.  Verificare che il valore visualizzato sia quello configurato.

## Utilizzare Shell per configurare i domini e i mittenti bloccati

Per sostituire i valori esistenti, eseguire questo comando:

    Set-SenderFilterConfig -BlockedSenders <sender1,sender2...> -BlockedDomains <domain1,domain2...> -BlockedDomainsAndSubdomains <domain1,domain2...>

In questo esempio l'agente Filtro mittente viene configurato per bloccare i messaggi da kim@contoso.com e john@contoso.com, i messaggi dal dominio fabrikam.com e i messaggi da northwindtraders.com e tutti i relativi sottodomini.

    Set-SenderFilterConfig -BlockedSenders kim@contoso.com,john@contoso.com -BlockedDomains fabrikam.com -BlockedDomainsAndSubdomains northwindtraders.com

Per aggiungere o rimuovere le voci senza modificare i valori esistenti, eseguire questo comando:

    Set-SenderFilterConfig -BlockedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BlockedDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...} -BlockedDomainsAndSubdomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

In questo esempio l'agente Filtro mittente viene configurato con le seguenti informazioni:

  - Aggiunta di chris@contoso.com e michelle@contoso.com all'elenco dei mittenti esistenti bloccati.

  - Rimozione di tailspintoys.com dall'elenco dei domini mittente esistenti bloccati.

  - Aggiunta di blueyonderairlines.com all'elenco dei domini e sottodomini mittente esistenti bloccati.

<!-- end list -->

    Set-SenderFilterConfig -BlockedSenders @{Add="chris@contoso.com","michelle@contoso.com"} -BlockedDomains @{Remove="tailspintoys.com"} -BlockedDomainsAndSubdomains @{Add="blueyonderairlines.com"}

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione dei mittenti bloccati, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    
        Get-SenderFilterConfig | Format-List BlockedSenders,BlockedDomains,BlockedDomainsAndSubdomains

2.  Verificare che i valori visualizzati siano quelli configurati.

## Utilizzare Shell per abilitare o disabilitare il blocco dei messaggi con mittenti vuoti

Per abilitare o disabilitare il blocco dei messaggi con mittenti vuoti, eseguire il seguente comando:

    Set-SenderFilterConfig -BlankSenderBlockingenabled <$true | $false>

In questo esempio l'agente Filtro mittente viene configurato per bloccare i messaggi in cui non viene specificato un mittente nel comando SMTP MAIL FROM:

    Set-SenderFilterConfig -BlankSenderBlockingEnabled $true

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione del blocco dei messaggi con mittenti vuoti, attenersi alla procedura seguente:

1.  Eseguire il comando indicato di seguito:
    
        Get-SenderFilterConfig | Format-List BlankSenderBlockingEnabled

2.  Verificare che il valore visualizzato sia quello configurato.

