---
title: 'Integrazione con SharePoint e Lync: Exchange 2013 Help'
TOCTitle: Integrazione con SharePoint e Lync
ms:assetid: 056b29f6-e0e9-4974-b763-002518857a93
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150480(v=EXCHG.150)
ms:contentKeyID: 50479938
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Integrazione con SharePoint e Lync

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Microsoft Exchange Server 2013 include molte funzionalità che si integrano con Microsoft SharePoint 2013 e Microsoft Lync 2013. Insieme, questi prodotti offrono un ventaglio di funzionalità che supportano l'eDiscovery aziendale e la collaborazione tramite l'utilizzo delle cassette postali del sito.

## Archiviazione, conservazione ed eDiscovery

L'archiviazione di posta elettronica e documenti, preservandoli per la durata richiesta a soddisfare requisiti relativi alle normative e requisiti aziendali e la possibilità di ricercarli velocemente per corrispondere alle richieste di eDiscovery è critico nella maggior parte delle organizzazioni. Exchange 2013, SharePoint 2013 e Lync Server 2013 insieme forniscono funzionalità integrate di archiviazione, conservazione e eDiscovery, consentendo di mantenere a disposizione dati importanti tra cassette postali Exchange, documenti SharePoint e siti web e contenuti Lync archiviati. Il Centro eDiscovery in SharePoint 2013 consente ai gestori di individuazione autorizzati di eseguire una ricerca eDiscovery in questi archivi, avere anteprime di risultati di ricerche ed esportare dati per revisioni legali.

## Archiviazione di contenuti Lync Server 2013 in Exchange 2013

Con Lync Server 2013 distribuito in una organizzazione con Exchange 2013, è possibile configurare Lync per archiviare la messaggistica istantanea e i contenuti di una riunione online, come ad esempio presentazioni condivise o documenti nella cassetta postale utente di Exchange 2013. L'archiviazione di dati Lync in Exchange 2013 consente di applicare loro i criteri di conservazione. Il contenuto di Lync archiviato compare anche in qualsiasi ricerca di eDiscovery. Per ulteriori informazioni relative all'archiviazione Lync e sulla sua distribuzione, vedere i seguenti argomenti:

  - [Pianificazione dell'archiviazione](https://go.microsoft.com/fwlink/p/?linkid=265005)

  - [Distribuzione dell'archiviazione](https://go.microsoft.com/fwlink/p/?linkid=265006)

## Ricerca Exchange, SharePoint e Lync utilizzando SharePoint 2013 eDiscovery Center

Exchange 2013 consente a SharePoint 2013 di effettuare ricerche nei contenuti delle cassette postali di Exchange utilizzando l'API di ricerca federata. SharePoint 2013 fornisce un Centro eDiscovery per consentire al personale autorizzato di eseguire una eDiscovery. Microsoft Search Foundation fornisce una comune infrastruttura di indicizzazione e una infrastruttura di ricerca a Exchange 2013 e SharePoint 2013 e consente di utilizzare la stessa sintassi di ricerca in entrambe le applicazioni. Questo assicura che una ricerca eDiscovery eseguita in SharePoint 2013 restituisce gli stessi risultati Exchange 2013 della stessa ricerca effettuata utilizzando In-Place eDiscovery in Exchange 2013. il Centro eDiscovery SharePoint 2013 consente di esportare i contenuti restituiti da una ricerca eDiscovery, incluso l'esportazione di contenuti Exchange 2013 in un file PST.

Per ulteriori dettagli, vedere i seguenti argomenti:

  - [eDiscovery sul posto](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)

  - [Archiviazione sul posto e conservazione per controversia legale](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-and-litigation-holds)

  - [Configurare eDiscovery in SharePoint 2013](https://go.microsoft.com/fwlink/p/?linkid=257727)

  - [Novità di eDiscovery in SharePoint Server 2013](https://go.microsoft.com/fwlink/?linkid=275091)

  - [Configurare Exchange per SharePoint eDiscovery Center](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)

## Cassette postali del sito

In numerose organizzazioni, le informazioni risiedono in due differenti archivi, la pasta elettronica in Microsoft Exchange e i documenti in SharePoint, con due interfacce diverse per accedervi. Questo provoca un'esperienza utente disgiunta e ostacola una collaborazione efficace. Le cassette postali del sito consentono agli utenti di collaborare efficientemente mettendo insieme posta elettronica di Exchange e documenti SharePoint. Per gli utenti, una cassetta postale del sito serve come uno schedario, fornendo un posto dove archiviare messaggi di posta elettronica su progetti e documenti ai quali possono accedere solo i membri del sito. Le cassette postali del sito sono replicate in Outlook 2013 e offrono agli utenti facile accesso alla posta elettronica e ai documenti dei progetti che li interessano. Inoltre, è possibile accedere agli stessi contenuti direttamente dallo stesso sito SharePoint.

All'interno di una cassetta postale del sito, i contenuti sono classificati per appartenenza. Exchange memorizza la posta elettronica, fornendo agli utenti la stessa visualizzazione per le conversazioni tramite posta elettronica utilizzate ogni giorno per le loro cassette postali. SharePoint archivia i documenti, registrando la creazione condivisa di documenti e di controllo delle versioni in una tabella. Exchange sincronizza una quantità sufficiente di metadati da SharePoint per creare la visualizzazione del documento in Outlook (ad esempio, nome del documento, data ultima modifica, ultimo autore modificatore, dimensioni).

Le cassette postali del sito sono predisposte e gestite da SharePoint 2013. Per ulteriori dettagli, vedere i seguenti argomenti:

  - [Cassette postali del sito](site-mailboxes-exchange-2013-help.md)

  - [Configurare cassette postali del sito in SharePoint Server 2013](https://go.microsoft.com/fwlink/p/?linkid=258264)

## Archivio unico dei contatti

L'archivio unico dei contatti (UCS) è una funzionalità che fornisce una interfaccia utente coerente per i contati tra i prodotti Microsoft Office. Questa funzionalità consente agli utenti di archiviare tutte le informazioni sui contatti nelle proprie cassette postali Exchange 2013 in modo che le stesse informazioni sui contatti siano disponibili globalmente tra Lync, Exchange, Outlook e Outlook Web App.

Dopo l'installazione in un ambiente con Exchange 2013Lync Server 2013 e aver configurato l'autenticazione da server a server tra i due, gli utenti possono avviare la migrazione dei contatti esistenti dal Lync Server 2013 a Exchange 2013. Per ulteriori informazioni, vedere [Planning and Deploying Unified Contact Store](https://go.microsoft.com/fwlink/p/?linkid=275092).

## Foto utente

Foto dell'utente è una funzionalità che consente di archiviare foto dell'utente ad alta risoluzione in Exchange 2013 accessibile dalle applicazioni client, inclusi Outlook, Outlook Web App, SharePoint 2013, Lync 2013 e client di posta elettronica mobile. Una foto a bassa risoluzione viene archiviata in Active Directory. Come con archivi contatti unificato, foto dell'utente consentono all'organizzazione garantire una foto dei profili utente coerente che può essere utilizzata dalle applicazioni client senza la necessità di ogni applicazione abbia il proprio foto dell'utente e i diversi modi per aggiungere e gestirle. È possibile gestire le loro foto utilizzando Outlook Web App, SharePoint 2013 o Lync 2013. Per informazioni sulla gestione delle immagini in Outlook Web App, vedere [il mio account](https://go.microsoft.com/fwlink/p/?linkid=269646).

## Presenza di Lync in Outlook Web App

In ambienti Exchange 2013 con installato Lync Server 2013, è possibile configurarli per abilitare gli utenti a vedere le informazioni sulla disponibilità in Outlook Web App. Gli utenti possono vedere i propri contatti di messaggistica istantanea e i gruppi nel pannello di navigazione di Outlook Web App, rispondere o iniziare una sessione di messaggistica istantanea da Outlook Web App e gestire i propri contatti di messaggistica istantanea e i gruppi.

## Autenticazione OAuth

Exchange 2013, SharePoint 2013 e Lync Server 2013 forniscono la funzionalità in comune tra i prodotti descritta in precedenza utilizzando il protocollo di autorizzazione OAuth per l'autenticazione "da server a server". L'utilizzo dello stesso protocollo di autenticazione consente a queste applicazioni di autenticarsi tra loro in modo semplice e sicuro. Il meccanismo di autenticazione supporta l'autenticazione come una applicazione utilizzando il contesto di un account collegato e la rappresentazione di un utente quando la richiesta di accesso viene effettuata nel contesto utente.

OAuth è un protocollo di autorizzazione standard utilizzato da numerosi siti web e servizi web. Consente ai client di accedere alle risorse offerte da un server di risorse senza dover specificare un nome utente e password. L'autenticazione viene eseguita da un server di autorizzazione attendibile dal proprietario della risorsa, che fornisce i client con un token di accesso. Il token concede l'accesso a un insieme specifico di risorse per un periodo specificato. Per informazioni dettagliate sulla Exchange 2013 dell'implementazione di OAuth, vedere [\[MS-XOAUTH\]: OAuth 2.0 autorizzazione Protocol Extensions](https://go.microsoft.com/fwlink/p/?linkid=275093).

**OAuth in distribuzioni locali**

All'interno di distribuzioni locali, Exchange 2013, SharePoint 2013 e Lync Server 2013 non è necessario un server di autorizzazioni per distribuire token. Ciascuna di queste applicazioni emette i propri token auto contrassegnati per accedere alle risorse fornite dalle altre applicazioni. L'applicazione che fornisce l'accesso alle risorse, ad esempio Exchange 2013, deve considerare attendibile il token presentato dall'applicazione chiamante. Un trust viene stabilito creando una configurazione *applicazione partner* per l'applicazione chiamante, la quale include ApplicationID, certificato e AuthMetadataUrl dell'applicazione chiamante. Exchange 2013, SharePoint 2013 e Lync Server 2013 pubblicano il loro documento dei metadati di autorizzazione in un URL noto.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Server</strong></p></td>
<td><p><strong>AuthMetadataUrl</strong></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/autodiscover/metadata/json/1</code></p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/metadata/json/1</code></p></td>
</tr>
<tr class="even">
<td><p>SharePoint 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/_layouts/15/metadata/json/1</code></p></td>
</tr>
</tbody>
</table>


**Exchange 2013 Server Auth Certificate**

Il programma di installazione di Exchange 2013 crea un certificato auto firmato con il nome descrittivo Microsoft Exchange Server Auth Certificate. Il certificato viene replicato su tutti i server front-end nell'organizzazione di Exchange 2013. L'identificazione personale del certificato viene specificata nella configurazione delle autorizzazioni di Exchange 2013, insieme al suo nome di servizio, un GUID noto che rappresenta Exchange 2013 locale. Exchange utilizza la configurazione delle autorizzazioni per pubblicare il suo documento dei metadati di autorizzazione.


> [!IMPORTANT]
> Il Server Auth Certificate predefinito creato da Exchange 2013 è valido per cinque anni. È necessario verificare che la configurazione di autorizzazione comprenda un certificato corrente.



Quando Exchange 2013 riceve una richiesta di accesso da una applicazione partner tramite Servizi Web Exchange (EWS), analizza la testata di `www-authenticate` della richiesta https, che contiene il token di accesso firmato dal server chiamante utilizzando la chiave privata. Il modulo di autenticazione convalida il token di accesso utilizzando la configurazione dell'applicazione partner. Quindi concede l'accesso alle risorse in base alle autorizzazioni RBAC concesse all'applicazione. Se il token di accesso è per conto di un utente, vengono controllate le autorizzazioni RBAC concesse all'utente. Ad esempio, se un utente esegue una ricerca eDiscovery utilizzando il Centro eDiscovery in SharePoint 2013, Exchange controlla se l'utente è membro del gruppo di ruoli Gestione individuazione o se è in possesso del ruolo Ricerca cassette postali e se le cassette postali nelle quali si effettua la ricerca rientrano nell'ambito di assegnazione del ruolo RBAC. Per ulteriori dettagli, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

## Gestione autenticazione OAuth

In Exchange 2013, sono presenti due oggetti di configurazione che si devono gestire con l'autenticazione OAuth con le applicazioni partner:

  - **AuthConfig**   Il AuthConfig creato da Exchange 2013 il programma di installazione e viene utilizzato per pubblicare i metadati di autorizzazione. Non è necessario gestire la configurazione di autenticazione, ad eccezione to effettuare il provisioning di un nuovo certificato quando il certificato esistente all'incirca di scadenza. In questo caso, è possibile rinnovare il certificato esistente e configurare il nuovo certificato come certificato successivo in AuthConfig e della data effettiva. Il nuovo certificato verrà replicato automaticamente in altri Exchange 2013 nell'organizzazione, il documento dei metadati di autorizzazione viene aggiornato con i dettagli del nuovo certificato e attraversa il AuthConfig per il nuovo certificato alla data effettiva.

  - **Applicazioni partner**   Per consentire alle applicazioni partner richiedere i token di accesso a Exchange 2013, è necessario creare una configurazione dell'applicazione partner. Exchange 2013 fornisce lo script `Configure-EnterprisePartnerApplication.ps1` , che consente di effettuare rapidamente e crea con facilità le configurazioni delle applicazioni partner e ridurre al minimo gli errori di configurazione. Per ulteriori informazioni, vedere [Configurazione dell'autenticazione OAuth con SharePoint 2013 e Lync 2013](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md).

