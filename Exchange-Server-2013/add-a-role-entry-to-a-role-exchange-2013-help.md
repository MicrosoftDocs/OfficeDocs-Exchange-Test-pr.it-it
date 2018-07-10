---
title: 'Aggiungere una voce di ruolo a un ruolo: Exchange 2013 Help'
TOCTitle: Aggiungere una voce di ruolo a un ruolo
ms:assetid: 30cd37bc-b3e8-4f39-a8ba-a4c20b1b27b7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335180(v=EXCHG.150)
ms:contentKeyID: 50480364
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere una voce di ruolo a un ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-04_

Se si desidera garantire l'accesso a un cmdlet, è necessario aggiungere la voce del ruolo di gestione associata al ruolo di gestione. Dopo aver aggiunto la voce al ruolo, gli utenti associati al ruolo saranno in grado di accedere al cmdlet. Per ulteriori informazioni sulle voci del ruolo di gestione in Microsoft Exchange Server 2013, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Non è possibile aggiungere voci di ruolo ai ruoli incorporati. Se si desidera personalizzare i ruoli, è necessario crearne uno nuovo. Per ulteriori informazioni sulla creazione di un nuovo ruolo, vedere [Creare un ruolo](create-a-role-exchange-2013-help.md).


> [!NOTE]
> In questo argomento non viene discusso come aggiungere le voci del ruolo di gestione senza ambito a un ruolo di gestione senza ambito. Per ulteriori informazioni su come aggiungere le voci di ruolo senza ambito, vedere <A href="add-a-role-entry-to-an-unscoped-top-level-role-exchange-2013-help.md">Aggiungere una voce di ruolo a un ruolo di primo livello senza ambito</A>.



Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - La voce di ruolo che si desidera aggiungere a un ruolo di gestione deve essere presente nel ruolo di gestione padre.

  - In questo argomento viene utilizzato il pipelining. Per ulteriori informazioni sul pipelining, vedere [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\)).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Aggiunta di una singola voce di ruolo da un ruolo padre

È possibile aggiungere una voce di ruolo a un ruolo non appena viene visualizzata sul ruolo padre utilizzando la sintassi seguente.

    Add-ManagementRoleEntry <child role name>\<cmdlet>

In questo esempio viene aggiunto il cmdlet **Set-Mailbox** al ruolo Amministratori destinatario.

    Add-ManagementRoleEntry "Recipient Administrators\Set-Mailbox"

Questo comando consente di controllare il ruolo padre e, se la voce di ruolo esiste, consente di aggiungerla al ruolo figlio. Se la voce di ruolo esiste già nel ruolo figlio, è possibile includere il parametro *Overwrite* per sovrascrivere la voce di ruolo esistente.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Add-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351236\(v=exchg.150\)).

## Aggiunta di una singola voce di ruolo da un ruolo padre e inclusione dei parametri specifici

Se si desidera aggiungere una voce di ruolo da un ruolo padre, ma si desidera includere solo i parametri specifici nella voce sul ruolo figlio, utilizzare la sintassi seguente.

    Add-ManagementRoleEntry <child role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

In questo esempio viene aggiunto il cmdlet **Set-Mailbox** al ruolo Assistenza, ma nella voce sul ruolo figlio vengono inclusi solo i parametri *DisplayName* e *EmailAddresses*.

    Add-ManagementRoleEntry "Help Desk\Set-Mailbox" -Parameters DisplayName, EmailAddresses

Questo comando consente di controllare il ruolo padre e, se la voce di ruolo esiste, consente di aggiungerla al ruolo figlio. Se la voce di ruolo esiste già nel ruolo figlio, è possibile includere il parametro *Overwrite* per sovrascrivere la voce di ruolo esistente.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Add-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351236\(v=exchg.150\)).

## Aggiunta di più voci di ruolo da un ruolo padre

Se si desidera aggiungere più voci di ruolo a un ruolo, è necessario recuperare un elenco di voci di ruolo presenti sul ruolo padre che si desidera aggiungere al ruolo figlio, quindi aggiungerle al ruolo figlio. Per eseguire l'operazione, è necessario recuperare l'elenco di voci di ruolo su un ruolo padre utilizzando il cmdlet **Get-ManagementRoleEntry**. Quindi, eseguire il piping dell'output del cmdlet **Get-ManagementRoleEntry** al cmdlet **Add-ManagementRoleEntry**. Per recuperare più voci di ruolo, è necessario utilizzare i caratteri jolly (\*).

Per aggiungere più voci da un ruolo padre a un ruolo figlio, utilizzare la sintassi seguente.

    Get-ManagementRoleEntry <parent role name>\*<partial cmdlet name>* | Add-ManagementRoleEntry -Role <child role name>

In questo esempio vengono aggiunte tutte le voci di ruolo che contengono la stringa `Mailbox` nel nome del cmdlet sul ruolo padre Destinatari posta nel ruolo figlio Destinatari posta Seattle.

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*" | Add-ManagementRoleEntry -Role "Seattle Mail Recipients"

Se le voci di ruolo esistono già nel ruolo figlio, è possibile includere il parametro *Overwrite* per sovrascrivere la voci di ruolo esistenti.

Per ulteriori informazioni sul recupero di un elenco di voci del ruolo di gestione, vedere [Visualizzazione voci di ruolo](view-role-entries-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd335210\(v=exchg.150\)) e [Add-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351236\(v=exchg.150\)).

