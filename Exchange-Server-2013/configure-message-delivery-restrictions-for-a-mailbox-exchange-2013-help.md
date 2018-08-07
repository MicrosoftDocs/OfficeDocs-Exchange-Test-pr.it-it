---
title: 'Configura restriz. recapito messaggi per cassetta postale: Exchange 2013 Help'
TOCTitle: Configurazione di restrizioni di recapito messaggi per una cassetta postale
ms:assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb397214(v=EXCHG.150)
ms:contentKeyID: 50555680
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione di restrizioni di recapito messaggi per una cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-29_

È possibile utilizzare EAC o Shell per applicare le restrizioni di recapito dei messaggi a singoli destinatari o meno. Le restrizioni di recapito dei messaggi sono utili per controllare chi può inviare messaggi agli utenti dell'organizzazione. Ad esempio, è possibile configurare una cassetta postale per accettare o rifiutare i messaggi inviati da utenti specifici o per accettare i messaggi solo dagli utenti dell'organizzazione di Exchange.

Le restrizioni di recapito dei messaggi trattate in questo argomento si applicano a tutti i tipi di destinatari. Per ulteriori informazioni sui diversi tipi di destinatari, vedere [Destinatari](recipients-exchange-2013-help.md).

Per le attività di gestione aggiuntive relative ai destinatari, vedere i seguenti argomenti:

  - [Gestire le cassette postali degli utenti](manage-user-mailboxes-exchange-2013-help.md)

  - [Creazione e gestione dei gruppi di distribuzione](create-and-manage-distribution-groups-exchange-2013-help.md)

  - [Gestione dei gruppi di distribuzione dinamici](manage-dynamic-distribution-groups-exchange-2013-help.md)

  - [Gestire gli utenti di posta](manage-mail-users-exchange-2013-help.md)

  - [Gestire i contatti di posta](manage-mail-contacts-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Configurazione delle restrizioni di recapito dei messaggi tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale per cui si desidera configurare le restrizioni di recapito dei messaggi, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

4.  In **Restrizioni di recapito dei messaggi** fare clic su **Visualizza dettagli** per visualizzare e modificare le restrizioni di recapito seguenti:
    
      - **Accetta messaggi da**   Utilizzare questa sezione per specificare chi può inviare messaggi a questo utente.
        
          - **Tutti i mittenti**   Questa opzione consente di specificare che l'utente può accettare messaggi da tutti i mittenti. Sono inclusi sia i mittenti nell'organizzazione di Exchange sia i mittenti esterni. Questa è l'opzione predefinita. Include gli utenti esterni solo se è stata deselezionata la casella di controllo **Richiedi autenticazione di tutti i mittenti**. Se si seleziona questa casella di controllo, i messaggi provenienti da utenti esterni saranno rifiutati.
        
          - **Solo i mittenti nell'elenco seguente**   Questa opzione consente di specificare che l'utente può accettare messaggi solo da un insieme specificato di mittenti nell'organizzazione di Exchange. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per visualizzare l'elenco di tutti i destinatari dell'organizzazione di Exchange. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").
        
          - **Richiedi autenticazione di tutti i mittenti**   Questa opzione consente di impedire agli utenti anonimi di inviare messaggi all'utente. Sono inclusi gli utenti esterni al di fuori dell'organizzazione di Exchange.
    
      - **Rifiuta messaggi da**   Utilizzare questa sezione per impedire ai contatti di inviare messaggi a questo utente.
        
          - **Nessun mittente**   Questa opzione consente di specificare che la cassetta postale non rifiuterà i messaggi provenienti dai mittenti nell'organizzazione di Exchange. Questa è l'opzione predefinita.
        
          - **Mittenti nel seguente elenco**   Questa opzione consente di specificare che la cassetta postale rifiuterà i messaggi da un insieme specificato di mittenti nell'organizzazione di Exchange. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per visualizzare l'elenco di tutti i destinatari dell'organizzazione di Exchange. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").

5.  Fare clic su **OK** per chiudere la pagina **Restrizioni di recapito dei messaggi**, quindi su **Salva** per salvare le modifiche.

## Configurazione delle restrizioni di recapito dei messaggi tramite Shell

Negli esempi seguenti viene illustrata la modalità di utilizzo di Shell per configurare le restrizioni di recapito dei messaggi per una cassetta postale. Per altri tipi di destinatari utilizzare il corrispondente cmdlet **Set-** con gli stessi parametri.

Con questo esempio viene configurata la cassetta postale di Robin Wood per accettare i messaggi solo dagli utenti Lori Penor, Jeff Phillips e dai membri del gruppo di distribuzione Legal Team 1.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"


> [!NOTE]
> Se si sta configurando una cassetta postale affinché accetti soltanto messaggi inviati da singoli mittenti, è necessario utilizzare il parametro <EM>AcceptMessagesOnlyFrom</EM>. Se si sta configurando una cassetta postale affinché accetti soltanto messaggi inviati da mittenti membri di un gruppo di distribuzione specifico, è necessario utilizzare il parametro <EM>AcceptMessagesOnlyFromDLMembers</EM>.



Con questo esempio l'utente denominato David Pelton viene aggiunto all'elenco di utenti i cui messaggi saranno accettati dalla cassetta postale di Robin Wood.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}

Con questo esempio viene configurata la cassetta postale di Robin Wood per richiedere l'autenticazione a tutti i mittenti. In questo modo la cassetta postale accetterà solo i messaggi inviati dagli altri utenti dell'organizzazione di Exchange.

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true

Con questo esempio viene configurata la cassetta postale di Robin Wood per rifiutare i messaggi dagli utenti Joe Healy, Terry Adams e dai membri del gruppo di distribuzione Legal Team 2.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"

Con questo esempio viene configurata la cassetta postale di Robin Wood per rifiutare anche i messaggi inviati dai membri del gruppo Legal Team 3.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}


> [!NOTE]
> Se si sta configurando una cassetta postale affinché rifiuti i messaggi inviati da singoli mittenti, è necessario utilizzare il parametro <EM>RejectMessagesFrom</EM>. Se si sta configurando una cassetta postale affinché rifiuti i messaggi inviati da mittenti membri di un gruppo di distribuzione specifico, è necessario utilizzare il parametro <EM>RejectMessagesFromDLMembers</EM>.



Per informazioni dettagliate sulla sintassi e sui parametri relative alla configurazione delle restrizioni di recapito per i diversi tipi di destinatari, vedere gli argomenti seguenti:

  - [Set-DistributionGroup](https://technet.microsoft.com/it-it/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/it-it/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/it-it/library/aa995950\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/it-it/library/aa995971\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta configurazione delle restrizioni di recapito dei messaggi per la cassetta postale utente, effettuare una delle seguenti operazioni:

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale per cui si desidera verificare le restrizioni di recapito dei messaggi, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

4.  In **Restrizioni di recapito dei messaggi** fare clic su **Visualizza dettagli** per verificare le restrizioni di recapito per la cassetta postale.

Oppure

Eseguire il seguente comando in Shell.

    Get-Mailbox <identity> | fl AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

