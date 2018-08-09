---
title: 'Configura limiti dimens. messaggi per cassetta postale: Exchange 2013 Help'
TOCTitle: Configurazione dei limiti nelle dimensioni dei messaggi per una cassetta postale
ms:assetid: d1220685-14c0-4c4f-abb2-3920f3046212
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124708(v=EXCHG.150)
ms:contentKeyID: 50555684
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurazione dei limiti nelle dimensioni dei messaggi per una cassetta postale

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-12_

È possibile utilizzare EAC e Shell per configurare i limiti di dimensione dei messaggi per la cassetta postale utente. Tali limiti controllano la dimensione dei messaggi che un utente può inviare e ricevere. Per impostazione predefinita, quando viene creata una cassetta postale, non sono presenti limiti di dimensione per i messaggi inviati e ricevuti.

È necessario tenere presente che esistono altre impostazioni in un'organizzazione di Exchange che determinano la dimensione massima dei messaggi che una cassetta postale può inviare e ricevere, ad esempio, la dimensione massima dei messaggi configurata in un server Cassette postali. Per ulteriori informazioni sulle restrizioni applicate alle dimensioni dei messaggi, inclusi i tipi di limiti di dimensione dei messaggi, l'ambito e l'ordine di precedenza, vedere [Limiti di dimensione dei messaggi](message-size-limits-exchange-2013-help.md).

Per le attività di gestione aggiuntive relative alle cassette postali utente, vedere [Gestire le cassette postali degli utenti](manage-user-mailboxes-exchange-2013-help.md).


> [!NOTE]
> È inoltre possibile controllare la dimensione dei messaggi inviati e ricevuti dagli utenti di posta e dalle cassette postali condivise.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Configurazione dei limiti per le dimensioni dei messaggi tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale di cui si desidera cambiare i limiti di dimensione dei messaggi, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

4.  In **Restrizioni di dimensione per i messaggi** fare clic su **Visualizza dettagli** per visualizzare e modificare i limiti di dimensione dei messaggi seguenti:
    
      - **Messaggi inviati**   Per specificare una dimensione massima per i messaggi inviati da questo utente, selezionare la casella di controllo **Dimensione massima messaggio (KB)** e digitare un valore nella casella. La dimensione dei messaggi deve essere compresa tra 0 e 2.097.151 KB. Se l'utente invia un messaggio di dimensioni superiori a quelle specificate, il messaggio viene restituito all'utente con un messaggio di errore descrittivo.
    
      - **Messaggi ricevuti**   Per specificare una dimensione massima per i messaggi ricevuti da questo utente, selezionare la casella di controllo **Dimensione massima messaggio (KB)** e digitare un valore nella casella. La dimensione dei messaggi deve essere compresa tra 0 e 2.097.151 KB. Se all'utente viene inviato un messaggio di dimensioni superiori a quelle specificate, questo verrà restituito al mittente con un messaggio di errore descrittivo.

5.  Fare clic su **OK**, quindi su **Salva** per salvare le modifiche.

## Configurazione dei limiti per le dimensioni dei messaggi tramite Shell

Con questo esempio viene impostata su 25 MB la dimensione massima per i messaggi inviati e su 35 MB la dimensione massima per i messaggi ricevuti per la cassetta postale di Debra Garcia.

    Set-Mailbox "Debra Garcia" -MaxSendSize 25mb -MaxReceiveSize 35mb

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta configurazione dei limiti di dimensione dei messaggi per una cassetta postale utente, effettuare una delle seguenti operazioni:

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nell'elenco delle cassette postali utente, fare clic sulla cassetta postale di cui si desidera verificare i limiti di dimensione dei messaggi, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina delle proprietà della cassetta postale, fare clic su **Funzionalità cassette postali**.

4.  In **Restrizioni di dimensione per i messaggi** fare clic su **Visualizza dettagli** per verificare i limiti di dimensione dei messaggi per la cassetta postale.

Oppure

Eseguire il seguente comando in Shell.

    Get-Mailbox <identity> | fl MaxSendSize,MaxReceiveSize

