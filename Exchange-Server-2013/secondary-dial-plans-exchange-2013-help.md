---
title: 'Secondario plan di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Secondario plan di messaggistica unificata
ms:assetid: ecf474c2-042d-4aaf-9f5b-d5138c56ef39
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ff629383(v=EXCHG.150)
ms:contentKeyID: 54915154
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Secondario plan di messaggistica unificata

 

_**Si applica a:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-03-09_

Quando si abilita un utente per la messaggistica unificata, è necessario assegnare un numero di interno e un criterio cassetta postale di messaggistica unificata che collegherà l'utente a un dial plan di messaggistica unificata. Quando l'utente è abilitato alla messaggistica unificata, è possibile assegnare ulteriori numeri di interno per tale utente nello stesso dial plan, ma tali numeri devono essere univoci. In alcune distribuzioni, a un utente potrebbe essere assegnato lo stesso numero di interno in due dial plan separati. In questo caso, è possibile collegare l'utente a un dial plan di messaggistica unificata secondario. Questo collegamento può risultare utile, ad esempio, se l'utente dispone di due telefoni fisici o si sposta tra posizioni diverse.

**Sommario**

Panoramica

Use of secondary extensions

UM features that operate differently for secondary dial plans

## Panoramica

Quando si abilita un utente per la messaggistica unificata, è necessario definire un numero di interno e un criterio cassetta postale di messaggistica unificata che collega l'utente a un singolo dial plan di messaggistica unificata. Quando si abilita l'utente per la messaggistica unificata e tale utente è collegato a un criterio cassetta postale di messaggistica unificata collegato a un URI SIP o a un dial plani E.164, è necessario fornire anche un indirizzo IP o un numero E.164 con il numero di interno dell'utente. La messaggistica unificata utilizza il dial plan e l'interno, insieme all'indirizzo SIP o al numero E.164, per individuare l'utente quando un messaggio vocale viene inviato alla sua cassetta postale.

Se si utilizzano dial plan impostati sull'interno telefonica e occorre fornire lo stesso numero di interno per un utente, è necessario creare un dial plan secondario, abilitare l'utente alla messaggistica unificata e fornire lo stesso numero di interno per l'utente. Questo perché il numero di interno deve essere univoco in un dial plan.


> [!NOTE]
> Non è previsto alcun limite al numero di interni secondari che è possibile aggiungere a un utente abilitato alla messaggistica unificata.



Può succedere che un utente si sposti tra posizioni diverse, possieda due o più telefoni o desideri ricevere messaggi vocali in un numero di interno DID (Direct Inward Dial) e fax su un altro numero di interno DID. Per ottenere questo risultato, è necessario aggiungere un numero di interno DID alla cassetta postale dell'utente e, in alcuni casi, aggiungere un dial plan secondario.

In alcune configurazioni, dopo aver aggiunto un secondo numero di interno ad un dial plan primario o uno o più numeri di interno ad un dial plan secondario, l'utente può ricevere messaggi vocali o fax utilizzando uno o più numeri di interno. Se si desidera che le chiamate fax vengano ricevute dalla messaggistica unificata e inviate al secondo numero di interno DID, è necessario configurare l'apparecchiatura telefonica dell'organizzazione per l'inoltro delle chiamate fax al secondo numero di interno DID.

Alla cassetta postale di un utente abilitato alla messaggistica unificata può essere assegnato quanto segue:

  - Un unico numero di interno, un indirizzo SIP (Session Initiation Protocol) o un indirizzo E.164 su un unico dial plan

  - Più numeri di interno su un unico dial plan

  - Più numeri di interno su due dial plan separati

Quando un utente è abilitato alla messaggistica unificata, è necessario specificare un numero di interno e un criterio cassetta postale di messaggistica unificata. La messaggistica unificata richiede il numero di interno per identificare l'utente quando accede a Outlook Voice Access per recuperare i messaggi. Il criterio cassetta postale di messaggistica unificata contiene una raccolta di proprietà di configurazione, che messaggistica unificata applica a ogni utente abilitato per la messaggistica unificata sotto quel criterio. Il criterio cassetta postale di messaggistica unificata è simile alla \&quot;classe di servizio\&quot; presenti in altri sistemi (ad esempio, caselle vocali o PBX), nel senso che una modifica ad un valore nel criterio cassetta postale di messaggistica unificata può influenzare un grande numero di utenti associati.

Una proprietà nel criterio cassetta postale di messaggistica unificata si riferisce al dial plan di messaggistica unificata. Rappresenta un insieme di interni con funzionalità telefoniche. Il piano di numerazione di questo gruppo non consente la duplicazione dei numeri di interno.

Pertanto, il numero di interno di un utente è univoco nel dial plan di messaggistica unificata nel quale è abilitato. Infatti, la coppia dial plan di messaggistica unificata e numero di interno deve essere univoca nell'organizzazione . Questo è un modo con cui la messaggistica unificata identifica in modo univoco un utente abilitato nell'organizzazione . Utilizzando un dial plan secondario rende facile mantenere univoci i dial plan e i numeri di interno in una organizzazione. Ad esempio, si immagini una organizzazione con due dial plan: Dial Plan A e Dial Plan B. Un numero di interno dell'utente nel Dial Plan A è 55555 e, nel Dial Plan B, è 66666. Quando viene utilizzato il dial plan secondario il numero di interno dell'utente nel Dial Plan A può essere 55555 e anche il numero di interno nel Dial Plan B può essere 55555. In entrambi i casi il numero di interno dell'utente è univoco.

Nella tabella seguente vengono definiti i termini utilizzati quando si fa riferimento ai numeri di interno principali e secondari, ai numero di Outlook Voice Access e ai dial plan di messaggistica unificata.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Termine</th>
<th>Definizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>numero di interno principale</p></td>
<td><p>Il numero di interno specificato quando l'utente è stato abilitato per la messaggistica unificata.</p></td>
</tr>
<tr class="even">
<td><p>dial plan primario</p></td>
<td><p>Il dial plan di messaggistica unificata specificato quando l'utente è stato abilitato per la messaggistica unificata. L'utente abilitato per la messaggistica unificata è associato al dial plan quando l'utente è collegato ad un criterio di cassetta postale di messaggistica unificata.</p></td>
</tr>
<tr class="odd">
<td><p>Numero di Outlook Voice Access principale</p></td>
<td><p>Il numero di Outlook Voice Access utilizzato per il dial plan primario dell'utente. Le chiamate per l'utente vengono inoltrate su questo numero se non c'è risposta o se la linea è occupata. È anche il numero che l'utente chiama quando vuole accedere a Outlook Voice Access.</p></td>
</tr>
<tr class="even">
<td><p>numero di interno secondario</p></td>
<td><p>Uno o più numeri di interno che possono essere aggiunti alla configurazione di un utente abilitato per la messaggistica unificata.</p></td>
</tr>
<tr class="odd">
<td><p>dial plan secondario</p></td>
<td><p>Un dial plan di messaggistica unificata diverso dal primario in cui possono essere configurati uno o più numeri di interno secondari.</p></td>
</tr>
<tr class="even">
<td><p>Numero di Outlook Voice Access secondario</p></td>
<td><p>Il numero di Outlook Voice Access utilizzato per il dial plan secondario di un utente. Un utente può chiamare questo numero dal proprio numero di interno secondario quando vuole accedere a Outlook Voice Access.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Utilizzo dei numeri di interno secondari

Nella maggior parte delle distribuzioni viene configurato solo un numero di interno per l'utente abilitato per la messaggistica unificata. Tuttavia, esistono alcune distribuzioni avanzate che richiedono di aggiungere un numero di interno secondario agli utenti.

Quando Microsoft Lync Server viene utilizzato per Enterprise Voice, la messaggistica unificata può fornire il sistema di caselle vocali. Tuttavia, il dial plan messaggistica unificata utilizzato per Enterprise Voice deve essere un dial plan SIP URI specifico per le configurazioni di messaggistica unificata con Lync Server. In queste distribuzioni il numero di interni dell'utente viene fornito da un endpoint Microsoft Unified Communications come MicrosoftOffice Communicator, in esecuzione sul computer dell'utente o Office Communicator Phone Edition, in esecuzione su un dispositivo telefonico IP supportato. Nella maggior parte dei casi, il dial plan primario dell'utente deve essere lo stesso dial plan SIP URI utilizzato con Lync Server. Ma se l'utente richiede più numeri di interno, non è possibile aggiungere numeri di interni secondari al dial plan primario. È necessario aggiungere un dial plan secondario e quindi aggiungere un numero di interno secondario o un indirizzo proxy EUM all'utente abilitato per messaggistica unificata.

Per ulteriori informazioni sull'aggiunta, la rimozione o la modifica delle estensioni, vedere:

  - [Modificare un numero interno](change-an-extension-number-exchange-2013-help.md)

  - [Aggiungere un numero interno](add-an-extension-number-exchange-2013-help.md)

  - [Rimuovere un numero interno](remove-an-extension-number-exchange-2013-help.md)

Per modificare gli indirizzi SIP o i numeri E.164 per gli utenti di messaggistica unificata, vedere:

  - [Aggiungere un indirizzo SIP](add-a-sip-address-exchange-2013-help.md)

  - [Modificare un indirizzo SIP](change-a-sip-address-exchange-2013-help.md)

  - [Rimuovere un indirizzo SIP](remove-a-sip-address-exchange-2013-help.md)

  - [Aggiungere un numero e. 164](add-an-e-164-number-exchange-2013-help.md)

  - [Modificare un numero e. 164](change-an-e-164-number-exchange-2013-help.md)

  - [Rimuovere un numero e. 164](remove-an-e-164-number-exchange-2013-help.md)

## Risponditore automatico

La messaggistica unificata fornisce entrambe le seguenti funzioni:

  - **Risponditore automatico**   Interviene quando un utente non risponde al telefono e la messaggistica unificata prende la chiamata.

  - **Outlook Voice Access**   Utilizzata dagli utenti quando chiamano il sistema di caselle vocali per accedere alla loro cassetta postale.

Due configurazioni vengono utilizzate di frequente:

  - Un utente abilitato per la messaggistica unificata è in possesso di due numeri di interno (un primario e un secondario) nel dial plan primario. Questi numeri di interno corrispondono a due differenti apparecchi telefonici sulla scrivania dell'utente e collegati allo stesso PBX. Questi numeri diversi sono disponibili per due diversi utilizzi. In questa configurazione, il numero primario è il numero \&quot;generico\&quot; mentre il secondario è dedicato ad attività specifiche, eventualmente helpdesk o numero fax dedicato.

  - Un utente abilitato alla messaggistica unificata trascorre un periodo di tempo, forse 3 settimane su 4, nell'ufficio principale della sua azienda e il resto del tempo presso una sede distaccata. I due uffici hanno diversi PBX, e il numero di interno è univoco per ciascun PBX. In questo esempio, l'utente è configurato per avere il numero di interno primario nel dial plan primario del PBX dell'ufficio principale e un numero di interno secondario nel dial plan secondario del PBX dell'altro ufficio.

In entrambe le configurazioni, i messaggi vocali o i messaggi di notifica di chiamata senza risposta generati per entrambi i numeri di interno vengono inviati alla cassetta postale dell'utente.

## Outlook Voice Access

Si potrebbe voler consentire all'utente abilitato alla messaggistica unificata l'accesso a Outlook Voice Access da qualsiasi numero di interno, primario o secondario. Pur essendo possibile, esistono alcune restrizioni architetturali che impediscono l'identico funzionamento dai diversi numeri di interno. Per accedere a Outlook Voice Access, gli utenti abilitati alla messaggistica unificata devono procedere come segue:

1.  Chiamare un numero di Outlook Voice Access.

2.  Immettere il proprio numero di interno, se si sta chiamando da un altro numero di telefono.

3.  Immettere il proprio PIN se non si è abilitati per Enterprise Voice e si sta chiamando da un telefono Unified Communications, Office Communicator o Lync Server.

**Scenari di utilizzo**

  - **Numero di interno unico con Outlook Voice Access**   Se l'utente possiede solo un numero di interno primario, deve sempre chiamare il numero di Outlook Voice Access del proprio dial plan primario di messaggistica unificata. Se si sta chiamando dal proprio numero di interno, non viene chiesto di immettere il proprio numero di interno e verrà saltato il passo 2 dei passaggi precedenti.

  - **Due numeri di interno nel dial plan primario con Outlook Voice Access**   Se l'utente possiede solo due numeri di interno, primario e secondario, ed entrambi i numeri sono nello stesso dial plan di messaggistica unificata, deve sempre chiamare il numero di Outlook Voice Access del dial plan. Se si sta chiamando dal proprio numero di interno primario o da quello secondario, non viene chiesto di immettere il proprio numero di interno e verrà saltato il passo 2 dei passaggi precedenti. La funzionalità Outlook Voice Access avrà lo stesso comportamento, indipendentemente dal numero di interno utilizzato per l'accesso.

  - **Numeri di interno nel dial plan primario e in un dial plan secondario con Outlook Voice Access**   Se l'utente dispone solo di due numeri di interno, primario e secondario, e questi risiedono in differenti dial plan di messaggistica unificata (primario e secondario), deve chiamare il numero di Outlook Voice Access appropriato per il dial plan. Dal numero di interno primario deve chiamare il numero di Outlook Voice Access del dial plan primario, mentre dal numero di interno secondario deve chiamare il numero di Outlook Voice Access del dial plan secondario. Se ci si comporta in questo modo, non viene chiesto di immettere il proprio numero di interno e verrà saltato il passo 2 dei passaggi precedenti.
    
    Le funzionalità di Outlook Voice Access che non implicano la composizione di chiamate esterne (ad esempio \&quot;Chiama il mittente\&quot; o \&quot;Chiama ufficio\&quot;) opereranno allo stesso modo, a prescindere dall'interno utilizzato per l'accesso. Le funzionalità di Outlook Voice Access che richiedono la composizione di chiamate esterne, invece, con funzioneranno nel modo previsto quando l'utente accede al dial plan secondario, a meno che le regole di composizione in uscita non siano esattamente identiche in entrambi i dial plan. Affinchè il comportamento della composizione in uscita sia esattamente lo stesso, ci si deve assicurare che le seguenti proprietà siano configurate in modo identico sia sul dial plan primario che su quello secondario:
    
      - Codici di chiamata (accesso trunk, nazionale e internazionale)
    
      - Codici di chiamata nazionali
    
      - Regole di composizione
    
      - Nomi di gruppi di regole di composizione

Un utente abilitato alla messaggistica unificata è associato a un criterio cassetta postale di messaggistica unificata che a sua volta è collegato al dial plan primario dell'utente. Il criterio cassetta posta di messaggistica unificata associato al dial plan dell'utente abilitato per la messaggistica unificata viene applicato all'utente. Se un utente è associato ad un dial plan secondario con un secondo numero di interno nel dial plan secondario, verranno comunque applicate le impostazioni del criterio cassetta posta di messaggistica unificata associate al dial plan primario. In Outlook Voice Access, le stesse impostazioni del criterio cassetta posta di messaggistica unificata associate al dial plan primario vengono applicate se l'utente chiama sul dial plan primario o sul dial plan secondario.

Le proprietà **AllowedInCountryOrRegionGroups** e **AllowedInternationalGroups** sulla cassetta postale di messaggistica unificata contiene i nomi dei gruppi di regole di composizione configurati sulle proprietà **ConfiguredInCountryOrRegionGroups** e **ConfiguredInternationalGroups** di un dial plan di messaggistica unificata. Quando un utente abilitato alla messaggistica unificata chiama Outlook Voice Access, le regole di composizione in uscita dal criterio cassetta postale di messaggistica unificata associato al dial plan primario o secondario verranno applicate alle chiamate effettuate, a seconda del numero chiamato dall'utente, il numero di Outlook Voice Access del dial plan primario o secondario.

Ad esempio, se il dial plan primario denominato \&quot;Contoso Dial Plan 1\&quot; ha una regola di composizione denominata \&quot;US e Canada\&quot; nella sua proprietà **ConfiguredInCountryOrRegionGroups**, il criterio cassetta postale di messaggistica unificata \&quot;Contoso UM Policy 1\&quot; potrebbe contenere \&quot;US e Canada\&quot; nella sua proprietà **AllowedInCountryOrRegionGroups**. Se si vuole aggiungere un numero di interno secondario in \&quot;Contoso Dial Plan 2\&quot; per un utente in \&quot;Contoso UM Policy 2\&quot;, ci si dovrebbe assicurare che anche la proprietà **ConfiguredInCountryOrRegionGroups** di \&quot;Contoso Dial Plan 2\&quot; contenga una regola denominata \&quot;US e Canada\&quot;. In caso contrario, se l'utente accede a Outlook Voice Access dal numero di interno secondario, la messaggistica unificata non sarà in grado di trovare una regola denominata \&quot;US and Canada\&quot; nel dial plan secondario. In questo caso, la messaggistica unificata consentirà all'utente di chiamare solo i numeri consentiti per tutti i chiamanti nel dial plan secondario, che potrebbe essere più limitativo.

Inizio pagina

## Funzionalità di messaggistica unificata che operano diversamente per i dial plan secondari

Esiste un gruppo di funzionalità di messaggistica unificata che possono utilizzare il dial plan secondario ma che in determinate situazioni potrebbero non operare correttamente. È importante comprendere come ciascuna di queste funzionalità viene influenzata mentre si configura un utente abilitato per la messaggistica unificata ad utilizzare un dial plan secondario.

## Ascolta al telefono

In Outlook Web App, Ascolta al telefono utilizza il gateway IP associato al dial plan primario dell'utente per effettuare le chiamate in uscita. Applica le regole di composizione dal dial plan primario e il criterio cassetta postale di messaggistica unificata associato alla cassetta postale dell'utente.

## Ricerca nelle directory (Outlook Voice Access)

Una ricerca nell'elenco di un utente che è stato autenticato seguirà queste regole:

  - La possibilità di cercare un utente e lasciare un messaggio vocale o chiamare un utente è disponibile solo se l'utente che effettua la ricerca è abilitato per la messaggistica unificata e ha il numero di interno primario nello stesso dial plan dell'utente chiamato. In questo caso, una ricerca per nome, alias e numero di interno primario sarà in grado di localizzare l'utente. Tuttavia, una ricerca effettuata utilizzando il numero di interno secondario non localizzerà l'utente.

  - Se l'utente ricercato è abilitato per la messaggistica unificata ed ha un numero di interno secondario sul dial plan chiamato, allora la ricerca per nome, alias e numero di interno secondario sarà in grado di trovare l'utente. Tuttavia, sebbene vengano offerte alcune opzioni di lasciare un messaggio vocale o chiame il contatto, l'opzione chiama contatto non avrà successo. In questo case, la ricerca per numero di interno primario non troverà l'utente.

  - Per trovare un utente e poter effettuare una chiamata o lasciare un messaggio vocale, un utente abilitato alla messaggistica unificata deve utilizzare Outlook Voice Access tramite il numero di Outlook Voice Access del proprio dial plan primario ed effettuare la ricerca per nome, alias o numero di interno primario. Se l'utente cercato viene chiamato utilizzando il numero di Outlook Voice Access del dial plan secondario, l'utente verrà trovato solo se la ricerca viene effettuata per nome, alias o numero di interno secondario. Se viene utilizzato il numero di interno primario, sarà disponibile solo l'opzione di lasciare un messaggio vocale.

## Ricerca nelle directory (Outlook Voice Access)

Una ricerca nell'elenco di un utente che non è stato autenticato seguirà queste regole:

  - L'utente cercato verrà trovato e verrà offerta l'opzione di lasciare un messaggio vocale o chiamare l'utente solo se l'utente è abilitato per la messaggistica unificata ed ha il numero di interno primario nel dial plan chiamato. In questo caso, una ricerca per nome, alias e numero di interno primario sarà in grado di trovare l'utente. Tuttavia, una ricerca effettuata utilizzando il numero di interno secondario non troverà l'utente.

  - Se l'utente che si sta cercando è abilitato alla messaggistica unificata, dispone di un numero di interno secondario sul dial plan chiamato ed è selezionata l'opzione **Trasferimento e ricerca** \> **Consenti ai chiamati di** \> **lasciare messaggi vocali senza far squillare il telefono dell'utente**sul dial plan chiamato, è possibile trovarlo con una ricerca per nome, alias e numero di interno secondario. Tuttavia, verrà offerta al chiamante l'opzione di lasciare un messaggio vocale e non ci sarà possibilità di chiamare.

  - Per trovare un utente e poter effettuare una chiamata o lasciare un messaggio vocale, il chiamante deve comporre il numero di Outlook Voice Access del dial plan primario ed effettuare la ricerca per nome, alias e numero di interno secondario dell'utente. Se viene chiamato il numero di Outlook Voice Access secondario dell'utente, questi potrà essere trovato solo se l'opzione **Consenti ai chiamanti di effettuare la ricerca per nome o alias** è impostata su **Nell'intera organizzazione**. In questo caso, verrà offerta solo l'opzione di lasciare un messaggio vocale.

## Chiama il mittente (Outlook Voice Access)

Quando un utente chiama Outlook Voice Access e sceglie l'opzione Chiama il mittente, può inviare un messaggio di posta elettronica o un messaggio vocale a un utente abilitato alla messaggistica unificata. Le opzioni disponibili dipendono dal fatto che il chiamante sia associato allo stesso dial plan del mittente che sta chiamando. Le chiamate a un utente abilitato alla messaggistica unificata quando il chiamante compone un numero di Outlook Voice Access ed è autenticato seguiranno queste regole:

  - **Messaggi di posta elettronica   **   Se il mittente del messaggio di posta elettronica è un utente abilitato alla messaggistica unificata, scegliendo di chiamare il mittente si genererà una chiamata al numero di interno primario del mittente che è stato configurato sul dial plan primario dell'utente. Nel caso in cui il numero di interno primario del mittente sia su un dial plan diverso da quello del chiamante, la richiesta \&quot;Chiama il mittente\&quot; verrà proposta solo se per il mittente è configurato un telefono di ufficio, abitazione o cellulare e le regole di composizione sono configurate per consentire la chiamata.

  - **Messaggi vocali e di posta elettronica**   Se il chiamante è un utente abilitato per la messaggistica unificata, l'opzione per la chiamata al mittente produrrà sempre una chiamata al numero di interno utilizzato dal mittente per lasciare i messaggi vocali. Se questo numero di interno ha un numero di cifre diverso da quello del dial plan chiamato, non verrà offerta la possibilità di chiamare il mittente a meno che non siano attive regole di composizione che consentono la chiamata. Ad esempio:
    
      - L'opzione \&quot;Chiama il mittente\&quot; sarà disponibile se il mittente utilizza un numero di interno sullo stesso dial plan utilizzato per inviare i messaggi vocali.
    
      - L'opzione \&quot;Chiama il mittente\&quot; verrà fatta ascoltare se il mittente utilizza un numero di interno su un dial plan diverso da quello utilizzato con Outlook Voice Access per inviare i messaggi vocali ed entrambi i dial plan hanno lo stesso numero di cifre. L'esito della chiamata sarà positivo se il gateway IP e l'infrastruttura del PBX consentono il trasferimento di chiamata.
    
      - L'opzione \&quot;Chiama il mittente\&quot; non verrà fatta ascoltare se il mittente utilizza un numero di interno su un dial plan diverso da quello utilizzato con Outlook Voice Access per inviare i messaggi vocali ed i dial plan hanno diverso numero di cifre e non sono presenti regole di chiamate esterne che corrispondono al numero di interno del mittente.

Inizio pagina

