---
title: 'Abilita/disabilita reg. cassetta postale controllo: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare la registrazione per una cassetta postale di controllo delle cassette postali
ms:assetid: c4bbfd52-6196-49c7-8c31-777fbbee11f2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff461937(v=EXCHG.150)
ms:contentKeyID: 50481610
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare la registrazione per una cassetta postale di controllo delle cassette postali

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-09-30_

Grazie alla registrazione di controllo delle cassette postali, è possibile tenere traccia degli accessi a una cassetta postale, nonché delle azioni effettuate dall'utente durante la connessione. Quando si abilita la registrazione di controllo per una cassetta postale, alcune azioni effettuate dagli amministratori e dai delegati vengono registrate per impostazione predefinita. Nessuna delle operazioni eseguite dal proprietario della cassetta postale viene registrata. Per ulteriori informazioni sulla registrazione di controllo delle cassette postali, vedere [Registrazione di controllo delle cassette postali](mailbox-audit-logging-exchange-2013-help.md).


> [!WARNING]
> Il controllo delle azioni del proprietario della cassetta postale può generare un numero elevato di voci nel log di controllo della cassetta postale che è quindi disabilitato per impostazione predefinita. È consigliabile abilitare solo il controllo di specifiche azioni del proprietario, necessarie per soddisfare i requisiti aziendali e di sicurezza.



Per altre attività relative alla registrazione di controllo delle cassette postali, vedere [Procedure di registrazione di controllo delle cassette postali](mailbox-audit-logging-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo delle cassette postali" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - È possibile utilizzare l'interfaccia di amministrazione di Exchange (EAC) per abilitare o disabilitare la cassetta postale di registrazione di controllo. È necessario utilizzare la Shell.

  - Un amministratore è stata assegnata l'autorizzazione accesso completo alla cassetta postale dell'utente viene considerato un utente delegato.

  - Cassette postali vengono considerate per accedere a un amministratore solo nei casi seguenti:
    
      - La funzionalità In-Place eDiscovery viene utilizzata per effettuare una ricerca in una cassetta postale.
    
      - Il cmdlet **New-MailboxExportRequest** viene utilizzato per esportare una cassetta postale.
    
      - Editor MAPI di Microsoft Exchange Server viene utilizzato per accedere alla cassetta postale.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Abilitazione o disabilitazione della registrazione di controllo delle cassette postali tramite Shell

È possibile utilizzare Shell per abilitare o disabilitare la registrazione di controllo per una cassetta postale. In questo modo viene abilitata o disabilitata la registrazione di tutte le operazioni specificate per amministratore, delegati e proprietario della cassetta postale.

In questo esempio la registrazione di controllo delle cassette postali viene abilitata per la cassetta postale di Ben Smith.
```powershell
    Set-Mailbox -Identity "Ben Smith" -AuditEnabled $true
```
In questo esempio la registrazione di controllo delle cassette postali viene disabilitata per la cassetta postale di Ben Smith.
```powershell
    Set-Mailbox -Identity "Ben Smith" -AuditEnabled $false
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Configurazione delle impostazioni della registrazione di controllo delle cassette postali per l'accesso di amministratori, delegati e proprietari tramite Shell

Quando viene abilitata la registrazione di controllo delle cassette postali per una cassetta postale, vengono registrate soltanto le azioni dell'amministratore, del delegato e del proprietario specificati nella configurazione della registrazione per la cassetta postale.

In questo esempio viene specificato che le azioni `SendAs` o `SendOnBehalf` eseguite dagli utenti delegati verranno registrate per la cassetta postale di Ben Smith.
```powershell
    Set-Mailbox -Identity "Ben Smith" -AuditDelegate SendAs,SendOnBehalf -AuditEnabled $true
```
In questo esempio viene specificato che le azioni `MessageBind` e `FolderBind` eseguite dagli amministratori verranno registrate per la cassetta postale di Ben Smith.
```powershell
    Set-Mailbox -Identity "Ben Smith" -AuditAdmin MessageBind,FolderBind -AuditEnabled $true
```
In questo esempio viene specificato che l'azione `HardDelete` eseguita dal proprietario della cassetta postale verrà registrata per la cassetta postale di Ben Smith.
```powershell
    Set-Mailbox -Identity "Ben Smith" -AuditOwner HardDelete -AuditEnabled $true
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver abilitato correttamente la registrazione di controllo delle cassette postali e specificato le impostazioni relative corrette per l'accesso di amministratori, delegati o proprietari, utilizzare il cmdlet [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) per recuperare le impostazioni della registrazione di controllo delle cassette postali per la cassetta postale in questione.

In questo esempio vengono recuperate le impostazioni della cassetta postale di Ben Smith e viene eseguito il pipelining delle impostazioni di controllo specificate, incluso il limite di validità del registro di controllo, nel cmdlet **Format-List**.
```powershell
    Get-Mailbox "Ben Smith" | Format-List *audit*
```
