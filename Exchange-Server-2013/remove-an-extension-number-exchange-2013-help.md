---
title: 'Rimuovere un numero interno: Exchange 2013 Help'
TOCTitle: Rimuovere un numero interno
ms:assetid: c2b896cf-21f7-4453-a4e6-b23d236a6dd3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351124(v=EXCHG.150)
ms:contentKeyID: 50555677
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un numero interno

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-07-21_

Quando si abilita un utente alla messaggistica unificata e lo si collega al dial plan di un numero di interno, viene creato per l'utente un indirizzo proxy di messaggistica unificata di Exchange contenente il numero di interno dell'utente. È necessario definire almeno un numero di interno per la messaggistica unificata in modo tale che la posta vocale possa essere inviata alla cassetta postale dell'utente. Il numero di interno viene inoltre utilizzato quando l'utente chiama un numero di Outlook Voice Access.

È possibile rimuovere il numero di interno primario aggiunto quando l'utente è stato abilitato alla messaggistica unificata o un numero di interno secondario aggiunto in seguito insieme ai relativi indirizzi proxy di messaggistica unificata di Exchange per l'utente. Il numero di interno primario aggiunto quando l'utente è stato abilitato alla messaggistica unificata verrà elencato come indirizzo proxy di messaggistica unificata di Exchange primario. Ulteriori numeri di interni aggiunti verranno elencati come indirizzi proxy di messaggistica unificata di Exchange secondari. Quando viene rimosso un numero di interno, i chiamanti non possono più disporre della posta vocale per l'utente al numero di interno rimosso.

Se si rimuove il numero di interno primario, la messaggistica unificata non sarà in grado di inviare la posta vocale alla cassetta postale dell'utente e le regole di risposta alle chiamate non verranno elaborate. Una volta rimosso il numero di interno primario, l'indirizzo proxy di messaggistica unificata di Exchange dell'utente verrà elencato come **Null** nella cassetta postale dell'utente in EAC e quando si esegue il cmdlet **Get-Mailbox** in Shell. Inoltre, quando si esegue il cmdlet **Get-UMMailbox** cmdlet, i parametri *Extensions*, *PhoneNumber* e *CallAnsweringRulesExtensions* saranno vuoti o null.

È possibile utilizzare EAC o Shell per rimuovere un numero di interno primario o secondario. È possibile utilizzare la pagina **Indirizzo di posta elettronica** nella cassetta postale dell'utente in EAC per rimuovere un numero di interno primario o secondario. Non è possibile utilizzare la pagina **Cassetta postale di messaggistica unificata** in EAC per rimuovere un numero di interno primario ma è possibile utilizzarla per rimuovere un numero di interno secondario.

È possibile visualizzare i numeri di interno primario e secondario per un utente utilizzando il cmdlet **Get-UMMailbox** o **Get-Mailbox** in Shell.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata e collegata a un dial plan di un numero di interno telefonico. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che i numeri di interno primario e secondario siano configurati per l'utente.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Rimozione del numero di interno primario o secondario tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione elenco, selezionare la cassetta postale da cui rimuovere un numero di interno, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Cassetta postale utente**, sotto **Indirizzo di posta elettronica**, selezionare il numero di interno da rimuovere dall'elenco, quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina"). L'indirizzo proxy di messaggistica unificata di Exchange o il numero di interno viene indicato nell'elenco in lettere e numeri in grassetto.

4.  Fare clic su **Salva**.

## Rimozione di un numero di interno secondario tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione elenco selezionare l'utente di cui si desidera rimuovere un numero di interno dalla cassetta postale.

3.  Nel riquadro dei dettagli, sotto **Funzionalità telefoniche e vocali** \> **Messaggistica unificata** fare clic su **Visualizza dettagli**.

4.  Nella pagina **Altri interni**, nella casella **Numero di interno** selezionare il numero di interno che si desidera rimuovere, quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

5.  Fare clic su **Salva**.

## Rimozione di un numero di interno tramite Shell

Con questo esempio viene eliminato il numero di interno 12345 dalla cassetta postale di Tony Smith, un utente abilitato alla messaggistica unificata.


> [!NOTE]
> Prima di rimuovere un numero di interno tramite Shell, è necessario determinare la posizione dell'indirizzo proxy di messaggistica unificata di Exchange che si desidera modificare. Per determinare la posizione, utilizzare il comando <STRONG>$mbx.EmailAddresses</STRONG>. Il primo indirizzo proxy di messaggistica unificata di Exchange nell'elenco sarà 0.



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.remove("eum:22222;phone-context=MyDialPlan.contoso.com") 
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

