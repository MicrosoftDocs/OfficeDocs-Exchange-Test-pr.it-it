---
title: 'Autorizzare chiamate utilizzando le regole di composizione: Exchange 2013 Help'
TOCTitle: Autorizzare chiamate utilizzando le regole di composizione
ms:assetid: 4c18bc07-f55c-42b7-81c1-729878aa93aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898499(v=EXCHG.150)
ms:contentKeyID: 51407360
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzare chiamate utilizzando le regole di composizione

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-03-09_

Per impostazione predefinita, gli utenti non sono abilitati a effettuare chiamate in uscita. Per specificare i tipi di chiamate che gli utenti possono effettuare, creare prima le regole di composizione, quindi autorizzare i gruppi di queste regole di composizione per i dial plan di messaggistica unificata, per i criteri cassette postali di messaggistica unificata o per gli operatori automatici di messaggistica unificata. Per poter autorizzare gruppi di regole di composizione, è innanzitutto necessario definire le regole di composizione per il dial plan di messaggistica unificata. Per ulteriori informazioni, vedere [Creare regole di composizione per gli utenti](create-dialing-rules-for-users-exchange-2013-help.md).

Ogni regola di composizione creata contiene i tipi di chiamate o il formato numero ai quali si desidera che gli utenti accedano. È possibile consentire differenti tipi di utenti per diversi tipi di chiamate. Le chiamate consentite possono essere nazionali o internazionali.

Per autorizzare o limitare le regole di composizione correttamente, è necessario configurare le seguenti impostazioni:

  - **Regole di composizione**   Le regole di composizione stabiliscono il numero che gli utenti abilitati alla messaggistica unificata possono comporre e il numero che verrà inviato dalla messaggistica unificata e composto dal PBX (Private Branch eXchange) o dall'IP PBX. È possibile creare un gruppo di regole di composizione aggiungendo una regola di composizione. Dopo aver creato un gruppo di regole di composizione, aggiungerlo all'elenco delle chiamate consentite per un paese/regione o al gruppo di regole di composizione internazionale.

  - **Gruppi di regole di composizione**   Determinano i tipi di chiamata che possono effettuare gli utenti di un gruppo di composizione.

  - **Autorizzazioni di composizione**   Determinano le autorizzazioni che verranno applicate per impedire agli utenti di effettuare chiamate su lunghe distanze e di ricevere addebiti per telefonate non richieste.

## Come autorizzare un gruppo di regole di composizione

Dove autorizzare un gruppo di regole di composizione dipende dai tipi di chiamanti ai quali si desidera consentire di effettuare chiamate in uscita. Ad esempio, se si desidera consentire solo a utenti di Outlook Voice Access di effettuare chiamate in uscita, verranno create le proprie regole di composizione e si autorizzeranno quei gruppi di regole di composizione al criterio di cassetta postale di messaggistica unificata ai quali sono collegati gli utenti di Outlook Voice Access. Nella seguente tabella viene mostrato come autorizzare chiamate per differenti tipi di chiamanti.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di chiamante</th>
<th>Autorizzare qui i gruppi di regole di composizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti non autenticati che chiamano un numero di Outlook Voice Access e non inseriscono il PIN</p></td>
<td><p>Dial plan di messaggistica unificata. Per ulteriori informazioni, vedere <a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Autorizzare chiamate per gli utenti in un dial plan</a>.</p></td>
</tr>
<tr class="even">
<td><p>Utenti autenticati che chiamano un numero di Outlook Voice Access e inseriscono il PIN</p></td>
<td><p>Criteri cassetta postale di messaggistica unificata per il chiamante. Per ulteriori informazioni, vedere <a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">Autorizzare le chiamate per un gruppo di utenti</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Utenti autenticati che chiamano un numero di telefono configurato per un operatore automatico di messaggistica unificata</p></td>
<td><p>Operatore automatico di messaggistica unificata. Per ulteriori informazioni, vedere <a href="authorize-calls-for-auto-attendant-callers-exchange-2013-help.md">Autorizzare chiamate per i chiamanti dell'operatore automatico</a>.</p></td>
</tr>
</tbody>
</table>


A seconda di quali utenti vengono autorizzati a effettuare chiamate in uscita, utilizzare la pagina **Autorizzazione di composizione** nell'interfaccia di amministrazione di Exchange per il dial plan, per l'operatore automatico o per il criterio di cassette postali di messaggistica unificata.

