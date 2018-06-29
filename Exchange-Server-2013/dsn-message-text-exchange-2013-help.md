---
title: 'Testo del messaggio DSN: Exchange 2013 Help'
TOCTitle: Testo del messaggio DSN
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 50481972
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Testo del messaggio DSN

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

È possibile includere il testo in un messaggio di notifica sullo stato del recapito (DSN, Delivery Status Notification) personalizzato in Microsoft Exchange Server 2013 e formattare il testo in HTML.

È possibile includere nel messaggio DSN qualsiasi informazione visualizzabile dal destinatario. Ad esempio, è possibile includere una descrizione dettagliata della notifica sullo stato del recapito, informazioni relative al contatto per il servizio di assistenza e un collegamento al sito Web del supporto tecnico dell'utente. Ciascun messaggio DSN può contenere un massimo di 512 caratteri.

Dato che i messaggi DSN possono essere visualizzati in formato HTML, è possibile incorporare i tag di formattazione nel testo del messaggio DSN. Ad esempio, per mettere in grassetto alcune parti del messaggio DSN, inserire il testo tra i tag HTML \<B\> e \</B\>. Nella seguente tabella vengono forniti alcuni esempi di tag HTML validi che possono essere utilizzati nel testo del messaggio DSN.

### Tag HTML validi per l'utilizzo nei messaggi DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag HTML</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;B&gt;</p></td>
<td><p>Inizio grassetto</p></td>
</tr>
<tr class="even">
<td><p>&lt;/B&gt;</p></td>
<td><p>Fine grassetto</p></td>
</tr>
<tr class="odd">
<td><p>&lt;A HREF=&quot;url&quot;&gt;</p></td>
<td><p>Inizio collegamento ipertestuale</p></td>
</tr>
<tr class="even">
<td><p>&lt;/A&gt;</p></td>
<td><p>Fine collegamento ipertestuale</p></td>
</tr>
<tr class="odd">
<td><p>&lt;BR&gt;</p></td>
<td><p>Interruzione collegamento</p></td>
</tr>
<tr class="even">
<td><p>&lt;EM&gt;</p></td>
<td><p>Inizio corsivo</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/EM&gt;</p></td>
<td><p>Fine corsivo</p></td>
</tr>
<tr class="even">
<td><p>&lt;P&gt;</p></td>
<td><p>Inizio paragrafo</p></td>
</tr>
<tr class="odd">
<td><p>&lt;/P&gt;</p></td>
<td><p>Fine paragrafo</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Per impostazione predefinita, Exchange invia messaggi DSN in formato HTML, tuttavia è possibile configurare Exchange per l'invio di messaggi DSN HTML a mittenti interni, esterni o entrambi. Per configurare questa funzionalità, modificare i parametri <EM>InternalDsnSendHtml</EM> e <EM>ExternalDsnSendHtml</EM> con il comando <STRONG>Set-TransportService</STRONG>.<BR>Se il parametro <EM>InternalDsnSendHtml</EM> è impostato su <CODE>$false</CODE>, Exchange eliminerà i tag HTML nei messaggi DSN inviati a mittenti interni. Se il parametro <EM>ExternalDsnSendHtml</EM> è impostato su <CODE>$false</CODE>, Exchange eliminerà i tag HTML nei messaggi DSN inviati a mittenti esterni.



I seguenti caratteri, utilizzati nel testo dei messaggi DSN, hanno significati speciali:

  - Simbolo "maggiore di" (\>)

  - Simbolo "minore di" (\<)

  - E commerciale (&)

  - Virgolette (")

Questi caratteri vengono utilizzati per determinare dove iniziano e finiscono i tag HTML e dove inizia e finisce il testo da visualizzare ai mittenti. Per visualizzare questi caratteri nei messaggi DSN, è necessario utilizzare i codici di escape nella tabella seguente.

Ad esempio, per visualizzare il messaggio `"Please contact the Help Desk at <1234>."`, è necessario aggiungere `"Please contact the Help Desk at &lt;1234&gt;." ` al testo del messaggio DSN.

### Codici di escape dei caratteri per il messaggio DSN

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Codice di escape</th>
<th>Carattere</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp;lt;</p></td>
<td><p>&lt;</p></td>
</tr>
<tr class="even">
<td><p>&amp;gt;</p></td>
<td><p>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>&amp;quot;</p></td>
<td><p>&quot;</p></td>
</tr>
<tr class="even">
<td><p>&amp;amp;</p></td>
<td><p>&amp;</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> Se nel testo del messaggio DSN viene incluso un tag HTML che contiene virgolette doppie ("), ad esempio <CODE>&lt;A HREF="url"&gt;</CODE>, è necessario utilizzare virgolette singole (') attorno all'intero testo del messaggio DSN. Se vengono utilizzate le virgolette doppie attorno all'intero testo del messaggio DSN e attorno a un tag HTML, viene visualizzato un messaggio di errore.


