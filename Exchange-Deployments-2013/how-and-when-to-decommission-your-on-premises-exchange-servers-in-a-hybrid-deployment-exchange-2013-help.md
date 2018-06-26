---
title: 'Modalità e tempistica di rimozione dei server locali di Exchange in una distribuzione ibrida: Exchange 2013 Help'
TOCTitle: Modalità e tempistica di rimozione dei server locali di Exchange in una distribuzione ibrida
ms:assetid: 4f884b7a-3b8a-4207-8843-65d3141731dc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn931280(v=EXCHG.150)
ms:contentKeyID: 65015121
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modalità e tempistica di rimozione dei server locali di Exchange in una distribuzione ibrida

 

_<strong>Si applica a:</strong>Exchange Online, Exchange Server, Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2017-07-27_

Se si è pronti passare da una distribuzione ibrida di Exchange ibrida a un'implementazione cloud completa, leggere questo articolo.

Una delle opzioni più conveniente per ottenere una società per Exchange Online consiste nell'utilizzare il metodo di distribuzione ibrida descritto in [distribuzione ibrida di Exchange e la migrazione a Office 365](https://msdn.microsoft.com/en-us/library/ff633682\(v=exchsrvcs.149\).aspx). Questo è l'unica opzione che consente alle cassette postali di bordo e facilmente off Consiglio (tutte le altre opzioni native sono bordo solo). Oltre alla possibilità di disattivare area, una configurazione ibrida presenta le seguenti opzioni principali.

In questo argomento consentono di acquisire familiarità con le opzioni per la rimozione delle autorizzazioni di Exchange hybrid e deve essere implementata quando ognuna di queste opzioni. Esistono molti scostamenti quando e come rimuovere il server ibridi Exchange. Il tempo dedicato a comprendere le implicazioni e pianificare correttamente la rimozione completa o parziale del server locale è importante.

  - **Disponibilità cross-premise**. Consente di visualizzare le informazioni di disponibilità di un utente quando si pianifica una riunione, a prescindere dalla posizione delle cassette postali.

  - **Archivio cross-premise**. Consente a un cliente di spostare nel cloud soltanto la cassetta postale dell'utente. Tale opzione rappresenta il primo passo, per gli utenti, per provare Office 365 e, in particolare, Exchange Online.

  - **Ricerche di individuazione cross-premise**. Consente al cliente di eseguire una ricerca E-discovery che eseguirà una ricerca per indicizzazione delle cassette postali e degli archivi in entrambi gli ambienti locali (tale opzione richiede che sia configurata l'autenticazione OAuth).

  - **Outlook Web App Reindirizzamento URL**. Consente di reindirizzare gli utenti agli ambienti locali adeguati per accedere a Outlook Web App.

  - **Non è necessario ricreare il profilo dopo lo spostamento**. A differenza di altre opzioni di migrazione, il GUID della cassetta postale non cambia. Ciò significa che non è necessario ricreare il profilo o scaricare di nuovo l'OST dopo aver spostato una cassetta postale.

A seconda delle esigenze dell'organizzazione, la distribuzione ibrida rappresenta la migliore opzione per fornire un'esperienza utente e di coesistenza senza problemi.

## Altri metodi per eseguire la migrazione a Exchange Online

Una distribuzione ibrida non è disponibile per tutti gli utenti; in realtà sono in genere migliori opzioni. Molti dei tenant che decide di distribuire una configurazione ibrida sono postazioni in cinquanta. Sebbene possa sembrare interessante per l'elenco dei vantaggi di una distribuzione ibrida, è dotato di un prezzo hefty per quanto riguarda la complessità. Alcuni dei più piccole tenant richiedono le caratteristiche di una distribuzione ibrida, ma, per la maggior parte dei tenant, sarebbe utilizzare entrambi una completa, migliorate in fasi, o l'opzione di migrazione IMAP. Non esiste un programma denominato FastTrack è possibile utilizzare quando si sceglie l'approccio alla migrazione da eseguire. Nella [pagina di Office 365 FastTrack](https://go.microsoft.com/fwlink/?linkid=846696)sono riportate informazioni su FastTrack.

Utilizzare la tabella seguente per decidere il tipo di migrazione può essere utilizzato per l'organizzazione. (Per ulteriori informazioni, vedere [modi per eseguire la migrazione di più account di posta elettronica a Office 365](https://support.office.com/en-us/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842?ui=en-us%26rs=en-sg%26ad=sg))


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Organizzazione esistente</th>
<th>Numero di cassette postali di cui eseguire la migrazione</th>
<th>Gestione degli account utente nell'organizzazione locale</th>
<th>Tipo di migrazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013, Exchange 2010, Exchange 2007 o Exchange 2003</p></td>
<td><p>Meno di 2.000</p></td>
<td><p>No</p></td>
<td><p>Migrazione completa di Exchange</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007 oppure Exchange 2003</p></td>
<td><p>Meno di 2.000</p></td>
<td><p>No</p></td>
<td><p>Migrazione di Exchange in fasi</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2007 oppure Exchange 2003</p></td>
<td><p>Più di 2.000 cassette postali*</p></td>
<td><p>Sì</p></td>
<td><p>Migrazione di Exchange in fasi o migrazione di spostamento remoto in una distribuzione ibrida di Exchange</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 oppure Exchange 2010</p></td>
<td><p>Più di 2.000 cassette postali*</p></td>
<td><p>Sì</p></td>
<td><p>Migrazione di spostamento remoto in una distribuzione ibrida di Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2000 Server o versioni precedenti</p></td>
<td><p>Illimitato</p></td>
<td><p>Sì</p></td>
<td><p>Migrazione IMAP</p></td>
</tr>
<tr class="even">
<td><p>Sistema di messaggistica locale non Exchange</p></td>
<td><p>Illimitato</p></td>
<td><p>Sì</p></td>
<td><p>Migrazione IMAP</p></td>
</tr>
</tbody>
</table>


\* Alcune organizzazioni con meno di 2.000 cassette postali possono usufruire di caratteristiche e funzionalità che sono disponibili solo con una distribuzione ibrida. È importante valutare con attenzione i vantaggi di una distribuzione ibrida con la complessità che sono state introdotte. Si consiglia ai clienti con meno di 2.000 cassette postali di valutare complete o in fasi migrazione prima di procedere con una distribuzione ibrida.

## Motivi per non rimuovere i server di Exchange dall'ambiente locale

Spesso, i clienti che utilizzano una configurazione ibrida notano che dopo un periodo di tempo tutte le loro cassette postali vengono spostate in Exchange Online. A questo punto, possono decidere di rimuovere i server Exchange dall'ambiente locale. Tuttavia, scoprono di non essere più in grado di gestire le cassette postali presenti nel cloud.

Quando per un tenant è attivata la sincronizzazione della directory e un utente viene sincronizzato dall'ambiente locale, Exchange Online non è in grado di gestire la maggior parte degli attributi, che pertanto devono essere gestiti in locale. Questo comportamento non è causato dalla configurazione ibrida, ma si verifica a causa della sincronizzazione della directory. Inoltre, anche se si dispone della sincronizzazione della directory senza che sia in esecuzione la configurazione ibrida guidata, non è comunque possibile gestire la maggior parte delle attività dei destinatari dal cloud. Per ulteriori informazioni, vedere questo [blog TechNet](http://blogs.technet.com/b/exchange/archive/2012/12/05/decommissioning-your-exchange-2010-servers-in-a-hybrid-deployment.aspx).

## È possibile utilizzare gli strumenti di gestione di terze parti?

Viene chiesto spesso se è possibile utilizzare gli strumenti di gestione di terze parti oppure ADSIEDIT. La risposta è che è possibile utilizzarli, ma è necessario tenere presente che non sono supportati. Exchange Management Console, Interfaccia di amministrazione di Exchange (EAC) ed Exchange Management Shell sono gli unici strumenti supportati, disponibili per gestire gli oggetti e i destinatari di Exchange. La decisione di utilizzare strumenti di gestione di terze parti è a proprio rischio. Gli strumenti di gestione di terze parti spesso funzionano correttamente, ma Microsoft non li approva.

## Scenari comuni

Il passaggio da una configurazione ibrida al cloud può causare problemi. La procedura per passare a una configurazione ibrida senza errori ha richiesto molto tempo. Sebbene vi siano dei problemi, è stato fatto un buon lavoro per trasformare questo passaggio quasi impossibile in una procedura guidata abbastanza semplice.

Tuttavia, lo sforzo per consentire agli utenti di passare da configurazione ibrida al solo cloud è stato minimo. A seconda degli obiettivi immediati, il processo può essere eseguito senza problemi, grazie ad alcune indicazioni. Di seguito sono riportati tre scenari ibridi comuni e i consigli per soddisfare l’obiettivo finale del cliente.

Dal momento che la base clienti delle soluzioni ibride è molto diversificata, è difficile riunirla in scenari "comuni". Di seguito vengono forniti alcuni scenari di alto livello per la rimozione di Exchange Server a livello locale. Nel leggere questi scenari e nel dare forma a un piano di rimozione, sarà necessario determinare lo scenario più adeguato alle proprie esigenze.

## Scenario uno

**Problema:** organizzazione è in esecuzione in una configurazione ibrida e disponibile tutte la cassette postali in Exchange Online. È possibile non è necessario gestire gli utenti in locale e non è più necessario per la sincronizzazione delle directory o la sincronizzazione delle password.

**Soluzione:** dal momento che tutti gli utenti verranno gestiti in Office 365 e la sincronizzazione della directory non più necessaria, è possibile disattivare questa funzionalità e rimuovere Exchange dall'ambiente locale.

![Rimozione di Exchange dall'ambiente locale](images/Dn931280.f9c2a2cb-4c16-4ca3-8244-b89c1cdf0744(EXCHG.150).jpg "Rimozione di Exchange dall'ambiente locale") Per disattivare la sincronizzazione della directory e disinstallare la configurazione ibrida di Exchange

1.  Eseguire `Get-OrganizationConfig |fl PublicFoldersEnabled` e assicurarsi che non è impostata su Remote. Se è impostato su Remote e le cartelle pubbliche sono un elemento che si desidera continuare ad accedere, è necessario eseguirne la migrazione a Exchange Online. Per ulteriori informazioni, vedere [Utilizzare la migrazione batch delle cartelle pubbliche legacy a Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/dn874017\(v=exchg.150\)).

2.  Supponendo che tutte le cassette postali siano state già spostate in Exchange Online, è possibile puntare i record MX e DNS di individuazione automatica a Exchange Online invece che all’ambiente locale. Per ulteriori informazioni, vedere [Riferimenti: record DNS esterni per Office 365](http://technet.microsoft.com/it-it/library/hh852557.aspx).
    

    > [!IMPORTANT]
    > Accertarsi di aver aggiornato sia il DNS interno che quello esterno. In caso contrario, potrebbero verificarsi connessioni instabili.



3.  Successivamente, è necessario rimuovere i valori relativi al punto di connessione del servizio dai server di Exchange. In questo modo non vengono restituiti punti di connessione del servizio. Al contrario, il client utilizzerà il metodo DNS per l'individuazione automatica. Di seguito è riportato un esempio:
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    

    > [!NOTE]
    > Se nel proprio ambiente sono disponibili server di Exchange&nbsp;2007, sarà necessario eseguire un comando analogo nei server di Exchange 2007, al fine di annullare le impostazioni.



4.  Se si desidera eliminare i connettori in ingresso e in uscita creati durante la configurazione ibrida guidata, eseguire la procedura seguente:
    
    1.  Accedere al [portale di amministrazione di Office 365](http://portal.office.com) ed effettuare l'accesso come amministratore tenant.
    
    2.  Selezionare l'opzione per gestire **Exchange**.
    
    3.  Passare a **Flusso della posta** -\> **Connessione**.
    
    4.  A questo punto, è possibile disabilitare o eliminare i connettori in ingresso e in uscita. La configurazione ibrida guidata crea connettori con spazio dei nomi univoco **in ingresso da \<identificatore univoco\>** e **in uscita da \<identificatore univoco\>**, come illustrato nell'immagine seguente.
        
        ![La procedura guidata per la configurazione ibrida consente di creare connettori con uno spazio dei nomi univoco](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "La procedura guidata per la configurazione ibrida consente di creare connettori con uno spazio dei nomi univoco")  

5.  Rimuovere la relazione organizzativa creata dalla configurazione ibrida guidata. Eseguire la procedura seguente:
    
    1.  Accedere al [portale di amministrazione di Office 365](http://portal.office.com) ed effettuare l'accesso come amministratore tenant.
    
    2.  Selezionare l'opzione per gestire Exchange.
    
    3.  Accedere a **Organizzazione**.
    
    4.  In **Condivisione organizzazione**, rimuovere l'organizzazione denominata **Da O365 a On-Premises– \<identificatore univoco\>**, come illustrato nell'immagine seguente.
        
        ![Rimuovere la relazione organizzativa creata dalla procedura guidata per la configurazione ibrida.](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "Rimuovere la relazione organizzativa creata dalla procedura guidata per la configurazione ibrida.")  

6.  Se OAuth è configurato per una distribuzione ibrida di Exchange, è necessario disabilitare la configurazione dall'ambiente locale e da Office 365. Nella maggior parte degli ambienti, è possibile ignorare questa procedura poiché soltanto un piccolo gruppo di clienti dispone di OAuth configurato.
    
    Per disattivare la configurazione locale:
    
    1.  Da un server di Exchange 2013, aprire Exchange Management Shell.
    
    2.  Eseguire il comando seguente:
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Per disabilitare la configurazione di Exchange Online:
    
    1.  Connettere Windows PowerShell a Exchange Online.
    
    2.  Eseguire il comando seguente:
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        Il parametro *Identity* presuppone che per configurare OAuth sia stata utilizzata la configurazione ibrida guidata. In caso contrario, potrebbe essere necessario regolare il valore specificato per l'identità dei connettori.

7.  Disattivare la sincronizzazione della directory per i tenant. Al termine di questo passaggio, tutte le attività di gestione utenti verranno eseguite dagli strumenti di gestione di Office 365. Ciò significa che non si utilizzerà più Exchange Management Console o Interfaccia di amministrazione di Exchange. Per ulteriori informazioni su come disattivare la sincronizzazione della directory, vedere [Disattivare la sincronizzazione della directory](https://technet.microsoft.com/it-it/library/dn144760.aspx).

8.  A questo punto, è possibile disinstallare in modo sicuro Exchange dai server locali.

## Scenario due

**Problema:** da un anno l'organizzazione esegue una configurazione ibrida e ora anche l'ultima cassetta postale è stata spostata sul cloud. Tuttavia, si pensa di mantenere i servizi AD FS per eseguire l'autenticazione utente delle cassette postali Exchange Online degli utenti (questo scenario è valido per tutti i clienti che intendono mantenere la sincronizzazione della directory).

**Soluzione:** dal momento che il cliente intende mantenere i servizi AD FS, conserverà anche la sincronizzazione della directory poiché è un prerequisito di tali servizi. Per questo motivo, non è possibile rimuovere completamente i server di Exchange dall'ambiente locale. Tuttavia, è possibile rimuovere la maggior parte dei server di Exchange lasciandone qualcuno per la gestione degli utenti. Tenere presente che i server lasciati in esecuzione possono essere eseguiti su macchine virtuali, dal momento che il carico di lavoro passa quasi completamente a Exchange Online.

Nell'immagine seguente viene descritto lo stato finale desiderato:

![Rimozione di una parte dei server di Exchange](images/Dn931280.d7734579-6999-45b2-9a0f-a23f18353a49(EXCHG.150).jpg "Rimozione di una parte dei server di Exchange")

Nell'immagine seguente viene descritto lo stato finale effettivo:

![Stato precedente alla rimozione dei server di Exchange](images/Dn931280.c692f0af-6536-4bc9-950d-58a1e486525f(EXCHG.150).jpg "Stato precedente alla rimozione dei server di Exchange") Per mantenere AD FS e la sincronizzazione della directory e rimuovere la maggior parte dei server di Exchange

1.  Eseguire `Get-OrganizationConfig |fl PublicFoldersEnabled` e assicurarsi che non sia impostato su Remoto. Se è impostato su Remoto e si desidera continuare ad accedere alle cartelle pubbliche, è necessario eseguire la migrazione delle cartelle a Exchange Online. Per informazioni su come eseguire questa operazione, vedere [Utilizzare la migrazione batch delle cartelle pubbliche legacy a Office 365 ed Exchange Online](https://technet.microsoft.com/it-it/library/dn874017\(v=exchg.150\)).
    

    > [!IMPORTANT]
    > Se la migrazione delle cartelle pubbliche a Exchange Online non è un'opzione e tali cartelle sono comunque necessarie per gli utenti, interrompere la procedura.



2.  Dopo aver spostato tutte le cassette postali in Exchange Online, la prima cosa da fare per rimuovere la maggior parte dei server di Exchange consiste nel puntare i record MX e DNS di individuazione automatica a Exchange Online invece che all'ambiente locale Per ulteriori informazioni, vedere [Riferimenti: record DNS esterni per Office 365](http://technet.microsoft.com/it-it/library/hh852557.aspx).
    

    > [!IMPORTANT]
    > Accertarsi di aver aggiornato sia il DNS interno che quello esterno. In caso contrario, potrebbero verificarsi connessioni e flusso di posta instabili.



3.  Successivamente, è necessario rimuovere i valori relativi al punto di connessione del servizio dai server di Exchange. In questo modo non vengono restituiti punti di connessione del servizio. Al contrario, il client utilizzerà il metodo DNS per l'individuazione automatica. Di seguito è riportato un esempio:
    
        Get-ClientAccessServer | Set-ClientAccessServer -AutoDiscoverServiceInternalUri $Null
    

    > [!NOTE]
    > Se nel proprio ambiente sono disponibili server di Exchange&nbsp;2007, è necessario eseguire un comando analogo nei server di Exchange 2007, al fine di annullare le impostazioni



4.  Per evitare che gli oggetti della configurazione ibrida vengano creati di nuovo in futuro, è necessario rimuovere l’oggetto della configurazione ibrida da Active Directory. A tal fine, aprire Exchange Management Shell ed effettuare le operazioni seguenti:
    
        Remove-HybridConfiguration

5.  Rimuovere tutti i server di Exchange tranne quelli che devono essere mantenuti per la gestione e la creazione degli utenti. Due server sono sufficienti per la gestione degli utenti, sebbene sia possibile effettuare tali operazioni con un solo server. Inoltre, non è necessario disporre di un gruppo di disponibilità del database o di altre opzioni di disponibilità elevata.

6.  Se OAuth è configurato per una distribuzione ibrida di Exchange, è necessario disabilitare la configurazione dall'ambiente locale e da Office 365. Nella maggior parte degli ambienti, è possibile ignorare questa procedura poiché soltanto un piccolo gruppo di clienti dispone di OAuth configurato.
    
    Per disattivare la configurazione locale:
    
    1.  Da un server di Exchange 2013, aprire Exchange Management Shell.
    
    2.  Eseguire il comando seguente:
        
            Get-IntraorganizationConnector -Identity ExchangeHybridOnPremisesToOnline | Set-IntraOrganizationConnector -Enabled $False
    
    Per disabilitare la configurazione di Exchange Online:
    
    1.  Connettere Windows PowerShell a Exchange Online.
    
    2.  Eseguire il comando seguente:
        
            Run Get-IntraorganizationConnector -Identity ExchangeHybridOnlineToOnPremises | Set-IntraOrganizationConnector -Enabled $False
        
        Il parametro Identity presuppone che per configurare OAuth sia stata utilizzata la configurazione ibrida guidata. In caso contrario, potrebbe essere necessario regolare il valore specificato per l'identità dei connettori.

7.  Se si desidera eliminare i connettori in ingresso e in uscita creati durante la configurazione ibrida guidata, eseguire la procedura seguente:
    
    1.  Accedere al [portale di amministrazione di Office 365](http://portal.office.com) ed effettuare l'accesso come amministratore tenant.
    
    2.  Selezionare l'opzione per gestire **Exchange**.
    
    3.  Passare a **Flusso della posta** -\> **Connettori**.
    
    4.  A questo punto, è possibile disabilitare o eliminare i connettori in ingresso e in uscita. La configurazione ibrida guidata crea connettori con spazio dei nomi univoco **in ingresso da \<identificatore univoco\>** e **in uscita da \<identificatore univoco\>**, come illustrato nell'immagine seguente.
        
        ![La procedura guidata per la configurazione ibrida consente di creare connettori con uno spazio dei nomi univoco](images/Dn931280.7b1b6f0b-43d6-4407-8cd7-7dd52e016697(EXCHG.150).jpg "La procedura guidata per la configurazione ibrida consente di creare connettori con uno spazio dei nomi univoco")  

8.  Rimuovere la relazione organizzativa creata dalla configurazione ibrida guidata. Eseguire la procedura seguente:
    
    1.  Accedere al [portale di amministrazione di Office 365](http://portal.office.com) ed effettuare l'accesso come amministratore tenant.
    
    2.  Selezionare l'opzione per gestire **Exchange**.
    
    3.  Accedere a **Organizzazione**.
    
    4.  In **Condivisione organizzazione**, rimuovere l'organizzazione denominata **Da O365 a On-Premises– \<identificatore univoco\>**, come illustrato nell'immagine seguente.
        
        ![Rimuovere la relazione organizzativa creata dalla procedura guidata per la configurazione ibrida.](images/Dn931280.2f0c1077-8785-487a-87a5-a75f0a4f0fea(EXCHG.150).jpg "Rimuovere la relazione organizzativa creata dalla procedura guidata per la configurazione ibrida.")  

## Scenario tre

**Problema:** si desidera rimuovere i server locali di Exchange dopo aver spostato tutte le cassette postali in Exchange Online. Tuttavia, si è scoperto che tali cassette postali utilizzano Exchange per altri scopi, ad esempio, per l'inoltro di SMTP (Simple Mail Transfer Protocol) per un'applicazione o per accedere alle cartelle pubbliche. Se si necessita dei server locali di Exchange per soddisfare le esigenze attuali dell'organizzazione, non è consigliabile rimuovere i server locali.

**Soluzione:** si consiglia di non rimuovere Exchange e la configurazione ibrida in questa fase. Se si era in procinto di avviare il processo puntando i record di individuazione automatica a Exchange Online, alcune funzionalità sarebbero state interrotte immediatamente, ad esempio, l'accesso alla cartella pubblica ibrida. È possibile modificare il record MX in modo che punti a Exchange Online Protection Se non è stato già fatto, è possibile anche rimuovere alcuni dei server locali di Exchange. Tuttavia, è necessario mantenere un numero sufficiente di server al fine di gestire le funzioni ibride rimanenti. In genere, l'impatto sull'ambiente locale è limitato.

