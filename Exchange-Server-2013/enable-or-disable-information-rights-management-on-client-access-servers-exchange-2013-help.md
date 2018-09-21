---
title: 'Attiva/disattiva IRM su server Accesso Client: Exchange 2013 Help'
TOCTitle: Attivare o disattivare Information Rights Management sui server Accesso Client
ms:assetid: c7ce069b-a572-4755-90a3-7105472e4c83
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876938(v=EXCHG.150)
ms:contentKeyID: 50481659
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attivare o disattivare Information Rights Management sui server Accesso Client

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

L'abilitazione di Information Rights Management (IRM) sui server Accesso client consente le seguenti funzionalità:

  - Microsoft Office Outlook Web App

  - IRM in Microsoft Exchange ActiveSync

Se IRM è abilitato sul server Accesso Client, gli utenti Outlook Web App possono protetto con IRM messaggi tramite l'applicazione di un modello di [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) creato nel cluster AD RMS. gli utenti Outlook Web App inoltre possono visualizzare i messaggi protetti tramite IRM e allegati è supportata. Prima di abilitare IRM sui server Accesso Client, è necessario aggiungere la cassetta postale di federazione al gruppo utenti con privilegi avanzati nel cluster AD RMS.


> [!IMPORTANT]
> Ai membri del gruppo di utenti con privilegi avanzati viene concessa una licenza d'uso con diritti di proprietario quando richiedono una licenza dal cluster AD&nbsp;RMS. Ciò consente al cluster di decrittografare tutto il contenuto protetto da RMS.



Per le attività di gestione aggiuntive correlate a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Configurazione di IRM (Information Rights Management)" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Un cluster AD RMS deve essere installato nella foresta di Active Directory.

  - La cassetta postale della federazione è stata aggiunta al gruppo di utenti con privilegi avanzati AD RMS. Per istruzioni dettagliate, vedere [Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Le funzionalità IRM devono essere abilitate per l'organizzazione. Per istruzioni dettagliate, vedere [Abilitazione o disabilitazione di IRM per i messaggi interni](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - Utilizzare il cmdlet **Set-IRMConfiguration** per abilitare o disabilitare IRM in Outlook Web App e IRM in Exchange ActiveSync per tutta l'organizzazione di Exchange o a livelli specifici.
    
    È possibile controllare IRM in Outlook Web App ai seguenti livelli:
    
      - **Directory virtuale di Outlook Web App**   Per abilitare o disabilitare IRM in Outlook Web App per una directory virtuale di Outlook Web App, utilizzare il cmdlet **Set-OWAVirtualDirectory** e impostare il parametro *IRMEnabled* su `$false` o `$true` (predefinito). Ciò consente di disabilitare IRM in Outlook Web App per una directory virtuale su un server Accesso client di Exchange 2013, tenendolo abilitato su un'altra directory virtuale su un diverso server Accesso client.
    
      - **Criteri cassetta postale per Outlook Web App**   Per abilitare o disabilitare IRM in Outlook Web App per i criteri delle cassette postali di Outlook Web App, usare il cmdlet **Set-OWAMailboxPolicy** e impostare il parametro *IRMEnabled* su `$false` o `$true` (predefinito). Ciò consente di abilitare IRM in Outlook Web App per un gruppo di utenti e disabilitarlo per un altro gruppo assegnando loro criteri di cassetta postale diversi per Outlook Web App.
    
    È possibile controllare IRM in Exchange ActiveSync per il criterio cassetta postale di Exchange ActiveSync. Per abilitare o disabilitare IRM in Exchange ActiveSync per un criterio cassetta postale di Exchange ActiveSync, utilizzare il cmdlet **Set-ActiveSyncMailboxPolicy** e impostare il parametro *IRMEnabled* su `$false` o su `$true` (impostazione predefinita). Ciò consente di abilitare IRM in Exchange ActiveSync per un gruppo di utenti e disabilitarlo per un altro gruppo assegnando loro criteri cassette postali diversi di Exchange ActiveSync.

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per abilitare o disabilitare IRM nei server Accesso client. È necessario utilizzare la shell.

## Operazione desiderata?

## Abilitazione di IRM sui server Accesso client tramite Shell

In questo esempio IRM viene abilitato su un server Accesso client di un'organizzazione di Exchange.

```powershell
Set-IRMConfiguration -ClientAccessServerEnabled $true
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Disabilitazione di IRM sui server Accesso client tramite Shell

In questo esempio IRM viene disabilitato su un server Accesso client di un'organizzazione di Exchange.

```powershell
Set-IRMConfiguration -ClientAccessServerEnabled $false
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver abilitato o disabilitato correttamente IRM nei server Accesso client, effettuare le operazioni seguenti:

  - Eseguire il cmdlet **Get-IRMConfiguration** e controllare il valore della proprietà *ClientAccessServerEnabled*.
    
    Per un esempio delle modalità di recupero della configurazione IRM, vedere [Examples](https://technet.microsoft.com/it-it/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) in **Get-IRMConfiguration**.

  - Utilizzare Outlook Web App per creare o leggere un messaggio protetto da IRM.

