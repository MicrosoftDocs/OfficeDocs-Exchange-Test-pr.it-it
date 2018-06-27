---
title: 'Aggiungere un numero interno: Exchange 2013 Help'
TOCTitle: Aggiungere un numero interno
ms:assetid: 1a73c9c8-cb50-4bd7-a101-dadd20e28031
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335124(v=EXCHG.150)
ms:contentKeyID: 50555552
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiungere un numero interno

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-14_

Quando si abilita un utente alla messaggistica unificata e lo si collega al dial plan di un numero di interno, viene creato per l'utente un indirizzo proxy di messaggistica unificata di Exchange contenente il numero di interno dell'utente. È necessario definire almeno un numero di interno per la messaggistica unificata in modo tale che la posta vocale possa essere inviata alla cassetta postale dell'utente. Il numero di interno viene inoltre utilizzato quando l'utente chiama un numero di Outlook Voice Access.

Il numero di interno primario aggiunto quando l'utente era abilitato alla messaggistica unificata verrà riportato come indirizzo proxy primario della messaggistica unificata di Exchange. Se il numero di interno primario è stato eliminato, il primo indirizzo proxy di messaggistica unificata di Exchange aggiunto che contiene il numero di interno dell'utente diventerà l'indirizzo proxy primario di messaggistica unificata di Exchange. Qualsiasi altro numero di interno che si aggiunge verrà riportato come indirizzo proxy secondario di messaggistica unificata di Exchange. Quando vengono aggiunti numeri di interni secondari, i chiamanti possono lasciare messaggi vocali per l'utente a tutti i numeri di interni che sono stati impostati. Tutti i messaggi vocali saranno recapitati alla cassetta postale dell'utente stesso.

È possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per aggiungere un numero di interno primario o secondario per un utente. È possibile utilizzare la pagina **Indirizzo di posta elettronica** sulla cassetta postale dell'utente nell'interfaccia di amministrazione di Exchange per aggiungere un numero di interno primario o secondario. Non è possibile utilizzare la pagina **Cassetta postale di messaggistica unificata** nell'interfaccia di amministrazione di Exchange per aggiungere un numero di interno primario, ma è possibile aggiungere la pagina per aggiungere numeri di interni secondari.

È possibile visualizzare i numeri di interni primari e secondari per un utente utilizzando il cmdlet **Get-UMMailbox** o il cmdlet **Get-Mailbox** in Shell.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata di un numero di interno prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, confermare che la cassetta postale dell'utente sia stata abilitata per la messaggistica unificata e collegata al dial plan di un numero di interno. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Prima di eseguire queste procedure, confermare che il numero di interno che verrà assegnato all'utente contenga il numero corretto di insieme di cifre sul dial plan di messaggistica unificata.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Utilizzare l'interfaccia di amministrazione di Exchange per aggiungere un numero di interno secondario

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzaazione elenco, selezionare la cassetta postale alla quale si desidera aggiungere un numero di interno.

3.  Nel riquadro dei dettagli, **Funzionalità telefoniche e vocali** sotto **Messaggistica unificata** fare clic su **Visualizza dettagli**.

4.  Nella pagina **Cassetta postale di messaggistica unificata** fare clic su **Altri interni**, quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

5.  Nella pagina **Altri interni**, accanto alla casella **Dial plan di messaggistica unificata**, fare clic su **Sfoglia** e individuare il dial plan per l'utente.

6.  Nella pagina **Altri interni**, nella casella **Numero dell'interno**, digitare il numero dell'interno, quindi fare clic su **OK**.

7.  Fare clic su **Salva**.

## Utilizzo dell'interfaccia di amministrazione di Exchange per aggiungere un numero di interno primario o secondario

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione elenco, selezionare la cassetta postale a cui aggiungere un numero di interno, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Cassetta postale utente**, sotto **Indirizzo di posta elettronica**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Nella pagina **Nuovo indirizzo di posta elettronica**, selezionare **Messaggistica unificata di Exchange** e nella casella **Indirizzo/Estensione**, digitare il numero di interno per l'utente.

5.  Nella pagina **Nuovo indirizzo di posta elettronica**,sotto **Dial plan**, fare clic su **Sfoglia** per selezionare il dial plan del numero di interno, quindi fare clic su **OK**.

6.  Fare clic su **Salva**.

## Utilizzo di Shell per aggiungere un numero di interno

In questo esempio viene aggiunto un numero di interno 22222 per Tony Smith, un utente abilitato alla messaggistica unificata.


> [!NOTE]
> Prima di aggiungere un numero di interno utilizzando Shell, è necessario determinare la posizione dell'indirizzo proxy di messaggistica unificata di Exchange che si desidera aggiungere. Per determinare la posizione, utilizzare il comando <STRONG>$mbx.EmailAddresses</STRONG>. Il primo indirizzo proxy nell'elenco sarà 0.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

