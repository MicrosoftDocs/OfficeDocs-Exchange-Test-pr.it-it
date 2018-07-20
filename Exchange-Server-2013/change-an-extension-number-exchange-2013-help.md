---
title: 'Modificare un numero interno: Exchange 2013 Help'
TOCTitle: Modificare un numero interno
ms:assetid: ff22b366-3bfb-4bf7-9f11-62fba48f1caf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232208(v=EXCHG.150)
ms:contentKeyID: 50555714
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare un numero interno

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-14_

Quando si abilita un utente alla messaggistica unificata e lo si collega al dial plan di un numero di interno, viene creato per l'utente un indirizzo proxy di messaggistica unificata di Exchange contenente il numero di interno dell'utente. È necessario definire almeno un numero di interno per la messaggistica unificata in modo tale che la posta vocale possa essere inviata alla cassetta postale dell'utente. Il numero di interno viene inoltre utilizzato quando l'utente chiama un numero di Outlook Voice Access.

È possibile modificare il numero di interno primario aggiunto quando l'utente è stato abilitato alla messaggistica unificata o un numero di interno secondario aggiunto in seguito insieme ai relativi indirizzi proxy di messaggistica unificata di Exchange per l'utente. Il numero di interno primario aggiunto quando l'utente è stato abilitato alla messaggistica unificata verrà elencato come indirizzo proxy di messaggistica unificata di Exchange primario. Ulteriori numeri di interni secondari aggiunti verranno elencati come indirizzi proxy di messaggistica unificata di Exchange secondari. Una volta che i numeri di interno sono stati modificati, i chiamanti possono lasciare messaggi vocali per l'utente a tutti i nuovi numeri di interno impostati. Tutti i messaggi vocali saranno consegnati alla cassetta postale dello stesso utente.

È possibile utilizzare EAC o Shell per modificare un numero di interno primario o secondario per l'utente. È possibile utilizzare la pagina **Indirizzo di posta elettronica** nella cassetta postale dell'utente in EAC per modificare un numero di interno primario o secondario. Non è possibile utilizzare la pagina **Cassetta postale di messaggistica unificata** in EAC per modificare un numero di interno primario ma è possibile utilizzarla per modificare un numero di interno secondario. Se si desidera modificare un numero di interno secondario, è innanzitutto necessario rimuovere il numero di interno secondario esistente, quindi aggiungere il numero di interno secondario corretto per l'utente.

È possibile visualizzare i numeri di interno primario e secondario per un utente utilizzando il cmdlet **Get-UMMailbox** o **Get-Mailbox** in Shell.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire queste procedure, confermare la creazione del dial plan di messaggistica unificata dell'interno telefonico. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata e collegata a un dial plan di un numero di interno telefonico. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Prima di eseguire queste procedure, confermare che il numero di interno che verrà assegnato all'utente contenga il numero corretto di cifre impostato sul dial plan di messaggistica unificata.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Modifica del numero di interno primario o secondario tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione elenco, selezionare la cassetta postale per cui modificare un numero di interno, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Cassetta postale utente**, sotto **Indirizzo di posta elettronica**, selezionare il numero di interno da modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica"). Il numero di interno primario è elencato in lettere e numeri in grassetto.

4.  Dalla pagina **Indirizzo di posta elettronica** immettere il nuovo numero di interno per l'utente nella casella **Indirizzo/estensione**. Per selezionare un nuovo dial plan di messaggistica unificata, fare clic su **Sfoglia**.

5.  Fare clic su **Salva**.

## Modifica del numero di interno primario o secondario tramite Shell

Con questo esempio viene modificato il numero di interno in 22222 per l'utente abilitato alla messggistica unificata Tony Smith.


> [!NOTE]
> Prima di modificare un numero di interno tramite Shell, è necessario determinare la posizione dell'indirizzo proxy di messaggistica unificata di Exchange che si desidera modificare. Per determinare la posizione, utilizzare il comando <STRONG>$mbx.EmailAddresses</STRONG>. Il primo indirizzo di messaggistica unificata di Exchange è il numero di interno primario predefinito e sarà pari a 0 nell'elenco.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(0)="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

