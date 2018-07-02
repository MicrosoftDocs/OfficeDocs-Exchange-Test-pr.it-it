---
title: 'Creare una regola di protezione di Outlook: Exchange 2013 Help'
TOCTitle: Creare una regola di protezione di Outlook
ms:assetid: da64750d-faaf-44de-ad8c-888eba7fbdbf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638196(v=EXCHG.150)
ms:contentKeyID: 50481811
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare una regola di protezione di Outlook

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Utilizzando le regole di protezione di Microsoft Outlook è possibile proteggere i messaggi con Information Rights Management (IRM) applicando un modello AD RMS (Active Directory Rights Management Services) in Outlook 2010 prima di inviare i messaggi.

Per le attività di gestione aggiuntive correlate a IRM, vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Protezione dei diritti" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - È necessario disporre di un server [AD RMS](https://technet.microsoft.com/en-us/library/hh831364.aspx) distribuito nella stessa foresta del server che esegue Microsoft Exchange Server 2013Active Directory.

  - Se si configurano le regole di protezione di Outlook per i messaggi protetti da IRM, è opportuno valutare l'attivazione della decrittografia del trasporto per consentire agli agenti di trasporto, compreso l'agente Regole di trasporto, di decrittografare e accedere al messaggio. Se si utilizza l'inserimento nel journal, è inoltre opportuno valutare l'attivazione della decrittografia dei report del journal per consentire all'agente di inserimento nel journal di salvare una copia decrittografata nel report del journal. Per ulteriori informazioni, vedere [Decrittografia dei rapporti del journal](journal-report-decryption-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per creare le regole di protezione di Outlook. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Creazione di una regola di protezione di Outlook tramite Shell

Con questo esempio viene creata la regola di protezione di Outlook Project Contoso. La regola consente di proteggere i messaggi inviati al gruppo di distribuzione ContosoPMs utilizzando il modello di AD RMS Business Critical.

    New-OutlookProtectionRule -Name "Project Contoso" -SentTo "DL-ContosoPMs@contoso.com" -ApplyRightsProtectionTemplate "Business Critical"


> [!NOTE]
> Quando si utilizza il predicato <CODE>SentTo</CODE> per una regola di protezione di Outlook e si specifica un gruppo di distribuzione, vengono protetti tramite IRM solo i messaggi indirizzati al gruppo di distribuzione nei campi A, Cc o Ccn. La protezione IRM non viene applicata ai messaggi indirizzati ai singoli membri del gruppo di distribuzione.



È inoltre possibile utilizzare i predicati `FromDepartment` e `SentToScope` per applicare la protezione IRM ai messaggi inviati dagli utenti in un reparto specifico o ai messaggi inviati all'ambito specificato (`InOrganization` per i messaggi interni, `All` per tutti i destinatari).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-OutlookProtectionRule](https://technet.microsoft.com/it-it/library/dd298182\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che una regola di protezione di Outlook sia stata creata correttamente, procedere come segue:

  - Eseguire il cmdlet [Get-OutlookProtectionRule](https://technet.microsoft.com/it-it/library/dd298004\(v=exchg.150\)) per verificare l'avvenuta creazione della regola e per visualizzarne le proprietà. Per un esempio di come recuperare una regola di protezione di Outlook, vedere [Examples](https://technet.microsoft.com/it-it/dd298004\(exchg.150\)#examples) in **Get-OutlookProtectionRule**.

  - Utilizzare Outlook 2010 per creare un messaggio di prova in grado di soddisfare la condizione della regola e assicurarsi che la regola sia attivata sul client.
    

    > [!NOTE]
    > La disponibilità della regola di protezione in Outlook potrebbe richiedere alcuni minuti.


