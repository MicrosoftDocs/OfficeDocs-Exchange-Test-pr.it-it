---
title: "Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore: Exchange 2013 Help"
TOCTitle: Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore
ms:assetid: c7188d53-e672-492b-b57d-cd711379ddb3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff459262(v=EXCHG.150)
ms:contentKeyID: 50553901
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-12-02_

È possibile effettuare una ricerca nei log di controllo dell'amministratore per individuare chi ha apportato delle modifiche alla configurazione dell'organizzazione, del server e del destinatario. Questa funzionalità può rivelarsi utile quando si cerca di individuare la causa di un comportamento imprevisto, di identificare un amministratore malintenzionato o di verificare se i requisiti di conformità sono stati soddisfatti. Per ulteriori informazioni sulla registrazione dei controlli dell'amministratore, vedere [Registrazione controlli dell'amministratore](administrator-audit-logging-exchange-2013-help.md).

Se si desidera eseguire la ricerca nel log di controllo della cassetta postale, vedere [Registrazione di controllo delle cassette postali](mailbox-audit-logging-exchange-2013-help.md).


> [!TIP]
> In Exchange Online, è possibile utilizzare l'interfaccia di amministrazione di Exchange per visualizzare le voci nel registro di controllo dell'amministratore. Per ulteriori informazioni, vedere <A href="view-the-administrator-audit-log-exchange-2013-help.md">Visualizzare il registro di controllo dell'amministratore</A>.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: meno di 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo dell'amministratore in sola visualizzazione" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - La registrazione di controllo dell'amministratore è abilitata per impostazione predefinita. Per verificare che sia abilitata, utilizzare il comando seguente:
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    Il valore `True` indica che la registrazione di controllo dell'amministratore è abilitata. Il valore `False` indica che è disabilitata. Per abilitare la registrazione di controllo dell'amministratore per un'organizzazione di Exchange locale, eseguire il seguente comando:
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $true
    

    > [!NOTE]
    > Il cmdlet <STRONG>Set-AdminAuditLogConfig</STRONG> non è disponibile in Exchange Online.

    
    Per ulteriori informazioni, vedere [Amministratore di gestire la registrazione di controllo](manage-administrator-audit-logging-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Esecuzione del report delle modifiche al gruppo del ruolo di gestione tramite EAC

Per individuare quali modifiche nell'appartenenza al gruppo del ruolo di gestione sono state apportate ai gruppi di ruolo dell'organizzazione, è possibile utilizzare il report del gruppo del ruolo di amministratore in Interfaccia di amministrazione di Exchange. Grazie al report del gruppo del ruolo di amministratore, è possibile visualizzare un elenco dei gruppi di ruolo modificati in un determinato arco di tempo. È possibile inoltre selezionare gruppi di ruolo specifici per visualizzarne le modifiche.

1.  In EAC selezionare **Gestione della conformità** \> **Controllo**, quindi fare clic su **Esegui il rapporto di un gruppo di ruoli amministratore**.

2.  Selezionare un intervallo di date utilizzando i campi **Data di inizio** e **Data di fine**.

3.  Fare clic su **Seleziona gruppi di ruoli**, quindi selezionare i gruppi di ruoli per cui si desidera visualizzare le modifiche oppure lasciare il campo vuoto per cercare le modifiche in tutti i gruppi di ruoli.

4.  Fare clic su **Cerca**.

Se vengono rilevate delle modifiche utilizzando i criteri specificati, verrà visualizzato un elenco delle modifiche nel riquadro dei risultati. Se si seleziona un gruppo di ruolo, le modifiche apportate a tale gruppo vengono visualizzate nel riquadro dei dettagli.

## Esportazione del log di controllo dell'amministratore tramite EAC

Per creare un file XML che contiene le modifiche apportate all'organizzazione, è possibile utilizzare il report dell'esportazione del log di controllo dell'amministratore in EAC. Utilizzando il report dell'esportazione del log di controllo dell'amministratore, è possibile specificare un intervallo di date nell'ambito del quale cercare le voci del log di controllo che contengono le modifiche apportate dagli utenti specificati. Il file XML viene quindi inviato a un destinatario come allegato di posta elettronica. La dimensione massima del file XML è 10 megabyte (MB).


> [!NOTE]
> Outlook Web App non consente di aprire gli allegati XML per impostazione predefinita. È possibile configurare Exchange per consentire la visualizzazione degli allegati XML con Outlook Web App oppure è possibile usare un altro client di posta elettronica, ad esempio Microsoft Outlook, per visualizzare l'allegato. Per informazioni sulla configurazione di Outlook Web App per consentire la visualizzazione di un allegato XML, vedere <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Consente di visualizzare o configurare le directory virtuali di Outlook Web App</A>.



1.  In EAC selezionare **Gestione della conformità** \> **Controllo**, quindi fare clic su **Esporta il registro di controllo dell'amministratore**.

2.  Selezionare un intervallo di date utilizzando i campi **Data di inizio** e **Data di fine**.

3.  Nel campo **Invia il rapporto di controllo a** fare clic su **Seleziona utenti** e quindi selezionare il destinatario a cui si desidera inviare il report.

4.  Fare clic su **Esporta**.

Se vengono individuate delle voci utilizzando i criteri specificati, verrà creato un file XML che sarà inviato come allegato di posta elettronica al destinatario specificato.

## Ricerca delle voci del log di controllo tramite Shell

La shell può essere utilizzata per cercare le voci del log di controllo che soddisfano i criteri specificati. Per un elenco dei criteri di ricerca, vedere [Registrazione controlli dell'amministratore](administrator-audit-logging-exchange-2013-help.md). In questa procedura viene utilizzato il cmdlet **Search-AdminAuditLog** e i risultati della ricerca vengono visualizzati nella shell. È possibile utilizzare questo cmdlet per la restituzione di un set di risultati che supera i limiti definiti nel cmdlet **New-AdminAuditLogSearch** o nei report di controllo di Interfaccia di amministrazione di Exchange.

Per inviare i risultati della ricerca effettuata nel log di controllo in un allegato di posta elettronica a un destinatario, vedere Use the Shell to search for audit log entries and send results to a recipient più avanti in questo argomento.

Per effettuare una ricerca nel log di controllo in base ai criteri specificati, utilizzare la sintassi seguente.

    Search-AdminAuditLog - Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False >


> [!NOTE]
> Per impostazione predefinita, il cmdlet <STRONG>Search-AdminAuditLog</STRONG> restituisce un massimo di 1.000 voci di registro. Utilizzare il parametro <EM>ResultSize</EM> per specificare fino a 250.000 voci di registro. In alternativa, utilizzare il valore <CODE>Unlimited</CODE> per la restituzione di tutte le voci.



In questo esempio viene eseguita la ricerca di tutte le voci del log di controllo con i seguenti criteri:

  - **Data di inizio**   04/08/2012

  - **Data di fine**   03/10/2012

  - **ID utente**   davids chrisd, kima

  - **Cmdlet**   **Set-Mailbox**

  - **Parametri**   *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

<!-- end list -->

    Search-AdminAuditLog -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima

In questo esempio vengono cercate le modifiche apportate a una cassetta postale specifica. Questa ricerca è utile per la risoluzione dei problemi o se è necessario fornire informazioni per un'analisi. Vengono utilizzati i seguenti criteri:

  - **Data di inizio**   01/05/2012

  - **Data di fine**   03/10/2012

  - **ID oggetto**   contoso.com/Users/DavidS

<!-- end list -->

    Search-AdminAuditLog -StartDate 05/01/2012 -EndDate 10/03/2012 -ObjectID contoso.com/Users/DavidS

Se la ricerca restituisce molte voci di registro, si consiglia di utilizzare la procedura descritta in Use the Shell to search for audit log entries and send results to a recipient più avanti in questo argomento. Nella procedura descritta nella sezione citata, viene inviato un file XML come allegato di posta elettronica ai destinatari specificati, consentendo di estrarre più facilmente i dati a cui si è interessati.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Search-AdminAuditLog](https://technet.microsoft.com/it-it/library/ff459250\(v=exchg.150\)).

## Visualizzazione dei dettagli del log di controllo

Il cmdlet **Search-AdminAuditLog** restituisce i campi descritti nella sezione dedicata al contenuto dei log di controllo di [Registrazione controlli dell'amministratore](administrator-audit-logging-exchange-2013-help.md). Dei due campi restituiti dal cmdlet, due, ovvero **CmdletParameters** e **ModifiedProperties**, contengono ulteriori informazioni non visualizzabili per impostazione predefinita.

Per visualizzare il contenuto dei campi **CmdletParameters** e **ModifiedProperties**, attenersi alla procedura riportata di seguito. In alternativa, per creare un file XML è possibile utilizzare la procedura descritta in Use the Shell to search for audit log entries and send results to a recipient più avanti in questo argomento.

In questa procedura vengono utilizzati i seguenti concetti:

  - [Array](https://technet.microsoft.com/it-it/library/aa998267\(v=exchg.150\))

  - [Variabili definite dall'utente](https://technet.microsoft.com/it-it/library/bb123690\(v=exchg.150\))

<!-- end list -->

1.  Scegliere i criteri in base ai quali eseguire la ricerca, eseguire il cmdlet **Search-AdminAuditLog** e memorizzare i risultati in una variabile utilizzando il comando seguente.
    
        $Results = Search-AdminAuditLog <search criteria>

2.  Ogni voce del log di controllo viene memorizzata come un elemento di matrice nella variabile `$Results`. È possibile selezionare un elemento di matrice specificandone l'indice. Gli indici degli elementi di matrice iniziano da zero (0) per il primo elemento della matrice. Ad esempio, per recuperare il quinto elemento della matrice, il cui indice è 4, utilizzare il comando seguente.
    
        $Results[4]

3.  Il comando precedente restituisce la voce di registro memorizzata nell'elemento 4 della matrice. Per visualizzare il contenuto nei campi **CmdletParameters** e **ModifiedProperties** per questa voce di registro, utilizzare il comando seguente.
    
        $Results[4].CmdletParameters
        $Results[4].ModifiedProperties

4.  Per visualizzare il contenuto dei campi **CmdletParameters** o **ModifiedParameters** in un'altra voce di registro, modificare l'indice degli elementi di matrice.

## Ricerca delle voci del log di controllo e invio dei risultati a un destinatario tramite Shell

La shell può essere utilizzata per la ricerca delle voci del log di controllo che soddisfano i criteri specificati, quindi per l'invio dei risultati a un destinatario in un file XML allegato. I risultati vengono inviati al destinatario nel giro di 15 minuti. Per un elenco dei criteri di ricerca, vedere [Registrazione controlli dell'amministratore](administrator-audit-logging-exchange-2013-help.md).


> [!NOTE]
> Outlook Web App non consente di aprire gli allegati XML per impostazione predefinita. È possibile configurare Exchange per consentire la visualizzazione degli allegati XML con Outlook Web App oppure è possibile usare un altro client di posta elettronica, ad esempio Microsoft Outlook, per visualizzare l'allegato. Per informazioni sulla configurazione di Outlook Web App per consentire la visualizzazione di un allegato XML, vedere <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Consente di visualizzare o configurare le directory virtuali di Outlook Web App</A>.



Per effettuare una ricerca nel log di controllo in base ai criteri specificati, utilizzare la sintassi seguente.

    New-AdminAuditLogSearch -Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False > -StatusMailRecipients <recipient 1, recipient 2, ...> -Name <string to include in subject>

In questo esempio viene eseguita la ricerca di tutte le voci del log di controllo con i seguenti criteri:

  - **Data di inizio**   04/08/2012

  - **Data di fine**   03/10/2012

  - **ID utente**   davids chrisd, kima

  - **Cmdlet**   **Set-Mailbox**

  - **Parametri**   *ProhibitSendQuota*, *ProhibitSendReceiveQuota*, *IssueWarningQuota*, *MaxSendSize*, *MaxReceiveSize*

Il comando consente di inviare i risultati all'indirizzo davids@contoso.com con "Modifiche al limite della cassetta postale" incluso nell'oggetto del messaggio.

    New-AdminAuditLogSearch -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima -StatusMailRecipients davids@contoso.com -Name "Mailbox limit changes"


> [!NOTE]
> Le dimensioni del report generato dal cmdlet <STRONG>New-AdminAuditLogSearch</STRONG> possono raggiungere un massimo di 10&nbsp;MB. Se la ricerca effettuata restituisce un report di dimensioni superiori a 10&nbsp;MB, modificare i criteri di ricerca specificati. Ad esempio, ridurre la portata dell'intervallo di date ed eseguire più report, ciascuno con una parte dell'intervallo di date originale.



Per ulteriori informazioni sul formato del file XML, vedere [Struttura del Registro di controllo amministratore](administrator-audit-log-structure-exchange-2013-help.md).

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-AdminAuditLogSearch](https://technet.microsoft.com/it-it/library/ff459243\(v=exchg.150\)).

