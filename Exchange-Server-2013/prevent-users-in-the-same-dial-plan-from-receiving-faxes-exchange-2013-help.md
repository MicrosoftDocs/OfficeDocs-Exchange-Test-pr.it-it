---
title: 'Impedire agli utenti in stesso dial plan di ricevere fax: Exchange 2013 Help'
TOCTitle: Impedire agli utenti in stesso dial plan di ricevere fax
ms:assetid: 4fc66414-c950-4bca-ac20-4e489f288d06
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201688(v=EXCHG.150)
ms:contentKeyID: 52057248
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impedire agli utenti in stesso dial plan di ricevere fax

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

È possibile impedire che gli utenti abilitati alla messaggistica unificata associati a un dial plan di messaggistica unificata ricevano messaggi fax. Per impostazione predefinita, gli utenti abilitati alla messaggistica unificata associati a un dial plan di messaggistica unificata possono ricevere messaggi fax. Tuttavia, talvolta è necessario non consentire la ricezione dei fax agli utenti associati a uno specifico dial plan di messaggistica unificata.

Per impedire che degli utenti abilitati alla messaggistica unificata ricevano fax è possibile configurare il dial plan di messaggistica unificata, il criterio cassetta postale di messaggistica unificata o le cassette postali degli utenti. Se si disabilita il recapito dei messaggi fax in arrivo in un dial plan di messaggistica unificata, tutti gli utenti associati a quel dial plan non potranno più ricevere fax. L'abilitazione o la disabilitazione del servizio fax in un dial plan di messaggistica unificata ha la precedenza rispetto alle impostazioni dei singoli utenti abilitati alla messaggistica unificata.


> [!NOTE]
> È possibile utilizzare l'interfaccia di amministrazione di Exchange per configurare un criterio cassette postali di messaggistica unificata. Tuttavia, è necessario utilizzare Shell per configurare le impostazioni fax per i dial plan o per utenti singoli.



Per ulteriori informazioni sui partner fax, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Per altre attività di gestione relative alle operazioni fax, vedere [Fax procedure](faxing-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di Shell per impedire che gli utenti associati a un dial plan ricevano messaggi fax

In questo esempio viene mostrato come bloccare la ricezione di fax per gli utenti abilitati alla messaggistica unificata associati al dial plan di messaggistica unificata `MyUMDialPlan`.

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $false

