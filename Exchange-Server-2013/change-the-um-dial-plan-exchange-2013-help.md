---
title: 'Modificare il dial plan di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Modificare il dial plan di messaggistica unificata
ms:assetid: 4a6b6b6f-c61c-44e8-91dd-c5d28835f441
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633465(v=EXCHG.150)
ms:contentKeyID: 50480537
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare il dial plan di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-05_

Potrebbe essere necessario trasferire un utente abilitato per la messaggistica unificata in un altro dial plan di messaggistica unificata o modificare il dial plan associato a tale utente. Ad esempio, si potrebbe dover trasferire un utente abilitato per la messaggistica unificata dal dial plan impostato sull'interno al dial plan URI SIP.

Per modificare il dial plan di messaggistica unificata, sarà necessario disabilitare la messaggistica unificata per l'utente per abilitarla nuovamente nel nuovo dial plan di messaggistica unificata. Ciò avviene perché i diversi dial plan possono avere diversi requisiti e diverse impostazioni e, ad esempio, utilizzare valori con lunghezza diversa per l'interno o il tipo di URI. Ad esempio, per un dial plan impostato su URI SIP è necessario che a ciascuna cassetta postale abilitata per la messaggistica unificata sia assegnato un identificatore risorsa SIP, mentre questo non vale per i dial plan impostati sull'interno. Inoltre, ciascuna cassetta postale di messaggistica unificata contiene riferimenti sia al dial plan di messaggistica unificata che al criterio cassetta postale di messaggistica unificata. A sua volta, il criterio relativo alla cassetta postale di messaggistica unificata contiene riferimenti al dial plan. Se si modifica l'indirizzo proxy primario per un utente abilitato per la messaggistica unificata impostandolo in modo che punti a un altro dial plan, lo stato della cassetta postale di messaggistica unificata risulta incoerente.

Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che il destinatario Exchange sia abilitato alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Come eseguire l'operazione

## Passaggio 1: Creare il nuovo dial plan di messaggistica unificata


> [!IMPORTANT]
> Se si sta eseguendo la migrazione di utenti abilitati per la messaggistica unificata a Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server, è necessario innanzitutto creare un dial plan URI SIP.



Per istruzioni dettagliate, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

## Passaggio 2: Disabilitare la messaggistica unificata per l'utente

Per istruzioni dettagliate, vedere [Disabilitare la segreteria telefonica di un utente](disable-voice-mail-for-a-user-exchange-2013-help.md).

## Passaggio 3: Abilitare l'utente per la messaggistica unificata nel nuovo dial plan


> [!IMPORTANT]
> Se si esegue il trasferimento degli utenti in un ambiente con Office Communications Server 2007 R2 o Lync Server, è necessario assegnare anche un identificatore risorsa SIP all'utente quando questo viene abilitato per la messaggistica unificata. Inoltre, occorre selezionare il criterio cassetta postale di messaggistica unificata associato a un dial plan impostato su SIP.



Per istruzioni dettagliate, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

