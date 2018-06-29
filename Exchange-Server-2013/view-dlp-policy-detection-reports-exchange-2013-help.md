---
title: 'Visualizzare i report di rilevamento dei criteri DLP: Exchange 2013 Help'
TOCTitle: Visualizzare i report di rilevamento dei criteri DLP
ms:assetid: 5c3f1cf6-d8c7-4d83-bb24-641ea9d50cbc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150520(v=EXCHG.150)
ms:contentKeyID: 50479740
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzare i report di rilevamento dei criteri DLP

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-16_

In generale, gestione rilevamento criteri criterio DLP perdita di dati definisce le attività che esegue un'organizzazione per poter identificare, analizzare e risolvere violazioni dei criteri DLP. Per gestire i problemi, è necessario accedere a informazioni che identifica quali è stata rilevata per i criteri DLP. Queste informazioni di rilevamento sono integrate con dati Exchange Server 2013 Microsoft esistenti e registro viene formattato in modo che è possibile utilizzare un sistema esistente avanzato dei dati per la gestione degli interventi di flusso di posta elettronica.

Per informazioni sulla creazione di un rapporto sull'incidente insieme a un evento di rilevamento singolo criterio, vedere [Creare i rapporti operazioni non consentite per i rilevamenti di criteri DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md). Per ulteriori informazioni sui registri dei messaggi, vedere [Tenere traccia dei messaggi con i rapporti di recapito](track-messages-with-delivery-reports-exchange-2013-help.md).


> [!NOTE]
> Exchange 2013: Prevenzione perdita dati (DLP) è una funzionalità premium che richiede una licenza di accesso client (CAL, Client Access License) di Enterprise di Exchange. Per ulteriori informazioni sulle licenze CAL e sulla gestione delle licenze server, vedere l'articolo relativo alla <A href="https://go.microsoft.com/fwlink/p/?linkid=237292">gestione delle licenze di Exchange Server</A>.



## Informazioni di controllo

Dati relativi alla gestione rilevamento DLP di Exchange sono integrati in messaggio di verifica dei registri, noto anche come rapporti di mancato recapito. Le funzionalità di riutilizzare gran parte del framework di registrazione esistente disponibile nel sistema. Per informazioni generali, incluse informazioni sulla struttura dei file di registro di verifica messaggi esaminare il contenuto esistente in [Understanding Message Tracking](message-tracking-exchange-2013-help.md) o [Tenere traccia dei messaggi con i rapporti di recapito](track-messages-with-delivery-reports-exchange-2013-help.md).

Il rapporto di recapito è un registro dettagliato di tutte le attività di messaggio come i messaggi vengono trasferiti a e da un computer in cui è in esecuzione il servizio di trasporto su un server cassette postali. Registro di verifica messaggi sia possono accedere tramite Exchange Management Shell utilizzando il cmdlet **Get-MessageTrackingLog** . Dati DLP sono integrati nel rapporto di recapito seguenti formati di dati e le convenzioni di esistenti.

## Formato di registrazione dei dati

Registri di verifica messaggi contengono dati da agenti coinvolti nell'elaborazione del contenuto di flusso di posta elettronica. Per DLP, l'agente regole di trasporto (TRA) viene utilizzato per richiamare la scansione del contenuto di messaggio completa e applicare i criteri definiti come parte della ETRs. L'evento AgentInfo esistente viene utilizzato per aggiungere DLP relative voci nel Registro di verifica messaggi.

Il nome dell'agente sarà **TRA** o **Agente della regola di trasporto** nell'evento AgentInfo. Verrà registrato un evento AgentInfo singolo per ogni messaggio che descrive l'elaborazione DLP applicato al messaggio. Il campo **CustomData** del campo della voce del Registro di verifica dei messaggi è dove verranno visualizzati i dati DLP registrati dall'agente regole di trasporto. In questo campo può contenere più voci: riga di informazioni di classificazione e i client dei uno dati per ogni classificazione di dati trovato nel messaggio, riga di una regola per ogni regola si applica al messaggio e una riga di monitoraggio dello stato per ogni regola che supera la soglia di caricamento o il tempo di esecuzione.

Di seguito viene visualizzato un esempio di voce del registro DLP. L'output è stata formattata per visualizzare le stringhe su righe separate con nuove righe tra.

Origine: AGENTE

EventId: AGENTINFO

CustomData: S:TRA DC = | dcid = 41BFDBC6C9D811E0816A3CD34824019B | count = 10 | conf = 77;

S:tra = DC | dcid = C7ECCBA0CA0011E0B6C00B124924019B | count = 3 | conf = 81;

S:tra = CI | sndOverride inglese o | appena = motivi aziendali;

S:TRA=CI|sndOverride=fp;

S:TRA=ETR|ruleId=FC2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=PrependSubject|action=Encrypt|sev=2|mode=audit|dcid=41BFDBC6C9D811E0816A3CD34824019B|sndOverride=or;

S:TRA=ETR|ruleId=AB2AA60C9D811E0AFC076D34824019B|dlpid=1B81CC82C9DB11E09052C5D64824019B|st=2010-11-03 15:30T|action=Encrypt|sev=1|mode=enabled|dcid=C7ECCBA0CA0011E0B6C00B124924019B|sndOverride=fp;

S:TRA=ETRP|ruleId=C27D21EECA0311E0BCB896154924019B|LoadW=200|LoadC=100|ExecW=5500|ExecC=200;

Agente regole di trasporto sono necessari della regola di raggruppamento ID DLP Policy ID (facoltativo) ultima data, azione, gravità, modalità di rilevamento classificazione dei dati (facoltativo) e sostituzione mittente (facoltativo) in base all'ID regola (indicata dal "TRA = ETR" nella riga registro). È necessario anche l'ID di classificazione dei dati, count e livello di probabilità di classificazioni raggruppate in base al nome di classificazione (indicato da "TRA DC =" nella riga registro).

Ulteriori raggruppamenti includere l'ID di classificazione dei dati, sostituzione mittente (facoltativo) ed eseguire l'override di giustificazione (facoltativa) in base all'ID di classificazione dei dati per tutte le classificazioni che sono stati rilevati nel client (indicata dal "TRA = CI" nella riga registro). Agente regole di trasporto richiede anche l'ID della regola, il carico orologio (facoltativo) parete, clock della CPU del carico (facoltativo), orologio parete esecuzione (facoltativo) e l'esecuzione CPU raggruppare in base all'ID regola orologio (facoltativo) per tutte le regole che superano il carico parete / o CPU clock soglie (indicata dal "TRA = ETRP" nella riga registro).

Di seguito è riportato un elenco completo dei campi dati. Tutti i dati di MTL è di tipo string. Nella colonna formato viene descritto come riconoscere ogni campo nel Registro di verifica dei messaggi. Colonna campo facoltativo specifica quali campi potrebbero non essere registrati quando corrisponde a una regola. DLP specifica colonna Visualizza tutti i campi sono specifici per la funzionalità DLP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Nome del campo</strong></p></td>
<td><p><strong>Descrizione</strong></p></td>
<td><p><strong>Formato</strong></p></td>
<td><p><strong>Campo facoltativo</strong></p></td>
<td><p><strong>DLP specifico</strong></p></td>
</tr>
<tr class="even">
<td><p>TRA</p></td>
<td><p>Agente della regola di trasporto; Digitare AgentName</p></td>
<td><p>TRA = controller di dominio, ETR, CI o ETRP</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>DC</p></td>
<td><p>Classificazione dei dati; Digitare groupName</p></td>
<td><p>TRA DC =</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>ETR</p></td>
<td><p>Regola di trasporto di Exchange. Digitare groupName</p></td>
<td><p>TRA = ETR</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>CI</p></td>
<td><p>Informazioni sul client, tipo groupName</p></td>
<td><p>TRA = CI</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>ETRP</p></td>
<td><p>Prestazioni della regola di trasporto Exchange; Digitare groupName</p></td>
<td><p>TRA = ETRP</p></td>
<td><p>Facoltativo</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>dcid</p></td>
<td><p>ID della classificazione di dati</p></td>
<td><p>dcid = GUID</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>conteggio</p></td>
<td><p>Conteggio della classificazione di dati</p></td>
<td><p>conteggio = intero</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>conf</p></td>
<td><p>Livello di probabilità della classificazione di dati</p></td>
<td><p>conf = intero (%)</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>sndOverride</p></td>
<td><p>Sostituzione di mittente; il campo è facoltativo.</p>
<p>Nel TRA = CI riga quando campo è impostata su &quot;o&quot; indica che la classificazione dei dati è stato sottoposto a override. Se nel campo è impostato su &quot;PF&quot; indica che la classificazione dei dati è stato segnalato come falso positivo.</p>
<p>Nel TRA = riga ETR, quando il campo è impostato su &quot;o&quot; indica la regola o è stato sottoposto a override parte della regola. Se il campo è impostato su &quot;PF&quot; indica la regola o parte della regola è stata dichiarata come falso positivo.</p></td>
<td><p>sndOverride inglese o o PF</p>
<p>Dove &quot;o&quot; rappresenta l'override e &quot;PF&quot; significa falso positivo. Il campo sndOverride è presente quando un utente finale ha segnalato una sostituzione o un falso positivo per una regola.</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>solo</p></td>
<td><p>Giustificazione; il campo è facoltativo e sono disponibili solo quando il campo Ignora mittente è uguale a &quot;o&quot; in TRA la riga CI =. Giustificazione testo fornito dall'utente finale come motivo della classificazione dei dati deve essere sottoposto a override.</p></td>
<td><p>solo = Information Worker giustificazione input stringa</p>
<p>Campo giustificazione viene registrato solo quando l'utente finale segnala una sostituzione.</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>ruleId</p></td>
<td><p>ID di una regola</p></td>
<td><p>ruleId=GUID</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>dlpId</p></td>
<td><p>ID per un criterio DLP. Il campo è facoltativo. Se non esiste alcun dlpId la regola non appartiene a un criterio DLP.</p></td>
<td><p>dlpId=GUID</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>st</p></td>
<td><p>Data ultima modifica di una regola</p></td>
<td><p>ST = data e ora UTC</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>azione</p></td>
<td><p>Azione eseguita da una regola; potrebbe includere più azioni per ogni regola</p></td>
<td><p>azione = singola azione</p>
<p>Se sono presenti più azioni applicate per una regola, ci sarà più campi di azione.</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>gravità</p></td>
<td><p>Gravità della regola di controllo</p></td>
<td><p>gravità = 1, 2 o 3</p>
<p>Dove 1 corrisponde a bassa, 2 è medium e 3 significa elevata.</p></td>
<td><p>Facoltativo</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>modalità</p></td>
<td><p>Informazioni sullo stato della regola quando era hit test (l'applicazione, controllo o auditandnotify).</p></td>
<td><p>modalità = controllo, auditandnotify o l'applicazione</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>loadW</p></td>
<td><p>Carico parete Clock; il campo è facoltativo</p></td>
<td><p>loadW = tempo in millisecondi</p></td>
<td><p>Facoltativo</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>loadC</p></td>
<td><p>Carico CPU Clock; il campo è facoltativo</p></td>
<td><p>loadC = tempo in millisecondi</p></td>
<td><p>Facoltativo</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>execW</p></td>
<td><p>Esecuzione di Clock parete; il campo è facoltativo</p></td>
<td><p>execW = tempo in millisecondi</p></td>
<td><p>Facoltativo</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>execC</p></td>
<td><p>Esecuzione di Clock della CPU; il campo è facoltativo</p></td>
<td><p>execC = tempo in millisecondi</p></td>
<td><p>Facoltativo</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>id messaggio</p></td>
<td><p>ID del messaggio</p></td>
<td><p>id messaggio = ID del messaggio</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Data-ora</p></td>
<td><p>Data e ora che è stato inviato il messaggio nel tempo universale</p></td>
<td><p>Data / ora = data e ora UTC</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>indirizzo mittente</p></td>
<td><p>Indirizzo di posta elettronica specificato nel campo mittente</p></td>
<td><p>indirizzo mittente = indirizzo di posta elettronica</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>indirizzo destinatario</p></td>
<td><p>Indirizzi dei destinatari del messaggio di posta elettronica</p></td>
<td><p>indirizzo destinatario = indirizzo di posta elettronica</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>oggetto del messaggio</p></td>
<td><p>Dati trovati nel campo oggetto del messaggio</p></td>
<td><p>oggetto messaggio = stringa di input dell'utente finale</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Creare i rapporti operazioni non consentite per i rilevamenti di criteri DLP](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)

[Tenere traccia dei messaggi con i rapporti di recapito](track-messages-with-delivery-reports-exchange-2013-help.md)

