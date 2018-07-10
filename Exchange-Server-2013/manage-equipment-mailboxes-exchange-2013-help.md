---
title: 'Gestire le cassette postali attrezzatura: Exchange 2013 Help'
TOCTitle: Gestire le cassette postali attrezzatura
ms:assetid: e5f58b3a-83e1-4742-8846-85103a44ee18
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ215770(v=EXCHG.150)
ms:contentKeyID: 50479876
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire le cassette postali attrezzatura

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-10-09_

Una *cassetta postale apparecchiatura* è una cassetta postale per le risorse assegnata a una risorsa non specifica per un luogo, ad esempio un computer portatile, un proiettore, un microfono o un'auto aziendale. Una volta creata dall'amministratore la cassetta postale attrezzatura, gli utenti possono prenotare facilmente l'attrezzatura includendo la cassetta postale attrezzatura corrispondente in una convocazione di riunione. È possibile creare una cassetta postale attrezzatura o modificarne le proprietà tramite l'interfaccia di amministrazione di Exchange e la shell. Per ulteriori informazioni, vedere [Destinatari](recipients-exchange-2013-help.md).

Per informazioni su un altro tipo di cassetta postale delle risorse, la cassetta postale della sala, vedere [Creazione e gestione delle cassette sala](create-and-manage-room-mailboxes-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2-5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creazione di una cassetta postale attrezzatura

## Creazione di una cassetta postale attrezzatura tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Risorse**.

2.  Per creare una cassetta postale attrezzatura, fare clic su **Nuova** \> **Cassetta postale attrezzatura**. Per creare una cassetta postale della sala, fare clic su **Nuova** \> **Cassetta postale sala**.

3.  Utilizzare le opzioni disponibili nella pagina per specificare le impostazioni per la nuova cassetta postale delle risorse.
    
      - **\* Nome attrezzature**   Utilizzare questa casella per digitare un nome per la cassetta postale attrezzatura. Si tratta del nome presente nell'elenco delle cassette postali per le risorse in Stima al completamento e nella rubrica dell'organizzazione. Questo nome è obbligatorio e non può superare i 64 caratteri.
        

        > [!TIP]
        > Benché vi siano altri campi che descrivono i dettagli della sala, ad esempio Capacità, è utile riepilogare i dettagli più importanti nel nome delle attrezzature utilizzando una convenzione di denominazione coerente. Ciò è necessario in quanto gli utenti possono visualizzare facilmente i dettagli quando selezionano l'attrezzatura dalla rubrica nella convocazione di riunione.

    
      - **\* Indirizzo di posta elettronica**   La cassetta postale attrezzatura dispone di un indirizzo di posta elettronica per ricevere le richieste di prenotazione. L'indirizzo di posta elettronica è costituito da un alias alla sinistra del simbolo @, che deve essere univoco nella foresta, e da un nome di dominio a destra. L'indirizzo di posta elettronica è obbligatorio.

4.  Al termine, scegliere **Salva** per creare la cassetta postale attrezzatura.

Una volta creata la cassetta postale attrezzatura, è possibile modificare la cassetta postale apparecchiatura per aggiornare le informazioni sulle opzioni di prenotazione, suggerimenti messaggio e i delegati. Estrarre modifica apparecchiature delle cassette postali area proprietà riportati di seguito per modificare le proprietà della cassetta postale sala

## Creazione di una cassetta postale apparecchiatura tramite Shell

Con questo esempio viene creata una cassetta postale apparecchiatura con la seguente configurazione:

  - La cassetta postale apparecchiatura si trova nel database Mailbox Database 1.

  - Il nome dell'attrezzatura è MotorVehicle2 e sarà visualizzato nell'elenco indirizzi globale come Motor Vehicle 2.

  - L'indirizzo di posta elettronica è MotorVehicle2@contoso.com.

  - La cassetta postale si trova nell'unità organizzativa Equipment.

  - Il parametro *Equipment* specifica che questa cassetta postale sarà creata come cassetta postale attrezzatura.

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name MotorVehicle2 -OrganizationalUnit Equipment -DisplayName "Motor Vehicle 2" -Equipment

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-Mailbox](https://technet.microsoft.com/it-it/library/aa997663\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione della cassetta postale utente, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Risorse**. La nuova cassetta postale utente viene visualizzata nell'elenco delle cassette postali. In **Tipo di cassetta postale**, il tipo è **Attrezzature**.

  - Nella shell, eseguire il comando riportato di seguito per visualizzare le informazioni sulla nuova cassetta postale attrezzatura.
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Modifica delle proprietà della cassetta postale attrezzatura

Una volta creata la cassetta postale attrezzatura, è possibile modificarla e impostare proprietà aggiuntive utilizzando l'interfaccia di amministrazione di Exchange o la shell.

## Modifica delle proprietà della cassetta postale attrezzatura tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Risorse**.

2.  Nell'elenco delle cassette postali per le risorse, fare clic sulla cassetta postale attrezzatura di cui modificare le proprietà e scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà della cassetta postale attrezzatura, fare clic su una delle seguenti sezioni per visualizzane o modificane le proprietà.
    
      - General
    
      - Delegati
    
      - Booking Options
    
      - Contact Information
    
      - Email Address
    
      - MailTip

## Generale

Utilizzare la sezione **Generale** per visualizzare o modificare le informazioni di base sulla risorsa.

  - **\* Nome dell'attrezzatura**   Il nome presente nell'elenco delle cassette postali per le risorse nell'interfaccia di amministrazione di Exchange e nella rubrica dell'organizzazione. L'alias modificato non può superare i 64 caratteri.

  - **\* Indirizzo di posta elettronica**   Casella di sola lettura in cui viene visualizzato l'indirizzo di posta elettronica per la cassetta postale attrezzatura. È possibile modificarlo nella sezione Email Address.

  - **Capacità**   Casella che consente di immettere il numero massimo di utenti che possono utilizzare tale risorsa, se applicabile. Ad esempio, se la cassetta postale attrezzatura corrisponde a un'utilitaria, immettere **4**.

Fare clic su **Altre opzioni** per visualizzare o modificare le seguenti proprietà aggiuntive:

  - **Unità organizzativa**   In questa casella di sola lettura è visualizzata l'unità organizzativa contenente l'account per la cassetta postale attrezzatura. Per spostare l'account verso un'unità organizzativa (OU) diversa, è necessario utilizzare Utenti e computer di Active Directory.

  - **Database delle cassette postali**   In questa casella di sola lettura è visualizzato il nome del database delle cassette postali che ospita la cassetta postale attrezzatura. Utilizzare la pagina **Migrazione** in Stima al completamento per spostare la cassetta postale in un database diverso.

  - **Alias** Utilizzare questa casella per modificare l'alias della cassetta postale attrezzatura.

  - **Non visualizzare negli elenchi di indirizzi di Exchange** Selezionare questa casella di controllo per non consentire la visualizzazione della cassetta postale attrezzatura nella rubrica e in altri elenchi di indirizzi definiti nell'organizzazione Exchange. Una volta selezionata questa casella di controllo, gli utenti possono comunque inviare messaggi di prenotazione alla cassetta postale attrezzatura utilizzando l'indirizzo di posta elettronica.

  - **Reparto**   Utilizzare questa casella per specificare il nome del reparto a cui la risorsa è associata. È possibile utilizzare questa proprietà per creare condizioni del destinatario per i gruppi di distribuzione dinamici e gli elenchi di indirizzi.

  - **Società**   Utilizzare questa casella per specificare un nome di società a cui la risorsa è associata. Analogamente alla proprietà Reparto, è possibile utilizzare questa proprietà per creare condizioni del destinatario per i gruppi di distribuzione dinamici e gli elenchi di indirizzi.

  - **Criterio rubrica**   Opzione che consente di specificare un criterio rubrica per la risorsa. I criteri rubrica contengono un elenco di indirizzi globale, una rubrica offline , un elenco di sale e un set di elenchi di indirizzi. Per ulteriori informazioni, vedere [Criteri delle rubriche](address-book-policies-exchange-2013-help.md).
    
    Nell'elenco a discesa, selezionare il criterio da associare a questa cassetta postale.

  - **Attributi personalizzati**   In questa sezione vengono visualizzati gli attributi personalizzati definiti per la cassetta postale attrezzatura. Per specificare valori personalizzati per gli attributi, fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). È possibile specificare fino a 15 attributi personalizzati per un destinatario.

## Delegati

Utilizzare questa sezione per visualizzare o modificare le modalità di gestione delle richieste di prenotazione nella cassetta postale attrezzatura e per definire gli utenti che possono accettare o rifiutare le richieste di prenotazione se l'operazione non è automatica.

  - **Richieste di prenotazione**   Selezionare una delle seguenti opzioni per la gestione delle richieste di prenotazione.
    
      - **Accetta o rifiuta automaticamente le richieste di prenotazione**   Una convocazione di riunione valida prenota automaticamente la risorsa. Se è presente un conflitto di pianificazione con una prenotazione esistente o se la richiesta di prenotazione viola i limiti di pianificazione della risorsa, ad esempio la durata della prenotazione è troppo lunga, la convocazione della riunione viene automaticamente negata.
    
      - **Seleziona delegati per accettazione o rifiuto delle richieste di prenotazione**   I delegati delle risorse sono responsabili dell'accettazione o del rifiuto delle convocazioni di riunione inviate alla cassetta postale attrezzatura. Se si assegnano più delegati della risorsa, solo uno di loro dovrà agire su una convocazione di riunione specifica.

  - **Delegati**   Se si seleziona l'opzione che prevede l'invio ai delegati delle richieste di prenotazione, verranno elencati i delegati specificati. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") o su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi") per aggiungere o rimuovere i delegati dall'elenco.

## Opzioni di prenotazione

Utilizzare la sezione **Opzioni di prenotazione** per visualizzare o modificare le impostazioni del criterio di prenotazione che definisce quando è possibile pianificare la risorsa, per quanto tempo può essere prenotata e quanto in anticipo.

  - **Consenti riunioni ricorrenti**   Questa impostzione consente o meno riunioni ricorrenti per la risorsa. Per impostazione predefinita, questa impostazione è abilitata, pertanto le riunioni ricorrenti sono consentite.

  - **Consenti pianificazione solo durante le ore lavorative**   Questa impostazione consente di accettare o rifiutare convocazioni di riunioni che non si svolgono durante le ore lavorative definite per la risorsa. Questa impostazione è disabilitata per impostazione predefinita, quindi le convocazioni di riunione sono consentite al di fuori dell'orario di lavoro. Per impostazione predefinita, l'orario di lavoro è dalle 8.00 alle 17.00 dal lunedì al venerdì. È possibile configurare le ore lavorative della cassetta postale attrezzatura nella sezione Aspetto della pagina Calendario.

  - **Rifiuta sempre se la data di fine supera questo limite**   Questa impostazione consente di controllare il comportamento delle riunioni ricorrenti che superano la data specificata nell'impostazione del lead time di prenotazione massimo.
    
      - Se si abilita questa impostazione, la richiesta di prenotazione ricorrente viene rifiutata automaticamente se le prenotazioni hanno inizio nella data specificata dal valore presente nella casella **Lead time di prenotazione massimo** o in una data precedente e superano la data specificata. Questa impostazione è quella predefinita.
    
      - Se si disabilita questa impostazione, la richiesta di prenotazione ricorrente viene rifiutata automaticamente se le richieste di prenotazione hanno inizio nella data specificata dal valore presente nella casella **Lead time di prenotazione massimo** o in una data precedente e superano la data specificata. Tuttavia, il numero di prenotazioni viene ridotto in modo che nessuna prenotazione oltrepassi la data specificata.

  - **Lead time di prenotazione massimo (giorni)**   Questa impostazione consente di specificare il numero massimo di giorni di anticipo con cui è possibile prenotare la risorsa. Input valido è un numero intero compreso tra 0 e 1080. Il valore predefinito è 180 giorni.

  - **Durata massima (ore)**   Questa impostazione consente di specificare la durata massima per cui è possibile prenotare la risorsa in una richiesta di prenotazione. Il valore predefinito è 24 ore.
    
    Per le richieste di prenotazione ricorrenti, la durata massima della prenotazione viene applicata alla durata di ogni istanza della richiesta di prenotazione ricorrente.

In questa pagina è disponibile anche una casella utilizzabile per scrivere un messaggio che verrà inviato agli utenti che inviano convocazioni di riunioni per prenotare la risorsa.

## Informazioni di contatto

La sezione **Informazioni di contatto** consente di visualizzare o modificare le informazioni di contatto per la risorsa. Le informazioni di questa pagina vengono visualizzate nella Rubrica.


> [!TIP]
> Il campo <STRONG>Stato/provincia</STRONG> consente di creare le condizioni relative ai destinatari per i gruppi di distribuzione dinamici, i criteri per gli indirizzi di posta elettronica o gli elenchi di indirizzi.



## Indirizzo di posta elettronica

La sezione **Indirizzo di posta elettronica** consente di visualizzare o modificare gli indirizzi di posta elettronica associati alla cassetta postale attrezzatura. Sono inclusi l'indirizzo SMTP primario della cassetta postale e qualsiasi indirizzo proxy associato. L'indirizzo SMTP primario (chiamato anche *indirizzo di risposta*) viene visualizzato in grassetto nell'elenco degli indirizzi, con il valore **SMTP** maiuscolo nella colonna **Tipo**.

  - **Aggiungi **  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere un nuovo indirizzo di posta elettronica per la cassetta postale. Selezionare uno dei seguenti tipi di indirizzo:
    
      - **SMTP**   Questo è il tipo di indirizzo predefinito. Fare clic su questo pulsante e quindi digitare il nuovo indirizzo SMTP nella casella **\* Indirizzo di posta elettronica**.
    
      - **EUM**   L'indirizzo EUM (Exchange Unified Messaging) viene utilizzato dal servizio Messaggistica unificata di Microsoft Exchange per individuare i destinatari abilitati alla messaggistica unificata in un'organizzazione di Exchange. L'indirizzo di messaggistica unificata di Exchange è costituito dal numero di interno e dal dial plan per l'utente abilitato alla messaggistica unificata. Fare clic su questo pulsante e digitare il numero di telefono interno nella casella **Indirizzo/Estensione**. Fare clic su **Sfoglia** e selezionare un dial plan per la cassetta postale.
    
      - **Tipo di indirizzo personalizzato**   Fare clic su questo pulsante e digitare uno dei tipi di indirizzi di posta elettronica non SMTP supportati nella casella **\* Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Fatta eccezione per gli indirizzi X.400, Exchange non convalida gli indirizzi personalizzati per verificarne la corretta formattazione. È necessario verificare che l'indirizzo personalizzato specificato sia conforme ai requisiti di formato per tale tipo di indirizzo.

    

    > [!NOTE]
    > Quando si aggiunge un nuovo indirizzo di posta elettronica, è possibile specificarlo come indirizzo SMTP primario.



  - **Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario   **Selezionare questa casella di controllo per aggiornare automaticamente gli indirizzi di posta elettronica dei destinatari in base alle modifiche apportate ai criteri degli indirizzi di posta elettronica nell'organizzazione.

## MailTip

La sezione **Avviso messaggio** consente di aggiungere un avviso messaggio per informare gli utenti dei problemi che potrebbero verificarsi se inviano una richiesta di prenotazione alla cassetta postale attrezzatura. Un avviso messaggio è un testo che viene visualizzato sulla barra informazioni quando questo destinatario viene aggiunto nella riga A, Cc o Ccn di un nuovo messaggio di posta elettronica.


> [!NOTE]
> Gli avvisi messaggio possono includere tag HTML, ma gli script non sono consentiti. La lunghezza di un avviso messaggio personalizzato non può superare 175 caratteri visualizzati. I tag HTML non vengono conteggiati in tale limite.



## Modifica delle proprietà della cassetta postale attrezzatura tramite Shell

Per visualizzare e modificare le proprietà della cassetta postale attrezzatura, utilizzare i seguenti insiemi di cmdlet: i cmdlet **Get-Mailbox** e **Set-Mailbox** che consentono di visualizzare e modificare le proprietà generali e gli indirizzi di posta elettronica per le cassette postali attrezzatura. Utilizzare i cmdlet **Get-CalendarProcessing** e **Set-CalendarProcessing** per visualizzare e modificare i delegati e le opzioni di prenotazione.

  - **Get-User** e **Set-User**   Cmdlet che consentono di visualizzare e impostare proprietà generali quali nomi di reparto e di società.

  - **Get-Mailbox** e **Set-Mailbox**   Cmdlet che consentono di visualizzare e impostare le proprietà delle cassette postali, come gli indirizzi di posta elettronica e il database delle cassette postali.

  - **Get-CalendarProcessing** e **Set-CalendarProcessing**    Cmdlet che consentono di visualizzare e impostare le opzioni di prenotazione e i delegati.

Per ulteriori informazioni su questi cmdlet, vedere i seguenti argomenti:

  - [Get-User](https://technet.microsoft.com/it-it/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/it-it/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/it-it/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/it-it/library/dd335046\(v=exchg.150\))

Di seguito sono riportati alcuni esempi dell'utilizzo della shell per modificare le proprietà della cassetta postale attrezzatura.

In questo esempio vengono modificati il nome visualizzato e l'indirizzo SMTP primario (denominato indirizzo di risposta predefinito) per la cassetta postale attrezzatura MotorPool 1. L'indirizzo di risposta precedente viene mantenuto come indirizzo proxy.

    Set-Mailbox "MotorPool 1" -DisplayName "Motor Pool 1 - Compact" -EmailAddresses SMTP:MP1.compact@contoso.com,smtp:MP.1@contoso.com

In questo esempio vengono configurate le cassette postali attrezzatura per consentire la pianificazione delle richieste di prenotazione solo durante le ore lavorative.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true

In questo esempio vengono utilizzati il cmdlet **Get-User** per individuare tutte le cassette postali attrezzatura nel reparto audiovisivi e il cmdlet **Set-CalendarProcessing** per inviare richieste di prenotazione al delegato Ann Beebe che accetterà o rifiuterà.

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox') -and (Department -eq 'Audio Visual')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Ann Beebe"

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che le proprietà di una cassetta postale attrezzatura siano state modificate correttamente, procedere come segue.

  - In EAC selezionare la cassetta postale e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare le proprietà o le caratteristiche modificate. A seconda della proprietà modificata, la proprietà potrebbe essere visualizzata nel riquadro Dettagli per la cassetta postale selezionata.

  - In Shell, utilizzare il cmdlet **Get-Mailbox** per verificare le modifiche. Utilizzando Shell è possibile visualizzare più proprietà per più cassette postali. Nell'esempio precedente, in cui le richieste di prenotazione potevano essere pianificate solo durante le ore lavorative, eseguire il comando riportato di seguito per verificare il nuovo valore.
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours

