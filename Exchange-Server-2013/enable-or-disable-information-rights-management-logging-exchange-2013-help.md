---
title: 'Abilita/disabilita registrazione IRM: Exchange 2013 Help'
TOCTitle: Enable or Disable Information Rights Management registrazione
ms:assetid: 6933bc65-4d98-4878-9167-0e9eaac68b6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff686962(v=EXCHG.150)
ms:contentKeyID: 50480871
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Enable or Disable Information Rights Management registrazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-12_

In Exchange Server 2013, è possibile utilizzare i registri di Information Rights Management (IRM) per monitorare le operazioni IRM e risolvere eventuali problemi. La registrazione IRM è abilitata per impostazione predefinita.

I log IRM utilizzano il seguente insieme comune di parametri:

  - *IrmLogEnabled*   Consente di abilitare o disabilitare la registrazione di IRM. Valore predefinito: `$true`.

  - *IrmLogMaxAge*   Specifica il limite massimo di validità dei file di log di IRM. I file precedenti al valore specificato vengono eliminati. Valore predefinito: 30 giorni.

  - *IrmLogMaxDirectorySize*   Specifica la dimensione massima della directory che contiene i log di IRM. Quando una directory raggiunge la dimensione massima dei file, il server elimina innanzitutto i file di log meno recenti. Valore predefinito: 250 MB.

  - *IrmLogMaxFileSize*   Specifica la dimensione massima di ciascun file di log di IRM. Quando un file di log raggiunge la dimensione specificata, ne viene creato uno nuovo. Valore predefinito: 10 MB.

  - *IrmLogPath*   Specifica il percorso della directory del log di IRM. Valore predefinito: `%ExchangeInstallPath%Logging\IRMLogs`.

Per le attività di gestione aggiuntive correlate a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 2-5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Configurazione della registrazione IRM" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per abilitare o disabilitare la registrazione IRM su un server. È necessario utilizzare Shell

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Abilitazione della registrazione IRM su un server tramite Shell

In questo esempio, la registrazione IRM viene abilitata su un server Cassette postali.

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-TransportService](https://technet.microsoft.com/it-it/library/jj215682\(v=exchg.150\)).

## Disbilitazione della registrazione IRM su un server tramite Shell

In questo esempio, la registrazione IRM viene disabilitata su un server Cassette postali.

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-TransportService](https://technet.microsoft.com/it-it/library/jj215682\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente abilitato o disabilitato la registrazione IRM su un server, eseguire il cmdlet [Get-TransportService](https://technet.microsoft.com/it-it/library/jj215746\(v=exchg.150\)) per visualizzare le impostazioni IRM.

In questo esempio vengono visualizzare tutte le proprietà di registrazione IRM sul server EXCH01.

    Get-TransportService -Identity EXCH01 | Format-List IRMLog*

