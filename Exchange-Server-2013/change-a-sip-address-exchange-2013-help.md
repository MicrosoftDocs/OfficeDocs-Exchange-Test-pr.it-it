---
title: 'Modificare un indirizzo SIP: Exchange 2013 Help'
TOCTitle: Modificare un indirizzo SIP
ms:assetid: 33f4f464-9baa-48af-bf5e-a0d55bb45f60
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335189(v=EXCHG.150)
ms:contentKeyID: 50555564
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare un indirizzo SIP

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-14_

Quando si abilita un utente alla messaggistica unificata e lo si collega ad un dial plan SIP URI, vengono creati due indirizzi proxy di messaggistica unificata di Exchange. Uno contiene il numero di interno dell'utente e l'altro contiene un indirizzo SIP per l'utente. Il numero di interno viene utilizzato quando l'utente chiama un numero di Outlook Voice Access.

I dial plan impostati su URI SIP e gli indirizzi SIP vengono utilizzati quando si effettua l'integrazione con la messaggistica unificata e Office Communications Server 2007 R2 o Microsoft Lync Server. L'indirizzo SIP viene utilizzato da Communications Server o Lync Server per instradare le chiamate in arrivo e inviare messaggi vocali all'utente. Per impostazione predefinita, l'indirizzo utilizzato dalla messaggistica unificata sarà l'indirizzo SIP utilizzato da Communications Server o Lync Server.

È possibile modificare l'indirizzo primario SIP che è stato aggiunto quando l'utente era abilitato alla messaggistica unificata o un indirizzo secondario SIP aggiunto successivamente, insieme agli indirizzi proxy di messaggistica unificata per l'utente. L'indirizzo primario SIP aggiunto quando l'utente era abilitato alla messaggistica unificata verrà riportato come indirizzo proxy primario della messaggistica unificata di Exchange. Qualsiasi altro indirizzo SIP secondario che si aggiunge verrà riportato come indirizzo proxy secondario di messaggistica unificata di Exchange. Quando vengono modificati indirizzi SIP secondari, i chiamanti possono lasciare messaggi vocali per l'utente agli endpoint SIP nei quali l'utente è registrato per utilizzare i nuovi indirizzi SIP- Tutti i messaggi vocali saranno inoltrati sulla cassetta postale dello stesso utente.

È possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per modificare un indirizzo SIP primario o secondario per un utente. È possibile utilizzare la pagina **Indirizzo di posta elettronica** sulla cassetta postale dell'utente nell'interfaccia di amministrazione di Exchange per modificare un indirizzo SIP primario o secondario. Non è possibile utilizzare la pagina **Cassetta postale di messaggistica unificata** nell'interfaccia di amministrazione di Exchange per modificare un indirizzo SIP primario o secondario.

È possibile visualizzare gli indirizzi SIP primari e secondari per un utente utilizzando il cmdlet **Get-UMMailbox** o il cmdlet **Get-Mailbox** in Shell.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata SIP URI prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, confermare che l'utente esistente sia stato abilitato per la messaggistica unificata e collegato al dial plan SIP URI. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Prima di eseguire queste procedure, confermare che l'indirizzo SIP che verrà assegnato all'utente sia valido e formattato correttamente.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Modifica di un indirizzo SIP primario o secondario tramite l'interfaccia di amministrazione di Exchange

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione elenco, selezionare la cassetta postale su cui si desidera modificare un indirizzo SIP, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Cassetta postale utente**, sotto **Indirizzo di posta elettronica**, selezionare l'indirizzo SIP che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). L'indirizzo SIP primario è riportato in lettere e numeri in grassetto.

4.  Nella pagina **Indirizzo di posta elettronica**, nella casella **Indirizzo/Estensione**, immettere il nuovo indirizzo SIP per l'utente, quindi fare clic su **OK**. Per selezionare un nuovo dial plan di messaggistica unificata, fare clic su **Sfoglia**.

5.  Fare clic su **Salva**.

## Modifica dell'indirizzo SIP primario o secondario tramite Shell

In questo esempio un indirizzo SIP viene modificato per Tony Smith.


> [!NOTE]
> Prima di modificare un indirizzo SIP utilizzando Shell, è necessario determinare la posizione dell'indirizzo proxy di messaggistica unificata di Exchange che si desidera modificare. Per determinare la posizione, utilizzare il comando <STRONG>$mbx.EmailAddresses</STRONG>. Il primo indirizzo proxy di messaggistica unificata di Exchange è l'indirizzo SIP predefinito (primario) e sarà 0 nell'elenco.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1)="eum:tsmith@contoso.com;phone-context=MySIPDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

