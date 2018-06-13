---
title: 'Opzioni di trasporto nelle distribuzioni ibride di Exchange 2013/Exchange 2010: Exchange 2013 Help'
TOCTitle: Opzioni di trasporto nelle distribuzioni ibride di Exchange 2013/Exchange 2010
ms:assetid: 57f93b81-d153-4f0d-81f6-085130319803
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn393960(v=EXCHG.150)
ms:contentKeyID: 59634757
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Opzioni di trasporto nelle distribuzioni ibride di Exchange 2013/Exchange 2010

Questo argomento è in fase di definizione.  

_**Si applica a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

In una distribuzione ibrida possono essere presenti cassette postali che risiedono nell'organizzazione locale di Exchange e anche in una organizzazione di Exchange Online. Un componente critico per fare che queste due organizzazioni separate appaiano agli utenti come una organizzazione combinata e che i messaggi siano scambiati tra loro è il trasporto ibrido. Con il trasporto ibrido i messaggi scambiati dagli utenti di qualsiasi organizzazione vengono autenticati, crittografati e trasferiti usando Transport Layer Security (TLS), e appaiono come "interni�? a componenti di Exchange quali i ruoli di trasporto, journal e criteri antispam. Il trasporto ibrido viene configurato automaticamente dalla procedura guidata di configurazione ibrida in Exchange 2013

Affinché la configurazione del trasporto ibrido funzioni con la procedura guidata di configurazione ibrida, l'endpoint SMTP che accetta le connessioni da Microsoft Exchange Online Protection (EOP), che gestisce il trasporto per l'organizzazione Exchange Online, deve essere un server di Accesso client Exchange 2013, un server Trasporto Edge Exchange 2013 o un server Trasporto Edge SP3 Exchange Server 2010.


> [!IMPORTANT]
> Non possono essere presenti altri servizi o host SMTP fra i server Accesso client di Exchange 2013 locali o un server Trasporto Edge di Exchange 2013/Exchange&nbsp;2010 SP3 ed EOP. L'informazione aggiunta ai messaggi per abilitare le funzionalità di trasporto ibrido viene rimossa quando i messaggi attraversano un server non Exchange 2013, server anteriori a Exchange 2010 SP3 o un host SMTP. Se nell'organizzazione non sono stati distribuiti server Trasporto Edge di Exchange&nbsp;2010 SP2 da utilizzare per il trasporto ibrido, è necessario effettuarne l'aggiornamento a Exchange&nbsp;2010 SP3.



I messaggi in ingresso inviati a destinatari di entrambe le organizzazioni da mittenti Internet esterni seguono un instradamento di ingresso comune. I messaggi in uscita inviati dalle organizzazioni a destinatari Internet esterni possono essere inviati tramite una route di uscita comune o possono essere inviati tramite ruote diverse.

Durante la pianificazione è necessario decidere come instradare la posta elettronica in ingresso e in uscita e configurare una distribuzione ibrida. La route seguita dai messaggi in ingresso e in uscita, inviati e ricevuti dai destinatari delle organizzazioni locale e di Exchange Online, dipende dai fattori elencati di seguito:

  - Si desidera che la posta in entrata per le cassette postali locali e di Exchange Online venga instradata attraverso Microsoft Office 365 ed EOP o tramite l'organizzazione locale?
    
    È possibile scegliere di instradare la posta Internet in arrivo per entrambe le organizzazioni attraverso l'organizzazione locale o attraverso EOP e l'organizzazione di Exchange Online. Il percorso seguito dai messagggi in entrata per entrambe le organizzazioni varia a seconda che si abiliti o meno il trasporto centralizzato della posta nella distribuzione ibrida.

  - Si desidera instradare la posta elettronica in uscita dall'organizzazione Exchange Online, e indirizzata a destinatari esterni, attraverso l'organizzazione locale o si vuole inviarla direttamente su Internet?
    
    Con il trasporto centralizzato della posta è possibile instradare tutta la posta elettronica proveniente dalle cassette postali dell'organizzazione di Exchange Online attraverso l'organizzazione locale prima che venga inviata su Internet. Questo approccio è utile negli scenari di conformità in cui la posta elettronica da e verso Internet deve essere elaborata da server locali. In alternativa, è possibile configurare Exchange Online per inviare messaggi diretti a destinatari esterni direttamente a Internet.
    

    > [!NOTE]
    > Il trasporto centralizzato della posta è consigliato solamente per le organizzazioni con specifiche esigenze di trasporto legate alla conformità. Nelle organizzazioni Exchange standard, è consigliabile non abilitare il trasporto centralizzato della posta.



  - Si desidera distribuire un server Trasporto Edge nell'organizzazione locale?
    
    Se non si desidera esporre direttamente a Internet i server Exchange 2013 interni uniti al dominio, è possibile distribuire server Trasporto Edge di Exchange 2013 o Exchange 2010 SP3 nella propria rete perimetrale. Per ulteriori informazioni sull'aggiunta di un server Trasporto Edge alla distribuzione ibrida, vedere [Server Trasporto Edge nelle distribuzioni ibride di Exchange 2013/Exchange 2010](edge-transport-servers-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md).

Indipendentemente da come si instradano i messaggi inviati e ricevuti tramite Internet, tutti i messaggi scambiati tra l'organizzazione locale e l'organizzazione Exchange Online vengono inviati utilizzando il trasporto sicuro. Per ulteriori informazioni, vedere [Trusted communication](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md) più avanti in questo argomento.

Per ulteriori informazioni sull'effetto di queste opzioni sul routing dei messaggi nell'organizzazione, vedere [Routing di trasporto nelle distribuzioni ibride di Exchange 2013/Exchange 2010](transport-routing-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md).

## Exchange Online Protection nelle distribuzioni ibride

EOP è un servizio online fornito da Microsoft che viene utilizzato da molte società per proteggere le organizzazioni locali da virus, spam, tentativi di phishing e violazioni dei criteri. In Office 365 EOP viene utilizzato per proteggere le organizzazioni di Exchange Online dalle stesse minacce. Quando ci si iscrive a Office 365 viene automaticamente creata un'azienda EOP, che viene associata all'organizzazione di Exchange Online.

Un'azienda EOP contiene varie impostazioni di trasporto della posta elettronica che possono essere configurate per l'organizzazione di Exchange Online. È possibile specificare quale dominio SMTP deve provenire da specifici indirizzi IP, richiedere un TLS e un certificato SSL (Secure Sockets Layer), evitare criteri di conformità e molto altro. EOP costituisce il punto di accesso principale all'organizzazione Exchange Online. Tutti i messaggi, indipendentemente dall'origine, devono passare attraverso EOP prima di raggiungere le cassette postali nell'organizzazione Exchange Online, e tutti i messaggi inviati dall'organizzazione Exchange Online devono passare attraverso EOP prima di raggiungere Internet.

Quando si configura una distribuzione ibrida con la procedura guidata di configurazione ibrida, tutte le impostazioni di trasporto vengono automaticamente configurate nell'organizzazione locale e nell'azienda EOP incluse nell'organizzazione Exchange Online. La procedura guidata di configurazione ibrida consente di configurare tutti i connettori in ingresso e in uscita e altre impostazioni in questa azienda EOP, in modo da proteggere i messaggi scambiati fra l'organizzazione locale e l'organizzazione Exchange Online e da instradarli verso la destinazione corretta. Anche le impostazioni di trasporto personalizzate per l'organizzazione Exchange Online possono essere configurate nell'azienda EOP, se necessario.

## Comunicazione attendibile

Per proteggere i destinatari sia nell'organizzazione locale che nell'organizzazione Exchange Online, e per assicurare che i messaggi scambiati fra le organizzazioni non vengano intercettati e letti, il trasporto tra l'organizzazione locale ed EOP viene configurato per l'uso forzato di TLS. Il trasporto TLS usa certificati Secure Sockets Layer (SSL) forniti da un'autorità di certificazione (CA) attendibile di terze parti. Anche i messaggi scambiati fra EOP e l'organizzazione Exchange Online utilizzano TLS.

Quando si utilizza il trasporto TLS, i server di invio e ricezione esaminano il certificato configurato sull'altro server. Il nome soggetto o uno dei nomi alternativi soggetto (SAN) configurato sui certificati deve essere uguale al nome di dominio completo (FQDN) che un amministratore ha specificato esplicitamente sull'altro server. Ad esempio, se la configurazione di EOP prevede l'accettazione e la protezione dei messaggi inviati dal nome di dominio completo mail.contoso.com, il server Accesso client o Trasporto Edge locale di invio deve possedere un certificato SSL con mail.contoso.com nel nome dell'oggetto o SAN. Se questa condizione non è soddisfatta, EOP rifiuta la connessione.


> [!NOTE]
> Non è necessario che il nome di dominio completo sia uguale al nome di dominio di posta elettronica dei destinatari. L'unico requisito è che il nome di dominio completo nel nome soggetto o nome alternativo soggetto del certificato sia uguale al nome di dominio completo accettato dai server di invio e ricezione.



Oltre a utilizzare TLS, i messaggi tra le organizzazioni sono trattati come "interni�?. In questo modo i messaggi possono ignorare le impostazioni di antispam e altri servizi.

Per ulteriori informazioni sui certificati SSL e sulla protezione del dominio, vedere [Requisiti dei certificati per le distribuzioni ibride](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md) e [Informazioni sui certificati TLS](http://go.microsoft.com/fwlink/p/?linkid=187237).

