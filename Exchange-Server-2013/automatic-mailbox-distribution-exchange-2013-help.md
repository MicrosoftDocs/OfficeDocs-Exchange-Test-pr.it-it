---
title: 'Distribuzione automatica delle cassette postali: Exchange 2013 Help'
TOCTitle: Distribuzione automatica delle cassette postali
ms:assetid: f4db4636-948c-466b-839c-300c1a3a9544
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff477621(v=EXCHG.150)
ms:contentKeyID: 59634750
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuzione automatica delle cassette postali

 

_**Si applica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-08-13_

Quando si crea o si sposta una cassetta postale, o si abilita all'uso della posta un utente esistente, tale cassetta postale deve essere archiviata nel database delle cassette postali. In Microsoft Exchange Server 2013 è possibile lasciare la scelta del database a Exchange utilizzando la distribuzione automatica delle cassette postali.

Con la distribuzione automatica delle cassette postali, Exchange esamina i database delle cassette postali disponibili nell'organizzazione, esclude i database non adatti, tramite i criteri illustrati più avanti in questo argomento, e quindi sceglie casualmente il database in cui inserire la cassetta postale. Questo processo distribuisce casualmente le cassette postali tra tutti i database delle cassette postali appropriati dell'organizzazione.

Viene utilizzata la distribuzione automatica quando non si specifica il parametro *Database* nei cmdlet **New-Mailbox** ed **Enable-Mailbox** o il parametro *TargetDatabase* nel cmdlet **New-MoveRequest**.


> [!NOTE]
> La distribuzione automatica delle cassette postali viene eseguita solo quando una cassetta postale viene creata in un server Exchange 2013, spostata in un server Exchange 2013 o quando un utente viene abilitato all'uso della posta. I cmdlet <STRONG>New-Mailbox</STRONG>, <STRONG>New-MoveRequest</STRONG> ed <STRONG>Enable-Mailbox</STRONG> devono essere eseguiti da un server che esegue Exchange 2013. Exchange non ridistribuisce il carico tra le cassette postali automaticamente in base al carico del server.



Per trovare un database delle cassette postali appropriato quando è necessario scegliere la posizione di una cassetta postale nuova o da spostare, viene utilizzato il processo seguente:

1.  Exchange recupera un elenco di tutti i database delle cassette postali nell'organizzazione di Exchange 2013.

2.  Tutti i database delle cassette postali contrassegnati per l'esclusione dal processo di distribuzione vengono rimossi dall'elenco dei database disponibili. È possibile controllare i database esclusi. Per ulteriori informazioni, vedere Exclude Databases from Automatic Distribution più avanti in questo argomento.

3.  Tutti i database delle cassette postali che non rientrano negli ambiti di gestione dei database applicati all'amministratore che esegue l'operazione vengono rimossi dall'elenco dei database disponibili. Per ulteriori informazioni, vedere Database Scopes più avanti in questo argomento.

4.  Tutti i database delle cassette postali che non si trovano nel sito di Active Directory locale in cui viene eseguita l'operazione vengono rimossi dall'elenco dei database disponibili.

5.  Exchange sceglie casualmente un database nell'elenco dei database delle cassette postali rimanenti. Se il database è online e integro, verrà utilizzato da Exchange. Se è offline o non integro, verrà scelto casualmente un altro database. Se non è possibile trovare un database offline e integro, l'operazione non riesce e viene restituito un errore.

Il processo di selezione del database delle cassette postali viene eseguito dall'agente di estensione del cmdlet dell'agente di gestione delle risorse delle cassette postali. `Mailbox Resources Management Agent` è uno dei numerosi agenti di estensione dei cmdlet che estendono le funzionalità dei cmdlet in esecuzione. Per ulteriori informazioni sugli agenti di estensione cmdlet, vedere [Agenti di estensione di cmdlet](cmdlet-extension-agents-exchange-2013-help.md).

Se non si desidera eseguire la distribuzione automatica delle cassette postali, è possibile disabilitare `Mailbox Resources Management Agent`. Se si disabilita l'agente, la modifica viene applicata all'intera organizzazione di Exchange. Per ulteriori informazioni su come disabilitare gli agenti di estensione dei cmdlet, vedere [Gestire gli agenti di estensione cmdlet](manage-cmdlet-extension-agents-exchange-2013-help.md).

## Esclusione di database dalla distribuzione automatica

Per impostazione predefinita, tutti i database delle cassette postali online e integri disponibili nei server di Exchange 2013 nel sito Active Directory locale possono essere scelti dalla distribuzione automatica delle cassette postali per l'archiviazione delle cassette postali nuove o da spostare. Può essere tuttavia necessario escludere alcuni database dal processo di distribuzione per vari motivi. Ad esempio, un database delle cassette postali può essere designato come database del journal, in cui è possibile inserire solo le cassette postali specificate manualmente. Può essere anche necessario rimuovere temporaneamente un database dalla rotazione per eseguire la manutenzione pianificata. Exchange 2013 offre la possibilità di escludere permanentemente o temporaneamente i database dal processo di esclusione utilizzando il parametro *IsExcludedFromProvisioning*, che può essere impostato con il cmdlet **Set-MailboxDatabase**.


> [!NOTE]
> Altri due parametri, <EM>IsSuspendedFromProvisioning</EM> e <EM>IsExcludedFromInitialProvisioning</EM>, sono disponibili nel cmdlet <STRONG>Set-MailboxDatabase</STRONG>. Tali parametri saranno rimossi in una versione futura di Exchange e il loro uso non è supportato.



Il parametro *IsExcludedFromProvisioning* ha due valori validi, `$True` e `$False`. Quando si imposta questa proprietà su `$True`, il database delle cassette postali viene escluso dal processo di distribuzione automatica. Quando si imposta questa proprietà su `$False`, il database delle cassette postali viene incluso nel processo di distribuzione automatica. Il valore predefinito è `$False`.

Per escludere un database delle cassette postali dalla distribuzione automatica, utilizzare il comando seguente:

```powershell
Set-MailboxDatabase <database name> -IsExcludedFromProvisioning $True
```

Quando un database delle cassette postali viene escluso dalla distribuzione automatica, è possibile creare o spostare una cassetta postale in tale database esclusivamente utilizzando il parametro *Database* con i cmdlet **New-Mailbox** ed **Enable-Mailbox** oppure il parametro *TargetDatabase* con il cmdlet **New-MoveRequest**.

## Ambiti di gestione dei database

Gli ambiti di gestione del database costituiscono un ulteriore livello di controllo sul processo di distribuzione automatica delle cassette postali disponibile in Exchange 2013. Se un database delle cassette postali è online e integro, risiede nel sito Active Directory locale e non è stato escluso dal processo di distribuzione automatica, Exchange 2013 verifica che il database delle cassette postali sia incluso nell'ambito di database applicato all'amministratore che esegue il cmdlet. Se è incluso nell'ambito di gestione dei database, compare nell'elenco dei database disponibili per tale amministratore.

Gli ambiti di gestione dei database fanno parte del modello di autorizzazioni RBAC (Role Based Access Control). Per ulteriori informazioni su RBAC e sugli ambiti di gestione dei database, vedere gli argomenti seguenti:

  - [Controllo di accesso basato sui ruoli](understanding-role-based-access-control-exchange-2013-help.md)

  - [Comprensione degli ambiti di gestione dei ruoli](understanding-management-role-scopes-exchange-2013-help.md)

Gli ambiti di gestione dei database possono essere utili se il sito Active Directory locale include numerosi database delle cassette postali disponibili per la distribuzione automatica, ma si desidera limitare i database che possono essere utilizzati da determinati gruppi di amministratori. Ciò avviene, ad esempio, quando i server Exchange 2013 possono servire numerose agenzie ma si desidera che ogni agenzia possa creare o spostare cassette postali solo in database delle cassette postali ad essa assegnati.

Per impostazione predefinita, tutti gli amministratori in un'organizzazione Exchange 2013 possono visualizzare tutti i database delle cassette postali dell'organizzazione. Per limitare i database che possono essere visualizzati dagli amministratori, e quindi i database in cui potrebbero creare o spostare cassette postali, è necessario effettuare le operazioni seguenti:

1.  Utilizzando il cmdlet **New-ManagementScope**, creare un ambito di gestione dei database personalizzato contenente solo i database delle cassette postali che possono essere utilizzati dagli amministratori.

2.  Associare il nuovo ambito di gestione dei database a un'assegnazione del ruolo di gestione, utilizzando uno dei metodi seguenti:
    
      - Aggiungere il nuovo ambito di gestione dei database a un'assegnazione del ruolo di gestione esistente utilizzando il parametro *CustomConfigWriteScope* con il cmdlet **Set-ManagementRoleAssignment**. L'ambito di gestione dei database viene in tal modo applicato al gruppo dei ruoli di gestione, al gruppo di sicurezza universale o all'assegnazione di ruolo associata all'utente.
    
      - Creare un'assegnazione di ruolo di gestione utilizzando il cmdlet **New-ManagementRoleAssignment** e utilizzare il parametro *CustomConfigWriteScope* per specificare il nuovo ambito di gestione dei database. È possibile creare un'assegnazione di ruoli tra un ruolo di gestione e un gruppo di ruoli, un gruppo di sicurezza universale o un utente.

3.  Se è stata creata un'assegnazione di ruolo per un gruppo di ruoli o un gruppo di sicurezza universale, aggiungere a tale gruppo gli utenti a cui si desidera applicare l'assegnazione di ruolo e l'ambito di gestione dei database.

4.  Se necessario, rimuovere l'utente, o gli utenti membri dei gruppi di ruoli o dei gruppi di sicurezza universale creati nei passaggi precedenti, a cui è stata assegnata la nuova assegnazione di ruolo da qualsiasi altro gruppo di ruolo o gruppo di sicurezza universale a cui potrebbe essere assegnato un ambito di gestione dei database contenente database a cui non si desidera che accedano.

5.  Verificare che gli amministratori abbiano accesso solo ai database appropriati.

Al termine di questa procedura, gli amministratori a cui sono state associate assegnazioni di ruolo con gli ambiti di gestione dei database creati potranno creare o spostare cassette postali esclusivamente nei database specificati.

Per ulteriori informazioni su come utilizzare gli ambiti di gestione dei database per limitare i database delle cassette postali disponibili agli amministratori, vedere [Controllare la distribuzione automatica delle cassette postali tramite gli ambiti dei database](control-automatic-mailbox-distribution-using-database-scopes-exchange-2013-help.md).

