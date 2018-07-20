---
title: 'Suggerimenti per i criteri: Exchange 2013 Help'
TOCTitle: Suggerimenti per i criteri
ms:assetid: 4266b83c-dd8a-4b3d-99ff-402e68fc810c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150512(v=EXCHG.150)
ms:contentKeyID: 50479725
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suggerimenti per i criteri

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-07-22_

È possibile ottenere per impedire l'organizzazione Microsoft Outlook, Outlook Web App (OWA) e OWA per gli utenti di posta elettronica di dispositivi in modo improprio l'invio di informazioni riservate mediante la creazione di criteri di criterio DLP perdita di dati che includono i messaggi di notifica *Suggerimento del criterio* . Analogamente ai suggerimenti messaggio che sono stati introdotti in Microsoft Exchange Server 2010, i messaggi di notifica suggerimento sul criterio vengono visualizzati agli utenti in Outlook durante la creazione di un messaggio di posta elettronica. Messaggi di notifica suggerimento criterio visualizzata solo se un elemento sui messaggi di posta elettronica del mittente sembra violano i criteri DLP contenenti sul posto e che criterio sono inclusi una regola per ricevere una notifica al mittente quando vengono soddisfatte le condizioni che si stabilisce. Guardare questo video per ulteriori informazioni.

> [!VIDEO https://www.microsoft.com/it-it/videoplayer/embed/dd629bb7-063d-49f3-b7e1-8f2e0aa4de13]

Affinché i suggerimenti per il criterio vengano visualizzati, è necessario che le regole includano l'azione **Notifica al mittente con un suggerimento per il criterio**. Questa azione può essere aggiunta dall'editor delle regole nell'interfaccia di amministrazione di Exchange. Per ulteriori informazioni, vedere [Gestire i suggerimenti sui criteri](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).

In fase di valutazione dei messaggi e delle condizioni dei criteri, l'agente della regola di trasporto che forza i criteri per la prevenzione della perdita di dati non differenzia tra allegati, oggetto o corpo del testo. Ad esempio, se un utente crea un messaggio di posta elettronica che include un numero di carta di credito nella riga dell'oggetto e tenta di inviare il messaggio a un destinatario esterno all'organizzazione, è possibile impostare la visualizzazione in Outlook o Outlook Web App di un messaggio di notifica con un suggerimento per il criterio per ricordare all'utente le modalità di gestione da parte dell'organizzazione delle informazioni di quel tipo. Tuttavia, questo tipo di notifica verrà visualizzato solamente se è stato configurato un criterio per la prevenzione della perdita di dati che limita le azioni di esempio descritte; in questo caso, aggiungendo un alias di posta elettronica esterno all'intestazione del messaggio con i dati della carta di credito. Quando si creano i criteri per la prevenzione della perdita di dati è possibile scegliere tra una vasta gamma di condizioni, azioni ed eccezioni. In questo modo, sarà possibile personalizzare i criteri in base alle specifiche esigenze di ciascuna organizzazione.

Ogni volta che in un ruolo vengono utilizzate le azioni di notifica al mittente o di sostituzione, si consiglia di includere che il messaggio è stato inviato all'interno dell'organizzazione. A tale scopo, è possibile utilizzare l'editor delle regole per aggiungere la condizione seguente: **Il mittente si trova in…** \> **all'interno dell'organizzazione**. Per ulteriori informazioni sulla modifica dei criteri DLP esistenti, vedere [Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md). Questa procedura è consigliata in quanto l'azione di notifica al mittente viene applicata come parte dell'esperienza di creazione del messaggio dell'azienda. Mediante questa azione, i mittenti sono gli autori del messaggio all'interno dell'azienda. L'intervento dell'utente presentato dai Suggerimenti criteri non può essere applicato dagli utenti per i messaggi in ingresso e verrà ignorato quando il mittente si trova all'esterno dell'organizzazione. È possibile applicare i criteri DLP per analizzare i messaggi in ingresso ed eseguire varie azioni, ma in questo caso, non è possibile aggiungere l'azione di notifica al mittente.

Se i mittenti che stanno componendo un messaggio vengono informati in tempo reale degli standard e delle aspettative dell'organizzazione tramite le notifiche con un suggerimento per il criterio, è meno probabile che possano violare gli standard che l'organizzazione desidera applicare.


> [!NOTE]
> <UL>
> <LI>
> <P>Exchange Online: Prevenzione perdita dati (DLP) è una funzionalità premium che richiede una sottoscrizione Exchange Online Piano 2. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=286154">Confronto tra i piani di Exchange Online</A>.</P>
> <LI>
> <P>Exchange 2013: Prevenzione perdita dati (DLP) è una funzionalità premium che richiede una licenza di accesso client (CAL, Client Access License) di Enterprise di Exchange. Per ulteriori informazioni sulle licenze CAL e sulla gestione delle licenze server, vedere l'articolo relativo alla <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">gestione delle licenze di Exchange Server</A>.</P>
> <LI>
> <P>Se l'organizzazione utilizza Exchange 2013 SP1 o Exchange Online, i suggerimenti dei criteri sono disponibili agli utenti per l'invio di posta da Outlook 2013, Outlook Web App o OWA per i dispositivi. Tuttavia, se l'organizzazione attualmente utilizza Exchange 2013, i suggerimenti criteri sono disponibili solo per gli utenti che inviano messaggi di posta elettronica da Outlook 2013.</P></LI></UL>



## Testo predefinito per i suggerimenti per i criteri e le opzioni per le regole

Quando si aggiungono le regole per la notifica al mittente nei criteri per la prevenzione della perdita di dati è possibile scegliere tra diverse opzioni. Quando si aggiunge una regola per la notifica al mittente inserendo l'azione **Notifica al mittente con un suggerimento per il criterio** in un criterio per la prevenzione della perdita di dati, è possibile scegliere il livello di limitazione. Sono disponibili le opzioni di notifica elencate nella seguente tabella. Per ulteriori informazioni sulla modifica dei criteri, vedere [Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md). Per informazioni specifiche sulla creazione dei suggerimenti per il criterio, vedere [Gestire i suggerimenti sui criteri](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Regola di notifica</th>
<th>Significato</th>
<th>Messaggio di notifica predefinito con un suggerimento per il criterio che verrà visualizzato dagli utenti di Outlook</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Notifica solo</strong></p></td>
<td><p>Simile agli avvisi messaggio, visualizza un messaggio di notifica con un suggerimento relativo alla violazione di un criterio. Un mittente può evitare la visualizzazione di questo tipo di suggerimenti utilizzando la finestra di dialogo delle opzioni per i suggerimenti per i criteri disponibile in Outlook.</p></td>
<td><p>Questo messaggio può contenere informazioni sensibili. Tutti i destinatari devono essere autorizzati a ricevere questo contenuto.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rifiuta messaggio</strong></p></td>
<td><p>Il messaggio non verrà recapitato fino a quando la condizione non sarà stata eliminata. Il mittente può indicare che il messaggio di posta elettronica non contiene informazioni riservate. In questo caso si parla anche di override dei falsi positivi. Se il mittente sceglie questa soluzione, Outlook permette al messaggio di uscire dalla Posta in uscita in modo che il rapporto dell'utente possa essere controllato, ma Exchange blocca l'invio del messaggio.</p></td>
<td><p>Questo messaggio può contenere informazioni sensibili. L'organizzazione non consentirà l'invio del messaggio finché tale contenuto non verrà rimosso.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rifiuta in assenza di override dei falsi positivi</strong></p></td>
<td><p>Il risultato di questa regola di notifica è simile a quello prodotto dalla regola <strong>Rifiuta messaggio</strong>. Tuttavia, se si seleziona questa regola, Exchange consente l'invio del messaggio al destinatario specificato, senza bloccarlo.</p></td>
<td><p><strong>Prima che il mittente selezioni un'opzione per l'override:</strong> Questo messaggio potrebbe contenere informazioni sensibili. L'organizzazione non consentirà l'invio del messaggio finché tale contenuto non verrà rimosso.</p>
<p><strong>Dopo che il mittente ha selezionato l'opzione di override:</strong> Il feedback dell'utente verrà inviato all'amministratore quando viene inviato il messaggio.</p></td>
</tr>
<tr class="even">
<td><p><strong>Rifiuta in assenza di override automatico</strong></p></td>
<td><p>Il messaggio non verrà recapitato fino a quando la condizione non sarà stata eliminata o il mittente non avrà indicato un override. Il mittente ha la possibilità di indicare che desidera eseguire l'override del criterio.</p></td>
<td><p><strong>Prima che il mittente selezioni un'opzione per l'override:</strong> Questo messaggio potrebbe contenere informazioni sensibili. L'organizzazione non consentirà l'invio del messaggio finché tale contenuto non verrà rimosso.</p>
<p><strong>Dopo che il mittente ha selezionato l'opzione di override:</strong> È stato eseguito l'override dei criteri dell'organizzazione per le informazioni sensibili contenute nel messaggio. Tale azione verrà controllato dall'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rifiuta in assenza di override esplicito</strong></p></td>
<td><p>Il risultato con questa regola di notifica è simile a quello prodotto dalla regola <strong>Rifiuta in assenza di override automatico</strong>, ma in questo caso, quando il mittente tenta di eseguire l'override del criterio, deve fornire una giustificazione per la sua richiesta.</p></td>
<td><p><strong>Prima che il mittente selezioni un'opzione per l'override:</strong> Questo messaggio potrebbe contenere informazioni sensibili. L'organizzazione non consentirà l'invio del messaggio finché tale contenuto non verrà rimosso.</p>
<p><strong>Dopo che il mittente ha selezionato l'opzione di override:</strong> È stato eseguito l'override dei criteri dell'organizzazione per le informazioni sensibili contenute nel messaggio. Tale azione verrà controllato dall'organizzazione.</p></td>
</tr>
</tbody>
</table>


## Personalizzare i messaggi di notifica del suggerimento sul criterio

Per personalizzare il testo di notifica suggerimento sul criterio che i mittenti di posta elettronica vedere il programma di posta elettronica, selezionare **Suggerimenti sui criteri di gestione** nella pagina di prevenzione della perdita di dati. Per consentire di testo personalizzato venga visualizzato, una regola del criterio DLP deve includere l'azione **notifica al mittente con un suggerimento sul criterio**. Aggiungere l'azione a una regola utilizzando l'editor delle regole DLP.

Per le procedure che illustrano come creare suggerimenti criteri, vedere [Gestire i suggerimenti sui criteri](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md). Il testo personalizzato che si crea possibile sostituire il testo predefinito indicato nella tabella precedente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazioni e azioni notifica suggerimento dei criteri</th>
<th>Significato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Informare il mittente</strong></p></td>
<td><p>Il testo viene visualizzata solo quando viene avviata un'azione <strong>notifica al mittente ma consentire loro di invio</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Consentire al mittente di eseguire l'override</strong></p></td>
<td><p>Il testo viene visualizzata solo quando vengono inizializzate le seguenti operazioni: <strong>Blocca il messaggio a meno che non è un falso positivo</strong>, <strong>bloccare il messaggio, ma Consenti al mittente di intervenire e inviarlo</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Bloccare il messaggio</strong></p></td>
<td><p>Il testo viene visualizzata solo quando viene avviata un'azione <strong>Blocca il messaggio</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Collegare a URL di conformità</strong></p></td>
<td><p>L'URL di conformità è un collegamento a una pagina web in cui vengono illustrate la conformità e ignorare i criteri. Quando un utente fa clic sul collegamento <strong>ulteriori dettagli</strong>, viene visualizzato questo collegamento dal suggerimento del criterio.</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md)

[Gestire i suggerimenti sui criteri](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)

