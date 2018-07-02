---
title: 'Credenziali della sottoscrizione Edge: Exchange 2013 Help'
TOCTitle: Credenziali della sottoscrizione Edge
ms:assetid: 1d291bc1-9c00-4d1b-8da0-cb81f63d8305
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb266959(v=EXCHG.150)
ms:contentKeyID: 61183404
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Credenziali della sottoscrizione Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

L'argomento spiega come la procedura di sottoscrizione Edge fornisce credenziali utilizzate per proteggere il processo di sincronizzazione EdgeSync e il modo in cui tali credenziali vengono utilizzate da EdgeSync per stabilire una connessione LDAP protetta tra un server Cassette postali di Exchange 2013 e un server Trasporto Edge. Per ulteriori informazioni sul processo di sottoscrizione Edge, vedere [Sottoscrizioni Edge](edge-subscriptions-exchange-2013-help.md).

**Sommario**

Edge Subscription process

EdgeSync replication accounts

Authenticate initial replication

Authenticate scheduled synchronization sessions

Renew EdgeSync replication accounts

## Processo di sottoscrizione Edge

Il server Trasporto Edge viene sottoscritto a un sito di Active Directory per stabilire una relazione di sincronizzazione tra i server Cassette postali di un sito di Active Directory e il server Trasporto Edge sottoscritto. Le credenziali di cui viene effettuato il provisioning durante il processo di sottoscrizione Edge vengono utilizzate per fornire protezione alla connessione LDAP tra un server Cassette postali e un server Trasporto Edge nella rete perimetrale.

Quando si esegue il cmdlet **New-EdgeSubscription** su un server Trasporto Edge, le credenziali dell'account di replica bootstrap EdgeSync (ESBRA) vengono create nella directory Lightweight Directory Services (AD LDS) sul server locale e quindi scritte nel file di sottoscrizione Edge. Queste credenziali vengono utilizzate solo per stabilire la sincronizzazione iniziale e scadranno dopo 24 ore dalla creazione del file sottoscrizione Edge. Se il processo di sottoscrizione Edge non viene completato entro 24 ore, sarà necessario eseguire nuovamente il cmdlet **New-EdgeSubscription** per creare un nuovo file di sottoscrizione Edge. Il file XML di sottoscrizione Edge contiene i dati di configurazione della sottoscrizione Edge.

Il file XML di sottoscrizione di Edge contiene i dati riportati nella seguente tabella.

### Contenuto del file sottoscrizione Edge

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Dati di sottoscrizione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EdgeServerName</strong></p></td>
<td><p>Nome NetBIOS del server Trasporto Edge Il nome di Active Directory della sottoscrizione Edge corrisponderà a questo nome.</p></td>
</tr>
<tr class="even">
<td><p><strong>EdgeServerFQDN</strong></p></td>
<td><p>Il nome di dominio completo (FQDN) del server Trasporto Edge. I server Cassette postali nel sito di Active Director sottoscritto devono essere in grado di individuare il server Trasporto Edge utilizzando DNS per la risoluzione del nome di domino completo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeCertificateBlob</strong></p></td>
<td><p>La chiave pubblica del certificato autofirmato del server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p><strong>ESRAUsername</strong></p></td>
<td><p>Il nome assegnato all'account ESBRA. L'account ESBRA presenta il seguente formato: ESRA.<em>Nome server Trasporto Edge</em>. ESRA sta per account di replica di EdgeSync; tenere presente la differenza tra ESBRA (account di replica bootstrap iniziale) ed ESRA.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ESRAPassword</strong></p></td>
<td><p>La password assegnata all'account ESBRA, viene creata da un generatore di numeri casuali e archiviata nel file sottoscrizione Edge in formato testo non crittografato.</p></td>
</tr>
<tr class="even">
<td><p><strong>EffectiveDate</strong></p></td>
<td><p>La data di creazione del file sottoscrizione Edge.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Durata</strong></p></td>
<td><p>Il periodo di validità delle credenziali prima della scadenza. L'account ESBRA è valido solo per 24 ore.</p></td>
</tr>
<tr class="even">
<td><p><strong>AdamSslPort</strong></p></td>
<td><p>La porta LDAP protetta alla quale è associato EdgeSync durante la sincronizzazione dei dati da Active Directory ad AD LDS. Per impostazione predefinita, viene utilizzata la porta TCP 50636.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProductID</strong></p></td>
<td><p>Le informazioni sulla licenza per il server Trasporto Edge. È necessario assegnare una licenza al server Trasporto Edge prima di creare la sottoscrizione Edge.</p></td>
</tr>
<tr class="even">
<td><p><strong>VersionNumber</strong></p></td>
<td><p>Il numero della versione del file di sottoscrizione Edge.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SerialNumber</strong></p></td>
<td><p>La versione di Exchange del server Trasporto Edge.</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> Le credenziali ESBRA vengono scritte nel file sottoscrizione Edge in formato testo non crittografato. Questo file deve essere protetto durante tutto il processo di sottoscrizione. Dopo aver importato il file di sottoscrizione Edge nell'organizzazione Exchange, eliminare immediatamente questo file dal server Trasporto Edge, dalla condivisione di rete utilizzata per importare il file nell'organizzazione Exchange&nbsp;e da qualsiasi supporto rimovibile.



Inizio pagina

## Account di replica EdgeSync

Gli account di replica EdgeSync (ESRA) sono un importante componente di protezione di EdgeSync. L'autenticazione e l'autorizzazione dell'account ESRA è il meccanismo utilizzato per fornire protezione alla connessione tra un server Trasporto Edge e un server Cassette postali.

L'account ESBRA contenuto nel file sottoscrizione Edge viene utilizzato per stabilire una connessione LDAP protetta durante la sincronizzazione iniziale. Dopo aver importato il file sottoscrizione Edge in un server Cassette postali nel sito di Active Directory a cui viene sottoscritto il server Trasporto Edge, in Active Directory vengono creati account ESRA aggiuntivi per ogni coppia di server Trasporto Edge-Cassette postali. Durante la sincronizzazione iniziale, le credenziali degli account ESRA appena creati vengono replicate in AD LDS. Tali credenziali vengono utilizzate per fornire protezione alle sessioni di sincronizzazione successive.

A ogni account di replica EdgeSync vengono assegnate le proprietà descritte nella seguente tabella.

### Proprietà Ms-Exch-EdgeSyncCredential

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome proprietà</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>TargetServerFQDN</strong></p></td>
<td><p>String</p></td>
<td><p>Il server Trasporto Edge che accetta queste credenziali.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceServerFQDN</strong></p></td>
<td><p>Stringa</p></td>
<td><p>Il server Cassette postali che presenta queste credenziali. Se si tratta di credenziali bootstrap, questo valore sarà vuoto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EffectiveTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>Il momento in cui sarà possibile iniziare a utilizzare le credenziali.</p></td>
</tr>
<tr class="even">
<td><p><strong>ExpirationTime</strong></p></td>
<td><p>DateTime (UTC)</p></td>
<td><p>Il momento in cui non sarà più possibile utilizzare le credenziali.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserName</strong></p></td>
<td><p>Stringa</p></td>
<td><p>Il nome utente utilizzato per l'autenticazione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Password</strong></p></td>
<td><p>Byte</p></td>
<td><p>La password utilizzata per l'autenticazione. Questa password viene crittografata utilizzando <strong>ms-Exch-EdgeSync-Certificate</strong>.</p></td>
</tr>
</tbody>
</table>


Nelle seguenti sezioni vengono descritti il provisioning e l'utilizzo delle credenziali dell'account ESRA durante il processo di sincronizzazione EdgeSync.

## Provisioning dell'account di replica bootstrap EdgeSync

Quando si esegue il cmdlet **New-EdgeSubscription** sul server Trasporto Edge, viene effettuato il provisioning dell'account ESBRA nel seguente modo:

  - Viene creato un certificato autofirmato (Edge-Cert) sul server Trasporto Edge. La chiave privata viene memorizzata nell'archivio del computer locale e la chiave pubblica viene scritta nel file sottoscrizione Edge.

  - L'account ESBRA viene creato in AD LDS e le credenziali vengono scritte nel file di sottoscrizione Edge.

  - Il file di sottoscrizione Edge viene esportato copiandolo in un supporto removibile (poiché il server Edge non si trova nel sito di Active Directory, non è possibile utilizzare una cartella condivisa per esportare il file), per essere quindi importato in un server Cassette postali.

## Provisioning degli account di replica EdgeSync in Active Directory

Quando il file sottoscrizione Edge viene importato in un server Cassette postali, si verificano i seguenti passaggi per definire un record della sottoscrizione Edge in Active Directory ed effettuare il provisioning delle credenziali degli account ESRA aggiuntivi.

1.  Viene creato l'oggetto di configurazione server Trasporto Edge in Active Directory. Il certificato Edge-Cert viene scritto in questo oggetto come attributo.

2.  Ogni server Cassette postali nel sito di Active Directory sottoscritto riceve da Active Directory una notifica relativa alla registrazione di una nuova sottoscrizione Edge. Una volta ricevuta la notifica, l'account ESRA.edge viene recuperato da ogni server Cassette postali e crittografato tramite la chiave pubblica Edge-Cert. L'account crittografato ESRA.edge viene quindi scritto nell'oggetto di configurazione server Trasporto Edge.

3.  Viene creato un certificato autofirmato (TransportService-Cert) da ogni server Cassette postali. La chiave privata viene memorizzata nell'archivio del computer locale e la chiave pubblica viene archiviata nell'oggetto di configurazione server Cassette postali in Active Directory.

4.  L'account ESRA.edge viene crittografato in ogni server Cassette postali tramite la chiave pubblica del suo certificato TransportService e quindi viene archiviato nell'oggetto di configurazione corrispondente.

5.  Ogni server Cassette postali genera un account ESRA per ogni oggetto di configurazione del server Trasporto Edge esistente in Active Directory (ESRA.edge. *Mailboxname.\#*).
    
    Esempio: ESRA.edge.Example.0
    
    La password per ESRA.edge viene creata da un generatore di numeri casuali e crittografata tramite la chiave pubblica del certificato TransportService-Cert. La lunghezza massima della password è quella consentita per Windows Server.

6.  Ogni account ESRA.edge. *Mailboxname.\#* viene crittografato tramite la chiave pubblica del certificato Edge-Cert e viene archiviato nell'oggetto di configurazione server Trasporto Edge in Active Directory.

Le sezioni seguenti spiegano come questi conti vengono utilizzati durante la sincronizzazione di EdgeSync.

Inizio pagina

## Autenticare la replica iniziale

L'account ESBRA viene utilizzato solo per stabilire la sincronizzazione iniziale. Durante la prima sincronizzazione di EdgeSync, gli account ESRA aggiuntivi, ESRA.edge.*Mailboxname.\#*, vengono replicati in AD LDS. Tali account vengono utilizzati per autenticare le sessioni di sincronizzazione EdgeSync successive.

Il server Cassette postali che esegue la replica iniziale viene determinato in modo casuale. Il primo server Cassette postali nel sito di Active Directory che esegue un'analisi della topologia e rileva la nuova sottoscrizione Edge esegue la replica iniziale. Poiché tale rilevamento si basa sulla tempistica dell'analisi, qualunque server Cassette postali nel sito potrebbe eseguire la replica iniziale.

EdgeSync avvia una sessione LDAP protetta dal server Cassette postali al server Trasporto Edge. Il server Trasporto Edge fornisce il proprio certificato autofirmato e il server Cassette postali verifica che questo certificato corrisponda a quello archiviato nell'oggetto di configurazione del server Trasporto Edge in Active Directory. Dopo aver verificato l'identità del server Trasporto Edge, il server Cassette postali fornisce le credenziali dell'account ESRA.edge.*Mailboxname.\#* al server Trasporto Edge, che ne effettua la verifica in base all'account archiviato in AD LDS.

Quindi, il servizio EdgeSync sul server Cassette postali invia i dati relativi a topologia, configurazione e destinatari da Active Directory ad AD LDS. La modifica dell'oggetto di configurazione server Trasporto Edge in Active Directory viene replicata in AD LDS. AD LDS riceve gli elementi ESRA.edge.*Mailboxname.\#* appena aggiunti e il servizio credenziali di Microsoft Exchange crea l'account AD LDS corrispondente. Tali account saranno quindi disponibili per autenticare le sessioni di sincronizzazione EdgeSync pianificate in seguito.

## Servizio credenziali di Microsoft Exchange

Il servizio credenziali di Microsoft Exchange fa parte del processo di sottoscrizione Edge che viene eseguito solo sul server Trasporto Edge. Questo servizio consente di creare in AD LDS account ESRA reciproci in modo che un server Cassette postali possa autenticarsi su un server Trasporto Edge per eseguire la sincronizzazione EdgeSync. Il servizio EdgeSync non comunica direttamente con il servizio credenziali di Microsoft Exchange. Quest'ultimo comunica con AD LDS e installa le credenziali dell'account ESRA ogni volta che vengono aggiornate dal server Cassette postali.

Inizio pagina

## Autenticare le sessioni di sincronizzazione pianificate

Al termine della sincronizzazione iniziale EdgeSync, viene definita una pianificazione di sincronizzazione e i dati modificati in Active Directory vengono aggiornati a intervalli regolari in AD LDS. Un server Cassette postali avvia una sessione LDAP protetta con l'istanza AD LDS sul server Trasporto Edge. L'istanza AD LDS fornisce il certificato autofirmato al server Cassette postali per dimostrare la propria identità, mentre il server Cassette postali fornisce ad AD LDS le proprie credenziali ESRA.edge. La password dell'account ESRA.edge è crittografata tramite la chiave pubblica del certificato autofirmato del server Cassette postali. Solo questo server Cassette postali specifico può utilizzare tali credenziali per autenticarsi in AD LDS.

Inizio pagina

## Rinnovo degli account di replica EdgeSync

La password dell'account ESRA deve soddisfare i criteri password del server locale. Per evitare che la procedura di rinnovo della password provochi errori di autenticazione temporanei, sette giorni prima che scada il primo account viene creato un secondo account ESRA.edge, con data di validità a partire da tre giorni prima della scadenza del primo account ESRA. Quando il secondo account ESRA.edge diventa effettivo, EdgeSync smette di utilizzare il primo account e inizia a utilizzare il secondo. Quando viene raggiunta la data di scadenza del primo account, le relative credenziali vengono eliminate. Questa procedura di rinnovo continua finché non viene rimossa la sottoscrizione Edge.

Inizio pagina

