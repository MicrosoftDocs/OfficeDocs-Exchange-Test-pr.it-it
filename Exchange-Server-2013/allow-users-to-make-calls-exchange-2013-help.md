---
title: 'Consentire agli utenti di effettuare chiamate: Exchange 2013 Help'
TOCTitle: Consentire agli utenti di effettuare chiamate
ms:assetid: b6e696ce-c848-475b-a598-9035677497e2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232172(v=EXCHG.150)
ms:contentKeyID: 51407403
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire agli utenti di effettuare chiamate

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2015-03-09_

L'*esecuzione di chiamate esterne* è il processo tramite cui gli utenti chiamano in un dial plan di messaggistica unificata utilizzando un numero di Outlook Voice Access e collocano o trasferiscono una chiamata a un numero telefonica interno o esterno. La messaggistica unificata utilizza le impostazioni di esecuzione di chiamate esterne per comporre le chiamate per gli utenti. Per configurare l'esecuzione di chiamate esterne è necessario configurare regole di composizione, gruppi di regole di composizione e autorizzazioni di composizione nei dial plan di messaggistica unificata e autorizzare quindi l'esecuzione di chiamate esterne in dial plan di messaggistica unificata, criteri cassetta postale di messaggistica unificata e operatori automatici. È possibile, inoltre, configurare i dial plan di messaggistica unificata in modo da disporre di codici di chiamata o di accesso, di un prefisso nazionale e di formati di numeri nazionali e internazionali che consentano di controllare l'esecuzione di chiamate esterne nell'organizzazione. In questo argomento vengono illustrate le regole di composizione, i gruppi di regole di composizione e le autorizzazioni di composizione e il relativo utilizzo per autorizzare e controllare le chiamate esterne per l'organizzazione.

**Sommario**

Panoramica

Types of users

Outdialing settings

Configuring outdialing

Applying configured dialing rule groups

Applying dialing rules

## Panoramica

Le chiamate esterne avvengono quando:

  - Viene effettuata una chiamata a un numero di telefono esterno.

  - Una chiamata viene trasferita a un operatore automatico.

  - Una chiamata viene trasferita a un utente dell'organizzazione.

  - Un utente abilitato alla messaggistica unificata utilizza la funzionalità Ascolta al telefono.

Per garantire il corretto funzionamento delle chiamate esterne, è necessario configurare le seguenti impostazioni:

  - **Regole di composizione**   Indicano il numero composto dall'utente abilitato alla messaggistica unificata e il numero che verrà composto da Private Branch eXchange (PBX) o IP PBX.

  - **Gruppi di regole di composizione**   Determinano i tipi di chiamata che possono effettuare gli utenti di un gruppo di composizione.

  - **Autorizzazioni di composizione**   Determinano le restrizioni che verranno applicate per impedire agli utenti di effettuare chiamate su lunghe distanze e di ricevere addebiti per telefonate non necessarie.

Per abilitare le chiamate esterne per gli utenti che chiamano in un dial plan o un operatore automatico, è necessario:

  - Accertarsi che i gateway IP rappresentati da un gateway IP di messaggistica unificata collegato a un dial plan consenta le chiamate esterne.

  - Creare gruppi di regole di composizione creando regole di composizione nel dial plan di messaggistica unificata.

  - Aggiungere le autorizzazioni di composizione per i gruppi di regole di composizione nazionali e internazionali nel dial plan di messaggistica unificata, criterio cassetta postale di messaggistica unificata o operatore automatico associato allo stesso dial plan del gateway IP di messaggistica unificata.

## Tipi di utenti

Due tipi di utenti possono utilizzare la funzionalità di chiamata esterna nella messaggistica unificata: autenticati o non autenticati. Tutti gli utenti che chiamano un operatore automatico di messaggistica unificata non sono autenticati. Quando un utente chiama un numero di Outlook Voice Access, viene considerato non autenticato poiché non ha fornito il proprio numero di interno e il PIN e non ha effettuato l'accesso alla propria cassetta postale. Gli utenti vengono autenticati dopo aver fornito il proprio numero di interno e il PIN e avere effettuato l'accesso alla propria cassetta postale.

Quando gli utenti chiamato un numero di Outlook Voice Access configurato in un dial plan di messaggistica unificata e tentano di effettuare o trasferire una chiamata senza accedere alla propria cassetta postale, alla chiamata vengono applicate solo le impostazioni di chiamata esterna del dial plan di messaggistica unificata. Quando un utente anonimo o non autenticato chiama un operatore automatico di messaggistica unificata, vengono applicate alla chiamata sia le impostazioni per le chiamate esterne configurate per l'operatore automatico che quelle configurate nel dial plan associato all'operatore automatico.

Quando gli utenti chiamano un numero di Outlook Voice Access configurato in un dial plan e accedono alla propria cassetta postale diventano utenti autenticati. Quando gli utenti sono autenticati, le impostazioni delle chiamate esterne utilizzano le impostazioni delle regole di composizione e di autorizzazione di composizione del criterio cassetta postale di messaggistica unificata collegato a tali utenti.

Inizio pagina

## Impostazioni per le chiamate esterne

Per applicare le regole per le chiamate esterne per l'organizzazione è necessario configurare diverse impostazioni. Oltre a configurare i dial plan di messaggistica unificata, gli operatori automatici di messaggistica unificata e i criteri cassette postali di messaggistica unificata creati con le regole e le autorizzazioni di composizione corrette, è necessario configurare i codici di accesso, i prefissi numerici e i formati numerici nei dial plan di messaggistica unificata. Le seguenti impostazioni per le chiamate esterne sono configurate in base ai dial plan, agli operatori automatici e ai criteri cassetta postale di messaggistica unificata:

  - Linea esterna, codici di accesso nazionali e internazionali

  - Prefissi numeri nazionali

  - Formati numeri nazionali e internazionali

  - Configurato nei gruppi di regole di composizione nazionali e internazionali

  - Consentito nei gruppi di regole di composizione nazionali e internazionali

  - Voci delle regole di composizione

  - Autorizzazioni di composizione

Per configurare correttamente le chiamate esterne per l'organizzazione, è necessario innanzitutto capire il modo in cui ogni componente può essere utilizzato per l'esecuzione di chiamate esterne e in che modo deve essere configurato. Nella seguente tabella viene presentato ogni componente da configurare nei dial plan di messaggistica unificata, negli operatori automatici di messaggistica unificata e nei criteri cassette postali di messaggistica unificata per consentire il corretto funzionamento delle chiamate esterne.

### Componenti per l'esecuzione delle chiamate esterne

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Codici di chiamata, prefissi e formati dei numeri</p></td>
<td><p>La messaggistica unificata utilizza codici di chiamata, prefissi e formati di numeri per stabilire il numero corretto da comporre quando si effettua una chiamata esterna. È possibile configurare i codici di chiamata, i prefissi e i formati dei numeri per limitare le chiamate in uscita per gli utenti che chiamano un operatore automatico di messaggistica unificata associato a un dial plan di messaggistica unificata o per gli utenti che compongono un numero di Outlook Voice Access configurato nel dial plan.</p></td>
</tr>
<tr class="even">
<td><p>Gruppi di regole di composizione</p></td>
<td><p>I gruppi di regole di composizione vengono creati per consentire la modifica dei numeri di telefono prima che vengano inviati a PBX per le chiamate esterne. I gruppi di regole di composizione rimuovono o aggiungono cifre ai numeri di telefono da chiamare tramite la messaggistica unificata. Ad esempio, è possibile creare un gruppo di regole di composizione che consente l'aggiunta automatica del numero 9 come prefisso a un numero di telefono a 7 cifre per consentire l'accesso a una linea esterna. In questo esempio, gli utenti che effettuano chiamate in uscita non devono digitare il numero 9 prima del numero di telefono per raggiungere una persona esterna all'organizzazione.</p>
<p>Ogni gruppo di regole di composizione contiene regole di composizione che determinano i tipi di chiamate nazionali e internazionali che possono essere effettuate dagli utenti di un gruppo di regole di composizione. I gruppi di regole di composizione sono applicate agli utenti associati a un dial plan di messaggistica unificata o agli operatori automatici di messaggistica unificata e ai criteri cassetta postale di messaggistica unificata associati al dial plan. Ogni gruppo di regole di composizione deve contenere almeno una regola di composizione.</p></td>
</tr>
<tr class="odd">
<td><p>Voci delle regole di composizione</p></td>
<td><p>Una regola di composizione viene utilizzata per determinare i tipi di chiamate che possono essere effettuate dagli utenti di un gruppo di regole di composizione. Quando si crea un gruppo di regole di composizione, è necessario configurare una o più regole di composizione.</p>
<p>Per ogni regola di composizione configurata è necessario immettere il nome della regola, il modello numero da trasformare (<em>maschera del numero</em>) e il numero composto. È possibile immettere anche un commento. I commenti hanno la funzione di descrivere l'utilizzo della regola di composizione o di descrivere il gruppo di utenti a cui la regola verrà applicata. Quando si aggiunge la maschera di un numero e il numero composto a una regola di composizione, è possibile utilizzare la lettera x per sostituire una cifra in un numero di telefono, ad esempio 91425xxxxxxx. È possibile utilizzare anche il simbolo dell'asterisco (*) come carattere jolly, ad esempio 91425*.</p></td>
</tr>
<tr class="even">
<td><p>Autorizzazioni di composizione</p></td>
<td><p>Un'autorizzazione di composizione utilizza i gruppi di regole di composizione per applicare restrizioni di composizione agli utenti associati a uno specifico criterio cassetta postale, dial plan o operatore automatico di messaggistica unificata. Possono essere utilizzate anche per consentire agli utenti di effettuare chiamate a numeri di telefono nazionali o internazionali.</p>
<p>Dopo avere creato regole di composizione in base al dial plan di messaggistica unificata, aggiungere il gruppo di regole di composizione a un criterio cassetta postale, dial plan o operatore automatico di messaggistica unificata. Dopo avere effettuato questa operazione, tutte le impostazioni o regole che sono state definite verranno applicate agli utenti abilitati alla messaggistica unificata collegati al criterio cassetta postale di messaggistica unificata.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Configurazione dell'esecuzione delle chiamate esterne

Un gruppo di regole di composizione è una raccolta di una o più regole di composizione configurate in un dial plan di messaggistica unificata. È possibile configurare due tipi di gruppi di regole di composizione in un dial plan di messaggistica unificata: nazionali e internazionali. I gruppi di regole di composizione nazionali si applicano ai numeri di telefono composti nell'ambito dello stesso paese o area geografica. I gruppi di regole di composizione internazionali si applicano ai numeri di telefono internazionali composti da un paese o area geografica verso un paese o area geografica diversa.

Ogni dial plan di messaggistica unificata può contenere uno o più gruppi di regole di composizione. Per applicare un gruppo di regole di composizione a un insieme di utenti, dopo aver creato il gruppo di regole di composizione è necessario aggiungerlo all'elenco dei gruppi di regole di composizione consentiti presenti nel dial plan di messaggistica unificata, negli operatori automatici di messaggistica unificata e nei criteri cassetta postale di messaggistica unificata associati al dial plan.

I gruppi di regole di composizione consentono di specificare le regole di composizione da applicare a un gruppo di utenti abilitati alla messaggistica unificata che rientrano in una categoria specifica. Ad esempio, è possibile utilizzare i gruppi di regole di composizione per specificare quale gruppo di utenti è autorizzato a effettuare chiamate internazionali e quale gruppo può effettuare solo chiamate nazionali o locali. È possibile creare un gruppo di regole di composizione utilizzando l'interfaccia di amministrazione di Exchange (EAC) o il cmdlet **Set-UMDialPlan** in Exchange Management Shell. Quando si crea un gruppo di regole di composizione, è necessario definire almeno una regola di composizione per il gruppo.

Quando un utente compone un numero di telefono, la messaggistica unificata cerca una corrispondenza tra il numero e le regole di composizione. Se la corrispondenza viene trovata, la messaggistica unificata utilizza la regola di composizione per stabilire il numero da comporre esaminando il numero telefonico o le cifre elencate nella sezione **Numero chiamato** della regola di composizione. Il numero riportato nella casella **Numero composto** della regola di composizione verrà composto.

Nella seguente tabella viene illustrato un esempio di gruppi di regole di composizione e di regole di composizione. In questo esempio, i gruppi di regole di composizione che sono stati creati sono Local-Calls-Only e Low-Rate. Il gruppo di regole di composizione Local-Calls-Only contiene due regole di composizione: 91425\* e 91206\*. Anche i gruppo di regole di composizione Low-Rate contiene due regole di composizione: 91509\* e 91360\*.

### Gruppi di regole di composizione e regole di composizione

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>NumberMask</th>
<th>DialedNumber</th>
<th>Commento</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Solo chiamate locali</p></td>
<td><p>91425*</p></td>
<td><p>91*</p></td>
<td><p>Chiamate locali</p></td>
</tr>
<tr class="even">
<td><p>Solo chiamate locali</p></td>
<td><p>91206*</p></td>
<td><p>91*</p></td>
<td><p>Chiamate locali</p></td>
</tr>
<tr class="odd">
<td><p>Tariffa economica</p></td>
<td><p>91509*</p></td>
<td><p>9*</p></td>
<td><p>Chiamate nazionali</p></td>
</tr>
<tr class="even">
<td><p>Tariffa economica</p></td>
<td><p>91360*</p></td>
<td><p>9*</p></td>
<td><p>Chiamate nazionali</p></td>
</tr>
</tbody>
</table>


Ad esempio., quando un utente compone il numero 9-1-425-555-1234, la messaggistica unificata compone il numero 4255551234 perché rimuove tutti i caratteri non numerici (in questo esempio i trattini) e applica la maschera del numero indicata nella regola di composizione. In questo esempio, viene applicata la maschera del numero 91\*. La maschera indicherà al servizio di messaggistica unificata di non comporre il numero 9 o il numero 1, ma di comporre tutte le altre cifre del numero di telefono che si trovano alla destra del numero 1, tra cui tutti i numeri rappresentati dall'asterisco (\*).

È possibile EAC o Shell per creare e configurare uno o più gruppi e regole di composizione nazionali e internazionali. Tuttavia, se si creano diversi gruppi e regole di composizione o gruppi e regole complessi, è possibile utilizzare un file CSV (Comma-Separated Value) in Shell. È possibile importare o esportare un elenco di gruppi di regole di composizione e di regole di composizione.

Per importare un elenco di gruppi e di regole di composizione definiti in un file CSV, eseguire il cmdlet **Set-UMDialPlan** come segue:

    Set-UMDialPlan "MyUMDialPlan" -ConfiguredInCountryOrRegionGroups $(IMPORT-CSV c:\dialrules\InCountryRegion.csv)

Per recuperare un elenco di gruppi di regole di composizione configurati in un dial plan di messaggistica unificata, eseguire il cmdlet **Get-UMDialPlan** come indicato di seguito.

    (Get-UMDialPlan -id "MyUMDialPlan").ConfiguredInCountryOrRegionGroups | EXPORT-CSV C:\incountryorregion.csv

Il file CSV deve essere creato e salvato nel formato corretto. Ogni riga del file CSV rappresenta una regola di composizione. Tuttavia, ogni regola di composizione è configurata nello stesso gruppo di regole di composizione. Ogni regola presente nel file conterrà quattro sezioni separate da virgole: nome, maschera del numero, numero composto e commento. Tutte le sezioni sono obbligatorie ed è necessario immettere le informazioni corrette in ogni sezione, ad eccezione della sezione relativa al commento. Non devono essere inseriti spazi fra il testo immesso e la virgola per la sezione successiva, né righe vuote tra le regole o alla fine. Di seguito viene riportato un esempio di file CSV che è possibile utilizzare per creare gruppi e di regole e regole di composizione nazionali.

**Name,NumberMask,DialedNumber,Comment**

**Low-rate,91425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9xxxxxxx,9xxxxxxx,Local call**

**Any,91\*,91\*,Open access to in-country/region numbers**

**Long-distance,91408\*,91408\*,long distance**

Di seguito viene riportato un esempio di file CSV che è possibile utilizzare per creare gruppi e voci di regole di composizione internazionali.

**Name,NumberMask,DialedNumber,Comment**

**International, 901144\*, 901144\*, international call**

**International, 901133\*, 901133\*, international call**

Inizio pagina

## Applicazione dei gruppi di regole di composizione configurati

I gruppi di regole di composizione vengono creati in un dial plan di messaggistica unificata. È possibile creare gruppi di regole di composizione nazionali o internazionali utilizzando EAC o il cmdlet **Set-UMDialPlan** in Shell. Una volta creati i gruppi di regole di composizione appropriati in un dial plan di messaggistica unificata e definite le regole di composizione, è possibile applicare i gruppi di regole creati a un dial plan di messaggistica unificata, a un operatore automatico di messaggistica unificata o agli utenti associati a un criterio cassetta postale di messaggistica unificata, a seconda della modalità di accesso dell'utente al sistema di caselle vocali.

È possibile applicare ai seguenti elementi i gruppi di regole di composizione creati in un dial plan di messaggistica unificata:

  - **Stesso dial plan**   Le impostazioni verranno applicate a tutti gli utenti che chiamano un numero Outlook Voice Access ma non accedono alla propria cassetta postale. Per applicare un gruppo di regole di composizione nazionale denominato `MyAllowedDialRuleGroup` allo stesso dial plan, utilizzare il cmdlet di **Set-UMDialPlan** di Shell come indicato di seguito.
    
        Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Uno o più criteri cassetta postale di messaggistica unificata  **Le impostazioni configurate in un criterio cassetta postale di messaggistica unificata verranno applicate a tutti gli utenti collegati a tale criterio cassetta postale di messaggistica unificata. Le impostazioni configurate in un criterio cassetta postale di messaggistica unificata vengono applicate agli utenti che chiamano un numero Outlook Voice Access e accedono alla propria cassetta postale. Per applicare un gruppo di regole di composizione nazionale denominato `MyAllowedDialRuleGroup` a un singolo criterio cassetta postale di messaggistica unificata, utilizzare la scheda **Autorizzazione di composizione** nell'interfaccia di amministrazione di Exchange o il cmdlet **Set-UMMailboxPolicy** in Shell, come indicato di seguito.
    
        Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Uno o più operatori automatici associati al dial plan di messaggistica unificata**   Verrà applicato a tutti gli utenti che chiamano un operatore automatico di messaggistica unificata. Per applicare il gruppo di regole di composizione nazionale denominato `MyAllowedDialRuleGroup` a un singolo operatore automatico di messaggistica unificata, utilizzare la pagina **Autorizzazione di composizione** dell'operatore automatico in EAC o il cmdlet **Set-UMAutoAttendant** in Shell, come indicato di seguito.
    
        Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

Nella seguente tabella sono riepilogate le modalità di applicazione dei gruppi di regole di composizione nella messaggistica unificata.

### Applicazione delle regole relative alle chiamate esterne

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di chiamante</th>
<th>Ambito</th>
<th>Impostazioni applicate per le chiamate esterne</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Numero di Outlook Voice Access</p></td>
<td><p>L'utente chiama un numero di Outlook Voice Access del dial plan e accede alla propria cassetta postale</p></td>
<td><p>Criterio cassetta postale di messaggistica unificata</p></td>
</tr>
<tr class="even">
<td><p>Chiamante anonimo</p></td>
<td><p>L'utente chiama un numero di Outlook Voice Access del dial plan</p></td>
<td><p>Dial plan di messaggistica unificata</p></td>
</tr>
<tr class="odd">
<td><p>Chiamante anonimo</p></td>
<td><p>L'utente chiama un numero pilota dell'operatore automatico o un numero di interno</p></td>
<td><p>Operatore automatico di messaggistica unificata</p></td>
</tr>
<tr class="even">
<td><p>Chiamante all'interno dell'organizzazione</p></td>
<td><p>L'utente chiama il numero di Ascolta al telefono</p></td>
<td><p>Criterio cassetta postale di messaggistica unificata</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Applicazione delle regole di composizione

Il processo di esecuzione delle chiamate esterne viene attivato quando:

  - Il servizio di messaggistica unificata effettua una chiamata a un numero di telefono esterno per un chiamante.

  - Il servizio di messaggistica unificata trasferisce la chiamata a un operatore automatico.

  - Il servizio di messaggistica unificata trasferisce una chiamata a un utente dell'organizzazione.

  - Un utente abilitato alla messaggistica unificata utilizza la funzionalità Ascolta al telefono.

In ogni scenario di esecuzione delle chiamate esterne, il servizio di messaggistica unificata applica le regole di composizione configurate ed effettua la chiamata per l'utente. Tuttavia, a seconda dello scenario a del modo con cui la chiamata è stata avviata dall'utente, il servizio di messaggistica unificata potrebbe applicare solo alcune regole di composizione al numero di telefono composto. In altri scenari di esecuzione delle chiamate esterne, il servizio di messaggistica unificata potrebbe applicare al numero di telefono composto tutte le regole per le chiamate esterne che sono state configurate.

Inizio pagina

