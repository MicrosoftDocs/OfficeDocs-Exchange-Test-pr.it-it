---
title: 'Impedire ai chiamanti senza un ID chiamante di lasciare un messaggio vocale: Exchange 2013 Help'
TOCTitle: Impedire ai chiamanti senza un ID chiamante di lasciare un messaggio vocale
ms:assetid: dd5dad32-2f69-4bf4-8ff0-545c413d395a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673571(v=EXCHG.150)
ms:contentKeyID: 50481858
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impedire ai chiamanti senza un ID chiamante di lasciare un messaggio vocale

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile consentire o impedire agli utenti abilitati alla messaggistica unificata di ricevere messaggi vocali da chiamanti anonimi. Per impostazione predefinita, gli utenti abilitati alla messaggistica unificata possono ricevere chiamate anonime che non contengono informazioni sull'ID chiamante.

Nella maggioranza dei casi, le chiamate ricevute da un server Exchange contengono un ID chiamante utilizzabile per determinare l'origine della chiamata in arrivo. Tuttavia, è possibile che le chiamate in arrivo non includano informazioni sull'ID chiamante per i seguenti motivi:

  - L'apparecchiatura telefonica dell'organizzazione è configurata per non includere informazioni sull'ID chiamante.

  - La chiamata in arrivo proviene da un cellulare o da un telefono esterno.

  - Il chiamante ha disabilitato l'ID chiamante sul proprio telefono.

Poiché il parametro *AnonymousCallersCanLeaveMessages* è abilitato per impostazione predefinita, gli utenti abilitati alla messaggistica unificata possono ricevere messaggi vocali anche se questi non includono le informazioni sull'ID chiamante. Se l'opzione *AnonymousCallersCanLeaveMessages* è disabilitata e un utente abilitato alla messaggistica unificata riceve una chiamata che non include un ID chiamate, la chiamata verrà identificata come anonima e l'utente abilitato alla messaggistica unificata non riceverà il messaggio vocale.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che la cassetta postale dell'utente sia stata abilitata alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Impedire la ricezione di messaggi vocali di chiamanti anonimi tramite Shell

In questo esempio viene mostrato come evitare che l'utente tonismith@contoso.com abilitato alla messaggistica unificata riceva messaggi vocali da chiamate che non contengono informazioni sull'ID chiamante.

    Set-UMMailbox -Identity tonysmith@contoso.com -AnonymousCallersCanLeaveMessages $false

