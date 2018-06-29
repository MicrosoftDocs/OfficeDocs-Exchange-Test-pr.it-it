---
title: 'Messaggi di saluto, istruzioni e lingue di messaggistica UNIFICATA: Exchange 2013 Help'
TOCTitle: Messaggi di saluto, istruzioni e lingue di messaggistica UNIFICATA
ms:assetid: d48df962-9669-420b-838f-44bfe1012e2f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124728(v=EXCHG.150)
ms:contentKeyID: 50481759
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Messaggi di saluto, istruzioni e lingue di messaggistica UNIFICATA

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

È possibile installare e configurare Language Pack per supportare più lingue negli ambienti di messaggistica unificata.

I Language Pack di messaggistica unificata consentono ai chiamanti e agli utenti di Outlook Voice Access di interagire con il sistema di caselle vocali in più lingue. Dopo avere installato una lingua supplementare in un server Cassette postali, i chiamanti e gli utenti di Outlook Voice Access potranno ascoltare i messaggi di posta elettronica e interagire con il sistema di caselle vocali nella lingua specificata.

Esistono diversi componenti fondamentali su cui i Language Pack di messaggistica unificata si basano per consentire agli utenti e ai chiamanti di interagire in modo efficiente con la messaggistica unificata in più lingue. Ogni Language Pack di messaggistica unificata comprende un motore di sintesi vocale (TTS), le istruzioni vocali preregistrate e il supporto per il riconoscimento vocale automatico (ASR) e l'anteprima della posta vocale per una lingua specifica. In questo argomento vengono descritti i Language Pack di messaggistica unificata, i componenti di messaggistica unificata che utilizzano tali supporti e come è possibile utilizzare i Language Pack di messaggistica unificata, dopo l'installazione, per configurare i dial plan di messaggistica unificata e gli operatori automatici di messaggistica unificata per l'utilizzo di altre lingue.

Exchange Language pack di messaggistica unificata sono specifiche di piattaforma e versione. Successivamente Exchange Server 2007, sono stati più versioni per i language pack di messaggistica UNIFICATA, tra cui la versione RTM di Exchange 2007, Exchange 2007 SP1, SP2 e SP3, la versione RTM di Exchange Server 2010, Exchange 2010 SP1 e Service Pack 2 e Exchange 2013. Per alcune di queste versioni download sia a 32 bit e 64 bit sono disponibili, ma per altre versioni download solo a 64 bit sono disponibili.

È molto importante installare la versione e la piattaforma corrette dei Language Pack di messaggistica unificata su un server Cassette postali. Non installare Language Pack di messaggistica unificata su un server Cassette postali installato su una versione precedente di Exchange o progettato per una piattaforma a 32 bit.

**Sommario**

Overview of UM language packs

UM language components and features

Voice Mail Preview

Unified Messaging languages

Unified Messaging language packs

UM dial plan languages

UM auto attendant languages

Client language selection process

## Cenni preliminari sui Language Pack di messaggistica unificata

I Language Pack di messaggistica unificata consentono a un server Cassette postali di utilizzare altre lingue per la conversazione con i chiamanti o di riconoscere altre lingue quando i chiamanti utilizzano ASR o durante la trascrizione dei messaggi vocali. I Language Pack di messaggistica unificata contengono:

  - Prompt preregistrati nella lingua del Language Pack di messaggistica unificata. Ad esempio, "Dopo il segnale acustico, registrare il proprio messaggio. Al termine della registrazione, riagganciare o premere il tasto \# per ottenere altre opzioni."

  - I file di grammatica nella lingua del Language Pack di messaggistica unificata, utilizzati da un server Cassette postali per ricercare i nomi degli utenti nella directory.

  - La conversione di sintesi vocale (TTS), in modo che il contenuto (messaggi di posta elettronica, calendario, informazioni di contatto e così via) possa essere letto ai chiamanti nella lingua del Language Pack di messaggistica unificata.

  - Supporto per il riconoscimento vocale automatico (ASR), che consente ai chiamanti di interagire con la messaggistica unificata utilizzando l'interfaccia vocale (VUI) nella lingua del Language Pack di messaggistica unificata.

  - Supporto per l'anteprima della posta vocale, che consente agli utenti di leggere la trascrizione dei messaggi vocali in una lingua specifica all'interno di un client di posta elettronica supportato, come Outlook o Outlook Web App.

I Language Pack di messaggistica unificata contengono istruzioni vocali preregistrate, il supporto per la conversione della sintesi vocale per una data lingua e, in alcuni casi, il supporto per il riconoscimento vocale automatico. Negli ambienti multilingue, è possibile installare altri Language Pack di messaggistica unificata in quanto alcuni chiamanti preferiscono essere informati in una lingua diversa oppure perché essi ricevono messaggi di posta elettronica in più lingue. È necessario installare più Language Pack di messaggistica unificata per supportare la capacità del server Cassette postali di leggere un messaggio di posta elettronica contenente più lingue. Il sistema di conversione TTS deve infatti essere istruito in merito alla lingua da selezionare in funzione del testo del messaggio da leggere. Se il Language Pack di messaggistica unificata non è stato installato, il messaggio di posta elettronica verrà letto all'utente in modo illogico e incoerente. L'installazione del Language Pack appropriato consente al motore TTS di leggere i messaggi di posta elettronica e gli elementi del calendario all'utente di Outlook Voice Access utilizzando la lingua corretta, fornendo anche istruzioni vocali preregistrate per la messaggistica unificata specifiche della lingua prescelta. In alcuni casi, possono fornire anche un supporto per ASR.


> [!NOTE]
> Il motore di sintesi vocale converte il testo in un discorso vocale ma non esegue l'operazione inversa. Gli utenti abilitati alla messaggistica unificata possono inviare a un altro utente un messaggio di posta elettronica con un file vocale allegato. Tuttavia, non possono creare e inviare un messaggio di posta elettronica basato su testo a un altro utente.



Quando si installa un Language Pack, il programma di installazione esegue la seguente procedura:

1.  Copia i prompt della lingua che saranno utilizzati per configurare gli operatori automatici e i dial plan di messaggistica unificata.

2.  Consente al modulo TTS di leggere i messaggi quando un utente di Outlook Voice Access accede alla Posta in arrivo.

3.  Consente il riconoscimento vocale automatico per i dial plan e gli operatori automatici di messaggistica unificata abilitati al servizio di sintesi vocale per la lingua installata.

4.  Consente l'anteprima della posta vocale per i client in altre lingue.

È possibile aggiungere i language pack di messaggistica UNIFICATA utilizzando il comando **Setup.exe** oppure eseguendo il programma di installazione .exe *\<UMLanguagePack\>*dopo aver scaricato il language pack di messaggistica UNIFICATA di [Exchange Server 2013 messaggistica UNIFICATA di Language Pack](https://go.microsoft.com/fwlink/p/?linkid=266542). Tuttavia, è necessario utilizzare il comando Setup.exe per rimuovere un language pack di messaggistica UNIFICATA. Non esiste alcun cmdlet Management Shell Exchange utilizzabile per aggiungere o rimuovere lingue da un server cassette postali. Per ulteriori informazioni su come installare un language pack di messaggistica UNIFICATA, vedere [Installare un Language Pack di messaggistica unificata](install-a-um-language-pack-exchange-2013-help.md). Per ulteriori informazioni su come rimuovere un language pack di messaggistica UNIFICATA, vedere [Rimuovere un language pack di messaggistica unificata](remove-a-um-language-pack-exchange-2013-help.md).


> [!NOTE]
> Per impostazione predefinita, quando si installa un server Cassette postali, viene installato il Language Pack per inglese americano (en-US). Non è possibile rimuoverle, a meno che non si rimuova il server Cassette postali dal computer.



Inizio pagina

Nella seguente tabella sono elencati i Language Pack di messaggistica unificata attualmente disponibili. Sono inoltre indicati i nomi dei file di installazione per ciascun Language Pack di messaggistica unificata e l'ID della lingua di messaggistica unificata.

### Nomi file e ID della lingua per l'installazione dei Language Pack di messaggistica unificata

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Lingua</th>
<th>Paese</th>
<th>ID lingua</th>
<th>Nome del file di installazione</th>
<th>Disponibilità</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Catalano</p></td>
<td><p>Spagna</p></td>
<td><p>ca-ES</p></td>
<td><p>UMLanguagePack.ca-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Cinese (Hong Kong)</p></td>
<td><p>Cina</p></td>
<td><p>zh-HK</p></td>
<td><p>UMLanguagePack.zh-HK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Cinese (semplificato)</p></td>
<td><p>Cina</p></td>
<td><p>zh-CHS</p></td>
<td><p>UMLanguagePack.zh-CN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Cinese (tradizionale)</p></td>
<td><p>Taiwan</p></td>
<td><p>zh-TW</p></td>
<td><p>UMLanguagePack.zh-TW</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Danese</p></td>
<td><p>Danimarca</p></td>
<td><p>da-DK</p></td>
<td><p>UMLanguagePack.da-DK</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Olandese</p></td>
<td><p>Paesi Bassi</p></td>
<td><p>nl-NL</p></td>
<td><p>UMLanguagePack.nl-NL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Inglese</p></td>
<td><p>Australia</p></td>
<td><p>en-AU</p></td>
<td><p>UMLanguagePack.en-AU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Inglese</p></td>
<td><p>Canada</p></td>
<td><p>en-CA</p></td>
<td><p>UMLanguagePack.en-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Inglese</p></td>
<td><p>India</p></td>
<td><p>en-IN</p></td>
<td><p>UMLanguagePack.en-IN</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Inglese</p></td>
<td><p>Regno Unito</p></td>
<td><p>en-GB</p></td>
<td><p>UMLanguagePack.en-GB</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Inglese</p></td>
<td><p>Stati Uniti</p></td>
<td><p>en-US</p></td>
<td><p>Incluso con l'installazione di un server Cassette postali</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Finlandese</p></td>
<td><p>Finlandia</p></td>
<td><p>fi-Fl</p></td>
<td><p>UMLanguagePack.fi-Fl</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Francese</p></td>
<td><p>Canada</p></td>
<td><p>fr-CA</p></td>
<td><p>UMLanguagePack.fr-CA</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Francese</p></td>
<td><p>Francia</p></td>
<td><p>fr-FR</p></td>
<td><p>UMLanguagePack.fr-FR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Tedesco</p></td>
<td><p>Germania</p></td>
<td><p>de-DE</p></td>
<td><p>UMLanguagePack.de-DE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Italiano</p></td>
<td><p>Italia</p></td>
<td><p>it-IT</p></td>
<td><p>UMLanguagePack.it-IT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Giapponese</p></td>
<td><p>Giappone</p></td>
<td><p>ja-JP</p></td>
<td><p>UMLanguagePack.ja-JP</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Coreano</p></td>
<td><p>Coreano</p></td>
<td><p>ko-KR</p></td>
<td><p>UMLanguagePack.ko-KR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Norvegese (Bokmål)</p></td>
<td><p>Norvegia</p></td>
<td><p>nb-NO</p></td>
<td><p>UMLanguagePack.nb-NO</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Polacco</p></td>
<td><p>Polonia</p></td>
<td><p>pl-PL</p></td>
<td><p>UMLanguagePack.pl-PL</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Portoghese</p></td>
<td><p>Brasile</p></td>
<td><p>pt-BR</p></td>
<td><p>UMLanguagePack.pt-BR</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Portoghese</p></td>
<td><p>Portogallo</p></td>
<td><p>pt-PT</p></td>
<td><p>UMLanguagePack.pt-PT</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Russo</p></td>
<td><p>Russia</p></td>
<td><p>ru-RU</p></td>
<td><p>UMLanguagePack.ru-RU</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Spagnolo</p></td>
<td><p>Spagna</p></td>
<td><p>es-ES</p></td>
<td><p>UMLanguagePack.es-ES</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="odd">
<td><p>Spagnolo</p></td>
<td><p>Messico</p></td>
<td><p>es-MX</p></td>
<td><p>UMLanguagePack.es-MX</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
<tr class="even">
<td><p>Svedese</p></td>
<td><p>Svezia</p></td>
<td><p>sv-SE</p></td>
<td><p>UMLanguagePack.sv-SE</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=266542">Download disponibile</a></p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Componenti e funzionalità della lingua di messaggistica unificata

Esistono diversi componenti e funzionalità fondamentali nella messaggistica unificata che consentono agli utenti e ai chiamanti di interagire con un sistema di caselle vocali della messaggistica unificata multilingue. Per il corretto funzionamento di questi componenti e funzionalità e per consentire ai chiamanti di interagire con il sistema in più lingue, i Language Pack di messaggistica unificata devono essere installati in modo corretto su un server Cassette postali.

## Istruzioni vocali preregistrate

Il ruolo del server Cassette postali viene installato con un insieme di file di istruzioni audio predefinite. Questi file audio contengono le registrazioni per i menu di Outlook Voice Access, i messaggi di saluto per il sistema di caselle vocali e i numeri utilizzati dalla messaggistica unificata di Exchange. I file audio vengono riprodotti su un server Cassette postali per le chiamate interne ed esterne in arrivo. Molti file audio sono istruzioni predefinite che forniscono agli utenti dell'interfaccia utente telefonica (TUI, telephony user interface) e di Outlook Voice Access le informazioni necessarie per spostarsi all'interno dell'interfaccia TUI e dell'interfaccia utente vocale (VUI, voice user interface). Le istruzioni si trovano in \<*Programmi*\>\\Microsoft\\Exchange Server\\V15\\UnifiedMessaging\\Prompts\\\<lingua\>. Le istruzioni vocali utilizzate dal server Cassette postali per aiutare i chiamanti a spostarsi all'interno dei menu non devono essere sostituite né modificate.

Tuttavia, se viene installato un Language Pack di messaggistica unificata aggiuntivo, verranno installati anche i prompt preregistrati per la lingua in questione. Una volta installato un Language Pack di messaggistica unificata, i prompt preregistrati per tale lingua possono essere utilizzati dagli operatori automatici e dai dial plan di messaggistica unificata.

## Lingue di sintesi vocale

La messaggistica unificata si basa sul motore di sintesi vocale (TTS). La funzionalità TTS viene fornita dal servizio Microsoft Speech Server. Il motore di sintesi vocale legge e converte il testo scritto in un output udibile che può essere ascoltato dal chiamante. Il modulo di sintesi vocale legge e converte i seguenti tipi di elementi in una cassetta postale dell'utente:

  - Corpo, oggetto e nome dei messaggi di posta elettronica e vocali

  - Corpo, oggetto, posizione e nome degli elementi del calendario

  - Nomi dei contatti personali

  - Messaggi di saluto predefiniti per il sistema di caselle vocali degli utenti


> [!NOTE]
> Una volta registrati i messaggi di saluto personalizzati per il sistema di caselle vocali, la versione della sintesi vocale dei messaggi di saluto non verrà più utilizzata.



## Riconoscimento vocale automatico

Oltre alla sintesi vocale, nella messaggistica unificata è incluso il supporto ASR. La funzionalità ASR viene fornita dal servizio Microsoft Speech Server. Il riconoscimento vocale automatico consente ai chiamanti di utilizzare i comandi vocali per spostarsi all'interno dei menu e interagire con gli elementi provenienti dalle cassette postali individuali, compresi messaggi, contatti personali e calendario. Il supporto del riconoscimento vocale automatico è incluso in ogni Language Pack.

Inizio pagina

## Anteprima della posta vocale

I Language Pack di messaggistica unificata forniscono inoltre il supporto per l'anteprima della posta vocale, che consente agli utenti di scorrere velocemente i messaggi vocali leggendo le trascrizioni da un client di posta elettronica supportato come Outlook o Outlook Web App.

Quando un chiamante lascia un messaggio vocale per un utente abilitato alla messaggistica unificata, il file del messaggio vocale e una trascrizione relativa vengono inseriti nel corpo del messaggio vocale inviato alla cassetta postale dell'utente.

Tutti i Language Pack di messaggistica unificata sono singoli file che possono essere scaricati. Questi Language Pack includono i prompt preregistrati, i file di grammatica, la conversione della sintesi vocale (TTS) e il riconoscimento vocale automatico. Tuttavia, non tutti i Language Pack di messaggistica unificata contengono il supporto per l'anteprima della posta vocale.

I seguenti Language Pack di messaggistica unificata contengono il supporto per tutti i componenti e tutte le funzionalità, compresa l'anteprima della posta vocale:

  - Inglese (Stati Uniti) - (en-US)

  - Inglese (Canada) (en-CA)

  - Francese (Francia) - (fr-FR)

  - Italiano - (it-IT)

  - Polacco (pl-PL)

  - Portoghese (Portogallo) (pt-PT)

  - Spagnolo (Spagna) (es-ES)

Per impostazione predefinita, quando si installa il server Cassette postali, il server invierà le anteprime della posta vocale agli utenti abilitati alla messaggistica unificata, se è installato un Language Pack di messaggistica unificata supportato.

Sono disponibili i partner dell'anteprima di posta vocale di messaggistica unificata che offrono un supporto di trascrizione avanzato per la funzionalità corrispondente. Tali partner utilizzano persone che correggono le trascrizioni della posta vocale create utilizzando il riconoscimento vocale automatico. Ogni partner dell'anteprima di posta vocale deve soddisfare una serie di requisiti per ottenere la certificazione e interagire con la messaggistica unificata.

Se si rileva che le anteprime posta vocali inviati a utenti non sono abbastanza accurati, è possibile contattare uno dei partner certificati Anteprima messaggio vocale elencate nella pagina [Individuare Microsoft per la messaggistica unificata](https://go.microsoft.com/fwlink/p/?linkid=261951) e accesso backup con loro un costo aggiuntivo.

È possibile scaricare i language pack di messaggistica UNIFICATA dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542). Per ulteriori informazioni, vedere [Installare un Language Pack di messaggistica unificata](install-a-um-language-pack-exchange-2013-help.md).

## Lingue di messaggistica unificata

Per abilitare i chiamanti all'utilizzo delle funzionalità multilingue disponibili nella messaggistica unificata, è anzitutto necessario installare un Language Pack di messaggistica unificata. L'utente potrà quindi configurare altri componenti di messaggistica unificata.

  - Installare il Language Pack di messaggistica unificata sui server Cassette postali dell'organizzazione.

  - Se necessario, configurare la lingua predefinita per un dial plan di messaggistica unificata. Questo consente agli utenti di Outlook Voice Access associati al dial plan di messaggistica unificata di utilizzare la nuova lingua durante l'accesso alla loro cassetta postale. Gli utenti possono tuttavia configurare l'impostazione della lingua dalle opzioni di Outlook Web App.

  - Per abilitare più lingue negli operatori automatici, configurare le impostazioni della lingua per un operatore automatico di messaggistica unificata. Per impostazione predefinita, un operatore automatico di messaggistica unificata utilizza la lingua del dial plan di messaggistica unificata. È comunque possibile modificare questa impostazione e consentire ai chiamanti non autenticati di connettersi all'organizzazione e di spostarsi nei menu dell'operatore automatico di messaggistica unificata nella lingua specificata.

## Language Pack di messaggistica unificata

Installare un Language Pack di messaggistica unificata sul server Cassette postali mediante Setup.exe. Una volta installato il nuovo Language Pack, la lingua associata al Language Pack verrà aggiunta all'elenco delle lingue disponibili per l'uso. È possibile visualizzare le lingue che sono state installate utilizzando il cmdlet [Get-UMService](https://technet.microsoft.com/it-it/library/jj552407\(v=exchg.150\)) in Exchange Management Shell.

Quando si installa la lingua di messaggistica UNIFICATA pack, i file che vengono utilizzati dal motore di sintesi VOCALE e le istruzioni per la lingua scelta preregistrate vengono copiate e reso disponibile per gli utenti che si connettono al sistema di segreteria telefonica. È possibile scaricare i language pack di messaggistica UNIFICATA dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542). Per ulteriori informazioni, vedere [Installare un Language Pack di messaggistica unificata](install-a-um-language-pack-exchange-2013-help.md).

## Lingue del dial plan di messaggistica unificata

Ogni dial plan di messaggistica unificata creato contiene un'impostazione predefinita della lingua. È necessario impostare la lingua per il dial plan di messaggistica unificata perché la messaggistica unificata potrebbe dover utilizzare la conversione della sintesi vocale o riprodurre un'istruzione audio standard per gli utenti di Outlook Voice Access che accedono alla propria cassetta postale. Non è necessario selezionare una lingua predefinita per il dial plan.

Alla prima installazione di Exchange, la lingua predefinita, nonché l'unica disponibile per il dial plan, è Inglese (Stati Uniti). Una volta installato un Language Pack di messaggistica unificata su un server Cassette postali, anche la lingua associata al Language Pack verrà elencata come opzione disponibile durante la configurazione della lingua predefinita per il dial plan.

La lingua predefinita è importante per i chiamanti. Se un utente di Outlook Voice Access chiama il sistema di caselle vocali, l'impostazione utilizzata si basa sull'impostazione della lingua in Outlook Web App, impostata al primo accesso alla cassetta postale da parte dell'utente. La messaggistica unificata confronta la lingua impostata in Outlook Web App con l'elenco delle lingue disponibili sul dial plan associato all'utente. Se non esiste una corrispondenza appropriata, verrà utilizzata la lingua del dial plan di messaggistica unificata predefinita. Se ad esempio si dispone di un dial plan contenente solo utenti francesi, l'utente avrà la possibilità di modificare l'impostazione della lingua predefinita del dial plan su Francese.

## Lingue degli operatori automatici di messaggistica unificata

Per impostazione predefinita, gli operatori automatici di messaggistica unificata sono associati a un dial plan di messaggistica unificata al momento della creazione e utilizzano quindi l'impostazione della lingua predefinita del dial plan di messaggistica unificata associato. Tuttavia, è possibile modificare questa impostazione dopo avere creato l'operatore automatico di messaggistica unificata.

L'impostazione della lingua dell'operatore automatico di messaggistica unificata è utile perché la messaggistica unificata può avere bisogno di utilizzare la conversione della sintesi vocale oppure di riprodurre un prompt audio standard a un chiamante. La messaggistica unificata non consente di controllare che la lingua dei prompt personalizzati dell'operatore automatico corrisponda all'impostazione della lingua sull'operatore automatico. Tuttavia, si consiglia di verificare che l'impostazione della lingua dell'operatore automatico corrisponda alla lingua dei prompt personalizzati. In caso contrario, il chiamante può sentire che il sistema passa da una lingua all'altra.

La possibilità di modificare l'impostazione della lingua dell'operatore automatico di messaggistica unificata è utile anche nel caso in cui siano richiesti diversi operatori automatici inerenti alla lingua per i chiamanti.

## Processo di selezione della lingua del client

I Language Pack di messaggistica unificata consentono ai chiamanti e agli utenti di Outlook Voice Access di interagire con il sistema di messaggistica unificata in più lingue. Dopo avere installato Language Pack supplementari su un server Cassette postali, i chiamanti e gli utenti di Outlook Voice Access potranno ascoltare i messaggi di posta elettronica e interagire con il sistema di caselle vocali. Gli utenti di Outlook Web App e quelli che utilizzano Outlook 2010 o una versione successiva potranno visualizzare la trascrizione di un messaggio vocale utilizzando Anteprima casella vocale in una lingua specifica.

Per supportare una lingua specifica, è necessario installare un Language Pack client di messaggistica unificata su ogni server Cassette postali.

In alcuni casi, se non è stato installato e quindi non è disponibile un Language Pack di messaggistica unificata per una lingua specifica, è possibile utilizzare una lingua di fallback client. Le lingue client di messaggistica unificata di fallback possono essere utilizzate al posto di altre lingue ma sono disponibili solo per alcune lingue. Se non è stato installato un Language Pack di messaggistica unificata per una lingua specifica e per tale lingua non è disponibile una lingua di fallback, viene utilizzata la lingua en-US (inglese Stati Uniti).

Nella seguente tabella è incluso un elenco delle lingue client e delle lingue di fallback utilizzate quando su un server Cassette postali non è installato uno specifico Language Pack di messaggistica unificata.

### Lingue di fallback client per la messaggistica unificata

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Lingua</th>
<th>Paese</th>
<th>ID del gruppo linguistico</th>
<th>Prima lingua scelta, se installata</th>
<th>Seconda lingua scelta, se installata</th>
<th>Terza lingua scelta, se installata</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Catalano</p></td>
<td><p>Spagna</p></td>
<td><p>ca-ES</p></td>
<td><p>ca-ES</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Cinese (Hong Kong)</p></td>
<td><p>Cina</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="odd">
<td><p>Cinese (semplificato)</p></td>
<td><p>Cina</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-CN</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-TW</p></td>
</tr>
<tr class="even">
<td><p>Cinese (tradizionale)</p></td>
<td><p>Taiwan</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-TW</p></td>
<td><p>zh-HK</p></td>
<td><p>zh-CN</p></td>
</tr>
<tr class="odd">
<td><p>Danese</p></td>
<td><p>Danimarca</p></td>
<td><p>da-DK</p></td>
<td><p>da-DK</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Olandese</p></td>
<td><p>Paesi Bassi</p></td>
<td><p>nl-NL</p></td>
<td><p>nl-NL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inglese</p></td>
<td><p>Australia</p></td>
<td><p>en-AU</p></td>
<td><p>en-AU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Inglese</p></td>
<td><p>Canada</p></td>
<td><p>en-CA</p></td>
<td><p>en-CA</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inglese</p></td>
<td><p>India</p></td>
<td><p>en-IN</p></td>
<td><p>en-IN</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Inglese</p></td>
<td><p>Regno Unito</p></td>
<td><p>en-GB</p></td>
<td><p>en-GB</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Inglese</p></td>
<td><p>Stati Uniti</p></td>
<td><p>en-US</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Finlandese</p></td>
<td><p>Finlandia</p></td>
<td><p>fi-FL</p></td>
<td><p>fi-FL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Francese</p></td>
<td><p>Canada</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-CA</p></td>
<td><p>fr-FR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Francese</p></td>
<td><p>Francia</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-FR</p></td>
<td><p>fr-CA</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Tedesco</p></td>
<td><p>Germania</p></td>
<td><p>de-DE</p></td>
<td><p>de-DE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Italiano</p></td>
<td><p>Italia</p></td>
<td><p>it-IT</p></td>
<td><p>it-IT</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Giapponese</p></td>
<td><p>Giappone</p></td>
<td><p>ja-JP</p></td>
<td><p>ja-JP</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Coreano</p></td>
<td><p>Corea</p></td>
<td><p>ko-KR</p></td>
<td><p>ko-KR</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Norvegese (Bokmål)</p></td>
<td><p>Norvegia</p></td>
<td><p>nb-NO</p></td>
<td><p>nb-NO</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Polacco</p></td>
<td><p>Polonia</p></td>
<td><p>pl-PL</p></td>
<td><p>pl-PL</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Portoghese</p></td>
<td><p>Brasile</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-BR</p></td>
<td><p>pt-PT</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Portoghese</p></td>
<td><p>Portogallo</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-PT</p></td>
<td><p>pt-BR</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Russo</p></td>
<td><p>Russia</p></td>
<td><p>ru-RU</p></td>
<td><p>ru-RU</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Spagnolo</p></td>
<td><p>Spagna</p></td>
<td><p>es-ES</p></td>
<td><p>es-ES</p></td>
<td><p>es-MX</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="odd">
<td><p>Spagnolo</p></td>
<td><p>Messico</p></td>
<td><p>es-MX</p></td>
<td><p>es-MX</p></td>
<td><p>es-ES</p></td>
<td><p>en-US</p></td>
</tr>
<tr class="even">
<td><p>Svedese</p></td>
<td><p>Svezia</p></td>
<td><p>sv-SE</p></td>
<td><p>sv-SE</p></td>
<td><p>en-US</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


Inizio pagina

