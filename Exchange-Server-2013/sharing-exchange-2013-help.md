---
title: 'Condivisione: Exchange 2013 Help'
TOCTitle: Condivisione
ms:assetid: 09e6732a-4e99-44d0-801d-9463fdc57a9b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638083(v=EXCHG.150)
ms:contentKeyID: 50479967
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Condivisione

 

_**Si applica a:** Exchange Server 2013, Outlook 2013_

_**Ultima modifica dell'argomento:** 2015-02-27_

Potrebbe essere necessario coordinare pianificazioni con persone in diverse organizzazioni o con amici e parenti per poter lavorare insieme a progetti o pianificare eventi sociali. Con Exchange 2013, gli amministratori possono configurare diversi livelli di accesso al calendario per consentire alle aziende di collaborare con altre aziende e agli utenti di condividere con altri le proprie pianificazioni. La condivisione dei calendari tra aziende è configurata mediante la creazione di *relazioni organizzative*. La condivisione del calendario tra utenti è configurata mediante l'applicazione di *criteri di condivisione*.


> [!IMPORTANT]
> Questa funzionalità di Exchange Server 2013 non è completamente compatibile con Office 365 utilizzato da 21Vianet in Cina e potrebbe essere soggetta a limitazioni. Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/?linkid=313640">Informazioni su Office 365 utilizzato da 21Vianet</A>.



**Sommario**

Sharing Scenarios in Exchange 2013

Limitations of free/busy sharing

Firewall considerations for federated sharing

Coexistence with Exchange 2010

Coexistence with Exchange 2007

Sharing Documentation

## Condivisione di scenari in Exchange 2013

I seguenti scenari di condivisione sono supportati in Exchange 2013:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Obiettivo di condivisione</th>
<th>Impostazione da utilizzare</th>
<th>Requisiti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Condividere i calendari con un'organizzazione di Office 365</p></td>
<td><p>Relazioni dell'organizzazione</p></td>
<td><p>L'organizzazione di Office 365 è pronta per la configurazione. L'amministratore di Exchange locale deve configurare una relazione di autenticazione con il cloud (nota anche come &quot;federazione&quot;) e deve soddisfare i requisiti software minimi. Per ulteriori informazioni sulla configurazione della federazione, vedere <a href="federation-exchange-2013-help.md">Federazione</a>.</p></td>
</tr>
<tr class="even">
<td><p>Condividere i calendari con un'altra organizzazione di Exchange locale</p></td>
<td><p>Relazioni dell'organizzazione</p></td>
<td><p>Entrambe le organizzazioni di Exchange locali devono configurare la federazione e soddisfare i requisiti software minimi</p></td>
</tr>
<tr class="odd">
<td><p>Condividere il calendario di un utente di Exchange con un utente di Internet</p></td>
<td><p>Criteri di condivisione</p></td>
<td><p>Nessuno, pronto per la configurazione</p></td>
</tr>
<tr class="even">
<td><p>Condividere il calendario di un utente di Exchange con un altro utente di Exchange locale</p></td>
<td><p>Criteri di condivisione</p></td>
<td><p>Entrambe le organizzazioni di Exchange locali devono configurare la federazione e soddisfare i requisiti software minimi.</p></td>
</tr>
</tbody>
</table>


Nella seguente tabella vengono elencate le differenze tra le relazioni di organizzazione e i criteri di condivisione.

### Relazioni di organizzazione e criteri di condivisione

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Relazione organizzativa</th>
<th>Criterio di condivisione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Richiede una relazione di trust federativa per l'organizzazione</p></td>
<td><p>Sì</p></td>
<td><p>Sì se si tratta di condivisione con altre organizzazioni di domini federati. Non necessaria per i criteri di condivisione Internet.</p></td>
</tr>
<tr class="even">
<td><p>Consiglia la federazione del dominio esterno</p></td>
<td><p>Sì</p></td>
<td><p>Sì se si tratta di condivisione con altre organizzazioni di domini federati. Non necessaria per i criteri di condivisione Internet.</p></td>
</tr>
<tr class="odd">
<td><p>Consente la condivisione di informazioni sulla disponibilità (compresi l'oggetto e il percorso) con organizzazioni esterne per una serie di utenti.</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Consente la condivisione delle cartelle Calendario con informazioni sulla disponibilità</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Consente la condivisione delle cartelle Calendario con le informazioni sulla disponibilità, compresi l'oggetto e il corpo</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Richiede agli utenti di inviare un invito di condivisione a destinatari esterni</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Fornisce un metodo di accesso</p></td>
<td><p>Il server Accesso client accede al server Accesso client dell'organizzazione esterna e recupera le informazioni sulla disponibilità per l'utente esterno, quando richiesto.</p></td>
<td><p>Il server Accesso client accede al server Accesso client dell'organizzazione esterna ed esegue la sottoscrizione alla cartella del calendario dell'utente esterno. Per i criteri di condivisione Internet, gli utenti esterni accedono a un URL pubblico o con restrizioni sul server Accesso client.</p></td>
</tr>
<tr class="even">
<td><p>Può essere applicata a tutti i domini esterni</p></td>
<td><p>No (una relazione uno-a-uno tra due organizzazioni di Exchange 2013)</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Fornisce agli utenti diverse esperienze di condivisione con i destinatari esterni</p></td>
<td><p>No</p></td>
<td><p>Sì, in base al criterio di condivisione applicato</p></td>
</tr>
<tr class="even">
<td><p>Disabilita la condivisione per alcuni utenti</p></td>
<td><p>Sì, specificando un gruppo di distribuzione della protezione per la relazione organizzativa</p></td>
<td><p>Sì, disabilitando il criterio di condivisione applicato</p></td>
</tr>
<tr class="odd">
<td><p>Richiede la presenza della cassetta postale su un server Cassette postali di Exchange 2013</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Limitazioni sulla condivisione delle informazioni sulla disponibilità

La condivisione delle informazioni sulla disponibilità tra organizzazioni di Exchange è soggetta alle seguenti limitazioni:

1.  **Outlook Web Access 2003**   Quando un utente di un'organizzazione Exchange 2003 utilizza Outlook Web Access per accedere alle informazioni sulla disponibilità per gli utenti in un'organizzazione Exchange 2013 remota, la richiesta non riesce. Le connessioni di Outlook Web Access da Exchange 2003 non possono instaurare connessioni WebDAV (Web-based Distributed Authoring and Versioning) con una cartella di sistema relativa alla disponibilità per recuperare le informazioni sulla disponibilità per gli utenti remoti. Dal momento che Exchange 2013 non supporta le connessioni WebDAV, il server Exchange 2003 non è in grado di connettersi a External (FYDIBOHF25SPDLT) sul server Accesso client Exchange 2013 per le richieste Outlook Web Access. I client Outlook non sono soggetti a questa limitazione perché utilizzano MAPI invece di WebDAV per la connessione a External (FYDIBOHF25SPDLT).

2.  **Latenza WAN (Wide Area Network)**   Nelle organizzazioni Exchange 2003, le repliche per tutte le cartelle disponibili o occupate devono risiedere su server Cassette postali di Exchange 2010 SP2 o versione successiva. Negli ambienti in cui i database delle cartelle pubbliche di Exchange 2003 si trovano in più siti fisici, potrebbero verificarsi una latenza eccessiva e problemi di prestazioni se le query interne per le informazioni sulla disponibilità devono attraversare collegamenti WAN per accedere ai database delle cartelle pubbliche di Exchange 2010 che non si trovano nello stesso sito fisico.

3.  **Periodo delle informazioni sulla disponibilità**   Le richieste relative alle informazioni sulla disponibilità inviate a un'organizzazione Exchange 2007 da un'organizzazione Exchange 2013 potrebbero non riuscire a causa della mancata corrispondenza del periodo delle informazioni sulla disponibilità richieste. Per impostazione predefinita, Exchange 2007 accetta richieste di informazioni sulla disponibilità per un periodo di 42 giorni e Exchange 2013 può richiedere informazioni sulla disponibilità per un periodo di 62 giorni. Se la richiesta supera il limite predefinito di 42 giorni imposto da Exchange 2007, si verificherà un errore.
    
    Per configurare i server Accesso client Exchange 2007 in modo che accettino richieste di informazioni sulla disponibilità relative a periodi più lunghi, fare quanto segue:
    
    1.  Su tutti i server Accesso client Exchange 2007, aprire il seguente file con un editor di testo (ad esempio, Blocco note): \<Percorso di installazione di Exchange\>\\V14\\ClientAccess\\ExchWeb\\EWS\\web.config
        

        > [!WARNING]
        > Prima di modificare il file web.config, eseguire una copia del file e archiviarla in un percorso sicuro.

    
    2.  Individuare la sezione **appSettings** nel file web.config.
    
    3.  Aggiungere una nuova chiave "\<add key="maximumQueryIntervalDays" value="62" /\>" e salvare il file web.config.
        

        > [!NOTE]
        > Il valore di maximumQueryIntervalDays non è presente per impostazione predefinita. Quando tale valore non è presente, Exchange 2007 utilizza l'intervallo predefinito di 42 giorni.

    
    4.  Arrestare e riavviare Microsoft Internet Information Services (IIS) su tutti i server Accesso client Exchange 2007.

4.  **Organizzazioni Exchange che includono utenti locali e basati su cloud**   Se si configura la condivisione del calendario con un'altra organizzazione Exchange configurata in una distribuzione ibrida con Microsoft Office 365, non sarà possibile eseguire ricerche di informazioni sulla disponibilità di utenti remoti o basati su Office 365 trasferiti sul cloud. Poiché la relazione organizzativa per l'organizzazione Exchange è con l'organizzazione Exchange remota, non con l'organizzazione Exchange Online basata su Office 365, la richiesta di informazioni sulla disponibilità non è in grado di eseguire query sugli utenti basati su Office 365. Exchange 2013 non supporta la funzionalità per l'invio tramite proxy di queste richieste di informazioni sulla disponibilità al servizio Office 365.

Per i dettagli su come configurare la condivisione delle informazioni sulla disponibilità tra distribuzioni Exchange comuni, vedere [Configurazione della condivisione federata tra organizzazioni di Exchange](configuring-federated-sharing-between-exchange-organizations-exchange-2013-help.md).

## Considerazioni sui firewall per la condivisione federata

Caratteristiche di condivisione federate richiedono che il server Accesso Client dell'organizzazione disponibili in uscita a Internet tramite HTTPS. È necessario consentire l'accesso HTTPS (porta 443 per TCP) in uscita per tutti i server cassette postali Exchange 2013 nell'organizzazione.

Affinché un'organizzazione esterna possa avere accesso alle informazioni sulla disponibilità dell'organizzazione, è necessario pubblicare almeno un server Accesso client su Internet. Ciò richiede l'accesso HTTPS in ingresso da Internet al server Accesso client. I server Accesso client dei siti di Active Directory che non dispongono di un server Accesso client pubblicato su Internet possono utilizzare i server Accesso client di altri siti di Active Directory accessibili da Internet. I server Accesso client non pubblicati su Internet devono disporre dell'URL esterno della directory virtuale dei servizi Web impostata con l'URL visibile alle organizzazioni esterne.

Inizio pagina

## Coesistenza con Exchange 2010

Nelle organizzazioni che contengono server Exchange 2010 ed Exchange 2013, gli utenti che dispongono di una cassetta postale su un server Cassette postali Exchange 2010 possono utilizzare le relazioni organizzative per condividere le informazioni sulla disponibilità con i destinatari delle organizzazioni Exchange 2013 esterne di domini federati. Sui server Cassette postali e Accesso client di Exchange 2010 deve essere in esecuzione SP2 o versioni successive ed è necessario che almeno un server Accesso client di Exchange 2013 sia presente nell'organizzazione Exchange 2010.

## Coesistenza con Exchange 2007

Nelle organizzazioni contenenti i server Exchange 2013 ed Exchange 2007, gli utenti, che dispongono di una cassetta postale su un server Cassette postali di Exchange 2007, possono utilizzare le relazioni di organizzazione per condividere le informazioni sulla disponibilità con i destinatari delle organizzazioni esterne di domini federati. Sul server Cassette postali deve essere in esecuzione Exchange 2007 SP2 o versioni successive ed è necessario disporre di almeno un server Accesso client di Exchange 2013 nell'organizzazione Exchange. È possibile utilizzare le relazioni di organizzazione introducendo un unico server Accesso client di Exchange 2013 nell'organizzazione e fornendo una soluzione più efficace rispetto alle soluzioni che sincronizzano le informazioni sulla disponibilità e che richiedono la sincronizzazione GAL.

Durante l'utilizzo di Outlook 2010 o Outlook Web App per pianificare una riunione su un server Exchange 2007, un utente che dispone di una cassetta postale su un server Exchange 2007 può visualizzare le informazioni sulla disponibilità per un utente dell'organizzazione esterna. Le informazioni sulla disponibilità per le cassette postali di Exchange 2007 sono visibili ai destinatari dell'organizzazione esterna.

I criteri di condivisione vengono assegnati agli utenti delle cassette postali di Exchange 2013. Per utilizzare i criteri di condivisione, una cassetta postale deve trovarsi su un server Cassette postali di Exchange 2013. Per generare o rispondere agli inviti di condivisione, si possono utilizzare solo i client Outlook 2010 e Outlook Web App.

Inizio pagina

## Documentazione sulla condivisione

Nella seguente tabella sono riportati i collegamenti ad argomenti che forniscono ulteriori informazioni sulla condivisione e sulla sua gestione in Exchange 2013.


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
<td><p><a href="federation-exchange-2013-help.md">Federazione</a></p></td>
<td><p>Più informazioni sull'infrastruttura di trust sottostante che supporta la condivisione un metodo semplice per gli utenti per condividere le informazioni relative al calendario con destinatari esterni.</p></td>
</tr>
<tr class="even">
<td><p><a href="organization-relationships-exchange-2013-help.md">Relazioni dell'organizzazione</a></p></td>
<td><p>Ulteriori informazioni sulle relazioni dirette tra organizzazioni Exchange che consentono la condivisione delle informazioni sulla disponibilità.</p></td>
</tr>
<tr class="odd">
<td><p><a href="sharing-policies-exchange-2013-help.md">Criteri di condivisione</a></p></td>
<td><p>Ulteriori informazioni sui criteri di relazione diretta che consentono la condivisione.</p>
<p></p></td>
</tr>
</tbody>
</table>

