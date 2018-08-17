---
title: 'Creazione e gestione delle cassette sala: Exchange 2013 Help'
TOCTitle: Creazione e gestione delle cassette sala
ms:assetid: f70752ad-fce0-4e14-8428-fc5ac63f6c54
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215781(v=EXCHG.150)
ms:contentKeyID: 50479881
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creazione e gestione delle cassette sala

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-02-02_

Tempo stimato per il completamento: 5 minuti.

Una cassetta postale della sala è una cassetta postale delle risorse assegnata a un'ubicazione fisica, ad esempio una sala riunioni, un auditorium o un'aula per la formazione. In seguito alla creazione di cassette postali della sala da parte di un amministratore, gli utenti possono prenotare facilmente spazi includendo le cassette postali sala nelle convocazioni di riunione. Per altri dettagli, vedere [Destinatari](recipients-exchange-2013-help.md).

Per informazioni su un altro tipo di cassette postali delle risorse, vedere [Gestire le cassette postali attrezzatura](manage-equipment-mailboxes-exchange-2013-help.md).

## Operazione desiderata?

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).


> [!IMPORTANT]
> Se si esegue Exchange 2013 in uno scenario ibrido, assicurarsi di creare le cassette postali di sale nel percorso appropriato. Creare le cassette postali di sala per l'organizzazione locale, mentre le cassette postali di sala per Exchange Online devono essere create nel cloud.




## Creazione di una cassetta postale sala

## Usare l'interfaccia di amministrazione di Exchange per creare una cassetta postale della sala

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Risorse**.

2.  Per creare una cassetta postale della sala, fare clic su **Nuova**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") \> **Cassetta postale della sala**.

3.  Utilizzare le opzioni disponibili nella pagina per specificare le impostazioni per la nuova cassetta postale delle risorse.
    
      - **\* Nome della sala**   Utilizzare questa casella per digitare un nome per la cassetta postale sala. Si tratta del nome presente nell'elenco delle cassette postali per le risorse nell'interfaccia di amministrazione di Exchange e nella rubrica dell'organizzazione. Questo nome è obbligatorio e non può superare i 64 caratteri.
        

        > [!TIP]
        > Benché vi siano altri campi che descrivono i dettagli della sala, ad esempio Posizione e Capacità, è utile riepilogare i dettagli più importanti nel nome della cassetta postale sala utilizzando una convenzione di denominazione coerente. Ciò è necessario in quanto gli utenti possono vedere facilmente i dettagli quando selezionano la sala dalla rubrica nella convocazione della riunione.

    
      - **\* Indirizzo di posta elettronica**   La cassetta postale sala dispone di un indirizzo di posta elettronica che consente di ricevere le richieste di prenotazione. L'indirizzo di posta elettronica è costituito da un alias alla sinistra del simbolo @, che deve essere univoco nella foresta, e da un nome di dominio a destra. L'indirizzo di posta elettronica è obbligatorio.
    
      - **Posizione**, **Telefono**, **Capacità**   È possibile utilizzare questi campi per immettere dettagli relativi allo spazio. Tuttavia, come illustrato in precedenza, è possibile includere tutte queste informazioni o solo alcune di esse nel nome della sala affinché siano visibili agli utenti.

4.  Al termine, scegliere **Salva** per creare la cassetta postale sala.

Dopo aver creato la cassetta postale della sala, è possibile modificare la cassetta postale della sala per aggiornare le informazioni sulle opzioni di prenotazione, Suggerimenti messaggio e sulla delega per la cassetta postale. Consultare la sezione Utilizzo dell'interfaccia di amministrazione di Exchange di seguito per modificare le proprietà della cassetta postale della sala

## Creazione di una cassetta postale della sala tramite Exchange PowerShell

Con questo esempio viene creata una cassetta postale sala con la seguente configurazione:

  - La cassetta postale sala si trova nel database delle cassette postali 1.

  - Il nome della cassetta postale è ConfRoom1. Questo nome verrà anche utilizzato per creare l'indirizzo di posta elettronica della sala.

  - Il nome visualizzato nell'interfaccia di amministrazione di Exchange e nella rubrica sarà Sala riunioni 1.

  - L'opzione *Room* specifica che questa cassetta postale sarà creata come cassetta postale sala.

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name ConfRoom1 - -DisplayName "Conference Room 1" -Room

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-Mailbox](https://technet.microsoft.com/it-it/library/aa997663\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

È possibile verificare se la cassetta postale della sala è stata creata correttamente in un paio di modi diversi:

  - Nell'interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Risorse**. La nuova cassetta postale della sala viene visualizzata nell'elenco delle cassette postali. In **Tipo di cassetta postale**, il tipo è **Sala**.

  - In Exchange PowerShell, eseguire il comando riportato di seguito per visualizzare le informazioni sulla nuova cassetta postale della sala.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Creazione di elenco di sala

Se si intende disporre di oltre cento sale o se sono state già create più di cento sale, utilizzare un elenco di sala per organizzarle. Se l'azienda dispone di diversi edifici con sale che possono essere prenotate per le riunioni, potrebbe essere utile creare elenchi di sale per ciascun edificio. Gli elenchi di sale rappresentano gruppi di distribuzione contrassegnati in modo specifico che possono essere gestiti in modo analogo ai gruppi di distribuzione. Tuttavia, è possibile creare elenchi di sale solo con Exchange Management Shell.

## Creazione di un elenco di sale tramite Exchange PowerShell

In questo esempio viene creato un elenco di sala per l'edificio 32.

    New-DistributionGroup -Name "Building 32 Conference Rooms" -OrganizationalUnit "contoso.com/rooms" -RoomList

## Aggiunta di una sala a un elenco di sale tramite Exchange PowerShell

In questo esempio la sala confroom3223 viene aggiunta all'elenco di sala relativo all'edificio 32.

    Add-DistributionGroupMember -Identity "Building 32 Conference Rooms" -Member confroom3223@contoso.com

## Conversione di un gruppo di distribuzione in un elenco di sale tramite Exchange PowerShell

È possibile che l'utente abbia già creato gruppi di distribuzione che comprendono la sala riunioni. Non è necessario crearli di nuovo. Verranno convertiti in modo rapido in elenchi di sala.

In questo esempio il gruppo di distribuzione, sale riunioni dell'edificio 34, viene convertito in un elenco di sala.

    Set-DistributionGroup -Identity "Building 34 Conference Rooms" -RoomList

## Modifica delle proprietà della cassetta postale sala

Una volta creata la cassetta postale della sala, è possibile modificarla e impostare proprietà aggiuntive utilizzando l'interfaccia di amministrazione di Exchange o Exchange PowerShell.

## Usare l'interfaccia di amministrazione di Exchange per modificare le proprietà della cassetta postale della sala

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Risorse**.

2.  Nell'elenco delle cassette postali per le risorse, fare clic sulla cassetta postale sala di cui modificare le proprietà e scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà della cassetta postale sala, fare clic su una delle seguenti sezioni per visualizzare o modificare le proprietà.
    
      - Generale
    
      - Delegati
    
      - Opzioni di prenotazione
    
      - Informazioni di contatto
    
      - Indirizzo di posta elettronica
    
      - MailTip

## Generale

Utilizzare la sezione **Generale** per visualizzare o modificare le informazioni di base sulla risorsa.

  - **\* Nome sala**   Si tratta del nome presente nell'elenco delle cassette postali per le risorse nell'interfaccia di amministrazione di Exchange e nella rubrica dell'organizzazione. L'alias modificato non può superare i 64 caratteri.

  - **\* Indirizzo di posta elettronica**   Casella di sola lettura in cui viene visualizzato l'indirizzo di posta elettronica della cassetta postale sala. È possibile modificarlo nella sezione Indirizzo di posta elettronica.

  - **Capacità**   Questa casella consente l'inserimento del numero massimo di persone autorizzate a occupare la sala in sicurezza.

Fare clic su **Altre opzioni** per visualizzare o modificare le seguenti proprietà aggiuntive:

  - **Unità organizzativa**   In questa casella di sola lettura è visualizzata l'unità organizzativa contenente l'account per la cassetta postale sala. Per spostare l'account verso un'unità organizzativa (OU) diversa, è necessario utilizzare Utenti e computer di Active Directory.

  - **Database delle cassette postali**   In questa casella di sola lettura è visualizzato il nome del database che ospita la cassetta postale sala. Utilizzare la pagina **Migrazione** nell'interfaccia di amministrazione di Exchange per spostare la cassetta postale in un database diverso.

  - **Alias** Questa casella consente di modificare l'alias della cassetta postale sala.

  - **Non visualizzare negli elenchi di indirizzi di Exchange** Selezionare questa casella di controllo per non consentire la visualizzazione della cassetta postale sala nella rubrica e in altri elenchi di indirizzi definiti nell'organizzazione Exchange. Una volta selezionata questa casella di controllo, gli utenti possono comunque inviare messaggi di prenotazione alla cassetta postale sala utilizzando l'indirizzo di posta elettronica.

  - **Reparto**   Questa casella consente di specificare il nome del reparto a cui la sala è associata. È possibile utilizzare questa proprietà per creare condizioni del destinatario per i gruppi di distribuzione dinamici e gli elenchi di indirizzi.

  - **Società**   Questa casella consente di specificare un nome di società a cui la sala è associata, se disponibile. Analogamente alla proprietà Reparto, è possibile utilizzare questa proprietà per creare condizioni del destinatario per i gruppi di distribuzione dinamici e gli elenchi di indirizzi.

  - **Criteri rubrica**   Utilizzare questa opzione per specificare un criterio per la rubrica (ABP) per la cassetta postale della sala. I criteri rubrica contengono un elenco di indirizzi globale, una rubrica offline , un elenco di sale e un set di elenchi di indirizzi. Per ulteriori informazioni, vedere [Criteri delle rubriche](address-book-policies-exchange-2013-help.md).
    
    Nell'elenco a discesa, selezionare il criterio da associare a questa cassetta postale.

  - **Attributi personalizzati**   In questa sezione vengono visualizzati gli attributi personalizzati definiti per la cassetta postale sala. Per specificare valori personalizzati per gli attributi, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). È possibile specificare fino a 15 attributi personalizzati per un destinatario.

## Delegati

Utilizzare questa sezione per visualizzare o modificare le modalità di gestione delle richieste di prenotazione della cassetta postale sala e per definire gli utenti che possono accettare o rifiutare le richieste di prenotazione se l'operazione non è automatica.

  - **Richieste di prenotazione**   Selezionare una delle seguenti opzioni per la gestione delle richieste di prenotazione.
    
      - **Accetta o rifiuta automaticamente le richieste di prenotazione**   Una convocazione di riunione valida prenota automaticamente la sala. Se è presente un conflitto di pianificazione con una prenotazione esistente o se la richiesta di prenotazione viola i limiti di pianificazione della risorsa, ad esempio la durata della prenotazione è troppo lunga, la convocazione della riunione viene automaticamente negata.
    
      - **Seleziona delegati per accettazione o rifiuto delle richieste di prenotazione**   I delegati delle risorse sono responsabili dell'accettazione o del rifiuto delle convocazioni di riunione inviate alla cassetta postale sala. Se si assegnano più delegati della risorsa, solo uno di loro dovrà agire su una convocazione di riunione specifica.

  - **Delegati**   Se si seleziona l'opzione che prevede l'invio ai delegati delle richieste di prenotazione, verranno elencati i delegati specificati. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") o su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi") per aggiungere o rimuovere i delegati dall'elenco.

## Opzioni di prenotazione

Utilizzare la sezione **Opzioni di prenotazione** per visualizzare o modificare le impostazioni del criterio di prenotazione che definisce quando è possibile pianificare la sala, per quanto tempo può essere prenotata e quanto in anticipo.

  - **Consenti riunioni ricorrenti**   Questa impostzione consente o meno riunioni ricorrenti per la sala. Per impostazione predefinita, questa impostazione è abilitata, pertanto le riunioni ricorrenti sono consentite.

  - **Consenti pianificazione solo durante le ore lavorative**   Questa impostazione consente di accettare o rifiutare convocazioni di riunioni che non si svolgono durante le ore lavorative definite per la sala. Questa impostazione è disabilitata per impostazione predefinita, quindi le convocazioni di riunione sono consentite al di fuori dell'orario di lavoro. Per impostazione predefinita, l'orario di lavoro è dalle 8.00 alle 17.00 dal lunedì al venerdì. È possibile configurare le ore lavorative della cassetta postale sala nella sezione Aspetto della pagina Calendario.

  - **Rifiuta sempre se la data di fine supera questo limite**   Questa impostazione consente di controllare il comportamento delle riunioni ricorrenti che superano la data specificata nell'impostazione del lead time di prenotazione massimo.
    
      - Se si abilita questa impostazione, la richiesta di prenotazione ricorrente viene rifiutata automaticamente se le prenotazioni hanno inizio nella data specificata dal valore presente nella casella **Lead time di prenotazione massimo** o in una data precedente e superano la data specificata. Questa impostazione è quella predefinita.
    
      - Se si disabilita questa impostazione, la richiesta di prenotazione ricorrente viene rifiutata automaticamente se le richieste di prenotazione hanno inizio nella data specificata dal valore presente nella casella **Lead time di prenotazione massimo** o in una data precedente e superano la data specificata. Tuttavia, il numero di prenotazioni viene ridotto in modo che nessuna prenotazione oltrepassi la data specificata.

  - **Lead time di prenotazione massimo (giorni)**   Questa impostazione consente di specificare il numero massimo di giorni di anticipo con cui è possibile prenotare la sala. Input valido è un numero intero compreso tra 0 e 1080. Il valore predefinito è 180 giorni.

  - **Durata massima (ore)**   Questa impostazione consente di specificare la durata massima per cui è possibile prenotare la sala in una richiesta di prenotazione. Il valore predefinito è 24 ore.
    
    Per le richieste di prenotazione ricorrenti, la durata massima della prenotazione viene applicata alla durata di ogni istanza dell'interfaccia di amministrazione di Exchange della richiesta di prenotazione ricorrente.

In questa pagina è disponibile anche una casella utilizzabile per scrivere un messaggio che verrà inoltrato agli utenti che inviano richieste di prenotazione per la sala.

## Informazioni di contatto

La sezione **Informazioni di contatto** consente di visualizzare o modificare le informazioni di contatto per la sala. Le informazioni di questa pagina vengono visualizzate nella Rubrica.


> [!TIP]
> Il campo <STRONG>Stato/provincia</STRONG> consente di creare le condizioni relative ai destinatari per i gruppi di distribuzione dinamici, i criteri per gli indirizzi di posta elettronica o gli elenchi di indirizzi.



## Indirizzo di posta elettronica

La sezione **Indirizzo di posta elettronica** consente di visualizzare o modificare gli indirizzi di posta elettronica associati alla cassetta postale sala. Sono inclusi l'indirizzo SMTP primario della cassetta postale e qualsiasi indirizzo proxy associato. L'indirizzo SMTP primario (chiamato anche *indirizzo di risposta*) viene visualizzato in grassetto nell'elenco degli indirizzi, con il valore **SMTP** maiuscolo nella colonna **Tipo**.

  - **Aggiungi**  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere un nuovo indirizzo di posta elettronica per la cassetta postale. Selezionare uno dei seguenti tipi di indirizzo:
    
      - **SMTP**   Questo è il tipo di indirizzo predefinito. Fare clic su questo pulsante e quindi digitare il nuovo indirizzo SMTP nella casella **\* Indirizzo di posta elettronica**.
    
      - **EUM**   L'indirizzo EUM (Exchange Unified Messaging) viene utilizzato dal servizio Messaggistica unificata di Microsoft Exchange per individuare i destinatari abilitati alla messaggistica unificata in un'organizzazione di Exchange. L'indirizzo di messaggistica unificata di Exchange è costituito dal numero di interno e dal dial plan per l'utente abilitato alla messaggistica unificata. Fare clic su questo pulsante e digitare il numero di telefono interno nella casella **Indirizzo/Estensione**. Fare clic su **Sfoglia** e selezionare un dial plan per la cassetta postale.
    
      - **Tipo di indirizzo personalizzato**   Fare clic su questo pulsante e digitare uno dei tipi di indirizzi di posta elettronica non SMTP supportati nella casella **\* Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Fatta eccezione per gli indirizzi X.400, Exchange non convalida gli indirizzi personalizzati per verificarne la corretta formattazione. È necessario verificare che l'indirizzo personalizzato specificato sia conforme ai requisiti di formato per tale tipo di indirizzo.

    

    > [!NOTE]
    > Quando si aggiunge un nuovo indirizzo di posta elettronica, è possibile specificarlo come indirizzo SMTP primario.



  - **Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario** Selezionare questa casella di controllo per aggiornare automaticamente gli indirizzi di posta elettronica dei destinatari in base alle modifiche apportate ai criteri degli indirizzi di posta elettronica nell'organizzazione.

## MailTip

La sezione **Avviso messaggio** consente di aggiungere un avviso messaggio per informare gli utenti dei problemi che potrebbero verificarsi se inviano una richiesta di prenotazione alla cassetta postale sala. Un avviso messaggio è un testo che viene visualizzato sulla barra informazioni quando questo destinatario viene aggiunto nella riga A, Cc o Ccn di un nuovo messaggio di posta elettronica.


> [!NOTE]
> Gli avvisi messaggio possono includere tag HTML, ma gli script non sono consentiti. La lunghezza di un avviso messaggio personalizzato non può superare 175 caratteri visualizzati. I tag HTML non vengono conteggiati in tale limite.



## Modifica delle proprietà della cassetta postale della sala tramite Exchange PowerShell

Per visualizzare e modificare le proprietà della cassetta postale sala, utilizzare i seguenti insiemi di cmdlet: i cmdlet **Get-Mailbox** e **Set-Mailbox** che consentono di visualizzare e modificare le proprietà generali e gli indirizzi di posta elettronica per le cassette postali sala. Utilizzare i cmdlet **Get-CalendarProcessing** e **Set-CalendarProcessing** per visualizzare e modificare i delegati e le opzioni di prenotazione.

  - **Get-User** e **Set-User**   Cmdlet che consentono di visualizzare e impostare proprietà generali quali posizione, nomi di reparto e di società.

  - **Get-Mailbox** e **Set-Mailbox**   Cmdlet che consentono di visualizzare e impostare le proprietà delle cassette postali, come gli indirizzi di posta elettronica e il database delle cassette postali.

  - **Get-CalendarProcessing** e **Set-CalendarProcessing**    Cmdlet che consentono di visualizzare e impostare le opzioni di prenotazione e i delegati.

Per ulteriori informazioni su questi cmdlet, vedere i seguenti argomenti:

  - [Get-User](https://technet.microsoft.com/it-it/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/it-it/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/it-it/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/it-it/library/dd335046\(v=exchg.150\))

Di seguito sono riportati alcuni esempi dell'utilizzo di Exchange PowerShell per modificare le proprietà della cassetta postale della sala.

In questo esempio vengono modificati il nome visualizzato e l'indirizzo SMTP primario (denominato indirizzo di risposta predefinito) per la cassetta postale sala. Inoltre, l'indirizzo di risposta precedente viene mantenuto come indirizzo proxy.

    Set-Mailbox "Conf Room 123" -DisplayName "Conf Room 31/123 (12)" -EmailAddresses SMTP:Rm33.123@contoso.com,smtp:rm123@contoso.com -ResourceCapacity 12

In questo esempio le cassette postali sala vengono confgurate per consentire richieste di prenotazione da pianificare solo durante le ore lavorative e viene impostata una durata massima di 9 ore.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true -MaximumDurationInMinutes 540

In questo esempio vengono utilizzati il cmdlet **Get-User** per individuare tutte le cassette postali sala che corrispondono a sale riunioni private e il cmdlet **Set-CalendarProcessing** per inviare richieste di prenotazione al delegato Robin Wood che accetterà o rifiuterà.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox') -and (DisplayName -like 'Private*')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Robin Wood"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che le proprietà di una cassetta postale sala siano state modificate correttamente, procedere come segue.

  - Nell'interfaccia di amministrazione di Exchange, selezionare la cassetta postale e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare le proprietà o le caratteristiche modificate. A seconda della proprietà modificata, la proprietà potrebbe essere visualizzata nel riquadro Dettagli per la cassetta postale selezionata.

  - In Exchange PowerShell, utilizzare il cmdlet **Get-Mailbox** per verificare le modifiche. Utilizzando Shell è possibile visualizzare più proprietà per più cassette postali. Nell'esempio precedente, in cui le richieste di prenotazione potevano essere pianificate solo durante le ore lavorative per una durata massima di 9 ore, eseguire il comando riportato di seguito per verificare i nuovi valori.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours,MaximumDurationInMinutes

Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..


