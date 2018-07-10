---
title: 'Funzionalità TLS e relativa terminologia: Exchange 2013 Help'
TOCTitle: Funzionalità TLS e relativa terminologia
ms:assetid: 294ba2a9-892d-4a90-beec-9d298426b5f4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb430753(v=EXCHG.150)
ms:contentKeyID: 52063047
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Funzionalità TLS e relativa terminologia

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-06-18_

Microsoft Exchange Server 2013 fornisce funzionalità amministrative e altri potenziamenti che migliorano la gestione complessiva dei servizi TLS (Transport Layer Security). Lavorando con questa nuova funzionalità, sarà necessario comprendere alcune delle funzionalità e caratteristiche relative al TLS. Alcuni termini e alcuni concetti si riferiscono a più di una caratteristica relativa al TLS. In questo argomento, viene fornita una breve spiegazione di ogni funzionalità tesa a chiarire alcune differenze e garantire una maggiore comprensione della terminologia generale relativa a TLS e al gruppo di funzionalità di protezione del dominio:

  - **Transport Layer Security   **TLS rappresenta un protocollo standard utilizzato per consentire comunicazioni Web sicure su Internet o nelle reti Intranet. Tale protocollo consente ai client di autenticare i server oppure, facoltativamente, consente ai server di autenticare i client. Inoltre, offre un canale protetto crittografando le comunicazioni. TLS rappresenta la versione più recente del protocollo SSL (Secure Sockets Layer).

  - **Autenticazione TLS reciproca**   L'autenticazione TLS reciproca è diversa dalla normale distribuzione TLS. Normalmente, quando viene distribuito, il protocollo TLS viene utilizzato soltanto per garantire la riservatezza tramite la crittografia. Nessuna autenticazione avviene tra il mittente e il destinatario. Durante la distribuzione TLS, delle volte può capitare che soltanto il server di ricezione viene autenticato. Questa distribuzione del TLS è propria dell'implementazione HTTP del TLS. Tale implementazione, in cui soltanto il server di ricezione viene autenticato, è SSL.
    
    Con l'autenticazione TLS reciproca, ogni server verifica l'identità dell'altro server convalidando il certificato fornito dall'altro server. In questo scenario, in cui i messaggi sono ricevuti da domini esterni su connessioni verificate in un ambiente Exchange 2013, Microsoft Outlook visualizza un'icona di **Dominio protetto**.

  - **Protezione del dominio**   La protezione del dominio è una serie di caratteristiche, come la gestione del certificato, la funzionalità del connettore e il comportamento del client di Oulook, che attiva l'autenticazione reciproca TLS con una tecnologia utile e gestibile. La protezione del dominio non è supportata quando la posta viene inviata tramite un server Accesso client di Exchange 2013.

  - **TLS opportunistico**   In Exchange 2013, la procedura di installazione crea un certificato autofirmato. Per impostazione predefinita, TLS è abilitato. Ciò consente a qualsiasi sistema di invio di crittografare la sessione SMTP in ingresso in Exchange. Per impostazione predefinita, Exchange 2013 tenta di applicare TLS a tutte le connessioni remote.

  - **Trust diretto**   Per impostazione predefinita, tutto il traffico tra i server Trasporto Edge e i server Cassette postali viene autenticato e crittografato. Di nuovo, il meccanismo di base per l'autenticazione e la crittografia è l'autenticazione reciproca TLS. Anziché utilizzare la convalida X.509, in Exchange 2013 i certificati vengono autenticati tramite trust diretto. Trust diretto significa che la presenza del certificato in Active Directory o AD LDS (Active Directory Lightweight Directory Services) costituisce la convalida del certificato stesso. Active Directory è considerato un meccanismo di archiviazione attendibile. Inoltre, in questi casi è irrilevante che il certificato sia autofirmato o firmato da un'Autorità di certificazione. Quando si sottoscrive un server Trasporto Edge in un'organizzazione di Exchange, la sottoscrizione pubblica il certificato del server Trasporto Edge in Active Directory affinché i server Cassette postali possano eseguire la convalida. Il servizio Microsoft Exchange EdgeSync aggiorna AD LDS con la serie di certificati del server Cassette postali affinché il server Trasporto Edge possa eseguire la convalida.

