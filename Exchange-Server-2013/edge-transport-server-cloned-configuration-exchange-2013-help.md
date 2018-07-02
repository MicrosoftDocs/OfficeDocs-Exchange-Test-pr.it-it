---
title: 'Configurazione clonata del server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Configurazione clonata del server Trasporto Edge
ms:assetid: 683a6b8a-59bf-43ed-96c8-504945c2f665
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998622(v=EXCHG.150)
ms:contentKeyID: 61183408
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione clonata del server Trasporto Edge

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

I server Trasporto Edge archiviano le informazioni sulla configurazione in Active Directory Lightweight Directory Services (AD LDS). È possibile più di un server Trasporto Edge nella rete perimetrale e utilizzare un round robin DNS per facilitare il bilanciamento del traffico di rete tra i server Trasporto Edge. Il round robin è un semplice meccanismo utilizzato dai server DNS per condividere e distribuire carichi per le risorse di rete.

Per assicurare che i server Trasporto Edge utilizzino le stesse informazioni di configurazione, utilizzare gli script di configurazione clonati per duplicare le configurazioni del server di origine su un server di destinazione.

La *configurazione clonata* viene utilizzata per distribuire nuovi server Trasporto Edge in base a un server di origine configurato. Le informazioni sulla configurazione del server di origine vengono duplicate e poi esportate su file XML. che viene importato nel server di destinazione.

In questo argomento viene fornita una panoramica delle due procedure di configurazione clonata. Per la procedura dettagliata per configurare i server Trasporto Edge tramite configurazione clonata, vedere [Configurare il server Trasporto Edge utilizzando una configurazione clonata](configure-edge-transport-server-using-cloned-configuration-exchange-2013-help.md).

**Sommario**

Cloned configuration and EdgeSync

Cloned configuration process

Transport configuration information

## Configurazione clonata ed EdgeSync

Eseguire il processo EdgeSync dopo aver importato la configurazione clonata. Per l'esecuzione di ricerche dei destinatari e di attività di protezione dei messaggi da parte del server Trasporto Edge, sono necessari dati che risiedono in Active Directory. *EdgeSync* è una raccolta di processi eseguiti su un server cassette postali di Exchange 2013 per stabilire una replica monodirezionale del destinatario e le informazioni di configurazione da Active Directory sull'istanza AD LDS su un server Trasporto Edge. EdgeSync copia solo le informazioni richieste al server Edge Transport per eseguire le attività relative alla posta indesiderata e le informazioni di configurazione del connettore necessarie per abilitare il flusso di posta end-to-end. EdgeSync esegue gli aggiornamenti pianificati così da mantenere aggiornate le informazioni contenute in AD LDS.

La configurazione clonata non duplica le impostazioni di sottoscrizione Edge. I certificati utilizzati dal servizio EdgeSync non vengono clonati. È necessario eseguire il processo EdgeSync separatamente per ciascun server Trasporto Edge. EdgeSync sovrascrive le impostazioni incluse nelle informazioni di configurazione clonate e nelle informazioni sulla replica di EdgeSync. Queste impostazioni includono i connettori di invio, i connettori di ricezione, i domini accettati e i domini remoti.

## Processo di configurazione clonata

Il processo di configurazione clonata consiste di tre passaggi:

1.  esportazione della configurazione dal server di origine.
    
    Eseguire lo script ExportEdgeConfig.ps1 (presente in %ExchangeInstallPath%Scripts) per esportare le informazioni di configurazione del server di origine su un file XML intermedio.

2.  Convalida della configurazione nel server di destinazione.
    
    Eseguire lo script ImportEdgeConfig.ps1 (presente in %ExchangeInstallPath%Scripts). Questo script controlla le informazioni esistenti nel file XML intermedio per verificare che le impostazioni esportate siano valide per il server di destinazione. Procede quindi con la creazione di un file di risposta, Il file di risposta specifica le informazioni specifiche del server utilizzate quando viene importata la configurazione nel server di destinazione. Nel file di risposta sono contenute le voci per ciascuna impostazione del server di origine che non è valida per il server di destinazione. È possibile modificare queste impostazioni in modo da renderle valide per il server di destinazione. Se tutte le impostazioni sono valide, nel file di risposta non è contenuta nessuna voce.

3.  Importazione della configurazione nel server di destinazione.
    
    Lo script ImportEdgeConfig.ps1 utilizza il file XML intermedio e il file di risposta per clonare una configurazione esistente o per ripristinare nel server una configurazione specifica.

## Passo 1: esportazione della configurazione dal server di origine

Dopo aver installato e configurato il ruolo del server Trasporto Edge, eseguire lo script ExportEdgeConfig.ps1 (presente in %ExchangeInsallPath%Scripts). Questo script recupera le informazioni di configurazione del server di origine e le archivia in un file XML intermedio.

Le informazioni che seguono vengono esportate dal server di origine e archiviate nel file XML intermedio:

  - informazioni relative al servizio di trasporto e al percorso del file di registro:
    
      - *ReceiveProtocolLogPath*
    
      - *SendProtocolLogPath*
    
      - *MessageTrackingLogPath*
    
      - *PickupDirectoryPath*
    
      - *RoutingTableLogPath*

  - Informazioni relative all'agente di trasporto che includono le impostazioni di stato e di priorità per ciascun agente di trasporto.

  - Informazioni relative al connettore di invio. Se i connettori di invio vengono configurati per l'utilizzo delle credenziali, la password viene scritta nel file XML intermedio come stringa crittografata. È possibile utilizzare il parametro *-key* con gli script ImportEdgeConfig.ps1 e ExportEdgeConfig.ps1 per specificare la stringa a 32 byte da utilizzare per la crittografia e la decrittografia della password. Se non si utilizza il parametro *-key*, viene utilizzata una chiave di crittografia predefinita.

  - Informazioni relative al connettore di ricezione. Per modificare le proprietà della porta e del binding di rete locale, è necessario modificare le informazioni di configurazione nel file di risposta creato nel passo di convalida della configurazione.

  - Configurazione del dominio accettato.

  - Configurazione del dominio remoto.

  - Impostazioni di configurazione delle funzionalità di protezione da posta indesiderata:
    
      - Informazioni relative all'elenco indirizzi IP consentiti. Vengono esportate solo le voci dell'elenco indirizzi IP consentiti configurate manualmente dall'amministratore.
    
      - Informazioni relative all'elenco indirizzi IP bloccati.
    
      - Configurazione del Filtro contenuto.
    
      - Configurazione del Filtro destinatario.
    
      - Voci di riscrittura degli indirizzi.
    
      - Voci del filtro degli allegati.

Inizio pagina

## Passo 2: Convalida della configurazione nel server di destinazione

Il server di destinazione è un server Exchange 2013 con una nuova installazione del ruolo server Trasporto Edge. Per prima cosa, eseguire lo script ImportEdgeConfig.ps1 (presente in %ExchangeInsallPath%Scripts) sul server di destinazione per convalidare le informazioni esistenti nel file XML intermedio e per creare il file di risposta. Il file di risposta specifica le informazioni specifiche del server utilizzate quando viene importata la configurazione nel server di destinazione. Nel file di risposta sono contenute le voci per ciascuna impostazione del server di origine che non è valida per il server di destinazione. È necessario modificare queste impostazioni in modo da renderle valide per il server di destinazione. Se tutte le impostazioni sono valide, nel file di risposta non è contenuta nessuna voce. Il file XML intermedio può essere utilizzato per server di destinazione diversi. Il file di risposta è specifico per un dato server di destinazione.

Lo script ImportEdgeConfig.ps1 (si trova in % ExchangeInsallPath % script) effettua le seguenti attività:

  - verifica che i percorsi dei dati e dei registri possano essere creati nel server di destinazione. In caso contrario, nel file di risposta viene inserito un percorso vuoto.

  - Per ciascun connettore di invio nel file XML, lo script aggiunge una voce vuota per l'indirizzo IP di origine nel file di risposta.

  - Per ciascun connettore di ricezione nel file XML, lo script aggiunge una voce vuota per i binding di rete locale nel file di risposta.

È necessario modificare manualmente il file di risposta per fornire le seguenti informazioni relative alle impostazioni specifiche per il server:

  - Compilare i percorsi dei dati e dei registri. Se questi percorsi sono lasciati vuoti nel file di risposta, nel passaggio successivo dell'importazione della configurazione nel server di destinazione, vengono utilizzati i percorsi configurati nel file XML intermedio.

  - Per ciascuna voce del connettore di invio, completare l'indirizzo IP di origine. Se il campo viene lasciato vuoto, si verifica un errore durante il passaggio dell'importazione della configurazione.

  - Per ciascuna voce del connettore di ricezione, completare i binding di rete locale. Se i binding di rete locale vengono lasciati vuoti, si verificherà un errore durante l'importazione della configurazione nel server di destinazione.

Inizio pagina

## Passo 3: Importazione della configurazione nel server di destinazione

È possibile eseguire questo passaggio su un server di destinazione per clonare la configurazione di un server Trasporto Edge esistente o per ripristinare nel server una configurazione specifica. Eseguire lo script ImportEdgeConfig.ps1 (presente in %ExchangeInsallPath%Scripts) per convalidare e importare la nuova configurazione. Dopo aver eseguito lo script, la configurazione del server di destinazione confronta le impostazioni nel file XML intermedio e nel file di risposta.


> [!IMPORTANT]
> Si consiglia di eseguire il back up della configurazione del server esistente prima di eseguire il processo di configurazione di importazione, in questo modo se l'operazione di clonazione non riesce, è possibile ripristinare il server allo stato stabile precedente.



Questa operazione prevede l'utilizzo delle informazioni specifiche del server fornite nel file di risposta. Se un'impostazione non è specificata nel file di risposta, vengono utilizzati i dati contenuti nel file XML intermedio. Prima che la configurazione venga modificata dallo script, i dati contenuti nel file XML intermedio e nel file di risposta vengono convalidati dallo script stesso.

La configurazione di importazione consente di modificare le seguenti impostazioni di configurazione del server di destinazione:

  - La configurazione dell'agente di trasporto viene modificata.

  - I connettori esistenti nel server di destinazione vengono rimossi e aggiunti quelli presenti nel file XML intermedio.

  - I domini accettati esistenti vengono rimossi e vengono aggiunte le voci dei domini accettati presenti nel file XML intermedio.

  - I domini remoti esistenti vengono rimossi e vengono aggiunte le voci dei domini remoti presenti nel file XML intermedio.

  - Le voci esistenti dell'elenco indirizzi IP consentiti vengono rimosse e vengono aggiunte quelle presenti nel file intermedio dei domini remoti.

  - Le voci esistenti dell'elenco indirizzi IP bloccati vengono rimosse e vengono aggiunte quelle presenti nel file intermedio dei domini remoti.

  - Nel server di destinazione viene clonata la seguente configurazione di protezione da posta indesiderata:
    
      - Configurazione del Filtro contenuto
    
      - Configurazione del Filtro destinatario
    
      - Voci di riscrittura degli indirizzi
    
      - Voci del filtro degli allegati

Inizio pagina

## Informazioni sulle configurazioni di trasporto

Le impostazioni dell'oggetto di configurazione trasporto definiscono le impostazioni del trasporto dei messaggi di posta elettronica a livello di server per un server Trasporto Edge. Una volta importato il file XML intermedio nel server di destinazione, tutte le impostazioni dell'oggetto di configurazione del trasporto verranno importate, ad eccezione di quanto riportato di seguito.

  - Nomi generici e date di creazione dal file XML esportato

  - Informazioni sul connettore di invio

  - Informazioni sul connettore di ricezione

  - Voci del filtro degli allegati

  - Voce dell'attributo **MaxDumpsterSizePerStorageGroup**

Una volta completato il processo di importazione, è possibile anche configurare le impostazioni utilizzando il cmdlet **Set-TransportConfig**. Per ulteriori informazioni, vedere [Set-TransportConfig](https://technet.microsoft.com/it-it/library/bb124151\(v=exchg.150\)).

Gli attributi presenti nella seguente tabella sono associati all'oggetto di configurazione trasporto e ai valori predefiniti. È possibile configurare l'oggetto sia sui server cassette postali sia sui server Trasporto Edge. Tuttavia, molti attributi vengono applicati solo al servizio di trasporto su server cassette postali Exchange 2013. La configurazione di tali attributi su un server Trasporto Edge non avrà effetti.

### Attributi di configurazione trasporto e valori predefiniti

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Attributo</th>
<th>Descrizione</th>
<th>Valore predefinito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ClearCategories</strong></p></td>
<td><p>Questo attributo specifica se le categorie di Microsoft Outlook devono essere eliminate durante la conversione del contenuto.</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><strong>GenerateCopyOfDSNFor</strong></p></td>
<td><p>Questo attributo consente di specificare i codici DSN (Delivery Status Notification) che causano la copia del messaggio DSN nell'indirizzo di posta elettronica del postmaster. I codici DSN devono essere immessi nel formato <em>x.y.z</em> separati da virgole.</p></td>
<td><p>5.4.8, 5.4.6, 5.4.4, 5.2.4, 5.2.0, 5.1.4</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalSMTPServers</strong></p></td>
<td><p>Questo attributo consente di specificare un elenco di indirizzi IP del server SMTP interno o intervalli di indirizzi IP che devono essere ignorati dall'ID mittente e dal filtro connessioni.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>JournalingReportNdrTo</strong></p></td>
<td><p>Questo attributo consente di specificare l'indirizzo di posta elettronica al quale vengono inviati i rapporti del journal se la cassetta postale del journal non è disponibile. Questo attributo non si applica alla configurazione di un server Trasporto Edge.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxDumpsterSizePerStorageGroup</strong></p></td>
<td><p>Questo attributo consente di specificare la dimensione massima del dumpster del trasporto su un server cassette postali. Questo attributo non si applica alla configurazione di un server Trasporto Edge.</p></td>
<td><p>18 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxDumpsterTime</strong></p></td>
<td><p>Questo attributo consente di specificare la lunghezza che il messaggio di posta elettronica dovrà mantenere nel dumpster del trasporto su un server cassette postali. Questo attributo non si applica alla configurazione di un server Trasporto Edge.</p></td>
<td><p>7.00:00:00</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxReceiveSize</strong></p></td>
<td><p>Questo attributo consente di specificare la dimensione massima dei messaggi che i destinatari dell'organizzazione possono ricevere. Questo attributo non si applica alla configurazione di un server Trasporto Edge.</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxRecipientEnvelopeLimit</strong></p></td>
<td><p>Questo attributo consente di specificare il numero massimo di destinatari consentiti per un singolo messaggio di posta elettronica. Questo attributo non si applica alla configurazione di un server Trasporto Edge.</p></td>
<td><p>5,000</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxSendSize</strong></p></td>
<td><p>Questo attributo consente di specificare la dimensione massima dei messaggi che i mittenti dell'organizzazione possono inviare. Questo attributo non si applica alla configurazione di un server Trasporto Edge.</p></td>
<td><p>10 MB</p></td>
</tr>
<tr class="even">
<td><p><strong>TLSReceiveDomainSecureList</strong></p></td>
<td><p>Questo attributo consente di specificare i domini remoti che utilizzano l'autenticazione MTLS (Mutual Transport Layer Security) attraverso i connettori di ricezione configurati per supportare la protezione del dominio. Più domini devono essere separati da virgole. Il carattere jolly (*) non è supportato nei domini elencati in questo attributo.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="odd">
<td><p><strong>TLSSendDomainSecureList</strong></p></td>
<td><p>Questo attributo consente di specificare i domini remoti che utilizzano l'autenticazione MTLS quando un messaggio di posta elettronica viene inviato attraverso un connettore di invio configurato per supportare la protezione del dominio e lo spazio indirizzi del dominio di destinazione. Più domini devono essere separati da virgole. Il carattere jolly (*) non è supportato nei domini elencati in questo attributo.</p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><strong>VerifySecureSubmitEnabled</strong></p></td>
<td><p>Questo attributo consente di verificare che i client di posta elettronica che inoltrano messaggi dalle cassette postali sui server Cassette postali utilizzino l'invio MAPI crittografato. Questo attributo non si applica alla configurazione di un server Trasporto Edge. I valori validi per questo attributo sono <code>$true</code> e <code>$false</code>.</p></td>
<td><p>False</p></td>
</tr>
<tr class="odd">
<td><p><strong>VoicemailJournalingEnabled</strong></p></td>
<td><p>Questo attributo consente di specificare se i messaggi vocali della messaggistica unificata devono essere inseriti nel journal dall'agente di journaling. Questo attributo non si applica alla configurazione di un server Trasporto Edge.</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Se il server Trasporto Edge viene sottoscritto successivamente nell'organizzazione Exchange, il valore dell'attributo <STRONG>InternalSMTPServers</STRONG> viene sovrascritto durante il processo EdgeSync. Per ulteriori informazioni, vedere <A href="edge-subscriptions-exchange-2013-help.md">Sottoscrizioni Edge</A>.



Inizio pagina

