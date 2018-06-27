---
title: "Utilizzo dell'autenticazione OAuth per supportare eDiscovery in un'implementazione ibrida di Exchange: Exchange 2013 Help"
TOCTitle: Utilizzo dell'autenticazione OAuth per supportare eDiscovery in un'implementazione ibrida di Exchange
ms:assetid: b069f8db-fbe1-4047-ad97-d00172ee6a12
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn497703(v=EXCHG.150)
ms:contentKeyID: 61292119
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizzo dell'autenticazione OAuth per supportare eDiscovery in un'implementazione ibrida di Exchange

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Per eseguire correttamente delle ricerche eDiscovery estese in un'organizzazione Exchange 2013 ibrida, è necessario configurare l'autenticazione OAuth (Open Authorization) tra organizzazioni Exchange in locale e Exchange Online in modo che sia possibile utilizzare eDiscovery in locale per ricercare cassette postali in locale e basate sul cloud. L'autenticazione OAuth supporta i seguenti scenari di eDiscovery in un'implementazione ibrida di Exchange:

  - Cassette postali di ricerca locali che utilizzano il Archiviazione Exchange Online per le cassette postali basate su cloud.

  - Ricerca locale e cassette postali basate su cloud nella ricerca di eDiscovery stesso.

Per istruzioni dettagliate sulla configurazione dell'autenticazione OAuth per supportare eDiscovery, vedere [Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md).

## Che cos'è l'autenticazione OAuth?

L'autenticazione OAuth è un protocollo di autenticazione S2S che consente alle applicazioni di eseguire l'autenticazione reciproca. Con l'autenticazione OAuth non avviene alcun passaggio di password e credenziali utente da un computer all'altro. Al contrario, l'autenticazione e l'autorizzazione si basano sullo scambio di token di sicurezza, che forniscono accesso a un gruppo specifico di risorse per un periodo di tempo specifico.

Di solito, l'autenticazione OAuth comprende tre parti: un server di autorizzazione singolo e due aree di autenticazione che devono comunicare fra loro. I token di sicurezza vengono rilasciati dal server di autorizzazione (noto anche come server del token di sicurezza) nelle due aree di autenticazione che devono comunicare. Questi due token verificano che le comunicazioni originate da un'area di autenticazione siano considerate attendibili dall'altra area di autenticazione. Durante l'utilizzo dell'autenticazione OAuth tra un'organizzazione Exchange locale ed Exchange Online, la funzione del server di autorizzazione è garantita dai servizi di controllo di accesso di Microsoft Azure Active Directory nell'organizzazione Office 365. Ad esempio, durante una ricerca eDiscovery cross-premise, il servizio di controllo di accesso Azure genera token che verificano che l'amministratore, o il responsabile della conformità, dell'organizzazione Exchange locale sia in grado di accedere alle cassette postali nell'organizzazione Exchange Online e viceversa.

## Scenari di eDiscovery in una distribuzione ibrida

La tabella seguente identifica gli scenari eDiscovery in una distribuzione ibrida di Exchange che richiedono l'autenticazione OAuth.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Scenario eDiscovery</th>
<th>Richiede l'autenticazione OAuth?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cercare le cassette postali Exchange locali e le cassette postali Exchange Online nella stessa ricerca eDiscovery inizializzata dall'organizzazione Exchange locale. Ad esempio, ricercare tutte le cassette postali dell'organizzazione in un'unica ricerca eDiscovery.</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Cercare le cassette postali di Exchange locali che utilizzano l'Archiviazione Exchange Online per le cassette postali basate su cloud. Quando si utilizza eDiscovery sul posto, viene eseguita la ricerca nelle cassette postali di archiviazione e principali.</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Cercare cassette postali di Exchange Online da una ricerca eDiscovery inizializzata dall'organizzazione Exchange locale da un amministratore o responsabile della conformità.</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Cercare cassette postali locali tramite una ricerca eDiscovery inizializzata dall'organizzazione Exchange locale da un amministratore o responsabile della conformità.</p></td>
<td><p>No</p>

> [!NOTE]
> Come illustrato precedentemente, l'autenticazione OAuth sarà necessaria se le cassette postali locali sono state configurate con cassette postali specifiche per l'archiviazione basate su cloud.


</td>
</tr>
<tr class="odd">
<td><p>Cercare cassette postali di Exchange Online da una ricerca eDiscovery inizializzata da Exchange Online o dal Centro eDiscovery in SharePoint Online da un amministratore titolare di Office 365 o un responsabile della conformità che abbia eseguito l'accesso con account utente Office 365.</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Configurazione dell'autenticazione OAuth per supportare eDiscovery

Come affermato in precedenza, vedere [Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md) per istruzioni sulla configurazione dell'autenticazione OAuth per supportare eDiscovery in una distribuzione Exchange ibrida.

Se OAuth non è configurato per la distribuzione Exchange ibrida, non è possibile utilizzare eDiscovery per cercare cassette postali di Exchange locale e di Exchange Online nella stessa ricerca eDiscovery. Sarà necessario cercare le cassette postali locali da una ricerca eDiscovery inizializzata dall'organizzazione locale. Analogamente, sarà possibile cercare solo le cassette postali di Exchange Online da una ricerca eDiscovery inizializzata dall'organizzazione Exchange Online o utilizzando il Centro eDiscovery in SharePoint Online. Inoltre, non sarà possibile cercare le cassette postali locali principali se la cassetta postale specifica per l'archiviazione risiede in Exchange Online o in un'organizzazione di Archiviazione Exchange Online.

## Ulteriori informazioni

  - È anche possibile utilizzare l'autenticazione OAuth per consentire ad altre applicazioni, ad esempio SharePoint 2013 e Lync Server 2013, di eseguire l'autenticazione a Exchange 2013. Per ulteriori informazioni, vedere [Configurazione dell'autenticazione OAuth con SharePoint 2013 e Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

  - È possibile configurare l'autenticazione da server a server tra Exchange 2013 e SharePoint 2013 in modo che gli amministratori e responsabili della conformità possano utilizzare il Centro eDiscovery in SharePoint 2013 per cercare nelle cassette postali di Exchange 2013. Per ulteriori informazioni, vedere [Configurare Exchange per SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md).

  - È possibile configurare una distribuzione ibrida di Exchange utilizzando la procedura guidata Configurazione ibrida in Exchange 2013. Per elenco di controllo configurazione distribuzione ibrida dettagliato e personalizzato, vedere [Exchange Server Deployment Assistant](https://go.microsoft.com/fwlink/p/?linkid=277105).

