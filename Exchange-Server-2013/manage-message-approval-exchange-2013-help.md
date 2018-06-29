---
title: 'Gestione approvazione del messaggio: Exchange 2013 Help'
TOCTitle: Gestione approvazione del messaggio
ms:assetid: 43a89f71-8002-4cb0-b3c8-1c2b2597f227
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd297936(v=EXCHG.150)
ms:contentKeyID: 50480518
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestione approvazione del messaggio

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-05-04_

Talvolta è opportuno avere un secondo insieme di infrarouges in un messaggio prima che il messaggio viene recapitato. Amministratore Exchange, è possibile impostare questo. Questo processo è noto come *moderazione*e al responsabile approvazione viene chiamato *moderatore*. In base al quali i messaggi necessaria l'approvazione, è possibile utilizzare uno dei due approcci:

  - Modificare le proprietà del gruppo di distribuzione

  - Creare una regola di flusso di posta elettronica

In questo articolo viene descritto:

  - Come stabilire l'approccio approvazione da utilizzare

  - Come funziona il processo di approvazione

Per informazioni su come implementare scenari comuni, vedere [Scenari comuni di approvazione messaggio](common-message-approval-scenarios-exchange-2013-help.md).

## Come stabilire l'approccio approvazione da utilizzare

Ecco un confronto tra i due approcci per l'approvazione del messaggio.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Operazione desiderata</th>
<th>Approccio</th>
<th>Primo passaggio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Creare un gruppo di distribuzione con moderatore in tutti i messaggi al gruppo devono essere approvati.</p></td>
<td><p>Impostare l'approvazione del messaggio al gruppo di distribuzione.</p></td>
<td><p>Accedere a Interfaccia di amministrazione di Exchange (EAC) &gt; <strong>destinatari</strong> &gt; <strong>gruppi</strong>, modificare il gruppo di distribuzione e quindi selezionare <strong>approvazione del messaggio</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Richiedere l'approvazione per i messaggi che soddisfano criteri specifici o che vengono inviati a una persona specifica.</p></td>
<td><p>Creare una regola di trasporto tramite l'azione <strong>Inoltra il messaggio per approvazione</strong>.</p>
<p>È possibile specificare criteri di messaggio, inclusi i destinatari, mittenti e modelli di testo. I criteri possono inoltre contenere eccezioni.</p></td>
<td><p>Accedere a EAC &gt; <strong>flusso di posta</strong> &gt; <strong>regole</strong>.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Come funziona il processo di approvazione

Quando si riceve un messaggio a un utente o gruppo che richiede l'approvazione, se si sta utilizzando Outlook Web Access, si è una notifica che potrebbe essere ritardato il messaggio.

![Messaggio di notifica di approvazione di un messaggio](images/Dd297936.80e2e5f1-0a1e-4c37-9076-794581155405(EXCHG.150).png "Messaggio di notifica di approvazione di un messaggio")

Moderatore riceve un messaggio di posta elettronica con una richiesta per approvare o rifiutare il messaggio. L'allegato include il messaggio originale per esaminare il testo del messaggio include pulsanti per approvare o rifiutare il messaggio.

![Messaggio di richiesta di approvazione, allegato incluso](images/Dd297936.bf517f5a-b10e-40df-a48a-403b395b5962(EXCHG.150).png "Messaggio di richiesta di approvazione, allegato incluso")

Moderatore può assumere uno dei tre azioni:

![Flusso di lavoro con opzioni per l'approvazione di un messaggio](images/Dd297936.dc7a6ca9-c67d-487a-8713-4d628e07f4b3(EXCHG.150).png "Flusso di lavoro con opzioni per l'approvazione di un messaggio")

1.  Se approvata, il messaggio viene inoltrata al destinatario originale. Non è una notifica al mittente originale.

2.  Se rifiutato, viene inviato un messaggio di rifiuto al mittente. Per aggiungere una spiegazione moderatore:
    
    ![Avviso di rifiuto, con commenti del moderatore](images/Dd297936.a663d36a-c67d-4155-b8f6-4b5dc8e105d9(EXCHG.150).png "Avviso di rifiuto, con commenti del moderatore")  

3.  Se il responsabile approvazione consente di eliminare o ignora il messaggio di approvazione, al mittente viene inviato un messaggio di scadenza. Ciò si verifica dopo due giorni di Exchange Online e dopo cinque giorni in Exchange Server 2013. (In Exchange Server 2013, è possibile modificare questo periodo di tempo).

Il messaggio è in attesa di approvazione temporaneamente archiviato in una *cassetta postale di arbitraggio*denominata cassetta postale di sistema. Fino a quando non moderatore decide di approvare o rifiutare il messaggio, Elimina il messaggio di approvazione o consente il messaggio di approvazione di scadenza, il messaggio originale viene mantenuto nella cassetta postale di arbitraggio.

Inizio pagina

## Domande e risposte

**Che cos'è la differenza tra il responsabile approvazione e il proprietario di un gruppo di distribuzione?**

Il proprietario di un gruppo di distribuzione è responsabile della gestione l'appartenenza al gruppo di distribuzione, ma non potrà potrebbero essere in grado di moderare i messaggi inviati a esso. Ad esempio, una persona in IT potrebbe essere il proprietario di un gruppo di distribuzione denominato tutti i dipendenti, ma solo il manager delle risorse umane potrebbe essere impostato come moderatore.

**Cosa succede quando il moderatore o responsabile approvazione invia un messaggio al gruppo di distribuzione?**

Il messaggio utilizza direttamente al gruppo, ignorando il processo di approvazione.

**Cosa succede quando un sottoinsieme dei destinatari richiede l'approvazione?**

È possibile inviare un messaggio a un gruppo di destinatari in un sottoinsieme dei destinatari richiede l'approvazione. Si consideri un messaggio inviato ai 12 destinatari, uno dei quali è un gruppo di distribuzione con moderatore. Il messaggio viene automaticamente divisa in due copie. Un messaggio viene recapitato immediatamente ai 11 destinatari che non richiedono l'approvazione e il secondo messaggio viene inviato al processo di approvazione per il gruppo di distribuzione con moderatore. Se un messaggio è destinato a più destinatari con moderatore, una copia separata del messaggio viene creata automaticamente per ciascun destinatario moderato e ogni copia passa attraverso il processo di approvazione appropriato.

**Se il gruppo di distribuzione contiene moderati destinatari che richiedono l'approvazione?**

Un gruppo di distribuzione può includere i destinatari con moderatore che richiedono l'approvazione. In questo caso, dopo l'approvazione, il messaggio al gruppo di distribuzione si verifica un processo di approvazione distinti per ciascun destinatario moderato è un membro del gruppo di distribuzione. È tuttavia possibile abilitare l'approvazione automatica dei membri del gruppo di distribuzione dopo l'approvazione il messaggio al gruppo di distribuzione con moderatore. A tale scopo, si utilizza il parametro *BypassNestedModerationEnabled* nel cmdlet [Set-DistributionGroup](https://technet.microsoft.com/it-it/library/bb124955\(v=exchg.150\)) .

**È il processo diverso se si dispone di un server di Exchange?**

Per impostazione predefinita, viene utilizzata una cassetta postale di arbitraggio per ogni organizzazione di Exchange. Se si dispone di server Exchange e necessitano di ulteriori cassette postali di arbitraggio di bilanciamento del carico, seguire le istruzioni per l'aggiunta di cassette postali di arbitraggio nel [Gestire e risolvere i problemi di approvazione del messaggio](manage-and-troubleshoot-message-approval-exchange-2013-help.md). Cassette postali di arbitraggio sono cassette postali di sistema e non richiedono una licenza di Exchange.


> [!NOTE]
> <STRONG>Se si dispone di Exchange&nbsp;2007:</STRONG> Microsoft Exchange Server 2007 non supporta i destinatari con moderatore. Se un messaggio inviato a un gruppo di distribuzione con moderatore è espanso in un server Trasporto Hub Exchange&nbsp;2007, il messaggio viene ignorato moderazione e viene recapitato a tutti i membri del gruppo di distribuzione. Se sono presenti server Trasporto Hub Exchange&nbsp;2007 nell'organizzazione di Exchange, è necessario designare un server cassette postali Exchange Server 2013 come server di espansione di gruppi di distribuzione con moderatore. Ciò assicura che tutti i messaggi inviati al gruppo di distribuzione sono con moderatore.



Inizio pagina

## Ulteriori informazioni

[Gestire le regole di flusso di posta elettronica](manage-mail-flow-rules-exchange-2013-help.md)

[Riferimento rapido a Exchange Management Shell per Exchange 2013](exchange-management-shell-quick-reference-for-exchange-2013-exchange-2013-help.md)

[Exchange Online PowerShell](https://technet.microsoft.com/it-it/library/jj200677\(v=exchg.150\))

