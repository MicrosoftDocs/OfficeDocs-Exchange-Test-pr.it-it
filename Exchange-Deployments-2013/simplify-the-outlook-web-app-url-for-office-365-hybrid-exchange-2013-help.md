---
title: "Semplificazione dell'URL di Outlook Web App per la versione ibrida di Office 365: Exchange 2013 Help"
TOCTitle: Semplificazione dell'URL di Outlook Web App per la versione ibrida di Office 365
ms:assetid: 19449aee-3796-4298-90c6-c7579b8d2f7a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt791749(v=EXCHG.150)
ms:contentKeyID: 74259167
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Semplificazione dell'URL di Outlook Web App per la versione ibrida di Office 365

 

_<strong>Ultima modifica dell'argomento:</strong>2016-11-11_

Informazioni su come configurare un URL per Outlook sul Web (Outlook Web App) dedicato agli utenti della cassetta postale cloud in un ambiente ibrido.

La migrazione dalla versione locale di Exchange a da Office 365 è un'operazione complessa e delicata per l'impatto che può avere sull'esperienza degli utenti. Gli utenti necessitano di accesso continuo alle cassette postali, a prescindere da dove e quando viene spostata la cassetta postale. Considerando quanto appena detto, la passata coesistenza di Outlook sul Web (in precedenza noto come Outlook Web App) è molto importante.

Tenere presente la seguente situazione: un'azienda utilizza una distribuzione ibrida per spostare alcune cassette postali dalla versione locale di Exchange a Office 365. Il venerdì precedente al trasferimento, gli utenti hanno eseguito l'accesso alle loro cassette postali locali tramite l'URL https://mail.contoso.com/owa. Il lunedì successivo al trasferimento, quegli stessi utenti ricevono un errore quando provano ad accedere alle cassette postali con l'URL di prima.

Per consentire agli utenti interessati dal problema di connettersi alle cassette postali tramite Outlook sul Web, sono disponibili due opzioni:

  - **Comunicare agli utenti il nuovo URL (ad esempio, https://outlook.com/owa/contoso.com)**   I problemi di questa opzione sono i seguenti:
    
      - L'URL è complesso.
    
      - L'esperienza degli utenti interessati non è continuativa.

  - **Configurare l'impostazione TargetOWAUrl nella relazione organizzativa**   I problemi di questa opzione sono i seguenti:
    
      - L'endpoint delle cassette postali cloud è esterno, vale a dire che non si trova nel dominio previsto dagli utenti.
    
      - L'endpoint necessita del dominio nell'URL per distinguere tra Office 365 aziendale e le offerte per gli utenti di outlook.com.
    
      - L'endpoint genera avvisi di mancata corrispondenza del certificato che vengono visualizzati agli utenti.

Per evitare questi problemi agli utenti con cassette postali cloud, eseguire questa procedura:

1.  **Creare un record CNAME in DNS (ad esempio, cloudowa.contoso.com), che punti a mail.office365.com**
    
      - Assicurarsi di creare il record CNAME nel DNS interno ed esterno (pubblico), poiché gli utenti potrebbero connettersi usando connessioni Internet esterne o interne.
    
      - In questo esempio, il dominio contoso.com viene utilizzato nella richiesta (la parte cloudowa è stata rimossa). Ciò significa che non è necessario specificare il dominio nell'URL.

2.  **Configurare il reindirizzamento di Outlook sul Web nella relazione organizzativa locale**   A questo scopo, utilizzare la sintassi seguente in Exchange Management Shell nelle versioni locali di Exchange:
    
        Set-OrganizationRelationship -TargetOWAUrl http://<CNAME value>/owa
    
    Ad esempio, se il record CNAME creato al passaggio 1 è cloudowa.contoso.com, eseguire il comando seguente:
    
        Set-OrganizationRelationship -TargetOWAUrl http://cloudowa.contoso.com/owa
    
    **Note:** 
    
      - Utilizzare http invece di https.
    
      - Nella relazione organizzativa è necessario utilizzare il valore finale /owa. Tuttavia, l'utente non deve digitare /owa nell'URL.

## Più richieste di autenticazione

È possibile che gli utenti ricevano più richieste di autenticazione, a seconda di varie situazione:

  - Dove si connettono (connessioni Internet interne o esterne).

  - Se il computer è aggiunto o meno a un dominio.

  - Se si utilizza la federazione delle identità nella distribuzione ibrida.

La procedura di richiesta di autenticazione prevista è descritta nella tabella seguente:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Metodo di autenticazione</th>
<th>Client computer</th>
<th>Esperienza relativa alla richiesta di autenticazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Federazione delle identità</p></td>
<td><p>Connessione Internet interna</p></td>
<td><p>Singola richiesta</p></td>
</tr>
<tr class="even">
<td><p>Federazione delle identità</p></td>
<td><p>Connessione Internet esterna</p></td>
<td><p>Richiesta doppia</p></td>
</tr>
<tr class="odd">
<td><p>Nessuna federazione delle identità</p></td>
<td><p>Aggiunto a dominio (interno o esterno)</p></td>
<td><p>Richiesta doppia</p></td>
</tr>
<tr class="even">
<td><p>Con o senza federazione delle identità</p></td>
<td><p>Non aggiunto a dominio (interno o esterno)</p></td>
<td><p>Richiesta doppia</p></td>
</tr>
</tbody>
</table>


**Nota:**  La federazione delle identità prevede che l'endpoint di AD FS sia configurato nell'area Intranet di Internet Explorer, così come descritto nell'argomento <https://go.microsoft.com/fwlink/p/?linkid=834460>, e che AD FS sia configurato nel rispetto delle istruzioni generali di Office 365.

