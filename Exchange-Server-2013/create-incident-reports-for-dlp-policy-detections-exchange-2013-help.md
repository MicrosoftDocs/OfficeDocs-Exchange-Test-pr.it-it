---
title: 'Crea rapp. operaz. non consentite rilevamenti criteri DLP: Exchange 2013 Help'
TOCTitle: Creare i rapporti operazioni non consentite per i rilevamenti di criteri DLP
ms:assetid: 8e807f94-384c-43f5-be6f-06c5587175a0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150534(v=EXCHG.150)
ms:contentKeyID: 50479760
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creare i rapporti operazioni non consentite per i rilevamenti di criteri DLP

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

In Exchange Server 2013, è possibile definire un'azione per creare un rapporto sull'incidente all'interno di un set di regole dei criteri DLP. Inoltre, è possibile indicare a cui inviare il report e si desidera procedere con il messaggio originale. Rapporto operazioni non consentite può contenere le informazioni seguenti.

## Contenuto di un report di gestione degli eventi imprevisti

L'azione **Genera rapporto operazioni non consentite** consente agli utenti di inviare segnalazioni di operazioni non consentite per una cassetta postale di gestione degli eventi imprevisti. Viene generato un singolo rapporto operazioni non consentito per ogni messaggio solo se l'azione **Genera rapporto operazioni non consentite** viene applicato all'interno di un criterio.

Di seguito è riportato un elenco completo dei nomi di riga nel modello di rapporto operazioni non consentite. Nella colonna formato viene descritto come riconoscere ogni campo del rapporto. Nella colonna campo facoltativo specifica quali campi potrebbero non essere del rapporto per ogni corrispondenza della regola. La colonna specifica DLP Mostra tutti i campi presenti in seguito a funzionalità DLP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Riga</strong> <strong>nome</strong></p></td>
<td><p><strong>Descrizione</strong></p></td>
<td><p><strong>Formato</strong></p></td>
<td><p><strong>Campo facoltativo</strong></p></td>
<td><p><strong>DLP specifico</strong></p></td>
</tr>
<tr class="even">
<td><p>Id messaggio</p></td>
<td><p>ID del messaggio originale inviato</p></td>
<td><p>Id messaggio: ID del messaggio</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Mittente</p></td>
<td><p>True mittente del messaggio originale</p></td>
<td><p>Mittente: Indirizzo del mittente di posta elettronica</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>Oggetto del messaggio originale</p></td>
<td><p>Oggetto: stringa soggetto di input dell'utente finale</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>Destinatario o ai destinatari del messaggio originale</p>
<p>Ogni riga conterrà solo un singolo destinatario e possono essere presenti fino a 10 destinatari visualizzati nel rapporto operazioni non consentite. Se sono presenti altri destinatari, alla riga successiva viene visualizzato il numero di destinatari rimanenti.</p></td>
<td><p>A: Indirizzo di posta elettronica del destinatario</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>Indirizzo di posta elettronica CC del messaggio originale. la riga è facoltativa</p>
<p>Ogni riga CC conterrà solo un unico indirizzo di posta elettronica CC e può essere presente solo un massimo di 10 indirizzi di posta elettronica CC visualizzati nel rapporto operazioni non consentite. Se sono presenti ulteriori indirizzi CC, la riga CC successiva verrà visualizzato il numero di indirizzi di posta elettronica CC rimanenti.</p></td>
<td><p>CC: Indirizzo di posta elettronica del destinatario CC</p></td>
<td><p>Facoltativo</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Ccn</p></td>
<td><p>Indirizzo di posta elettronica Ccn del messaggio originale. la riga è facoltativa</p>
<p>Ogni riga Ccn conterrà solo un unico indirizzo di posta elettronica Ccn e può essere presente solo fino a 10 indirizzi Ccn visualizzati nel rapporto operazioni non consentite. Se sono presenti altri indirizzi di posta elettronica Ccn, la seguente riga Ccn verrà visualizzato il numero di indirizzi di posta elettronica Ccn rimanenti.</p></td>
<td><p>Ccn: Indirizzo di posta elettronica del destinatario Ccn</p></td>
<td><p>Facoltativo</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Gravità</p></td>
<td><p>Gravità del riscontro regola; controllo Visualizza la gravità più alto se raggiunti più regole.</p></td>
<td><p>Gravità: Bassa, Media o avanzata</p></td>
<td><p>Facoltativo</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Sostituisci</p></td>
<td><p>Indica se è stato segnalato una sostituzione per il messaggio e la giustificazione di sostituzione se specificato.</p></td>
<td><p>Sostituzione: Sì, giustificazione: Information Worker di input stringa giustificazione</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Falsi positivi</p></td>
<td><p>Indica se il messaggio è stato segnalato un falso positivo.</p></td>
<td><p>Falsi positivi: Sì</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Classificazione dei dati</p></td>
<td><p>Classificazioni dei dati rilevati trovati nel messaggio originale. la riga è facoltativa.</p>
<p>Ogni riga di classificazione dei dati conterrà solo un singolo rilevato classificazione con il relativo livello di probabilità minima consigliata, probabilità e conteggio degli. Verrà visualizzato fino a 5 classificazioni rilevate nel rapporto operazioni non consentite. Se la classificazione rilevata era un'affinità, il valore di count non sono valide e non verranno visualizzato.</p></td>
<td><p>Classificazione dei dati: tipo di informazione sensibile, Count: istanze di informazioni riservate trovata nel messaggio confidenza: valore percentuale, probabilità minima consigliata: valore percentuale</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Frequenza di accessi al regola</p></td>
<td><p>Visualizza tutte le regole di frequenza di accessi al messaggio originale.</p>
<p>Include il nome della regola che è stato raggiunto il criterio DLP (facoltativo) che la regola in cui risiede azioni scritte sul messaggio per la regola, classification(s) dati sulla regola che ha causato la regola da sottoporre a hit e la definizione della regola.</p></td>
<td><p>Hit test regola: nome della regola, criterio DLP: nome del criterio DLP se applicabile, azione: singola azione, classificazione dei dati: tipo di informazioni riservate, definizione: definizione della regola, se applicabile</p></td>
<td><p>Obbligatorio</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>ID di corrispondenza</p></td>
<td><p>Visualizza la classificazione di dati corrispondente, il contenuto corrispondente esatto del messaggio e la dimostrazione primaria della corrispondenza di classificazione dei dati. la riga è facoltativa.</p></td>
<td><p>Dell'ID corrispondenti: tipo di informazioni riservate, valore: valore effettivo di dati riservati, contesto: testo tra i dati riservati nel messaggio</p></td>
<td><p>Facoltativo</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

[Visualizzare i report di rilevamento dei criteri DLP](view-dlp-policy-detection-reports-exchange-2013-help.md)

[Prevenzione della perdita di dati](https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

