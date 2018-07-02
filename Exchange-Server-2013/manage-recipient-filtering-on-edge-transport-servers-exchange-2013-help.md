---
title: 'Gestire il filtro destinatari nei server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Gestire il filtro destinatari nei server Trasporto Edge
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 50482031
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire il filtro destinatari nei server Trasporto Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Il filtro destinatario è fornito dall'agente filtro destinatario. Quando il filtro destinatario è abilitato su un server Exchange, vengono filtrati i messaggi in ingresso provenienti da Internet, che tuttavia non vengono autenticati. Questi messaggi vengono gestiti come messaggi esterni.


> [!NOTE]
> Anche se l'agente filtro destinatari è disponibile nei server Cassette postali, non deve essere configurato. Quando il filtro destinatari in un server Cassette postali rileva un destinatario non valido o bloccato in un messaggio contenente altri destinatari validi, il messaggio viene rifiutato. Se si installano agenti antispam in un server Cassette postali, l'agente filtro destinatari viene attivato per impostazione predefinita. Tuttavia, non è configurato per bloccare destinatari. Per ulteriori informazioni, vedere <A href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali</A>.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione da posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per impostazione predefinita le funzionalità di protezione da posta indesiderata non sono abilitate nel servizio di trasporto in un server Cassette postali. Le funzionalità di protezione da posta indesiderata in un server Cassette postali vengono solitamente abilitate se l'organizzazione di Exchange non prevede filtri preventivi di protezione da posta indesiderata prima di accettare i messaggi in arrivo. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Il parametro *AddressBookEnabled* del cmdlet **Set-AcceptedDomain** consente di abilitare o disabilitare il filtro destinatario per i destinatari in un dominio accettato. Per impostazione predefinita, il filtro destinatario è abilitato per i domini autorevoli e disabilitato per i domini di inoltro interni ed esterni. Per visualizzare lo stato del parametro *AddressBookEnabled* per i domini accettati dell'organizzazione, eseguire il comando riportato di seguito:
    
        Get-AcceptedDomain | Format-List Name,AddressBookEnabled

  - Se il filtro destinatario viene disabilitato utilizzando la procedura descritta in questo argomento, la funzionalità del filtro destinatario sarà disabilitata, ma l'agente filtro destinatario sottostante rimarrà abilitato.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione del filtro destinatari tramite Shell

Per disabilitare i filtri destinatario, eseguire il seguente comando:

    Set-RecipientFilterConfig -Enabled $false

Per abilitare il filtro destinatario, utilizzare il seguente comando:

    Set-RecipientFilterConfig -Enabled $true


> [!NOTE]
> Quando si disabilita il filtro destinatario, l'agente filtro destinatario sottostante rimane abilitato. Per disabilitare l'agente filtro destinatario, eseguire il comando riportato di seguito: <CODE>Disable-TransportAgent "Recipient Filter Agent"</CODE>.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare che il filtro destinatario sia stato abilitato o disabilitato correttamente, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    
        Get-RecipientFilterConfig | Format-List Enabled

2.  Verificare che il valore visualizzato sia quello configurato.

## Abilitazione o disabilitazione dell'elenco dei destinatari bloccati tramite Shell

Eseguire il comando indicato di seguito:

    Set-RecipientFilterConfig -BlockListEnabled <$true | $false>

In questo esempio viene abilitato l'elenco dei destinatari bloccati:

    Set-RecipientFilterConfig -BlockListEnabled $true

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'elenco dei destinatari bloccati sia stato abilitato o disabilitato correttamente, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    
        Get-RecipientFilterConfig | Format-List BlockListEnabled

2.  Verificare che il valore visualizzato sia quello configurato.

## Configurazione dell'elenco dei destinatari bloccati tramite Shell

Per sostituire i valori esistenti, eseguire questo comando:

    Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>

In questo esempio viene configurato l'elenco dei destinatari bloccati con valuesmark@contoso.com e kim@contoso.com:

    Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com

Per aggiungere o rimuovere le voci senza modificare i valori esistenti, eseguire questo comando:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

In questo esempio viene aggiunto chris@contoso.com e rimosso michelle@contoso.com nell'elenco nell'elemnco di destinatari bloccati:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'elenco dei destinatari bloccati sia stato configurato correttamente, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    
        Get-RecipientFilterConfig | Format-List BlockedRecipients

2.  Verificare che i valori visualizzati siano quelli configurati.

## Abilitazione o disabilitazione della ricerca dei destinatari tramite Shell

Eseguire il comando indicato di seguito:

    Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>

Per bloccare i messaggi per i destinatari non inclusi nell'organizzazione, utilizzare il seguente comando:

    Set-RecipientFilterConfig -RecipientValidationEnabled $true

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la ricerca dei destinatari sia stata abilitata o disabilitata correttamente, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    
        Get-RecipientFilterConfig | Format-List RecipientValidationEnabled

2.  Verificare che il valore visualizzato sia quello configurato.

