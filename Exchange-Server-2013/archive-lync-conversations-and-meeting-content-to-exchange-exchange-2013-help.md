---
title: 'Archiviare le conversazioni Lync e contenuto delle riunioni a Exchange: Exchange 2013 Help'
TOCTitle: Archiviare le conversazioni Lync e contenuto delle riunioni a Exchange
ms:assetid: 3cff970e-e5ed-4a54-88e6-3665d84b5ed7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn508399(v=EXCHG.150)
ms:contentKeyID: 59678843
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Archiviare le conversazioni Lync e contenuto delle riunioni a Exchange

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

È possibile archiviare contenuto Lync Online, ad esempio le conversazioni di messaggistica immediata, alla cassetta postale dell'utente in Exchange Online. Nelle distribuzioni in locale, è possibile archiviare contenuto Lync 2013 alle cassette postali Exchange 2013. In entrambi in linea e ambienti locali, richiede l'immissione di conservazione per controversia legale o an In-Place Hold nella cassetta postale dell'utente. Quando Lync contenuto viene eliminato definitivamente da un utente la cui cassetta postale è in attesa, Lync archiviato il contenuto viene mantenuto nella cartella elementi ripristinabili nella cassetta postale dell'utente. Non è visibile per gli utenti, ma è incluso in ricerche eDiscovery.

Quando si effettua una cassetta postale di conservazione per controversia legale, tutti i tipi di contenuto, inclusi gli elementi di Lync, vengono conservati. Per impostazione predefinita, questo è il caso quando si crea an In-Place Hold. Tuttavia, se si desidera utilizzare an In-Place Hold per conservare solo gli elementi di Lync, è possibile utilizzare l'opzione **selezionare tipi di messaggi** dalla procedura guidata **In-Place eDiscovery e conservazione** per selezionare **gli elementi di Lync**, come illustrato nella figura riportata di seguito.

![Archiviazione sul posto di elementi di Lync](images/Dn508399.691d2324-9fac-4689-8527-c78d387e0e3e(EXCHG.150).jpg "Archiviazione sul posto di elementi di Lync")


> [!NOTE]
> È inoltre possibile configurare an In-Place Hold per escludere gli elementi di Lync. Ad esempio, le organizzazioni preferibile conservare elementi della segreteria telefonica e messaggistica immediata per un periodo di tempo più breve rispetto ad altri tipi di contenuto. Per implementare questo tipo di criterio di conservazione, è necessario creare un'archiviazione sul posto per conservare il contenuto per un lungo periodo di tempo (ad esempio, 7 anni) ed escludere elementi Lync dall'esenzione. È quindi necessario creare un altro In-Place Hold con una durata di conservazione più breve che mantiene solo gli elementi di Lync. È inoltre possibile specificare per quanto tempo il contenuto deve essere mantenuto. Per ulteriori informazioni sulla creazione di un'esenzione con un determinato periodo di tempo, vedere <A href="in-place-hold-and-litigation-hold-exchange-2013-help.md">Archiviazione sul posto e conservazione per controversia legale</A>.



Vedere gli argomenti seguenti per istruzioni dettagliate per l'immissione di un utente in attesa:

  - [Creare o rimuovere un'archiviazione sul posto](create-or-remove-an-in-place-hold-exchange-2013-help.md)

  - [Conservazione in caso di dispute di una cassetta postale](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

Per altre attività di gestione relative all'archiviazione, vedere:

  - [Abilitare o disabilitare una cassetta postale di archiviazione in Exchange Online.](https://technet.microsoft.com/it-it/library/jj984357\(v=exchg.150\))

  - [Gestione degli archivi In Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

## Ulteriori informazioni

  - Archiviazione del contenuto Lync è disponibile nel server, indipendentemente se l'utente dispone di client Lync configurato alla [Salva conversazioni di messaggistica Istantanea di Lync nella cartella Cronologia conversazioni](https://go.microsoft.com/fwlink/p/?linkid=400589).

  - Archiviazione del contenuto Lync inizia dopo che l'utente viene inserito nella conservazione per controversia legale o archiviazione sul posto. Per garantire Lync dell'utente comunicazioni vengono archiviate dal momento in cui che viene creato il proprio account, mettere l'account in attesa subito dopo averlo creato.

Inoltre, nelle distribuzioni di Exchange 2013 e Lync 2013 locale:

  - È necessario configurare l'autenticazione OAuth tra Lync 2013 ed Exchange 2013. Per ulteriori informazioni, vedere [Integrazione con SharePoint e Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md).

  - È inoltre possibile archiviare Lync 2013 contenuto Exchange 2013 indipendentemente dal fatto che un utente viene messa in attesa. Questa operazione viene eseguita la configurazione dei criteri di archiviazione di Exchange dell'utente. Utilizzare il cmdlet `Set-CsUser` nel server Lync 2013 per impostare proprietà *ExchangeArchivingPolicy* dell'utente Lync su `ArchivingToExchange`.

  - Per ulteriori informazioni sull'archiviazione del contenuto Lync nelle distribuzioni in locale, vedere [Planning for Archiving](https://go.microsoft.com/fwlink/p/?linkid=400590) nella documentazione relativa a Lync 2013.

