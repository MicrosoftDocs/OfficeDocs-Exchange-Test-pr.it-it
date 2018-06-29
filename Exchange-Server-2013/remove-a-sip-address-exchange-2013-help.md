---
title: 'Rimuovere un indirizzo SIP: Exchange 2013 Help'
TOCTitle: Rimuovere un indirizzo SIP
ms:assetid: eaaff0b0-7d85-4845-a7b8-ac22b42bc415
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ662761(v=EXCHG.150)
ms:contentKeyID: 50555706
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un indirizzo SIP

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-14_

Quando si abilita un utente alla messaggistica unificata e lo si collega a un dial plan URI SIP, vengono creati due indirizzi proxy di messaggistica unificata di Exchange. Uno contiene il numero di interno dell'utente e l'altro l'indirizzo SIP dell'utente. Il numero di interno viene utilizzato quando l'utente chiama un numero di Outlook Voice Access.

I dial plan URI SIP e gli indirizzi SIP vengono utilizzati quando si effettua l'integrazione della messaggistica unificata e di Office Communications Server 2007 R2 o Microsoft Lync Server. L'indirizzo SIP viene utilizzato da Communications Server o Lync Server per instradare le chiamate in arrivo e inviare la posta vocale all'utente. Per impostazione predefinita, l'indirizzo SIP utilizzato dalla messaggistica unificata sarà l'indirizzo SIP utilizzato da Communications Server o Lync Server.

È possibile rimuovere l'indirizzo SIP primario aggiunto quando l'utente è stato abilitato alla messaggistica unificata o un indirizzo SIP secondario aggiunto in seguito insieme all'indirizzo proxy di messaggistica unificata di Exchange per l'utente. L'indirizzo SIP primario aggiunto quando l'utente è stato abilitato alla messaggistica unificata verrà elencato come indirizzo proxy di messaggistica unificata di Exchange primario. Ulteriori indirizzi SIP aggiunti verranno elencati come indirizzi proxy di messaggistica unificata di Exchange secondari. Quando viene rimosso un indirizzo SIP, i chiamanti non possono più lasciare messaggi vocali per l'utente all'indirizzo SIP rimosso anche se l'utente ha eseguito l'accesso con l'indirizzo SIP assegnato all'utente in Communications Server o Lync Server.

Se si rimuove l'indirizzo SIP primario, la messaggistica unificata non sarà in grado di inviare la posta vocale alla cassetta postale dell'utente e le regole di risposta alle chiamate non verranno elaborate. Una volta rimosso l'indirizzo SIP primario, l'indirizzo proxy di messaggistica unificata di Exchange dell'utente verrà elencato come **Null** nella cassetta postale dell'utente in EAC e quando si esegue il cmdlet **Get-Mailbox** in Shell. Inoltre, quando si esegue il cmdlet **Get-UMMailbox** cmdlet, i parametri *Extensions*, *PhoneNumber* e *CallAnsweringRulesExtensions* saranno vuoti o null.

È possibile utilizzare EAC o Shell per rimuovere un indirizzo SIP primario o secondario. È possibile utilizzare la pagina **Indirizzo di posta elettronica** nella cassetta postale dell'utente in EAC per rimuovere un indirizzo SIP primario o secondario. Non è possibile utilizzare la pagina **Cassetta postale di messaggistica unificata** in EAC per rimuovere un indirizzo SIP primario o secondario.

È possibile visualizzare gli indirizzi SIP primario e secondario di un utente utilizzando il cmdlet **Get-UMMailbox** o **Get-Mailbox** in Shell.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata e collegata a un dial plan URI SIP. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che gli indirizzi SIP primario e secondario siano configurati per l'utente.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Rimozione dell'indirizzo SIP primario o secondario tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione elenco, selezionare la cassetta postale da cui rimuovere un indirizzo SIP, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Cassetta postale utente**, sotto **Indirizzo di posta elettronica**, selezionare l'indirizzo SIP da rimuovere dall'elenco, quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina"). L'indirizzo proxy di messaggistica unificata di Exchange o l'indirizzo SIP viene indicato nell'elenco in lettere e numeri in grassetto.

4.  Fare clic su **Salva**.

## Rimozione dell'indirizzo SIP primario o secondario tramite Shell

Con questo esempio viene rimosso l'indirizzo SIP tsmith@contoso.com dalla cassetta postale di Tony Smith, un utente abilitato alla messaggistica unificata.


> [!NOTE]
> Prima di rimuovere un indirizzo SIP tramite Shell, è necessario determinare la posizione dell'indirizzo proxy di messaggistica unificata di Exchange che si desidera modificare. Per determinare la posizione, utilizzare il comando <STRONG>$mbx.EmailAddresses</STRONG>. Il primo indirizzo proxy di messaggistica unificata di Exchange nell'elenco sarà 0.



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:tsmith@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

