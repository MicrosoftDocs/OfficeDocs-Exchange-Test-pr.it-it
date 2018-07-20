---
title: "Aggiornare l'organizzazione di Exchange quando cambia l'ora legale o il fuso orario: Exchange 2013 Help"
TOCTitle: Aggiornare l'organizzazione di Exchange quando cambia l'ora legale o il fuso orario
ms:assetid: 5b12615c-24cf-4f46-bf3c-2334dc734ef8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh530051(v=EXCHG.150)
ms:contentKeyID: 70076148
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Aggiornare l'organizzazione di Exchange quando cambia l'ora legale o il fuso orario

 

_**Si applica a:** Exchange Online, Exchange Server, Exchange Server 2010, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Se il paese o la regione dove risiedono l'organizzazione o alcuni degli utenti ha modificato il criterio di riconoscimento dell'ora legale (DST), o ha modificato lo spostamento dell'ora locale dall'ora UTC (Coordinated Universal Time), potrebbe essere necessario aggiornare Microsoft Windows, Microsoft Exchange, Microsoft Outlook, o altri programmi per gestire queste modifiche.

Per ulteriori informazioni sulle modifiche dell'ora legale nel mondo, inclusi i collegamenti, vedere [la Guida dell'ora legale di Microsoft e supporto tecnico](https://go.microsoft.com/fwlink/p/?linkid=99640). Inoltre, visitare il supporto per i siti Web dell'altri fornitori di software per verificare se richiedono eventuali aggiornamenti aggiuntivi.

Anche se il proprio fuso orario non è stato modificato, se si interagisce con altri computer o utenti in modo globale, il proprio computer deve essere in grado di eseguire accuratamente i calcoli di data e ora per eventi che si verificano ovunque nel mondo.

Installare gli aggiornamenti per il fuso orario al più presto possibile minimizza il numero di riunioni o appuntamenti programmati nel periodo di transizione tra il vecchio fuso orario e quello nuovo.

## Come eseguire l'operazione?

## Passaggio 1: Installare l'aggiornamento di Windows DST su tutti i computer client e desktop

Poiché il sistema di autenticazione di Office 365 viene aggiornato quando si modifica il fuso orario o l'ora legale, tutti i computer client di Office 365 devono essere aggiornati o si potrebbero verificare problemi di connettività.

  - Verificare che tutti i computer client e del desktop sono installato l'aggiornamento Windows dell'ora legale. Per ulteriori informazioni, vedere [come configurare dell'ora legale per i sistemi operativi Microsoft Windows](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=914387).

## Passaggio 2: Installare l'aggiornamento di Windows DST su tutti i server

1.  Aggiornare tutti i server locali con l'aggiornamento Windows DST.

2.  Se si sta eseguendo Office 365, aggiornare qualsiasi server che interagisce con il sistema di autenticazione di Office 365, quali DirSync o server AD FS. Questi server devono essere aggiornati per garantire i tempi di attività.

**Nota**   Se si sta aggiornando i cluster di server, assicurarsi di che eseguire il normale processo di aggiornamento i gruppi. Aggiornare prima il server passivo, il failover sul server passivo (che diventa attivo) e quindi aggiornare il server (ora passivo) precedentemente attivo. Per ulteriori informazioni su come aggiornare i cluster di server e i gruppi di server a elevata disponibilità, vedere Update Exchange Server Clusters and High Availability Servers e [come aggiornare i cluster di failover di Windows Server](https://support.microsoft.com/en-us/kb/174799).

## Passaggio 3: Aggiornamento Exchange e Outlook, se necessario, nei computer client e del desktop

1.  Se gli utenti utilizzano Outlook 2007 o client precedenti, determinare quali gli strumenti di fuso orario Exchange o Outlook per l'esecuzione, tramite la tabella di eseguire la procedura seguente.

2.  Inviare un messaggio agli utenti per i quali è necessario aggiornare i computer fornendo loro un collegamento allo strumento appropriato.

Nella tabella seguente quando gli utenti devono eseguire [Strumento di aggiornamento del calendario di Exchange](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879) o [Strumento di aggiornamento dei dati di fuso orario per Microsoft Office Outlook](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667). Individuare quale versione dei server dell'organizzazione siano in esecuzione e quindi determinare quali programmi client degli utenti sono in esecuzione.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>Versione del client</strong></p></td>
<td> </td>
</tr>
<tr class="even">
<td><p><strong>Versione dell'organizzazione</strong></p></td>
<td><p><strong>Outlook 2003 o Outlook 2007</strong></p></td>
<td><p><strong>Outlook 2010</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2003 locale</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Strumento di calendario di Exchange</a> o</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Aggiornare i dati del fuso orario strumento per Microsoft Office Outlook</a></p></td>
<td><p>Nessuna operazione richiesta</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2007 locale</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Strumento di calendario di Exchange</a> o</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Aggiornare i dati del fuso orario strumento per Microsoft Office Outlook</a></p></td>
<td><p>Nessuna operazione richiesta</p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2010 locale</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Strumento di calendario di Exchange</a> o</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Aggiornare i dati del fuso orario dello strumento di Microsoft Office Outlook</a></p></td>
<td><p>Nessuna operazione richiesta</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2013 in locale</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Aggiornare i dati del fuso orario dello strumento di Microsoft Office Outlook</a></p></td>
<td><p>Nessuna operazione richiesta</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPOS-S (Exchange 2007)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Aggiornare i dati del fuso orario dello strumento di Microsoft Office Outlook</a></p></td>
<td><p>Nessuna operazione richiesta</p></td>
</tr>
<tr class="even">
<td><p><strong>BPOS-S (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Aggiornare i dati del fuso orario dello strumento di Microsoft Office Outlook</a></p></td>
<td><p>Nessuna operazione richiesta</p></td>
</tr>
<tr class="odd">
<td><p><strong>Office 365 (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Aggiornare i dati del fuso orario dello strumento di Microsoft Office Outlook</a> (non è supportata con Outlook 2003)</p></td>
<td><p>Nessuna operazione richiesta</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 (Exchange 2013)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Aggiornare i dati del fuso orario dello strumento di Microsoft Office Outlook</a> (non è supportata con Outlook 2003)</p></td>
<td><p>Nessuna operazione richiesta</p></td>
</tr>
<tr class="odd">
<td> </td>
<td> </td>
<td> </td>
</tr>
</tbody>
</table>

