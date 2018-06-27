---
title: 'Archiviazione sul posto di Exchange 2013: Exchange 2013 Help'
TOCTitle: Archiviazione sul posto di Exchange 2013
ms:assetid: b5e4c0e9-0558-4b90-bc12-f67adbfb59ac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd979800(v=EXCHG.150)
ms:contentKeyID: 50481480
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Archiviazione sul posto di Exchange 2013

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

L'*archivio locale* consente di controllare i dati di messaggistica dell'organizzazione eliminando la necessità di utilizzare file di archivio personale (PST) e permettendo agli utenti di archiviare i messaggi in una *cassetta postale di archiviazione* accessibile in MicrosoftOutlook 2010 e versioni successive e Microsoft OfficeOutlook Web App.

In Microsoft Exchange Server 2013, l'archivio locale offre agli utenti un percorso di archiviazione alternativo in cui salvare i dati cronologici della messaggistica. L'archivio sul posto è un'ulteriore cassetta postale (denominata 'cassetta postale di archiviazione') disponibile per l'utente della cassetta postale. Gli utenti di Outlook 2007 e versioni successive e di Outlook Web App possono accedere facilmente alle proprie cassette postali di archiviazione. Utilizzando una di queste applicazioni client, gli utenti possono visualizzare una cassetta postale di archiviazione e spostare o copiare i messaggi tra la cassetta postale principale e l'archivio. L'archivio locale offre agli utenti una visualizzazione coerente dei dati di messaggistica ed evita loro i problemi legati alla gestione dei file PST.

È possibile predisporre l'archivio personale di un utente nello stesso database di cassette postale in cui si trova la cassetta principale, in un altro database di cassette postali sullo stesso server Cassette postali o in un database di cassette postali su un altro server Cassette postali nello stesso sito Active Directory. Nelle distribuzioni ibride di Exchange 2010 e delle versioni successive, è possibile eseguire il provisioning anche degli archivi basati su cloud per le cassette postali che si trovano nei server Cassette postali locali.

**Sommario**

Messaging data and .pst files

Client access to archive mailboxes

Delegate access

Moving messages to the archive mailbox

Archive and retention policies

Default MRM policy

Archive quotas

In-Place Archives and other Exchange features

Managing archive mailboxes

## Dati di messaggistica e file PST

Outlook utilizza i file PST per archiviare localmente i dati sui computer o sulle condivisioni di rete degli utenti. A differenza dei file di archivio offline (OST) utilizzati da Outlook nella modalità cache di Exchange per archiviare una copia della cassetta postale per l'accesso offline, i file PST non vengono sincronizzati con la cassetta postale Exchange dell'utente. Se un utente sposta i messaggi in un file .pst, quei messaggi vengono rimossi dalla cassetta postale.

L'utilizzo dei file .pst per la gestione dei dati di messaggistica può portare ai seguenti problemi:

  - **File non gestiti**   In genere, i file.pst vengono creati dagli utenti e risiedono nei computer o nelle condivisioni di rete. Non vengono gestiti dall'organizzazione. Di conseguenza, gli utenti possono creare una serie di file .pst contenenti gli stessi o diversi messaggi e archiviarli in diversi percorsi, senza alcun controllo da parte dell'organizzazione.

  - **Maggiori costi di individuazione**   A volte le azioni legali o altri requisiti normativi o aziendali possono portare a richieste di individuazione. L'individuazione dei dati di messaggistica nei file .pst sui computer degli utenti può costituire uno lavoro manuale piuttosto costoso. Siccome la verifica dei file .pst non gestiti non è facile, in molti casi i dati .pst potrebbero non essere individuabili. Ciò potrebbe esporre l'organizzazione a rischi legali e finanziari.

  - **Impossibilità di applicare i criteri di conservazione di messaggistica**   I criteri di conservazione di messaggistica non possono essere applicati ai messaggi che si trovano nei file .pst. Di conseguenza, in base ai regolamenti aziendali o applicabili, l'organizzazione potrebbe non essere conforme.

  - **Rischio di furto dei dati**   I dati di messaggistica archiviati nei file .pst possono venire rubati. Ad esempio, i file .pst vengono spesso archiviati in dispositivi portatili quali computer portatili, dischi rigidi rimovibili e dispositivi multimediali portatili, come unità USB, CD e DVD.

  - **Visualizzazione frammentata dei dati di messaggistica**   Agli utenti che archiviano le informazioni nei file .pst non viene restituita una visualizzazione uniforme dei dati. In genere, i messaggi archiviati nei file .pst sono disponibili esclusivamente sul computer in cui si trova il file .pst. Di conseguenza, se gli utenti accedono alle loro cassette postali utilizzando Outlook Web App o Outlook su un altro computer, i messaggi archiviati nei loro file PST non sono accessibili.

## Accesso cliente alle cassette postali di archiviazione

Nella seguente tabella vengono elencate le applicazioni client che è possibile utilizzare per accedere alle cassette postali di archiviazione.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Accesso alla cassetta postale di archiviazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013, Outlook 2010, Outlook 2007 e Outlook Web App</p></td>
<td><p>Sì. Gli utenti di Outlook 2013, Outlook 2010, Outlook 2007 e Outlook Web App possono copiare o spostare gli elementi dalla cassetta postale principale a quella di archiviazione e anche utilizzare i criteri di conservazione per spostare gli elementi nell'archivio.</p>

> [!NOTE]
> Outlook 2010 e versioni successive e gli utenti di Outlook 2007 possono inoltre copiare o spostare gli elementi dai file pst alla cassetta postale di archivio. Gli utenti di Outlook 2007 richiedono l'aggiornamento cumulativo di Office 2007 di febbraio 2011. Esistono alcune differenze nel supporto di archiviazione tra Outlook 2010 o versione successiva e Outlook 2007. Per ulteriori informazioni, vedere l'articolo di Blog del Team di Exchange, vedere <A href="https://blogs.technet.com/b/exchange/archive/2010/12/20/3411710.aspx">Sì Virginia, esiste il supporto di archiviazione di Exchange 2010 in Outlook 2007</A>.


</td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Archiviazione sul posto è una funzionalità avanzata e richiede una licenza di accesso client (CAL) dell'organizzazione di Exchange. Per ulteriori informazioni sulla licenza di Exchange, vedere <A href="https://go.microsoft.com/fwlink/?linkid=237292">Gestione delle licenze di Exchange Server</A>. Per informazioni dettagliate sulle versioni di Outlook necessari per accedere a una cassetta postale di archiviazione, vedere <A href="https://go.microsoft.com/fwlink/?linkid=237276">requisiti relativi alle licenze per l'archivio personale e i criteri di conservazione</A>.



Outlook non crea una copia in locale della cassetta postale di archiviazione sul computer di un utente, anche se è configurato per l'uso della modalità cache. Gli utenti possono accedere alla cassetta postale di archiviazione solo in modalità online.

## Accesso delegato

L'*accesso delegato* si verifica quando a un utente o a un gruppo di utenti viene concesso di accedere alla cassetta postale di un altro utente. Esistono numerosi sistemi per fornire l'accesso delegato, tra cui:

  - Consentire a uno o più utenti di accedere alla cassetta postale di un utente che non lavora più nell'organizzazione. In questo caso, tra gli utenti a cui è concesso l'accesso delegato possono esserci il responsabile o il supervisore del reparto in cui operava l'utente o un altro utente che prenderà il suo posto.

  - Consentire a uno o più utenti di accedere a una cassetta postale condivisa.

  - Consentire agli assistenti di direzione di accedere alle cassette postali dei dirigenti con cui lavorano.

In Exchange 2013, quando si assegnano le autorizzazioni per l'accesso completo a una cassetta postale, il delegato a cui vengono assegnate le autorizzazioni può accedere anche all'archivio dell'utente. I delegati devono utilizzare Outlook per accedere alla cassetta postale ed essere connessi a un server Accesso client Exchange 2010 SP1 o versioni successive per le operazioni di individuazione automatica. L'individuazione automatica è un servizio di Exchange che fornisce le impostazioni per configurare automaticamente i client Outlook. Quando i delegati utilizzano Outlook per accedere a una cassetta postale Exchange 2013, sia la cassetta principale che l'archivio personale a cui possono accedere sono visibili in Outlook.

## Spostamento dei messaggi nella cassetta postale di archiviazione

Esistono diversi modi per spostare i messaggi nelle cassette postali di archiviazione:

  - **Spostamento o copia manuale dei messaggi**   Gli utenti delle cassette postali possono spostare o copiare manualmente i messaggi dalla cassetta principale o un file .pst nella cassetta di archiviazione. La cassetta postale di archiviazione viene visualizzata come un'altra cassetta o un file .pst in Outlook e Outlook Web App.

  - **Spostamento o copia dei messaggi tramite le regole di posta in arrivo**   Gli utenti delle cassette postali possono creare regole di posta in arrivo in Outlook o Outlook Web App per spostare automaticamente i messaggi in una cartella nella cassetta postale di archiviazione. Per ulteriori informazioni, vedere [Informazioni sulle regole della posta in arrivo](http://help.outlook.com/it-it/140/bb899620.aspx).

  - **Spostamento dei messaggi tramite i criteri di conservazione**   È possibile utilizzare i criteri di conservazione per spostare automaticamente i messaggi nell'archivio. Gli utenti possono anche applicare un tag personale per spostare i messaggi nell'archivio. Per i dettagli su criteri di conservazione e archiviazione, vedere Archive and retention policies più avanti in questo argomento.
    

    > [!NOTE]
    > I tag personali sono disponibili solo in Outlook Web App e Outlook 2010 e versioni successive.



  - **Importazione di messaggi da un file pst**   In Exchange 2013, è possibile utilizzare una richiesta di importazione della cassetta postale per importare i messaggi da un file pst all'archivio o alla cassetta postale principale dell'utente. Per informazioni dettagliate, vedere [Cassetta postale di importare ed esportare le richieste](mailbox-import-and-export-requests-exchange-2013-help.md). È anche possibile utilizzare lo strumento PST Capture per cercare file con estensione pst nel computer dell'organizzazione e importarne i dati negli archivi degli utenti.

## Criteri di conservazione e archiviazione

In Exchange 2013, è possibile applicare i criteri di archiviazione a una cassetta postale per spostare automaticamente i messaggi dalla cassetta postale principale di un utente alla cassetta postale di archiviazione dopo un determinato periodo di tempo. I criteri di archiviazione vengono implementati creando dei tag di conservazione che utilizzano l'azione di conservazione **Sposta nell'archivio**.

I messaggi vengono spostati in una cartella nella cassetta postale di archiviazione che ha lo stesso nome della cartella di origine nella cassetta postale principale. Se nella cassetta postale di archiviazione non è presente una cartella con lo stesso nome, viene creata quando l'Assistente cartelle gestite sposta un messaggio. Se nella cassetta postale di archiviazione si ricrea la stessa gerarchia di cartelle, gli utenti potranno trovare più facilmente i messaggi.

Per ulteriori informazioni su criteri, tag e azione di conservazione **Sposta nell'archivio**, vedere [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md).

## Criterio di gestione record di messaggistica predefinito

Il programma di installazione di Exchange 2013 crea un criterio di conservazione e archiviazione predefinito **criterio di gestione record di messaggistica predefinito**. Questo criterio contiene i tag di conservazione a cui è associata l'azione **Sposta nell'archivio**, come mostrato nella seguente tabella.


> [!NOTE]
> In Exchange&nbsp;2010 il criterio di conservazione e archiviazione predefinito creato dal programma di installazione di Exchange è denominato <STRONG>criterio di archiviazione e conservazione predefinito</STRONG>.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del tag di conservazione</th>
<th>Tipo di tag</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Sposta elementi predefiniti in archivio dopo 2 anni</strong></p></td>
<td><p>Predefinito (DPT)</p></td>
<td><p>I messaggi vengono automaticamente spostati nella cassetta postale di archiviazione dopo due anni. Viene applicato agli elementi dell'intera cassetta postale che non dispongono di un tag di conservazione applicato esplicitamente o ereditato dalla cartella.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sposta elementi personali in archivio dopo 1 anni</strong></p></td>
<td><p>Personale</p></td>
<td><p>I messaggi vengono automaticamente spostati nella cassetta postale di archiviazione dopo un anno.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sposta elementi personali in archivio dopo 5 anni</strong></p></td>
<td><p>Personale</p></td>
<td><p>I messaggi vengono automaticamente spostati nella cassetta postale di archiviazione dopo cinque anni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Nessuno spostamento nell'archivio personale</strong></p></td>
<td><p>Personale</p></td>
<td><p>I messaggi non vengono mai spostati nella cassetta postale di archiviazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sposta elementi recuperabili in archivio dopo 14 giorni</strong></p></td>
<td><p>Cartella degli elementi ripristinabili</p></td>
<td><p>I messaggi vengono spostati dalla cartella Elementi ripristinabili della cassetta postale principale dell'utente nella cartella Elementi ripristinabili della cassetta postale di archiviazione. Gli utenti che tentano di ripristinare gli elementi eliminati nell'archivio devono utilizzare la funzionalità Recupera elementi eliminati sulla cassetta postale di archiviazione.</p></td>
</tr>
</tbody>
</table>


Se si abilita un archivio locale per un utente della cassetta postale e a questa non è stato ancora assegnato un criterio di conservazione, le viene automaticamente assegnato il criterio di conservazione e archiviazione predefinito. Dopo che l'Assistenti cassette postali ha elaborato la cassetta postale, questi tag diventano disponibili e l'utente può quindi contrassegnare le cartelle o i messaggi da spostare nella cassetta postale di archiviazione. Per impostazione predefinita, i messaggi di posta elettronica dall'intera cassetta postale vengono spostati dopo due anni.

Prima di fornire le cassette postali di archiviazione agli utenti, è opportuno illustrare loro i criteri di archiviazione che verranno applicati alle cassette postali e fornire loro le istruzioni o la documentazione necessaria per soddisfare le loro esigenze. Le informazioni fornite dovrebbe includere dettagli sui seguenti elementi:

  - Funzionalità disponibile nell'archivio, criteri di conservazione e archiviazione predefiniti.

  - Informazioni sulla tempistica dello spostamento automatico dei messaggi nell'archivio.

  - Informazioni sulla gerarchia di cartelle creata nella cassetta postale di archiviazione.

  - Modalità di applicazione dei tag personali (visualizzati nel menu Criteri di archiviazione in Outlook e Outlook Web App).


> [!NOTE]
> Quando si applica un criterio di conservazione agli utenti che dispongono di una cassetta postale di archiviazione, il criterio di conservazione sostituisce il criterio di gestione record di messaggistica predefinito. È possibile creare uno o più tag di conservazione con l'azione <STRONG>Sposta nell'archivio</STRONG> e collegare i tag al criterio di conservazione. È inoltre possibile aggiungere i tag predefiniti <STRONG>Sposta nell'archivio</STRONG> (creati dal programma di installazione e collegati al criterio di gestione record di messaggistica predefinito) a tutti i criteri di conservazione creati.



Per informazioni su conformità e archiviazione in Outlook 2010 e versioni successive, vedere [pianificare la conformità e archiviazione in Outlook 2010](https://go.microsoft.com/fwlink/?linkid=210902).

## Quote di archiviazione

Le cassette postali di archiviazione consentono agli utenti di archiviare i dati cronologici di messaggistica esternamente alla cassetta postale principale. Spesso gli utenti utilizzano i file .pst a causa delle basse quote di archiviazione della cassetta postale e delle restrizioni imposte quando queste quote vengono superate. Ad esempio, è possibile impedire agli utenti di inviare messaggi quando le dimensioni della cassetta postale superano la quota *Impedisci l'invio*. Analogamente, è possibile impedire agli utenti di inviare e ricevere messaggi quando le dimensioni della cassetta postale superano la quota *Impedisci l'invio e la ricezione*.

Per eliminare la necessità di utilizzare i file .pst, è possibile fornire a una cassetta postale di archiviazione i limiti di archiviazione che soddisfano le esigenze dell'utente. È comunque possibile mantenere un certo controllo sulle quote di archiviazione e le dimensioni delle cassette postali di archiviazione per consentire il monitoraggio dei costi e dell'espansione.

Per consentire questo controllo, è possibile configurare una *quota di avviso per l'archiviazione* e una *quota di archiviazione* per le cassette postali di archiviazione. Quando una cassetta postale di archiviazione supera la quota di avviso specificata per l'archiviazione, nel registro eventi Applicazione viene registrato un evento. Quando una cassetta postale di archiviazione supera la quota di archiviazione specificata, i messaggi non vengono più spostati nell'archivio, nel registro eventi Applicazione viene registrato un evento di avviso e all'utente della cassetta postale viene inviato un messaggio di quota. Per impostazione predefinita in Exchange 2013 la quota di avviso per l'archiviazione è impostata su 45 GB e la quota di archiviazione è impostata su 50 GB.

Nella tabella seguente vengono elencati gli eventi registrati e i messaggi di avviso inviati quando vengono raggiunte le quota di avviso per l'archiviazione e la quota di archiviazione.


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
<th>Quota</th>
<th>ID evento</th>
<th>Tipo</th>
<th>Origine</th>
<th>Category</th>
<th>Messaggio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Quota di avviso per l'archiviazione</p></td>
<td><p>10022</p></td>
<td><p>Avviso</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>Assistente cartelle gestite</p></td>
<td><p>La cassetta postale di archivio '&lt;nome visualizzato&gt;:&lt;GUID&gt;:&lt;database di cassette postali&gt;:&lt;nome di dominio completo server&gt;' ha superato la quota di avviso per l'archiviazione '&lt;quota di avviso per l'archiviazione&gt;'. La dimensione della cassetta postale di archivio è di '&lt;dimensione&gt;' byte.</p></td>
</tr>
<tr class="even">
<td><p>Quota di archiviazione</p></td>
<td><p>8537</p></td>
<td><p>Avviso</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>Generale</p></td>
<td><p>La cassetta postale di archivio per &lt;DN legacy&gt; ha superato la dimensione massima consentita. Non è possibile copiare o spostare gli elementi nella cassetta postale di archivio. Tutte le azioni relative alla conservazione dei messaggi che spostano gli elementi nella cassetta postale di archivio non riusciranno e la cassetta postale principale potrebbe contenere elementi con tag di conservazione scaduti fino a quando la cassetta postale di archivio rientra nel limite di dimensione massima. Notificare al proprietario la condizione della cassetta postale di archivio.</p></td>
</tr>
</tbody>
</table>


## Archivi locali e altre funzionalità di Exchange

In questa sezione viene illustrata l'interazione funzionale tra gli archivi locali e le diverse funzionalità di Exchange:

  - **Ricerca Exchange   **La possibilità di eseguire velocemente delle ricerche nei messaggi è ancora più importante nelle cassette postali di archiviazione. Per Exchange Search, non ci sono differenze tra la cassetta postale principale e quella di archiviazione. Il contenuto di entrambe viene indicizzato. Dal momento che la cassetta postale di archiviazione non è salvata nella cache sul computer dell'utente (anche quando lavora nella modalità cache di Exchange in Outlook), i risultati della ricerca per l'archivio vengono sempre forniti da Exchange Search. Quando la ricerca viene eseguita nell'intera cassetta postale in Outlook 2010 e versioni successive e Outlook Web App, i risultati della ricerca includono la cassetta postale principale e di archiviazione dell'utente.

  - **eDiscovery locale**   Quando un responsabile dell'individuazione esegue una ricerca eDiscovery locale, la ricerca viene eseguita anche nelle cassette postali di archiviazione degli utenti. Non sono disponibili opzioni per escludere le cassette postali di archiviazione quando si crea una ricerca di individuazione da Interfaccia di amministrazione di Exchange. Quando si utilizza Exchange Management Shell per creare una ricerca di individuazione, è possibile escludere l'archivio utilizzando l'opzione *DoNotIncludeArchive*. Per ulteriori informazioni, vedere [New-MailboxSearch](https://technet.microsoft.com/it-it/library/dd298064\(v=exchg.150\)). Per ulteriori informazioni, vedere [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Non è possibile utilizzare la funzionalità eDiscovery locale per eseguire una ricerca in una cassetta postale disconnessa.



  - **Archiviazione sul posto e conservazione per controversia legale**   Quando si imposta una cassetta postale sull'archiviazione sul posto o sulla conservazione per controversia legale, l'archiviazione e la conservazione interessano sia la cassetta postale principale che quella di archiviazione. Per ulteriori informazioni sull'archiviazione sul posto e sulla conservazione per controversia legale, vedere [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md).

  - **Cartella Elementi ripristinabili   **La cassetta postale di archiviazione contiene una sua cartella Elementi ripristinabili che è soggetta alle stesse quote specificate per la cartella Elementi ripristinabili della cassetta postale principale. Per ulteriori informazioni sugli elementi ripristinabili, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md).

  - **Archiviazione contenuto Lync in Exchange**   È possibile archiviare le conversazioni di messaggistica istantanea e i documenti delle riunioni online condivise nella cassetta postale primaria dell'utente. La cassetta postale deve trovarsi in un server Cassette postali Exchange 2013 ed è necessario che nell'organizzazione sia distribuito Microsoft Lync 2013. Per ulteriori informazioni, vedere [Integrazione con SharePoint e Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

## Gestione delle cassette postali di archiviazione

In Exchange 2013, la creazione e la gestione delle cassette postali di archiviazione vengono integrate da attività comuni di gestione delle cassette postali, incluse:

  - **Creazione di una cassetta postale di archiviazione**   È possibile creare una cassetta postale di archiviazione quando si crea una cassetta postale così come abilitare una cassetta di archiviazione per una cassetta postale esistente. Per ulteriori informazioni, vedere [Gestione degli archivi In Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

  - **Spostamento di una cassetta postale di archiviazione**   È possibile spostare la cassetta postale di archiviazione di un utente in un altro database di cassette postali sullo stesso server Cassette postali o su un altro server, indipendentemente dalla cassetta postale principale. Per spostare la cassetta postale di archiviazione di un utente, è necessario innanzitutto creare una richiesta di spostamento. Per ulteriori informazioni, vedere [Gestire spostamenti locali](manage-on-premises-moves-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > L'individuazione dell'archivio e della cassetta postale di un utente su versioni diverse di Exchange Server non è supportata.



  - **Disabilitazione di una cassetta postale di archiviazione**   Può essere necessario disabilitare la cassetta postale di archiviazione di un utente per risolvere eventuali problemi o se si sta spostando la cassetta postale principale su una versione di Exchange che non supporta l'archiviazione locale. La disabilitazione di un archivio è simile alla disabilitazione della cassetta postale principale. Per ulteriori informazioni, vedere [Gestione degli archivi In Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md). Nelle distribuzioni locali una cassetta postale di archiviazione disabilitata viene conservata nel database di cassette postali fino al termine del periodo di conservazione delle cassette eliminate specificato per il database. Durante questo periodo di tempo, è possibile ricollegare l'archivio a un utente della cassetta postale. Quando viene raggiunto il termine del periodo di conservazione delle cassette postali eliminate, la cassetta postale scollegata viene eliminata dal database di cassette postali.

  - **Recupero delle statistiche per cassette postali e cartelle**   È possibile recuperare le statistiche per la cassetta postale di archiviazione di un utente utilizzando l'opzione *Archive* con i cmdlet [Get-MailboxStatistics](https://technet.microsoft.com/it-it/library/bb124612\(v=exchg.150\)) e [Get-MailboxFolderStatistics](https://technet.microsoft.com/it-it/library/aa996762\(v=exchg.150\)).

  - **Test della connettività dell'archivio**   In Exchange 2013 è possibile utilizzare il cmdlet [Test-ArchiveConnectivity](https://technet.microsoft.com/it-it/library/hh529914\(v=exchg.150\)) per verificare la connettività in un archivio locale o basata su cloud di un utente specifico.

