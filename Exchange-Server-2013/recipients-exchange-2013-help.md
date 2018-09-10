---
title: 'Destinatari: Exchange 2013 Help'
TOCTitle: Destinatari
ms:assetid: 40300ed4-85a5-463d-bb3a-cf787bd44e9d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201680(v=EXCHG.150)
ms:contentKeyID: 50480487
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Destinatari

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Le persone e le risorse che inviano e ricevono messaggi costituiscono il nucleo di qualsiasi sistema di collaborazione e messaggistica. In un'organizzazione Exchange, tali persone e risorse sono definite *destinatari*. Un destinatario è qualsiasi oggetto abilitato alla posta in Active Directory a cui Microsoft Exchange può recapitare o instradare i messaggi.

## Tipi di destinatari di Exchange

Microsoft include diversi tipi di destinatari espliciti. Ciascun tipo di destinatario viene identificato nell'interfaccia di amministrazione di Exchange e dispone di un valore univoco nella proprietà *RecipientTypeDetails* in Exchange Management Shell. L'utilizzo di tipi di destinatari specifici presenta i seguenti vantaggi:

  - La differenza che sussiste tra i vari tipi di destinatari è immediata.

  - È possibile cercare e ordinare in base al tipo di destinatario.

  - È possibile eseguire in modo più semplice operazioni di gestione globali per i tipi di destinatario selezionati.

  - È possibile visualizzare in modo più semplice le proprietà dei destinatari in quanto Interfaccia di amministrazione di Exchange utilizza i tipi di destinatario per differenziare le pagine delle proprietà. Ad esempio, la capacità delle risorse viene visualizzata per una cassetta postale sala, ma non è presente per la cassetta postale di un utente.

Nella tabella seguente vengono elencati i tipi di destinatario disponibili. Maggiori dettagli su questi tipi di destinatari sono forniti più avanti in questo argomento.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di destinatario</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gruppo di distribuzione dinamico</p></td>
<td><p>Gruppo di distribuzione che utilizza filtri per i destinatari e condizioni per determinare la propria appartenenza al momento dell'invio dei messaggi.</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale attrezzatura</p></td>
<td><p>Una cassetta postale per la risorse assegnata a una risorsa non specifica di un luogo, quale un computer portatile, un proiettore, un microfono o un'auto aziendale. Le cassette postali attrezzatura possono essere incluse come risorse in convocazioni di riunione, offrendo un modo semplice ed efficace di utilizzare le risorse per gli utenti.</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale collegata</p></td>
<td><p>Cassetta postale assegnata a un singolo utente in una foresta trusted separata.</p></td>
</tr>
<tr class="even">
<td><p>Contatto di posta</p></td>
<td><p>Contatto di Active Directory abilitato alla posta contenente informazioni su persone e organizzazioni esistenti all'esterno di un'organizzazione Exchange. Ciascun contatto di posta dispone di un indirizzo di posta elettronica esterno. Tutti i messaggi inviati al contatto di posta vengono instradati a questo indirizzo di posta elettronica esterno.</p></td>
</tr>
<tr class="odd">
<td><p>Contatto di posta della foresta</p></td>
<td><p>Contatto di posta che rappresenta un oggetto destinatario proveniente da un'altra foresta. I contatti di posta della foresta vengono generalmente creati dalla sincronizzazione di Identity Integration Server (MIIS) di Microsoft.</p>

> [!IMPORTANT]
> I contatti di posta elettronica della foresta sono oggetti destinatario in sola lettura che è possibile aggiornare solo tramite MIIS o un'analoga sincronizzazione personalizzata. Non è possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per rimuovere o modificare un contatto di posta della foresta.


</td>
</tr>
<tr class="even">
<td><p>Utente di posta</p></td>
<td><p>Utente di Active Directory abilitato alla posta che rappresenta un utente all'esterno dell'organizzazione Exchange. Ciascun utente di posta dispone di un indirizzo di posta elettronica esterno. Tutti i messaggi inviati all'utente di posta vengono instradati a questo indirizzo di posta elettronica esterno.</p>
<p>L'utente di posta elettronica è simile al contatto di posta, tranne per il fatto che dispone di credenziali di accesso a Active Directory e che può accedere alle risorse.</p></td>
</tr>
<tr class="odd">
<td><p>Gruppo non universale abilitato alla posta</p></td>
<td><p>Oggetto del gruppo locale o globale di Active Directory abilitato alla posta elettronica. I gruppi non universali abilitati alla posta elettronica erano sospesi in Exchange Server 2007 e possono esistere solo se è stata eseguita la migrazione da Exchange 2003 o da versioni precedenti di Exchange. Non è possibile utilizzare Exchange Server 2013 per creare gruppi di distribuzione non universali.</p></td>
</tr>
<tr class="even">
<td><p>Cartella pubblica abilitata all'utilizzo della posta</p></td>
<td><p>Cartella pubblica di Exchange configurata per la ricezione di messaggi.</p></td>
</tr>
<tr class="odd">
<td><p>Gruppi di distribuzione</p></td>
<td><p>Un gruppo di distribuzione è un oggetto di distribuzione Active Directory abilitato alla posta che può essere utilizzato solo per distribuire i messaggi a un gruppo di destinatari.</p></td>
</tr>
<tr class="even">
<td><p>Gruppo di sicurezza abilitato all'utilizzo della posta</p></td>
<td><p>Un gruppo di sicurezza abilitato all'utilizzo della posta è un gruppo di sicurezza universale di Active Directory che può essere utilizzato per concedere le autorizzazioni di accesso alle risorse di Active Directory e per distribuire messaggi.</p></td>
</tr>
<tr class="odd">
<td><p>Destinatario di Microsoft Exchange</p></td>
<td><p>Oggetto destinatario speciale che fornisce un mittente conosciuto e unificato in grado di differenziare i messaggi generati dal sistema dagli altri messaggi. Sostituisce il mittente Amministratore di sistema che veniva utilizzato per i messaggi generati dal sistema nelle versioni precedenti di Exchange.</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale sala</p></td>
<td><p>Cassetta postale per la risorsa che viene assegnata a un luogo di riunione come una sala conferenze, un auditorium o un'aula per corsi di formazione. Le cassette postali sala possono essere incluse come risorse in convocazioni di riunione, offrendo un modo semplice ed efficiente per organizzare riunioni per gli utenti.</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale condivisa</p></td>
<td><p>Una cassetta postale non associata principalmente a un singolo utente e che viene generalmente configurata per consentire l'accesso a più utenti.</p></td>
</tr>
<tr class="even">
<td><p>Cassette postali del sito</p></td>
<td><p>Una cassetta postale costituita da una cassetta postale di Exchange per l'archiviazione di messaggi di posta elettronica e un sito SharePoint per l'archiviazione di documenti. Gli utenti possono accedere sia ai messaggi di posta elettronica sia ai documenti utilizzando la stessa interfaccia client. Per ulteriori informazioni, vedere <a href="site-mailboxes-exchange-2013-help.md">Cassette postali del sito</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale utente</p></td>
<td><p>Cassetta postale assegnata a un singolo utente nell'organizzazione Exchange. In genere contiene messaggi, elementi di calendario, contatti, attività, documenti e altri importanti dati aziendali.</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale Office 365</p></td>
<td><p>Nelle distribuzioni ibride, una cassetta postale Office 365 consiste in un utente di posta in Active Directory locale e una cassetta postale del cloud presente in Exchange Online.</p></td>
</tr>
<tr class="odd">
<td><p>Utente collegato</p></td>
<td><p>Un utente collegato è un utente la cui cassetta postale si trova in una foresta differente rispetto a quelle in sui si trova l'utente.</p></td>
</tr>
</tbody>
</table>


## Cassette postali

Le cassette postali costituiscono il tipo di destinatario più comune utilizzato dagli Information Worker in un'organizzazione Exchange. Ciascuna cassetta postale è associata a un account utente di Active Directory. L'utente può utilizzare la cassetta postale per inviare e ricevere messaggi, nonché per archiviare messaggi, appuntamenti, attività, note e documenti. Le cassette postali rappresentano il principale strumento di messaggistica e collaborazione per gli utenti nell'organizzazione Exchange.

## Componenti della cassetta postale

Ciascuna cassetta postale comprende un utente di Active Directory e i dati della cassetta postale archiviati nel database delle cassette postali di Exchange (come mostrato nella figura seguente). Tutti i dati di configurazione della cassetta postale sono archiviati negli attributi di Exchange dell'oggetto utente di Active Directory. Nel database delle cassette postali sono contenuti i dati presenti nella cassetta postale associata all'account utente.


> [!IMPORTANT]
> Quando si crea una cassetta postale per un nuovo utente o per uno esistente, gli attributi di Exchange&nbsp;richiesti per una cassetta postale vengono aggiunti all'oggetto utente di Active Directory. I dati della cassetta postale associata non vengono creati fino a quando la cassetta postale non riceve un messaggio o finché l'utente non vi accede.



**Componenti della cassetta postale**

![Parti che costituiscono una cassetta postale](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "Parti che costituiscono una cassetta postale")


> [!WARNING]
> Se si rimuove una cassetta postale, vengono eliminati non solo i relativi dati archiviati nel database delle cassette postali di Exchange contrassegnati per l'eliminazione, ma viene eliminato da Active Directory anche l'account utente. Per mantenere l'account utente ed eliminare solo i dati della cassetta postale, è necessario disabilitare la cassetta postale.



## Tipi di cassetta postale

Exchange supporta i seguenti tipi di cassetta postale:

  - **Cassette postali utente   **Le cassette postali utente sono assegnate a singoli utenti nell'organizzazione Exchange. Le cassette postali utente offrono agli utenti una ricca piattaforma di collaborazione. Gli utenti possono inviare e ricevere messaggi, gestire i propri contatti, pianificare riunioni e gestire un elenco di attività. Gli utenti possono anche disporre di messaggi vocali recapitati alle proprie cassette postali. Le cassette postali utente costituiscono il tipo di cassetta postale più comunemente utilizzato e vengono generalmente assegnate agli utenti dell'organizzazione.

  - **Cassette postali collegate**   Le cassette postali collegate sono cassette postali cui gli utenti hanno accesso in una foresta trusted e separata. Le cassette postali collegate possono essere necessarie per organizzazioni che distribuiscono Exchange in un foresta di risorse. Lo scenario della foresta delle risorse consente a un'organizzazione di centralizzare Exchange in una singola foresta, consentendo al contempo l'accesso all'organizzazione Exchange con account utente in una o più foreste trusted.
    
    Come illustrato in precedenza, a ogni cassetta postale deve essere associato un account utente. Tuttavia, l'account utente che accede alla cassetta postale collegata non esiste nella foresta in cui Exchange è distribuito. Pertanto, un account utente disabilitato presente nella stessa foresta di Exchange è associato a ciascuna cassetta postale collegata. Nella figura seguente è illustrata la relazione tra l'account utente collegato utilizzato per accedere alla cassetta postale collegata e l'account utente disabilitato nella foresta di risorse di Exchange associato alla cassetta postale collegata.
    
    **Cassetta postale collegata**
    
    ![Organizzazione di Exchange complessa con foresta di risorse](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organizzazione di Exchange complessa con foresta di risorse")  

  - **Cassette postali Office 365   **Quando si crea una cassetta postale Office 365 in Exchange Online in una distribuzione ibrida, l'utente di posta viene creato in Active Directory locale. La sincronizzazione delle directory, se configurata, sincronizza automaticamente il nuovo oggetto utente in Office 365, dove viene convertito in una cassetta postale del cloud in Exchange Online. È possibile creare cassette postali Office 365 come cassette postali utente normali, cassette postali per le risorse per sale riunione e attrezzature e cassette postali condivise.

  - **Cassette postali condivise**   Le cassette postali condivise sono cassette postali non associate principalmente a singoli utenti e vengono generalmente configurate per consentire l'accesso a più utenti.
    
    Sebbene sia possibile concedere a utenti aggiuntivi le autorizzazioni di accesso a qualsiasi tipo di cassetta postale, le cassette postali condivise sono dedicate a questa funzionalità. L'utente di Active Directory associato a una cassetta postale condivisa deve essere un account disabilitato. Dopo aver creato una cassetta postale condivisa, è necessario concedere le autorizzazioni a tutti gli utenti che richiedono di accedervi.

  - **Cassette postali per le risorse**   Le cassette postali per le risorse sono cassette postali speciali progettate per essere utilizzate per la pianificazione delle risorse. Come tutti gli altri tipi di cassette postali, la cassetta postale per le risorse dispone di un account utente di Active Directory, che deve però essere un account disabilitato. Sono disponibili i seguenti tipi di cassette postali per le risorse:
    
      - **Cassette postali sala**   Queste cassette postali sono assegnate a luoghi di incontro, quali sale riunioni, auditorium e laboratori per esercitazioni.
    
      - **Cassette postali attrezzatura**   Queste cassette postali vengono assegnate alle risorse che non sono specifiche di una posizione, quali computer portatili, proiettori, microfoni o auto aziendali.
    
    Entrambi i tipi di cassette postali per le risorse possono essere inclusi in convocazioni di riunione, offrendo un modo semplice ed efficace di utilizzare le risorse da parte degli utenti. È possibile configurare le cassette postali per le risorse per elaborare automaticamente le convocazioni di riunione in arrivo basate sui criteri di prenotazione risorse definiti dai proprietari delle risorse stesse. Ad esempio, una sala riunione può essere configurata per accettare automaticamente le convocazioni di riunione, fatta eccezione per le riunioni ricorrenti, in quanto queste possono essere soggette all'approvazione del proprietario delle risorse.

## Cassette postali di sistema

Le cassette postali di sistema vengono create da Exchange nel dominio radice della foresta di Active Directory durante l'installazione. Gli utenti o gli amministratori non possono accedere a queste cassette postali. Le cassette postali di sistema vengono create per funzionalità di Exchange quali Messaggistica unificata, migrazione, approvazione di messaggi ed eDiscovery in locale. Nella tabella seguente sono riportate le informazioni sulle cassette postali di sistema, così come vengono visualizzate in Active Directory.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cassetta postale</th>
<th>Nome</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Organizzazione</p></td>
<td><p>SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
</tr>
<tr class="even">
<td><p>Approvazione del messaggio</p></td>
<td><p>SystemMailbox {1f05a927-<em>xxxx</em>- <em>xxxx</em> - <em>xxxx</em> -<em>xxxxxxxxxxxx</em>}</p>
<p>dove <em>x</em> è un numero univoco casualmente assegnato per ciascuna foresta di Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Archiviazione dei dati di messaggistica unificata</p></td>
<td><p>SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
</tr>
<tr class="even">
<td><p>Individuazione</p></td>
<td><p>DiscoverySearchMailbox {D919BA05-46A6-415f-80AD-7E09334BB852}</p></td>
</tr>
<tr class="odd">
<td><p>Posta elettronica federata</p></td>
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
</tr>
<tr class="even">
<td><p>Migrazione</p></td>
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
</tr>
</tbody>
</table>


Per mettere fuori uso l'ultimo server Cassette postali nella propria organizzazione Exchange, è necessario disabilitare prima queste cassette postali di sistema utilizzando il cmdlet [Disable-Mailbox](https://technet.microsoft.com/it-it/library/aa997210\(v=exchg.150\)). Quando vengono rimosse le autorizzazioni da un server Cassette postali che contiene queste cassette postali di sistema, è necessario spostarle su un altro server Cassette postali per non perdere la funzionalità.

## Pianificazione delle cassette postali

Le cassette postali vengono create nei database delle cassette postali sui server Exchange in cui è installato il ruolo del server Cassette postali. Per offrire agli utenti delle cassette postali una piattaforma efficiente e affidabile, è essenziale pianificare in modo dettagliato la distribuzione dei server Cassette postali e dei database. Per ulteriori informazioni sulla pianificazione dei database e dei server Cassette postali, vedere [Pianificazione e distribuzione](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Gruppi di distribuzione

I gruppi di distribuzione sono oggetti gruppo di Active Directory abilitati alla posta utilizzati principalmente per la distribuzione di messaggi a più destinatari. Qualsiasi tipo di destinatario può essere membro di un gruppo di distribuzione.


> [!IMPORTANT]
> Notare le differenze di terminologia tra Active Directory ed Exchange. In Active Directory, con gruppo di distribuzione si intende qualsiasi gruppo che non dispone di un contesto di protezione, indipendentemente dal fatto che sia abilitato alla posta o meno. In Exchange, con gruppi di distribuzione si fa riferimento a tutti i gruppi abilitati alla posta elettronica, indipendentemente dal fatto che abbiano o meno un contesto di protezione.



Exchange supporta i seguenti tipi di gruppi di distribuzione:

  - **Gruppi di distribuzione**   Sono oggetti gruppo di distribuzione universale di Active Directory abilitati alla posta elettronica. Possono essere utilizzati solo per distribuire i messaggi a un gruppo di destinatari.

  - **Gruppi di protezione abilitati alla posta elettronica**   Sono oggetti gruppo di protezione universali di Active Directory abilitati alla posta elettronica. Possono essere utilizzati per assegnare le autorizzazioni di accesso alle risorse in Active Directory e anche per distribuire messaggi.

  - **Gruppi non universali abilitati alla posta**   Sono oggetti gruppi locali o globali di Active Directory abilitati alla posta. È possibile creare o abilitare alla posta elettronica solo i gruppi di distribuzione universali. Possono essere disponibili gruppi abilitati alla posta migrati da versioni precedenti di Exchange che non sono gruppi universali. È ancora possibile gestire questi gruppi utilizzando Interfaccia di amministrazione di Exchange o Shell.
    

    > [!NOTE]
    > Per convertire un gruppo globale o locale al dominio in un gruppo universale, è possibile utilizzare il cmdlet <A href="https://technet.microsoft.com/it-it/library/bb123770(v=exchg.150)">Set-Group</A> in Shell.



## Gruppi di distribuzione dinamici

I gruppi di distribuzione dinamici sono gruppi di distribuzione in cui l'appartenenza è basata su filtri destinatario specifici anziché su un insieme specifico di destinatari.

Diversamente dai gruppi di distribuzione normali, l'elenco di appartenenza a un gruppo di distribuzione dinamico viene calcolato in base ai filtri e alle condizioni specificate dall'utente ogni volta che un messaggio viene inviato al gruppo. Quando viene inviato un messaggio di posta elettronica a un gruppo di distribuzione dinamico, il messaggio viene recapitato anche a tutti i destinatari presenti nell'organizzazione che soddisfano i criteri definiti per quel gruppo di distribuzione dinamico.


> [!IMPORTANT]
> Un gruppo di distribuzione dinamico include tutti i destinatari in Active Directory con gli attributi che corrispondono al filtro del gruppo al momento dell'invio di un messaggio. Qualora le proprietà di un destinatario vengano modificate per soddisfare i criteri del filtro del gruppo, il destinatario potrebbe involontariamente diventare un membro del gruppo e ricevere messaggi inviati al gruppo di distribuzione dinamico. Per ridurre le probabilità che si verifichi tale problema, è necessario adottare processi di provisioning degli account ben definiti e coerenti.



Per facilitare la creazione dei filtri destinatario per i gruppi di distribuzione dinamici, è possibile utilizzare appositi filtri predefiniti. Un *filtro predefinito* è un filtro di uso comune che può essere utilizzato per soddisfare un'ampia gamma di criteri di filtro destinatario. È possibile utilizzare questi filtri per specificare i tipi di destinatario che si desidera includere nel gruppo di distribuzione dinamico. È inoltre possibile specificare un elenco di condizioni che i destinatari devono soddisfare. È possibile creare condizioni predefinite basate sulle seguenti proprietà:

  - Attributi personalizzati 1-15

  - Stato o provincia

  - Società

  - Reparto

  - Contenitore dei destinatari

È inoltre possibile specificare condizioni diverse rispetto a quelle precedentemente elencate basate sulle proprietà dei destinatari. A questo scopo, è necessario utilizzare Shell per creare una query personalizzata per il gruppo di distribuzione dinamico. Si ricordi che le impostazioni del filtro e delle condizioni per i gruppi di distribuzione dinamici che dispongono di filtri destinatari personalizzati possono essere gestite solo da Shell. Per un esempio di come creare un gruppo di distribuzione dinamico utilizzando una query personalizzata, vedere [Gestione dei gruppi di distribuzione dinamici](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/manage-dynamic-distribution-groups).

## Contatti di posta

I contatti di posta contengono generalmente informazioni su persone o organizzazioni esistenti all'esterno dell'organizzazione Exchange. I contatti di posta possono essere visualizzati nella rubrica condivisa dell'organizzazione (denominata anche Elenco indirizzi globale) e in altri elenchi di indirizzi e possono essere aggiunti come membri ai gruppi di distribuzione. Ciascun contatto dispone di un indirizzo di posta elettronica esterno e tutti i messaggi di posta elettronica inviati a un contatto vengono automaticamente inoltrati a quell'indirizzo. I contatti sono lo strumento ideale per rappresentare le persone esterne all'organizzazione di Exchange (nella rubrica condivisa) che non hanno bisogno di accedere alle risorse interne. Di seguito sono riportati i tipi di contatto di posta elettronica:

  - **Contatti di posta**   Sono contatti di Active Directory abilitati alla posta elettronica che contengono informazioni su persone e organizzazioni esistenti all'esterno dell'organizzazione Exchange.

  - **Contatti di posta della foresta**   Rappresentano oggetti destinatari provenienti da un'altra foresta e vengono generalmente creati dalla sincronizzazione delle directory. I contatti di posta elettronica della foresta sono oggetti destinatario in sola lettura che è possibile aggiornare o rimuovere esclusivamente tramite la sincronizzazione. Non è possibile utilizzare le interfacce di gestione di Exchange per modificare o rimuovere un contatto della foresta di posta elettronica.

## Utenti di posta elettronica

Gli utenti di posta sono simili ai contatti di posta. Entrambi possiedono indirizzi di posta elettronica esterni, contengono informazioni su persone esterne all'organizzazione Exchange e possono essere visualizzati nella rubrica condivisa e in altri elenchi di indirizzi. Tuttavia, a differenza di un contatto di posta elettronica, gli utenti di posta dispongono delle credenziali di accesso di Active Directory e possono accedere alle risorse per le quali dispongono dell'autorizzazione.

Se una persona esterna all'organizzazione richiede l'accesso alle risorse nella rete, è necessario creare un utente di posta anziché un contatto di posta. Ad esempio, è possibile creare utenti di posta per consulenti a breve termine che necessitano di accedere all'infrastruttura del server, ma che utilizzano i propri indirizzi esterni.

Un altro scenario possibile è costituito dalla creazione nell'organizzazione di utenti di posta per i quali non si desidera mantenere una cassetta postale di Exchange. Ad esempio, in seguito a un'acquisizione, la società acquisita può mantenere la propria infrastruttura di messaggistica separata ma può anche necessitare dell'accesso alle risorse nella rete. Per tali utenti è possibile creare utenti di posta anziché utenti di cassette postali.


> [!NOTE]
> In Interfaccia di amministrazione di Exchange, utilizzare la pagina <STRONG>Destinatari</STRONG> &gt; <STRONG>Contatti</STRONG> per creare e gestire gli utenti di posta. Non è disponibile una pagina distinta per gli utenti di posta.



## Cartelle pubbliche abilitate alla posta

Le cartelle pubbliche sono state progettate per fungere da archivio delle informazioni condivise tra molti utenti. L'abilitazione di una cartella pubblica all'utilizzo della posta offre agli utenti un livello aggiuntivo di funzionalità. Oltre che per l'invio di normali messaggi, gli utenti possono utilizzare la cartella anche per l'invio e, talvolta, la ricezione di messaggi di posta elettronica. Per ciascuna cartella abilitata alla posta è disponibile in Active Directory un oggetto in cui sono archiviati l'indirizzo di posta elettronica, il nome della rubrica e altri attributi relativi alla posta.

È possibile gestire le cartelle pubbliche utilizzando Interfaccia di amministrazione di Exchange o Shell. Per ulteriori informazioni sulla gestione delle cartelle pubbliche, vedere [Cartelle pubbliche](public-folders-exchange-2013-help.md).

## Destinatario di Microsoft Exchange

Il destinatario di Microsoft Exchange è uno speciale oggetto destinatario che fornisce un mittente del messaggio conosciuto e unificato e in grado di distinguere i messaggi generati dal sistema dagli altri messaggi. Sostituisce il mittente Amministratore di sistema che veniva utilizzato per i messaggi generati dal sistema nelle versioni precedenti di Exchange.

Il destinatario di Microsoft Exchange non è un oggetto destinatario tipico, come una cassetta postale, un utente o un contatto di posta, e non viene gestito con gli strumenti tipici del destinatario. Tuttavia, è possibile utilizzare il cmdlet [Set-OrganizationConfig](https://technet.microsoft.com/it-it/library/aa997443\(v=exchg.150\)) in Shell per configurare il destinatario di Microsoft Exchange.


> [!NOTE]
> Quando vengono inviati i messaggi generati dal sistema a un mittente esterno, il destinatario di Microsoft Exchange non viene utilizzato come mittente del messaggio. Invece, viene utilizzato l'indirizzo di posta elettronica specificato dal parametro <EM>ExternalPostmasterAddress</EM> nel cmdlet <A href="https://technet.microsoft.com/it-it/library/bb124151(v=exchg.150)">Set-TransportConfig</A>.



## Documentazione di destinatari

Nella seguente tabella, sono riportati i collegamenti agli argomenti che offrono maggiori informazioni sui destinatari di Exchange e ne facilitano la gestione.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Argomento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Creazione di cassette postali utente</a></p></td>
<td><p>Ulteriori informazioni sulla creazione di utenti di cassette postali utilizzando l'interfaccia di amministrazione di Exchange o Exchange Management Shell.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes">Gestire le cassette postali degli utenti</a></p></td>
<td><p>Maggiori informazioni su come creare cassette postali utente, modificare le proprietà delle cassette postali e modificare in blocco le proprietà selezionate per più cassette postali.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-mailboxes-exchange-2013-help.md">Gestire le cassette postali collegate</a></p></td>
<td><p>Maggiori informazioni sui requisiti delle cassette postali collegate, su come crearle e collegarle a un account master e su come modificare le proprietà delle cassette postali collegate.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-distribution-groups/manage-distribution-groups">Creazione e gestione dei gruppi di distribuzione</a></p></td>
<td><p>Maggiori informazioni su come creare e gestire gruppi di distribuzione e creare un criterio di denominazione dei gruppi per l'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-mail-enabled-security-groups">Gestire gruppi di sicurezza abilitati alla posta elettronica</a></p></td>
<td><p>Maggiori informazioni su come creare e gestire i gruppi di protezione abilitati alla posta elettronica.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/manage-dynamic-distribution-groups">Gestione dei gruppi di distribuzione dinamici</a></p></td>
<td><p>Maggiori informazioni su come creare i gruppi di distribuzione dinamici e gestire le proprietà dei gruppi di distribuzione dinamici, quali l'utilizzo di attributi personalizzati e altre proprietà per determinare l'appartenenza al gruppo.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-mail-contacts">Gestire i contatti di posta</a></p></td>
<td><p>Maggiori informazioni su come creare e gestire i contatti di posta.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-mail-users-exchange-2013-help.md">Gestire gli utenti di posta</a></p></td>
<td><p>Maggiori informazioni su come creare e gestire gli utenti di posta.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-room-mailboxes">Creazione e gestione delle cassette sala</a></p></td>
<td><p>Maggiori informazioni su come creare cassette postali sala e gestirne le proprietà, quali l'abilitazione di riunioni ricorrenti e la configurazione delle opzioni di prenotazione e pianificazione.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-equipment-mailboxes">Gestire le cassette postali attrezzatura</a></p></td>
<td><p>Maggiori informazioni su come creare le cassette postali attrezzatura, configurare le opzioni di prenotazione e pianificazione e gestire altre proprietà delle cassette.</p></td>
</tr>
<tr class="odd">
<td><p><a href="disconnected-mailboxes-exchange-2013-help.md">Cassette postali disconnesse</a></p></td>
<td><p>Informazioni sui due tipi di cassette postali disconnesse e su come gestirle.</p></td>
</tr>
<tr class="even">
<td><p><a href="custom-attributes-exchange-2013-help.md">Attributi personalizzati</a></p></td>
<td><p>Informazioni su come aggiungere informazioni sui destinatari utilizzando attributi personalizzati.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/it-it/library/bb124268(v=exchg.150)">Filtri destinatario comandi Shell</a></p></td>
<td><p>Informazioni sull'utilizzo di filtri predefiniti o personalizzati per filtrare un gruppo di destinatari.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-permissions-for-recipients">Gestione delle autorizzazioni per i destinatari</a></p></td>
<td><p>Informazioni sull'utilizzo dell'interfaccia di amministrazione di Exchange o di Shell per l'assegnazione di autorizzazioni a utenti e gruppi.</p></td>
</tr>
<tr class="odd">
<td><p><a href="automatic-mailbox-distribution-exchange-2013-help.md">Distribuzione automatica delle cassette postali</a></p></td>
<td><p>Informazioni su come funziona la distribuzione automatica delle cassette postali e su come controllare quali database delle cassette postali sono selezionati per le cassette postali nuove e spostate.</p></td>
</tr>
</tbody>
</table>

