---
title: 'Consenti agli utenti di stesso dial plan di ricevere fax: Exchange 2013 Help'
TOCTitle: Consenti agli utenti di stesso dial plan di ricevere fax
ms:assetid: cb245028-0b86-4171-879e-934dd35fa626
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124557(v=EXCHG.150)
ms:contentKeyID: 52057334
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consenti agli utenti di stesso dial plan di ricevere fax

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile consentire agli utenti collegati a un dial plan di messaggistica unificata di ricevere messaggi fax nelle loro cassette postali. Per impostazione predefinita, gli utenti abilitati alla messaggistica unificata collegati a un dial plan di messaggistica unificata possono ricevere messaggi fax. Per consentire agli utenti abilitati alla messaggistica unificata di ricevere messaggi fax nelle loro cassette postali, il dial plan deve essere configurato per accettare le chiamate fax in arrivo. È necessario, inoltre, abilitare la funzionalità fax nel criterio cassetta postale di messaggistica unificata e per l'utente. Per impostazione predefinita la funzionalità fax è abilitata nei dial plan, nei criteri cassetta postale di messaggistica unificata e per gli utenti. Talvolta, però, queste impostazioni vengono modificate e gli utenti abilitati alla messaggistica unificata non possono ricevere messaggi fax.

Se si impedisce la ricezione dei messaggi fax in un dial plan, tutti gli utenti associati a tale dial plan non saranno in grado di ricevere messaggi fax, anche se le proprietà di un singolo utente vengono modificate per consentirne la ricezione. L'abilitazione o la disabilitazione della funzionalità fax per un dial plan di messaggistica unificata ha la precedenza sulle impostazioni di un criterio cassetta postale di messaggistica unificata o di un singolo utente abilitato alla messaggistica unificata.


> [!NOTE]
> È possibile utilizzare EAC per configurare le impostazioni fax in un criterio cassetta postale di messaggistica unificata. Per configurare le impostazioni fax nei dial plan o per singoli utenti, è necessario utilizzare Shell.



Per ulteriori informazioni sui partner fax, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Per ulteriori attività di gestione relative all'invio e ricezione di fax, vedere [Fax procedure](faxing-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di Shell per consentire la ricezione di fax agli utenti collegati a un dial plan

In questo esempio si consente agli utenti abilitati alla messaggistica unificata collegati al dial plan di messaggistica unificata denominato `MyUMDialPlan` di ricevere fax in ingresso.

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $true

