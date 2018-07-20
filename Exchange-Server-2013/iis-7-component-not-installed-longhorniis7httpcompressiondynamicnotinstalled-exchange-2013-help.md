---
title: 'Componente di IIS 7 non installed_LonghornIIS7HttpCompressionDynamicNotInstalled: Exchange 2013 Help'
TOCTitle: Componente di IIS 7 non installed_LonghornIIS7HttpCompressionDynamicNotInstalled
ms:assetid: d909e329-2436-43f9-af75-a5ee14e67ebf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.longhorniis7httpcompressiondynamicnotinstalled(v=EXCHG.150)
ms:contentKeyID: 50481805
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Componente di IIS 7 non installed\_LonghornIIS7HttpCompressionDynamicNotInstalled

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2015-03-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Il programma di installazione di Microsoft Exchange Server 2010 o il programma di installazione di Microsoft Exchange Server 2007 non può installare il ruolo del Server accesso Client (CAS) o il ruolo del server cassette postali in un computer che esegue Microsoft Windows Server 2008 o in un computer basato su Windows Server 2008 R2 perché non sono installati i componenti necessari di Internet Information Server (IIS) 7.

Il programma di installazione di Exchange 2010 e installazione di Exchange 2007 richiedono che il computer basato su Windows Server 2008 o il computer basato su Windows Server 2008 R2 in cui si sta installando il ruolo del server accesso client già è installati i componenti seguenti di IIS 7.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Componenti IIS 7 per il ruolo del server accesso client</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Compressione del contenuto dinamico</p></td>
</tr>
<tr class="even">
<td><p>Compressione del contenuto statico</p></td>
</tr>
<tr class="odd">
<td><p>Autenticazione di base</p></td>
</tr>
<tr class="even">
<td><p>Autenticazione di Windows</p></td>
</tr>
<tr class="odd">
<td><p>Autenticazione del Digest 7 IIS</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>Mapping dei certificati client</p></td>
</tr>
<tr class="even">
<td><p>Esplorazione directory</p></td>
</tr>
<tr class="odd">
<td><p>Errori HTTP</p></td>
</tr>
<tr class="even">
<td><p>Registrazione HTTP</p></td>
</tr>
<tr class="odd">
<td><p>Reindirizzamento HTTP</p></td>
</tr>
<tr class="even">
<td><p>Funzionalità di traccia</p></td>
</tr>
<tr class="odd">
<td><p>Filtri ISAPI</p></td>
</tr>
<tr class="even">
<td><p>Monitor richieste</p></td>
</tr>
<tr class="odd">
<td><p>Contenuto statico</p></td>
</tr>
</tbody>
</table>


Il programma di installazione di Exchange 2010 e installazione di Exchange 2007 richiedono che il computer basato su Windows Server 2008 o il computer basato su Windows Server 2008 R2 in cui si sta installando il ruolo del server cassette postali già è installati i componenti seguenti di IIS 7.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Componenti IIS 7 per il ruolo del server cassette postali</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autenticazione di base</p></td>
</tr>
<tr class="even">
<td><p>Autenticazione di Windows</p></td>
</tr>
</tbody>
</table>


Per risolvere questo problema, attenersi alla procedura appropriata per installare i componenti di IIS 7 necessari nel computer di destinazione e quindi rieseguire il programma di installazione di Microsoft Exchange.

Installare i componenti di IIS 7 per il ruolo del server accesso client utilizzando Server Manager di Windows Server 2008

1.  Fare clic sul pulsante **Start**, scegliere **Strumenti di amministrazione** e quindi **Server Manager**.

2.  Nel riquadro di spostamento espandere **ruoli**, destro del mouse sul **Server Web (IIS)** e quindi fare clic su **Aggiungi servizi ruolo**.

3.  Nel riquadro **Selezione servizi ruolo**, scorrere verso il basso per **IIS**.

4.  Nell'area di **sicurezza**, fare clic per selezionare le caselle di controllo seguenti:
    
      - **Autenticazione di base**
    
      - **Autenticazione del digest**
    
      - **Autenticazione di Windows**

5.  Nell'area **delle prestazioni**, fare clic per selezionare le caselle di controllo seguenti:
    
      - **Compressione statica**
    
      - **Compressione dinamica**

6.  Nel riquadro **Selezione servizi ruolo** fare clic su **Avanti** e quindi fare clic su **Installa** nel riquadro **Conferma selezioni**.

7.  Fare clic su **Chiudi** per chiudere la procedura guidata Aggiunta servizi ruolo.

Installare i componenti di IIS 7 per il ruolo del server cassette postali utilizzando Server Manager di Windows Server 2008

1.  Fare clic sul pulsante **Start**, scegliere **Strumenti di amministrazione** e quindi **Server Manager**.

2.  Nel riquadro di spostamento espandere **ruoli**, destro del mouse sul **Server Web (IIS)** e quindi fare clic su **Aggiungi servizi ruolo**.

3.  Nel riquadro **Selezione servizi ruolo**, scorrere verso il basso per **IIS**.

4.  Nell'area di **sicurezza**, fare clic per selezionare le caselle di controllo seguenti:
    
      - **Autenticazione di base**
    
      - **Autenticazione di Windows**

5.  Nel riquadro **Selezione servizi ruolo** fare clic su **Avanti** e quindi fare clic su **Installa** nel riquadro **Conferma selezioni**.

6.  Fare clic su **Chiudi** per chiudere la procedura guidata Aggiunta servizi ruolo.

