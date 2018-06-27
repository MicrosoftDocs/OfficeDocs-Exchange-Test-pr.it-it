---
title: 'Creazione di un operatore automatico di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Creazione di un operatore automatico di messaggistica unificata
ms:assetid: 773f53fb-d80f-4a79-8bd3-bd753942489f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998875(v=EXCHG.150)
ms:contentKeyID: 50481002
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.CreateAutoAttendantWizardForm.CreateAutoAttendantWizardPage
ms.translationtype: MT
---

# Creazione di un operatore automatico di messaggistica unificata

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-03-08_

Dopo aver creato un operatore automatico di messaggistica unificata (UM), le chiamate in arrivo a un numero di telefono esterno che potrebbe rispondere a un operatore umano sono ha risposto per l'operatore automatico. A differenza con altri componenti di messaggistica unificata, ad esempio messaggistica unificata dial plan e i gateway IP di messaggistica unificata, non sono necessari per creare gli operatori automatici di messaggistica unificata. Tuttavia, gli operatori automatici Guida interno e i chiamanti esterni consente di individuare gli utenti o i reparti che esistono in un'organizzazione e trasferire loro le chiamate.

Per altre attività di gestione relative agli operatori automatici di messaggistica unificata, vedere [Procedure di operatore automatico di messaggistica unificata](um-auto-attendant-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Operatori automatici di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per creare un operatore automatico di messaggistica unificata

1.  
    
    In EAC accedere a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**, selezionare il dial plan di messaggistica unificata per cui si desidera aggiungere un operatore automatico e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") .

2.  Nella pagina **Dial Plan**, in **Operatori automatici di messaggistica unificata**, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **nuovo operatore automatico**, immettere le informazioni seguenti:
    
      - **Nome**   Utilizzare questa casella per creare il nome visualizzato per l'operatore automatico di messaggistica unificata. Il nome di un operatore automatico di messaggistica unificata è obbligatorio e deve essere univoco. Tuttavia, viene utilizzato solo per la visualizzazione in EAC e Shell.
        
        Qualora fosse necessario modificare il nome visualizzato dell'operatore automatico dopo che è stato creato, eliminare in primo luogo l'operatore automatico di messaggistica unificata esistente, quindi creare un altro operatore automatico con il nome desiderato. Se nell'organizzazione vengono utilizzati più operatori automatici di messaggistica unificata, si consiglia di utilizzare nomi significativi per gli operatori automatici di messaggistica unificata. La lunghezza massima del nome di un operatore automatico di messaggistica unificata è di 64 caratteri e può contenere spazi.
        
        Anche se è possibile assegnare un nome un nuovo operatore automatico di messaggistica unificata per includere gli spazi, se è integrare la messaggistica unificata con Office Communications Server 2007 R2 o Microsoft Lync Server, il nome dell'operatore automatico non possono includere spazi. Di conseguenza, se è stato creato un operatore automatico con spazi nel nome visualizzato e si sta l'integrazione con Lync Server o Office Communications Server 2007 R2, è necessario innanzitutto eliminare tale operatore automatico e quindi creare un altro operatore automatico non include spazi nel nome visualizzato.
    
      - **Creare l'operatore automatico come abilitato**    Selezionare questa casella di controllo per abilitare l'operatore automatico di rispondere alle chiamate in arrivo al termine della messaggistica unificata automatico operatore Creazione guidata. Per impostazione predefinita, viene creato un nuovo operatore automatico come disabilitata.
        
        Se si decide di creare l'operatore automatico di messaggistica unificata come disabilitata, è possibile utilizzare EAC o Shell per abilitare l'operatore automatico dopo aver completato la procedura guidata.
    
      - **Imposta operatore automatico per rispondere ai comandi vocali**   Selezionare questa casella di controllo per abilitare l'operatore automatico di messaggistica unificata al servizio di sintesi vocale. In questo modo, i chiamanti possono rispondere mediante toni o input vocali ai prompt di sistema o ai prompt personalizzati utilizzati dall'operatore automatico di messaggistica unificata. Per impostazione predefinita, l'operatore automatico non è abilitato al servizio di sintesi vocale quando viene creato.
        
        Per i chiamanti per utilizzare un operatore automatico abilitato, è necessario installare il language pack appropriato alla messaggistica unificata che include il supporto di riconoscimento vocale automatico (ASR) e configurare le proprietà di operatore automatico per utilizzare questa lingua.
    
      - **Numeri di accesso**    Utilizzare questa casella per immettere i numeri di interno o numeri di telefono che i chiamanti verranno utilizzata per raggiungere l'operatore automatico. Digitare un numero di interno o numero di telefono nella casella e quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere il numero all'elenco. Il numero di cifre nel numero di interno o numero di telefono forniti non deve necessariamente corrispondere al numero di cifre per un numero di interno configurati nel dial plan di messaggistica unificata associato. Ciò avviene perché le chiamate dirette sono consentite per gli operatori automatici di messaggistica unificata.
        
        Il numero di numeri di interno o numeri di telefono immessi è un numero illimitato. Tuttavia, è possibile creare il nuovo operatore automatico di senza un numero di interno elencato. Un numero di interno o numero di telefono non è obbligatorio.
        
        È possibile modificare o rimuovere un numero interno esistente o un numero di telefono. Per modificare un numero interno esistente o un numero di telefono, fare clic su **Modifica**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere un numero interno esistente o un numero di telefono dall'elenco, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

4.  Fare clic su **Salva**.

## Utilizzo della Shell per creare un operatore automatico di messaggistica unificata

In questo esempio viene creato l'operatore automatico di messaggistica unificata denominato `MyUMAutoAttendant` in grado di accettare le chiamate in arrivo, ma non abilitato al servizio di sintesi vocale.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 55000 -Enabled $false

In questo esempio viene creato l'operatore automatico di messaggistica unificata abilitato al servizio di sintesi vocale denominato `MyUMAutoAttendant`.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true

