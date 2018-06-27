---
title: "Suggerimenti messaggio tramite le relazioni dell'organizzazione: Exchange 2013 Help"
TOCTitle: Suggerimenti messaggio tramite le relazioni dell'organizzazione
ms:assetid: 1784256f-abe1-4503-b8c4-26d544b73452
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ670165(v=EXCHG.150)
ms:contentKeyID: 50480067
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suggerimenti messaggio tramite le relazioni dell'organizzazione

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Microsoft Exchange Server 2013 consente di configurare le relazioni organizzative con Microsoft Exchange Online o altre organizzazioni di Exchange. La creazione di una relazione organizzativa consente di ottimizzare il lavoro degli utenti quando trattano con un'altra organizzazione. Ad esempio, è possibile condividere dati sulla disponibilità, configurare flussi di messaggi sicuri e abilitare la verifica dei messaggi per entrambe le organizzazioni.

## Controllo del livello di accesso dei suggerimenti messaggio

Si potrebbe desiderare di limitare determinati tipi di suggerimenti messaggio. È possibile consentire la restituzione di tutti i suggerimenti messaggio o solo di una serie limitata che eviterebbe rapporti di mancato recapito. È possibile configurare tale impostazione utilizzando il parametro *MailTipsAccessLevel* del cmdlet **Set-OrganizationRelationship**. Nella tabella seguente, vengono illustrati gli avvisi messaggio che vengono restituiti relativamente alla relazione organizzativa.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Avviso messaggio</th>
<th>Il suggerimento messaggio è disponibile quando il livello di accesso è impostato su Tutto?</th>
<th>Il suggerimento messaggio è disponibile quando il livello di accesso è impostato su Limitato?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pubblico esteso</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Risposte automatiche</p></td>
<td><p>Sì</p>
<p>Se il dominio remoto del destinatario è specificato come interno, viene visualizzata la risposta automatica interna. In caso contrario, viene visualizzata la risposta automatica esterna.</p></td>
<td><p>Sì</p>
<p>Viene visualizzata la risposta automatica esterna.</p></td>
</tr>
<tr class="odd">
<td><p>Destinatario moderato</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Messaggio troppo grande</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Destinatario con limitazioni</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale piena</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Suggerimenti messaggio personalizzati</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Destinatari esterni</p></td>
<td><p>Sì</p>
<p>Se il dominio remoto del destinatario è specificato come interno, l'avviso messaggio viene rimosso. In caso contrario, viene restituito l'avviso messaggio esterno.</p></td>
<td><p>Sì</p>
<p>Se il dominio remoto del destinatario è specificato come interno, l'avviso messaggio viene rimosso. In caso contrario, viene restituito l'avviso messaggio esterno.</p></td>
</tr>
</tbody>
</table>


Per la procedura dettagliata su come configurare i livelli di accesso degli avvisi messaggio, vedere [Gestire i suggerimenti per le relazioni dell'organizzazione](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

## Controllo dell'ambito di accesso de suggerimenti messaggio

Quando si abilitano gli avvisi messaggio per una relazione organizzativa e si imposta il livello di accesso su `All`, vengono restituiti gli avvisi messaggio specifici del destinatario, Cassetta postale piena, Risposte automatiche e personalizzati per tutti gli utenti. Tuttavia, è possibile che si desideri consentire tali avvisi messaggio solo per un determinato gruppo di utenti. Ad esempio, se si configura una relazione organizzativa con un partner, è possibile che si desideri consentire tali avvisi messaggio solo per gli utenti che lavorano con quel partner.

A tale scopo, è necessario creare prima un gruppo e aggiungere tutti gli utenti per cui si desidera condividere avvisi messaggio specifici del destinatario con quel gruppo. È, quindi, possibile specificare tale gruppo nella relazione organizzativa.

Una volta implementata tale restrizione, i server Accesso client verificheranno prima se il destinatario per cui hanno ricevuto la query sugli avvisi messaggio fa parte di questo gruppo. Se il destinatario è un membro del gruppo, i server Accesso client eseguiranno nuovamente il proxy di tutti gli avvisi messaggio, inclusi quelli specifici del destinatario. In caso contrario, includeranno gli avvisi messaggio specifici del destinatario nella risposta.

Per la procedura dettagliata su come configurare i livelli di accesso degli avvisi messaggio, vedere [Gestire i suggerimenti per le relazioni dell'organizzazione](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

