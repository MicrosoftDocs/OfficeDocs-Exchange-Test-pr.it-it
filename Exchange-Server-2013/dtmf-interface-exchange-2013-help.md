---
title: 'Interfaccia DTMF: Exchange 2013 Help'
TOCTitle: Interfaccia DTMF
ms:assetid: 2c7c9d8a-ed12-4dcf-a5b7-3cea0e785e49
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996919(v=EXCHG.150)
ms:contentKeyID: 54652835
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interfaccia DTMF

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Nella messaggistica unificata, i chiamanti possono utilizzare la multifrequenza (DTMF), nota anche come composizione a toni, e input vocali per interagire con il sistema. I metodi utilizzati dai chiamanti dipendono dalla configurazione dei dial plan e degli operatori automatici di messaggistica unificata.

L'interfaccia DTMF consente ai chiamanti di utilizzare la tastiera del telefono per individuare gli utenti e di spostarsi all'interno del sistema di menu della posta vocale di messaggistica unificata per le chiamate verso il numero di Outlook Voice Access configurato per il dial plan o verso un numero di telefono configurato per l'operatore automatico. In questo argomento viene descritta l'interfaccia DTMF e il suo utilizzo da parte dei chiamanti per individuare gli utenti e spostarsi all'interno del sistema di menu della casella vocale di messaggistica unificata.

**Sommario**

DTMF overview

UM dial plans and dial by name

DTMF maps

DTMF maps for users who aren't enabled for Unified Messaging

DTMF maps for users who are enabled for Unified Messaging

For more information

## Panoramica su DTMF

In DTMF, il chiamante deve premere un tasto sulla tastiera del telefono corrispondente a un'opzione del menu di messaggistica unificata o inserire il nome di un utente utilizzando le lettere presenti sui tasti per specificare il nome o l'alias di posta elettronica dell'utente. I chiamanti possono utilizzare DTMF perché il riconoscimento vocale automatico (ASR) non è stato abilitato o perché il tentativo di utilizzare i comandi vocali non è riuscito. In entrambi i casi, gli input DTMF vengono utilizzati per spostarsi all'interno dei menu e cercare gli utenti.

Per impostazione predefinita, nella messaggistica unificata, gli input DTMF vengono utilizzati nei dial plan e rappresentano l'interfaccia predefinita dei chiamanti per gli operatori automatici di messaggistica unificata.

I chiamanti possono utilizzare gli input DTMF per:

  - Accedere in remoto al dial plan mediante Outlook Voice Access.

  - Individuare la directory del dial plan e gli utenti.

  - Operatori automatici non abilitati al servizio di sintesi vocale.

  - Operatori automatici abilitati al servizio di sintesi vocale per i quali è stato o non è stato configurato un fallback del segnale multifrequenza (DTMF).

  - Operatori automatici per il fallback del segnale multifrequenza DTMF (non abilitati al servizio di sintesi vocale).

## Dial plan di messaggistica unificata e composizione per nome

Quando si crea un dial plan di messaggistica unificata, è possibile configurare il metodo di input principale e secondario che i chiamanti utilizzeranno per la ricerca dei nomi quando cercano o contattano un utente. Queste impostazioni si trovano nella pagina **Impostazioni** del dial plan e vengono chiamate **Modalità principale di ricerca dei nomi** e **Modalità secondaria di ricerca dei nomi**. Le seguenti opzioni sono disponibili per entrambe le modalità di ricerca dei nomi:

  - Cognome Nome

  - Nome cognome

  - Indirizzo SMTP

Inoltre, per la modalità secondaria di ricerca dei nomi, è disponibile l'opzione **Nessuno**.

Per impostazione predefinita, **Cognome Nome** è selezionata come modalità principale di ricerca dei nomi e dell'**indirizzo SMTP**. Pertanto, quando un chiamante compone un numero di Outlook Voice Access configurato nel dial plan di messaggistica unificata, risponderà l'operatore del dial plan con un messaggio di benvenuto simile a "Benvenuti in Contoso Outlook Voice Access. Per accedere alla propria cassetta postale, immettere l'interno. Per contattare qualcuno, premere il tasto cancelletto". Una volta premuto il tasto \#, il sistema risponde con "Specificare il nome della persona chiamata, iniziando dal cognome oppure per specificare l'alias di posta elettronica, premere due volte il tasto cancelletto". In questo scenario, in base alla configurazione del dial plan, al chiamante viene richiesto di immettere prima il cognome dell'utente e quindi il nome (Cognome Nome) o di specificare l'alias di posta elettronica, escludendo il nome di dominio. Ad esempio, se l'alias di posta elettronica dell'utente è tsmith@contoso.com, il chiamante dovrà immettere tsmith.

Se si desidera modificare la configurazione predefinita perché non soddisfa le proprie esigenze, è possibile modificarla per consentire ai chiamanti di immettere prima l'alias di posta elettronica dell'utente o il nome dell'utente seguito dal cognome. In questo caso, la **Modalità principale di ricerca dei nomi** viene configurata con l'impostazione **Indirizzo SMTP** e la **Modalità secondaria di ricerca dei nomi** con l'impostazione **Nome Cognome**. Le impostazioni dei metodi di composizione per nome saranno anche applicate agli operatori automatici di messaggistica unificata associati al dial plan. Per consentire ai chiamanti di immettere il nome dell'utente utilizzando gli input DTMF o i tasti sulla tastiera del telefono, deve esistere una mappa DTMF con i valori dell'utente nella directory della propria organizzazione.

Per ulteriori informazioni su come modificare il metodo principale e secondario di composizione per nome per un dial plan di messaggistica unificata, vedere [Configurare il mezzo principale per Outlook Voice Access la ricerca](configure-the-primary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md) e [Configurare la modalità secondaria per Outlook Voice Access la ricerca](configure-the-secondary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md).

Inizio pagina

## Mappe DTMF

In un'organizzazione di Exchange, l'attributo denominato **msExchUMDtmfMap** viene associato a ogni utente creato nella directory. La messaggistica unificata utilizza questo attributo per associare il nome e cognome dell'utente e l'alias di posta elettronica a un insieme di numeri. Questa associazione viene definita mappa DTMF. Una mappa DTMF consente al chiamante di immettere le cifre che corrispondono alle lettere del nome o dell'alias di posta elettronica dell'utente sulla tastiera del telefono. Questo attributo contiene i valori necessari per creare una mappa DTMF per il nome dell'utente seguito dal cognome, per il cognome dell'utente seguito dal nome e per l'alias di posta elettronica dell'utente.

Nella seguente tabella vengono mostrati i valori della mappa DTMF archiviati in Active Directory per l'attributo **msExchUMDtmfMap** dell'utente abilitato alla messaggistica unificata denominato Paolo Rossi con l'alias tsmith@contoso.com.

**Valori DTMF archiviati per l'utente abilitato alla messaggistica unificata denominato Tony Smith**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Voce di directory</th>
<th>Nome dell'utente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>firstNameLastName:866976484</p></li>
</ul></td>
<td><p>tonysmith</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>lastNameFirstName:764848669</p></li>
</ul></td>
<td><p>smithtony</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>emailAddress:876484</p></li>
</ul></td>
<td><p>tsmith</p></td>
</tr>
</tbody>
</table>


I nomi e gli alias di posta elettronica possono contenere altri caratteri non alfanumerici, quali virgole, trattini, caratteri di sottolineatura o punti che non verranno utilizzati nella mappa DTMF di un utente. Ad esempio, se l'alias di posta elettronica per Tony Smith è tony-smith@contoso.com, il valore della mappa DTMF sarà 866976484 e il trattino non verrà incluso. Tuttavia, se l'alias di posta elettronica di un utente contiene uno o più numeri, ad esempio tonysmith123@contoso.com, i numeri verranno utilizzati nella mappa DTMF creata. La mappa DTMF per tonysmith123 sarà 866976484123.

Per consentire ai chiamanti di immettere il nome o l'alias di posta elettronica dell'utente, è necessaria la mappa DTMF dell'utente. Tuttavia, non per tutti gli utenti esiste una mappa DTMF associata al relativo account utente.

Inizio pagina

## Mappe DTMF per utenti non abilitati alla messaggistica unificata

Per impostazione predefinita, gli utenti, compresi gli utenti abilitati alla cassetta postale, non sono abilitati alla messaggistica unificata. L'attributo **msExchUMDtmfMap** viene compilato con i valori richiesti delle mappe DTMF per gli utenti non abilitati alla messaggistica unificata. Per impostazione predefinita, le seguenti mappe DTMF vengono create per tutti gli utenti quando viene creata una cassetta postale:

1.  emailAddress

2.  firstNameLastName

3.  lastNameFirstName

Se non sono stati definiti i valori della mappa DTMF dei relativi account utente, i chiamanti non saranno in grado di contattarli premendo un tasto del telefono dal menu dell'operatore automatico di messaggistica unificata o di eseguire una ricerca nella directory. Inoltre, gli utenti abilitati alla messaggistica unificata non potranno inviare messaggi o trasferire le chiamate agli utenti che non dispongono di una mappa DTMF, a meno che non utilizzino il riconoscimento vocale automatico (ASR). Per consentire ai chiamanti di trasferire le chiamate o di contattare gli utenti non abilitati alla messaggistica unificata utilizzando la tastiera del telefono, è necessario creare i valori richiesti per la mappa DTMF degli utenti. È possibile utilizzare il cmdlet **Set-User** con il parametro *-CreateDtmfMap* per creare e aggiornare la mappa DTMF di un singolo utente o per aggiornare la mappa DTMF di un utente se il nome è stato modificato dopo la creazione della mappa. È eventualmente possibile creare uno script di Exchange Management Shell utilizzando questo cmdlet per aggiornare i valori della mappa DTMF per più utenti.

Per ulteriori informazioni sul cmdlet **Set-User**, vedere [Set-User](https://technet.microsoft.com/it-it/library/aa998221\(v=exchg.150\)).

Inizio pagina

## Mappe DTMF per utenti abilitati alla messaggistica unificata

Per impostazione predefinita, la mappa DTMF viene creata per gli utenti abilitati alla messaggistica unificata. In tal modo viene consentito il trasferimento delle chiamate provenienti da chiamanti esterni a un utente abilitato alla messaggistica unificata, da utenti non abilitati alla messaggistica unificata e da altri utenti abilitati che utilizzano la tastiera del telefono per specificare il nome o l'alias di posta elettronica dell'utente.

Una volta creati i valori della mappa DTMF per un utente abilitato alla messaggistica unificata, i chiamanti possono utilizzare la funzionalità di ricerca nelle directory. I chiamanti utilizzano la ricerca nelle directory con la tastiera del telefono nei seguenti casi:

  - Per identificare o cercare un utente per le chiamate verso il numero di Outlook Voice Access.

  - Per identificare o trasferire le chiamate a un utente abilitato alla messaggistica unificata per le chiamate all'operatore automatico di messaggistica unificata.

Per ulteriori informazioni sulle modalità di abilitazione di un utente alla messaggistica unificata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

Talvolta il nome, il cognome o l'alias di posta elettronica di un utente viene modificato dopo che l'utente è stato abilitato alla messaggistica unificata. I valori della mappa DTMF dell'utente non vengono aggiornati automaticamente. Se un chiamante immette il nuovo nome o l'alias di posta elettronica dell'utente e la mappa DTMF non è stata aggiornata in base alle modifiche del nome o dell'alias di posta elettronica, il chiamante non sarà in grado di individuare l'utente nella directory, di inviare un messaggio o di trasferire le chiamate all'utente. Per aggiornare la mappa DTMF di un utente dopo l'abilitazione alla messaggistica unificata, è possibile utilizzare il cmdlet **Set-User** con il parametro *-CreateDtmfMap*. È inoltre possibile creare uno script di Exchange Management Shell utilizzando questo cmdlet per aggiornare le mappe DTMF per più utenti abilitati alla messaggistica unificata.


> [!WARNING]
> Si consiglia di non modificare manualmente i valori DTMF degli utenti utilizzando uno strumento quale ADSI Edit, poiché potrebbero verificarsi configurazioni incoerenti o altri errori. Si consiglia di utilizzare solo il cmdlet <STRONG>Set-UMService</STRONG> o <STRONG>Set-User</STRONG> per creare o aggiornare le mappe DTMF degli utenti.



## Ulteriori informazioni

[Panoramica di ADSI Edit](https://go.microsoft.com/fwlink/p/?linkid=73175)

