---
title: "Gestisci aggregazione dell'elenco indirizzi attendibili: Exchange 2013 Help"
TOCTitle: Gestisci aggregazione dell'elenco indirizzi attendibili
ms:assetid: 5ac17168-f411-4cb7-ae98-ebefb865b210
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998280(v=EXCHG.150)
ms:contentKeyID: 50480677
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestisci aggregazione dell'elenco indirizzi attendibili

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

*Aggregazione dell'elenco indirizzi attendibili* fa riferimento a una funzionalità di protezione da posta indesiderata condivisa da Microsoft Outlook e Microsoft Exchange Server 2013. Questa funzionalità raccoglie i dati dagli elenchi Mittenti attendibili, elenchi Destinatari attendibili, elenchi Mittenti bloccati e i dati dei contatti configurati dagli utenti di Outlook e rende questi dati disponibili per gli agenti di protezione da posta indesiderata di Exchange. L'aggregazione dell'elenco indirizzi attendibili consente di ridurre le istanze di falsi positivi durante l'esecuzione del filtro di protezione dalla posta indesiderata da parte dei server di Exchange in cui sono in esecuzione gli agenti di protezione di posta indesiderata.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti

  - Sezione Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere"Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md) e sezione "Funzionalità di protezione da posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per impostazione predefinita le funzionalità di protezione da posta indesiderata non sono abilitate nel servizio di trasporto in un server Cassette postali. Le funzionalità di protezione da posta indesiderata in un server Cassette postali vengono solitamente abilitate se l'organizzazione di Exchange non prevede filtri preventivi di protezione da posta indesiderata prima di accettare i messaggi in arrivo. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Prestare attenzione al traffico di rete e di replica che potrebbe essere generato durante l'esecuzione del cmdlet **Update-SafeList**. Se il comando viene eseguito su più cassette postali in cui gli elenchi indirizzi attendibili vengono utilizzati in modo intensivo, è possibile che venga generata una quantità significativa di traffico. Se si esegue il comando su più cassette postali, è consigliabile effettuare l'operazione negli orari di scarso traffico e non di ufficio.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Configurazione dei limiti di raccolta dell'elenco indirizzi attendibili per le cassette postali tramite Shell

È possibile configurare il numero massimo di mittenti attendibili e mittenti bloccati configurabili per un utente. Per impostazione predefinita, gli utenti possono configurare fino a 5.000 mittenti attendibili e 500 mittenti bloccati.

Per configurare il numero massimo di mittenti attendibili e di mittenti bloccati, utilizzare il seguente comando:
```powershell
    Set-Mailbox <MailboxIdentity> -MaxSafeSenders <Integer> -MaxBlockedSenders <Integer>
```
In questo esempio, la cassetta postale john@contoso.com viene configurata per disporre di un massimo di 2.000 mittenti attendibili e 200 mittenti bloccati.

```powershell
Set-Mailbox john@contoso.com -MaxSafeSenders 2000 -MaxBlockedSenders 200
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver configurato con esito positivo i limiti di raccolta dell'elenco indirizzi attendibili, procedere come segue:

1.  Eseguire il comando indicato di seguito:
    ```powershell
        Get-Mailbox <Identity> | Format-List Name,Max*Senders
    ```
2.  Verificare che i valori visualizzati corrispondano a quelli configurati.

## Esecuzione del comando Update-Safelist tramite Shell

In Exchange 2013, l'aggregazione dell'elenco indirizzi attendibili viene effettuata automaticamente; quindi, non è necessario pianificare o eseguire manualmente il cmdlet **Update-Safelist**. Tuttavia, a volte potrebbe essere necessario eseguire questo cmdlet per verificare l'aggregazione dell'elenco indirizzi attendibili.

In questo esempio viene scritto l'elenco dei mittenti attendibili per la cassetta postale john@contoso.com su Active Directory.

```powershell
Update-Safelist john@contoso.com -Type SafeSenders
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Update-SafeList](https://technet.microsoft.com/it-it/library/bb125034\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare se l'operazione ha effettuato con successo la configurazione dell''aggregazione dell'elenco indirizzi attendibili, attenersi alla seguente procedura:

## Passaggio 1: Utilizzare Shell per verificare che l'agente filtro contenuti sia abilitato sul server Exchange

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
    Get-ContentFilterConfig | Format-List Enabled
    ```

2.  Se il parametro *Enabled* è impostato su `True`, il filtro del contenuto è abilitato. Se non lo è, utilizzare il seguente comando per abilitare il filtro contenuti e l'agente Filtro contenuti sul server Exchange:
    
    ```powershell
    Set-ContentFilterConfig -Enabled $true
    ```

## Passaggio 2: (Facoltativo) Utilizzare Modifica ADSI per verificare i dati dell'aggregazione dell'elenco indirizzi attendibili sui server Trasporto Edge

Questo passaggio è necessario se si esegue l'agente Filtro contenuti su un server Trasporto Edge nella rete perimetrale.

È possibile visualizzare gli oggetti utente nell'istanza Active Lightweight Directory Services (AD LDS) sul server Trasporto Edge per verificare che i dati di raccolta dell'elenco indirizzi attendibili siano aggiornati per gli oggetti utente e che il servizio Microsoft Exchange EdgeSync abbia replicato i dati sull'istanza AD LDS.

Esistono tre attributi di raccolta dell'elenco indirizzi attendibili per ogni oggetto utente:

  - **msExchSafeRecipientsHash**   Questo attributo memorizza il valore hash della raccolta degli elenchi Destinatari protetti per l'utente.

  - **msExchSafeSendersHash**   Questo attributo memorizza il valore hash della raccolta degli elenchi Mittenti protetti per l'utente.

  - **msExchBlockedSendersHash**   Questo attributo consente di memorizzare il valore hash della raccolta dell'elenco Mittenti bloccati per l'utente.

Se una stringa esadecimale, ad esempio `0xac 0xbd 0x03 0xca`, è presente nell'attributo, l'oggetto utente è stato aggiornato. Se presenta il valore `<Not Set>`, l'attributo non è stato aggiornato.

È possibile ricercare e visualizzare gli attributi utilizzando lo snap-in AD LDS Active Directory Service Interfaces (ADSI) Edit.

## Passaggio 3: Inviare un messaggio di prova per verificare che il funzionamento dell'aggregazione dell'elenco indirizzi attendibili stia funzionando

Per verificare se l'aggregazione dell'elenco indirizzi attendibili sta funzionando, è necessario che l'utente si faccia inviare un messaggio da un mittente attendibile che altrimenti verrebbe bloccato dal filtro contenuti. Se l'aggregazione degli elenchi indirizzi attendibili sta funzionando, il messaggio arriverà nella Posta in arrivo dell'utente.

1.  Trovare un account esterno di posta elettronica esistente da utilizzare oppure creare un account di posta elettronica gratuito con un provider basato su Web come Micosoft Hotmail.

2.  Aggiungere tale account all'elenco Mittenti attendibili di Microsoft Outlook.

3.  Il cmdlet **Update-SafeList** consente di ottenere la raccolta dell'elenco indirizzi attendibili dalla cassetta postale copiata in Active Directory.

4.  Facoltativo: Se si sta eseguendo l'agente Filtro contenuti su un server Trasporto Edge nella rete perimetrale, eseguire il cmdlet**Start-EdgeSynchronization** per forzare la replica EdgeSync.

5.  Aggiungere una parola specifica come frase bloccata alla configurazione del filtro contenuto. Per la procedura dettagliata, vedere [Gestire il filtro contenuto](manage-content-filtering-exchange-2013-help.md).

6.  Dall'account di posta elettronica esterno creato nel passo 1, inviare un messaggio alla cassetta postale di Exchange che includa la frase bloccato configurata nel passaggio 5.
    
    Se il messaggio viene recapitato con successo nella Posta in arrivo, l'aggregazione dell'elenco indirizzi attendibili sta funzionando correttamente.

