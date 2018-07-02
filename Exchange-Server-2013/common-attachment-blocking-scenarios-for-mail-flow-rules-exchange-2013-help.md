---
title: 'Scenari comuni relativi al blocco degli allegati: Exchange 2013 Help'
TOCTitle: Scenari comuni relativi al blocco degli allegati
ms:assetid: 5c576439-d55b-4c7f-90ed-a7f72cbb16c2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn950026(v=EXCHG.150)
ms:contentKeyID: 65207683
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Scenari comuni relativi al blocco degli allegati

 

_**Si applica a:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-02-23_

L'organizzazione potrebbe richiedere che determinati tipi di messaggi vengano bloccati o rifiutati per soddisfare requisiti legali o di conformità o per implementare esigenze aziendali specifiche. Ecco alcuni esempi di scenari comuni per bloccare tutti gli allegati che è possibile impostare utilizzando le regole di trasporto in Exchange:

  -  
    Esempio 1: Bloccare i messaggi con allegati e comunicarlo al mittente

  -  
    Esempio 2: Informare i destinatari interessati quando viene bloccato un messaggio in ingresso

  -  
    Esempio 3: Modificare la riga dell'oggetto per le notifiche

  -  
    Esempio 4: Applicare una regola con un limite di tempo

Per ulteriori esempi che mostrano come bloccare allegati specifici, vedere:

  - [Utilizzare le regole di trasporto per esaminare messaggi con allegati](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013)

  - [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/it-it/library/jj919236\(v=exchg.150\)) (Exchange Online, Exchange Online Protection)

Il filtro antimalware include un Filtro tipi di allegato comuni. Nell'Interfaccia di amministrazione di Exchange (EAC), andare a **Protezione**, quindi fare clic su **Nuovo** (![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")) per aggiungere filtri. Nel portale Exchange Online passare a **Protezione**, quindi selezionare **Filtro antimalware**.

Per iniziare a implementare uno di questi scenari per bloccare determinati tipi di messaggio:

1.  Accedere a Interfaccia di amministrazione di Exchange.

2.  Andare a **Flusso di posta** \>**Regole**.

3.  Fare clic su **Nuovo** (![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")), quindi selezionare **Crea una nuova regola**.

4.  Nella casella **Nome**, specificare un nome per la regola, quindi fare clic su **Altre opzioni**.

5.  Selezionare le condizioni e le operazioni desiderate.

**Nota:**  Nell'interfaccia di amministrazione di Exchange, la dimensione dell'allegato più piccola che è possibile immettere è 1 kilobyte, che dovrebbe rilevare la maggior parte degli allegati. Tuttavia, se si desidera rilevare tutti gli allegati di qualsiasi dimensione possibile, è necessario usare PowerShell per regolare la dimensione dell'allegato a 1 byte dopo aver creato la regola nell''interfaccia di amministrazione di Exchange. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).Per informazioni su come usare Windows PowerShell per connettersi a Exchange Online, vedere [Connessione a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).Per informazioni su come usare Windows PowerShell per connettersi a Exchange Online Protection, vedere [Connessione a Exchange Online Exchange Online Protection PowerShell](https://go.microsoft.com/fwlink/p/?linkid=627290).

Sostituire *\<Rule Name\>* con il nome della regola esistente ed eseguire il seguente comando per impostare la dimensione dell'allegato su 1 byte:

    Set-TransportRule -Identity "<Rule Name>" -AttachmentSizeOver 1B

Dopo aver modificato la dimensione dell'allegato a 1 byte, il valore visualizzato per la regola nell'interfaccia di amministrazione di Exchange diventa **0,00 KB**.

## Esempio 1: Bloccare i messaggi con allegati e comunicarlo al mittente

Se non si desidera che le persone dell'organizzazione inviino o ricevano allegati, è possibile configurare una regola di trasporto per bloccare tutti i messaggi con allegati.

In questo esempio, tutti i messaggi inviati o ricevuti dall'organizzazione con allegati vengono bloccati.

![Regola che consente di bloccare tutti gli allegati](images/Dn950026.38094183-166f-4ba5-a9cf-242e7d0f4e04(EXCHG.150).png "Regola che consente di bloccare tutti gli allegati")

Se si vuole semplicemente bloccare il messaggio, è consigliabile interrompere l'elaborazione della regola dopo averla assegnata. Scorrere verso il basso nella finestra di dialogo della regola e selezionare la casella di controllo **Interrompi l'elaborazione di ulteriori regole**.

## Esempio 2: Informare i destinatari interessati quando viene bloccato un messaggio in ingresso

Se si desidera rifiutare un messaggio ma comunicando al destinatario che cosa è successo, è possibile utilizzare l'operazione **Invia una notifica al destinatario tramite messaggio**.

È possibile includere segnaposto nel messaggio di notifica in modo che includa informazioni sul messaggio originale. I segnaposto devono essere racchiusi tra due segni di percentuale (%%) e quando viene inviato il messaggio di notifica, i segnaposto vengono sostituiti con le informazioni del messaggio originale. È inoltre possibile utilizzare HTML di base come \<br\>, \<b\>, \<i\> e \<img\> nel messaggio.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Tipo di informazioni</strong></p></td>
<td><p><strong>Segnaposto</strong></p></td>
</tr>
<tr class="even">
<td><p>Il mittente del messaggio.</p></td>
<td><p>%%From%%</p></td>
</tr>
<tr class="odd">
<td><p>Destinatari elencati nella riga &quot;A&quot;.</p></td>
<td><p>%%To%%</p></td>
</tr>
<tr class="even">
<td><p>Destinatari elencati nella riga &quot;Cc&quot;.</p></td>
<td><p>%%Cc%%</p></td>
</tr>
<tr class="odd">
<td><p>Oggetto del messaggio originale.</p></td>
<td><p>%%Subject%%</p></td>
</tr>
<tr class="even">
<td><p>Intestazioni del messaggio originale. È simile all'elenco delle intestazioni in una notifica sullo stato del recapito (DSN) generata per il messaggio originale.</p></td>
<td><p>%%Headers%%</p></td>
</tr>
<tr class="odd">
<td><p>La data in cui è stato inviato il messaggio originale.</p></td>
<td><p>%%MessageDate%%</p></td>
</tr>
</tbody>
</table>


In questo esempio vengono bloccati tutti i messaggi contenenti allegati e inviati alle persone all'interno dell'organizzazione e il destinatario riceve una notifica.

![Regola che avvisa i destinatari quando viene bloccato un messaggio in ingresso](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Regola che avvisa i destinatari quando viene bloccato un messaggio in ingresso")

## Esempio 3: Modificare la riga dell'oggetto per le notifiche

Quando viene inviata una notifica al destinatario, la riga dell'oggetto è l'oggetto del messaggio originale. Se si desidera modificare l'oggetto in modo che sia più chiaro per il destinatario, è necessario utilizzare due regole di trasporto:

  - La prima regola aggiunge la parola "non recapitabile" all'inizio dell'oggetto di tutti i messaggi con allegati.

  - La seconda regola blocca il messaggio e invia un messaggio di notifica al mittente utilizzando il nuovo oggetto del messaggio originale.


> [!IMPORTANT]
> Le due regole devono avere condizioni identiche. Le regole vengono elaborate nell'ordine, in modo che la prima regola aggiunga la parola "non recapitabile" e la seconda regola blocchi il messaggio e informi il destinatario.



Ecco l'aspetto che dovrebbe avere la prima regola se si desidera aggiungere "non recapitabile" per l'oggetto:

![Regola che antepone Impossibile da recapitare ai messaggi con allegati](images/Dn950026.2552b0bd-c69d-48b4-9e69-267fcaf20e70(EXCHG.150).png "Regola che antepone Impossibile da recapitare ai messaggi con allegati")

E la seconda regola esegue il blocco e invia la notifica (la stessa regola dall'esempio 2):

![Regola che avvisa i destinatari quando viene bloccato un messaggio in ingresso](images/Dn950026.f9a14733-d68a-4528-a736-206325881c47(EXCHG.150).png "Regola che avvisa i destinatari quando viene bloccato un messaggio in ingresso")

## Esempio 4: Applicare una regola con un limite di tempo

Se si verifica un attacco malware, è possibile applicare una regola con un limite di tempo in modo da bloccare temporaneamente gli allegati. Ad esempio, la regola seguente contiene sia un giorno sia un'ora di inizio e fine:

![Regola che mostra un limite di tempo](images/Dn950026.bdc8c4d8-72fa-4c5b-97f2-5fe76d50e643(EXCHG.150).png "Regola che mostra un limite di tempo")

## Vedere anche


[Regole del flusso di posta o di trasporto](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)  


[Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\))  
[Regole del flusso di posta (regole di trasporto in Exchange Online Protection](https://technet.microsoft.com/it-it/library/dn271424\(v=exchg.150\))

