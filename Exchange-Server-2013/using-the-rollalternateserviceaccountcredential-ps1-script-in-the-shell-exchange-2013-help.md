---
title: 'Utilizzando lo Script RollAlternateserviceAccountCredential.ps1 in Shell: Exchange 2013 Help'
TOCTitle: Utilizzando lo Script RollAlternateserviceAccountCredential.ps1 in Shell
ms:assetid: 6ac55aae-472a-4ed6-83df-2d0e7b48e05c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff808311(v=EXCHG.150)
ms:contentKeyID: 63915393
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzando lo Script RollAlternateserviceAccountCredential.ps1 in Shell

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

È possibile utilizzare lo script RollAlternateServiceAccountPassword.ps1 nell'aggiornamento fto Exchange Server 2013 una credenziale dell'account di servizio alternativo (credenziale ASA) e distribuire l'aggiornamento ai server Accesso Client specificati.


> [!NOTE]
> Exchange Management Shell non caricare automaticamente gli script. È necessario far precedere tutti gli script con "<STRONG>. \</STRONG> ", ad esempio, per eseguire lo script RollAlternateServiceAccountPassword.ps1, digitare <CODE>.\RollAlternateServiceAccountPassword.ps1</CODE>.




> [!NOTE]
> Questo script viene fornito solo in inglese.



Per ulteriori informazioni su come utilizzare e scrivere script, vedere [Scripting con Exchange Management Shell](https://technet.microsoft.com/it-it/library/bb123798\(v=exchg.150\)).

## Sintassi

    RollAlternateServiceAccountPassword.ps1 -Scope <Object> -Identity <Object> -Source <Object> -

## Descrizione dettagliata

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Protezione dell'accesso client" nell'argomento Client Access Permissions.

## Dettagli tecnici dello Script credenziali Account di servizio alternativo

Questo script favorisce il programma di installazione e manutenzione della credenziale ASA. Dopo aver creato le credenziali ASA e impostare i nomi dell'entità servizio appropriato, è possibile utilizzare lo script per distribuire le credenziali per tutti i server Accesso Client di destinazione.

Per utilizzare lo script, è necessario identificare i server che si desidera assegnare e quali credenziali da utilizzare come la credenziale ASA.

## Ambito del server

È possibile scegliere di avere lo script di tutti i membri di un particolare array server Accesso Client o server specifici, tutti i server Accesso Client nella foresta di destinazione. I parametri disponibili sono *ToEntireForest*, *ToArraryMembers*e *ToSpecificServers*. Se si destinazione lo script ai server specifico o a membri di un array di server specifici, il parametro *Identity* deve essere specificato con il server o i nomi di array di server che si desidera assegnare.

## Origine credenziali

Lo script è possibile copiare la password dell'account di servizio alternativo da un server esistente. In alternativa, è possibile specificare l'account che si desidera utilizzare e lasciare che lo script di generare una nuova password per l'account. I parametri disponibili sono *GenerateNewPasswordFor* e *CopyFrom*. Il parametro *GenerateNewPasswordFor* è necessario specificare una stringa di account nel formato seguente: dominio\\nome account. Se si sta utilizzando un account computer, è necessario aggiungere "$" alla fine del nome dell'account, ad esempio CONTOSO\\ClientServerAcct$. Il parametro *CopyFrom* accetta il nome di un server Accesso Client esistente come origine credenziali.

## Generazione di una nuova Password per una credenziale

La password viene creata dallo script. Non è necessario alcun input dell'utente. Lo script tenterà di distribuire la password per tutti i computer di destinazione e quindi cercherà di aggiornare le credenziali dell'account Active Directory con la password appena generato.

La password generata appena 73 caratteri e soddisfi i requisiti di password complesse standard. Se i requisiti di password differiscono, potrebbe essere necessario impostare manualmente la password e quindi copiarlo in server di destinazione.

Per impedire l'interruzione del servizio, lo script viene esaminata ogni server Accesso Client e gestisce la password corrente oltre all'aggiunta la nuova password. Dopo l'esecuzione dello script, le credenziali ASA condivisa saranno in grado di utilizzare una delle 2 password: la password corrente come archiviate in Active Directory o la nuova password ancora non è stata impostata in Active Directory.

Tutte le password che non sono più valide, ad esempio una password scaduta verranno rimosso dal server di destinazione. Se la password in Active Directory non può essere modificata, ad esempio perché la password è scaduta, lo script tenterà una reimpostazione della password. Questo richiederà l'account che esegue lo script per disporre delle autorizzazioni per reimpostare le password degli account computer Active Directory o le password degli account utente, a seconda che l'account di servizio alternativo sia un account computer o un account utente.

Se le password non sono state modificate correttamente per tutti i server Accesso Client di destinazione, aggiornare la password Active Directory può causare un errore di autenticazione. Se lo script viene eseguito in modalità automatica, non aggiornare la password Active Directory con la nuova password solo se tutti i server Accesso Client di destinazione sono stati aggiornati correttamente. Se lo script viene eseguito in modalità automatica, verrà richiesto se si desidera aggiornare la password in Active Directory.

## Creazione di un'attività pianificata per l'automazione di manutenzione della Password

Se si desidera che lo script per creare un'attività pianificata per mantenere le password in modo continuativo, utilizzare il parametro *CreateScheduledTask* . Questo parametro richiede una stringa per il nome dell'attività che si desidera creare.


> [!NOTE]
> Eseguire lo script e verificare che funzioni correttamente in modalità automatica prima di creare l'attività pianificata automatico.



Lo script consente di creare un file con estensione cmd nella cartella in cui si trova lo script. Crea quindi un'attività per eseguire tale file con estensione cmd ogni tre settimane. È possibile utilizzare Windows utilità di pianificazione per modificare l'attività pianificata, ad esempio, per impostare il maggiore o minore frequenza di esecuzione. Per impostazione predefinita, l'attività verrà eseguito come utente attualmente connesso. Inoltre, lo script verrà eseguito solo quando l'utente è connesso al computer. È consigliabile modificare l'attività pianificata da eseguire se l'utente è connesso o meno. È anche possibile scegliere di eseguire con un account diverso, se tale account disponga delle autorizzazioni Active Directory per reimpostare le password, nonché il ruolo di amministratore dell'organizzazione di Exchange. Quando si crea un'attività pianificata, lo script verrà automaticamente eseguito in modalità automatica.

## Attività questione esula dall'ambito dello Script

Lo script non gestire i nomi SPN della credenziale ASA o consentono di rimuovere un account di servizio alternativo da un server. Per rimuovere un account di servizio alternativo da un server, vedere la sezione [Turn Kerberos authentication off](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md) in [Configurazione dell'autenticazione Kerberos per i server Accesso client con bilanciamento del carico](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md).

## Risoluzione dei problemi lo script.

È consigliabile eseguire lo script e verificare che funzioni correttamente in modalità automatica prima di creare l'attività pianificata automatico. Per ulteriori informazioni, vedere [Risoluzione dei problemi lo Script RollAlternateServiceAccountCredential.ps1](troubleshooting-the-rollalternateserviceaccountcredential-ps1-script-exchange-2013-help.md).

## Convalida lo script.

L'output dello script quando si esegue in modo interattivo con il livello di dettaglio flag - deve indicare quali operazioni di script sono state completate. Per verificare che siano stati aggiornati i server Accesso Client, è possibile verificare l'ora ultima modifica alla credenziale ASA. Nell'esempio seguente viene generato un elenco di server Accesso Client e l'ultima volta in cui è stato aggiornato l'account di servizio alternativo.

    Get-ClientAccessServer -IncludeAlternateServiceAccountCredentialstatus |Fl Name, AlternateServiceAccountConfiguration

È anche possibile esaminare il registro eventi nel computer in cui viene eseguito lo script. Le voci del registro eventi per lo script vengono registrati nel registro eventi applicazioni e sono compresi l' origine *MSExchange Management Application*. Nella tabella seguente sono elencati gli eventi che vengono registrati e il significato gli eventi.

### ID evento script e relativa spiegazione

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>14001</p></td>
<td><p>Start</p></td>
</tr>
<tr class="even">
<td><p>14002</p></td>
<td><p>Operazioni riuscite (informazioni)</p></td>
</tr>
<tr class="odd">
<td><p>14003</p></td>
<td><p>Esito positivo ma con avvisi.</p>
<p>Lo script ha rilevato alcuni problemi, ma è stato in grado di evitare tali o confermato l'input dell'utente che non siano necessarie. Se lo script è in esecuzione in modalità interattiva, leggere l'output dello script per ulteriori dettagli avviso.</p></td>
</tr>
<tr class="even">
<td><p>14004</p></td>
<td><p>Operazione non riuscita</p></td>
</tr>
</tbody>
</table>


Se lo script viene eseguito come attività pianificata, nella cartella di **registrazione**Exchange server in una sottocartella denominata **RollAlternateServiceAccountPassword** verranno registrati i relativi risultati.

È possibile utilizzare il registro per verificare che l'attività è stato eseguito correttamente.

## Parametri


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ToEntireForest</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>ToEntireForest</em> riguarda lo script a tutti i server Accesso Client nella foresta.</p></td>
</tr>
<tr class="even">
<td><p><em>ToArrayMembers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>ToArrayMembers</em> riguarda lo script per tutti i membri di un array di server Accesso Client specifico.</p>

> [!NOTE]
> Se si utilizza il parametro <EM>ToArrayMembers</EM> o <EM>ToSpecificServers</EM> , è necessario specificare i nomi dei server o i nomi di array di server utilizzando il parametro <EM>Identity</EM> .


</td>
</tr>
<tr class="odd">
<td><p><em>ToSpecificServers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>ToSpecificServers</em> riguarda lo script per server specifici.</p>

> [!NOTE]
> Se si utilizza il parametro <EM>ToArrayMembers</EM> o <EM>ToSpecificServers</EM> , è necessario specificare i nomi dei server o i nomi di array di server utilizzando il parametro <EM>Identity</EM> .


</td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Il parametro <em>Identity</em> Specifica nome dell'array di server Accesso Client o i nomi dei server specifici di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>GenerateNewPasswordFor&lt;String&gt;</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>GenerateNewPasswordFor</em> specifica che lo script deve generare una nuova password per il ASA. Il valore stringa devono essere account ASA nel formato seguente: dominio\nome account. Se si sta utilizzando un account computer, è necessario aggiungere il carattere $ alla fine del nome dell'account.</p></td>
</tr>
<tr class="even">
<td><p><em>CopyFrom&lt;String&gt;</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>CopyFrom</em> specifica che le credenziali viene copiata da un altro server Accesso Client. Il valore di stringa specificato è il nome del server Accesso Client.</p></td>
</tr>
<tr class="odd">
<td><p><em>Mode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>L'opzione <em>Mode</em> specifica se lo script viene eseguito in modalità manuale o automatica. La modalità automatica non richiede l'input dell'utente e viene automaticamente scelto le opzioni più tradizionale, quando necessario.</p></td>
</tr>
<tr class="even">
<td><p><em>CreateScheduledTask&lt;String&gt;</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>CreateScheduledTask</em> indica lo script per creare un'attività pianificata per eseguire l'aggiornamento di credenziali ASA. Il valore stringa è il nome dell'operazione pianificata che verrà creato.</p>

> [!NOTE]
> Questo script consente di creare un file con estensione cmd nella cartella in cui si trova lo script. L'operazione pianificata eseguirà il file con estensione cmd una volta ogni tre settimane. È possibile modificare l'attività direttamente in Windows utilità di pianificazione per modificare la frequenza dell'attività.


</td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>L'opzione <em>WhatIf</em> consente al comando di simulare le azioni da intraprendere sull'oggetto. Utilizzando l'opzione <em>WhatIf</em>, è possibile visualizzare quali modifiche verrebbero apportate, senza doverle applicare. Con l'opzione <em>WhatIf</em> non è necessario specificare alcun valore.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>L'opzione <em>Confirm</em> consente di sospendere l'elaborazione. L'utente deve confermare l'operazione che verrà eseguita dal comando prima che l'elaborazione continui. Con l'opzione <em>Confirm</em> non è necessario specificare alcun valore.</p></td>
</tr>
<tr class="odd">
<td><p><em>Verbose</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>Verbose</em> indica lo script per eseguire la registrazione dettagliata, in modo che ulteriori informazioni sulle azioni dello script viene scritto il file di registro.</p></td>
</tr>
<tr class="even">
<td><p><em>Debug</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>Debug</em> indica lo script per l'esecuzione in modalità di debug. Questo parametro deve essere utilizzato per determinare il motivo per cui lo script si verifica un errore.</p></td>
</tr>
</tbody>
</table>


## Esempi

## Esempio 1

Questo esempio viene utilizzato lo script per estrarre le credenziali per tutti i server Accesso Client nell'insieme di strutture per la prima installazione.

    .\RollAlternateserviceAccountPassword.ps1 -ToEntireForest -GenerateNewPasswordFor "Contoso\ComputerAccount$" -Verbose

## Esempio 2

In questo esempio viene generata una nuova password per una credenziale ASA dell'account utente e le distribuisce la password per tutti i membri di array di server Accesso Client in cui il nome corrisponde \* \* cassetta postale.

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers *mailbox* -GenerateNewPasswordFor "Contoso\UserAccount" -Verbose

## Esempio 3

In questo esempio viene pianifica un'attività di pianificata (in inglese) una sola volta un mese automatica password denominata "Exchange RollAsa". Le credenziali ASA per tutti i server Accesso Client nell'intera foresta verranno aggiornati con una nuova password generata script. L'operazione pianificata viene creato, ma non è possibile eseguire lo script. Quando viene eseguita l'operazione pianificata, lo script viene eseguito in modalità automatica.

    .\RollAlternateServiceAccountPassword.ps1 -CreateScheduledTask "Exchange-RollAsa" -ToEntireForest -GenerateNewPasswordFor 'contoso\computerAccount$'

## Esempio 4

Questo esempio viene aggiornata la credenziale ASA per tutti i server Accesso Client dell'array di server Accesso Client denominato CAS01. Ottiene le credenziali dall'account del computer Active Directory ServiceAc1 nel dominio Contoso.

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers "CAS01" -GenerateNewPasswordFor "CONTOSO\ServiceAc1$" 

## Esempio 5

In questo esempio viene illustrato come è possibile utilizzare lo script per distribuire ASA a un computer nuovo o a un computer in cui viene messa nuovamente in servizio si sono l'aumento delle dimensioni dell'array di server o perché si sta introduzione nuovamente i membri della matrice dopo la manutenzione.

È necessario aggiornare le credenziali ASA prima che il server Accesso Client riceve il traffico. Copiare la credenziale ASA condivisa da qualsiasi server Accesso Client è già stato configurato correttamente. Ad esempio, se un Server attualmente è una credenziale ASA lavorative e Server B appena aggiunta nella matrice, è possibile utilizzare lo script per copiare la credenziale (compresa la password) dal Server al Server B. Ciò è utile se il Server B è stato premuto o non è ancora un membro della matrice quando la password è stato eseguito il rollback l'ultima volta.

    .\RollAlternateServiceAccountPassword.ps1 -CopyFrom ServerA -ToSpecificServers ServerB -Verbose

