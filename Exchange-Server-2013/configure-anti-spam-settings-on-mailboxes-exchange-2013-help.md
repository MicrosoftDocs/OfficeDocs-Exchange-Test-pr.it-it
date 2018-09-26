---
title: 'Config. imp. protez. posta indes. cassette postali: Exchange 2013 Help'
TOCTitle: Configurare le impostazioni di protezione da posta indesiderata per cassette postali
ms:assetid: 868d7fd8-e817-46ba-9b67-edf2f50b9494
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123559(v=EXCHG.150)
ms:contentKeyID: 50481089
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le impostazioni di protezione da posta indesiderata per cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-11-17_

È possibile configurare su singole cassette postali impostazioni di protezione dalla posta indesiderata specifiche e diverse dalle impostazioni di protezione dalla posta indesiderata applicate alle altre cassette postali nell'organizzazione di Exchange. Quando si configura un'impostazione di protezione dalla posta indesiderata su una cassetta postale, tale impostazione sostituisce l'impostazione di protezione dalla posta indesiderata configurata per l'organizzazione o l'impostazione di filtraggio del contenuto a livello di organizzazione.


> [!NOTE]
> Dal 1° novembre 2016, Microsoft ha interrotto gli aggiornamenti delle definizioni spam per i filtri SmartScreen in Exchange e Outlook. Le definizioni spam SmartScreen esistenti non verranno eliminate, ma la loro efficacia si ridurrà progressivamente. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Deprecating support for SmartScreen in Outlook and Exchange (Eliminazione del supporto per SmartScreen in Outlook ed Exchange)</A>.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Funzionalità di protezione dalla posta indesiderata" nell'argomento [Autorizzazioni di protezione da posta indesiderata e antimalware](anti-spam-and-anti-malware-permissions-exchange-2013-help.md) e "Protezione dalla posta indesiderata" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per impostazione predefinita le funzionalità di protezione da posta indesiderata non sono abilitate nel servizio di trasporto in un server Cassette postali. Le funzionalità di protezione da posta indesiderata in un server Cassette postali vengono solitamente abilitate se l'organizzazione di Exchange non prevede filtri preventivi di protezione da posta indesiderata prima di accettare i messaggi in arrivo. Per ulteriori informazioni, vedere [Attivare la funzionalità di protezione dalla posta indesiderata sui server cassette postali](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Il valore di soglia del livello di probabilità di posta indesiderata per la cartella Posta indesiderata si comporta in maniera diversa rispetto ai valori di eliminazione, rifiuto e messa in quarantena di SCL. Per ulteriori informazioni, vedere [Soglia del livello di probabilità di posta indesiderata](spam-confidence-level-threshold-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo di Shell per configurare le funzionalità di protezione da posta indesiderata su una singola cassetta postale

Per configurare le impostazioni di protezione dalla posta indesiderata su una singola cassetta postale, utilizzare la seguente sintassi.
```powershell
    Set-Mailbox <MailboxIdentity> -AntispamBypassEnabled <$true | $false> -RequireSenderAuthenticationEnabled <$true | $false> -SCLDeleteEnabled <$true | $false | $null> -SCLDeleteThreshold <0-9 | $null> -SCLJunkEnabled <$true | $false | $null > -SCLJunkThreshold <0-9 | $null> -SCLQuarantineEnabled <$true | $false | $null > -SCLQuarantineThreshold <0-9 | $null> -SCLRejectEnabled <$true | $false | $null > -SCLRejectThreshold <0-9 | $null>
```

In questo esempio la cassetta postale dell'utente Jeff Phillips viene configurata per ignorare tutti i filtri di protezione dalla posta indesiderata e per ottenere il recapito nella sua cartella Posta indesiderata in Microsoft Outlook dei messaggi che corrispondono o superano la soglia 5 del livello di probabilità di posta indesiderata per la cartella Posta indesiderata.

```powershell
Set-Mailbox "Jeff Phillips" -AntispamBypassEnabled $true -SCLJunkEnabled $true -SCLJunkThreshold 4
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione delle funzionalità di protezione dalla posta indesiderata su una singola cassetta postale, attenersi alla procedura seguente:

1.  Eseguire il comando indicato di seguito:
    ```powershell
        Get-Mailbox <MailboxIdentity> | Format-List SCL*,Bypass*,*SenderAuth*
    ```

2.  Verificare che il valore visualizzato sia quello configurato.

## Utilizzare Shell per configurare le funzionalità di protezione dalla posta indesiderata per più cassette postali

Per configurare tutte le impostazioni di protezione dalla posta indesiderata su più cassette postali, utilizzare la seguente sintassi.
```powershell
    Get-Mailbox [<Filter>]| Set-Mailbox <Anti-Spam Settings>
```

In questo esempio viene abilitata la soglia di quarantena SCL con un valore pari a 7 in tutte le cassette postali nel contenitore Utenti del dominio Contoso.com.
```powershell
    Get-Mailbox -OrganizationalUnit Contoso.com/Users | Set-Mailbox -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7
````

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione delle funzionalità di protezione dalla posta indesiderata su più cassette postali, attenersi alla procedura seguente:

1.  Eseguire il comando indicato di seguito:
    ```powershell
        Get-Mailbox [<Filter>] | Format-List Name,SCL*,*SenderAuth*
    ```
2.  Verificare che i valori visualizzati siano quelli configurati.

## Utilizzare Shell per configurare la soglia di posta indesiderata per tutte le cassette postali della propria organizzazione

Eseguire il comando indicato di seguito:

```powershell
Set-OrganizationConfig -SCLJunkThreshold <Integer>
```

In questo la soglia di posta indesiderata dell'organizzazione viene impostata su 5.

```powershell
Set-OrganizationConfig -SCLJunkThreshold 5
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione della soglia di posta indesiderata per tutte le cassette postali nell'organizzazione, attenersi alla procedura seguente:

1.  Eseguire il comando indicato di seguito:
    
    ```powershell
        Get-OrganizationConfig | Format-List SCLJunkThreshold
    ```

2.  Verificare che il valore visualizzato sia quello configurato.

