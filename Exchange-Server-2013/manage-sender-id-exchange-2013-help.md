---
title: "Gestione dell'ID mittente: Exchange 2013 Help"
TOCTitle: Gestione dell'ID mittente
ms:assetid: 2e7b646a-8a66-4be7-a7c1-0bd43bb79a5b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997136(v=EXCHG.150)
ms:contentKeyID: 50480255
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione dell'ID mittente

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

La funzionalità deIl'ID mittente è fornita dall'agente dell'ID mittente. L'ID mittente consente di convalidare l'origine dei messaggi di posta elettronica verificando l'indirizzo IP del mittente in base al proprietario del dominio del mittente. Il filtro dell'ID mittente viene eseguito sui messaggi in entrata che provengono da Internet ma non sono autenticati. Questi messaggi vengono gestiti come messaggi esterni.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione da posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per impostazione predefinita le funzionalità di protezione da posta indesiderata non sono abilitate nel servizio di trasporto in un server Cassette postali. Le funzionalità di protezione da posta indesiderata in un server Cassette postali vengono solitamente abilitate se l'organizzazione di Exchange non prevede filtri preventivi di protezione da posta indesiderata prima di accettare i messaggi in arrivo. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione dell'ID mittente tramite Shell

Per disabilitare l'ID mittente, eseguire il comando riportato di seguito:

```powershell
Set-SenderIDConfig -Enabled $false
```

Per abilitare l'ID mittente, eseguire il comando riportato di seguito:

```powershell
Set-SenderIDConfig -Enabled $true
```


> [!NOTE]
> Quando si disabilita l'ID mittente, l'agente dell'ID mittente è ancora attivato. Per disabilitare l'agente dell'ID mittente, eseguire il comando: <CODE>Disable-TransportAgent "Sender ID Agent"</CODE>.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'ID mittente sia stato abilitato o disabilitato con successo, fare quanto segue:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-SenderIDConfig | Format-List Enabled
```

2.  Verificare che il valore visualizzato sia quello configurato.

## UtilizzareShell per configurare le azioni dell'ID mittente per i messaggi falsificati

Per configurare l'azione dell'ID mittente per i messaggi falsificati, utilizzare il seguente comando:

```powershell
Set-SenderIDConfig -SpoofedDomainAction <StampStatus | Reject | Delete>
```

Questo esempio configura l'agente dell'ID mittente per rifiutare tutti i messaggi in cui l'indirizzo IP del server di invio non è elencato come un server mittente SMTP autorevole nel record SPF del DNS per il dominio specificato.

```powershell
Set-SenderIDConfig -SpoofedDomainAction Reject
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'ID mittente sia stato configurato con successo per i messaggi falsificati, fare quanto segue:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-SenderIDConfig | Format-List SpoofedDomainAction
```

2.  Verificare che il valore visualizzato sia quello configurato.

## Utilizzo di Shell per configurare le azioni dell'ID mittente per gli errori temporanei

Per configurare l'azione dell'ID mittente per gli errori temporanei, utilizzare il seguente comando:

```powershell
Set-SenderIDConfig -TempErrorAction <StampStatus | Reject | Delete>
```

In questo esempio l'agente ID mittente viene configurato per contrassegnare i messaggi per cui non è possibile determinare lo stato dell'ID mittente a causa di un errore temporaneo del server DNS. Il messaggio sarà elaborato da altri agenti di posta indesiderata e l'agente Filtro contenuto utilizzerà il contrassegno per determinare il valore SCL per il messaggio.

```powershell
Set-SenderIDConfig -TempErrorAction StampStatus
```

Si noti che `StampStatus` è il valore predefinito per il parametro *TempErrorAction*.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'ID mittente sia stato configurato con successo per gli errori temporanei fare quanto segue:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-SenderIDConfig | Format-List TempErrorAction
```

2.  Verificare che il valore visualizzato sia quello configurato.

## Utilizzare la shell per configurare le eccezioni di dominio del mittente e del destinatario

Per sostituire i valori esistenti, eseguire questo comando:

    Set-SenderIDConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenderDomains <domain1,domain2...>

Questo esempio configura l'agente dell'ID mittente per ignorare il controllo dell'ID mittente per i messaggi inviati a kim@contoso.com e john@contoso.com e per ignorare il controllo dell'ID mittente per i messaggi inviati dal dominio fabrikam.com.

    Set-SenderIDConfig -BypassedRecipients kim@contoso.com,john@contoso.com -BypassedSenderDomains fabrikam.com

Per aggiungere o rimuovere le voci senza modificare i valori esistenti, eseguire questo comando:

    Set-SenderIDConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Questo esempio consente di configurare l'agente ID mittente con le seguenti informazioni:

  - Aggiungere chris@contoso.com e michelle@contoso.com all'elenco dei destinatari esistenti che ignorano il controllo dell'ID mittente.

  - Eliminare tailspintoys.com dall'elenco dei domini esistenti che ignorano il controllo dell'ID mittente.

<!-- end list -->

    Set-SenderIDConfig -BypassedRecipients @{Add="chris@contoso.com","michelle@contoso.com"} -BypassedSenderDomains @{Remove="tailspintoys.com"}

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che le eccezioni del dominio del mittente e del destinarlo siano state configurate con successo, fare quanto segue:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-SenderIDConfig | Format-List BypassedRecipients,BypassedSenderDomains
```

2.  Verificare che i valori visualizzati siano quelli configurati.

