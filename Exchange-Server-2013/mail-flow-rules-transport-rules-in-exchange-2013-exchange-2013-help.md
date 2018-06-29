---
title: 'Regole del flusso di posta o di trasporto: Exchange 2013 Help'
TOCTitle: Regole del flusso di posta (regole di trasporto)
ms:assetid: c3d2031c-fb7b-4866-8ae1-32928d0138ef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351127(v=EXCHG.150)
ms:contentKeyID: 50481608
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Regole del flusso di posta o di trasporto

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-04-28_

È possibile utilizzare le regole del flusso di posta elettronica (noto anche come regole di trasporto) per identificare ed esegue azioni sui messaggi che passano attraverso l'organizzazione Exchange 2013. Regole del flusso di posta elettronica sono simili alle regole posta in arrivo disponibili in Outlook e Outlook Web App. La differenza principale è regole del flusso di posta elettronica eseguire l'azione necessaria messaggi mentre sono in corso e non dopo che il messaggio viene recapitato alla cassetta postale. Regole del flusso di posta elettronica è incluso un unica offerta più ricca condizioni, eccezioni e azioni, che comprende la flessibilità necessaria per implementare molti altri tipi di criteri di messaggistica.

In questo articolo sono illustrati i componenti delle regole del flusso di posta e il loro funzionamento.

È possibile utilizzare Interfaccia di amministrazione di Exchange (EAC) o Exchange Management Shell per gestire le regole del flusso di posta elettronica. Per istruzioni su come gestire le regole di trasporto, vedere [Gestire le regole di flusso di posta elettronica](manage-mail-flow-rules-exchange-2013-help.md).

Per ciascuna regola è possibile applicare, verificare o testare e inviare una notifica al mittente. Per ulteriori informazioni sulle opzioni di verifica, vedere [Testare una regola del flusso di posta elettronica](test-a-mail-flow-rule-exchange-2013-help.md) e [Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).

Per implementare criteri specifici messaggistica utilizzando regole del flusso di posta elettronica, vedere i seguenti argomenti:

  - [Utilizzare le regole di trasporto per esaminare messaggi con allegati](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [Scenari comuni relativi al blocco degli allegati](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)

  - [Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità per tutta l'organizzazione](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [Utilizzare le regole di flusso di posta elettronica in modo che i messaggi possono ignorare confusione](use-mail-flow-rules-so-messages-can-bypass-clutter-exchange-2013-help.md)

  - [Utilizzare regole del flusso di posta per instradare le e-mail in base a un elenco di parole, frasi o motivi](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)

  - [Scenari comuni di approvazione messaggio](common-message-approval-scenarios-exchange-2013-help.md)

## Componenti delle regole di trasporto

UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_TransportRules\_Components\_Intro)

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_TransportRule\_Conditions\_Intro)
    
    Per un elenco completo delle condizioni delle regole del flusso di posta elettronica, vedere [Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md). L'elenco delle condizioni è disponibile anche nella finestra di dialogo **del flusso della posta** in EAC. Se si utilizza il Exchange Management Shell, utilizzando il cmdlet [Get-TransportRulePredicate](https://technet.microsoft.com/it-it/library/aa997151\(v=exchg.150\)) per recuperare l'elenco delle condizioni.

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_TransportRules\_Exceptions)

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_TransportRules\_Actions\_Intro)
    
    Per un elenco completo delle azioni delle regole di trasporto disponibili, vedere [Azioni della regola di trasporto](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md). Elenco delle azioni è disponibile anche nella finestra di dialogo **del flusso della posta** in EAC. Se si utilizza Shell, è possibile recuperare l'elenco delle operazioni tramite il cmdlet [Get-TransportRuleAction](https://technet.microsoft.com/it-it/library/aa998551\(v=exchg.150\)) .

  - Nella tabella seguente vengono descritte le proprietà della regola che sono disponibili nelle regole di flusso della posta.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Nome proprietà nell'interfaccia di amministrazione di Exchange</th>
    <th>Nome parametro in PowerShell</th>
    <th>Descrizione</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Priorità</strong></p></td>
    <td><p><em>Priority</em></p></td>
    <td><p>Indica in che ordine le regole vengono applicate ai messaggi. La priorità predefinita si basa sul momento di creazione della regola; le regole meno recenti hanno una priorità superiore rispetto a quelle più nuove, mentre le regole con priorità superiore vengono elaborate prima delle regole con priorità inferiore.</p>
    <p>La priorità della regola vengono modificate nell'interfaccia di amministrazione di Exchange spostando la regola verso l'alto o verso il basso nell'elenco delle regole. In PowerShell, impostare il numero di priorità (0 è la priorità più alta).</p>
    <p>Ad esempio, in caso di una regola per rifiutare i messaggi che includono un numero di carta di credito e un'altra che richiede l'approvazione, è possibile far applicare per prima la regola per il rifiuto e interrompere l'applicazione delle altre regole.</p>
    <p>Per ulteriori informazioni, vedere <a href="manage-mail-flow-rules-exchange-2013-help.md">Impostare le priorità delle regole del flusso di posta</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Modalità</strong></p></td>
    <td><p><em>Mode</em></p></td>
    <td><p>È possibile specificare se la regola deve elaborare i messaggi immediatamente oppure se le regole devono essere testate senza coinvolgere il recapito del messaggio (con o senza suggerimenti sui criteri DLP).</p>
    <p>I suggerimenti per i criteri presentano una breve nota in Outlook o Outlook sul Web nella quale sono riportate informazioni sulle possibili violazioni del criterio indirizzate alla persona che sta creando il messaggio. Per ulteriori informazioni, vedere <a href="technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md">Suggerimenti per i criteri</a>.</p>
    <p>Per ulteriori informazioni sulle modalità, vedere <a href="test-a-mail-flow-rule-exchange-2013-help.md">Testare una regola del flusso di posta elettronica</a>.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Attiva la regola in data</strong></p>
    <p><strong>Disattiva la regola in data</strong></p></td>
    <td><p><em>ActivationDate</em></p>
    <p><em>ExpiryDate</em></p></td>
    <td><p>Specifica l'intervallo di date in cui la data è attiva.</p></td>
    </tr>
    <tr class="even">
    <td><p>Casella di controllo <strong>On</strong> selezionata o deselezionata</p></td>
    <td><p>Nuove regole: parametro <em>Enabled</em> nel cmdlet <strong>New-TransportRule</strong>.</p>
    <p>Regole esistenti: Utilizzare il cmdlet <strong>Enable-TransportRule</strong> o <strong>Disable-TransportRule</strong>.</p>
    <p>Il valore viene visualizzato nella proprietà <strong>State</strong> della regola.</p></td>
    <td><p>È possibile creare una regola disabilitata e abilitarla successivamente, quando l'utente è pronto per sottoporla a test. In alternativa, è possibile disabilitare una regola senza eliminarla per preservare le impostazioni.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Rimanda il messaggio se l'elaborazione della regola non può essere completata</strong></p></td>
    <td><p><em>RuleErrorAction</em></p></td>
    <td><p>È possibile specificare in che modo bisogna gestire il messaggio, se l'elaborazione della regola non può essere completata. Per impostazione predefinita, la regola sarà ignorata, ma è possibile scegliere di inviare di nuovo il messaggio per l'elaborazione.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Trova l'indirizzo del mittente nella parte seguente del messaggio</strong></p></td>
    <td><p><em>SenderAddressLocation</em></p></td>
    <td><p>Se la regola usa condizioni o eccezioni che esaminano l'indirizzo e-mail del mittente, è possibile cercare il valore nell'intestazione del messaggio, nella busta del messaggio o in entrambi i punti.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Arrestare l'elaborazione di più regole</strong></p></td>
    <td><p><em>SenderAddressLocation</em></p></td>
    <td><p>Si tratta di un'azione per la regola, ma ha l'aspetto di una proprietà nell'interfaccia di amministrazione di Exchange. È possibile scegliere di interrompere l'applicazione di ulteriori regole a un messaggio dopo che una regola elabora un messaggio.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Commenti</strong></p></td>
    <td><p><em>Comments</em></p></td>
    <td><p>È possibile immettere commenti descrittivi sulla regola.</p></td>
    </tr>
    </tbody>
    </table>


## Più condizioni, eccezioni e azioni

Nella tabella seguente è illustrato come in una regola vengono gestite più condizioni, valori della condizione, eccezioni e azioni.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Logica</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Più condizioni</p></td>
<td><p>E</p></td>
<td><p>Un messaggio deve corrispondere a tutte le condizioni della regola. Se occorre una condizione di corrispondenza o un'altra, è possibile utilizzare regole distinte per ogni condizione. Ad esempio, per aggiungere la stessa dichiarazione di non responsabilità nei messaggi con allegati e nei messaggi con testo specifico, è possibile creare una regola per ogni condizione. Nell'interfaccia di amministrazione di Exchange, è possibile copiare facilmente una regola.</p></td>
</tr>
<tr class="even">
<td><p>Una condizione con più valori</p></td>
<td><p>OPPURE</p></td>
<td><p>Le stesse condizioni consentono di specificare più valori. Il messaggio deve corrispondere a uno qualsiasi (non tutti) dei valori specificati. Ad esempio, se in un messaggio di posta elettronica l'oggetto è <strong>Informazioni sul prezzo delle azioni</strong> e la condizione <strong>L'oggetto include una o più parole seguenti</strong> è configurata per la corrispondenza alle parole <strong>Contoso</strong> o <strong>azioni</strong>, la condizione è soddisfatta perché l'oggetto contiene almeno uno dei valori specificati.</p></td>
</tr>
<tr class="odd">
<td><p>Più eccezioni</p></td>
<td><p>OPPURE</p></td>
<td><p>Se un messaggio corrisponde a una qualsiasi delle eccezioni, le azioni non vengono applicate al messaggio. Quest'ultimo non deve necessariamente corrispondere a tutte le eccezioni.</p></td>
</tr>
<tr class="even">
<td><p>Più azioni</p></td>
<td><p>E</p></td>
<td><p>I messaggi che corrispondono alle condizioni di una regola prendono tutte le azioni che sono specificate dalla regola. Ad esempio, se vengono selezionate le azioni <strong>Anteponi all'oggetto del messaggio</strong> e <strong>Aggiungi destinatari alla casella Ccn</strong>, verranno applicate entrambe al messaggio.</p>
<p>Tenere presente che alcune azioni come <strong>Elimina il messaggio senza inviare alcuna notifica</strong> impediscono l'applicazione a un messaggio delle regole successive. Altre azioni quali <strong>Inoltra il messaggio</strong> non consentono azioni aggiuntive.</p>
<p>È inoltre possibile impostare un'azione su una regola in modo che quando quella regola viene applicata, le regole successive non vengono applicate al messaggio.</p></td>
</tr>
</tbody>
</table>


Torna all'inizio

## Proprietà delle regole di trasporto

UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_TransportRule\_Properties)

Torna all'inizio

## Modalità di applicazione delle regole di trasporto

UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_TransportRule\_HowApplied)

Torna all'inizio

## Differenze di elaborazione in base al tipo di messaggio

Esistono diversi tipi di messaggi che passano attraverso un'organizzazione. Nella seguente tabella sono riportati i tipi di messaggio che possono essere elaborati dalle regole del flusso di posta.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di messaggio</th>
<th>È possibile applicare una regola?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Messaggi normali</strong>   Messaggi che contengono un unico corpo in formato RTF, HTML o in testo normale oppure un corpo costituito da più parti o un insieme alternativo di corpi del messaggio.</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p><strong>Crittografia dei messaggi di Office 365</strong>    Messaggi crittografati da Crittografia dei messaggi di Office 365 in Office 365. Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=392525">Crittografia dei messaggi di Office 365</a>.</p></td>
<td><p>Le regole possono sempre accedere alle intestazioni delle buste ed elaborare i messaggi in base alle condizioni che esaminano quelle intestazioni.</p>
<p>Affinché una regola possa esaminare o modificare i contenuti di un messaggio crittografato, è necessario verificare che la crittografia di trasporto sia abilitata (Obbligatoria o Facoltativa; l'impostazione predefinita è Facoltativa). Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">Abilitare o disabilitare la decrittografia di trasporto</a>.</p>
<p>È inoltre possibile creare una regola che consente di decrittografare automaticamente i messaggi crittografati. Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=402846">Definire le regole per crittografare o decrittografare i messaggi di posta elettronica</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Messaggi crittografati (S/MIME)</strong></p></td>
<td><p>Le regole possono accedere solo alle intestazioni delle buste ed elaborare i messaggi in base alle condizioni che esaminano quelle intestazioni.</p>
<p>Le regole con le condizioni che richiedono l'analisi del contenuto del messaggio oppure le azioni che modificano i contenuti del messaggio non possono essere elaborate.</p></td>
</tr>
<tr class="even">
<td><p><strong>Messaggi protetti da RMS</strong>   Messaggi su cui è stato applicato il criterio Active Directory Rights Management Services (AD RMS) o Azure Rights Management (RMS).</p></td>
<td><p>Le regole possono sempre accedere alle intestazioni delle buste ed elaborare i messaggi in base alle condizioni che esaminano quelle intestazioni.</p>
<p>Affinché una regola possa esaminare o modificare i contenuti di un messaggio protetto da RMS, è necessario verificare che la crittografia di trasporto sia abilitata (Obbligatoria o Facoltativa; l'impostazione predefinita è Facoltativa). Per ulteriori informazioni, vedere <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">Abilitare o disabilitare la decrittografia di trasporto</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Messaggi con firma in chiaro</strong>   Messaggi firmati ma non crittografati.</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p><strong>Messaggi di messaggistica unificata</strong>   Messaggi creati o elaborati dal servizio di messaggistica unificata, ad esempio messaggi di segreteria telefonica, fax, notifiche di chiamata senza risposta e messaggi creati o inoltrati utilizzando Microsoft Outlook Voice Access.</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p><strong>Messaggi anonimi</strong>   Messaggi inviati da mittenti anonimi.</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p><strong>Rapporto di lettura</strong>   Rapporti generati in risposta alle richieste di conferma di lettura dei mittenti. I rapporti di lettura utilizzano la classe messaggio <code>IPM.Note*.MdnRead</code> o <code>IPM.Note*.MdnNotRead</code>.</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


## Regole di trasporto e appartenenza a gruppi

Quando si definisce una regola di trasporto utilizzando una condizione che espande l'appartenenza a un gruppo di distribuzione, l'elenco di destinatari risultante viene memorizzato nel servizio di trasporto sul server Cassette postali che applica la regola. La cache è definita *cache dei gruppi espansa* ed è utilizzata dall'agente di journaling per valutare l'appartenenza ai gruppi per le regole del journal. Per impostazione predefinita, la cache dei gruppi espansa memorizza l'appartenenza ai gruppi per quattro ore. Vengono archiviati anche i destinatari restituiti dal filtro destinatari di un gruppo di distribuzione dinamico. La cache dei gruppi espansa rende inutili i ripetuti round trip verso Active Directory e il traffico di rete dovuto alla risoluzione delle appartenenze ai gruppi.

In Exchange 2013, questo intervallo e gli altri parametri relativi alla cache dei gruppi espansa possono essere configurati. È possibile ridurre l'intervallo di scadenza della cache o disabilitare del tutto la memorizzazione nella cache per garantire un aggiornamento più frequente delle appartenenze ai gruppi. È opportuno pianificare l'aumento di carico sui controller di dominio Active Directory dovuto alle query di espansione dei gruppi di distribuzione. È inoltre possibile cancellare la cache su un server Cassette postali riavviando il servizio di trasporto di Microsoft Exchange su tale server. Questa operazione deve essere eseguita su ciascun server Cassette postali per cui si desidera cancellare la cache. Durante la creazione, la modifica e la risoluzione dei problemi relativi alle regole di trasporto che utilizzano condizioni basate sull'appartenenza ai gruppi di distribuzione è importante tenere conto anche dell'impatto della cache dei gruppi espansa.

Torna all'inizio

## Archiviazione e replica delle regole

Le regole di trasporto create vengono archiviate nella replica di Active Directory e sono disponibili dopo la replica di Active Directory su tutti i server Exchange nell'organizzazione di Exchange 2013. In questo modo è possibile applicare un insieme coerente di regole nell'intera organizzazione di Exchange.

Quando si crea una nuova regola di trasporto o quando si modifica o si elimina una regola di trasporto esistente, la modifica viene replicata in tutti i controller di dominio Active Directory nell'organizzazione. Tutti i server Exchange nell'organizzazione leggono quindi la nuova configurazione dai server Active Directory e applicano le nuove regole di trasporto o quelle modificate.


> [!IMPORTANT]
> Replica delle regole di trasporto in un'organizzazione dipende dal Active Directory replica. Tempo di replica tra i controller di dominio Active Directory varia a seconda del numero di siti nell'organizzazione, collegamenti lenti e altri fattori all'esterno del controllo di Exchange. Quando si configurano le regole di trasporto nell'organizzazione, assicurarsi di prendere in considerazione dei ritardi di replica. Per ulteriori informazioni sulla replica Active Directory, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=64499">Le tecnologie di replica di Active Directory</A>.




> [!IMPORTANT]
> Il servizio di trasporto su ciascun server Cassette postali conserva una cache dei destinatari utilizzata per cercare informazioni sui destinatari e sulle liste di distribuzione. La cache dei destinatari riduce il numero di richieste che ogni server Cassette postali deve eseguire su un controller di dominio di Active Directory. La cache dei destinatari viene aggiornata ogni quattro ore. Non è possibile modificare l'intervallo di aggiornamento della cache dei destinatari. Pertanto, le modifiche apportate ai destinatari delle regole di trasporto, quali l'aggiunta o la rimozione di membri della lista di distribuzione, non possono essere applicate alle regole di trasporto fino all'aggiornamento della cache dei destinatari. Per forzare un aggiornamento immediato della cache del destinatario, è necessario arrestare e avviare il servizio di trasporto di Microsoft Exchange. È necessario fare questo per ciascun server Cassette postali su cui si desidera forzare l'aggiornamento della cache del destinatario.




> [!NOTE]
> Ogni volta che viene recuperata una nuova configurazione delle regole di trasporto dal servizio di trasporto sul server Cassette postali, viene registrato un evento nel registro di protezione del Visualizzatore eventi.



Torna all'inizio

## Archiviazione e replica delle regole in ambienti misti

Esistono due scenari di ambienti misti comuni: le distribuzioni ibride in cui parte dell'organizzazione risiede su Office 365 e la coesistenza tra Exchange 2013 e Exchange 2010 o Exchange 2007.

Nello scenario ibrido, non esistono regole duplicate tra la distribuzione locale e Office 365. Di conseguenza, quando si crea una regola nell'organizzazione Exchange locale, è necessario creare una regola corrispondente in Office 365. Le regole create in Office 365 vengono archiviate nel cloud, insieme alla parte restante della configurazione dell'organizzazione Office 365, mentre le regole create nell'organizzazione Exchange locale vengono archiviate in locale in Active Directory. Quando si gestiscono le regole in uno scenario ibrido, è necessario accertarsi che i due insiemi di regole siano sempre sincronizzati apportando le modifiche ad entrambi o effettuando la modifica in un ambiente, esportando le regole e importandole nell'altro ambiente.


> [!IMPORTANT]
> Nonostante la sostanziale sovrapposizione tra le condizioni e le azioni disponibili in Office 365 e Exchange locale, esistono alcune differenze. Se si intende creare la stessa regola in entrambe le posizioni, accertarsi che tutte le condizioni e tutte le azioni che di pensa di utilizzare siano disponibili. Per visualizzare l'elenco di condizioni e azioni disponibili per ciascuna distribuzione, vedere i seguenti argomenti:<BR><A href="https://technet.microsoft.com/it-it/library/jj919235(v=exchg.150)">Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online</A> in Office 365<BR><A href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">Condizioni delle regole di trasporto (predicati)</A> in Exchange locale<BR><A href="https://technet.microsoft.com/it-it/library/jj919237(v=exchg.150)">Posta azioni delle regole del flusso di Exchange Online</A> in Office 365<BR><A href="mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md">Azioni della regola di trasporto</A> in Exchange locale



In caso di coesistenza con Exchange 2007, tutte le regole di trasposto vengono archiviate in Active Directory e replicate nell'organizzazione indipendentemente dalla versione di Exchange Server utilizzata per crearle. Tuttavia, tutte le regole di trasporto associate alla versione del server Exchange utilizzata per crearle vengono archiviate in un contenitore specifico della versione in Active Directory. Quando si distribuisce per la prima volta Exchange 2013 nell'organizzazione, tutte le regole esistenti vengono importate in Exchange 2013 come parte del processo di impostazione. Tuttavia, eventuali modifiche successive dovrebbero essere effettuate con entrambe le versioni. Ad esempio, se si modifica una regola esistente tramite l'interfaccia di amministrazione di Exchange 2013, è necessario eseguire la stessa modifica con Exchange 2007 EMC.

Torna all'inizio

## Informazioni aggiuntive

  - Se si utilizza sia Exchange Server 2010 che Exchange Server 2013, tenere presente che Exchange Server 2010 non è in grado di elaborare le regole che vengono elencate come **versione 15**. Per assicurarsi che tutte le regole possono essere elaborate, utilizzare solo le regole della **versione 14**.

## Ulteriori informazioni

[Gestire le regole di flusso di posta elettronica](manage-mail-flow-rules-exchange-2013-help.md)

[Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Azioni della regola di trasporto](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Agenti di trasporto](transport-agents-exchange-2013-help.md)

