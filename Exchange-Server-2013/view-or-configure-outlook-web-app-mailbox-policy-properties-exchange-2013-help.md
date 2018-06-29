---
title: 'Visualizzazione o configurazione delle proprietà dei criteri cassetta postale di Outlook Web App: Exchange 2013 Help'
TOCTitle: Visualizzazione o configurazione delle proprietà dei criteri cassetta postale di Outlook Web App
ms:assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351097(v=EXCHG.150)
ms:contentKeyID: 50481581
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzazione o configurazione delle proprietà dei criteri cassetta postale di Outlook Web App

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-04-13_

Dopo aver creato un criterio cassette postali di Outlook Web App, è possibile configurare numerose opzioni per controllare le funzionalità disponibili per gli utenti in Outlook Web App. Ad esempio, è possibile abilitare o disabilitare le regole di Posta in arrivo o creare un elenco di tipi di file consentiti per gli allegati.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di Outlook Web App" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per visualizzare o configurare i criteri cassetta postale di Outlook Web App

1.  In EAC, fare clic su **Autorizzazioni** \> **Criteri di Outlook Web App**.

2.  Nel riquadro di lavoro fare clic per selezionare il criterio cassetta postale che si desidera visualizzare o configurare.

3.  Fare clic sul pulsante **Modifica**.

4.  
    
    Nella scheda **Generale** è possibile visualizzare e modificare il nome del criterio.

5.  
    
    Nella scheda **Funzionalità** utilizzare le caselle di controllo per abilitare o disabilitare le funzionalità. Per impostazione predefinita sono visualizzate le funzionalità più comuni. Per vedere tutte le funzionalità che possono essere abilitate o disabilitate, fare clic su **Altre opzioni**.
    

    > [!NOTE]
    > Le impostazioni delle funzionalità per i criteri della cassetta postale Outlook Web App hanno precedenza sulle impostazioni della directory virtuale Outlook Web App. È possibile modificare le impostazioni di segmentazione per singoli utenti utilizzando il cmdlet <STRONG>Set-CASMailbox</STRONG> nella Shell.



6.  
    
    Nella scheda **Accesso ai File**, utilizzare le caselle di controllo di **accesso diretto ai file** per configurare l'accesso al file e opzioni di visualizzazione per gli utenti. Accesso ai file consente di aprire o visualizzare il contenuto del file allegati al messaggio di posta elettronica.
    
    L'accesso ai file può essere controllato valutando se un utente ha effettuato l'accesso su un computer pubblico o privato. L'opzione che consente agli utenti di selezionare l'accesso a computer privati o pubblici è disponibile solo quando si utilizza l'autenticazione basata su moduli. Tutte le altre forme di autenticazione corrispondono, per impostazione predefinita, all'accesso a un computer privato.

7.  Nella scheda **Accesso offline** utilizzare i pulsanti di opzione per configurare la disponibilità dell'accesso offline.

8.  Fare clic su **Salva** per aggiornare il criterio.

## Utilizzare la shell per configurare i criteri cassette postali di Outlook Web App

In questo esempio viene abilitato l'accesso al calendario nel criterio cassette postali predefinito.

    Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-OwaMailboxPolicy](https://technet.microsoft.com/it-it/library/dd297989\(v=exchg.150\)).

## Utilizzare la shell per visualizzare i criteri cassette postali di Outlook Web App

In questo esempio, vengono recuperate le proprietà del criterio cassetta postale di Outlook Web App`Executives` nell'organizzazione `Fabrikam`.

    Get-OwaMailboxPolicy -Identity Fabrikam\Executives

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-OwaMailboxPolicy](https://technet.microsoft.com/it-it/library/dd351095\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la modifica corretta di criterio cassetta postale di Outlook Web App:

1.  in Interfaccia di amministrazione di Exchange fare clic su **Autorizzazioni** \> **Criteri di Outlook Web App**, quindi scegliere un criterio cassetta postale di Outlook Web App specifico.

2.  Fare clic sul pulsante **Modifica** per visualizzare le proprietà del criterio cassetta postale.

3.  Fare clic su **Salva** o **Annulla** per chiudere la pagina delle proprietà.

