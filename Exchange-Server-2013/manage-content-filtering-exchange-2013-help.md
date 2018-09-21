---
title: 'Gestire il filtro contenuto: Exchange 2013 Help'
TOCTitle: Gestire il filtro contenuto
ms:assetid: 05bd9d39-81dc-4514-8b75-7be386d5bcad
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa995953(v=EXCHG.150)
ms:contentKeyID: 50479934
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire il filtro contenuto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Il filtro contenuto è fornito dall'agente filtro contenuto. L'agente filtro contenuto filtra tutti i messaggi che giungono al server Exchange tramite tutti i connettori di ricezione. Sono filtrati solo i messaggi provenienti da origini non autenticate.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione da posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per impostazione predefinita le funzionalità di protezione da posta indesiderata non sono abilitate nel servizio di trasporto in un server Cassette postali. Le funzionalità di protezione da posta indesiderata in un server Cassette postali vengono solitamente abilitate se l'organizzazione di Exchange non prevede filtri preventivi di protezione da posta indesiderata prima di accettare i messaggi in arrivo. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione del filtro contenuto tramite Shell

Per disabilitare il filtro contenuto, eseguire il seguente comando:

```powershell
Set-ContentFilterConfig -Enabled $false
```

Per abilitare il filtro di contenuti, eseguire questo comando:

```powershell
Set-ContentFilterConfig -Enabled $true
```


> [!NOTE]
> Quando si disabilita il filtro contenuto, l'agente filtro contenuto sottostante è ancora abilitato. Per disabilitare l'agente filtro contenuto, eseguire il comando: <CODE>Disable-TransportAgent "Content Filter Agent"</CODE>.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione del filtro contenuto, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-ContentFilterConfig | Format-List Enabled
```

2.  Verificare il valore della proprietà *Enabled* visualizzata.

## Utilizzo di Shell per abilitare o disabilitare il filtro contenuto per i messaggi esterni

Per impostazione predefinita, la funzionalità relativa al filtro contenuto è abilitata per i messaggi esterni.

Per disabilitare il filtro contenuto per i messaggi esterni, eseguire il comando riportato di seguito:

```powershell
Set-ContentFilterConfig -ExternalMailEnabled $false
```

Per abilitare il filtro contenuto per i messaggi esterni, eseguire il comando riportato di seguito:

```powershell
Set-ContentFilterConfig -ExternalMailEnabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione del filtro contenuto per i messaggi esterni, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-ContentFilterConfig | Format-List ExternalMailEnabled
```

2.  Verificare il valore della proprietà *ExternalMailEnabled* visualizzata.

## Utilizzo di Shell per abilitare o disabilitare il filtro contenuto per i messaggi interni

Si consiglia di non filtrare i messaggi provenienti da partner attendibili o dall'interno dell'organizzazione. Quando si eseguono i filtri protezione da posta indesiderata, è sempre possibile che vengano individuati falsi positivi. Per ridurre la possibilità che i filtri gestiscano in modo errato i messaggi di posta elettronica sicuri, è necessario abilitare gli agenti protezione posta indesiderata in modo che vengano eseguiti solo sui messaggi provenienti da origini sconosciute o potenzialmente non attendibili.

Per abilitare il filtro contenuto per i messaggi interni, eseguire il comando riportato di seguito:

```powershell
Set-ContentFilterConfig -InternalMailEnabled $true
```

Per disabilitare il filtro contenuto per i messaggi interni, eseguire il comando riportato di seguito:

```powershell
Set-ContentFilterConfig -InternalMailEnabled $false
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta abilitazione o disabilitazione del filtro contenuto per i messaggi interni, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-ContentFilterConfig | Format-List InternalMailEnabled
```

2.  Verificare il valore della proprietà *InternalMailEnabled* visualizzata.

## Utilizzare la shell per configurare le eccezioni di mittente e destinatario

Per sostituire i valori esistenti, eseguire questo comando:

    Set-ContentFilterConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenders <sender1,sender2...> -BypassedSenderDomains <domain1,domain2...>

Questo esempio consente di configurare le seguenti eccezioni nel filtro contenuto:

  - I destinatari laura@contoso.com e julia@contoso.com non sono controllati dal filtro contenuto.

  - I mittenti steve@fabrikam.com e cindy@fabrikam.com non sono controllati dal filtro contenuto.

  - Tutti i mittenti nel dominio nwtraders.com e in tutti i sottodomini non sono controllati dal filtro contenuto.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients laura@contoso.com,julia@contoso.com -BypassedSenders steve@fabrikam.com,cindy@fabrikam.com -BypassedSenderDomains *.nwtraders.com

Per aggiungere o rimuovere le voci senza modificare i valori esistenti, eseguire questo comando:

    Set-ContentFilterConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

Questo esempio consente di configurare le seguenti eccezioni nel filtro contenuto:

  - Aggiungere tiffany@contoso.com e chris@contoso.com all'elenco dei destinatari esistenti che non vengono controllati dal filtro contenuto.

  - Aggiungere joe@fabrikam.com e michelle@fabrikam.com all'elenco dei destinatari esistenti che non vengono controllati dal filtro contenuto.

  - Aggiungere blueyonderairlines.com all'elenco dei domini esistenti i cui mittenti non sono controllati dal filtro contenuto.

  - Rimuovere il dominio woodgrovebank.com e tutti i sottodomini dall'elenco dei domini esistenti i cui mittenti non sono controllati dal filtro contenuto.

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients @{Add="tiffany@contoso.com","chris@contoso.com"} -BypassedSenders @{Add="joe@fabrikam.com","michelle@fabrikam.com"} -BypassedSenderDomains @{Add="blueyonderairlines.com"; Remove="*.woodgrovebank.com"}

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione delle eccezioni relative a destinatari e mittenti, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
        Get-ContentFilterConfig | Format-List Bypassed*

2.  Verificare che i valori visualizzati corrispondano alle impostazioni specificate.

## Utilizzare la shell per configurare le frasi consentite e bloccate

Per aggiungere frasi e parole consentite e bloccate, eseguire il seguente comando:

    Add-ContentFilterPhrase -Influence GoodWord -Phrase <Phrase> -Influence BadWord -Phrase <Phrase>

In questo esempio vengono autorizzati tutti i messaggi che contengono la frase "feedback dei clienti".

```powershell
Add-ContentFilterPhrase -Influence GoodWord -Phrase "customer feedback"
```

In questo esempio vengono bloccati tutti i messaggi che contengono la frase "suggerimento azioni".

```powershell
Add-ContentFilterPhrase -Influence BadWord -Phrase "stock tip"
```

Per rimuovere frasi consentite o bloccate, eseguire il seguente comando:

```powershell
Remove-ContentFilterPhrase -Phrase <Phrase>
```

In questo esempio viene rimossa la frase "suggerimento azioni":

```powershell
Remove-ContentFilterPhrase -Phrase "stock tip"
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione delle frasi consentite e bloccate, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-ContentFilterPhrase | Format-List Influence,Phrase
```

2.  Verificare che i valori visualizzati corrispondano alle impostazioni specificate.

## Utilizzare la shell per configurare le soglie SCL

Per configurare le soglie e le azioni del livello di probabilità di posta indesiderata (SCL), eseguire il seguente comando:

    Set-ContentFilterConfig -SCLDeleteEnabled <$true | $false> -SCLDeleteThreshold <Value> -SCLRejectEnabled <$true | $false> -SCLRejectThreshold <Value> -SCLQuarantineEnabled <$true | $false> -SCLQuarantineThreshold <Value>


> [!NOTE]
> L'azione di eliminazione ha precedenza sull'azione di rifiuto, che a sua volta ha precedenza sull'azione di quarantena. Quindi, la soglia del livello di probabilità di posta indesiderata per l'azione di eliminazione deve essere maggiore della soglia del livello di probabilità di posta indesiderata per l'azione di rifiuto, che a sua volta deve essere maggiore della soglia del livello di probabilità di posta indesiderata per l'azione di quarantena. Solo l'azione di rifiuto è abilitata per impostazione predefinita e presenta un valore di soglia del livello di probabilità di posta indesiderata pari a 7.



Questo esempio consente di configurare i seguenti valori per le soglie del livello di probabilità di posta indesiderata:

  - L'azione di eliminazione è abilitata e la corrispondente soglia del livello di probabilità di posta indesiderata è impostata su 9.

  - L'azione di rifiuto è abilitata e la corrispondente soglia del livello di probabilità di posta indesiderata è impostata su 8.

  - L'azione di quarantena è abilitata e la corrispondente soglia del livello di probabilità di posta indesiderata è impostata su 7.

<!-- end list -->

    Set-ContentFilterConfig -SCLDeleteEnabled $true -SCLDeleteThreshold 9 -SCLRejectEnabled $true -SCLRejectThreshold 8 -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione delle soglie del livello di probabilità di posta indesiderata, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
        Get-ContentFilterConfig | Format-List SCL*

2.  Verificare che i valori visualizzati corrispondano alle impostazioni specificate.

## Utilizzare la shell per configurare la risposta di rifiuto

Quando l'azione di rifiuto viene abilitata, è possibile personalizzare la risposta di rifiuto inviata al mittente del messaggio. La risposta di rifiuto non può superare i 240 caratteri.

Per configurare una risposta di rifiuto personalizzata, eseguire il comando seguente:

```powershell
Set-ContentFilterConfig -RejectionResponse "<Custom Text>"
```

In questo esempio l'agente filtro contenuto viene configurato per inviare una risposta di rifiuto personalizzata.

    Set-ContentFilterConfig -RejectionResponse "Your message was rejected because it appears to be SPAM."

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione della risposta di rifiuto, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
        Get-ContentFilterConfig | Format-List *Reject*

2.  Verificare che i valori visualizzati corrispondano alle impostazioni specificate.

## Abilitazione o disabilitazione del timbro posta elettronica Outlook tramite Shell

La convalida del *timbro posta elettronica Outlook* è una prova di calcolo che Microsoft Outlook applica ai messaggi in uscita per consentire ai sistemi di messaggistica dei destinatari di distinguere la posta elettronica legittima dalla posta indesiderata. Il timbro posta elettronica è disponibile in Outlook 2007 o versioni successive. La funzionalità di timbro aiuta a ridurre i falsi positivi. Il timbro posta elettronica Outlook è attivato per impostazione predefinita.

Per disabilitare il timbro posta elettronica Outlook, eseguire il comando riportato di seguito:

```powershell
Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $false
```

Per abilitare il timbro posta elettronica Outlook, eseguire il comando riportato di seguito:

```powershell
Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $true
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione del timbro posta elettronica Outlook, effettuare le seguenti operazioni:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
Get-ContentFilterConfig | Format-List OutlookEmailPostmarkValidationEnabled
```

2.  Verificare che il valore visualizzato corrisponda all'impostazione specificata.

