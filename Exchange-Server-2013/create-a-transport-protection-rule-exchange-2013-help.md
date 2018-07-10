---
title: 'Creare una regola di protezione del trasporto: Exchange 2013 Help'
TOCTitle: Creare una regola di protezione del trasporto
ms:assetid: 3a857185-ee16-4ee7-9e57-8be95f7e753a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd302432(v=EXCHG.150)
ms:contentKeyID: 50480445
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare una regola di protezione del trasporto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile utilizzare le regole di protezione del trasporto per applicare la protezione dei diritti permanente ai messaggi in base alle proprietà quali mittente, destinatario, oggetto del messaggio e contenuto.


> [!WARNING]
> Prima di creare le regole di trasporto nel proprio ambiente di produzione, si consiglia di crearle in un ambiente di testing e verificarle con attenzione. Le regole di trasporto create in questo argomento sono esempi. È possibile creare le regole di trasporto utilizzando i valori e i predicati della regola di trasporto appropriati in base ai requisiti.



Per altre attività di gestione relative a Information Rights Management (IRM), vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2-5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Regole di trasporto" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Un server che esegue [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) deve essere disponibile nell'organizzazione e contenere modelli RMS esistenti.

  - Se si configurano le regole di protezione del trasporto per proteggere i messaggi utilizzando IRM e si utilizza anche l'inserimento nel journal, si tenga presente che è necessaria l'abilitazione della decrittografia del rapporto del journal per consentire all'agente di journaling di salvare una copia decrittografata del messaggio nel rapporto del journal. Per ulteriori informazioni, vedere [Decrittografia dei rapporti del journal](journal-report-decryption-exchange-2013-help.md).

  - Dopo aver creato una regola di protezione del trasporto, se la regola non può essere applicata ai messaggi poiché non è disponibile un server AD RMS, i messaggi verranno messi in coda dal servizio Trasporto sui server Cassette postali. A seconda del volume di questi messaggi, è possibile che venga utilizzato più spazio su disco sui server Cassette postali. Exchange tenterà di proteggere tramite IRM i messaggi tre volte. Dopo questi tentativi, se il server AD RMS non è raggiungibile o il messaggio non può essere protetto con IRM, viene inviato al mittente un rapporto di mancato recapito.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Utilizzare l'interfaccia di amministrazione di Exchange per creare una regola di protezione del trasporto

1.  Passare a **Flusso di posta** \> **Regole**.

2.  Nella vista dell'elenco, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  In **Nuova regola**, prima fare clic su **Altre opzioni**, quindi completare i seguenti campi:
    
      - **Nome**   Digitare un nome per la regola di trasporto.
    
      - **Applica la regola se**   Selezionare una condizione e immettere i valori richiesti per la condizione. Per aggiungere altre condizioni, fare clic su **Aggiungi condizione**.
        

        > [!IMPORTANT]
        > Se non si seleziona nessuna condizione quando si crea una regola di protezione del trasporto, tutti i messaggi gestiti dai server Exchange 2013 con il servizio Trasporto nell'organizzazione sono protetti da IRM. La protezione con IRM di tutti i messaggi richiede più risorse. Quindi, si raccomanda di programmare il server Cassette postali e la distribuzione AD&nbsp;RMS di conseguenza.

    
      - **Effettua la seguente azione**   Selezionare **Applica protezione dei diritti al messaggio con** e utilizzare la finestra di dialogo **Seleziona modello RMS** per selezionare un modello.
    
      - **Ad eccezione di**   (Facoltativo) Fare clic su **Aggiungi eccezione** per specificare un'eccezione alla regola.

4.  Fare clic su **Salva** per creare la regola di trasporto.

## Creazione di una regola di protezione del trasporto tramite Shell

  - Per creare una regola di protezione del trasporto, è necessario disporre dei modelli RMS esistenti nella distribuzione AD RMS. In questo esempio vengono recuperati i modelli disponibili dal cluster AD RMS.
    
        Get-RMSTemplate | format-list
    
    Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-RMSTemplate](https://technet.microsoft.com/it-it/library/dd297960\(v=exchg.150\)).

  - In questo esempio viene creata la regola di protezione del trasporto Protect-BusinessCriticalProject. La regola protegge con IRM i messaggi che contengono la frase "Business Critical" nel campo Oggetto con il modello **Non inoltrare**.
    

    > [!NOTE]
    > Il predicato <CODE>SubjectContainsWords</CODE> viene utilizzato in questo esempio. È possibile utilizzare qualsiasi combinazione dei predicati della regola di trasporto per formare le condizioni e le eccezioni per la regola. Per informazioni sui predicati disponibili, vedere <A href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">Condizioni delle regole di trasporto (predicati)</A>.

    
        New-TransportRule -Name "Protect-BusinessCriticalProject" -SubjectContainsWords "Business Critical" -ApplyRightsProtectionTemplate "Do Not Forward"
    
    Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-TransportRule](https://technet.microsoft.com/it-it/library/bb125138\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta creazione di una regola di protezione del trasporto, effettuare una delle seguenti operazioni:

  - Utilizzare l'interfaccia di amministrazione di Exchange per verificare che la regola sia stata creata, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare le proprietà della regola.

  - Utilizzare il cmdlet [Get-TransportRule](https://technet.microsoft.com/it-it/library/aa998585\(v=exchg.150\)) per recuperare la regola. Per un esempio di come recuperare una regola, vedere [Examples](https://technet.microsoft.com/it-it/aa998585\(exchg.150\)#examples) in **Get-TransportRule**.

  - Utilizzando Outlook, Outlook Web App, o un dispositivo mobile, inviare un messaggio di testo che soddisfi le condizioni della regola e controllare se il messaggio ricevuto dal destinatario è protetto da IRM.

