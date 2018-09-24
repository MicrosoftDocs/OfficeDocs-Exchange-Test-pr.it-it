---
title: 'Scenario: Distribuzione di criteri della Rubrica: Exchange 2013 Help'
TOCTitle: 'Scenario: Distribuzione di criteri della Rubrica'
ms:assetid: 6ac3c87d-161f-447b-afb2-149ae7e3f1dc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ657455(v=EXCHG.150)
ms:contentKeyID: 50480827
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Scenario: Distribuzione di criteri della Rubrica

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

## Scenari di distribuzione

Nei tre scenari seguenti vengono descritte le soluzioni di distribuzione possibili per tre diversi tipi di organizzazione. Sebbene esistano anche molti altri scenari, quelli illustrati in questo articolo sono i più frequenti. Gli elenchi di indirizzi e gli Elenchi indirizzi globali (GAL) in tali scenari sono stati creati in base a filtri, come Attributi personalizzati, che raggruppano gli oggetti in modo logico.

## Scenario 1: Due società distinte - Una singola organizzazione di Exchange

Questo scenario è applicabile a agenzie governative, divisioni o dipartimenti che condividono le infrastrutture ma non la linea manageriale e non hanno impiegati in comune. Inoltre, tali divisioni non hanno particolari problemi di privacy o sicurezza. In questo scenario, vengono creati due criteri di rubrica (ABP) dove gli impiegati possono vedere solo i membri della stessa organizzazione quando visualizzano l'elenco indirizzi globale o guardano l'appartenenza ad altri gruppi di distribuzione. Inoltre, nessun utente sarà membro di gruppi di distribuzione che coprono l'intera organizzazione.

![Criteri della rubrica con due società distinte](images/JJ657455.b4fc82da-a659-4ade-ba33-d55d90dcf204(EXCHG.150).gif "Criteri della rubrica con due società distinte")

I criteri della rubrica di Contoso e Humungous Insurance sono stati creati utilizzando i seguenti elenchi di indirizzi, elenco indirizzi globale, elenco delle sale, e rubrica fuori rete, che sono state create utilizzando un filtro destinatari che ha raggruppato gli oggetti con un filtro quale attributo personalizzato. Poiché le due società sono separate e non presentano alcuna interazione, non esistono elenchi di indirizzi in comune.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Contoso</p></td>
<td><p>Humongous Insurance</p></td>
</tr>
<tr class="even">
<td><p>Elenchi indirizzi</p></td>
<td><p>AL_CON_Groups</p>
<p>AL_CON_Users</p>
<p>AL_CON_Contacts</p></td>
<td><p>AL_HI_Groups</p>
<p>AL_HI_Users</p>
<p>AL_HI_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>Elenco indirizzi globale</p></td>
<td><p>GAL_CON</p></td>
<td><p>GAL_HI</p></td>
</tr>
<tr class="even">
<td><p>Elenco indirizzi sale</p></td>
<td><p>AL_CON_Rooms</p></td>
<td><p>AL_HI_Rooms</p></td>
</tr>
<tr class="odd">
<td><p>Rubrica fuori rete (OAB, offline address book)</p></td>
<td><p>OAB_CON</p></td>
<td><p>OAB_HI</p></td>
</tr>
</tbody>
</table>


## Scenario 2: Due società con lo stesso CEO

In questo scenario, Fabrikam e Tailspin Toys condividono la stessa organizzazione di Exchange e lo stesso CEO. Il CEO è la sola persona in comune tra le due società. Questo scenario richiede tre criteri della rubrica che hanno le seguenti caratteristiche:

  - Gli utenti in Tailspin Toys possono vedere solo gli utenti di Tailspin Toys quando sfogliano l'elenco indirizzi globale.

  - Gli utenti in Fabrikam possono vedere solo gli utenti di Fabrikam quando sfogliano l'elenco indirizzi globale.

  - In ciascuna società è presente un gruppo di distribuzione denominato SeniorLeaders, che include gli alti dirigenti della società e il CEO in comune.

  - Gli utenti che osservano il gruppo di appartenenza del CEO vedranno solo i gruppi che appartengono alla sua società. Non possono vedere i gruppi che non appartengono alla loro azienda.

  - Vengono creati tre criteri della rubrica: **Fab**, **Tail** e **CEO**.

![Due società, un CEO](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "Due società, un CEO")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Fabrikam</p></td>
<td><p>Tailspin Toys</p></td>
<td><p>CEO</p></td>
</tr>
<tr class="even">
<td><p>Elenchi indirizzi</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p></td>
<td><p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p>
<p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>Elenco indirizzi globale</p></td>
<td><p>GAL_FAB</p></td>
<td><p>GAL_TAIL</p></td>
<td><p>Elenco indirizzi globale predefinito</p></td>
</tr>
<tr class="even">
<td><p>Elenco indirizzi sale</p></td>
<td><p>AL_FAB_Rooms</p></td>
<td><p>AL_TAIL_Rooms</p></td>
<td><p>Tutte le sale predefinite</p></td>
</tr>
<tr class="odd">
<td><p>Rubrica fuori rete (OAB, offline address book)</p></td>
<td><p>OAB_FAB</p></td>
<td><p>OAB_TAIL</p></td>
<td><p>Rubrica offline predefinita</p></td>
</tr>
</tbody>
</table>


Se il CEO viene aggiunto ai gruppi di distribuzione delle singole organizzazioni e rientra nell'ambito del criterio della rubrica di ciascuna società, diventa visibile a ciascuna società. Il CEO può creare gruppi di distribuzione che comprendono entrambe le società e che saranno visibili in ciascun elenco indirizzi globale, ma i membri del gruppo di distribuzione saranno in grado di vedere solo i membri del gruppo che appartengono alla propria organizzazione.

## Scenario 3: Istruzione

Questo scenario è applicabile a scuole o università in cui è necessario mantenere separate le classi per assicurare la privacy degli studenti. Lo scenario della formazione ha le seguenti caratteristiche:

  - Gli studenti di ciascuna classe possono vedere solo altri studenti nella propria classe, i loro insegnanti e il preside.

  - Gli insegnanti possono vedere solo gli studenti nelle loro classi.

  - Gli insegnanti possono vedere tutti gli altri insegnanti e il preside.

  - Vengono creati gruppi di distribuzione per i genitori di ogni classe e per la facoltà.

![Scenario didattico per i criteri della rubrica](images/JJ657455.435f3b1a-9752-4c61-ab8a-80115c643d12(EXCHG.150).gif "Scenario didattico per i criteri della rubrica")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Students_ClassA</p></td>
<td><p>Teachers_ClassA</p></td>
<td><p>Preside</p></td>
</tr>
<tr class="even">
<td><p>Elenchi indirizzi</p></td>
<td><p>AL_ClassAAL_Principal</p></td>
<td><p>AL_ClassAAL_AllTeachersAL_AllGroupsAL_Principal</p></td>
<td><p>AL_ClassA</p>
<p>AL_ClassB</p>
<p>AL_AllTeachers</p>
<p>AL_AllStudents</p>
<p>AL_AllGroups</p></td>
</tr>
<tr class="odd">
<td><p>Elenco indirizzi globale</p></td>
<td><p>GAL_StudentsClassA</p></td>
<td><p>GAL_TeachersClassA</p></td>
<td><p>GAL_Everyone</p></td>
</tr>
<tr class="even">
<td><p>Elenco indirizzi sale</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>Tutte le sale predefinite</p></td>
</tr>
<tr class="odd">
<td><p>Rubrica fuori rete (OAB, offline address book)</p></td>
<td><p>OAB_StudentsClassA</p></td>
<td><p>OAB_TeachersClassA</p></td>
<td><p>Rubrica offline predefinita</p></td>
</tr>
</tbody>
</table>


## Considerazioni e procedure consigliate

Quando si utilizzano i criteri della rubrica nella propria organizzazione, è necessario ricordare quanto segue:

  - I criteri della rubrica funzionano correttamente solo se la cassetta postale a cui vengono applicati risiede in un server Exchange 2010 SP2 o Exchange 2013.

  - Non eseguire il ruolo del server Accesso client di Exchange 2010 sul server di catalogo globale, perché in tal caso come interfaccia NSPI (Name Service Provider Interface) verrebbe utilizzato Active Directory anziché il servizio Rubrica di Microsoft Exchange. È possibile eseguire i ruoli del server di Exchange 2013 su un server di catalogo globale e avere un funzionamento corretto dei criteri della rubrica, tuttavia non è consigliabile installare Exchange in un controller di dominio.

  - Non è possibile utilizzare contemporaneamente rubriche gerarchiche e criteri della rubrica. Per ulteriori informazioni, vedere [Rubriche gerarchiche](https://docs.microsoft.com/it-it/exchange/address-books/hierarchical-address-books/hierarchical-address-books).

  - Ogni singolo utente a cui viene assegnato un criterio della rubrica deve essere incluso in un Elenco indirizzi globale a sé.

  - Se si consente alle applicazioni client di accedere ad Active Directory direttamente tramite LDAP, tali applicazioni eluderanno la logica incorporata nei criteri della rubrica. Poiché Outlook per Mac 2011 ed Entourage 2008 utilizzano query LDAP dirette per accedere ad Active Directory, tali applicazioni client non funzioneranno correttamente con i criteri della rubrica se il servizio di individuazione automatica fornisce o specifica un controller di dominio o un server di catalogo globale. Outlook per Mac 2011 può utilizzare EWS o una Rubrica offline locale per accedere alle informazioni relative alle directory. Se tuttavia Outlook per Mac 2011 è in grado di accedere direttamente a un servizio LDAP, tenterà di farlo.

  - L'Elenco indirizzi globale utilizzato in un criterio della rubrica deve contenere, come minimo, tutti gli elenchi di indirizzi definiti e specificati in un criterio della rubrica, incluso l'elenco di indirizzi delle sale. Non creare un Elenco indirizzi globale contenente un numero di oggetti inferiore a quello incluso negli elenchi di indirizzi di uno stesso criterio della rubrica.

  - È consigliabile creare gruppi di distribuzione che non oltrepassino i limiti dell'organizzazione virtuale. La creazione dei gruppi di distribuzione contenenti membri di più organizzazioni virtuali determina i problemi seguenti:
    
      - Se i membri del gruppo richiedono conferme di recapito o di lettura quando inviano messaggi di posta elettronica al gruppo di distribuzione, saranno in grado di vedere gli indirizzi di posta elettronica dei membri dei gruppi di altre organizzazioni virtuali
    
      - Se al gruppo di distribuzione viene inviato un messaggio crittografato e alcuni membri del gruppo non dispongono di ID digitali validi, il mittente riceverà un messaggio di avviso che include il numero totale dei membri che non dispongono di ID validi e un elenco dei relativi indirizzi di posta elettronica. Se tuttavia alcuni di tali membri privi di ID digitali validi appartengono a un'organizzazione diversa da quella del mittente, il messaggio di avviso includerà il numero corretto ma non gli indirizzi di posta elettronica dei membri dell'altra organizzazione. Il numero totale non corrisponderà pertanto all'elenco degli indirizzi dei membri.
        
        Si consideri ad esempio un gruppo di distribuzione contenente un totale di cinque membri appartenenti a due organizzazioni, Agenzia A e Agenzia B. Tre membri di tale gruppo appartengono all'Agenzia A e uno di essi ha ID digitale non valido. Gli altri due membri appartengono all'Agenzia B e hanno entrambi ID digitali non validi. Se un membro dell'Agenzia A invia un messaggio crittografato al gruppo di distribuzione, tale utente riceverà un messaggio di avviso in cui viene segnalato che sono presenti tre destinatari con ID digitale non valido in tutto. Tuttavia, nel messaggio di avviso verrà incluso solo l'indirizzo di posta elettronica del destinatario dell'Agenzia A.
    
      - I criteri della rubrica non vengono applicati ai cmdlet **Get-Group**. Pertanto, qualsiasi utente o processo in grado di eseguire **Get-Group** potrà visualizzare tutti i membri di tutti i gruppi a cui ha accesso.
        
        È consigliabile modificare le impostazioni di gestione dei gruppi nelle opzioni di OWA in modo che gli utenti non possano utilizzare Outlook Web App per gestire i gruppi. Per impedire agli utenti di utilizzare le opzioni di OWA per gestire i gruppi, è necessario escluderli dal ruolo RBAC MyDistributionGroupMembership. Per dettagli, vedere [Ruolo MyDistributionGroupMembership](mydistributiongroupmembership-role-exchange-2013-help.md).
    
      - Se si consente agli utenti di utilizzare Outlook o Outlook Web App per gestire i gruppi, i proprietari dei gruppi devono avere la possibilità di visualizzare l'elenco completo dei membri dei gruppi.

  - Tutti i criteri della rubrica devono includere un elenco di indirizzi delle sale. Se tuttavia nell'organizzazione non viene utilizzato alcun elenco di indirizzi delle sale, è possibile creare un elenco di indirizzi delle sale predefinito vuoto.

  - La distribuzione dei criteri della rubrica non impedisce agli utenti di un'organizzazione virtuale di inviare messaggi di posta elettronica agli utenti di un'altra organizzazione virtuale. Se si desidera impedire agli utenti di scambiare messaggi di posta elettronica tra organizzazioni diverse, è consigliabile creare una regola di trasporto. Per creare ad esempio una regola di trasporto che impedisce agli utenti di Contoso di ricevere messaggi dagli utenti di Fabrikam, e al tempo stesso consentire al team degli alti dirigenti di Fabrikam di inviare messaggi agli utenti di Contoso, eseguire il seguente comando della Shell:
  ```powershell  
        New-TransportRule -Name "StopFabrikamtoContosoMail" -FromMemberOf "AllFabrikamEmployees" -SentToMemberOf "AllContosoEmployees" -DeleteMessage -ExceptIfFrom seniorleadership@fabrikam.com
  ```

  - Se si desidera applicare una funzionalità simile al criterio della Rubrica nel client Lync, è possibile impostare l'attributo `msRTCSIP-GroupingID` per gli oggetti utente specifico. Per ulteriori informazioni, vedere l'argomento di [Partitionbyou con msRTCSIP-GroupingID](https://go.microsoft.com/fwlink/p/?linkid=232306) .

## Procedura di distribuzione generale

## Migrazione dalla segmentazione degli elenchi indirizzi ai criteri della rubrica

Se l'organizzazione configurato la soluzione di separazione elenco indirizzo Exchange 2007 sul posto, attenersi alle istruzioni in [organizzazioni virtuali configurazione e la separazione degli elenchi di indirizzi in Exchange 2007](https://go.microsoft.com/fwlink/p/?linkid=109601)il white paper, deve innanzitutto la migrazione a Exchange Server 2010 utilizzando la procedura descritta in [Migrate a Exchange Server 2010 criteri della Rubrica di Exchange Server 2007 indirizzo elenco separazione](https://go.microsoft.com/fwlink/p/?linkid=235967). Questa procedura richiederà alcuni tempi di inattività per l'organizzazione e pertanto è necessario pianificare di conseguenza.

## Nuova distribuzione di criteri della rubrica

Se nell'organizzazione si stanno distribuendo criteri della rubrica Exchange 2013 e non è stata utilizzata la separazione degli indirizzi in Exchange 2007, è possibile utilizzare queste istruzioni per distribuire i criteri della rubrica nella propria organizzazione.

La procedura riportata in questa sezione prenderà in esame lo scenario 2: Two companies sharing a CEO. In tale scenario, Fabrikam e Tailspin Toys sono aziende separate con CEO e team di alti dirigenti in comune.

## Passaggio 1: Installare e configurare l'agente dei criteri di routing della rubrica

Se si utilizzano criteri della rubrica, affinché gli utenti di organizzazioni virtuali separate non visualizzino le informazioni potenzialmente private l'una dell'altra, è possibile attivare l'agente dei criteri di routing della rubrica. L'agente dei criteri di routing della rubrica è un agente di trasporto in esecuzione su un server per cassette postali che controlla la soluzione per i destinatari nell'organizzazione. Quando l'agente dei criteri di routing della rubrica è installato e configurato, gli utenti cui sono assegnati diversi GAL vengono visualizzati come destinatari esterni ovvero non possono visualizzare le schede contatto dei destinatari esterni.

Per istruzioni dettagliate, vedere [Installare e configurare l'agente di Address Book Policy Routing](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md).

## Passaggio 2: Dividere le organizzazioni virtuali

È necessario trovare una soluzione per dividere l'organizzazione. Si raccomanda di utilizzare la proprietà CustomAttribute1-15 nelle cassette postali, contatti e gruppi invece degli attributi condizionali predefiniti quali Società, Dipartimento o Stato/Provincia per dividere le organizzazioni virtuali per i seguenti motivi:

  - Non tutti i tipi di destinatari dispongono di attributi condizionali predefiniti in Active Directory. Ad esempio, Gruppo di distribuzione e Gruppo di distribuzione dinamico non supportano gli attributi società, dipartimento e stato.

  - Per alcuni destinatari non tutti gli attributi condizionali predefiniti sono esposti nei cmdlet. Ad esempio, i parametri *Company*, *department* e *StateOrProvince* non sono disponibili nei cmdlet per utenti di posta elettronica, contatti, gruppi di distribuzione e cartelle pubbliche abilitate alla posta elettronica.

  - Sono necessari più cmdlet per separare destinatari quando si utilizzano attributi predefiniti. Ad esempio, è necessario eseguire Set-User per applicare un tag a *Company*, *Department*, *StateOrProvince* per una UserMailbox dopo aver eseguito i cmdlet **New-Mailbox** o **Set-Mailbox**.

  - I parametri *CustomAttributeX* sono tutti esposti nei cmdlet Set-\* per ciascun tipo di destinatario, possiamo completare la separazione per quel tipo usando un solo cmdlet

  - Gli attributi CustomAttributeX sono esplicitamente riservati alla personalizzazione di una organizzazione e sono completamente sotto il controllo degli amministratori delle organizzazioni.

Durante la suddivisione dell'organizzazione è inoltre consigliabile utilizzare gli identificatori delle società nei nomi dei gruppi di distribuzione e dei gruppi di distribuzione dinamici. In Exchange è presente una funzionalità criterio di denominazione del gruppo che aggiunge automaticamente al nome del gruppo di distribuzione un prefisso o un suffisso basato su vari attributi che l'utente ha utilizzati nella creazione del gruppo di distribuzione incluso la Società, Stato o provincia, Titolo e da CustomAttribute1 a CustomAttribute15. Il criterio di denominazione del gruppo è particolarmente importante se si consente agli utenti di creare i propri gruppi di distribuzione. Per ulteriori informazioni, vedere [Creare un gruppo di distribuzione dei criteri di denominazione](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-distribution-groups/create-group-naming-policy).

I criteri di denominazione del gruppo non si applicano ai gruppi di distribuzione dinamici, sarà quindi necessario separarli manualmente e applicare manualmente un criterio di denominazione.

## Passaggio 3: Creare gli elenchi di indirizzi, Elenchi indirizzi globali e Rubriche offline

Quando si creano elenchi di indirizzi e elenchi di indirizzi globali non utilizzare i parametri "IncludedRecipient" e "ConditionalX", così come ConditionalCompany e ConditionalCustomAttribute5. Si dovrebbe utilizzare invece un filtro destinatario. È necessario utilizzare Shell per creare i filtri destinatario. Per ulteriori informazioni sui filtri destinatari, vedere [Filtro destinatari nei server Trasporto Edge](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md)

Durante la creazione del criterio della rubrica verranno inclusi più elenchi di indirizzi in base alla modalità di visualizzazione degli elenchi in Outlook o Outlook Web App che si desidera applicare agli utenti. In questa organizzazione sono presenti quattro elenchi di indirizzi:

  - AL\_FAB\_Users\_DGs

  - AL\_FAB\_Contacts

  - AL\_TAIL\_Users\_DGs

  - AL\_TAIL\_Contacts

In questo esempio viene creato l'elenco di indirizzi AL\_TAIL\_Users\_DGs, L'elenco indirizzi contiene tutti gli utenti e gruppi di distribuzione in cui CustomAttribute15 è uguale a TAIL.
```powershell 
    New-AddressList -Name "AL_TAIL_Users_DGs" -RecipientFilter {((RecipientType -eq 'UserMailbox') -or (RecipientType -eq "MailUniversalDistributionGroup") -or (RecipientType -eq "DynamicDistributionGroup")) -and (CustomAttribute15 -eq "TAIL")}
```

Per ulteriori informazioni sulla creazione di elenchi di indirizzi tramite i filtri destinatari, vedere [Creare un elenco di indirizzi utilizzando filtri destinatario](https://docs.microsoft.com/it-it/exchange/address-books/address-lists/use-recipient-filters-to-create-an-address-list).

Per poter creare un criterio della rubrica è necessario fornire un elenco delle sale. Se nell'organizzazione non sono disponibili cassette postali per le risorse (ad esempio per le sale o le apparecchiature), è consigliabile creare un elenco delle sale vuoto. Nell'esempio seguente viene creato un elenco delle sale vuoto poiché nell'organizzazione non sono presenti cassette postali per le sale.
```powershell 
    New-AddressList -Name AL_BlankRoom -RecipientFilter {(Alias -ne $null) -and ((RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox'))}
```

Tuttavia, in questo scenario Fabrikam e Contoso dispongono entrambe di cassette postali per le sale. In questo esempio viene creato un elenco delle sale per Fabrikam utilizzando un filtro destinatario dove CustomAttribute15 è uguale a FAB.
```powershell
    New-AddressList -Name AL_FAB_Room -RecipientFilter {(Alias -ne $null) -and (CustomAttribute15 -eq "FAB")-and (RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox')}
```

L'elenco indirizzi globale utilizzato in un criterio della rubrica deve essere un soprainsieme dell'elenco indirizzi. Non creare un elenco indirizzi globale con un numero di oggetti inferiore a quello di alcuni o tutti gli elenchi di indirizzi nel criterio della rubrica. In questo esempio viene creato un elenco indirizzi globale per Tailspin Toys che comprende tutti i destinatari esistenti nell'elenco indirizzi e nell'elenco delle sale.
```powershell
    New-GlobalAddressList -Name "GAL_TAIL" -RecipientFilter {(CustomAttribute15 -eq "TAIL")}
```

Per ulteriori informazioni, vedere [Creare un elenco indirizzi globale](https://docs.microsoft.com/it-it/exchange/address-books/address-lists/create-global-address-list).

Quando si crea una rubrica offline è necessario includere l'appropriato elenco indirizzi globale nel parametro *AddressLists* di New- o Set-OfflineAddressBook per assicurarsi che non siano inaspettatamente mancanti alcune voci. Praticamente, è possibile personalizzare un gruppo di voci che saranno visibili dall'utente o ridurre la dimensione della rubrica offline da scaricare specificando un elenco di AddressLists in AddressLists di New/Set-OfflineAddressBook. Se tuttavia si desidera che gli utenti vedano tutte le voci dell'elenco indirizzi globale nella rubrica offline, è necessario includere l'elenco indirizzi globale in AddressLists.

In questo esempio viene creata una rubrica offline per Fabrikam denominata OAB\_FAB.

```powershell
New-OfflineAddressBook -Name "OAB_FAB" -AddressLists "GAL_FAB"
```

Per ulteriori informazioni, vedere [Creazione di una Rubrica fuori rete](https://docs.microsoft.com/it-it/exchange/address-books/offline-address-books/create-offline-address-book).

## Passaggio 4: Creare i criteri della rubrica

Dopo aver creato tutti gli oggetti necessari è quindi possibile create il criterio della rubrica. In questo esempio viene rimosso il criterio della rubrica denominato ABP\_TAIL.
```powershell
    New-AddressBookPolicy -Name "ABP_TAIL" -AddressLists "AL_TAIL_Users_DGs"," AL_TAIL_Contacts" -OfflineAddressBook "\OAB_TAIL" -GlobalAddressList "\GAL_TAIL" -RoomList "\AL_TAIL_Rooms"
```
Per ulteriori informazioni, vedere [Creare un criterio della Rubrica](https://docs.microsoft.com/it-it/exchange/address-books/address-book-policies/create-an-address-book-policy).

## Passaggio 5: Assegnare i criteri della rubrica alle cassette postali

L'assegnazione dei criteri della rubrica agli utenti è l'ultimo passaggio della procedura. I criteri della rubrica hanno effetto quando l'applicazione dell'utente si connette al servizio Rubrica di Microsoft Exchange nel server di accesso client. Se l'utente è già connesso a Outlook o Outlook Web App quando il criterio della rubrica viene applicato al proprio account, dovrà chiudere e riavviare l'applicazione client per poter visualizzare i nuovi elenchi di indirizzi e l'Elenco indirizzi globale.

In questo esempio viene assegnato ABP\_FAB a tutte le cassette postali dove CustomAttribute15 è uguale a "FAB".
```powershell
    Get-Mailbox -resultsize unlimited | where {$_.CustomAttribute15 -eq "TAIL"} | Set-Mailbox -AddressBookPolicy "ABP_TAIL"
```
Per ulteriori informazioni, vedere [Assegnare un criterio della Rubrica per gli utenti di posta](https://docs.microsoft.com/it-it/exchange/address-books/address-book-policies/assign-an-address-book-policy-to-mail-users).

