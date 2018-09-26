---
title: 'Consente o meno risponditore auto. server cassette postali: Exchange 2013 Help'
TOCTitle: Consentire o impedire risponditore automatico in un server cassette postali
ms:assetid: 4b860c09-6669-4e3d-b3dc-17b8018b3860
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997908(v=EXCHG.150)
ms:contentKeyID: 50555584
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consentire o impedire risponditore automatico in un server cassette postali

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-18_

È possibile scegliere se permettere o meno al servizio di messaggistica unificata di Microsoft Exchange su un server Cassette postali di rispondere alle nuove chiamate. Per impostazione predefinita, un server Cassette postali è abilitato dopo l'installazione. Per impostare il server Cassette postali affinché accetti le chiamate vocali, fax, tramite operatore automatico e Outlook Voice Access in ingresso, utilizzare il cmdlet **Set-ServerComponentState**.

La configurazione della modalità di manutenzione per un server Cassette postali consente di "mettere fuori servizio" il server. Nel caso di un server Cassette postali, "fuori servizio" significa che il server non ospita database attivi, tutte le sue code di trasporto sono vuote e il server non accetta chiamate in ingresso provenienti da server Accesso client, gateway VoIP, IP PBX, PBX abilitati per SIP o session border controller.

In Exchange 2007 e Exchange 2010, era disponibile un parametro di stato che consentiva di controllare lo stato operativo del server Messaggistica unificata. In Exchange 2013, nel cmdlet **Set-UMService** non ci sono parametri di stato disponibili a questo scopo per i server Cassette postali.


> [!IMPORTANT]
> Non è necessario che i server Accesso client e Cassette postali vengano aggiunti a un dial plan di messaggistica unificata prima di poter elaborare le chiamate per la messaggistica unificata, a meno che non si stia integrando la messaggistica unificata e Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. Per impostazione predefinita, tutti i server Accesso client e Cassette postali nell'organizzazione sono disponibili per rispondere alle chiamate.



Per informazioni sulle altre attività di gestione relative ai server Cassette postali, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni di configurazione del server Exchange" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare che il server Cassette postali sia installato sullo stesso computer del server Accesso client o su un altro computer.

  - Se si sta attivando la modalità di manutenzione su un server Cassette postali, verificare che la ridondanza disponibile sia sufficiente per tutte le copie del database così da permettere al server di andare "fuori servizio".

  - Prima di far uscire un server dalla modalità di manutenzione, verificarne l'integrità e controllare che sia pronto per tornare in servizio.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Attivazione o disattivazione della ricezione chiamata su un server Cassette postali tramite Shell

In questo esempio, al server Cassette postali `UMMBXr-05x.contoso.com` viene consentito di rispondere alle chiamate vocali, fax, tramite operatore automatico e Outlook Voice Access in ingresso provenienti da gateway VoIP, IP PBX, PBX abilitati per SIP e session border controller e gli viene permesso di scrivere le modifiche nel Registro di sistema sul server UMMBX-05x.
```powershell
    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Active -LocalOnly
```

In questo esempio, al server Cassette postali `UMMBX-05x.contoso.com` viene impedito di rispondere alle chiamate vocali, fax, tramite operatore automatico e Outlook Voice Access in ingresso provenienti da gateway VoIP, IP PBX, PBX abilitati per SIP e session border controller e gli viene permesso di scrivere le modifiche solo in Active Directory.
```powershell
    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly
```
