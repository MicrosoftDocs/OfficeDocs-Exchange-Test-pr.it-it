---
title: 'Opzioni di conversione TNEF: Exchange 2013 Help'
TOCTitle: Opzioni di conversione TNEF
ms:assetid: 989a62fc-4bc1-448f-90c8-7c7b56fe1084
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb310786(v=EXCHG.150)
ms:contentKeyID: 52057293
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Opzioni di conversione TNEF

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

È possibile specificare se Transport Neutral Encapsulation Format TNEF () devono essere conservati o rimossa dai messaggi che lasciano l'organizzazione Exchange. La codifica TNEF, nota anche come Outlook Rich Text Format o Exchange Rich Text Format è un Microsoft-formato specifico per l'incapsulamento proprietà del messaggio MAPI. Tutte le versioni di MicrosoftOutlook valutare la codifica TNEF. Outlook Web App Converte la codifica TNEF in MAPI e vengono visualizzati messaggi formattati. Tuttavia, altri client di posta elettronica che non supportano la codifica TNEF in genere visualizzato TNEF formattato messaggi come testo normale messaggi con allegati Winmail. dat o Win.

**Sommario**

Opzioni di conversione TNEF per il dominio remoto

Opzioni di conversione TNEF per gli utenti e i contatti di posta elettronica

Opzioni di conversione TNEF in Outlook

Ordine di precedenza per le opzioni di conversione TNEF

## Opzioni di conversione TNEF per il dominio remoto

Quando si configura opzioni di conversione TNEF per un dominio remoto, le opzioni di conversione TNEF vengono applicate a tutti i messaggi inviati a tale dominio.

  - Per Exchange Online Dedicated, utilizzare l'interfaccia di amministrazione di Exchange (EAC) per impostare le opzioni di conversione TNEF per un dominio remoto al **flusso di posta** \> **domini remoti** \> **Modifica** (![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica")) \> **Exchange utilizza il formato RTF**.

  - Per Exchange Online e Exchange 2013, utilizzare il parametro *TnefEnabled* nel cmdlet **Set-RemoteDomain** per impostare le opzioni di conversione TNEF per un dominio remoto.

Per i domini remoti nella propria organizzazione, sono disponibili le opzioni di configurazione seguenti per la conversione TNEF:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>In EAC</th>
<th>In Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utilizzare la codifica TNEF per tutti i messaggi inviati al dominio remoto.</p></td>
<td><p><strong>Always</strong></p></td>
<td><p><code>$true</code></p></td>
</tr>
<tr class="even">
<td><p>Non utilizzare mai TNEF per i messaggi inviati al dominio remoto.</p></td>
<td><p><strong>Never</strong></p></td>
<td><p><code>$false</code></p></td>
</tr>
<tr class="odd">
<td><p>Messaggi TNEF in modo specifico non sono consentiti o non consentiti per i destinatari nel dominio remoto. Se la codifica TNEF messaggi vengono inviati a destinatari compresi nel dominio remoto dipende dall'impostazione specifica il contatto di posta elettronica o un utente di posta elettronica o l'impostazione specificata in base al mittente in Outlook. Questo è il valore predefinito.</p></td>
<td><p><strong>Seguire le impostazioni utente</strong></p></td>
<td><p><code>$null</code> (vuoto)</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni sui domini remoti, vedere [Domini remoti](remote-domains-exchange-2013-help.md) o [Domini remoti in Exchange Online](https://technet.microsoft.com/it-it/library/jj966211\(v=exchg.150\)).

Inizio pagina

## Opzioni di conversione TNEF per gli utenti e i contatti di posta elettronica

Quando si configura opzioni di conversione TNEF per un contatto di posta elettronica o un utente di posta elettronica, le opzioni di conversione TNEF vengono applicate a tutti i messaggi inviati al destinatario specifico. Utilizzare il parametro *UseMapiRichTextFormat* sui cmdlet **Set-MailUser** e **Set-MailContact** per configurare le opzioni di conversione TNEF per gli utenti e i contatti di posta elettronica.

Per gli utenti e i contatti di posta elettronica all'interno dell'organizzazione, sono disponibili le opzioni di configurazione seguenti per la conversione TNEF:

  - **Sempre**   La codifica TNEF viene utilizzata per tutti i messaggi inviati al destinatario. Il valore corrispondente per il parametro *UseMapiRichTextFormat* è `Always`.

  - **Mai**   La codifica TNEF non viene mai utilizzata per i messaggi inviati al destinatario. Il valore corrispondente per il parametro *UseMapiRichTextFormat* è `Never`.

  - **Utilizzare le impostazioni predefinite**   Messaggi TNEF non sono in particolare consentiti o non consentiti per il contatto di posta elettronica utente o di posta elettronica. Se vengono inviati i messaggi TNEF per il destinatario dipende dall'impostazione specifica per il dominio remoto corrispondente o l'impostazione specificata in base al mittente in Outlook. Il valore corrispondente per il parametro *UseMapiRichTextFormat* è `UseDefaultSettings`. Questo è l'impostazione predefinita.

Inizio pagina

## Opzioni di conversione TNEF in Outlook

I mittenti possono controllare le opzioni di conversione predefinito messaggio TNEF per la codifica TNEF i messaggi inviati a tutti i destinatari esterni all'organizzazione di Exchange. Queste opzioni sono denominate le opzioni di *formato del messaggio Internet* . Le opzioni si applicano solo a destinatari remoti e non ai destinatari presenti nell'organizzazione di Exchange.


> [!NOTE]
> Le opzioni seguenti definiscono come sono gestiti i messaggi che contengono testo RTF di Outlook quando inviati a destinatari esterni. Se si utilizza il formato del messaggio HTML o in testo normale, queste impostazioni non sono valide.



Sono disponibili le seguenti opzioni di conversione TNEF in Outlook:

  - **Converti in formato HTML**   Si tratta dell'opzione predefinita. I messaggi TNEF inviati a destinatari remoti vengono convertiti in formato HTML. Eventuale formattazione nel messaggio strettamente dovrebbe essere simile al messaggio originale. I messaggi HTML codificata MIME sono supportati da molte, ma non tutti i client di posta elettronica.

  - **Conversione in formato testo normale**   I messaggi TNEF inviati a destinatari remoti vengono convertiti in testo normale. Eventuale formattazione nel messaggio vengono persa.

  - **Inviare utilizzando il formato RTF di Outlook**   Qualsiasi TNEF i messaggi inviati a destinatari remoti rimangono messaggi TNEF.

È possibile configurare queste opzioni nelle posizioni seguenti in Outlook:

  - **Outlook 2010 o Outlook 2013** **File** \> **Opzioni** \> **posta** \> **formato del messaggio**.   

  - **Outlook 2007** **Strumenti** \> **Opzioni** \> **Formato posta** \> **Formato Internet**.   

I mittenti è inoltre possono controllare le opzioni di conversione predefinito messaggio TNEF per la codifica TNEF i messaggi inviati a destinatari specifici esterni all'organizzazione di Exchange. Queste opzioni sono denominate opzioni *Formato messaggi destinatari Internet* . Le opzioni si applicano solo a destinatari remoti archiviati nella cartella Contatti e non ai destinatari presenti nell'organizzazione di Exchange. Sono disponibili le seguenti opzioni di conversione TNEF dei destinatari remoti nella cartella Contatti:

  - **Consentire a Outlook decidere il formato per l'invio**   Questo è l'impostazione predefinita. Questa impostazione impone Outlook per utilizzare l'opzione conversione TNEF specificato dal formato Internet predefinito. I possibili valori sono **Converti in formato HTML**, **convertire in formato testo normale** o **inviare utilizzando il formato RTF di Outlook**. Di conseguenza, il messaggio TNEF può essere sinistra come TNEF, conversione in HTML o convertito in testo normale. Se si desidera verificare che il messaggio TNEF rimane TNEF per il destinatario, è necessario modificare questa impostazione da **consentire a Outlook decidere il formato per l'invio** a **Invia nel formato RTF di Outlook**.

  - **Solo testo normale di invio**   Qualsiasi messaggio TNEF inviato al destinatario viene convertiti in testo normale. Eventuale formattazione nel messaggio vengono persa.

  - **Invia nel formato RTF di Outlook**   Qualsiasi TNEF i messaggi inviati a destinatari remoti rimangono messaggi TNEF.

È possibile configurare queste opzioni di un contatto nelle posizioni seguenti in Outlook:

  - **Outlook 2010 o Outlook 2013**   Aprire la scheda contatto, fare doppio clic su indirizzo di posta elettronica, fare clic sull'icona **Visualizza altre opzioni per interagire con questa persona** e selezionare **proprietà di Outlook**. Nella finestra di dialogo **Proprietà di posta elettronica** selezionare **Formato Internet**.

  - **Outlook 2007**   Aprire la scheda contatto, fare doppio clic sul campo **posta elettronica** e selezionare **Formato Internet**.

Inizio pagina

## Ordine di precedenza per le opzioni di conversione TNEF

Exchange utilizza l'ordine di precedenza come descritto di seguito per determinare le opzioni di conversione TNEF per i messaggi in uscita inviati a destinatari esterni all'organizzazione di Exchange:

1.  Impostazioni del dominio remoto

2.  Impostazioni dell'utente di posta o del contatto di posta

3.  Impostazioni di Outlook

Nell'elenco specifica l'ordine di precedenza dalla più elevato in ordine decrescente. L'impostazione TNEF del dominio remoto sostituisce le impostazioni di TNEF l'utente di posta elettronica contatto di posta elettronica o in Outlook. Si supponga, ad esempio, si invia un messaggio Rich Text in Outlook, ma il destinatario si trova in un dominio di cui l'impostazione del dominio remoto non consentire specificatamente messaggi con formattazione TNEF. Il messaggio inviato al destinatario è in testo normale o HTML, ma non la codifica TNEF.

Inoltre, Exchange mai invia messaggi di riepilogo Transport Neutral codifica formato (STNEF) a destinatari esterni. Solo la codifica TNEF messaggi possono essere inviati a destinatari esterni all'organizzazione di Exchange.

Inizio pagina

