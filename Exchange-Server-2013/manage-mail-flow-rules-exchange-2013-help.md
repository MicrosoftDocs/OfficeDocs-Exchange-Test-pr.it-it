---
title: 'Gestire le regole di flusso di posta elettronica: Exchange Online Protection Help'
TOCTitle: Gestire le regole di flusso di posta elettronica
ms:assetid: e7a81372-b6d7-4d1f-bc9e-a845a7facac2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657505(v=EXCHG.150)
ms:contentKeyID: 50481904
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire le regole di flusso di posta elettronica

 

_**Si applica a:**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Regole del flusso di posta elettronica, noto anche come regole di trasporto, è possibile utilizzare per cercare le condizioni specifiche nei messaggi che transitano attraverso l'organizzazione ed esegue azioni su di essi. In questo argomento viene illustrato come creare, Copia, modificare l'ordine, abilitare o disabilitare, eliminareo importare o esportare le regole e su come monitorare l'utilizzo regola.


> [!TIP]
> Per verificare che le regole funzionino nel modo desiderato, è necessario testare accuratamente ogni regola e le interazioni tra le regole.



Per informazioni sugli scenari in cui si utilizzano queste procedure Vedere i seguenti argomenti:

  - [Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità per tutta l'organizzazione](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [Utilizzare le regole di trasporto per esaminare messaggi con allegati](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [Scenari comuni relativi al blocco degli allegati](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)

  - [Utilizzare regole del flusso di posta per instradare le e-mail in base a un elenco di parole, frasi o motivi](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)

  - [Scenari comuni di approvazione messaggio](common-message-approval-scenarios-exchange-2013-help.md)

  - [Utilizzare le regole di flusso di posta elettronica in modo che i messaggi possono ignorare confusione](use-mail-flow-rules-so-messages-can-bypass-clutter-exchange-2013-help.md)

  - [Procedure consigliate per la configurazione delle regole del flusso di posta](best-practices-for-configuring-mail-flow-rules-exchange-2013-help.md)

  - [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/it-it/library/jj919236\(v=exchg.150\))

  - [Utilizzare le regole di trasporto per configurare il filtro di posta elettronica in blocco](https://technet.microsoft.com/it-it/library/dn720438\(v=exchg.150\))

  - [Definire le regole per crittografare o decrittografare i messaggi di posta elettronica](https://go.microsoft.com/fwlink/p/?linkid=402846)

  - [Creare a livello di organizzazione mittenti attendibili o degli elenchi di mittenti bloccati in Office 365](https://technet.microsoft.com/it-it/library/dn198251\(v=exchg.150\))

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Regole di trasporto" in [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md) (Exchange Server), oppure in [Autorizzazioni funzionalità in Exchange Online](https://technet.microsoft.com/it-it/library/jj200673\(v=exchg.150\)).

  - Quando una regola è riportata come **versione 14**, ciò significa che la regola si basa su un formato di regola del flusso di posta elettronica Exchange Server 2010. Tutte le opzioni sono disponibili per queste regole.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Quale operazione si desidera effettuare?

## Creare una regola di flusso di posta elettronica

Impostazione di un criterio di prevenzione della perdita di dati (DLP), la creazione di una nuova regola oppure copiando una regola, è possibile creare una regola del flusso di posta elettronica. È possibile utilizzare Interfaccia di amministrazione di Exchange (EAC) o Exchange Management Shell.


> [!NOTE]
> Dopo aver creare o modificare una regola del flusso di posta elettronica, possono richiedere fino a 30 minuti per la regola di nuova o aggiornata da applicare alla posta elettronica.



## Utilizzare un criterio DLP per creare regole del flusso di posta elettronica

Ogni criterio DLP è un insieme di regole del flusso di posta elettronica. Dopo aver creato il criterio DLP, è possibile ottimizzare le regole utilizzando le procedure riportate di seguito.

1.  Creare un criterio DLP. Per istruzioni, vedere:
    
      - [Procedure DLP in Exchange Server 2013](dlp-procedures-exchange-2013-help.md)
    
      - [Procedure DLP in Exchange Online](dlp-procedures-exchange-2013-help.md)

2.  Modificare le regole di flusso di posta elettronica create dal criterio DLP. Vedere visualizzare o modificare una regola di trasporto.

## Utilizzare EAC per creare una regola del flusso di posta elettronica

L'interfaccia di amministrazione di Exchange consente di creare regole del flusso di posta elettronica utilizzando un modello, copiando una regola esistente o partendo da zero.

1.  Andare a **Flusso di posta** \> **Regole**.

2.  Creare la regola tramite una delle opzioni seguenti:
    
      - Per creare una regola basandosi su un modello, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e selezionare un modello.
    
      - Per copiare una regola, selezionare la regola, quindi fare clic su **Copia**![Icona Copia](images/JJ657505.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "Icona Copia").
    
      - Per creare una nuova regola partendo da zero, selezionare **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), quindi **Crea una nuova regola**.

3.  Nella casella di dialogo **Nuova regola**, assegnare un nome alla regola e selezionare le condizioni e le azioni per la regola:
    
    1.  In **Applica questa regola se...**, selezionare la condizione desiderata dall'elenco di condizioni disponibili.
        
          - Alcune condizioni è necessario specificare i valori. Ad esempio, se si seleziona **il mittente è...** condizione, è necessario specificare un indirizzo del mittente. Se si sta aggiungendo una parola o frase, tenere presente che non sono consentiti spazi di fine riga.
        
          - Se la condizione desiderata non è nell'elenco o se si devono aggiungere delle eccezioni, selezionare **Altre opzioni**. Verrà visualizzato un elenco di eccezioni e condizioni aggiuntive.
        
          - Se non si desidera specificare una condizione e si desidera invece applicare la regola a ogni messaggio nell'organizzazione, selezionare la condizione **\[Applica a tutti i messaggi\]**.
    
    2.  In **Fai quanto segue...**, selezionare l'azione che la regola eseguirà sui messaggi che soddisfano i criteri dall'elenco delle azioni disponibili.
        
          - Alcune azioni richiederanno di specificare i valori. Ad esempio, se si seleziona la condizione **Inoltra il messaggio per l'approvazione a…**, sarà necessario selezionare un destinatario nell'organizzazione.
        
          - Se la condizione desiderata non è nell'elenco, selezionare **Altre opzioni**. Verrà visualizzato un elenco di condizioni aggiuntive.
    
    3.  Specificare la modalità di visualizzazione di [rapporti di prevenzione della perdita di dati (DLP)](https://go.microsoft.com/fwlink/p/?linkid=402768) e i [rapporti delle regole di trasporto](https://go.microsoft.com/fwlink/p/?linkid=402769)dati delle regole di corrispondenza della regola.
        
          - In **controllo questa regola con livello di gravità**, selezionare un livello per specificare il livello di gravità per la regola. L'attività di Office 365 report per le regole del flusso di posta elettronica corrispondenze di regole di gruppo per il livello di gravità. Livello di gravità è semplicemente un filtro per rendere più semplice utilizzare i report. Il livello di gravità non influisce sulla priorità in cui viene elaborata la regola.
            

            > [!NOTE]
            > Se si deseleziona la casella di controllo <STRONG>Controlla questa regola con livello di gravità</STRONG>, corrispondenze alla regola non verranno visualizzati nei rapporti delle regole.

    
    4.  Impostare la modalità per la regola. È possibile utilizzare uno dei due modalità di test per testare la regola senza influire sui flusso di posta. In entrambe le modalità di test, quando si verificano le condizioni, viene aggiunta una voce per l'analisi del messaggio.
        
          - **Imponi** La regola verrà attivata e sarà avviata immediatamente l'elaborazione dei messaggi. Tutte le azioni della regola verranno applicate.
        
          - **Verifica con suggerimenti per il criterio**   La regola viene attivata e tutte le azioni di Suggerimenti per il criterio (**Notifica al mittente con un suggerimento per il criterio**) verranno inviate, ma non sarà eseguita nessuna azione relativa al recapito dei messaggi. Per l'utilizzo di tale modalità è richiesta la prevenzione della perdita di dati (DLP). Per ulteriori informazioni, vedere [Suggerimenti per i criteri](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md).
        
          - **Verifica senza suggerimenti per il criterio**   Verrà applicata solo l'azione Genera rapporto operazioni non consentite. Non viene eseguita nessuna azione relativa al recapito dei messaggi.

4.  Se si è soddisfatti della regola, andare al passaggio 5. Per aggiungere ulteriori condizioni o azioni o per specificare eccezioni o impostare proprietà aggiuntive, fare clic su **Altre opzioni**. Dopo aver selezionato **Altre opzioni**, completare i seguenti campi per creare la regola:
    
    1.  Per aggiungere altre condizioni, fare clic su **Aggiungi condizione**. In presenza di più condizioni, rimuoverne una selezionando **Rimuovi X** accanto alla condizione da eliminare. Quando si seleziona **Altre opzioni**, verrà visualizzata una maggiore varietà di condizioni disponibili.
    
    2.  Per aggiungere ulteriori azioni, fare clic su **Aggiungi azione**. In presenza di più azioni, rimuoverne una selezionando **Rimuovi X** accanto all'azione da eliminare. Quando si seleziona **Altre opzioni**, verrà visualizzata una maggiore varietà di azioni disponibili.
    
    3.  Per specificare le eccezioni, fare clic su **Aggiungi eccezione**, quindi selezionare le eccezioni nell'elenco a discesa **Tranne se...**. Per rimuovere eccezioni dalla regola, fare clic su **Rimuovi X** accanto all'eccezione da eliminare.
    
    4.  Per rendere effettiva la regola dopo una determinata data, fare clic su **Attiva questa regola in data:** e specificare una data. La regola sarà comunque abilitata in quella data, ma non sarà elaborata.
        
        Analogamente, è possibile interrompere l'elaborazione della regola in una certa data. A tale scopo, fare clic su **Disattiva la regola in data:** e specificare una data. La regola rimarrà abilitata, ma non sarà elaborata.
    
    5.  Una volta che la regola ha elaborato un messaggio, è possibile scegliere di non applicare le regole aggiuntive. A tale scopo, fare clic su **Arresta l'elaborazione di altre regole**. Se si seleziona questa opzione e un messaggio viene elaborato dalla regola, non saranno elaborate regole successive per quel messaggio.
    
    6.  È possibile specificare come deve essere gestito il messaggio se non è possibile completare l'elaborazione della regola. Per impostazione predefinita la regola sarà ignorata e il messaggio sarà elaborato regolarmente, ma è possibile scegliere di inviare di nuovo il messaggio per l'elaborazione. A tale scopo, selezionare la casella di controllo **Rimanda il messaggio se l'elaborazione della regola non può essere completata**.
    
    7.  Se la regola analizza l'indirizzo del mittente, per impostazione predefinita esamina solo le intestazioni del messaggio. Tuttavia, è possibile configurare la regola perché venga esaminata anche la busta del messaggio SMTP. Per specificare gli oggetti di esame, fare clic su uno dei seguenti valori per **Corrispondenza con l'indirizzo del mittente nel messaggio**:
        
          - **Intestazione**   Vengono esaminate solo le intestazioni del messaggio.
        
          - **Busta**   Viene esaminata solo la busta del messaggio SMTP.
        
          - **Intestazione o busta**   Vengono esaminate sia le intestazioni che la busta del messaggio SMTP.
    
    8.  È possibile aggiungere commenti a questa regola nella casella **Commenti**.

5.  Fare clic su **Salva** per completare la creazione della regola.

## Utilizzare Exchange Management Shell per creare una regola del flusso di posta elettronica

In questo esempio viene utilizzato il cmdlet [New-TransportRule](https://technet.microsoft.com/it-it/library/bb125138\(v=exchg.150\)) per creare una nuova regola di flusso di posta elettronica che inserisce il prefisso "`External message to Sales DG:`" nei messaggi inviati dall'esterno dell'organizzazione al gruppo di distribuzione reparto vendite.

    New-TransportRule -Name "Mark messages from the Internet to Sales DG" -FromScope NotInOrganization -SentTo "Sales Department" -PrependSubject "External message to Sales DG:"

L'azione utilizzati nella procedura precedente e i parametri delle regole sono solo a scopo illustrativo. Esaminare tutte le condizioni regola flusso di posta elettronica disponibili e azioni per determinare quali soddisfino i requisiti.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver creato correttamente una nuova regola di flusso di posta elettronica, eseguire le operazioni seguenti:

  - In EAC, verificare che la nuova regola di flusso di posta elettronica creata sia elencata nell'elenco **regole**.

  - Exchange Management Shell, verificare creato correttamente la nuova regola di flusso di posta elettronica eseguendo il seguente comando (nell'esempio seguente viene verificata la regola creata nell'esempio sopra riportato Exchange Management Shell ):
    
        Get-TransportRule "Mark messages from the Internet to Sales DG"

## Consente di visualizzare o modificare una regola del flusso di posta elettronica


> [!NOTE]
> Dopo aver creato o modificare una regola del flusso di posta elettronica, possono richiedere fino a 30 minuti per la regola di nuova o aggiornata da applicare alla posta elettronica.



## Utilizzare EAC per visualizzare o modificare una regola del flusso di posta elettronica

1.  Dall'interfaccia di amministrazione di Exchange, andare a **Flusso di posta** \> **Regole**.

2.  Quando si seleziona una regola dall'elenco, le condizioni, le azioni, le eccezioni e le proprietà selezionate per la regola vengono visualizzate nel riquadro dei dettagli. Fare doppio clic su una regola specifica per visualizzarne tutte le proprietà. Verrà aperta la finestra Editor regole, in cui è possibile apportare modifiche alla regola. Per ulteriori informazioni sulle proprietà delle regole, vedere la sezione Use the EAC to create a new Transport rule descritta precedentemente in questo argomento.

## Utilizzare Exchange Management Shell per visualizzare o modificare una regola del flusso di posta elettronica

Negli esempi seguenti viene fornito un elenco di tutte le regole configurate nell'organizzazione:

    Get-TransportRule

Per visualizzare le proprietà di una regola di flusso di posta elettronica specifici, il nome di tale regola o il GUID. È in genere utile inviare l'output al cmdlet **Format-List** per formattare le proprietà. Nell'esempio seguente restituisce tutte le proprietà della regola di flusso di posta denominato **mittente è un membro di Marketing**:

    Get-TransportRule "Sender is a member of marketing" | Format-List

Per modificare le proprietà di una regola esistente, utilizzare il cmdlet[Set-TransportRule](https://technet.microsoft.com/it-it/library/bb123534\(v=exchg.150\)). Questo cmdlet consente di modificare qualsiasi proprietà, condizione, azione o eccezione associata alla regola. Nell'esempio seguente viene aggiunta un'eccezione alla regola "Sender is a member of marketing" in modo che non venga applicata ai messaggi inviati dall'utente Kelly Rollin:

    Set-TransportRule "Sender is a member of marketing" -ExceptIfFrom "Kelly Rollin"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che sia stata modificata correttamente una regola del flusso di posta elettronica, eseguire le operazioni seguenti:

  - Nell'elenco delle regole nell'interfaccia di amministrazione di Exchange, fare clic sulla regola modificata nell'elenco **Regole** e visualizzare il riquadro dei dettagli.

  - Exchange Management Shell, verificare che modificata la regola del flusso di posta elettronica correttamente eseguendo il comando seguente per elencare le proprietà modificate insieme al nome della regola (nell'esempio seguente viene verificata la regola modificata nell'esempio precedente Exchange Management Shell ):
    
        Get-TransportRule "Sender is a member of marketing" | Format-List Name,ExceptIfFrom

## Proprietà delle regole del flusso di posta elettronica

È inoltre possibile utilizzare il cmdlet Set-TransportRule per modificare le regole di trasporto esistenti nell'organizzazione. Di seguito vengono elencati le proprietà non disponibili nell'interfaccia di amministrazione Exchange che è possibile modificare. Per ulteriori informazioni su utilizzando il cmdlet Set-TransportRule per effettuare queste modifiche vedere [Set-TransportRule](https://technet.microsoft.com/it-it/library/bb123534\(v=exchg.150\))


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome della condizione nell'interfaccia di amministrazione di Exchange</th>
<th>Nome della condizione in Exchange Management Shell</th>
<th>Proprietà</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Arrestare l'elaborazione delle regole</strong></p></td>
<td><p><code>StopRuleProcessing </code></p></td>
<td><p><code> Not applicable</code></p></td>
<td><p>Consente di arrestare l'elaborazione delle altre regole</p></td>
</tr>
<tr class="even">
<td><p><strong>Corrispondenza intestazione/busta</strong></p></td>
<td><p><code>SenderAddressLocation </code></p></td>
<td><p>Non applicabile</p></td>
<td><p>Consente di esaminare la busta del messaggio SMTP per garantire l'intestazione e imbustare corrispondenza</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><strong>Controllo gravità</strong></p></td>
<td><p><code>SetAuditSeverity </code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>Consente di selezionare un livello di gravità per il controllo</p></td>
</tr>
<tr class="even">
<td><p><strong>Modalità delle regole</strong></p></td>
<td><p><code>Mode</code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>Consente di impostare la modalità per la regola</p></td>
</tr>
</tbody>
</table>


## Impostare la priorità di una regola del flusso di posta elettronica

La regola nella parte superiore dell'elenco viene elaborata per prima. Questa regola dispone di una **priorità** pari a 0.

## Utilizzo dell'interfaccia di amministrazione di Exchange per impostare la priorità di una regola

1.  Dall'interfaccia di amministrazione di Exchange, andare a **Flusso di posta** \> **Regole**. Vengono visualizzate le regole nell'ordine in cui sono elaborate.

2.  Selezionare una regola e utilizzare le frecce per spostare la regola verso l'inizio o verso la fine dell'elenco.

## Utilizzare il Exchange Management Shell per impostare la priorità di una regola

Nell'esempio seguente la priorità di "Sender is a member of marketing" viene impostata su 2:

    Set-TransportRule "Sender is a member of marketing" priority "2"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che sia stata modificata correttamente una regola del flusso di posta elettronica, eseguire le operazioni seguenti:

  - Dall'elenco delle regole nell'interfaccia di amministrazione di Exchange, osservare l'ordine delle regole.

  - In Exchange Management Shell, verificare la priorità delle regole (nell'esempio seguente viene verificata la regola modificata nell'esempio precedente Exchange Management Shell ):
    
        Get-TransportRule * | Format-List Name,Priority

## Abilitare o disabilitare una regola del flusso di posta elettronica

Le regole vengono attivate quando si crea. È possibile disabilitare una regola del flusso di posta elettronica.

## Utilizzare EAC per abilitare o disabilitare una regola del flusso di posta elettronica

1.  Dall'interfaccia di amministrazione di Exchange, andare a **Flusso di posta** \> **Regole**.

2.  Per disabilitare una regola, deselezionare la casella di controllo accanto al nome.

3.  Per abilitare una regola disabilitata, selezionare la casella di controllo accanto al nome.

## Utilizzare il Exchange Management Shell per abilitare o disabilitare una regola del flusso di posta elettronica

Nell'esempio seguente viene disabilitata la regola di flusso di posta "Sender is a member of marketing":

    Disable-TransportRule "Sender is a member of marketing"

Nell'esempio seguente viene abilitata la regola di flusso di posta elettronica "Sender is a member of marketing":

    Enable-TransportRule "Sender is a member of marketing"

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che hanno corretta abilitazione o disabilitazione di una regola del flusso di posta elettronica, eseguire le operazioni seguenti:

  - Nell'interfaccia di amministrazione di Exchange, visualizzare l'elenco **Regole** e controllare lo stato della casella di controllo nella colonna **ON**.

  - Da Exchange Management Shell, eseguire il seguente comando che restituisce un elenco di tutte le regole all'interno dell'organizzazione con il relativo stato:
    
        Get-TransportRule | Format-Table Name,State

## Rimuovere una regola del flusso di posta elettronica

## Utilizzare EAC per rimuovere una regola del flusso di posta elettronica

1.  Dall'interfaccia di amministrazione di Exchange, andare a **Flusso di posta** \> **Regole**.

2.  Selezionare la regola da eliminare, quindi scegliere **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

## Utilizzare Exchange Management Shell per rimuovere una regola del flusso di posta elettronica

Nell'esempio seguente viene rimossa la regola di flusso di posta elettronica "Sender is a member of marketing":

    Remove-TransportRule "Sender is a member of marketing"

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che sia stata rimossa correttamente la regola del flusso di posta elettronica, eseguire le operazioni seguenti:

  - Nell'interfaccia di amministrazione di Exchange, visualizzare l'elenco **Regole** e verificare che la regola rimossa non sia più visualizzata.

  - Dal Exchange Management Shell, eseguire il seguente comando e verificare che la regola che rimossa non è più elencata:
    
        Get-TransportRule

## Monitorare l'utilizzo della regola

Se si utilizza Exchange Online o Exchange Online Protection, è possibile controllare il numero di volte in cui viene individuata una corrispondenza con una regola tramite un rapporto sulle regole. Affinché una regola sia inserita nei rapporti, è necessario che la casella di controllo **Controlla questa regola con livello di gravità** sia selezionata. È possibile visualizzare un rapporto online o scaricare una versione di Excel di tutti i rapporti sulla protezione della posta.


> [!NOTE]
> Mentre la maggior parte dei dati viene visualizzata nel rapporto entro 24 ore, per alcuni dati potrebbero essere necessari 5 giorni.



## Utilizzare l'interfaccia di amministrazione di Office 365 per generare un rapporto sulle regole

1.  Nell'interfaccia di amministrazione di Office 365, selezionare **Rapporti**.

2.  Nella sezione **Regole**, selezionare **Corrispondenze principali della regola per la posta** oppure **Corrispondenze della regola per la posta**.

Per ulteriori informazioni, vedere [visualizzare i report di protezione posta elettronica](https://go.microsoft.com/fwlink/p/?linkid=402958).

## Scaricare una versione di Excel dei rapporti

1.  Nella pagina Rapporti nell'interfaccia di amministrazione di Office 365, selezionare **Rapporti sulla protezione della posta (Excel)**.

2.  Se è la prima volta che si utilizzano i rapporti sulla protezione della posta in Excel, una scheda indirizzerà alla pagina di download.
    
    1.  Selezionare **Download** per scaricare i plug-in di Microsoft Office 365 Excel di Exchange Online Reporting.
    
    2.  Aprire il download.
    
    3.  Nella casella di dialogo **Impostazioni rapporti sulla protezione della posta per Office 365**, selezionare **Avanti**, accettare i termini del contratto di licenza e selezionare **Avanti**.
    
    4.  Selezionare il servizio che si sta utilizzando, quindi **Avanti**.
    
    5.  Verificare i prerequisiti, quindi selezionare **Avanti**.
    
    6.  Selezionare **Installa**. Sul desktop viene creato un collegamento ai rapporti.

3.  Sul desktop, selezionare **Rapporti sulla protezione della posta per Office 365**.

4.  Nel rapporto, selezionare la scheda **Regole**.

## Importare o esportare una raccolta di regole del flusso di posta elettronica

È necessario utilizzare Exchange Management Shell per importare o esportare una raccolta di regole del flusso di posta elettronica. Per informazioni su come importare una raccolta di regole del flusso di posta elettronica da un file XML, vedere [Import-TransportRuleCollection](https://technet.microsoft.com/it-it/library/bb123582\(v=exchg.150\)). Per informazioni su come esportare una raccolta di regole del flusso di posta elettronica in file XML, vedere [Export-TransportRuleCollection](https://technet.microsoft.com/it-it/library/bb124410\(v=exchg.150\)).

## Per informazioni dettagliate,

Risorse per Exchange Online:

[Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\))

[Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online](https://technet.microsoft.com/it-it/library/jj919235\(v=exchg.150\))

[Posta azioni delle regole del flusso di Exchange Online](https://technet.microsoft.com/it-it/library/jj919237\(v=exchg.150\))

[Limiti di regola di trasporto e posta in arrivo](https://go.microsoft.com/fwlink/p/?linkid=324584)

Risorse per Exchange Online Protection:

[Regole del flusso di posta (regole di trasporto in Exchange Online Protection](https://technet.microsoft.com/it-it/library/dn271424\(v=exchg.150\))

[Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online Protection](https://technet.microsoft.com/it-it/library/jj919234\(v=exchg.150\))

[Posta elettronica di azioni delle regole del flusso di Exchange Online Protection](https://technet.microsoft.com/it-it/library/jj920117\(v=exchg.150\))

[Limiti di regola di trasporto e posta in arrivo](https://go.microsoft.com/fwlink/p/?linkid=324584)

Risorse per Exchange Server 2013:

[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Azioni della regola di trasporto](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

