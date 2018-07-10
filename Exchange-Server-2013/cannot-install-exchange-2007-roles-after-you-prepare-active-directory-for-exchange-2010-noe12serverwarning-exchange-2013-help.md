---
title: 'Impossibile installare i ruoli di Exchange 2007 dopo la preparazione di Active Directory per Exchange 2010_NoE12ServerWarning: Exchange 2013 Help'
TOCTitle: Impossibile installare i ruoli di Exchange 2007 dopo la preparazione di Active Directory per Exchange 2010_NoE12ServerWarning
ms:assetid: 4e579f69-0de9-421c-ba31-4e63a25e6a45
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.noe12serverwarning(v=EXCHG.150)
ms:contentKeyID: 50480646
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impossibile installare i ruoli di Exchange 2007 dopo la preparazione di Active Directory per Exchange 2010\_NoE12ServerWarning

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Quando si esegue Microsoft Exchange Server 2010**Setup /PrepareAD**, analizzatore di Microsoft Exchange Server esegue una query la topologia Active Directory esistente per determinare se esistono eventuali ruoli del server Microsoft Exchange Server 2007. Se non vengono rilevati i ruoli del server Exchange 2007, si riceve il messaggio di avviso seguenti:


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Il programma di installazione verrà per preparare l'organizzazione di Exchange Server 2010 tramite 'Setup /PrepareAD' e non sono stati rilevati ruoli nella topologia di Exchange Server 2007. Dopo l'operazione non sarà possibile installare i ruoli di Exchange Server 2007.</p></td>
</tr>
</tbody>
</table>


Prima di distribuire Exchange Server 2010, prendere in considerazione i fattori seguenti che potrebbero essere necessario distribuire un server Exchange 2007 con tutti i ruoli del server installati prima di distribuire Exchange 2007:

  - **Applicazioni sviluppate di terze parti o interne**   Le applicazioni sviluppate per Exchange 2003 potrebbero non essere compatibili con Exchange 2010 e pertanto devono essere aggiornati o sostituiti. È possibile gestire tali applicazioni e utenti associati di Exchange 2003; spostare in Exchange 2007, o si sostituisce il software con una versione compatibile per Exchange 2010.

  - **Requisiti di coesistenza o la migrazione**   Se si prevede di eseguire la migrazione delle cassette postali nell'organizzazione, è possibile distribuire Exchange 2007 e utilizzare Microsoft Transporter Suite, oppure utilizzare una soluzione di coesistenza o la migrazione di terze parti. Per scaricare Microsoft Transporter Suite, accedere a [Microsoft Transporter Suite](http://go.microsoft.com/fwlink/?linkid=82688) presso Microsoft Download Center.

Inoltre, quando si valutano le opzioni per l'organizzazione, assicurarsi di avere valutato gli aspetti seguenti:

  - Si dispone di una strategia sul posto per spostare le applicazioni dipendenti a Exchange 2010 prima Exchange 2003 raggiunga fine del supporto? Per ulteriori informazioni, visitare la pagina Web del ciclo di vita di supporto Microsoft ([https://go.microsoft.com/fwlink/?LinkID=55839](https://go.microsoft.com/fwlink/?linkid=55839)).

  - La strategia di richiede la coesistenza WebDAV e servizi Web (Exchange 2007 )?

  - Sono considerati prodotti di terze parti che supportano Exchange o altre tecnologie Microsoft che consentano di soddisfare i requisiti di migrazione o la coesistenza?

  - Che cos'è l'approccio del ciclo di vita dell'hardware (continuare a utilizzare tutti i server a 32 bit esistenti possibile confronto acquistare nuovi server a 64 bit)?

  - Che cos'è il piano di migrazione (migrazione il più presto rispetto alla migrazione di una strategia incrementale tutti i server). Analogamente, qual è la sequenza temporale per la coesistenza di versioni diverse di Exchange ?

Se si decide che è necessario distribuire un server Exchange 2007 prima di distribuire Exchange 2010, la distribuzione di un singolo Exchange 2007 con tutti i ruoli del server è sufficiente per consentire la distribuzione di server future Exchange 2007 nell'organizzazione. Per distribuire il server Exchange 2007 nell'organizzazione Exchange 2003, procedere come segue:

1.  Eseguire Exchange 2007**Setup /PrepareSchema**.

2.  Eseguire Exchange 2007**Setup /PrepareAD**.

3.  Eseguire Exchange 2007**Setup /PrepareDomain** in tutti i domini che contengono i destinatari, Exchange 2003 server o i cataloghi globali che potrebbero essere utilizzati da un server Exchange.

4.  Installare un server Exchange 2007 con tutti i ruoli del server quattro (Trasporto Hub, accesso Client, cassette postali e messaggistica unificata).

