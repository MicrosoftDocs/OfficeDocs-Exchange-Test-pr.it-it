---
title: 'Identità del messaggio DSN: Exchange 2013 Help'
TOCTitle: Identità del messaggio DSN
ms:assetid: 70ffba22-e4fd-4cd3-98f5-8bfca2df89e4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998835(v=EXCHG.150)
ms:contentKeyID: 50480856
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Identità del messaggio DSN

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

È possibile identificare un messaggio di notifica sullo stato del recapito (DSN) personalizzato in base alla sua sintassi. L'identità è costituita dal GUID (Globally Unique Identifier, identificatore univoco globale) del messaggio DSN (Delivery Status Notification) personalizzato o da una stringa costituita dai seguenti valori:

  - **Impostazioni locali**   Questa variabile specifica le impostazioni locali della lingua in cui viene visualizzato il messaggio di notifica sullo stato del recapito. Per l'elenco dei codici delle impostazioni locali utilizzabili con il comando **New-SystemMessage**, vedere [Lingue supportate per i messaggi di sistema](supported-languages-for-system-messages-exchange-2013-help.md).

  - **Interno o esterno**   Questa variabile specifica se il messaggio DSN deve essere inviato solo ai mittenti che fanno parte dell'organizzazione Microsoft Exchange Server 2013 interna o anche a mittenti esterni all'organizzazione Exchange. Utilizzare l'opzione Interni per includere uno specifico contatto o risoluzione di posta elettronica nei messaggi DSN inviati ai mittenti interni, senza tuttavia fornire queste informazioni ai mittenti esterni all'organizzazione.

  - **Codice DSN**   Questa variabile specifica il codice DSN del messaggio di notifica personalizzato sullo stato del recapito.

La sintassi dell'identità del messaggio DSN è `<Locale>\<Internal or External>\<DSN code>`.

Per ciascun codice DSN è possibile creare più messaggi DSN personalizzati, che possono essere diretti a mittenti interni o esterni, con impostazioni locali diverse. Ad esempio, la seguente tabella fornisce alcune delle configurazioni possibili per il codice DSN 5.1.2 e le corrispondenti identità dei messaggi DSN.

### Configurazioni e identità DSN di esempio

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Configurazione DSN</th>
<th>Identità DSN</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Visualizza i messaggi DSN ai mittenti interni in lingua inglese</p></td>
<td><p>En\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Visualizza i messaggi DSN ai mittenti esterni in lingua inglese</p></td>
<td><p>En\External\5.1.2</p></td>
</tr>
<tr class="odd">
<td><p>Visualizza i messaggi DSN ai mittenti interni in lingua giapponese</p></td>
<td><p>Ja\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>Visualizza i messaggi DSN ai mittenti esterni in lingua giapponese</p></td>
<td><p>Ja\External\5.1.2</p></td>
</tr>
</tbody>
</table>

