---
title: 'Creazione di un ruolo senza ambito: Exchange 2013 Help'
TOCTitle: Creazione di un ruolo senza ambito
ms:assetid: 5a042ccf-4d5f-4609-a91b-21c20d1e6459
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876886(v=EXCHG.150)
ms:contentKeyID: 50480722
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creazione di un ruolo senza ambito

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-06-09_

È possibile utilizzare un ruolo di gestione senza ambito per fornire ad amministratori ed utenti esperti l'accesso agli script di PowerShell di Windows e ai cmdlet non Exchange. È possibile creare un ruolo di primo livello senza ambito e aggiungere ad esso script o cmdlet non Exchange oppure creare un ruolo basato su un ruolo di primo livello senza ambito esistente. Dopo aver creato e personalizzato un ruolo senza ambito, il ruolo potrà essere assegnato a gruppi di ruoli di gestione, utenti e gruppi di protezione di tipo universale. Non è possibile assegnare ruoli senza ambito a criteri di assegnazione del ruolo di gestione. Per ulteriori informazioni sui ruoli senza ambito, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).


> [!WARNING]
> I ruoli senza ambito sono molto utili ed efficaci perchè, come suggerito dal nome, ad essi non è applicato nessun ambito di gestione. Ciò significa che gli script e i cmdlet non Exchange in essi contenuti possono essere eseguiti per qualsiasi oggetto nell'organizzazione di Exchange. Questo aspetto deve essere preso in considerazione ogniqualvolta vengono aggiunti script o cmdlet non Exchange a un ruolo senza ambito e il ruolo senza ambito viene assegnato.




> [!NOTE]
> Se si desidera creare un ruolo che contenga cmdlet Exchange, è necessario creare un ruolo basato su un ruolo di gestione esistente. Per ulteriori informazioni sulla creazione di ruoli con cmdlet Exchange , vedere <A href="create-a-role-exchange-2013-help.md">Creare un ruolo</A>.



Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - La creazione di ruoli senza ambito non è una funzionalità predefinita dei gruppi di ruoli di gestione. Affinché per un utente sia possibile creare un gruppo di ruoli, è necessario assegnare il ruolo Gestione ruoli senza ambito all'utente oppure a un gruppo di protezione universale o a un gruppo di ruoli di cui l'utente è membro. Per ulteriori informazioni sull'aggiunta di un ruolo a un utente, a un gruppo di protezione universale o a un gruppo di ruolo, vedere i seguenti argomenti:
    
      - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)
    
      - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di un ruolo di gestione di primo livello senza ambito

Se si desidera rendere disponibili agli amministratori o agli utenti esperti dell'organizzazione script o cmdlet non Exchange, è necessario creare un ruolo di primo livello senza ambito. È possibile aggiungere script e cmdlet non Exchange soltanto a un ruolo senza ambito creato come ruolo di primo livello dal momento che il ruolo senza ambito iniziale non eredita le caratteristiche di altri ruoli. Il nuovo ruolo di primo livello senza ambito avrà una relazione di ruolo padre rispetto ad altri ruoli senza ambito che, in funzione di tale relazione, potranno anch'essi utilizzare gli script e i cmdlet non Exchange aggiunti.

Di seguito vengono indicati i passi utili per creare un ruolo di primo livello senza ambito:

## Passo 1: Creare il ruolo di primo livello senza ambito

I ruoli di primo livello senza ambito non hanno un ruolo padre. Per creare un ruolo senza padre è necessario specificare l'opzione *UnscopedTopLevel*. Per creare un nuovo ruolo, utilizzare la seguente sintassi.

```powershell
New-ManagementRole <name of new role> -UnscopedTopLevel
```

In questo esempio viene creato il ruolo di primo livello senza ambito IT Scripts.

```powershell
New-ManagementRole "IT Scripts" -UnscopedTopLevel
```

Una volta creato, il ruolo resta vuoto finché ad esso non si aggiungono script o o cmdlet non Exchange.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRole](https://technet.microsoft.com/it-it/library/dd298073\(v=exchg.150\)).

## Passo 2a: Aggiungere voci di ruolo di gestione di script

Se al nuovo ruolo senza ambito si desidera aggiungere uno script, seguire questo passo. Se al nuovo ruolo senza ambito si desidera aggiungere un cmdlet non Exchange, seguire la procedura illustrata in Step 2b.

Per aggiungere uno script di Windows PowerShell a un ruolo di primo livello senza ambito, è necessario aggiungere una voce del ruolo di gestione al ruolo. La voce di ruolo contiene il nome e i parametri dello script che si desidera rendere disponibile per il ruolo.

Lo script deve risiedere nella directory `RemoteScripts` nel percorso di installazione di Microsoft Exchange Server 2013 su ogni server con Exchange 2013 a cui gli utenti potrebbero connettersi per eseguire lo script. Se un utente ha accesso all'esecuzione di uno script, ma lo script non si trova sul server Exchange 2013 a cui è connesso l'utente, si verifica un errore. Per impostazione predefinita, il percorso della directory `RemoteScripts` è C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts.

Una volta copiato lo script nei server Exchange 2013 appropriati e decisi i parametri da utilizzare, creare la voce di ruolo utilizzando la seguente sintassi.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

In questo esempio viene aggiunto lo script BulkProvisionUsers.ps1 al ruolo IT Scripts con i parametri *Name* e *Location*.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!NOTE]
> Il cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> consente di eseguire la convalida di base per assicurarsi di aggiungere solo i parametri esistenti nello script. Tuttavia, una volta aggiunta la voce di ruolo, non vengono effettuate altre convalide. Se i parametri vengono aggiunti o rimossi in seguito, è necessario aggiornare manualmente le voci di ruolo contenenti lo script.



## Passo 2b: Aggiungere voci di ruolo cmdlet non Exchange

Se al nuovo ruolo senza ambito si desidera aggiungere un cmdlet non Exchange, seguire questo passo. Se al nuovo ruolo senza ambito si desidera aggiungere uno script, seguire la procedura illustrata in Step 2a.

Per aggiungere un cmdlet non di Exchange a un ruolo di primo livello senza ambito, è necessario aggiungere una voce del ruolo di gestione al ruolo. La voce di ruolo contiene lo snap-in, il nome e i parametri del cmdlet che si desidera rendere disponibile per il ruolo.

Se vengono aggiunti cmdlet non di Exchange al nuovo ruolo, i cmdlet devono essere installati su ogni server Exchange 2013 a cui potrebbero connettersi gli utenti per l'esecuzione dei cmdlet. Per informazioni sulla corretta installazione e registrazione degli snap-in di Windows PowerShell contenenti i cmdlet desiderati, consultare la documentazione del prodotto.

Una volta installato lo snap-in Windows PowerShell contenente i cmdlet sui server Exchange 2013 appropriati e stabiliti i parametri da utilizzare, creare la voce di ruolo usando la seguente sintassi.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

In questo esempio viene aggiunto il cmdlet **Set-WidgetConfiguration** dello snap-in Contoso.Admin.Cmdlets al ruolo Widget Cmdlets con i parametri *Database* e *Size*.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!NOTE]
> Il cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> consente di eseguire la convalida di base per assicurarsi di aggiungere solo i parametri esistenti nello cmdlet. Tuttavia, una volta aggiunta la voce di ruolo, non vengono effettuate altre convalide. Se il cmdlet viene modificato in seguito e i parametri vengono aggiunti o rimossi in seguito, è necessario aggiornare manualmente le voci di ruolo contenenti il cmdlet.



## Passo 3: Assegnazione del ruolo di gestione

L'ultima operazione per la creazione e la configurazione di un ruolo è l'assegnazione a un assegnatario di ruolo.


> [!IMPORTANT]
> Gli ambiti di gestione non possono essere configurati per le assegnazioni di ruolo che prevedono un ruolo senza ambito. Se si decide di creare un'assegnazione di ruolo per un gruppo di ruolo, un utente o un gruppo di protezione universale, è necessario scegliere l'opzione per la creazione di un'assegnazione di ruolo senza un ambito di gestione.



È possibile assegnare il nuovo ruolo a un gruppo di ruolo, a un utente o a un gruppo di protezione universale. Per ulteriori informazioni, vedere i seguenti argomenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

## Creare un ruolo senza ambito basato su un altro ruolo senza ambito

Se si desidera utilizzare un ruolo di primo livello senza ambito o altri ruoli già esistenti per creare nuovi ruoli senza ambiti, è possibile generare ruoli senza ambito figlio. I ruoli senza ambito figlio possono contenere un sottoinsieme degli script e dei cmdlet contenuti nei ruoli senza ambito padre. Questa funzionalità è utile, ad esempio, se si desidera assegnare a un amministratore poco esperto solo un sottoinsieme degli script o dei cmdlet contenuti nel ruolo senza ambito padre.

Di seguito vengono indicati i passi utili per creare un ruolo senza ambito figlio:

## Passo 1: Creare il ruolo figlio senza ambito

I nuovi ruoli figlio senza ambito possono essere basati su ruoli senza ambito esistenti. Quando si crea un ruolo, un ruolo esistente e le relative voci del ruolo di gestione vengono copiati nel nuovo ruolo. Il ruolo esistente diventa l'elemento padre del nuovo ruolo figlio. Se si crea un ruolo senza ambito basato su un altro ruolo senza ambito, è necessario scegliere un ruolo che contenga tutti i cmdlet e i parametri necessari e, quindi, rimuovere quelli indesiderati. I ruoli senza ambito figlio non possono contenere voci di ruolo di gestione non presenti nel ruolo padre.


> [!NOTE]
> Se si desidera creare un ruolo senza ambito che contenga script o cmdlet non Exchange non presenti in nessun altro ruolo senza ambito, creare un ruolo di primo livello senza ambito. Per ulteriori informazioni, vedere Create an unscoped top-level management role, già illustrato in questo argomento.



Per creare un nuovo ruolo, utilizzare la seguente sintassi.

    New-ManagementRole -Parent <existing unscoped role to copy> -Name <name of new unscoped role>

In questo esempio il ruolo IT Global Scripts e le relative voci di ruolo di gestione vengono copiati nel ruolo Diagnostic IT Scripts.

```powershell
New-ManagementRole -Parent "IT Global Scripts" -Name "Diagnostic IT Scripts"
```

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-ManagementRole](https://technet.microsoft.com/it-it/library/dd298073\(v=exchg.150\)).

## Passo 2: Modificare le voci di ruolo di gestione ruoli

Una volta creato il ruolo, è necessario modificare le voci del ruolo. È possibile rimuovere una voce di ruolo completamente, il che determina l'impossibilità di accedere allo script o al cmdlet non Exchange ad essa associato. In alternativa, è possibile rimuovere i parametri da una voce di ruolo per rimuovere l'accesso a questi nello script o nel cmdlet non Exchange ad essa associato.

Non è possibile aggiungere voci di ruolo o parametri in voci di ruolo a meno che questi non esistano nel ruolo padre. Dato che il nuovo ruolo è stato creato da un ruolo padre nel Passo 1, non è possibile aggiungere altre voci di ruolo o altri parametri alle voci di ruolo, in quanto non esistenti nel ruolo padre.

Quando si modifica la voce di un ruolo, è possibile effettuare una delle seguenti operazioni:

  - Rimuovere una singola voce di ruolo.

  - Rimuovere più voci di ruolo.

  - Rimuovere parametri da una voce di ruolo.

Per rimuovere voci dal nuovo ruolo, vedere [Rimuovere una voce di ruolo da un ruolo](remove-a-role-entry-from-a-role-exchange-2013-help.md).

## Passaggio 3: Assegnazione del ruolo di gestione

L'ultima operazione per la creazione e la configurazione di un ruolo è l'assegnazione a un assegnatario di ruolo.


> [!IMPORTANT]
> Gli ambiti di gestione non possono essere configurati per le assegnazioni di ruolo che prevedono un ruolo senza ambito. Se si decide di creare un'assegnazione di ruolo per un gruppo di ruolo, un utente o un gruppo di protezione universale, è necessario scegliere l'opzione per la creazione di un'assegnazione di ruolo senza un ambito di gestione.



È possibile assegnare il nuovo ruolo a un gruppo di ruolo, a un utente o a un gruppo di protezione universale. Per ulteriori informazioni, vedere i seguenti argomenti:

  - [Gestire gruppi di ruoli](manage-role-groups-exchange-2013-help.md)

  - [Aggiungere un ruolo di un utente o gruppo di protezione universale](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

