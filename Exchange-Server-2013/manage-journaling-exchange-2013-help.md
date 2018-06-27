---
title: "Gestire l'inserimento nel journal: Exchange 2013 Help"
TOCTitle: Gestire l'inserimento nel journal
ms:assetid: d517f27e-f80a-4a06-988c-cbbf981c701d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ651670(v=EXCHG.150)
ms:contentKeyID: 50481761
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire l'inserimento nel journal

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Inserimento nel journal consentono alle organizzazioni di rispondere ai requisiti legali, normativi e organizzativi conformità mediante la registrazione di comunicazioni di posta elettronica in ingresso e in uscita. In questo argomento viene illustrato come eseguire attività di base relative alla gestione di inserimento nel journal in Exchange 2013 e Exchange Online.

L'inserimento standard nel journal è configurato su un database delle cassette postali. Consente all'agente di journaling di inserire nel journal tutti i messaggi inviati da e a cassette postali che si trovano in uno specifico database. È possibile anche utilizzare l'inserimento avanzato nel journal che consente all'agente di journaling di eseguire un'operazione più granulare utilizzando le regole di journal. Invece di inserire nel journal tutte le cassette postali presenti su un database, è possibile configurare delle regole del journal in base alle esigenze della propria organizzazione, così da inserire, ad esempio, singoli destinatari o membri dei gruppi di distribuzione. Per utilizzare l'inserimento avanzato, è necessario disporre della licenza CAL (Client Access License) di Exchange Enterprise.

Per ulteriori informazioni sull'inserimento dei dati nel journal, vedere [Inserimento nel journal](journaling-exchange-2013-help.md).

**Sommario**

Creare una regola del journal

Consente di visualizzare o modificare una regola del journal

Attivare o disattivare una regola del journal

Rimuovere una regola del journal

Abilitare o disabilitare l'inserimento nel journal di database per cassetta postale

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Inserimento nel journal" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - È stata creata una cassetta del journaling oppure una cassetta postale esistente è disponibile per l'uso come cassetta del journaling. Non è possibile designare una cassetta postale di Exchange Online come una cassetta del journaling. È possibile offrire rapporti del journal un locale archiviazione sistema o un servizio di archiviazione di terze parti. Se si esegue una distribuzione ibrida con le cassette postali suddivisi tra i server locali e Exchange Online, è possibile designare una cassetta postale locale come cassetta del journaling per le cassette postali Exchange Online e in locale.
    

    > [!IMPORTANT]
    > Se una regola di inserimento nel journal è configurato in Exchange Online di inviare che segnalazioni di giornale di registrazione a una cassetta del journaling che non esiste o non è una destinazione valida, il rapporto del journal rimane nella coda di trasporto nel server di datacenter Microsoft. In questo caso, il personale di datacenter Microsoft tenterà di contattare l'organizzazione e richiedere di risolvere il problema, in modo che i rapporti del journal possono correttamente recapitati alla cassetta postale di inserimento nel journal. Se il problema è non risolto dopo due giorni di contattato, Microsoft disabiliterà la regola di Journal problematico.



  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>. Se si riscontrano problemi con la cassetta postale <STRONG>JournalingReportDNRTo</STRONG>, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=331674">regole delle cassette postali in Exchange Online e trasporto non funziona come previsto</A>.



## Creare una regola del journal

## Creazione di una regola di journal tramite l'interfaccia di amministrazione di Exchange

1.  In EAC, andare a **Gestione conformità** \> **regole del Journal** e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  In **Regola di journal** specificare un nome per la regola del journal e completare i seguenti campi:
    
      - **Se il messaggio è inviato a o ricevuto da**   Specificare il destinario a cui è indirizzata la regola. È possibile anche selezionare un destinatario specifico o applicare la regola a tutti i messaggi.
    
      - **Inserisci i seguenti messaggi nel journal** Specificare l'ambito della regola di journal. È possibile inserire nel journal solo i messaggi interni, solo i messaggi esterni o tutti i messaggi, indipendentemente dall'origine o dalla destinazione.
    
      - **Invia rapporti del journal a**   Digitare l'indirizzo della cassetta del journaling che riceverà tutti i rapporti del journal.
        

        > [!NOTE]
        > È inoltre possibile digitare il nome visualizzato o l'alias di un utente di posta elettronica o un contatto di posta elettronica della cassetta postale del journal. In questo caso, verranno inviati rapporti del journal nell'indirizzo di posta elettronica esterno del contatto utente o di posta elettronica di posta elettronica. Ma, come indicato in precedenza, l'indirizzo di posta elettronica esterno di un contatto di posta elettronica utente o di posta elettronica non può essere l'indirizzo di una cassetta postale Exchange Online.



3.  Scegliere **Salva** per creare la regola di journal.

## Creazione di una regola del journal tramite Shell

In questo esempio viene creata la regola di journal "Discovery Journal Recipients" per inserire nel journal tutti i messaggi inviati e ricevuti dal destinatario user1@contoso.com.

    New-JournalRule -Name "Discovery Journal Recipients" -Recipient user1@contoso.com -JournalEmailAddress "Journal Mailbox" -Scope Global -Enabled $True

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la regola di journal sia stata creata correttamente, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, verificare che la nuova regola di journal creata sia elencata nella scheda **Regole del journal**.

  - Nella shell, verificare la presenza della nuova regola di journal eseguendo il comando riportato di seguito (nell'esempio seguente viene verificata la regola creata nell'esempio della shell precedente):
    
        Get-JournalRule "Discovery Journal Recipients"

Torna all'inizio

## Visualizzazione o modifica di una regola di journal

## Visualizzazione o modifica di una regola di journal tramite l'interfaccia di amministrazione di Exchange

1.  In EAC, andare a **Gestione conformità** \> **regole del Journal**.

2.  Nella visualizzazione elenco saranno visualizzate tutte le regole del journal dell'organizzazione.

3.  Fare doppio clic sulla regola che si intende visualizzare o modificare.

4.  In **Regola di journal** modificare le impostazioni desiderate. Per ulteriori informazioni sulle impostazioni in questa finestra di dialogo, vedere la procedura Use the EAC to create a journal rule descritta in precedenza in questo argomento.

## Visualizzazione o modifica di una regola di journal tramite Shell

In questo esempio viene visualizzato un elenco di riepilogo di tutte le regole del journal nell'organizzazione di Exchange:

    Get-JournalRule

In questo esempio viene recuperata la regola del journal "Brokerage Journal Rule" e viene eseguito il pipelining dell'output al comando **Format-List** per visualizzare le proprietà della regola con un formato elenco.

    Get-JournalRule "Brokerage Journal Rule" | Format-List

Se si desidera modificare le proprietà di una regola specifica, è necessario utilizzare il cmdlet [Set-JournalRule](https://technet.microsoft.com/it-it/library/bb125010\(v=exchg.150\)). In questo esempio viene modificato il nome della regola del journal `JR-Sales` in `TraderVault`. Vengono inoltre modificate le seguenti impostazioni della regola:

  - Ambito scrittura destinatario

  - JournalEmailAddress

  - Ambito

<!-- end list -->

    Set-JournalRule JR-Sales -Name TraderVault -Recipient traders@woodgrovebank.com -JournalEmailAddress tradervault@woodgrovebank.com -Scope Internal

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la regola di journal sia stata modificata correttamente, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Gestione conformità** \> **Regole del journal**. Fare doppio clic sulla regola modificata e verificare che le modifiche siano state salvate.

  - Nella shell, verificare che la regola di journal sia stata modificata correttamente eseguendo il comando riportato di seguito. Questo comando consentirà di elencare le proprietà modificate e il nome della regola (nell'esempio seguente viene verificata la regola modificata nell'esempio della shell precedente):
    
        Get-TransportRule "TraderVault" | Format-List Name,Recipient,JournalEmailAddress,Scope

Torna all'inizio

## Abilitazione o disabilitazione di una regola di journal


> [!IMPORTANT]
> Quando si disablita una regola di journal, l'agente di journaling bloccherà i messaggi di inserimento nel journal assegnati dalla regola. Quando una regola di journal è disabilitata, non vengono inseriti nel journal i messaggi che sarebbero stati normalmente inseriti nel journal dalla regola. Assicurarsi di non compromettere i requisiti normativi o di conformità dell'organizzazione disabilitando una regola di journal.



## Abilitazione o disabilitazione di una regola di journal tramite l'interfaccia di amministrazione di Exchange

1.  In EAC, andare a **Gestione conformità** \> **regole del Journal**.

2.  Nella visualizzazione elenco, nella colonna **On** accanto al nome della regola selezionare la casella di controllo per abilitare la regola o deselezionarla per disabilitarla.

## Abilitazione o disabilitazione di una regola del journal tramite Shell

In questo esempio viene abilitata la regola Contoso.

    Enable-JournalRule "Contoso Journal Rule"

In questo esempio viene disabilitata la regola Contoso.

    Disable-JournalRule "Contoso Journal Rule"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la regola di journal sia stata abilitata o disabilitata correttamente, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, visualizzare l'elenco delle regole del journal e controllare lo stato della casella di controllo nella colonna **On**.

  - Nella shell, eseguire il comando riportato di seguito per ottenere un elenco di tutte le regole del journal dell'organizzazione, incluso lo stato attinente:
    
        Get-JournalRule | Format-Table Name,Enabled

Torna all'inizio

## Rimozione di una regola di journal

## Rimozione di una regola di journal tramite l'interfaccia di amministrazione di Exchange

1.  In EAC, andare a **Gestione conformità** \> **regole del Journal**.

2.  Nella visualizzazione elenco, selezionare la regola che si intende rimuovere e fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

## Rimozione di una regola di journal tramite Shell

In questo esempio viene rimossa la regola "Brokerage Journal Rule".

    Remove-JournalRule "Brokerage Journal Rule"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la regola di journal sia stata rimossa correttamente, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, verificare che la regola di journal rimossa non sia più presente nell'elenco della scheda **Regole del journal**.

  - Nella shell, eseguire il comando riportato di seguito per verificare che la regola rimossa non sia più inclusa nell'elenco:
    
        Get-JournalRule

Torna all'inizio

## Abilitazione o disabilitazione dell'inserimento nel journal di database per cassetta postale


> [!WARNING]
> La disabilitazione dell'inserimento nel journal dei messaggi in un database delle cassette postali potrebbe avere come conseguenza la non conformità dell'organizzazione con i criteri di conservazione di messaggistica applicabili. Quando si disabilita l'inserimento nel journal dei messaggi in un database delle cassette postali, non verranno più inviate le conferme di recapito del journal per i messaggi inviati o ricevuti dalle cassette postali nel database delle cassette postali corrispondente.



## Abilitazione o disabilitazione dell'inserimento nel journal di database per cassetta postale tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Nella visualizzazione elenco, fare doppio clic sul database delle cassette postali per cui abilitare l'inserimento nel journal.

3.  Fare clic su **Manutenzione**, quindi su **Sfoglia** accanto alla casella **Destinatario journal** per selezionare la cassetta del journaling. L'indicazione di un destinatario del journal abilita l'inserimento nel journal per il database.
    
    Per disabilitare l'inserimento nel journal, rimuovere il destinatario del journal scegliendo **Rimuovi X**.

## Abilitazione o disabilitazione dell'inserimento nel journal di database per cassetta postale tramite Shell

In questo esempio viene abilitato l'inserimento nel journal per il database delle cassette postali "Sales Database" e viene impostata la cassetta del journaling "Sales Database" come destinatario del journal.

    Set-MailboxDatabase "Sales Database" -JournalRecipient "Sales Database Journal Mailbox"

In questo esempio viene disabilitato l'inserimento nel journal di database per cassetta postale nel database delle cassette postali "Sales Database".

    Set-MailboxDatabase "Sales Database" -JournalRecipient $Null

In questo esempio viene disabilitato l'inserimento nel journal di database per cassetta postale su tutti i database delle cassette postali nell'organizzazione di Exchange. Il cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb124924\(v=exchg.150\)) consente di recuperare tutti i database delle cassette postali nell'organizzazione di Exchange e i risultati del cmdlet vengono reindirizzati al cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\)).

    Get-MailboxDatabase | Set-MailboxDatabase -JournalRecipient $Null

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'inserimento nel journal di database per cassetta postale sia stato abilitato o disabilitato correttamente, effettuare una delle seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Database**.

2.  Fare doppio clic sul database da verificare, quindi selezionare la scheda **Manutenzione**.

3.  Se il destinatario del journal appropriato è elencato nella casella **Destinatario journal**, l'inserimento nel journal per il database delle cassette postali è stato abilitato correttamente. Se il destinatario del journal non è presente nel'elenco, l'inserimento nel journal è disabilitato per il database.

<!-- end list -->

  - Nella shell, eseguire il comando riportato di seguito per ottenere un elenco di tutti i database delle cassette postali dell'organizzazione, inclusi i destinatari del journal associati. L'inserimento nel journal risulta abilitato per i database con un destinatario del journal inserito nell'elenco, in caso contrario sarà disabilitato.
    
        Get-MailboxDatabase | Format-Table Name,JournalRecipient

Torna all'inizio

## Ulteriori informazioni

[Inserimento nel journal](journaling-exchange-2013-help.md)

[Disabilitare o abilitare l'inserimento nel journal dei messaggi vocali e delle notifiche di chiamata](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md)

[New-JournalRule](https://technet.microsoft.com/it-it/library/bb125242\(v=exchg.150\))

[Get-JournalRule](https://technet.microsoft.com/it-it/library/aa998866\(v=exchg.150\))

[Set-JournalRule](https://technet.microsoft.com/it-it/library/bb125010\(v=exchg.150\))

[Enable-JournalRule](https://technet.microsoft.com/it-it/library/bb123902\(v=exchg.150\))

[Disable-JournalRule](https://technet.microsoft.com/it-it/library/aa995925\(v=exchg.150\))

[Remove-JournalRule](https://technet.microsoft.com/it-it/library/bb123489\(v=exchg.150\))

[Set-MailboxDatabase](https://technet.microsoft.com/it-it/library/bb123971\(v=exchg.150\))

