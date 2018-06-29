---
title: 'Reimpostare un PIN della casella vocale: Exchange 2013 Help'
TOCTitle: Reimpostare un PIN della casella vocale
ms:assetid: bf07e6e7-01d2-4933-bff5-c615cc21a480
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124404(v=EXCHG.150)
ms:contentKeyID: 50555675
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.ResetUnifiedMessagingPinPropertyControl
ms.translationtype: MT
---

# Reimpostare un PIN della casella vocale

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

Quando un utente della posta vocale abilitato alla messaggistica unificata blocca la propria cassetta postale di Oulook Voice Access tentando di accedervi più volte mediante un PIN non corretto o dimenticando il proprio PIN, è possibile utilizzare le seguenti procedure per reimpostare il PIN dell'utente. Quando si reimposta il PIN di Outlook Voice Access di un utente, è possibile configurare la messaggistica unificata in modo da generare automaticamente un PIN oppure si può specificare manualmente il PIN. Il nuovo PIN viene inviato all'utente tramite posta elettronica. È possibile specificare le opzioni per il PIN aggiuntive come la richiesta all'utente di reimpostare il PIN al primo accesso. Gli utenti possono inoltre reimpostare il PIN di messaggistica unificata utilizzando Outlook o Outlook Web App.


> [!NOTE]
> Per accedere alle cassette postali abilitate alla messaggistica unificata, gli utenti di Outlook Voice Access devono utilizzare la composizione a toni, nota anche come multifrequenza (DTMF, Dual Tone Multi-Frequency). Il riconoscimento vocale non è disponibile per l'immissione del PIN.



Per ulteriori attività relative alla protezione del PIN di Outlook Voice Access, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Reimpostazione di un PIN di messaggistica unificata tramite EAC

1.  In EAC accedere a **Destinatari**. Nella visualizzazione elenco selezionare la cassetta postale utente che si desidera visualizzare.

2.  Nel riquadro dei dettagli, sotto **Funzionalità telefoniche e vocali** in **Messaggistica unificata** fare clic su **Visualizza dettagli**.

3.  Nella pagina **Cassetta postale di messaggistica unificata** sotto **Impostazioni della cassetta postale di messaggistica unificata** fare clic su **Reimposta PIN**.

4.  Nella pagina **Reimposta PIN della cassetta postale di messaggistica unificata** utilizzare le opzioni seguenti per reimpostare il PIN dell'utente abilitato alla messaggistica unificata:
    
      - **Genera automaticamente un PIN**   Utilizzare questa opzione per generare automaticamente il PIN usato dall'utente per poter accedere alla cassetta postale utilizzando Outlook Voice Access. Questa impostazione è abilitata per impostazione predefinita.
        
        Il PIN generato automaticamente verrà inviato in un messaggio di posta elettronica alla cassetta postale dell'utente. Dopo la ricezione del PIN e dopo l'accesso alla cassetta postale, verrà richiesto di modificare il PIN con un altro che sia più familiare.
        
        Outlook Web App e Microsoft Outlook consentono inoltre all'utente di reimpostare il proprio PIN. Il PIN viene generato automaticamente in base ai criteri per il PIN definiti dal criterio di messaggistica unificata associato alla cassetta postale dell'utente. Si consiglia di utilizzare la generazione automatica dei PIN per gli utenti Outlook Voice Access.
    
      - **Digita un PIN**   Utilizzare questa opzione per specificare manualmente un PIN per un utente di Outlook Voice Access. Per impostazione predefinita, questa impostazione è disabilitata.
        
        Se si specifica un PIN per un utente, il PIN verrà inviato in un messaggio di posta elettronica alla cassetta postale dell'utente. Dopo la ricezione del PIN e dopo l'accesso alla cassetta postale, è possibile modificare il PIN configurando le opzioni personali di Outlook Voice Access. Tuttavia, in Outlook Web App e Microsoft Outlook non è disponibile l'opzione per specificare manualmente un PIN.
    
      - **Richiedi all'utente di reimpostare il PIN al primo accesso**   Utilizzare questa casella di controllo per richiedere all'utente di reimpostare il PIN al primo accesso a Outlook Voice Access. Per impostazione predefinita, questa opzione è selezionata.
        
        Se si seleziona l'opzione di generazione automatica del PIN, è possibile abilitare questa opzione che richiede agli utenti di modificare il PIN quando accedono per la prima volta a Outlook Voice Access. Questa opzione aiuta a proteggere il PIN dell'utente.

5.  Fare clic su **Salva**.

## Reimpostazione di un PIN di messaggistica unificata tramite Shell

Con questo esempio il PIN della casella vocale di Tony Smith viene reimpostato su 1985848. Tuttavia, questo PIN dovrà essere modificato al primo accesso dell'utente a Outlook Voice Access.

    Set-UMMailboxPIN -Identity tonysmith@contoso.com -PIN 1985848 -PinExpired $true

