---
title: 'Risol. prob.script RollAlternateServiceAccountCredential.ps1:Exchange 2013 Help'
TOCTitle: Risoluzione dei problemi lo Script RollAlternateServiceAccountCredential.ps1
ms:assetid: 2bbf36d3-eb89-4f92-a8de-259a7cb64d62
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff808310(v=EXCHG.150)
ms:contentKeyID: 63913431
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi lo Script RollAlternateServiceAccountCredential.ps1

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-01-14_

In questo argomento vengono fornite informazioni sugli errori comuni che possono verificarsi quando si utilizza lo script RollAlternateServiceAccountPassword.ps1 e soluzioni.

## Uno o più server Accesso Client non possono essere aggiornati con le password

## Problema

Quando si utilizza il parametro *ToEntireForest* o *ToArrayMembers* con lo script, in alcuni casi, uno o più server Accesso Client potrebbero non essere aggiornati.

## Soluzione

Verificare i server lo script sarà destinato a tutti i server utilizzando il cmdlet **Get-ClientAccessArray** , come illustrato nell'esempio seguente.

    Get-ClientAccessArray | fl members

Se il server con problemi di aggiornare è un membro dell'array accesso Client e ancora non aggiornati correttamente, eseguire di nuovo Exchange il programma di installazione e aggiungere nuovamente il ruolo del server Accesso Client al server. È inoltre possibile specificare i singoli server di destinazione utilizzando il parametro *ToSpecificServers*.

## Alcuni server non rispondono allo script

## Problema

In alcuni casi, i server potrebbero non riuscire per l'aggiornamento a causa di errori temporanei, ad esempio una connessione di rete non valida.

## Soluzione

Verificare che i server in questione dispongono di connettività di rete e Active Directory e quindi riprovare a eseguire lo script.

## Alcuni membri della matrice sono fuori servizio per un periodo di tempo prolungato

## Problema

Se un server dalla rotazione per un periodo di tempo più lungo ma ancora un membro della matrice, come determinato da **Get-ClientAccessArray cmdlet**, la funzionalità di script può essere danneggiata quando si utilizza il parametro *ToArrayMembers* e *ToEntireForest*. Lo stesso problema si verificherà se un server ha avuto un errore permanente, ma non è stato rimosso correttamente l'applicazione della distribuzione.

## Soluzione

Per risolvere questo problema, rimuovere il server della distribuzione mediante Exchange il programma di installazione o eseguire lo script in modalità automatica fino a quando non è possibile rimuovere il server.

Se il server sarà solo verso il basso per un breve periodo di tempo e non si desidera rimuovere definitivamente Exchange, è possibile modificare lo script per eseguire sui server specifici utilizzando il parametro *ToSpecificServers* in modo che solo i server attivi vengono considerati come destinazione. In alternativa, è possibile rimuovere il servizio Accesso Client RPC dall'oggetto Active Directory del server non risponde utilizzando il cmdlet **Remove-ClientAccessArray** , come illustrato nell'esempio seguente.

    Remove-RPCClientAccess -Server Server.Contoso.com

Dopo che il servizio Accesso Client RPC è stato rimosso, il server non verrà restituito come membro di una matrice da [Get-ClientAccessArray](https://technet.microsoft.com/it-it/library/dd297976\(v=exchg.150\)) e lo script non impostarlo come destinazione. Non appena il server sia funziona nuovamente, è possibile aggiungere nuovamente il servizio Accesso Client RPC utilizzando il cmdlet **New-RpcClientAccess** . Quando il servizio Accesso Client RPC viene aggiunto nuovamente, è necessario riavviare il servizio Rubrica di Microsoft Exchange sul server interessato.


> [!WARNING]
> Prima di rimuovere il servizio Accesso Client RPC da un server, vedere l' argomento <A href="https://technet.microsoft.com/it-it/library/dd298151(v=exchg.150)">Remove-RPCClientAccess</A>.



## Per ulteriori informazioni

Per ulteriori informazioni su come utilizzare l'autenticazione Kerberos con un array di server Accesso Client o una soluzione di bilanciamento del carico, vedere gli argomenti seguenti:

  - [Configurazione dell'autenticazione Kerberos per i server Accesso client con bilanciamento del carico](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md)

  - [Utilizzando lo Script RollAlternateserviceAccountCredential.ps1 in Shell](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)

