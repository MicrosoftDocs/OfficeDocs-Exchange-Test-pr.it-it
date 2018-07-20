---
title: 'Visualizzare le autorizzazioni valide: Exchange 2013 Help'
TOCTitle: Visualizzare le autorizzazioni valide
ms:assetid: ae6cb7cf-f998-44a6-a69a-02ad736c8260
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638167(v=EXCHG.150)
ms:contentKeyID: 50481416
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzare le autorizzazioni valide

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-09_

Le autorizzazioni in Microsoft Exchange Server 2013 vengono concesse per mezzo di ruoli di gestione assegnati a gruppi di ruoli di gestione, criteri di assegnazione del ruolo di gestione, gruppi di protezione universale (USG) o direttamente agli utenti. Gli utenti ricevono le autorizzazioni se sono membri dei gruppi di ruolo o dei gruppi di protezione universali, oppure se sono stati loro assegnati criteri di assegnazione del ruolo.

La maggior parte delle autorizzazioni viene concessa in base all'appartenenza degli utenti finali al gruppo di ruolo o all'assegnazione agli utenti dei criteri di assegnazione. Anche se l'uso dei gruppi di ruolo e dei criteri di assegnazione facilita la concessione delle autorizzazioni a numerosi utenti, potrebbe essere difficile ricordare i membri di un gruppo di ruolo o gli assegnatari di un criterio di assegnazione. L'opzione *GetEffectiveUsers* del cmdlet **Get-ManagementRoleAssignment** è utile proprio a questo scopo. Consente di visualizzare a quali utenti sono concesse le autorizzazioni applicate da un ruolo di gestione attraverso i gruppi di ruolo, i criteri di assegnazione e i gruppi di protezione universali degli utenti.

L'opzione *GetEffectiveUsers* viene utilizzata insieme al cmdlet **Get-ManagementRoleAssignment** quando viene utilizzato il parametro *Role*. Se l'opzione viene specificata per un particolare ruolo, il cmdlet **Get-ManagementRoleAssignment** esamina tutti gli utenti assegnati al ruolo (ad esempio gruppi di ruolo, criteri di assegnazione e gruppi di protezione universali) ed elenca i membri di ciascun gruppo.


> [!NOTE]
> L'opzione <EM>GetEffectiveUser</EM> non consente di elencare gli utenti che sono membri di un gruppo di ruolo esterno collegato. Se viene individuato un gruppo di ruolo collegato, al posto dell'elenco di utenti viene visualizzato <STRONG>Membri di tutti i gruppi collegati</STRONG>. Per ulteriori informazioni sulle autorizzazioni in più foreste, vedere <A href="understanding-multiple-forest-permissions-exchange-2013-help.md">Informazioni sulle autorizzazioni di più foreste</A>.



Per ulteriori informazioni sui ruoli di gestione, sui gruppi di ruolo e sui criteri di assegnazione, vedere [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md). Per ulteriori informazioni sulle assegnazioni del ruolo di gestione, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alla gestione delle autorizzazioni, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di ruoli" o "Criterio di assegnazione dei ruoli" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Le procedure descritte in questo argomento possono essere eseguite solo in Shell. Non è possibile utilizzare Interfaccia di amministrazione di Exchange per visualizzare le autorizzazioni valide.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Visualizzazione dell'elenco degli utenti tramite Shell

Per elencare tutti gli utenti che hanno ottenuto le autorizzazioni concesse da un ruolo di gestione, utilizzare la seguente sintassi.

    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers

Con questo esempio vengono elencati tutti gli utenti che hanno ottenuto le autorizzazioni fornite dal ruolo Mail Recipients.

    Get-ManagementRoleAssignment -Role "Mail Recipients" -GetEffectiveUsers

Se si desidera modificare le proprietà restituite nell'elenco oppure esportare l'elenco in un file CSV, vedere Use the Shell to customize output and display it in questo argomento.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Individuazione di un utente specifico in un ruolo tramite Shell

Per individuare un utente specifico a cui sono state concesse autorizzazioni per mezzo di un ruolo di gestione, è necessario utilizzare il cmdlet **Get-ManagementRoleAssignment** per recuperare un elenco di tutti gli utenti interessati e poi inviare l'output del cmdlet al cmdlet **Where**. Il cmdlet **Where** consente di filtrare l'output e di restituire solo l'utente specificato. Utilizzare la seguente sintassi.

    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

Con questo esempio viene individuato l'utente David Strome nel ruolo Journaling.

    Get-ManagementRoleAssignment -Role Journaling -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" }

Se si desidera modificare le proprietà restituite nell'elenco o esportare l'elenco in un file CSV, vedere Use the Shell to customize output and display it in questo argomento.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Individuazione di un utente specifico in tutti i ruoli tramite Shell

Per conoscere tutti i ruoli da cui un utente riceve le autorizzazioni, è necessario utilizzare il cmdlet **Get-ManagementRoleAssignment** per recuperare un elenco di tutti gli utenti interessati per tutti i ruoli di gestione e poi inviare l'output del cmdlet al cmdlet **Where**. Il cmdlet **Where** consente di filtrare l'output e di restituire solo le assegnazioni di ruolo che concedono le autorizzazioni all'utente.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

Con questo esempio vengono individuate tutte le assegnazioni di ruolo elencati che concedono autorizzazioni all'utente Kim Akers.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "Kim Akers" }

Se si desidera modificare le proprietà restituite nell'elenco o esportare l'elenco in un file CSV, vedere la sezione Use the Shell to customize output and display it descritta in seguito in questo argomento.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Personalizzazione e visualizzazione dell'output tramite Shell

L'output predefinito del cmdlet **Get-ManagementRoleAssignment** potrebbe non contenere le informazioni desiderate. L'output del cmdlet contiene molte più proprietà di quelle a cui è possibile accedere. Di seguito sono riportate alcune proprietà che potrebbero risultare utili:

  - **EffectiveUserName**   Nome dell'utente.

  - **Role**   Ruolo che concede le autorizzazioni.

  - **RoleAssigneeName**   Il gruppo di ruolo, il criterio di assegnazione o il gruppo di protezione universale assegnato al ruolo che contiene l'utente indicato nella proprietà `EffectiveUserName`.

  - **RoleAssigneeType**   Indica se l'assegnazione di ruolo è relativa a un gruppo di ruolo, a un criterio di assegnazione, a un gruppo di protezione universale o a un utente.

  - **AssignmentMethod**   Indica se l'assegnazione tra il ruolo e l'assegnatario del ruolo è diretta o indiretta.

  - **CustomRecipientWriteScope**   Indica l'ambito di scrittura dei destinatari personalizzato, se presente, applicato all'assegnazione di ruolo durante la sua creazione. L'ambito specificato in questa proprietà sostituisce l'ambito di scrittura destinatari implicito specificato nella proprietà `RecipientWriteScope`.

  - **CustomConfigWriteScope**   Indica l'ambito di scrittura della configurazione personalizzato, se presente, applicato all'assegnazione di ruolo durante la sua creazione. L'ambito specificato in questa proprietà sostituisce l'ambito di scrittura della configurazione implicito specificato nella proprietà `ConfigWriteScope`.

  - **RecipientReadScope**   Indica l'ambito di lettura implicito dei destinatari applicato al ruolo.

  - **RecipientWriteScope**   Indica l'ambito di scrittura implicito dei destinatari applicato al ruolo.

  - **ConfigReadScope**   Indica l'ambito di lettura implicito della configurazione applicato al ruolo.

  - **ConfigWriteScope**   Indica l'ambito di scrittura implicito della configurazione applicato al ruolo.

Per scegliere le proprietà da visualizzare nell'elenco, utilizzare i comandi simili a quelli utilizzati nelle sezioni Use the Shell to list all effective users, Use the Shell to find a specific user on a role e Use the Shell to find a specific user on all roles. L'unica differenza è la necessità di inviare i risultati di questi comandi ai cmdlet **Format-Table** o **Select-Object**. Il cmdlet **Format-Table** è utile per inviare l'elenco dei risultati allo schermo. Il cmdlet **Select-Object** è utile per inviare l'elenco dei risultati a un file CSV.

Entrambi i cmdlet consentono di specificare le proprietà da visualizzare e l'ordine di presentazione. Il cmdlet **Format-Table** mette a disposizione un numero maggiore di opzioni per la visualizzazione dei risultati sullo schermo, mentre **Select-Object** non consente di modificare l'output ed è pertanto utile per l'invio dell'elenco a un file CSV.

Per ulteriori informazioni sui cmdlet **Format-Table** e **Select-Object**, vedere [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md).

## Invio di un elenco personalizzato allo schermo

1.  Scegliere le informazioni che si desidera visualizzare e individuare il comando associato utilizzando una delle seguenti procedure:
    
      - Use the Shell to list all effective users
    
      - Use the Shell to find a specific user a role
    
      - Use the Shell to find a specific user on all roles

2.  Selezionare le proprietà che si desidera visualizzare nell'elenco.

3.  Utilizzare la seguente sintassi per visualizzare l'elenco.
    
        <command to retrieve list > | Format-Table <property 1>, <property 2>, <property ...>

In questo esempio, viene individuato l'utente David Strome su tutti i ruoli e vengono visualizzate le proprietà `EffectiveUserName`, `Role`, `CustomRecipientWriteScope` e `CustomConfigWriteScope`.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Format-Table EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

## Invio di un elenco personalizzato a un file CSV

Per esportare un elenco in un file CSV, è necessario inviare al cmdlet **Select-Object** i risultati del comando **Get-ManagementRoleAssignment** nella procedura appropriata elencata in precedenza. L'output del cmdlet **Select-Object** viene quindi inviato al cmdlet **Export-CSV**, che consente di salvare l'output CSV in un file con il nome specificato.

1.  Scegliere le informazioni che si desidera visualizzare e individuare il comando associato utilizzando una delle seguenti procedure:
    
      - Use the Shell to list all effective users
    
      - Use the Shell to find a specific user a role
    
      - Use the Shell to find a specific user on all roles

2.  Selezionare le proprietà che si desidera visualizzare nell'elenco.

3.  Utilizzare la seguente sintassi per esportare l'elenco in un file CSV.
    
        <command to retrieve list > | Select-Object <property 1>, <property 2>, <property ...> | Export-CSV <filename>

In questo esempio, viene individuato l'utente David Strome su tutti i ruoli e vengono visualizzate le proprietà `EffectiveUserName`, `Role`, `CustomRecipientWriteScope` e `CustomConfigWriteScope`.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Select-Object EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope | Export-CSV c:\output.csv

Ora è possibile visualizzare il file CSV in qualsiasi visualizzatore.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351024\(v=exchg.150\)).

