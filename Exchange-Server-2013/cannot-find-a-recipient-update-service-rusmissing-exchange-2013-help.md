---
title: 'Non riesce a trovare un service_RUSMissing aggiornamento destinatari: Exchange 2013 Help'
TOCTitle: Non riesce a trovare un service_RUSMissing aggiornamento destinatari
ms:assetid: 920fbf51-d5e4-4ac6-869f-7f1c5d9a3024
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.rusmissing(v=EXCHG.150)
ms:contentKeyID: 50481207
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Non riesce a trovare un service\_RUSMissing aggiornamento destinatari

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2016-12-15_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Non può continuare l'installazione di Microsoft® Exchange Server 2007 o Exchange Server 2010 non è possibile trovare il servizio aggiornamento destinatari (RUS) responsabile per un dominio nell'organizzazione di Exchange esistente.

Richiede l'installazione di Microsoft Exchange che ogni dominio dell'organizzazione di Exchange esistente esista un'istanza del servizio aggiornamento destinatari.

Se un'istanza del servizio aggiornamento destinatari è manca per un dominio, nuovi oggetti utente creati nel dominio non riceverà gli indirizzi di posta elettronica inviati a loro.

Per risolvere questo problema, verificare che esista un'istanza del servizio aggiornamento destinatari per ogni dominio e creare un'istanza del servizio aggiornamento destinatari per i domini che non dispone di un e quindi rieseguire il programma di installazione di Microsoft Exchange.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Per creare un'istanza di servizio aggiornamento destinatari per un dominio</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Aprire il gestore di sistema di Exchange.</p></li>
<li><p>Espandere <strong>i destinatari</strong>.</p></li>
<li><p>Destro del mouse sul nodo <strong>Servizi aggiornamento destinatari</strong>, fare clic su <strong>Nuovo</strong> e quindi fare clic su <strong>Servizio aggiornamento destinatari</strong>.</p></li>
<li><p>Nella finestra nuovo oggetto, fare clic su <strong>Sfoglia</strong> per individuare il nome del dominio.</p></li>
<li><p>Selezionare il nome del dominio e quindi fare clic su <strong>OK</strong>.</p></li>
<li><p>Nella finestra nuovo oggetto, fare clic su <strong>Avanti</strong> e quindi <strong>Fine</strong>.</p></li>
</ol></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sul servizio aggiornamento destinatari, vedere gli articoli della Microsoft Knowledge Base seguenti:

  - "Come il servizio aggiornamento destinatari si applica criteri destinatario" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=328738](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=328738)).

  - "Come il servizio aggiornamento destinatari viene popolato elenchi indirizzi" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253828](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=253828)).

  - "Come verificare lo stato del servizio aggiornamento destinatari di Exchange" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=246127](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=246127)).

  - "Attività per il servizio aggiornamento destinatari di Exchange" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253770](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=253770)).

