---
title: 'Gestito i limiti di archiviazione: Exchange 2013 Help'
TOCTitle: Gestito i limiti di archiviazione
ms:assetid: bea9ec15-bfb5-4716-b14e-010e389c9f9e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt741981(v=EXCHG.150)
ms:contentKeyID: 73226022
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestito i limiti di archiviazione

 

_**Ultima modifica dell'argomento:**2016-09-15_

**Riepilogo:** limiti delle connessioni archivio gestito e relativa configurazione.

In MicrosoftExchange Server 2013, sono stati inseriti connessione e limiti di utilizzo per l'archivio gestito Exchange per evitare una singola applicazione o un singolo utente di utilizzare tutte le connessioni disponibili per l'archivio gestito. Se un singolo utente o l'applicazione è consentito utilizzare tutte le connessioni, altri utenti o applicazioni non sono in grado di accedere all'archivio gestito che potrebbero causare tempi di inattività.


> [!NOTE]
> Per le connessioni effettuate dagli account con privilegi di amministratore, i limiti di durata massima della sessione sono stati aumentati a 64.000.



## Terminologia

Conoscenza dei termini seguenti consentono di comprendere i tipi di connessioni a cui fa riferimento in questo argomento.

  - Sessioni  
    Sessioni rappresentano le connessioni utilizzate dai servizi e applicazioni client, ad esempio Microsoft Outlook, per connettersi all'archivio gestito. Servizi e i client possono avere più sessioni in un determinato momento. Le condizioni *connessioni* e le *sessioni* utilizzabile in modo intercambiabile.

<!-- end list -->

  - Thread di  
    Thread rappresentano richieste attualmente in esecuzione nell'archivio gestito. Ad esempio, se un'utente apre una cartella in Outlook, Outlook esegue una richiesta per l'archivio gestito per conto dell'utente. Eseguire la richiesta è un unico thread.
    
    In Exchange Server 2013, non sono più limiti dei thread in base al tipo di client. In realtà, per tutti i client, il numero massimo di thread **per ogni database delle cassette postali** è 50. L'eccezione è il servizio disponibilità, che ha un limite massimo di 16 per utente.

Inizio pagina

## Limitazioni delle sessioni

Nella tabella seguente sono elencati i tipi di connessioni client per l'archivio gestito e i limiti di base su tali connessioni. Se si desidera modificare i limiti di sessione, vedere "Configurazione dei limiti delle sessioni" subito dopo la tabella.

Versioni precedenti di Exchange di limitare il numero di connessioni per l'archivio gestito in base al numero di connessioni al server. In Exchange 2013, limitazioni delle sessioni si basano sulle connessioni al database delle cassette postali.

I tipi di limiti delle connessioni in Exchange 2013 sono i seguenti:

  - **Sessioni Max per processo**   Specifica il numero massimo di sessioni che un servizio Exchange può essere aperti contemporaneamente in un database delle cassette postali.

  - **Sessioni utente Max per processo**   Specifica il numero massimo di sessioni per un particolare protocollo per un singolo utente.

Nella sezione seguente, "Configurare limitazioni delle sessioni," viene descritto come modificare questi limiti.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di client</th>
<th> </th>
<th>Max sessioni al database delle cassette postali</th>
<th>Numero predefinito di sessioni utente al database delle cassette postali</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Admin</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Servizio Disponibilità</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Indicizzazione del contenuto</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td> </td>
<td><p>Non applicabile</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Servizi Web di Exchange</p></td>
<td> </td>
<td><p>Non applicabile</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>Gestione</p></td>
<td> </td>
<td><p>Non applicabile</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>MAPI al livello intermedio (MoMT)</p></td>
<td> </td>
<td><p>Non applicabile</p></td>
<td><p>32</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants: eventi</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxAssistants: si è verificato</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Chiamata di procedura remota MSExchange</p></td>
<td> </td>
<td><p>Non applicabile</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Outlook Web App</p></td>
<td> </td>
<td><p>Non applicabile</p></td>
<td><p>16</p></td>
</tr>
<tr class="even">
<td><p>POP3 e IMAP4</p></td>
<td> </td>
<td><p>Non applicabile</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Trasporto</p></td>
<td> </td>
<td><p>10,000</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="even">
<td><p>Messaggistica unificata</p></td>
<td> </td>
<td><p>Non applicabile</p></td>
<td><p>16</p></td>
</tr>
<tr class="odd">
<td><p>Altri</p></td>
<td> </td>
<td><p>Non applicabile</p></td>
<td><p>16</p></td>
</tr>
</tbody>
</table>


## Configurare i limiti di sessione

È possibile modificare i limiti di sessione predefinito.


> [!NOTE]
> Se si desidera modificare i limiti di sessione, è necessario modificarli in tutti i server cassette postali all'interno di eventuali gruppi di disponibilità del database (DAG). Se non si apportano le stesse modifiche in tutti i server, i risultati sarà coerenti. Per incrementare il limite sessione sul server Accesso Client, è necessario aumentare il valore <CODE>RCAMaxConcurrency</CODE> in Criteri di limitazione. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/dd298094(v=exchg.150)">Set-ThrottlingPolicy</A>.




> [!WARNING]
> La modifica non corretta del Registro di sistema può causare gravi problemi che potrebbero richiedere la reinstallazione del sistema operativo. Eventuali problemi derivanti dalla modifica non corretta del Registro di sistema potrebbero essere irrisolvibili. Prima di modificare il Registro di sistema, eseguire il backup di tutti i dati importanti.



1.  Avviare l'editor del Registro di sistema (regedit).

2.  Individuare la sottochiave del Registro di sistema seguente:
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**.

3.  Pulsante destro del mouse **ParametersSystem**, scegliere **Nuovo** e quindi fare clic su **valore DWORD (32 bit).**
    
    Nel riquadro dei risultati viene creato il nuovo valore.

4.  Rinominare il tasto a uno dei valori seguenti e quindi premere INVIO:
    
      - **Numero massimo di sessioni consentito Per utente**   Questo limite specifica il numero massimo di sessioni consentito per utente.
    
      - **Servizio consentiti massimo sessioni Per utente**   Questo limite specifica sessioni servizio consentito massima per utente.
    
      - **Exchange consentiti massimo sessioni per ogni servizio**   Questo limite specifica il numero massimo consentito Exchange sessioni per ogni servizio. Il valore predefinito è 10.000.

5.  Fare clic sulla chiave appena creata e quindi fare clic su **Modifica**.

6.  Nella casella**dativalore** digitare il numero di oggetti a cui si desidera limitare questa voce e quindi fare clic su **OK**. Utilizzare la tabella precedente per visualizzare le impostazioni predefinite.

Inizio pagina

## Apertura elementi limiti

Elemento aperto limiti sono limiti relativi al numero di elementi che possono essere aperti da un'unica cassetta postale in una singola sessione. Tuttavia, un utente può disporre di più sessioni aperte contemporaneamente. Ad esempio, se un utente dispone di due sessioni aperte, l'utente può aprire le 1.000 cartelle.

Se si desidera modificare questi limiti, vedere "Configurare Open elemento Limits" subito dopo la tabella.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di elemento</th>
<th>Tipo di oggetto del Registro di sistema</th>
<th>Numero massimo aperto per sessione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Visualizzazione ACL</p></td>
<td><p>objtACLView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Attachment</p></td>
<td><p>objtAttachment</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Visualizzazione allegati</p></td>
<td><p>objtAttachmentView</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>CStream</p></td>
<td><p>objtCStream</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>Cartella</p></td>
<td><p>objtFolder</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Visualizzazione delle cartelle</p></td>
<td><p>objtFolderView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Flusso di destinazione FX</p></td>
<td><p>objtFXDstStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="even">
<td><p>Flusso di origine FX</p></td>
<td><p>objtFXSrcStrm</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Messaggio</p></td>
<td><p>objtMessage</p></td>
<td><p>250</p></td>
</tr>
<tr class="even">
<td><p>Visualizzazione dei messaggi</p></td>
<td><p>objtMessageView</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>Notifica</p></td>
<td><p>objtNotify</p></td>
<td><p>500,000</p></td>
</tr>
<tr class="even">
<td><p>Visualizzazione regola</p></td>
<td><p>objtRulesView</p></td>
<td><p>Non applicabile</p></td>
</tr>
<tr class="odd">
<td><p>Oggetto Stream</p></td>
<td><p>objtStream</p></td>
<td><p>250</p></td>
</tr>
</tbody>
</table>


## Configurare i limiti di elemento aperto

È possibile limitare il numero massimo di risorse che un client MAPI è possibile utilizzare contemporaneamente.


> [!NOTE]
> Se si desidera modificare i limiti di elemento aperto, è necessario modificarli in tutti i server cassette postali all'interno di un DAG e matrici di accesso client. Se non si apportano le stesse modifiche in tutti i server, i risultati sarà coerenti.




> [!WARNING]
> La modifica non corretta del Registro di sistema può causare gravi problemi che potrebbero richiedere la reinstallazione del sistema operativo. Eventuali problemi derivanti dalla modifica non corretta del Registro di sistema potrebbero essere irrisolvibili. Prima di modificare il Registro di sistema, eseguire il backup di tutti i dati importanti.



1.  Avviare l'editor del Registro di sistema (regedit).

2.  Individuare la sottochiave del Registro di sistema seguente:
    
    **\\\\HKEY\_LOCAL\_MACHINE \\SYSTEM\\CurrentControlSet\\Services\\MSExchangeIS\\ParametersSystem**

3.  Fare clic con il pulsante destro del mouse su **ParametersSystem**, scegliere **Nuovo**, quindi fare clic su **Chiave**.
    
    Nell'albero della console, viene creata una nuova chiave.

4.  Rinominare la chiave **MaxObjsPerMapiSession** e quindi premere INVIO.

5.  Pulsante destro del mouse **MaxObjsPerMapiSession**, scegliere **Nuovo** e quindi fare clic su **valore DWORD (32 bit)**.
    
    Nel riquadro dei risultati viene creato il nuovo valore.

6.  Rinominare la chiave in *\<Object\_type\>*, dove *\<Object\_type\>* è il nome del tipo di oggetto del Registro di sistema che si sta modificando. Ad esempio, per modificare il numero di messaggi che possono essere aperte, utilizzare *objtMessage*. Premere INVIO.

7.  Fare clic sulla chiave appena creata e quindi fare clic su **Modifica**.

8.  Nella casella **dati valore** digitare il numero di oggetti che si desidera limitare questa voce e quindi fare clic su **OK**. Ad esempio, digitare **350** per aumentare il valore dell'oggetto.

9.  Riavviare il servizio Microsoft Exchange Information Store.

Inizio pagina

## Limiti dimensioni elementi

Limiti dimensioni elementi sono i limiti posizionati sugli elementi all'interno di postale una cassetta. Sono configurabili utilizzando i parametri *MaxSendSize* e *MaxReceiveSize* nel cmdlet [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) .


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di elemento</th>
<th>Limite</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Messaggio (salvata)</p></td>
<td><p>Dimensione massima di SendLimit, ReceiveLimit</p></td>
</tr>
<tr class="even">
<td><p>Messaggio (inviato)</p></td>
<td><p>Dimensione massima del SendLimit</p></td>
</tr>
<tr class="odd">
<td> </td>
<td> </td>
</tr>
</tbody>
</table>


Inizio pagina

