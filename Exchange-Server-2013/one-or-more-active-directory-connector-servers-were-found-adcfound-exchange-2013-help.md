---
title: 'Uno o più server di Active Directory Connector sono state found_ADCFound: Exchange 2013 Help'
TOCTitle: Uno o più server di Active Directory Connector sono state found_ADCFound
ms:assetid: a874f51f-09a2-4a76-9695-d61fb1ee6c1c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.adcfound(v=EXCHG.150)
ms:contentKeyID: 50481390
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Uno o più server di Active Directory Connector sono state found\_ADCFound

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-15_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Non può continuare l'installazione di Microsoft Exchange Server 2007 ed Exchange Server 2010 perché uno o più connettori ADC (Active Directory) sono state trovate nell'ambiente corrente di Microsoft Exchange.

ADC replica gli oggetti da Exchange Server versione 5.5 al servizio directory Active Directory in un ambiente di Microsoft Exchange in modalità mista e non supportate da Exchange 2007 o Exchange 2010.

Rimozione di tutti i componenti di ADC richiede l'installazione di Exchange 2007 o Exchange 2010.

Per risolvere questo problema, rimuovere tutti i componenti di ADC e rieseguire il programma di installazione di Exchange 2007 o Exchange 2010.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Per rimuovere i componenti di Active Directory Connector</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Per disabilitare il servizio nel server in cui è in esecuzione il servizio ADC ADC, destro del mouse sul <strong>Computer locale</strong> sul desktop e quindi fare clic su <strong>Gestisci</strong>.</p></li>
<li><p>Espandere il nodo <strong>servizi e applicazioni</strong> e quindi fare clic sul nodo <strong>servizi</strong>.</p></li>
<li><p>Nel riquadro destro destro del mouse sul <strong>Connettore Microsoft Active Directory</strong> e quindi scegliere <strong>proprietà</strong>.</p></li>
<li><p>Modificare il <strong>tipo di avvio</strong> su <strong>disabilitato</strong>. Al successivo avvio del computer, il servizio ADC non verrà avviato.</p></li>
<li><p>Fare clic su <strong>Applica</strong> e quindi su <strong>OK</strong>.</p></li>
<li><p>Per disinstallare il servizio ADC, utilizzare l'installazione guidata di Active Directory nel CD di Microsoft Exchange Server 2003 o Microsoft Exchange 2000 Server. Aprire la cartella \ADC\I386. e fare doppio clic sul programma Setup.exe. Seguire le istruzioni per <strong>Rimuovere tutti</strong> i componenti di servizio ADC.</p>

> [!IMPORTANT]
> È necessario completare il passaggio 6 e <STRONG>Rimuovi tutto</STRONG> ADC componenti per risolvere questo problema. È sufficiente per disattivare il servizio ADC.


</li>
</ol></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su ADC, vedere gli articoli della Microsoft Knowledge Base seguenti:

  - 325300, "supporto WebCast: Introduzione al connettore di Active Directory" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325300](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=325300)).

  - 325221, "Webcast del supporto tecnico: Microsoft Advanced Active Directory Connector" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=325221](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=325221)).

  - 312632 "Come installare e configurare il connettore di Active Directory in Exchange 2000 Server" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=312632](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=312632)).

