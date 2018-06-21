---
title: 'Configurare Exchange in modo da supportare le autorizzazioni per cassette postali con delega in una distribuzione ibrida: Exchange 2013 Help'
TOCTitle: Configurare Exchange in modo da supportare le autorizzazioni per cassette postali con delega in una distribuzione ibrida
ms:assetid: a2a10cb3-4557-4ff5-8191-c653522f4512
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Mt784505(v=EXCHG.150)
ms:contentKeyID: 74447325
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare Exchange in modo da supportare le autorizzazioni per cassette postali con delega in una distribuzione ibrida

 

_<strong>Ultima modifica dell'argomento:</strong>2018-01-30_

Le autorizzazioni per cassette postali delegate consentono di gestire parte della cassetta postale di altri utenti. Un esempio comune è quello di un assistente amministrativo che deve gestire le cassette postali e il calendario di un dirigente. Le distribuzioni ibride tra un'organizzazione di Exchange locale e Office 365 supportano le autorizzazioni per cassette postali delegate di tipo **Accesso completo** e **Invia per conto di**. Tuttavia, a seconda della versione di Exchange installata nell'organizzazione locale, è possibile eseguire altre operazioni di configurazione per utilizzare le autorizzazioni per cassette postali delegate in una distribuzione ibrida. Di seguito sono elencate le versioni di Exchange che supportano le autorizzazioni per cassette postali delegate in una distribuzione ibrida ed eventuali ulteriori configurazioni necessarie per tale versione.

  - **Exchange 2016** - Non sono necessarie ulteriori configurazioni.

  - **Exchange 2013** - Sono necessari un aggiornamento cumulativo di Exchange 2013 (CU) supportato e altre operazioni di configurazione.

  - **Exchange 2010** - Sono necessari un aggiornamento cumulativo di Exchange 2010 (RU) supportato e altre operazioni di configurazione.

Per ulteriori informazioni sui requisiti specifici per il supporto delle autorizzazioni per cassette postali delegate nelle distribuzioni ibride, esaminare [Autorizzazioni nelle distribuzioni ibride di Exchange](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md).

Nelle sezioni seguenti vengono descritti i passaggi per la configurazione delle distribuzioni locali di Exchange 2013 ed Exchange 2010 per abilitare il supporto alle autorizzazioni per cassette postali delegate. Prima di seguire questa procedura, è necessario verificare di disporre della versione più recente di Exchange 2013 CU o Exchange SP3 RU. Per ulteriori informazioni, vedere [Prerequisiti per la distribuzione ibrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

## Exchange 2013

Le operazioni necessarie per abilitare il supporto alle autorizzazioni per cassette postali delegate dipende da una serie di fattori. Se quando le cassette postali sono state spostate in Office 365:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Quanto riportato di seguito era installato...</th>
<th>E la sincronizzazione degli oggetti ACLable dell'organizzazione era...</th>
<th>A tal punto è necessario...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU9 o versioni precedenti</p></td>
<td><p>Questa funzione non è disponibile in Exchange 2013 CU9 e versioni precedenti.</p></td>
<td><p>Configurare manualmente ogni cassetta postale per supportare ACL</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU10 o versione successiva</p></td>
<td><p>Disabilitata</p></td>
<td><ol>
<li><p>Abilitare la sincronizzazione degli oggetti ACLable a livello di organizzazione</p></li>
<li><p>Abilitare manualmente gli ACL su ogni cassetta postale spostata in Office 365 prima dell’abilitazione della sincronizzazione degli oggetti ACLable a livello di organizzazione.</p></li>
</ol>
<p>Non sono necessarie configurazioni ulteriori per le cassette postali spostate in Office 365 in seguito all’abilitazione della sincronizzazione degli oggetti ACLable a livello di organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2013 CU10 o versione successiva</p></td>
<td><p>Abilitata</p></td>
<td><p>Non sono necessarie ulteriori configurazioni</p></td>
</tr>
</tbody>
</table>


## Abilitare la sincronizzazione degli oggetti ACLable

Per abilitare la sincronizzazione degli oggetti ACLable a livello di organizzazione, eseguire le operazioni seguenti.

1.  Installare la versione più recente di Azure Active Directory Connect (AAD Connect) in tutti i server AAD Connect. Questa operazione è necessaria per consentire ad AAD Connect di sincronizzare gli attributi necessari per supportare le autorizzazioni ibride. È possibile scaricare AAD Connect da [Microsoft Azure Active Directory Connect](http://go.microsoft.com/fwlink/p/?linkid=510956).

2.  Aprire Exchange Management Shell su un server che esegue la versione più recente disponibile di Exchange 2013 CU o l’aggiornamento cumulativo immediatamente precedente.

3.  Eseguire il comando riportato di seguito.
    
        Set-OrganizationConfig -ACLableSyncedObjectEnabled $True

Dopo tale operazione, tutte le cassette postali spostate in Office 365 verranno correttamente configurate per supportare le autorizzazioni per cassette postali delegate. Se le cassette postali sono state spostate in Office 365 prima di aver completato questa procedura, è necessario attivare manualmente gli ACL sulle cassette postali che utilizzano la procedura descritta in Abilitare ACL su cassette postali remote.


> [!IMPORTANT]
> Gli elenchi ACL non sono abilitate per le cassette postali remote create in Office 365. Se si crea una cassetta postale remota in Office 365, è necessario completare la procedura descritta negli elenchi di controllo Abilita nella sezione cassette postali remote per abilitare gli elenchi ACL su tale cassetta postale remota. Per evitare questo passaggio aggiuntivo, è consigliabile creare la cassetta postale su un server di Exchange locale e quindi spostare le cassette postali a Office 365.



## Abilitare ACL su cassette postali remote

Per abilitare manualmente gli ACL su ogni cassetta postale spostata in Office 365 prima dell’abilitazione della sincronizzazione degli oggetti ACLable a livello di organizzazione, eseguire le operazioni seguenti.

1.  Aprire Exchange Management Shell su un server che esegue la versione più recente disponibile di Exchange 2013 CU o l’aggiornamento cumulativo immediatamente precedente.

2.  Per abilitare gli ACL su una singola cassetta postale, eseguire il comando seguente.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Per abilitare gli ACL su tutte le cassette postali spostate in Office 365, eseguire il comando seguente.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  Per verificare che le cassette postali siano state aggiornate, eseguire il comando seguente.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

## Exchange 2010

I server Exchange 2010 SP3 supportano la configurazione di ACL sulle cassette postali remote. Tuttavia, tale configurazione deve essere impostata manualmente per ogni cassetta postale. A differenza delle versioni più recenti di Exchange, Exchange 2010 non fornisce la possibilità di impostare questa funzionalità a livello di organizzazione. Seguire la procedura riportata di seguito per tutte le cassette postali precedentemente spostate in Office 365 e per tutte le cassette postali che in futuro verranno spostate da un server Exchange 2010 SP3 in Office 365.

## Abilitare ACL su cassette postali remote

Per abilitare gli ACL sulle cassette postali spostate in Office 365, eseguire le operazioni seguenti.

1.  Aprire Exchange Management Shell su un server che esegue la versione più recente disponibile di Exchange 2010 SP3 RU o l’aggiornamento cumulativo immediatamente precedente.

2.  Per abilitare gli ACL su una singola cassetta postale, eseguire il comando seguente.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Per abilitare gli ACL su tutte le cassette postali spostate in Office 365, eseguire il comando seguente.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  Per verificare che le cassette postali siano state aggiornate, eseguire il comando seguente.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

