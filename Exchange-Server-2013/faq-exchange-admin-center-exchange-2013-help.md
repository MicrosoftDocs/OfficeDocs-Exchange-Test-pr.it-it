---
title: 'Domande frequenti: Interfaccia di amministrazione di Exchange: Exchange 2013 Help'
TOCTitle: 'Domande frequenti: Interfaccia di amministrazione di Exchange'
ms:assetid: 3de0042f-74a6-458f-947c-3cd6eeacd6ab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ552409(v=EXCHG.150)
ms:contentKeyID: 50480426
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domande frequenti: Interfaccia di amministrazione di Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento viene fornita con un elenco di domande frequenti per la nuova interfaccia di amministrazione Exchange (EAC) in Microsoft Exchange Server 2013. Sono altre domande relative all'interfaccia di amministrazione Exchange non riceve risposta qui? Inviare un messaggio di posta elettronica in [Ex2013HelpFeedback@microsoft.com](mailto:ex2013helpfeedback@microsoft.com).

## Il valore EAC sviluppato unicamente per Exchange Online?

Il valore EAC agisce da tutte le opzioni di distribuzione per Exchange 2013, tra cui i clienti che desiderano distribuire in locale, nel cloud con Exchange Online o una distribuzione ibrida.

## Sono stati rimossi Exchange Management Console (EMC) dal momento che si sta creando l'interfaccia principalmente per i clienti di piccoli e medie dimensioni?

L'interfaccia di amministrazione di Exchange è stata sviluppata per offrire un'esperienza di gestione unica e intuitiva per tutti i nostri clienti e sono stato progettato per semplificare l'esecuzione delle attività più comuni di amministrazione.

Viene creata un'unica interfaccia che fornisce soprainsieme copertura scenario su Exchange Management Console (EMC) e il pannello di controllo di Exchange (ECP) e uno che risolvono i problemi principali e gli scenari per i clienti.

Inoltre, si attendeva ai clienti di tutte le dimensioni e i problemi principali sono i seguenti:

  - Gestione e il download di patch per l'utilizzo di uno strumento di amministrazione è un carico operativo per i clienti che, a sua volta, comporta un aumento dei costi operativi.

  - Man mano che diventa sempre più mobile della forza lavoro IT, i clienti intendeva siano in grado di gestire i propri ambienti da qualsiasi luogo, non solo dal desktop e server in cui sono installati i propri strumenti di amministrazione.

  - Utilizzo degli strumenti più per le opzioni di distribuzione diversi diventa confusione e comporta un aumento dei costi operativi e formazione

## È la registrazione di PowerShell e l'esposizione cmdlet punta EAC?

Ci sono state anticipati feedback dei clienti su queste e valutano la possibilità di indirizzamento seguente in un aggiornamento futuro.

## EMC essere reintrodotto un prossimo service pack?

No. È completamente supportata l'esperienza EAC.

## È possibile utilizzare Exchange 2010 EMC per gestire gli oggetti di Exchange 2013?

No. È possibile utilizzare Exchange 2010 EMC per gestire gli oggetti Exchange 2013 e server. Mentre i clienti l'aggiornamento a Exchange 2013, Microsoft incoraggia loro di utilizzare EAC per:

1.  Gestire le cassette postali Exchange 2013, server e servizi corrispondenti.

2.  Visualizzare e aggiornare le proprietà e le cassette postali di Exchange 2010.

3.  Visualizzare e aggiornare le proprietà e le cassette postali di Exchange 2007.

Si consiglia di utilizzare Exchange 2010 EMC per creare e gestire le cassette postali di Exchange 2010.

Si consiglia di utilizzare Exchange 2007 EMC per creare e gestire le cassette postali di Exchange 2007.

I clienti possono continuare a eseguire attività di gestione utilizzando le attività di script di Exchange Management Shell.

## Perché non è la casella di ricerca sempre visibile?

Durante i principi di progettazione per Exchange 2013, volevamo consentono di assicurarsi che non si trovino nella come fino a quando non è necessario. Questa semplicità è rappresentata in tutti i nostri degli utenti finali (inclusa l'interfaccia di amministrazione di Exchange). Dopo aver fatto clic sull'icona, la casella di ricerca scorre verso l'esterno. Sono disponibili più spazio per l'utente digitare le query in casella di testo e include inoltre udinesi tipo che consentono di visualizzare una volta che si verifica in tempo reale query corrispondente. Questo miglioramento consente di nascondere inutili complessità senza ridurne l'esperienza di gestione. Si continuerà a migliorare tutti i nostri esperienze in base ai suggerimenti.

## Il valore EAC funzionerà su Tablet?

Amministrazione tramite Tablet e i dispositivi mobili non è supportato in questa fase.

## Perché Exchange 2010 ECP aprire quando si tenta di accedere a Exchange 2013 EAC?

Se la cassetta postale esistente in un server cassette postali Exchange 2010, viene automaticamente caricato il ECP di Exchange 2010 nel browser. Questo è per impostazione predefinita. È possibile accedere tramite EAC aggiungendo la versione di Exchange per l'URL. Ad esempio, per accedere alla directory virtuale di cui è ospitato sul server Accesso Client CAS01 NA EAC, utilizzare l'URL seguente: `https://CAS01-NA/ecp?ExchClientVer=15`.

## Definire i limiti in cui possono essere utilizzati tramite EAC

Per limitare Internet e accesso intranet, Exchange fornisce il partizionamento a livello di directory virtuali in IIS. Gli amministratori possono in modo esplicito Consenti o Nega gli scenari di gestione IT venga eseguita dal client internet esterni (ad esempio, da client non appartenente a un dominio all'interno del firewall aziendale). Per ulteriori informazioni, vedere [Disattivare l'accesso all'interfaccia di amministrazione di Exchange](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

## Novità per la casella degli strumenti di Exchange 2013?

In Exchange 2007 ed Exchange 2010, EMC contenuto casella degli strumenti che possono accedere a diversi strumenti per la gestione dell'organizzazione di Exchange. Casella degli strumenti di Exchange 2013 è notevolmente ridotto rispetto alle versioni precedenti. L'Editor di modelli di informazioni dettagliate, analizzatore connettività remota e il Visualizzatore code sono ancora disponibili nella casella degli strumenti di Exchange 2013. Gli strumenti rimanenti sono stati reimpiegati o spostati in EAC.

Nella tabella seguente sono elencate le modifiche alla casella degli strumenti di Exchange 2013:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Strumento</th>
<th>Dove è ora?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Best Practices Analyzer (ExBPA)</p></td>
<td><p>ExBPA è stato rimosso. Verifiche di conformità sono stata sostituita da ExBPA per assicurarsi che la foresta di Active Directory e i server di Exchange siano pronti per Exchange 2013. Ogni argomento di controllo di preparazione descritte le azioni che è possibile eseguire per risolvere i problemi che si trovano quando vengono eseguite le verifiche di conformità. Eseguire solo le procedure descritte in un argomento di controllo di preparazione di verifica della preparazione è stato visualizzato durante l'installazione.</p></td>
</tr>
<tr class="even">
<td><p>Risoluzione dei problemi del flusso di posta elettronica</p></td>
<td><p>Risoluzione dei problemi del flusso di posta elettronica è stato rimosso. È possibile utilizzare la funzione di rilevamento di messaggistica immediata in EAC. Andare a <strong>flusso di posta</strong> &gt; <strong>rapporti di recapito</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Performance Monitor</p></td>
<td><p>Performance Monitor è stato rimosso dalla casella degli strumenti. È comunque possibile trovare il monitoraggio delle prestazioni in <strong>Strumenti di amministrazione</strong> in Windows Server 2008 e Windows Server 2012.</p></td>
</tr>
<tr class="even">
<td><p>Strumento Risoluzione dei problemi di prestazioni</p></td>
<td><p>Risoluzione dei problemi di prestazioni è stato rimosso dalla casella degli strumenti.</p></td>
</tr>
<tr class="odd">
<td><p>Visualizzatore registri di routing</p></td>
<td><p>Il Visualizzatore Log di Routing è stato rimosso.</p></td>
</tr>
<tr class="even">
<td><p>Console Gestione cartelle pubbliche</p></td>
<td><p>Le cartelle pubbliche vengono ora gestite da in EAC. In EAC, accedere alle <strong>Cartelle pubbliche</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>Editor utente controllo di accesso basato sui ruoli</p></td>
<td><p>RBAC ora vengono gestite da in EAC. In EAC, andare a <strong>autorizzazioni</strong>.</p></td>
</tr>
</tbody>
</table>

