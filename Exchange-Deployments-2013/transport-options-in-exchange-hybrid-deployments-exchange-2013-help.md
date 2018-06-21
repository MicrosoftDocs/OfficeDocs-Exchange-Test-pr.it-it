---
title: 'Opzioni di trasporto nelle distribuzioni ibride di Exchange: Exchange 2013 Help'
TOCTitle: Opzioni di trasporto nelle distribuzioni ibride di Exchange
ms:assetid: da605a78-5429-4de8-8b04-bc4c45a41ba1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659055(v=EXCHG.150)
ms:contentKeyID: 50482159
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Opzioni di trasporto nelle distribuzioni ibride di Exchange

 

_<strong>Si applica a:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2016-12-09_

In una distribuzione ibrida possono essere presenti cassette postali che risiedono nell'organizzazione locale di Exchange e anche in una organizzazione di Exchange Online. Un componente critico per fare che queste due organizzazioni separate appaiano agli utenti come una organizzazione combinata e che i messaggi siano scambiati tra loro è il trasporto ibrido. Con il trasporto ibrido i messaggi scambiati dagli utenti di qualsiasi organizzazione vengono autenticati, crittografati e trasferiti usando Transport Layer Security (TLS) e appaiono come "interni" a componenti di Exchange quali i ruoli di trasporto, journal e criteri antispam. Il trasporto ibrido viene configurato automaticamente dalla procedura guidata di configurazione ibrida.

Affinché la configurazione del trasporto ibrido funzioni con la procedura guidata di configurazione ibrida, l'endpoint SMTP che accetta le connessioni da Exchange Online deve essere un server Cassette postali (Exchange 2016 e versioni successive), un server Accesso client (Exchange 2013), un server Trasporto Hub (Exchange 2010 e versioni precedenti) o un server Trasporto Edge (Exchange 2010 e versioni successive).


> [!IMPORTANT]
> Non inserire server, servizi o dispositivi, in grado di elaborare o modificare il traffico SMTP, tra i server Exchange locali e Office 365. Il flusso di posta sicura tra l'organizzazione di Exchange locale e Office 365 dipende dalle informazioni contenute nei messaggi inviati tra le organizzazioni. Sono supportati i firewall che consentano il traffico SMTP sulla porta TCP 25 senza alcuna modifica. Se un server, un servizio o un dispositivo elabora un messaggio inviato tra l'organizzazione di Exchange locale e Office 365, queste informazioni vengono rimosse. In questo caso, il messaggio non verrà più considerato interno all'organizzazione e sarà soggetto ai filtri di posta indesiderata, alle regole di trasporto e di journal e ad altri criteri che potrebbero non essere applicati.



I messaggi in ingresso inviati a destinatari di entrambe le organizzazioni da mittenti Internet esterni seguono un instradamento di ingresso comune. I messaggi in uscita inviati dalle organizzazioni a destinatari Internet esterni possono essere inviati tramite un instradamento comune di uscita o possono essere inviati tramite instradamenti diversi.

Durante la pianificazione è necessario decidere come instradare la posta elettronica in ingresso e in uscita e configurare una distribuzione ibrida. La route seguita dai messaggi in ingresso e in uscita, inviati e ricevuti dai destinatari delle organizzazioni locale e di Exchange Online, dipende dai fattori elencati di seguito:

  - Si desidera che la posta Internet in entrata per le cassette postali locali e di Exchange Online venga instradata tramite Exchange Online o tramite l'organizzazione locale?
    
    Il percorso seguito dai messaggi in entrata per entrambe le organizzazioni dipende da diversi fattori: dove si trova la maggior parte delle cassette postali,se si desidera proteggere l'organizzazione locale mediante l'analisi di protezione da posta indesiderata e antimalware di Office 365, dove viene configurata l'infrastruttura della conformità e così via.

  - Si desidera instradare la posta elettronica in uscita dall'organizzazione Exchange Online, e indirizzata a destinatari esterni, attraverso l'organizzazione locale o si vuole inviarla direttamente su Internet?
    
    Con il trasporto centralizzato della posta è possibile instradare tutta la posta elettronica proveniente dalle cassette postali dell'organizzazione di Exchange Online attraverso l'organizzazione locale prima che venga inviata su Internet. Questo approccio è utile negli scenari di conformità in cui la posta elettronica da e verso Internet deve essere elaborata da server locali. In alternativa, è possibile configurare Exchange Online per inviare messaggi diretti a destinatari esterni direttamente a Internet.
    

    > [!NOTE]
    > Il trasporto centralizzato della posta è consigliato solamente per le organizzazioni con specifiche esigenze di trasporto legate alla conformità. Nelle organizzazioni Exchange standard, è consigliabile non abilitare il trasporto centralizzato della posta poiché può aumentare in modo significativo la quantità di messaggi elaborati dai server locali, incrementare la larghezza di banda utilizzata e creare una dipendenza superflua sui server locali.



  - Si vuole distribuire un server Trasporto Edge nell'organizzazione locale?
    
    Se non si desidera esporre direttamente a Internet i server Exchange interni uniti al dominio, è possibile distribuire server Trasporto Edge nella propria rete perimetrale. Per ulteriori informazioni sull'aggiunta di un server Trasporto Edge alla distribuzione ibrida, vedere [Server Trasporto Edge con distribuzioni ibride](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md).

Indipendentemente da come si instradano i messaggi da e verso Internet, tutti i messaggi scambiati tra l'organizzazione locale e l'organizzazione di Exchange Online vengono inviati utilizzando il trasporto sicuro. Per ulteriori informazioni, vedere Comunicazione attendibile più avanti in questo argomento.

Per ulteriori informazioni sull'effetto di queste opzioni sul routing dei messaggi nell'organizzazione, vedere [Transport routing nelle distribuzioni ibride di Exchange](transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md).

## Exchange Online Protection nelle distribuzioni ibride

EOP è un servizio online fornito da Microsoft che viene utilizzato da molte società per proteggere le organizzazioni locali da virus, spam, tentativi di phishing e violazioni dei criteri. In Office 365 EOP viene utilizzato per proteggere le organizzazioni di Exchange Online dalle stesse minacce. Quando ci si iscrive a Office 365 viene automaticamente creata un'azienda EOP, che viene associata all'organizzazione di Exchange Online.

Un'azienda EOP contiene varie impostazioni di trasporto della posta elettronica che possono essere configurate per l'organizzazione di Exchange Online. Si può specificare quale dominio SMTP deve provenire da uno specifico indirizzo IP, richiedere un certificato TLS e Secure Sockets Layer (SSL), evitare filtri antispam o criteri di conformità e molto altro. EOP costituisce il punto di accesso principale all'organizzazione di Exchange Online. Tutti i messaggi, indipendentemente dall'origine, devono passare attraverso EOP prima di raggiungere le cassette postali nell'organizzazione di Exchange Online, e tutti i messaggi inviati dall'organizzazione di Exchange Online devono passare attraverso EOP prima di raggiungere Internet.

Quando si configura una distribuzione ibrida con la procedura guidata di configurazione ibrida, tutte le impostazioni di trasporto vengono automaticamente configurate nell'organizzazione locale e nell'azienda EOP incluse nell'organizzazione di Exchange Online. La procedura guidata di configurazione ibrida configura tutti i connettori in ingresso ed in uscita e altre impostazioni in tale azienda EOP, in modo da proteggere i messaggi scambiati fra l'organizzazione locale e l'organizzazione Exchange Online e da instradarli verso la destinazione corretta. Anche le impostazioni di trasporto personalizzate per l'organizzazione di Exchange Online possono essere configurate nell'azienda EOP, se necessario.

## Comunicazione attendibile

Per proteggere i destinatari sia nell'organizzazione locale che nell'organizzazione Exchange Online, e per assicurare che i messaggi scambiati fra le organizzazioni non vengano intercettati e letti, il trasporto tra l'organizzazione locale ed EOP viene configurato per l'uso forzato di TLS. Il componente Trasporto posta sicuro usa certificati TLS/SSL forniti da un'autorità di certificazione (CA) attendibile di terze parti. Anche i messaggi scambiati fra EOP e l'organizzazione Exchange Online utilizzano TLS.

Quando si utilizza il trasporto TLS, i server di invio e ricezione esaminano il certificato configurato sull'altro server. Il nome soggetto o uno dei nomi alternativi soggetto (SAN) configurato sui certificati deve essere uguale al nome di dominio completo (FQDN) che un amministratore ha specificato esplicitamente sull'altro server. Ad esempio, se la configurazione di EOP prevede l'accettazione e la protezione dei messaggi inviati dal nome di dominio completo mail.contoso.com, il server Accesso client o Trasporto Edge locale di invio deve possedere un certificato SSL con mail.contoso.com nel nome dell'oggetto o SAN. Se questa condizione non è soddisfatta, EOP rifiuta la connessione.


> [!NOTE]
> Non è necessario che il nome di dominio completo sia uguale al nome di dominio di posta elettronica dei destinatari. L'unico requisito è che il nome di dominio completo nel nome soggetto o nome alternativo soggetto del certificato sia uguale al nome di dominio completo accettato dai server di invio e ricezione.



Oltre a utilizzare TLS, i messaggi tra le organizzazioni sono trattati come "interni�?. In questo modo i messaggi possono ignorare le impostazioni di antispam e altri servizi.

Per ulteriori informazioni sui certificati SSL e sulla protezione del dominio, vedere [Requisiti dei certificati per le distribuzioni ibride](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md) e [Informazioni sui certificati TLS](http://go.microsoft.com/fwlink/p/?linkid=187237).

