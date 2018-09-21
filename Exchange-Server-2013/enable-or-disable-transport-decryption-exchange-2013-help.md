---
title: 'Abilitare o disabilitare la decrittografia di trasporto: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare la decrittografia di trasporto
ms:assetid: 4663f54e-dd0a-4a42-983e-8765e2adc412
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638126(v=EXCHG.150)
ms:contentKeyID: 50480506
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare la decrittografia di trasporto

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Abilitazione la decrittografia di trasporto consente l'agente delle regole di trasporto in Microsoft Exchange Server 2013 server delle cassette postali per accedere al contenuto nei messaggi protetti da Information Rights Management (IRM). Di conseguenza, altri agenti di trasporto possono accedere a contenuto del messaggio ed eventualmente apportarvi modifiche. L'agente delle regole di trasporto, ad esempio, potrebbe essere necessario esaminare il contenuto del messaggio e applicare le regole di trasporto (ad esempio le regole che riguardano il messaggio una dichiarazione di non responsabilità). Per decrittografare correttamente i messaggi protetti tramite IRM, è necessario aggiungere la cassetta postale federata recapito per il gruppo di utenti con privilegi avanzati configurato sul server di [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) .


> [!IMPORTANT]
> Ai membri del gruppo di utenti con privilegi avanzati viene concessa una licenza d'uso con diritti di proprietario quando richiedono una licenza dal cluster AD&nbsp;RMS. Ciò consente loro di decrittografare tutto il contenuto protetto con RMS creato dal cluster AD&nbsp;RMS.



Quando si abilita la decrittografia di trasporto, è possibile specificare le impostazioni seguenti:

  - **Obbligatorio**    Rifiuta i messaggi che non possono essere decrittografati e restituisce un rapporto di mancato recapito (NDR) al mittente.

  - **Facoltativo**    Utilizza un approccio sforzo di decrittografia. Se possibile, i messaggi vengano decrittografati, ma sta recapitati anche se la decrittografia ha esito negativo. Questo è l'impostazione predefinita.

Per ulteriori informazioni sulla decrittografia di trasporto, vedere [Decrittografia di trasporto](transport-decryption-exchange-2013-help.md).

Per le attività di gestione aggiuntive correlate a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Protezione dei diritti" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Un server AD RMS è presente nella foresta di Active Directory ed è accessibile.

  - La cassetta postale di recapito federato è stato aggiunto al gruppo di utenti con privilegi avanzati AD RMS. Per ulteriori informazioni, vedere [Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - È possibile utilizzare l'interfaccia di amministrazione di Exchange (EAC) per abilitare la decrittografia di trasporto. È necessario utilizzare la Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Quale operazione si desidera effettuare?

## Utilizzo della Shell per abilitare la decrittografia di trasporto

In questo esempio viene abilitata la decrittografia di trasporto per l'organizzazione Exchange 2013. I messaggi che non possono essere decrittografati vengono rifiutati e al mittente viene restituito un rapporto di mancato Recapito.

```powershell
Set-IRMConfiguration -TransportDecryptionSetting Mandatory
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Utilizzo della Shell per disabilitare la decrittografia di trasporto

In questo esempio viene disabilitata la decrittografia di trasporto per l'organizzazione Exchange 2013.

```powershell
Set-IRMConfiguration -TransportDecryptionSetting Disabled
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che è stata abilitata o disabilitata la decrittografia di trasporto, utilizza il cmdlet **Get-IRMConfiguration** e verifica il valore della proprietà *JournalDecryptionEnabled* .

Per un esempio di come controllare la configurazione IRM, vedere [Examples](https://technet.microsoft.com/it-it/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) in **Get-IRMConfiguration**.

