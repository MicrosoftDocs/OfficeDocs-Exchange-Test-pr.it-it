---
title: 'Utilizzare regole del flusso di posta per instradare le e-mail in base a un elenco di parole, frasi o motivi: Exchange 2013 Help'
TOCTitle: Utilizzare regole del flusso di posta per instradare le e-mail in base a un elenco di parole, frasi o motivi
ms:assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn951131(v=EXCHG.150)
ms:contentKeyID: 65210892
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilizzare regole del flusso di posta per instradare le e-mail in base a un elenco di parole, frasi o motivi

 

_**Si applica a:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-10-30_

Per consentire agli utenti di essere conformi ai criteri di posta elettronica dell'organizzazione, è possibile utilizzare le regole di trasporto di Exchange per determinare come vengono instradate le e-mail contenenti parole o motivi specifici. Per un breve elenco di parole o frasi, è possibile utilizzare l'Interfaccia di amministrazione di Exchange. Per un elenco più lungo, è consigliabile utilizzare il modulo Exchange affinché Windows PowerShell legga l'elenco da un file di testo.

  - Esempio 1: Utilizzare un breve elenco di parole inaccettabili

  - Esempio 2: Utilizzare un lungo elenco di parole inaccettabili

Se l'organizzazione utilizza Prevenzione della perdita di dati (DLP), vedere [Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md) per ulteriori opzioni per l'identificazione e l'instradamento dei messaggi di posta elettronica contenenti informazioni riservate.

## Esempio 1: Utilizzare un breve elenco di parole inaccettabili

Se l'elenco di parole o frasi è breve, è possibile creare una regola utilizzando l'Interfaccia di amministrazione di Exchange. Ad esempio, per assicurarsi che nessuno invii e-mail con parole non consentite o con errori ortografici nel nome dell'azienda, negli acronimi interni o nei nomi di prodotti, è possibile creare una regola che blocchi il messaggio e informi il mittente. Le parole, le frasi e i motivi non fanno distinzione tra maiuscole e minuscole.

In questo esempio vengono bloccati i messaggi con errori di battitura comuni.

![Regola che mostra il blocco di un messaggio basato su modelli di testo](images/Dn951131.a8489cbb-be59-4890-ae30-1431703eeb88(EXCHG.150).png "Regola che mostra il blocco di un messaggio basato su modelli di testo")

## Esempio 2: Utilizzare un lungo elenco di parole inaccettabili

Se l'elenco di parole, frasi o motivi è lungo, è possibile inserirli in un file di testo con ogni parola, frase o motivo su una riga. Utilizzare il modulo di Exchange affinché Windows PowerShell legga l'elenco di parole chiave in una variabile, crei una regola di trasporto e assegni la variabile con le parole chiave alla condizione della regola di trasporto. Ad esempio, lo script seguente prende un elenco di errori di ortografia da un file denominato misspelled\_companyname.csv.

    $keywords=Import-Content  .\misspelled_companyname.txt
    New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."

## Utilizzo di frasi e motivi nel file di testo

Il file di testo può contenere le espressioni regolari per i modelli. Queste espressioni non distinguono tra maiuscole e minuscole. Espressioni regolari comuni sono:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Espressione</strong></p></td>
<td><p><strong>Corrispondenze</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>Qualsiasi carattere</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>Qualsiasi carattere aggiuntivo</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>Qualsiasi cifra decimale</p></td>
</tr>
<tr class="odd">
<td><p>[<em>character_group</em>]</p></td>
<td><p>Qualsiasi carattere in <em>character_group</em>.</p></td>
</tr>
</tbody>
</table>


Ad esempio, questo file di testo contiene errori di ortografia comuni di Microsoft.

    [mn]sft
    [mn]icrosft
    [mn]icro soft
    [mn].crosoft

Per informazioni su come specificare criteri utilizzando espressioni regolari, vedere [Riferimenti sulle espressioni regolari](https://go.microsoft.com/fwlink/p/?linkid=532394).

