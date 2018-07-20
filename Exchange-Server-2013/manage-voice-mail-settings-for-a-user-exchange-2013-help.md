---
title: 'Gestire le impostazioni della posta vocale di un utente: Exchange 2013 Help'
TOCTitle: Gestire le impostazioni della posta vocale di un utente
ms:assetid: 73957938-048a-4f9c-bd0f-a3c2c3dcd638
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998851(v=EXCHG.150)
ms:contentKeyID: 50480979
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire le impostazioni della posta vocale di un utente

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile visualizzare o impostare la Messaggistica unificata (UM), le funzionalità per i messaggi vocali e le impostazioni di configurazione per un utente che è stato abilitato per la messaggistica unificata e i messaggi vocali. Ad esempio, non è possibile eseguire le seguenti operazioni:

  - Reimpostare il PIN di Outlook Voice Access.

  - Aggiungere un numero di interno operatore personale.

  - Aggiungere altri numeri interni.

  - Attivare o disattivare il riconoscimento vocale automatico (ASR).

  - Attivare o disattivare le regole ricezione chiamata.

  - Abilitare o disabilitare l'accesso alla posta elettronica o al calendario.


> [!NOTE]
> Alcune delle impostazioni e funzionalità possono essere configurate solo utilizzando Shell.



Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che l'utente esistente sia abilitato alla Messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Visualizzazione o configurazione delle proprietà di un utente abilitato alla messaggistica unificata tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione Elenco selezionare la cassetta postale per la quale si desidera modificare il criterio cassetta postale di messaggistica unificata.

3.  Nel riquadro dei dettagli, sotto **Phone and Voice Features** \> **Messaggistica unificata** fare clic su **Visualizza dettagli**.

4.  Nella pagina **Cassetta postale di messaggistica unificata**, fare clic su **Impostazioni cassetta postale di messaggistica unificata** per visualizzare o modificare le seguenti proprietà di messaggistica unificata per un utente abilitato alla messaggistica unificata:
    
      - **Stato PIN**   In questo campo di sola visualizzazione è riportato lo stato della cassetta postale dell'utente. Per impostazione predefinita, quando un utente è abilitato alla messaggistica unificata, lo stato del PIN è **Non bloccato**. Tuttavia, se l'utente inserisce più volte un PIN di Outlook Voice Access errato, lo stato viene visualizzato come **Bloccato**.
    
      - **Criteri cassetta postale di messaggistica unificata**   Questa casella mostra il nome dei criteri della cassetta postale di messaggistica unificata associato all'utente abilitato alla messaggistica unificata. È possibile fare clic su **Sfoglia** per individuare e specificare i criteri della cassetta postale di messaggistica unificata da associare a questa cassetta.
    
      - **Interno operatore personale**   Utilizzare questa casella per specificare il numero di interno di un operatore per l'utente. Per impostazione predefinita, il numero di interno non è configurato. Per il numero di interno è possibile inserire da 1 a 20 caratteri. Ciò consente di inoltrare le chiamate in arrivo per l'utente abilitato alla messaggistica unificata al numero specificato nella casella.
        
        È possibile configurare altri tipi di numeri di interno di operatori sui dial plan e per gli operatori automatici. Tuttavia, tali numeri sono in genere utilizzati per centralinisti o altri addetti che operano a livello di azienda globale. L'impostazione Interno operatore personale può, invece, essere utilizzata per consentire a un assistente amministrativo o un assistente personale di rispondere alle chiamate in arrivo per poi passarle all'utente.

5.  Nella pagina **Cassetta postale di messaggistica unificata**, sotto **Altri interni**, è possibile aggiungere, modificare e visualizzare i numeri interni per l'utente.
    
      - Per aggiungere un numero di interno, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). . Nella pagina **Aggiungi un altro interno**, utilizzare **Sfoglia** per selezionare il dial plan di messaggistica unificata quindi immettere il numero di interno nella casella **Numero interno**.
    
      - Per rimuovere un interno, selezionare il numero che si desidera rimuovere in questa casella e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

6.  Se si apportano modifiche, fare clic su **Salva**.

## Configurazione delle funzionalità per un utente abilitato alla messaggistica unificata tramite Shell

Con questo esempio vengono disabilitati Ascolta al telefono e le notifiche delle chiamate senza risposta, ma vengono abilitate le notifiche dei messaggi di testo (SMS).


> [!NOTE]
> Per le distribuzioni ibride e locali, durante l'integrazione della messaggistica unificata con Lync Server, le notifiche di chiamata senza risposta non sono disponibili per gli utenti la cui cassetta postale si trova su un server Cassette postali di Exchange 2007 o Exchange 2010. Una notifica di chiamata senza risposta viene generata quando un utente effettua la disconnessione prima che la chiamata sia inviata a un server Cassette postali.



    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -MissedCallNotificationEnabled $false -PlayonPhoneEnabled $false -SMSMessageWaitingNotificationEnabled $true

Con questo esempio si impedisce a un utente di accedere al Calendario, ma si consente l'accesso alla posta elettronica quando l'utente utilizza Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -Extension 523456 -FAXEnabled $true -TUIAccessToCal $false -TUIAccessToEmail True

Con questo esempio si impedisce a un utente di accedere al Calendario e alla posta elettronica quando l'utente utilizza Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -TUIAccessToCalendarEnabled $false -TUIAccessToEmailEnabled $false

Questo esempio impedisce a un utente di creare delle regole ricezione chiamata, di ricevere i fax in entrata e di utilizzare Outlook Voice Access, ma abilita il riconoscimento vocale automatico (ASR).

    Set-UMMailbox -Identity tony@contoso.com -AutomaticSpeechRecognitionEnabled $true -CallAnsweringRulesEnabled $false -FaxEnabled $false -SubscriberAccessEnabled $false 

## Visualizzazione delle proprietà di un utente abilitato alla messaggistica unificata tramite Shell

Con questo esempio viene visualizzato un elenco formattato di tutte le cassette postali abilitate alla messaggistica unificata nella foresta.

    Get-UMMailbox | Format-List

Con questo esempio vengono visualizzate le proprietà della cassetta postale di messaggistica unificata per tonysmith@contoso.com.

    Get-UMMailbox -Identity tonysmith@contoso.com


> [!IMPORTANT]
> Quando si eseguono Exchange 2007 e Exchange 2013 e la cassetta postale dell'utente si trova sul server Cassette postali di Exchange 2007, l'esecuzione del cmdlet <STRONG>Get-UMMailbox</STRONG> non funzionerà correttamente. Per risolvere il problema, eseguire il cmdlet <STRONG>Get-UMMailbox</STRONG> da un server Exchange 2007 o un computer su cui sono in esecuzione gli strumenti amministrativi di Exchange 2007.


