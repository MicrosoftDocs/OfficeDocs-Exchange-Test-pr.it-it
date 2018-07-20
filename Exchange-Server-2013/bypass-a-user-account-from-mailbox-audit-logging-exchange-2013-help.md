---
title: 'Bypass di un account utente dal controllo delle cassette postali registrazione: Exchange 2013 Help'
TOCTitle: Bypass di un account utente dal controllo delle cassette postali registrazione
ms:assetid: 98a87071-fe31-4b67-beb8-a73799e54df2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff461934(v=EXCHG.150)
ms:contentKeyID: 50481257
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Bypass di un account utente dal controllo delle cassette postali registrazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-05-21_

Quando si abilita la registrazione dei controlli in una cassetta postale, determinati eventi di accesso che interessano la cassetta postale (ad esempio, l'accesso a una cartella o un messaggio oppure l'eliminazione permanente di un messaggio) vengono registrati. È però necessario tenere presente che gli accessi eseguiti da alcuni account autorizzati (ad esempio, quelli utilizzati da strumenti di terzi o per il monitoraggio a fini legali) potrebbero creare un numero notevole di voci nel registro di controllo e tuttavia non essere di alcun interesse per l'organizzazione.

È possibile configurare un utente o un account in modo che ignori la registrazione dei controlli della cassetta postale; ciò significa che le azioni intraprese da quell'utente o da quell'account su una qualsiasi cassetta postale non verranno registrate. Se si escludono gli utenti e gli account attendibili che devono accedere spesso alle cassette postali, i registri di controllo delle cassette postali risulteranno più chiari.


> [!WARNING]
> Se si utilizza la registrazione dei controlli delle cassette postali per controllare azioni e accessi alle cassette postali, è necessario monitorare regolarmente le associazioni che vengono a crearsi a seguito dell'esclusione di determinati account o utenti da questi controlli. Se si sceglie di escludere un account dal controllo, questo account potrà accedere a qualunque cassetta postale nell'organizzazione, a patto che disponga delle autorizzazioni necessarie, e gli accessi o le azioni intraprese (ad esempio, l'eliminazione dei messaggi) non creeranno alcuna voce nel registro di controllo.



Per altre attività di gestione relative alla registrazione di controllo delle cassette postali, vedere [Procedure di registrazione di controllo delle cassette postali](mailbox-audit-logging-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo delle cassette postali" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Se si imposta la registrazione dei controlli di una cassetta postale in modo che ignori un account, tutti gli accessi effettuati da questo account su qualsiasi cassetta postale non verranno registrati. Non è possibile configurare un account in modo che la registrazione ignori i suoi accessi a una singola cassetta postale.

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange (EAC) per abilitare o disabilitare l'esclusione di un account dalla registrazione dei controlli delle cassette postali. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare Shell per abilitare o disabilitare l'esclusione di un account dalla registrazione dei controlli delle cassette postali

Per un esempio relativo alla modalità di abilitazione del bypass per la registrazione di controllo della cassetta postale per un account, vedere [Examples](https://technet.microsoft.com/it-it/ff696758\(exchg.150\)#examples) in [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/it-it/library/ff696758\(v=exchg.150\)).

Per un esempio relativo alla modalità di disabilitazione del bypass per la registrazione di controllo della cassetta postale per un account, vedere [Examples](https://technet.microsoft.com/it-it/ff696758\(exchg.150\)#examples) in [Set-MailboxAuditBypassAssociation](https://technet.microsoft.com/it-it/library/ff696758\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Dopo aver escluso un account utente dalla registrazione di controllo delle cassette postali, è possibile controllare le impostazioni di bypass eseguendo il cmdlet [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/it-it/library/ff696741\(v=exchg.150\)).

Per alcuni esempi relativo alla modalità di verifica delle associazioni di bypass per il controllo delle cassette postali, vedere [Examples](https://technet.microsoft.com/it-it/ff696741\(exchg.150\)#examples) in [Get-MailboxAuditBypassAssociation](https://technet.microsoft.com/it-it/library/ff696741\(v=exchg.150\)).

