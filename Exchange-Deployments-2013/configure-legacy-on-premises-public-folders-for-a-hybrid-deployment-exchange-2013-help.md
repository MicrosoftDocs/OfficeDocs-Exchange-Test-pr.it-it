---
title: 'Configurare cartelle pubbliche locali legacy per una distribuzione ibrida: Exchange 2013 Help'
TOCTitle: Configurare cartelle pubbliche locali legacy per una distribuzione ibrida
ms:assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn249373(v=EXCHG.150)
ms:contentKeyID: 54913120
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurare cartelle pubbliche locali legacy per una distribuzione ibrida

 

_<strong>Si applica a:</strong>Exchange Online, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2018-05-22_

**Riepilogo:**  utilizzare la procedura descritta in questo articolo per sincronizzare le cartelle pubbliche tra Office 365 e la distribuzione locale di Exchange 2007 o Exchange 2010.

In una distribuzione ibrida, gli utenti possono trovarsi in Exchange Online, in locale o in entrambe le posizioni mentre le cartelle pubbliche possono trovarsi in Exchange Online o in locale. Le cartelle pubbliche possono risiedere in un'unica posizione, pertanto è necessario decidere se devono trovarsi in Exchange Online o in locale, non possono occupare entrambe le posizioni. Le cassette postali delle cartelle pubbliche sono sincronizzate con Exchange Online tramite il servizio Sincronizzazione delle directory. Le cartelle pubbliche abilitate alla posta, però, non sono sincronizzate tra le strutture locali.

In questo argomento viene indicato come sincronizzare le cartelle pubbliche abilitate alla posta quando gli utenti si trovano in Office 365 e le cartelle pubbliche di Exchange 2010 SP3 o Exchange 2007 SP3 RU10 sono in locale. Tuttavia, un utente di Office 365 che non è rappresentato da un oggetto MailUser locale (da locale alla gerarchia della struttura delle cartelle pubbliche di destinazione) non sarà in grado di accedere alle cartelle pubbliche locali di Exchange 2013 o legacy.


> [!NOTE]
> Nell'ambito di questo argomento i server Exchange 2010 SP3 e Exchange 2007 SP3 RU10 vengono definiti <EM>server Exchange legacy</EM>.



Per sincronizzare le cartelle pubbliche abilitate alla posta è necessario utilizzare i seguenti script, che vengono avviati da un'attività di Windows in esecuzione nell'ambiente locale:

1.  `Sync-MailPublicFolders.ps1`   Questo script sincronizza gli oggetti delle cartelle pubbliche abilitate alla posta elettronica della distribuzione locale di Exchange con Office 365. Utilizza la distribuzione locale di Exchange come master per determinare le modifiche necessarie da applicare a O365. Lo script crea, aggiorna o elimina gli oggetti delle cartelle pubbliche abilitate alla posta elettronica su O365 Active Directory in base agli elementi esistenti nella distribuzione di Exchange locale.

2.  `SyncMailPublicFolders.strings.psd1`   File di supporto utilizzato dallo script di sincronizzazione precedente che deve essere copiato nello stesso percorso dello script precedente.

Al termine della procedura, gli utenti locali e di Office 365 saranno in grado di accedere alla stessa infrastruttura di cartelle pubbliche locale.

## Versioni ibride di Exchange che funzioneranno con le cartelle pubbliche

Nella seguente tabella vengono descritte le combinazioni di versione e percorso delle cassette postali degli utenti e delle cartelle pubbliche supportate. Lo scenario per cui è indicato "Ibrida non applicabile" è comunque uno scenario supportato ma non viene considerato uno scenario ibrido perché le cartelle pubbliche e gli utenti risiedono nella stessa posizione.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>   </th>
<th>Cassetta postale utente di Exchange 2007 o Exchange 2010 locale</th>
<th>Cassetta postale utente di Exchange 2013 locale</th>
<th>Cassetta postale utente di Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cartelle pubbliche di Exchange 2007 o Exchange 2010 locale</p></td>
<td><p>Ibrida non applicabile</p></td>
<td><p>Ibrida non applicabile</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="even">
<td><p>Cartelle pubbliche di Exchange 2013 locale</p></td>
<td><p>Ibrida non applicabile</p></td>
<td><p>Ibrida non applicabile</p></td>
<td><p>Supportato</p></td>
</tr>
<tr class="odd">
<td><p>Cartelle pubbliche di Exchange Online</p></td>
<td><p>Non supportato</p></td>
<td><p>Supportato</p></td>
<td><p>Ibrida non applicabile</p></td>
</tr>
</tbody>
</table>


La configurazione ibrida con le cartelle pubbliche di Exchange 2013 non è supportata. Se nell'organizzazione si esegue Exchange 2013, è necessario spostare tutti i database e le repliche delle cartelle pubbliche in Exchange 2007 SP3 RU10 o versione successiva. Nessuna replica di cartelle pubbliche può essere lasciata su Exchange 2003.


> [!NOTE]
> Outlook 2016 non supporta l'accesso alle cartelle pubbliche legacy di Exchange 2007. Se sono presenti utenti che hanno Outlook 2016, sarà necessario spostare le cartelle pubbliche su una versione più recente di Exchange. Ulteriori informazioni sulla compatibilità di Outlook 2016 e Office 2016 con Exchange 2007 e le versioni precedenti sono disponibili in <A href="https://go.microsoft.com/fwlink/p/?linkid=849053">questo articolo</A>.



## Passaggio 1: Che cosa è necessario sapere prima di iniziare

1.  Per queste istruzioni si presume che sia stata utilizzata la procedura guidata di configurazione ibrida per configurare e sincronizzare gli ambienti locale e Exchange Online e che i record DNS utilizzati per il servizio di individuazione automatica della maggior parte degli utenti faccia riferimento a un endpoint locale. Per ulteriori informazioni, vedere [Procedura guidata di configurazione ibrida](hybrid-configuration-wizard-exchange-2013-help.md).

2.  Per queste istruzioni si presume che Outlook via Internet sia abilitato e funzionale sui server Exchange legacy locali. Per informazioni su come abilitare Outlook via Internet, vedere [Outlook via Internet](https://technet.microsoft.com/it-it/library/bb123741\(v=exchg.150\)).

3.  L'implementazione della coesistenza delle cartelle pubbliche legacy per una distribuzione ibrida di Exchange con Office 365 potrebbe richiedere la risoluzione di conflitti durante la procedura di importazione. I conflitti possono verificarsi a causa di indirizzi di posta elettronica non instradabili assegnati a cartelle pubbliche abilitate alla posta, conflitti con altri utenti e gruppi in Office 365 e altri attributi.

4.  Per queste istruzioni si presume che l'organizzazione Exchange Online sia stata aggiornata a una versione che supporta le cartelle pubbliche.

5.  In Exchange Online, è necessario essere un membro del gruppo di ruoli Gestione organizzazione. Questo gruppo di ruoli differisce dalle autorizzazioni assegnate in fase di sottoscrizione a Exchange Online. Per informazioni dettagliate sull'abilitazione del gruppo di ruoli Gestione organizzazione, vedere [Gestire gruppi di ruoli](https://technet.microsoft.com/it-it/library/jj657480\(v=exchg.150\)).

6.  In Exchange 2010, è necessario essere un membro del gruppo di ruoli RBAC Gestione organizzazione o Gestione server. Per i dettagli, vedere [Add Members to a Role Group](https://go.microsoft.com/fwlink/?linkid=299212).

7.  In Exchange 2007, è necessario essere assegnati al ruolo di amministratore dell'organizzazione Exchange o di amministratore server di Exchange. Inoltre, è necessario essere assegnati al ruolo Amministratore cartelle pubbliche e al gruppo Amministratori locale per il server di destinazione. Per i dettagli, vedere [Aggiunta di un utente o di un gruppo a un ruolo di amministratore](https://go.microsoft.com/fwlink/p/?linkid=81779)

8.  Se Exchange Server 2007 è in esecuzione su Windows Server 2008 x64, è necessario eseguire l'aggiornamento a [Windows PowerShell 2.0 e WinRM 2.0 per Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930). Se Exchange Server 2007 è in esecuzione su Windows Server 2003 x64, è necessario eseguire l'aggiornamento a Windows PowerShell 2.0. Per ulteriori informazioni, vedere [Aggiornamento per Windows Server 2003 x64 Edition (KB968930)](https://www.microsoft.com/it-it/download/details.aspx?id=10512)..

9.  Per accedere alle cartelle pubbliche in più strutture locali, è necessario aggiornare i relativi client Outlook con l'aggiornamento pubblico di Outlook di novembre 2012 o successivo.
    
    1.  Per scaricare l'aggiornamento di novembre 2012 per Outlook 2010, vedere [Aggiornamento per Microsoft Outlook 2010 (KB2687623) Versione a 32 bit](https://www.microsoft.com/it-it/download/details.aspx?id=35702).
    
    2.  Per scaricare l'aggiornamento di novembre 2012 per Outlook 2007, vedere [Aggiornamento per Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/it-it/download/details.aspx?id=35718).

10. Outlook 2016 per Mac (e versioni precedenti) e Outlook per Mac per Office 365 non sono supportati per cartelle pubbliche cross-premise legacy. Per accedere alle cartelle pubbliche con Outlook per Mac o Outlook per Mac per Office 365, il percorso delle cartelle deve corrispondere a quello degli utenti. Inoltre, gli utenti le cui cassette postali sono in Exchange Online non saranno in grado di accedere alle cartelle pubbliche locali tramite Outlook Web App.

11. Dopo aver seguito le istruzioni di questo articolo che consentono di configurare le cartelle pubbliche locali per una distribuzione ibrida, gli utenti esterni all'organizzazione non saranno in grado di inviare messaggi a tali cartelle pubbliche, a meno che non si effettuino altre procedure. È possibile impostare il dominio accettato per le cartelle pubbliche su Inoltro interno (vedere [Gestione dei domini accettati in Exchange Online](https://technet.microsoft.com/it-it/library/jj945194\(v=exchg.150\)) per maggiori informazioni) oppure disabilitare DBEB (Directory Based Edge Blocking), come descritto in [Utilizzare il blocco Edge basato su directory per rifiutare i messaggi inviati a destinatari non validi](https://technet.microsoft.com/it-it/library/dn600322\(v=exchg.150\)).

## Passaggio 2: Rilevabilità delle cartelle pubbliche remote

1.  Se le cartelle pubbliche si trovano su server Exchange 2010 o versioni successive, è necessario installare il ruolo server Accesso client su tutti i server Cassette postali che contengono un database di cartelle pubbliche. In tal modo, il servizio RpcClientAccess di Microsoft Exchange potrà essere eseguito permettendo a tutti i client di accedere alle cartelle pubbliche. Il ruolo Accesso client non è richiesto per i server di cartelle pubbliche Exchange 2007 e questo passaggio non è necessario. Per ulteriori informazioni, vedere [Install Exchange Server 2010](https://technet.microsoft.com/it-it/library/bb124778\(v=exchg.141\).aspx). Questo passaggio non è necessario per le cartelle pubbliche di Exchange 2007.
    

    > [!NOTE]
    > Il server non deve essere parte del bilanciamento del carico di Accesso client. Per ulteriori informazioni, vedere <A href="https://technet.microsoft.com/it-it/library/ff625247(v=exchg.141).aspx">Understanding Load Balancing in Exchange 2010</A>.



2.  Creare un database delle cassette postali vuoto su ogni server di cartelle pubbliche.
    
    Per Exchange 2010, utilizzare il seguente comando. Questo comando esclude il database delle cassette postali dal sistema di bilanciamento del carico di provisioning delle cassette postali. In tal modo si impedisce l'aggiunta automatica di nuove cassette postali a questo database.
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true
    
    Per Exchange 2007, utilizzare il seguente comando:
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    

    > [!NOTE]
    > L'unica cassetta postale aggiunta a questo database deve essere la cassetta postale proxy creata al passaggio 3. Nessun'altra cassetta postale deve essere creata in questo database delle cassette postali.



3.  Creare una cassetta postale proxy nel nuovo database delle cassette postali e nascondere la cassetta postale dalla rubrica. L'SMTP di questa cassetta postale sarà restituito da Individuazione automatica come SMTP di *DefaultPublicFolderMailbox*, cosicché risolvendo questo SMTP il client può raggiungere il server Exchange legacy per l'accesso alle cartelle pubbliche.
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs>
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  Per Exchange 2010, abilitare Individuazione automatica per la restituzione delle cassette postali delle cartelle pubbliche proxy. Questo passaggio non è necessario per Exchange 2007.
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  Ripetere la procedura precedente per ogni server di cartelle pubbliche dell'organizzazione.

## Passaggio 3: Download degli script

1.  Scaricare i seguenti file da [Cartelle pubbliche abilitate alla posta elettronica - script di sincronizzazione delle directory](https://www.microsoft.com/it-it/download/details.aspx?id=46381):
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  Salvare i file nel computer locale da cui si eseguirà PowerShell. Ad esempio, C:\\PFScripts.

## Passaggio 4: Configurazione della sincronizzazione delle directory

Il servizio di sincronizzazione delle directory non sincronizza le cartelle pubbliche abilitate alla posta. Per sincronizzazione le cartelle pubbliche abilitate alla posta tra le strutture locali è necessario eseguire lo script seguente. Le autorizzazioni speciali assegnate alle cartelle pubbliche abilitate alla posta elettronica dovranno essere ricreate nel cloud poiché le autorizzazioni cross-premise non sono supportate negli scenari di distribuzione ibrida. Per ulteriori informazioni, vedere [Exchange hybrid deployment documentation](exchange-server-hybrid-deployments-exchange-2013-help.md).


> [!NOTE]
> Le cartelle pubbliche abilitate alla posta elettronica sincronizzate verranno visualizzate come oggetti contatto di posta per motivi di flusso di posta e non saranno visualizzabili nell'Interfaccia di amministrazione di Exchange. Vedere il comando Get-MailPublicFolder. Per ricreare le autorizzazioni SendAs nel cloud, utilizzare il comando Add-RecipientPermission.



1.  Nel server Exchange legacy, eseguire il seguente comando per sincronizzare le cartelle pubbliche abilitate alla posta dalla versione locale di Active Directory a O365.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` indica password e nome utente di Office 365 e `CsvSummaryFile` il percorso in cui si desidera registrare gli errori e le operazioni di sincronizzazione, in formato .csv.


> [!NOTE]
> Prima di eseguire lo script, si consiglia di simulare le operazioni che verrebbero effettuate dallo script nell'ambiente eseguendolo come descritto in precedenza con il parametro <CODE>-WhatIf</CODE>.<BR>Si consiglia inoltre di eseguire questo script ogni giorno per sincronizzare le cartelle pubbliche abilitate alla posta.



## Passaggio 5: Configurazione degli utenti di Exchange Online per l'accesso alle cartelle pubbliche locali

Mediante il passaggio finale di questa procedura, è possibile configurare l'organizzazione Exchange Online e consentire l'accesso alle cartelle pubbliche locali legacy.

Abilitare l'organizzazione Exchange Online per l'accesso alle cartelle pubbliche locali. Puntare a tutte le cassette postali delle cartelle pubbliche proxy create in Passaggio 2: Rilevabilità delle cartelle pubbliche remote.

Eseguire il comando indicato di seguito in **Windows PowerShell**:

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

Per visualizzare le modifiche è necessario attendere che la sincronizzazione di ActiveDirectory sia completa. Questo processo può richiedere fino a 3 ore. Se non si desidera attendere che si verifichino le sincronizzazioni ricorrenti ogni 3 ore, è possibile forzare la sincronizzazione delle directory in qualsiasi momento. Per istruzioni dettagliate per forzare la sincronizzazione delle directory, vedere [Forzare la sincronizzazione delle directory](http://technet.microsoft.com/it-it/library/jj151771.aspx). In Office 365 viene selezionata in modo casuale una delle cassette postali delle cartelle pubbliche fornite con questo comando.


> [!IMPORTANT]
> Un utente di Office 365 che non è rappresentato da un oggetto MailUser locale (da locale alla gerarchia della struttura delle cartelle pubbliche di destinazione) non sarà in grado di accedere alle cartelle pubbliche locali di Exchange 2013 o legacy. Per risolvere il problema, vedere l'articolo della Knowledge Base <A href="https://go.microsoft.com/fwlink/p/?linkid=699451">Gli utenti di Exchange Online non possono accedere alle cartelle pubbliche locali legacy</A>.



## Come verificare se l'operazione ha avuto esito positivo

1.  Accedere a Outlook per un utente in Exchange Online ed effettuare i seguenti test sulle cartelle pubbliche:
    
      - Visualizzare la gerarchia.
    
      - Controllare le autorizzazioni.
    
      - Creare ed eliminare cartelle pubbliche.
    
      - Pubblicare il contenuto ed eliminare il contenuto da una cartella pubblica.

## Nuovo utente di Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Piccola icona per LinkedIn Learning" alt="Piccola icona per LinkedIn Learning" /> <strong>Nuovo utente di Office 365?</strong><br />
Sono disponibili esercitazioni video gratuite per <a href="https://support.office.com/it-it/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> grazie a LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

