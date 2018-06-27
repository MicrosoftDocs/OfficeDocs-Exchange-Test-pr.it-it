---
title: 'Aggiungere una voce di ruolo a un ruolo di primo livello senza ambito: Exchange 2013 Help'
TOCTitle: Aggiungere una voce di ruolo a un ruolo di primo livello senza ambito
ms:assetid: 52fd3f20-c348-49d5-9bdb-f2cbf780cf2d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd979789(v=EXCHG.150)
ms:contentKeyID: 50480667
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere una voce di ruolo a un ruolo di primo livello senza ambito

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-03_

È possibile aggiungere script e cmdlet non di Exchange a ruoli di gestione di primo livello senza ambito se si desidera rendere disponibili nuovi script o cmdlet non di Exchange a ruoli senza ambito esistenti. Questi script e cmdlet non di Exchange vengono aggiunti come voci di ruolo di gestione ai ruoli di gestione di primo livello senza ambito. Quindi, possono essere utilizzati dalle voci di ruolo di primo livello senza ambito o da qualsiasi ruolo senza ambito che deriva dai ruoli di primo livello. Per ulteriori informazioni sulle voci di ruolo senza ambito, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).


> [!NOTE]
> Se si desidera modificare una voce per un ruolo di gestione contenente i cmdlet Exchange, vedere <A href="change-a-role-entry-exchange-2013-help.md">Modificare una voce di ruolo</A>.



Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - L'aggiunta di una voce di ruolo su un ruolo di primo livello senza ambito non è una funzionalità predefinita dei gruppi di ruoli di gestione. Affinché per un utente sia possibile aggiungere una voce di ruolo di primo livello senza ambito, è necessario assegnare il ruolo Gestione ruoli senza ambito all'utente oppure a un gruppo di protezione universale o a un gruppo di ruoli di cui l'utente sia membro. Per ulteriori informazioni sull'aggiunta di un ruolo a un gruppo di ruoli o a un gruppo di protezione universale, vedere gli argomenti seguenti:
    
      - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)
    
      - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Aggiunta di una voce di ruolo script a un ruolo di primo livello senza ambito

Se si desidera aggiungere uno script ad un ruolo senza ambito esistente, seguire questa procedura. Se si desidera aggiungere un cmdlet non di Exchange ad un ruolo senza ambito esistente, vedere la sezione "Aggiunta di una voce di ruolo cmdlet non di Exchange ad un ruolo di primo livello senza ambito" descritta in seguito.

Per aggiungere uno script di Windows PowerShell a un ruolo di primo livello senza ambito, è necessario aggiungere una voce del ruolo di gestione al ruolo. La voce di ruolo contiene il nome e i parametri dello script che si desidera rendere disponibile per il ruolo.

Lo script deve risiedere nella directory Script nel percorso di installazione di Microsoft Exchange Server 2013 su ogni server con Exchange 2013 a cui gli utenti potrebbero connettersi per eseguire lo script. Se un utente ha accesso all'esecuzione di uno script, ma lo script non si trova sul server Exchange 2013 a cui è connesso l'utente, si verifica un errore. Per impostazione predefinita, il percorso della directory Scripts è C:\\Programmi\\Microsoft\\Server Exchange\\V14\\Scripts.

Una volta copiato lo script nei server Exchange 2013 appropriati e decisi i parametri da utilizzare, creare la voce di ruolo utilizzando la seguente sintassi.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

In questo esempio viene aggiunto lo script BulkProvisionUsers.ps1 al ruolo IT Scripts con i parametri *Name* e *Location*.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!NOTE]
> Il cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> consente di eseguire la convalida di base per assicurarsi di aggiungere solo i parametri esistenti nello script. Tuttavia, una volta aggiunta la voce di ruolo, non vengono effettuate altre convalide. Se i parametri vengono aggiunti o rimossi in seguito, è necessario aggiornare manualmente le voci di ruolo contenenti lo script.



## Aggiunta di una voce di ruolo cmdlet non di Exchange ad un ruolo di primo livello senza ambito

Se si desidera aggiungere un cmdlet non di Exchange ad un ruolo senza ambito esistente, seguire questa procedura. Se si desidera aggiungere uno script a un ruolo senza ambito esistente, vedere la sezione "Aggiunta di una voce di ruolo script a un ruolo di primo livello senza ambito" in questo argomento.

Per aggiungere un cmdlet non di Exchange a un ruolo di primo livello senza ambito, è necessario aggiungere una voce del ruolo di gestione al ruolo. La voce di ruolo contiene lo snap-in, il nome e i parametri del cmdlet che si desidera rendere disponibile per il ruolo.

Se vengono aggiunti cmdlet non di Exchange al nuovo ruolo, i cmdlet devono essere installati su ogni server Exchange 2013 a cui potrebbero connettersi gli utenti per l'esecuzione dei cmdlet. Per informazioni sulla corretta installazione e registrazione degli snap-in di Windows PowerShell contenenti i cmdlet desiderati, consultare la documentazione del prodotto.

Una volta installato lo snap-in Windows PowerShell contenente i cmdlet sui server Exchange 2013 appropriati e stabiliti i parametri da utilizzare, creare la voce di ruolo usando la seguente sintassi.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

In questo esempio viene aggiunto il cmdlet **Set-WidgetConfiguration** dello snap-in Contoso.Admin.Cmdlets al ruolo Widget Cmdlets con i parametri *Database* e *Size*.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!NOTE]
> Il cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> consente di eseguire la convalida di base per assicurarsi di aggiungere solo i parametri esistenti nello cmdlet. Tuttavia, una volta aggiunta la voce di ruolo, non vengono effettuate altre convalide. Se il cmdlet viene modificato in seguito e i parametri vengono aggiunti o rimossi in seguito, è necessario aggiornare manualmente le voci di ruolo contenenti il cmdlet.



## Altre attività

Una volta aggiunta una voce di ruolo o un ruolo di primo livello senza ambito, è possibile anche effettuare le seguenti operazioni:

[Aggiungere una voce di ruolo a un ruolo](add-a-role-entry-to-a-role-exchange-2013-help.md)

[Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

[Gestire i membri del gruppo di ruolo](manage-role-group-members-exchange-2013-help.md)

[Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[Rimozione di un ruolo da un utente o gruppo di protezione universale](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

