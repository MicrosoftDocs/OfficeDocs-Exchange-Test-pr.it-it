---
title: 'Consente o meno risponditore autom. server Accesso Client: Exchange 2013 Help'
TOCTitle: Consentire o impedire risponditore automatico in un server Accesso Client
ms:assetid: 8287bb78-2621-4b80-a128-8f2ccd67923a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123529(v=EXCHG.150)
ms:contentKeyID: 50555629
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire o impedire risponditore automatico in un server Accesso Client

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-18_

È possibile abilitare il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange su un server Accesso client per rispondere alle nuove chiamate o, al contrario, per non consentire tale operazione. Per impostazione predefinita, il server Accesso client è abilitato dopo l'installazione. Quando si configura il server Accesso client per l'accettazione di chiamate vocali, fax, dell'operatore automatico e di Outlook Voice Access, viene utilizzato il cmdlet **Set-ServerComponentState**.

Configurando la modalità manutenzione per un server Accesso client, il server può essere messo fuori servizio. Un server Accesso client fuori servizio non accetterà chiamate in arrivo da gateway VoIP, sistemi IP PBX, PBX abilitati per SIP o session border controller (SBC).

In Exchange 2007 ed Exchange 2010 era presente un parametro di stato che poteva essere utilizzato per controllare lo stato funzionale di un server Messaggistica unificata. In Exchange 2013, il parametro 'status' è disponibile per tale finalità nel cmdlet **Set-UMCallRouterSettings** sul server Accesso client.


> [!IMPORTANT]
> Non è necessario aggiungere i server Accesso client e Cassette postali a un dial plan di messaggistica unificata prima che siano in grado di elaborare le chiamate per la messaggistica unificata, tranne quando si sta integrando la messaggistica unificata con Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. Per impostazione predefinita, tutti i server Accesso client e Cassette postali di un'organizzazione sono disponibili per rispondere alle chiamate in arrivo.



Per le attività di gestione aggiuntive relative ai server Accesso client, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni di configurazione del server Exchange" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare che il server Accesso client sia installato nello stesso computer del server Cassette postali o in un computer diverso.

  - Se il server Accesso client viene portato in modalità manutenzione, verificare che l'array del server sia sufficientemente integro da consentire al server di essere messo fuori servizio.

  - Prima di abbandonare la modalità manutenzione in un server, verificare l'integrità del server e assicurarsi che sia pronto ad essere di nuovo operativo.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Abilitazione o disabilitazione del risponditore automatico su un server Accesso client tramite Shell

In questo esempio, a un server Accesso client di `UMCallRouter-05x.contoso.com` viene consentito di rispondere alle chiamate vocali, fax, dell'operatore automatico e di Outlook Voice Access provenienti da gateway VoIP, sistemi IP PBX, PBX abilitati per SIP e SBC. La modifica viene riportata nel registro sul server UMCallRouter-05x.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

In questo esempio, a un server Accesso client di `UMCallRouter-05x.contoso.com` non viene consentito di rispondere alle chiamate vocali, fax, dell'operatore automatico e di Outlook Voice Access provenienti da gateway VoIP, sistemi IP PBX, PBX abilitati per SIP e SBC. La modifica viene riportata solo in Active Directory.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

