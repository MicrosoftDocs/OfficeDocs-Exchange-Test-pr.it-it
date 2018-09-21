---
title: 'Rimuovere una ricerca eDiscovery In locale: Exchange 2013 Help'
TOCTitle: Rimuovere una ricerca eDiscovery In locale
ms:assetid: 78461a78-1255-4a26-9d36-c6b8eb82a4f9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298078(v=EXCHG.150)
ms:contentKeyID: 50481004
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere una ricerca eDiscovery In locale

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-07-14_

In Microsoft Exchange Server 2013, è possibile utilizzare In-Place eDiscovery per la ricerca di contenuto delle cassette postali. È possibile rimuovere una ricerca eDiscovery In locale in qualsiasi momento. Quando si rimuove una ricerca eDiscovery In locale, i risultati della ricerca vengono rimossi dalla cassetta postale di individuazione.


> [!WARNING]
> Eliminazione di una ricerca eDiscovery In locale rimuoverà alcun risultato di ricerca copiati nella cassetta postale di individuazione.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2-5 minuti.

  - Per rimuovere una ricerca eDiscovery In locale con In-Place Hold abilitata, è necessario rimuovere In-Place Hold prima della ricerca. Per ulteriori informazioni, vedere [Creare o rimuovere un'archiviazione sul posto](https://docs.microsoft.com/it-it/exchange/security-and-compliance/create-or-remove-in-place-holds).

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "eDiscovery locale" nell'argomento[Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata

## Utilizzare EAC per rimuovere una ricerca eDiscovery In locale

1.  Accedere a **Gestione conformità** \> **eDiscovery e conservazione in locale**.

2.  Nella visualizzazione elenco, selezionare la ricerca di eDiscovery In locale che si desidera rimuovere e quindi fare clic su **Elimina**![Icona Elimina](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Icona Elimina").

## Utilizzo della Shell per rimuovere una ricerca eDiscovery In locale

Per un esempio di come rimuovere una ricerca eDiscovery In locale, vedere la sezione "Esempi" in [Remove-MailboxSearch](https://technet.microsoft.com/it-it/library/dd298130\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver rimosso correttamente una ricerca eDiscovery In locale, effettuare una delle operazioni seguenti:

  - Utilizzare EAC per verificare che la ricerca non è visualizzata nella visualizzazione elenco della scheda **In-place eDiscovery e conservazione**.

  - Utilizzare il cmdlet **Get-MailboxSearch** per recuperare le ricerche eDiscovery In locale. Per un esempio di come recuperare ricerche eDiscovery In locale, vedere la sezione "Esempi" in [Get-MailboxSearch](https://technet.microsoft.com/it-it/library/dd351021\(v=exchg.150\)).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


