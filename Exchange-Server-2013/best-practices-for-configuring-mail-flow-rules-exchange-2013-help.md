---
title: 'Procedure consigliate per regole flusso di posta: Exchange 2013 Help'
TOCTitle: Procedure consigliate per la configurazione delle regole del flusso di posta
ms:assetid: abd863c3-c0ce-42f3-9470-a573adc3cbba
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn960147(v=EXCHG.150)
ms:contentKeyID: 65211642
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Procedure consigliate per la configurazione delle regole del flusso di posta

 

_**Si applica a:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Seguire queste procedure consigliate per le regole di trasporto di Exchange per evitare di riscontrare comuni errori di configurazione. Ogni procedura consigliata è collegata a un argomento con un esempio e istruzioni dettagliate.

## Verificare le regole

Per assicurarsi che non si verifichino imprevisti alla posta elettronica e per accertarsi di perseguire effettivamente gli scopi della regola relativi alla conformità e agli aspetti legali e aziendali, sottoporre a test la regola. Esistono molte opzioni e le regole possono interagire tra loro, quindi è importante testare i messaggi che si prevede che risponderanno alla regola e che non risponderanno alla regola se è stata creata una regola eccessivamente generale. Per informazioni su tutte le opzioni per il test delle regole, vedere [Testare una regola del flusso di posta elettronica](test-a-mail-flow-rule-exchange-2013-help.md).

## Definire l'ambito della regola

Verificare che la regola venga applicata solo ai messaggi che si desidera. Ad esempio:

  - **Limitare una regola ai messaggi inviati o ricevuti dall'organizzazione**
    
    Per impostazione predefinita, una nuova regola viene applicata ai messaggi inviati o ricevuti dagli utenti dell'organizzazione. Se si desidera applicare la regola solo in modo unidirezionale, sarà necessario specificarlo nelle condizioni per la regola. Per un esempio, vedere [Scenari comuni relativi al blocco degli allegati](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md).

  - **Limitare una regola in base al dominio del mittente o del destinatario**
    
    Per impostazione predefinita, una nuova regola viene applicata ai messaggi inviati o ricevuti da qualsiasi dominio. A volte può essere utile applicare una regola a tutti i domini ad eccezione di uno o a un solo dominio. Per ulteriori esempi, vedere [Creare a livello di organizzazione mittenti attendibili o degli elenchi di mittenti bloccati in Office 365](https://technet.microsoft.com/it-it/library/dn198251\(v=exchg.150\)).

Per un elenco completo di tutte le condizioni e le eccezioni che sono disponibili per le regole di trasporto, vedere:

  - [Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online](https://technet.microsoft.com/it-it/library/jj919235\(v=exchg.150\))

  - [Condizioni delle regole di trasporto (predicati)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

  - [Condizioni ed eccezioni della regola del flusso di posta (predicati) in Exchange Online Protection](https://technet.microsoft.com/it-it/library/jj919234\(v=exchg.150\))

## Quando sono necessarie due regole

A volte sono necessarie due regole per eseguire le operazioni desiderate. Le regole di trasporto vengono elaborate nell'ordine, in modo che più regole possano essere applicate allo stesso messaggio. Ad esempio, se una delle azioni consiste nel bloccare il messaggio e si desidera applicare un'altra azione (come copiare il messaggio al responsabile del mittente oppure modificare l'oggetto del messaggio di notifica), potrebbero essere necessarie due regole. La prima consentirebbe di copiare il messaggio al responsabile del mittente e di modificare l'oggetto, mentre la seconda potrebbe bloccare il messaggio.

Se si utilizzano due regole simili a queste, assicurarsi che le condizioni siano identiche. Per vedere degli esempi, consultare l'esempio 3 in [Scenari comuni di approvazione messaggio](common-message-approval-scenarios-exchange-2013-help.md), l'esempio 3 in [Scenari comuni relativi al blocco degli allegati](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md) e [Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità per tutta l'organizzazione](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md).

## Non ripetere un'azione su tutti i messaggi di posta elettronica di una conversazione

La catena di e-mail in una conversazione può includere molti messaggi singoli e ripetere l'azione su ognuno dei messaggi nel thread potrebbe diventare fastidioso. Ad esempio, se si dispone di un'azione, ad esempio l'aggiunta di una dichiarazione di non responsabilità, è consigliabile applicarla solo al primo messaggio del thread. In questo caso, aggiungere un'eccezione per i messaggi che includono già il testo della dichiarazione di non responsabilità. Per un esempio, vedere [Intestazioni, piè di pagina, firme o dichiarazioni di non responsabilità per tutta l'organizzazione](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md).

## Quando interrompere l'elaborazione delle regole

A volte è opportuno interrompere l'elaborazione di una regola dopo averla assegnata. Ad esempio, se si dispone di una regola che blocca i messaggi con gli allegati e di una regola che inserisce una dichiarazione di non responsabilità nei messaggi che corrispondono a un criterio, probabilmente sarà necessario interrompere l'elaborazione della regola una volta che il messaggio sarà stato bloccato. Non è necessario eseguire ulteriori operazioni.

Per interrompere l'elaborazione di una regola dopo che è stata attivata, nella regola, selezionare la casella di controllo **Interrompi l'elaborazione di ulteriori regole**.

## Se si dispone di un numero elevato di parole chiave o criteri con cui trovare la corrispondenza, caricarli da un file

È consigliabile, ad esempio, impedire l'invio di messaggi di posta elettronica se contengono un elenco di parole non consentite o inaccettabili. È possibile creare un file di testo contenente tali parole e frasi, quindi utilizzare Windows PowerShell per configurare una regola di trasporto che consenta di bloccare i messaggi che le usano.

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


Per un esempio che mostra un file di testo con espressioni regolari e i comandi di Windows PowerShell del modulo Exchange da utilizzare, vedere [Utilizzare regole del flusso di posta per instradare le e-mail in base a un elenco di parole, frasi o motivi](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md).

Per informazioni su come specificare criteri utilizzando espressioni regolari, vedere [Riferimenti sulle espressioni regolari](https://go.microsoft.com/fwlink/p/?linkid=532394).

