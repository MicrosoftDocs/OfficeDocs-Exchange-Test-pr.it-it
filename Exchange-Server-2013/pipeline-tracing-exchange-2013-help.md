---
title: 'Analisi della pipeline: Exchange 2013 Help'
TOCTitle: Analisi della pipeline
ms:assetid: e7780499-9a6f-48b1-aea8-df88ecd8b18a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125018(v=EXCHG.150)
ms:contentKeyID: 52063113
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Analisi della pipeline

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

L'analisi della pipeline cattura copie dei messaggi di posta elettronica di uno specifico mittente mentre viaggiano attraverso il servizio di trasporto sui server Cassette postali, il servizio Recapito alle cassette postali sui server Cassette postali e tramite i sever Trasporto Edge. L'analisi della pipeline cattura le informazioni dettagliate sulle modifica applicate da ogni agente di trasporto ai messaggi nella pipeline di trasporto nei file snapshot del messaggio. Esaminando il contenuto dei file snapshot del messaggio, è possibile stabilire se gli agenti di trasporto hanno applicato le modifiche ai messaggi nella pipeline di trasporto come previsto. Per risolvere un problema, è necessario stabilire in quale agente di trasporto si è verificato l'errore. Dopo di che è possibile concentrarsi sull'agente per risolvere il problema. Successivamente i file snapshot del messaggio possono essere visualizzati di nuovo per assicurarsi che il problema sia stato effettivamente risolto.


> [!WARNING]
> <UL>
> <LI>
> <P>L'analisi della pipeline copia l'intero contenuto dei messaggi di posta elettronica che vengono inviati dall'indirizzo di posta elettronica del mittente. Per evitare l'esposizione indesiderata di informazioni riservate, è necessario impostare le autorizzazioni di protezione appropriate sulla cartella di analisi della pipeline.</P>
> <LI>
> <P>Non abilitare l'analisi della pipeline per periodi di tempo prolungati. L'analisi della pipeline crea file che possono accumularsi rapidamente. Controllare sempre lo spazio disponibile sul disco quando l'analisi della pipeline è abilitata.</P></LI></UL>



## Configurazione dell'analisi della pipeline

Prima di abilitare l'analisi della pipeline, è necessario specificare l'indirizzo di posta elettronica del mittente da monitorare. L'analisi della pipeline è progettata per registrare i messaggi inviati da uno specifico indirizzo di posta elettronica. L'indirizzo di posta elettronica del mittente può essere interno o esterno all'organizzazione Exchange. In alternativa, è possibile abilitare l'analisi della pipeline per i messaggi del sistema generati dal servizio di trasporto sullo specifico server Cassette postali o Trasporto Edge, ad esempio le risposte automatiche, i messaggi di notifica sullo stato del recapito (DSN), i rapporti del journal e altri messaggi generati dal sistema. È possibile, inoltre, modificare il percorso della cartella di analisi della pipeline.

I parametri utilizzati per configurare l'analisi della pipeline sono riassunti nella tabella seguente


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Parametro</th>
<th>Valore predefinito</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingSenderAddress</em></p></td>
<td><p>Vuoto (<code>$null</code>)</p></td>
<td><p>Specificare l'indirizzo di posta elettronica del mittente dal monitorare.</p>
<p>Specificare il valore &quot;&lt;&gt;&quot; per monitorare i messaggi generati dal sistema inviati al servizio di trasporto specificato sul server.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingPath</em></p></td>
<td><p><strong>Servizio di trasporto</strong>   <code>%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing</code></p>
<p><strong>Servizio Trasporto cassette postali</strong>   <code>%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing</code></p></td>
<td><p>Il percorso deve trovarsi sul server locale. I percorsi UNC non sono supportati.</p>
<p>Il percorso specificato contiene la cartella <code>MessageSnapshots</code> in cui sono archiviati i file di analisi della pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingEnabled</em></p></td>
<td><p><code>$false</code></p></td>
<td><p>È possibile abilitare l'analisi della pipeline solo per il servizio di trasporto specificato sul server dopo aver configurato l'indirizzo del mittente da monitorare.</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sull'abilitazione dell'analisi della pipeline e la configurazione dell'indirizzo del mittente per l'analisi della pipeline, vedere [Configurazione dell'analisi della pipeline](configure-pipeline-tracing-exchange-2013-help.md).

## File snapshot del messaggio

Le snapshot dei messaggi sono file in cui vengono catturate eventuali modifiche apportate a un messaggio dagli agenti di trasporto del servizio di trasporto o del servizio Recapito alle cassette postali. Tali file sono archiviati nella cartella `MessageSnapshots` nel percorso di analisi della pipeline corrispondente per il servizio di trasporto.

Nella cartella `MessageSnapshots`, Exchange crea una cartella per ogni messaggio inviato dal mittente monitorato che transita attraverso il servizio di trasporto specificato. Il nome di ogni cartella corrisponde a un GUID assegnato al messaggio. Se si abilita l'analisi della pipeline per il servizio Trasporto e il servizio Trasporto cassette postali sullo stesso server Cassette postali, ogni servizio assegna un GUID diverso allo stesso messaggio in modo che il nome della cartella per un messaggio presente nella cartella `MessageSnapshots` per il servizio Trasporto sia diverso da quello del messaggio presente nella cartella `MessageSnapshots` per il servizio Trasporto cassette postali Se si abilita l'analisi della pipeline su più server Exchange, un diverso GUID viene assegnato allo stesso messaggio che viaggia attraverso il servizio di trasporto specificato su ogni server Exchange.

Nella cartella di ogni messaggio, Exchange crea più file snapshot del messaggio con l'estensione eml. Tali file comprendono il contenuto del messaggio quando incontra i singoli eventi SMTP e agenti di trasporto.

Se un agente di trasporto viene registrato in un evento SMTP, Exchange crea una snapshot del messaggio prima che il messaggio incontri gli agenti di trasporto. In questo modo si ottiene una copia del messaggio prima che quest'ultimo incontri gli agenti di trasporto registrati sull'evento. Quindi verrà creato un nuovo snapshot del messaggio per ciascun agente di trasporto che il messaggio incontra, sia che l'agente di trasporto modifichi il contenuto del messaggio sia che non lo modifichi. Tuttavia, se su un evento non è registrato alcun agente, Exchange non crea snapshot del messaggio per l'evento in questione.

Ad esempio, se sull'evento **OnEndofData** vengono registrati tre agenti, ma solo due di essi modificano un messaggio, verranno creati quattro snapshot del messaggio. Il primo snapshot del messaggio cattura il messaggio quando incontra l'evento **OnEndofData** prima che vengano apportate modifiche eseguite dagli agenti di trasporto che hanno registrato l'evento. Quindi viene creato uno snapshot del messaggio per ogni agente di trasporto, indipendentemente dalla modifica o meno del messaggio da parte di un agente di trasporto.

I file snapshot del messaggio creati sono descritti nel seguente elenco:

  - **Original.eml** Questo file comprende il contenuto originale non modificato del messaggio di posta elettronica prima che questo incontri un evento SMTP o un agente di trasporto.

  - **Routingnnnn.eml**   Questi file comprendono il contenuto del messaggio di posta elettronica quando incontra gli eventi SMTP e gli agenti di trasporto registrati su tali eventi nella parte del servizio Trasporto costituita dalla classificazione. Il segnaposto *nnnn* rappresenta un valore intero che inizia con `0001`. Il valore viene aumentato per ogni evento SMTP e ogni agente di trasporto registrato su tali eventi nell'ordine in cui gli eventi e gli agenti agiscono sul messaggio. Il servizio Recapito alle cassette postali non genera tali file snapshot **Routing**.

  - **SmtpReceivennnn.eml**   Questi file comprendono il contenuto del messaggio di posta elettronica quando incontra gli eventi SMTP **OnEndofData** e **OnEndOfHeaders** e gli agenti di trasporto registrati durante la parte del servizio di trasporto o del servizio Recapito alle cassette postali costituita dalla ricezione SMTP. Il segnaposto *nnnn* rappresenta un valore intero che inizia con `0001`. Il valore viene aumentato per ogni evento SMTP e ogni agente di trasporto registrato su tali eventi nell'ordine in cui gli eventi e gli agenti agiscono sul messaggio.

È possibile aprire i file snapshot del messaggio utilizzando Notepad o altro editor di testo.

Ogni file snapshot del messaggio inizia con le intestazioni che vengono aggiunte al contenuto del messaggio ed elenca l'agente di trasporto e l'evento SMTP a cui si collega il file snapshot del messaggio. Queste intestazioni iniziano con `X-CreatedBy: MessageSnapshot-Begin injected headers` e terminano con `X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers`. Le intestazioni vengono sostituite nei singoli file snapshot del messaggio da ogni successivo agente di trasporto ed evento SMTP. Di seguito viene riportato un esempio delle intestazioni aggiunte a un file di messaggio di posta elettronica:

    X-CreatedBy: MessageSnapshot-Begin injected headers
    X-MessageSnapshot-UTC-Time: 2013-01-23T23:20:18.138Z
    X-MessageSnapshot-Record-Id: 21474836486
    X-MessageSnapshot-Source: OnSubmittedMessageX-Sender: michelle@nwtraders.com
    X-Receiver: chris@contoso.com
    X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers

Dopo le intestazioni degli snapshot del messaggio il file presenta il contenuto del messaggio, comprese tutte le intestazioni del messaggio originale. Se un agente di trasporto modifica il contenuto del messaggio, le modifiche verranno integrate al messaggio. Man mano che il messaggio viene elaborato da ogni agente di trasporto, le modifiche apportate dai singoli agenti vengono applicate al contenuto dei messaggi. Se un agente di trasporto non apporta modifiche al contenuto del messaggio, lo snapshot del messaggio creato dall'agente sarà identico allo snapshot del messaggio creato dall'agente di trasporto precedente.

