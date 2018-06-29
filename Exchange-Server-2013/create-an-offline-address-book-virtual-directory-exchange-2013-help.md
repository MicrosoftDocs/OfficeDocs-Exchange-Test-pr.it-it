---
title: 'Creare una directory virtuale della Rubrica offline: Exchange 2013 Help'
TOCTitle: Creare una directory virtuale della Rubrica offline
ms:assetid: 2c70e21f-2b12-414a-9e8c-65634a767c72
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996917(v=EXCHG.150)
ms:contentKeyID: 50480313
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare una directory virtuale della Rubrica offline

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-16_

La directory virtuale della Rubrica offline è la distribuzione per la Rubrica offline. Per impostazione predefinita, quando si installa Microsoft Exchange Server 2013, viene creata una nuova directory virtuale denominata Rubrica offline nel sito Web interno predefinito in IIS (Internet Information Services). Se esistono utenti sul lato client che si connettono a Microsoft Outlook esternamente al firewall dell'organizzazione, è possibile aggiungere un sito Web esterno. In alternativa, quando viene eseguito il cmdlet **New-OABVirtualDirectory** in Shell, viene creata una nuova directory virtuale denominata Rubrica offline nel sito Web IIS predefinito sul server Exchange locale.

La creazione di una directory virtuale Rubrica offline non è un'attività comune. Exchange supporta una sola directory virtuale denominata Rubrica offline e l'utente può crearne una solo se si è verificato un problema con quella corrente e la precedente era stata rimossa.

Per altre attività di gestione relative alle rubriche offline, vedere [Procedure della Rubrica fuori rete](offline-address-book-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Prima di creare una directory virtuale della Rubrica offline, assicurarsi che gli utenti siano a conoscenza delle modifiche apportate. È possibile che il processo di download della Rubrica offline per gli utenti venga interrotto.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Rubriche offline" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Sul server Exchange locale è installato il ruolo Accesso client.

  - Esiste un sito Web predefinito IIS (ad esempio, /w3svc/1/root).

  - Non esiste ancora una directory virtuale denominata Rubrica offline.

  - Sebbene la distribuzione basata sul Web venga abilitata per impostazione predefinita e non richieda un'ulteriore configurazione, si consiglia di abilitare SSL (Secure Sockets Layer) per il punto di distribuzione della Rubrica offline.

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Creazione di una directory virtuale della Rubrica offline tramite Shell

Per creare una directory virtuale della Rubrica offline con tutte le impostazioni predefinite, è possibile eseguire il cmdlet **New-OABVirtualDirectory** senza alcun parametro. La seguente procedura consente la creazione di una directory virtuale della Rubrica offline con impostazioni personalizzate.


> [!NOTE]
> Quando si crea una directory virtuale della Rubrica offline, si consiglia di abilitare SSL.



In questo esempio viene creata una directory virtuale Rubrica offline sul server Accesso client denominato CASServer01 con SSL abilitata e un URL esterno.

    New-OABVirtualDirectory -Server CASServer01 -RequireSSL $true -ExternalURL "https://www.contoso.com/OAB"

Una volta creata la nuova directory virtuale della Rubrica offline, è necessario modificare le impostazioni di ogni Rubrica offline che utilizza la distribuzione basata sul Web per la riconnessione alla directory virtuale. Per ulteriori informazioni, vedere [Modificare la pianificazione di generazione della Rubrica offline](change-the-offline-address-book-generation-schedule-exchange-2013-help.md).

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-OabVirtualDirectory](https://technet.microsoft.com/it-it/library/bb123735\(v=exchg.150\)).

