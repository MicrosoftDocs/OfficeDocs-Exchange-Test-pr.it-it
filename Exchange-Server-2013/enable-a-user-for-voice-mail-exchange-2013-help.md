---
title: 'Consentire a un utente per la segreteria telefonica: Exchange 2013 Help'
TOCTitle: Consentire a un utente per la segreteria telefonica
ms:assetid: ad027767-5e14-4cb1-9f8a-0791d9188db5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124147(v=EXCHG.150)
ms:contentKeyID: 50481384
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.EnableUnifiedMessagingWizardForm.EnableUnifiedMessagingWizardPage
ms.translationtype: MT
---

# Consentire a un utente per la segreteria telefonica

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

Quando si abilita un utente per la messaggistica unificata, all'utente viene applicato un insieme predefinito di proprietà e l'utente potrà utilizzare le funzionalità di posta vocale incluse con la messaggistica unificata. Dopo aver abilitato l'utente alla posta vocale, è possibile aggiungere un indirizzo SIP (Session Initiation Protocol) per l'utente se è stato assegnato a un criterio cassetta postale di messaggistica unificata collegato a un dial plan URI SIP. In alternativa è possibile aggiungere un numero E.164 all'utente se gli è stato assegnato un criterio cassetta postale di messaggistica unificata collegato a un dial plan E.164. In entrambi i casi l'utente deve disporre di un numero di interno configurato.

Un numero di interno è obbligatorio per ciascun utente associato a un interno telefonico, a un URI (Uniform Resource Identifier) SIP o a un dial plan E.164. Il numero di interno deve contenere il numero corretto di cifre, come specificato nel dial plan di messaggistica unificata per il criterio di messaggistica unificata.


> [!NOTE]
> È necessario aggiungere, rimuovere o modificare i numeri di interno per tutti gli utenti abilitati alla messaggistica unificata utilizzando EAC o Shell, anche se sono collegati a un URI SIP o a un dial plan E.164. Per aggiungere, rimuovere o modificare l'indirizzo SIP o i numeri E.164 per gli utenti, è necessario utilizzare Shell dal momento che le opzioni non sono disponibili in EAC.



Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per abilitare un utente alla posta vocale

1.  In Stima al completamento fare clic su **Destinatari**.

2.  Nella visualizzazione Elenco selezionare l'utente di cui si desidera abilitare la cassetta postale per la messaggistica unificata.

3.  Nel riquadro Dettagli sotto **Funzionalità telefono e vocali** fare clic su **Abilita**.

4.  Nella pagina **Abilita cassetta postale di messaggistica unificata**, fare clic sul pulsante **Sfoglia** accanto a **Criteri cassetta postale di messaggistica unificata**, individuare nell'elenco il criterio da assegnare all'utente, quindi fare clic su **OK**.

5.  Nella pagina **Abilita cassetta postale di messaggistica unificata** completare le seguenti caselle:
    
      - **Indirizzo SIP** o **Numero E.164**   Nella casella di testo **Indirizzo SIP** o **Numero E.164**, inserire l'indirizzo SIP o il numero E.164 per l'utente. Queste opzioni sono disponibili se l'utente abilitato per la messaggistica unificata è assegnato a un criterio cassetta postale di messaggistica unificata collegato a un URI SIP o a un dial plan E.164. Non è possibile aggiungere un indirizzo SIP o un numero E.164 per un utente associato al dial plan di un interno telefonico.
        
        Quando si assegna un utente a un criterio cassetta postale di messaggistica unificata collegato a un dial plan E.164 o URI SIP, è necessario immettere il numero di interno dell'utente, che lo utilizzerà per accedere alla propria cassetta postale tramite Outlook Voice Access. Il numero di cifre configurato in questa casella deve corrispondere al numero di cifre configurato sul dial plan URI SIP o E.164.
    
      - **Numero di interno**   Utilizzare questa casella di testo per immettere manualmente il numero di interno per l'utente che si sta abilitando alla messaggistica unificata.
        
        È necessario fornire un numero di interno valido per l'utente che contenga lo stesso numero di cifre specificato nel dial plan. È possibile inserire solo cifre da 1 a 20. Solitamente la lunghezza del numero di interno va da 3 a 7 cifre. Il numero di cifre nell'interno è impostato nel dial plan collegato al criterio cassetta postale di messaggistica unificata assegnato all'utente.
    
      - Sotto **Impostazioni PIN** completare quanto segue:
        
          - **Genera automaticamente PIN**   Fare clic su questo pulsante per generare automaticamente un PIN per l'utente abilitato alla messaggistica unificata da utilizzare per l'accesso alla casella vocale tramite Outlook Voice Access. È l'impostazione predefinita. Il PIN viene generato automaticamente in base ai criteri del PIN configurati nel criterio cassetta postale di messaggistica unificata assegnato all'utente. Utilizzando questa impostazione si protegge il PIN dell'utente. Il PIN viene inviato all'utente nel messaggio di benvenuto che riceve quando viene abilitato per la messaggistica unificata. Per impostazione predefinita, dovranno modificare questo PIN la prima volta che accedono alla loro cassetta postale per utilizzare la posta vocale.
        
          - **Digita un PIN**   Fare clic su questo pulsante per immettere un PIN che l'utente utilizzerà per accedere al sistema di caselle vocali. Il PIN deve essere conforme alle impostazioni del criterio del PIN configurate nel criterio cassetta postale di messaggistica unificata associato a questo utente abilitato alla messaggistica unificata. Ad esempio, se il criterio cassetta postale di messaggistica unificata è configurato per accettare solo PIN contenenti sette o più cifre, il PIN immesso in questa casella deve contenere almeno sette cifre.
        
          - **Richiedi all'utente di reimpostare il PIN al primo accesso**   Selezionare questa casella di testo per forzare la reimpostazione del PIN della casella vocale dell'utente quando questo accede al sistema di caselle vocali da un telefono utilizzando Outlook Voice Access per la prima volta. Verranno invitati a immettere un PIN che è più significativo per loro. Per motivi di sicurezza, è consigliabile richiedere agli utenti abilitati alla messaggistica unificata di modificare il loro PIN al primo accesso per evitare accessi non autorizzati ai loro dati e alla loro cartella Posta in arrivo. Questa casella di controllo è selezionata per impostazione predefinita.

6.  Esaminare le impostazioni nella pagina **Abilita cassetta postale di messaggistica unificata**. Fare clic su **Fine** per abilitare l'utente alla posta vocale. Fare clic su **Indietro** per modificare la configurazione.

## Utilizzo di Shell per abilitare in utente alla posta vocale

In questo esempio viene abilitata la messaggistica unificata nella cassetta postale di tonysmith@contoso.com, impostato il numero di interno su 51234, impostato il PIN per l'utente su 5643892 e assegnato l'utente a un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

In questo esempio viene abilitata la messaggistica unificata sulla cassetta postale di tonysmith@contoso.com, viene assegnato un utente a un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy` e vengono impostati il numero di interno, l'indirizzo SIP e il PIN per l'utente.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

