---
title: 'Autorizzazioni nelle distribuzioni ibride di Exchange: Exchange 2013 Help'
TOCTitle: Autorizzazioni nelle distribuzioni ibride di Exchange
ms:assetid: 58b46b2c-a6b2-424a-8fc2-0f1fe1ad8e18
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ906433(v=EXCHG.150)
ms:contentKeyID: 51406949
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Autorizzazioni nelle distribuzioni ibride di Exchange

 

_<strong>Si applica a:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2018-05-02_

L'organizzazione di Exchange Online in Office 365 è basata su Exchange Server e, come le organizzazioni locali, utilizza il controllo delle accessi in base ai ruoli (RBAC, Role Based Access Control) per verificare le autorizzazioni. Le autorizzazioni sono concesse agli amministratori, utilizzando i gruppi di ruoli di gestione, e agli utenti finali, tramite i criteri di assegnazione dei ruoli di gestione.

Ulteriori informazioni in merito alle autorizzazioni di Exchange Online e di Exchange in locale sono disponibili in: [Autorizzazioni](https://technet.microsoft.com/it-it/library/dd351175\(v=exchg.150\))

## Autorizzazioni dell'amministratore

Per impostazione predefinita, l'utente utilizzato per creare il tenant di Office 365 diventa un membro del gruppo dei ruoli Gestione organizzazione nell'organizzazione di Exchange Online. Tale utente è in grado di gestire l'intera organizzazione di Exchange Online, inclusi la configurazione delle impostazioni a livello di organizzazione e la gestione dei destinatari di Exchange Online.

È possibile aggiungere ulteriori amministratori nell'organizzazione di Exchange Online, a seconda del tipo di gestione necessario. Sono possibili diverse operazioni: aggiungere altri amministratori di organizzazione e dei destinatari, consentire agli utenti esperti di eseguire attività di verifica della conformità quali l'individuazione, la configurazione delle autorizzazioni personalizzate e altro ancora. È necessario che l'intera gestione delle autorizzazioni di Exchange Online per gli amministratori di Office 365 sia effettuata nell'organizzazione di Exchange Online tramite l'interfaccia di amministrazione di Exchange o Remote PowerShell.


> [!IMPORTANT]
> Non vi è alcun trasferimento di autorizzazioni tra l'organizzazione locale e l'organizzazione di Office 365. È necessario che le autorizzazioni definite per l'organizzazione locale siano ricreate per l'organizzazione di Office 365.



Per ulteriori informazioni, vedere [Gestire gruppi di ruoli](https://technet.microsoft.com/it-it/library/jj657480\(v=exchg.150\)) e [Gestire i membri del gruppo di ruolo](https://technet.microsoft.com/it-it/library/jj657492\(v=exchg.150\)).

## Delegare le autorizzazioni per le cassette postali

Nelle distribuzioni di Exchange locale, gli utenti possono essere concessi un'ampia gamma di autorizzazioni per le cassette postali di altri utenti. Si tratta delle cassette postali delegate le autorizzazioni e le relative utile quando è necessario gestire alcune parti della cassetta postale dell'utente, un Assistente amministrativo ad esempio, la gestione del calendario della persona. Distribuzioni ibride di Exchange supportano l'utilizzo di alcune, ma non tutte le autorizzazioni delle cassette postali tra le cassette postali che si trova in un'organizzazione di Exchange locale e cassette postali che si trovano in Office 365. Il tipo di autorizzazione di dettaglio nelle sezioni seguenti sono e non sono supportate. configurazione aggiuntiva necessaria per supportare le autorizzazioni delle cassette postali ibridi; e la modalità di sincronizzazione delle autorizzazioni delle cassette postali tra l'organizzazione locale e Office 365.

## Autorizzazioni per cassette postali supportate negli ambienti ibridi

Le seguenti autorizzazioni **sono** supportate:

  - **Accesso completo** A una cassetta postale in un server Exchange locale può essere concessa l'autorizzazione di **Accesso completo** per una cassetta postale di Office 365 e viceversa. Ad esempio, a una cassetta postale di Office 365 può essere concessa l'autorizzazione di **Accesso completo** per una cassetta postale condivisa locale. Gli utenti devono aprire la cassetta postale utilizzando il client desktop di Outlook. Le autorizzazioni per la cassetta postale cross-premise non sono supportate in Outlook sul web.
    

    > [!NOTE]
    > Gli utenti potrebbero visualizzare richieste di ulteriori credenziali quando accedono per la prima volta a una cassetta postale che si trova nell'altra organizzazione e l'aggiungono al proprio profilo di Outlook.



  - **Invia per conto di** A una cassetta postale in un server Exchange locale può essere concessa l'autorizzazione di **Invia per conto di** per una cassetta postale di Office 365 e viceversa. Ad esempio, a una cassetta postale di Office 365 può essere concessa l'autorizzazione di **Invia per conto di** per una cassetta postale condivisa locale. Gli utenti devono aprire la cassetta postale utilizzando il client desktop di Outlook. Le autorizzazioni per la cassetta postale cross-premise non sono supportate in Outlook sul web.
    
    Sono necessarie alcune modifiche nel server Azure Active Directory Connect per le autorizzazioni di Invio per conto di per la sincronizzazione tra il server Exchange locale ed Exchange Online. Per informazioni dettagliate, vedere Attivare il supporto per le autorizzazioni per cassette postali ibride in Azure Active Directory Connect più avanti in questo argomento.

  - **Folder permissions** Grants access to the contents of a particular folder.

  - **Elementi personali** Quando si aggiunge che un delegato l'opzione può essere configurato per consentire a un utente con autorizzazioni per le cartelle per visualizzare gli elementi del calendario privata.


> [!NOTE]
> A partire da febbraio 2018 la funzionalità per il supporto dell'accesso completo, invia per conto e cartella diritti insiemi di strutture è corso di implementazione e dovrebbe essere completata da 2018 aprile.



Le autorizzazioni seguenti o capacità **non sono** supportate:

  - **Send-As** Consente a un utente di inviare posta che sembra provenire dalla cassetta postale di un altro utente.

  - **Mapping automatico** consente ad Outlook, all'avvio, di aprire automaticamente tutte le cassette postali cui un utente ha ottenuto **accesso completo**.

Le cassette postali che ricevono tali autorizzazioni da un'altra cassetta postale devono essere spostate nello stesso momento in cui viene trasferita quella cassetta postale di concessione. Se una cassetta postale riceve autorizzazioni da più cassette postali, è necessario spostare contemporaneamente tutte le cassette postali (sia quella che riceve le autorizzazioni sia quelle che le concedono).

## Configurare i server di Exchange locali per supportare le autorizzazioni per cassette postali ibride

Per abilitare le autorizzazioni Accesso completo e Invia per conto di nelle distribuzioni ibride, potrebbero essere necessarie altre modifiche alla configurazione a seconda della versione di Exchange installata. La tabella seguente mostra le versioni di Exchange che supportano le autorizzazioni per cassette postali delegate in una distribuzione ibrida con Office 365 ed eventuali ulteriori configurazioni necessarie. Per istruzioni su come configurare i server e le cassette postali di Exchange 2013 e 2010 per il supporto di ACL, vedere [Configurare Exchange in modo da supportare le autorizzazioni per cassette postali con delega in una distribuzione ibrida](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versione di Exchange</th>
<th>Prerequisiti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2016</p></td>
<td><p>Non sono necessarie ulteriori configurazioni.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p>Per i server di Exchange 2013 è necessario quanto segue:</p>
<ul>
<li><p>L'aggiornamento cumulativo più recente (CU) oppure la CU immediatamente precedente, installato. I server Exchange 2013 che eseguono aggiornamenti cumulativi precedenti non sono supportati e potrebbero non funzionare con le autorizzazioni per cassette postali delegate nelle distribuzioni ibride.</p></li>
<li><p>L'organizzazione di Exchange è configurata per consentire agli elenchi di controllo di accesso (ACL) di essere contrassegnati negli oggetti di posta elettronica e sincronizzati con Office 365.</p></li>
<li><p>Le cassette postali remote locali associate con le cassette postali sono state spostate in Office 365 prima della configurazione manuale di Exchange 2013 CU10 per supportare gli ACL. Le cassette postali remote, create su server che eseguono Exchange 2013 CU10 o versione successiva e in seguito all’impostazione dell’organizzazione di Exchange per consentire gli ACL, vengono configurate automaticamente.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Per i server di Exchange 2010 SP3 è necessario quanto segue:</p>
<ul>
<li><p>L'aggiornamento cumulativo più recente (RU) oppure la RU immediatamente precedente, installato. I server Exchange 2010 SP3 che eseguono aggiornamenti cumulativi precedenti non sono supportati e potrebbero non funzionare con le autorizzazioni per cassette postali delegate nelle distribuzioni ibride.</p></li>
<li><p>Le cassette postali remote locali associate con cassette postali di Office 365 devono essere configurate per supportare gli ACL. L’operazione deve essere eseguita per ciascuna cassetta postale remota locale associata a una cassetta postale di Office 365.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 o versione precedente</p></td>
<td><p>Non supportato.</p></td>
</tr>
</tbody>
</table>


## Attivare il supporto per le autorizzazioni per cassette postali ibride in Azure Active Directory Connect

Oltre a configurare i server di Exchange locali, è necessario assicurarsi che i server di Azure Active Directory Connect (AAD Connect) siano stati configurati per la sincronizzazione delle autorizzazioni per cassette postali ibride. Di seguito viene riportata la procedura da seguire per verificare che il server AAD Connect sia pronto per supportare queste autorizzazioni:

  - **Connettere AAD aggiornamento** Connettere AAD deve essere aggiornato almeno a versione 1.1.553.0. È possibile scaricare la versione più recente di AAD Connect di [Azure Active Directory connettersi](http://go.microsoft.com/fwlink/p/?linkid=510956).

  - **Abilitare Exchange ibrido in AAD Connect** Per sincronizzare gli attributi che consentono le autorizzazioni per cassette postali ibride (in particolare l'autorizzazione Invia per conto di), è necessario verificare di aver abilitato l’opzione di configurazione **Distribuzione ibrida di Exchange** in AAD Connect. Per informazioni su come eseguire la procedura di installazione AAD Connect per aggiornare la configurazione, vedere [Sincronizzazione di Azure AD Connect: Eseguire l'installazione guidata una seconda volta](https://docs.microsoft.com/it-it/azure/active-directory/connect/active-directory-aadconnectsync-installation-wizard)

## Modalità di sincronizzazione delle autorizzazioni per cassette postali tra organizzazioni locali e di Office 365

## Autorizzazioni dell'utente finale

Come per le autorizzazioni dell'amministratore, in Exchange Online è possibile concedere autorizzazioni agli utenti finali. Per impostazione predefinita, agli utenti finali le autorizzazioni sono concesse tramite il criterio di assegnazione del ruolo predefinito. Questo criterio viene applicato a ogni cassetta postale dell'organizzazione di Exchange Online. Se le autorizzazioni concesse per impostazione predefinita sono sufficienti, non è necessario apportare alcuna modifica.

Al fine di personalizzare le autorizzazioni per l'utente finale, è possibile modificare l'attuale criterio di assegnazione dei ruoli predefinito oppure creare nuovi criteri di assegnazione. Se si creano più criteri di assegnazione, è possibile assegnare vari criteri a diversi gruppi di cassette postali, in modo da controllare le autorizzazioni concesse ad ogni gruppo a seconda delle relative esigenze. È necessario che la gestione di tutte le autorizzazioni per gli utenti finali di Exchange Online sia effettuata nell'organizzazione di Exchange Online tramite l'interfaccia di amministrazione di Exchange e Remote PowerShell.

Sia le autorizzazioni dell'amministratore che le autorizzazioni dell'utente finale non vengono trasferite tra l'organizzazione locale e l'organizzazione di Exchange Online. È necessario che tutte le autorizzazioni definite per l'organizzazione locale sia ricreata per l'organizzazione di Exchange Online.

Per ulteriori informazioni, vedere [Gestire i criteri di assegnazione dei ruoli](https://technet.microsoft.com/it-it/library/jj657511\(v=exchg.150\)) e [Modificare il criterio di assegnazione di una cassetta postale](https://technet.microsoft.com/it-it/library/dd638076\(v=exchg.150\)).

Nella tabella seguente sono elencate le autorizzazioni concesse dai criteri di assegnazione dei ruoli predefiniti nell'organizzazione di Exchange Online.

### Autorizzazioni del criterio di assegnazione del ruolo predefinito

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruoli di gestione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MyTeamMailboxes</p></td>
<td><p>Il ruolo di gestione <code>MyTeamMailboxes</code> consente ai singoli utenti di creare cassette postali del sito e connetterle ai siti Microsoft SharePoint.</p></td>
</tr>
<tr class="even">
<td><p>App Marketplace</p></td>
<td><p>I ruoli di gestione <code>My Marketplace Apps</code> consentono ai singoli utenti di visualizzare e modificare le relative app marketplace di Microsoft Office.</p></td>
</tr>
<tr class="odd">
<td><p>MyBaseOptions</p></td>
<td><p>I ruoli di gestione <code>MyBaseOptions</code> consentono ai singoli utenti di visualizzare e modificare la configurazione di base delle relative cassette postali e le impostazioni associate.</p></td>
</tr>
<tr class="even">
<td><p>MyContactInformation</p></td>
<td><p>I ruoli di gestione <code>MyContactInformation</code> consentono ai singoli utenti di modificare le relative informazioni di contatto, compresi l'indirizzo e i numeri di telefono.</p></td>
</tr>
<tr class="odd">
<td><p>MyDistributionGroupMembership</p></td>
<td><p>I ruoli di gestione <code>MyDistributionGroupMembership</code> consentono ai singoli utenti di visualizzare e modificare l'appartenenza ai gruppi di distribuzione in un'organizzazione, purché tali gruppi di distribuzione permettano di cambiare l'appartenenza a un gruppo.</p></td>
</tr>
<tr class="even">
<td><p>MyDistributionGroups</p></td>
<td><p>I ruoli di gestione <code>MyDistributionGroups</code> consentono ai singoli utenti di creare, modificare e visualizzare gruppi di distribuzione e di modificare, visualizzare, rimuovere e aggiungere membri ai relativi gruppi di distribuzione a cui appartengono.</p></td>
</tr>
<tr class="odd">
<td><p>MyMailSubscription</p></td>
<td><p>Il ruolo <code>MyMailSubscription</code> consente ai singoli utenti di visualizzare e modificare le impostazioni di sottoscrizione per la posta elettronica come il formato per i messaggi e le impostazioni predefinite di protocollo.</p></td>
</tr>
<tr class="even">
<td><p>MyProfileInformation</p></td>
<td><p>Il ruolo di gestione <code>MyProfileInformation</code> consente a singoli utenti di modificare il proprio nome.</p></td>
</tr>
<tr class="odd">
<td><p>MyRetentionPolicies</p></td>
<td><p>I ruoli di gestione <code>MyRetentionPolicies</code> consentono ai singoli utenti di visualizzare tag di conservazione e di visualizzare e modificare i valori predefiniti e le relative impostazioni.</p></td>
</tr>
<tr class="even">
<td><p>MyTextMessaging</p></td>
<td><p>Il ruolo di gestione <code>MyTextMessaging</code> consente ai singoli utenti di creare, visualizzare e modificare le impostazioni dei messaggi di testo.</p></td>
</tr>
<tr class="odd">
<td><p>MyVoiceMail</p></td>
<td><p>I ruoli di gestione <code>MyVoiceMail</code> consentono ai singoli utenti di visualizzare e modificare le impostazioni della casella vocale.</p></td>
</tr>
<tr class="even">
<td><p>App ReadWriteMailbox personali</p></td>
<td><p>Il ruolo di gestione <code>My ReadWriteMailbox Apps</code> consente agli utenti di installare le app con autorizzazioni ReadWriteMailbox.</p></td>
</tr>
<tr class="odd">
<td><p>App personalizzate</p></td>
<td><p>Il ruolo di gestione <code>My Custom Apps</code> consente agli utenti di visualizzare e modificare le app personalizzate.</p></td>
</tr>
</tbody>
</table>

