---
title: 'Gestire i criteri di assegnazione dei ruoli: Exchange 2013 Help'
TOCTitle: Gestire i criteri di assegnazione dei ruoli
ms:assetid: f93d502e-5df4-4ba0-b68d-01a17ccffb4d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657511(v=EXCHG.150)
ms:contentKeyID: 50482059
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire i criteri di assegnazione dei ruoli

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-09_

Se si desidera personalizzare le autorizzazioni assegnate a un gruppo di utenti finali, è possibile creare un nuovo criterio di assegnazione del ruolo di gestione personalizzato. Il criterio di assegnazione creato può essere personalizzato in base alle esigenze specifiche dell'utente finale. Per ulteriori informazioni sui criteri di assegnazione in Microsoft Exchange Server 2013, vedere [Informazioni sui criteri di assegnazione di ruolo di gestione](understanding-management-role-assignment-policies-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alla gestione delle autorizzazioni, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri di assegnazione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Aggiunta di un criterio di assegnazione

Dopo aver creato il nuovo criterio di assegnazione, è possibile assegnare gli utenti a esso. Per ulteriori informazioni, vedere [Modificare il criterio di assegnazione di una cassetta postale](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).

## Creazione di un nuovo criterio di assegnazione tramite l'interfaccia di amministrazione di Exchange


> [!NOTE]
> Nell'interfaccia di amministrazione di Exchange è possibile creare solo criteri di assegnazione espliciti. Per creare un nuovo criterio di assegnazione predefinito, è necessario utilizzare Exchange Management Shell. Per ulteriori informazioni, vedere la sezione "Creazione di un criterio di assegnazione predefinito tramite Shell" più avanti in questo argomento.



1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Autorizzazioni** \> **Ruoli utente**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella finestra dei criteri di assegnazione dei ruoli, specificare un nome per il nuovo criterio di assegnazione.

3.  Selezionare la casella di controllo accanto al ruolo o ai ruoli da aggiungere al criterio di assegnazione. È possibile selezionare più ruoli, inclusi i ruoli degli utenti finali aggiunti. Se si seleziona un ruolo a cui sono associati ruoli figlio, i ruoli figlio saranno automaticamente selezionati.

4.  Fare clic su **Salva** per salvare le modifiche ai criteri di assegnazione.

## Creazione di un criterio di assegnazione esplicito tramite Shell

Per creare un criterio di assegnazione esplicito che può essere assegnato manualmente alle cassette postali, utilizzare la seguente sintassi.

```powershell
New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign>
```

In questo esempio, viene creato il criterio di assegnazione esplicito Limited Mailbox Configuration a cui vengono assegnati i ruoli `MyBaseOptions`, `MyAddressInformation` e `MyDisplayName`.

```powershell
    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-RoleAssignmentPolicy](https://technet.microsoft.com/it-it/library/dd638101\(v=exchg.150\)).

## Creazione di un criterio di assegnazione predefinito tramite Shell

Per creare un criterio di assegnazione predefinito assegnato alle nuove cassette postali, utilizzare la seguente sintassi.

```powershell
New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign> -IsDefault
```

In questo esempio, viene creato il criterio di assegnazione predefinito Limited Mailbox Configuration a cui vengono assegnati i ruoli `MyBaseOptions`, `MyAddressInformation` e `MyDisplayName`.

```powershell
    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName -IsDefault
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-RoleAssignmentPolicy](https://technet.microsoft.com/it-it/library/dd638101\(v=exchg.150\)).

## Eliminazione di un criterio di assegnazione

È possibile rimuovere un criterio di assegnazione del ruolo di gestione, se non è più necessario.

## Che cosa è necessario sapere prima di iniziare

  - Tutti gli utenti assegnati al criterio di assegnazione devono essere trasferiti a un altro criterio di assegnazione. Per ulteriori informazioni su come modificare un criterio di assegnazione su una cassetta postale, vedere [Modificare il criterio di assegnazione di una cassetta postale](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).

  - Tutte le assegnazioni del ruolo di gestione tra il criterio di assegnazione e i ruoli di gestione assegnati devono essere rimosse. Per ulteriori informazioni sulla rimozione di un'assegnazione di ruolo da un criterio di assegnazione, vedere la sezione Use the Shell to remove a role from an assignment policy più avanti in questo argomento.

  - Se si desidera rimuovere un criterio di assegnazione predefinito, questo deve essere l'ultimo criterio di assegnazione nell'organizzazione di Exchange 2013.

## Rimozione di un criterio di assegnazione tramite il l'interfaccia di amministrazione di Exchange

1.  In EAC selezionare **Autorizzazioni** \> **Ruoli utente**.

2.  Selezionare il criterio di assegnazione da rimuovere e fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

## Rimozione di un criterio di assegnazione tramite Shell

Per rimuovere un criterio di assegnazione, utilizzare la seguente sintassi.

```powershell
Remove-RoleAssignmentPolicy <role assignment policy>
```

Con questo esempio viene rimosso il criterio di assegnazione New York Temporary Users.

```powershell
Remove-RoleAssignmentPolicy "New York Temporary Users"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-RoleAssignmentPolicy](https://technet.microsoft.com/it-it/library/dd638190\(v=exchg.150\)).

## Mostra un elenco di criteri di assegnazione o i dettagli dei criteri di assegnazione

È possibile visualizzare i criteri di assegnazione dei ruoli di gestione in diversi modi, in base alle informazioni desiderate e se si sta utilizzando l'interfaccia di amministrazione di Exchange o la shell.

Nell'interfaccia di amministrazione di Exchange è possibile visualizzare un elenco dei criteri di assegnazione e dei ruoli corrispondenti assegnati. In Shell è possibile visualizzare tutti i criteri di assegnazione nell'organizzazione, elencare le cassette postali assegnate a un criterio specifico e molto altro.

## Visualizzazione di un elenco di criteri di assegnazione tramite l'interfaccia di amministrazione di Exchange

1.  In EAC selezionare **Autorizzazioni** \> **Ruoli utente**. Tutti i criteri di assegnazione nell'organizzazione sono elencati qui.

2.  Per visualizzare i dettagli di un criterio di assegnazione specifico, selezionare quello che si desidera visualizzare. Nel riquadro dei dettagli viene visualizzata la descrizione insieme ai ruoli assegnati al criterio di assegnazione.

## Visualizzazione di un elenco di criteri di assegnazione tramite Shell

È possibile visualizzare un elenco di tutti i criteri di assegnazione nell'organizzazione non specificando i criteri, quando si esegue il cmdlet **Get-RoleAssignmentPolicy**.

Questa procedura utilizza il pipelining e il cmdlet **Format-Table**. Per ulteriori informazioni su questi concetti, vedere i seguenti argomenti:

  - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))

  - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

Per restituire un elenco di tutti i criteri di assegnazione nell'organizzazione, utilizzare il comando seguente.

```powershell
Get-RoleAssignmentPolicy
```

Per restituire un elenco delle proprietà specifiche per tutti i criteri di assegnazione nell'organizzazione, è possibile eseguire il piping dei risultati al cmdlet **Format-Table** e specificare le proprietà che si desidera nell'elenco dei risultati. Utilizzare la seguente sintassi.

```powershell
Get-RoleAssignmentPolicy | Format-Table <property 1>, <property 2...>
```

In questo esempio viene restituito un elenco di tutti i criteri di assegnazione nell'organizzazione e vengono incluse le proprietà **Name** e **IsDefault**.

```powershell
Get-RoleAssignmentPolicy | Format-Table Name, IsDefault
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) o [Get-RoleAssignmentPolicy](https://technet.microsoft.com/it-it/library/dd638195\(v=exchg.150\)).

## Visualizzazione dei dettagli di un unico criterio di assegnazione tramite Shell

È possibile visualizzare i dettagli di un criterio di assegnazione specifico utilizzando il cmdlet **Get-RoleAssignmentPolicy** ed eseguendo il piping dell'output al cmdlet **Format-List**.

Questa procedura utilizza il pipelining e il cmdlet **Format-List**. Per ulteriori informazioni su questi concetti, vedere i seguenti argomenti:

  - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))

  - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

Per visualizzare i dettagli di un criterio di assegnazione specifico, utilizzare la sintassi seguente.

```powershell
Get-RoleAssignmentPolicy <assignment policy name> | Format-List
```

In questo esempio vengono visualizzati i dettagli relativi al criterio di assegnazione Redmond Users - no Text Messaging.

```powershell
Get-RoleAssignmentPolicy "Redmond Users - no Text Messaging" | Format-List
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) o [Get-RoleAssignmentPolicy](https://technet.microsoft.com/it-it/library/dd638195\(v=exchg.150\)).

## Individuazione del criterio di assegnazione predefinito tramite Shell

È possibile individuare il criterio di assegnazione predefinito eseguendo il piping dell'output del cmdlet **Get-RoleAssignmentPolicy** al cmdlet **Where**. Con il cmdlet **Where**, filtrare i dati restituiti per visualizzare solo il criterio di assegnazione con la proprietà *IsDefault* impostata su `$True`.

In questa procedura viene utilizzato il pipelining e il cmdlet **Where**. Per ulteriori informazioni su questi concetti, vedere i seguenti argomenti:

  - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))

  - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

In questo esempio viene restituito il criterio di assegnazione predefinito.

```powershell
Get-RoleAssignmentPolicy | Where {     Get-RoleAssignmentPolicy | Where { $_.IsDefault -eq $True }.IsDefault -eq $True }
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) o [Get-RoleAssignmentPolicy](https://technet.microsoft.com/it-it/library/dd638195\(v=exchg.150\)).

## Visualizzazione delle cassette postali assegnate a un criterio specifico tramite Shell

È possibile individuare tutte le cassette postali assegnate a un criterio di assegnazione specifico eseguendo il piping dell'output del cmdlet **Get-Mailbox** al cmdlet **Where**. Con il cmdlet **Where**, filtrare i dati restituiti per visualizzare solo le cassette postali con la proprietà *RoleAssignmentPolicy* impostata sul nome del criterio di assegnazione specificato.

In questa procedura viene utilizzato il pipelining e il cmdlet **Where**. Per ulteriori informazioni su questi concetti, vedere i seguenti argomenti:

  - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))

  - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

Utilizzare la seguente sintassi.

```powershell
Get-Mailbox | Where {     Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<role assignment policy>" }.RoleAssignmentPolicy -Eq "<role assignment policy>" }
```

In questo esempio vengono individuate tutte le cassette postali assegnate al criterio Vancouver End Users.

```powershell
Get-Mailbox | Where {     Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Vancouver End Users" }.RoleAssignmentPolicy -Eq "Vancouver End Users" }
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) o [Get-RoleAssignmentPolicy](https://technet.microsoft.com/it-it/library/dd638195\(v=exchg.150\)).

## Modifica di un criterio di assegnazione predefinito

È possibile modificare i criteri di assegnazione del ruolo di gestione assegnato alle nuove cassette postali. Modificando il criterio di assegnazione del ruolo predefinito non verrà modificato il criterio di assegnazione assegnato alle cassette postali esistenti. Per modificare il criterio di assegnazione assegnato alle cassette postali esistenti, vedere [Modificare il criterio di assegnazione di una cassetta postale](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).


> [!NOTE]
> Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per modificare i criteri di assegnazione predefiniti. È necessario utilizzare la shell.



## Modifica dei criteri di assegnazione predefiniti tramite Shell

Per cambiare i criteri di assegnazione predefiniti, utilizzare la seguente sintassi.

```powershell
Set-RoleAssignmentPolicy <assignment policy name> -IsDefault
```

Con questo esempio i criteri di assegnazione Vancouver End Users vengono impostati come criteri di assegnazione predefiniti.

```powershell
Set-RoleAssignmentPolicy "Vancouver End Users" -IsDefault
```


> [!IMPORTANT]
> Alle nuove cassette postali vengono assegnati i criteri di assegnazione predefiniti, anche se ai criteri non sono stati assegnati ruoli di gestione. I criteri di assegnazione applicati alle cassette postali senza ruoli di gestione assegnati non possono accedere alle funzionalità di configurazione della cassetta postale in Microsoft Outlook Web App.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-RoleAssignmentPolicy](https://technet.microsoft.com/it-it/library/dd638090\(v=exchg.150\)).

## Aggiunta di un ruolo a un criterio di assegnazione

## Aggiunta di un ruolo a un criterio di assegnazione tramite l'interfaccia di amministrazione di Exchange

1.  In EAC selezionare **Autorizzazioni** \> **Ruoli utente**.

2.  Selezionare il criterio di assegnazione a cui aggiungere uno o più ruoli e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Selezionare la casella di controllo accanto al ruolo o ai ruoli da aggiungere al criterio di assegnazione. È possibile selezionare più ruoli, inclusi i ruoli degli utenti finali aggiunti. Se si seleziona un ruolo a cui sono associati ruoli figlio, i ruoli figlio saranno automaticamente selezionati.

4.  Fare clic su **Salva** per salvare le modifiche ai criteri di assegnazione.

## Uso di Shell per l'aggiunta di un ruolo a un criterio di assegnazione

Per creare un'assegnazione dei ruoli di gestione tra un ruolo e un criterio di assegnazione, utilizzare la seguente sintassi.

```powershell
    New-ManagementRoleAssignment -Name <role assignment name> -Role <role name> -Policy <assignment policy name>
```

In questo esempio, viene creata l'assegnazione del ruolo Utenti di Roma - Messaggi vocali tra il ruolo MyVoicemail e il criterio di assegnazione degli utenti di Seattle.

```powershell
    New-ManagementRoleAssignment -Name "Seattle Users - Voicemail" -Role MyVoicemail -Policy "Seattle Users"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd335193\(v=exchg.150\)).

## Eliminazione di un ruolo da un criterio di assegnazione

Se non si desidera che gli utenti finali siano autorizzati a gestire determinate funzionalità delle proprie cassette postali o dei propri gruppi di distribuzione, è possibile rimuovere il ruolo di gestione che concede tali autorizzazioni dal criterio di assegnazione del ruolo di gestione per tali utenti. Se allo stesso criterio di assegnazione sono assegnati altri utenti, anch'essi perdono la capacità di gestire tale funzionalità.

## Eliminazione di un ruolo da un criterio di assegnazione tramite l'interfaccia di amministrazione di Exchange

1.  In EAC selezionare **Autorizzazioni** \> **Ruoli utente**.

2.  Selezionare i criteri di assegnazione da cui si desidera rimuovere uno o più ruoli, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") .

3.  Deselezionare la casella di controllo accanto ai ruoli che si desidera rimuovere dai criteri di assegnazione. Se si deseleziona la casella di controllo di un ruolo che include ruoli figlio, verranno deselezionate anche le caselle di controllo dei ruoli figlio.

4.  Fare clic su **Salva** per salvare le modifiche ai criteri di assegnazione.

## Eliminazione di un ruolo da un criterio di assegnazione tramite Shell

Per rimuovere ruoli dai criteri di assegnazione, è possibile recuperare l'assegnazione di ruolo di gestione associata, tramite il cmdlet **Get-ManagementRoleAssignment**, e quindi reindirizzare al cmdlet **Remove-ManagementRoleAssignment** l'assegnazione di ruolo restituita.

Per ulteriori informazioni sulle assegnazioni del ruolo di delega, vedere [Informazioni sulle assegnazioni dei ruoli di gestione](understanding-management-role-assignments-exchange-2013-help.md).

Questa procedura utilizza il pipelining. Per ulteriori informazioni sull'esecuzione del piping, vedere [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\)).

Per rimuovere un ruolo da un criterio di assegnazione, utilizzare la sintassi seguente.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee <assignment policy name> -Role <role name> | Remove-ManagementRoleAssignment
```
In questo esempio viene rimosso il ruolo di gestione MyVoicemail, che consente agli utenti di gestire le opzioni del sistema di caselle vocali dal criterio di assegnazione degli utenti di Seattle.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee "Seattle Users" -Role MyVoicemail | Remove-ManagementRoleAssignment
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-ManagementRoleAssignment](https://technet.microsoft.com/it-it/library/dd351205\(v=exchg.150\)).

