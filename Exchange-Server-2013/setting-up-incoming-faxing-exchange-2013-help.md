---
title: 'Impostazione di fax in arrivo: Exchange 2013 Help'
TOCTitle: Impostazione di fax in arrivo
ms:assetid: 5d3cae58-1690-424d-9bef-011911d0b608
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633468(v=EXCHG.150)
ms:contentKeyID: 52057253
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostazione di fax in arrivo

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Messaggistica unificata di Microsoft Exchange si basa su soluzioni del partner fax certificate per funzionalità avanzate, come i fax o il routing dei fax in uscita. Per impostazione predefinita, i server di Exchange non sono configurati per recapitare i fax in arrivo ad un utente abilitato per messaggistica unificata. Al contrario, un server di Exchange reindirizza le chiamate fax in arrivo a una soluzione del partner fax certificata. Il server del partner fax riceve i dati e li invia alla cassetta postale dell'utente tramite un messaggio di posta elettronica con allegato il fax in formato .tif.

Per ulteriori informazioni sui partner fax, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238)

## Distribuzione e configurazione dei fax

Messaggistica unificata inoltra le chiamate fax in arrivo a una soluzione del partner fax dedicato che, a sua volta, stabilisce la chiamata fax con il mittente del fax e riceve il fax per conto dell'utente abilitato per messaggistica unificata. Tuttavia, per consentire agli utenti abilitati per messaggistica unificata di ricevere messaggi fax nelle casette postali, è necessario dapprima abilitare i fax in arrivo e impostare l'URI (Uniform Resource Identifier) del partner fax sul criterio cassetta postale di messaggistica unificata collegato a uno o più utenti abilitati per messaggistica unificata. È possibile consentire o impedire l'invio dei fax in arrivo sui dial plan e sui criteri casetta postale di messaggistica unificata oltre che sulla cassetta postale di un utente abilitato per messaggistica unificata. Per informazioni dettagliate, vedere i seguenti argomenti:

  - [Consenti agli utenti di stesso dial plan di ricevere fax](allow-users-in-the-same-dial-plan-to-receive-faxes-exchange-2013-help.md)

  - [Impedire agli utenti in stesso dial plan di ricevere fax](prevent-users-in-the-same-dial-plan-from-receiving-faxes-exchange-2013-help.md)

  - [Abilita fax per un gruppo di utenti](enable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [Disabilitare la funzionalità fax per un gruppo di utenti](disable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [Consentire agli utenti di ricevere fax](enable-a-user-to-receive-faxes-exchange-2013-help.md)

  - [Impedire a un utente di ricevere fax](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)

## Passaggio 1: Distribuire la messaggistica unificata

Prima di impostare l'invio di fax per l'organizzazione locale o ibrida, è necessario distribuire correttamente i server Accesso client e Cassette postali e configurare il gateway VoIP (Voice over IP) supportato per poter inviare i fax. Per informazioni dettagliate sulla distribuzione di messaggistica unificata, vedere [Distribuzione della messaggistica unificata di Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md). Per informazioni più dettagliate su come distribuire i gateway VoIP e IP Private Branch eXchange (PBX), vedere [Connettersi alla messaggistica unificata al sistema telefonico in uso](connect-um-to-your-telephone-system-exchange-2013-help.md).


> [!IMPORTANT]
> L'invio e la ricezione dei fax tramite T.38 o G.711 non sono supportati in un ambiente in cui messaggistica unificata, Microsoft&nbsp;Office Communications Server 2007 R2 o Microsoft Lync Server sono integrati.



## Passaggio 2: Configurare i server del partner fax

Successivamente, è necessario abilitare fax in arrivo e configurare l'URI del partner fax in ogni criterio cassetta postale di messaggistica UNIFICATA che richiedono all'interno dell'organizzazione. Per distribuire correttamente fax in arrivo, è necessario integrare una soluzione di fax certified partner con la messaggistica unificata di Exchange. Per ulteriori informazioni, vedere [Fax advisor per la messaggistica UNIFICATA di Exchange](fax-advisor-for-exchange-um-exchange-2013-help.md). Per un elenco di partner fax certificati, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238)


> [!NOTE]
> Poiché il server del partner fax è esterno all'organizzazione, è necessario configurare le porte del firewall per autorizzare le porte del protocollo T.38 a inviare fax in una rete basata su IP. Per impostazione predefinita, il protocollo T.38 utilizza le porte TCP 6004 e UDP (User Datagram Protocol) 6044, sebbene questa sia a discrezione del produttore dell'hardware. È necessario configurare le porte del firewall per autorizzare i dati fax che utilizzano le porte TCP, UDP o gli intervalli di porta definiti dal produttore.



## Passaggio 3: Abilitare l'invio dei fax su messaggistica unificata

È necessario configurare correttamente tre componenti, affinché gli utenti siano in grado di ricevere i fax tramite messaggistica unificata:

  - Dial plan di messaggistica unificata

  - Criteri cassetta postale di messaggistica unificata

  - Cassette postali di messaggistica unificata

L'invio di fax può essere abilitato o disabilitato per i dial plan, i criteri cassetta postale o una singola cassetta postale dell'utente abilitato per messaggistica unificata. È possibile abilitare o disabilitare i criteri cassetta postale di messaggistica unificata per l'invio di fax utilizzando l'interfaccia di amministrazione di Exchange o Exchange Management Shell. È necessario attivare e disattivare i dial plan e i singoli utenti abilitati per messaggistica unificata tramite Exchange Management Shell. Nella tabella riportata di seguito vengono mostrate le opzioni disponibili, oltre che i cmdlet e i parametri utilizzati per attivare e disattivare l'invio di fax.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente di messaggistica unificata</th>
<th>Abilitare e disabilitare tramite l'interfaccia di amministrazione di Exchange</th>
<th>Esempio di abilitazione dei fax tramite Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dial plan</p></td>
<td><p>No</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -faxenabled $true</code></p></td>
</tr>
<tr class="even">
<td><p>Criterio cassetta postale di messaggistica unificata</p></td>
<td><p>Sì</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyPolicy -AllowFax $true</code></p></td>
</tr>
<tr class="odd">
<td><p>Utente abilitato per messaggistica unificata</p></td>
<td><p>No</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -faxenabled $true</code></p></td>
</tr>
</tbody>
</table>


Anche se la cassetta postale dell'utente e il dial plan di messaggistica unificata consentono la ricezione dei fax, per impostazione predefinita è necessario abilitare i fax in entrata sul criterio cassetta postale assegnato all'utente abilitato per messaggistica unificata e quindi immettere l'URI del server del partner fax.

Per abilitare la ricezione dei fax da parte degli utenti abilitati alla messaggistica unificata, procedere come segue:

  - Verificare che ciascun dial plan di messaggistica unificata consenta agli utenti associati al dial plan di ricevere fax. Per impostazione predefinita, tutti gli utenti associati a un dial plan possono ricevere fax. Per consentire la ricezione dei messaggi fax nella cassetta postale degli utenti abilitati alla messaggistica unificata, è necessario configurare ogni gateway VoIP o IP PBX al fine di accettare le chiamate fax in arrivo. È inoltre necessario consentire agli utenti collegati al dial plan di ricevere messaggi fax. Per ulteriori informazioni sull'abilitazione o la disabilitazione della ricezione dei fax da parte degli utenti collegati a un dial plan, vedere [Consentire agli utenti di ricevere fax](enable-a-user-to-receive-faxes-exchange-2013-help.md).
    

    > [!NOTE]
    > Se si impedisce la ricezione dei messaggi fax su un dial plan, nessun utente associato ad esso sarà in grado di ricevere fax, anche se le proprietà di un singolo utente vengono configurate per consentire la ricezione dei fax. L'abilitazione o la disabilitazione dell'invio fax per un dial plan di messaggistica unificata ha la precedenza sulle impostazioni per un singolo utente abilitato alla messaggistica unificata.



  - Configurare il criterio cassetta postale associato all'utente abilitato alla messaggistica unificata. Il criterio cassetta postale di messaggistica unificata deve essere configurato per consentire la ricezione fax, compresi l'URI e il nome del server del partner fax. È necessario che il parametro *FaxServerURI* rispetti la forma seguente: sip:\<*URI del server fax*\>:\<*porta*\>;\<*trasporto*\>, dove "URI del server fax" indica un nome di dominio completo (FQDN) o un indirizzo IP del server del partner fax. La "porta" indica la porta su cui il server fax rimane in attesa delle chiamate fax in arrivo, mentre "trasporto" indica il protocollo di trasporto utilizzato per il fax in arrivo (UDP, TCP o TLS). Ad esempio, è possibile configurare un criterio cassetta postale di messaggistica unificata per ricevere un fax nel modo seguente.
    
        Set-UMMailboxPolicy MyUMMailboxPolicy -AllowFax $true -FaxServerURI "sip:faxserver.abc.com:5060;transport=tcp"

  - Per ulteriori informazioni, vedere [Impostare il partner fax URI del server a consentire l'invio di fax](set-the-partner-fax-server-uri-to-allow-faxing-exchange-2013-help.md).
    

    > [!WARNING]
    > Anche se è possibile includere più voci nel formato con il parametro <EM>FaxServerURI</EM> separandole con un punto e virgola, ne verrà utilizzata solo una. Questo parametro consente di utilizzare una sola voce poiché l'aggiunta di più voci non permette di bilanciare il carico delle richieste di fax.



  - Verificare che la cassetta postale abilitata alla messaggistica unificata sia in grado di ricevere i messaggi fax. Per impostazione predefinita, tutti gli utenti associati a un dial plan possono ricevere fax. Tuttavia, in alcune situazioni un utente non può ricevere i fax, in quanto la funzionalità è stata disabilitata per la cassetta postale. Per ulteriori informazioni sull'abilitazione della ricezione fax per un utente abilitato alla messaggistica unificata, vedere [Consentire agli utenti di ricevere fax](enable-a-user-to-receive-faxes-exchange-2013-help.md).
    
    È possibile impedire a un singolo utente associato a un dial plan di ricevere i messaggi fax. A tale scopo, configurare le proprietà per l'utente utilizzando il cmdlet **Set-UMMailbox** in Shell. Inoltre, è possibile utilizzare il cmdlet **Set-UMMailbox** per impedire a più utenti di ricevere i messaggi fax. Per ulteriori informazioni su come impedire a uno o più utenti di ricevere messaggi fax, vedere [Impedire a un utente di ricevere fax](prevent-a-user-from-receiving-faxes-exchange-2013-help.md).

## Passaggio 4: Configurare l'autenticazione

Oltre a configurare i dial plan, i criteri cassetta postale e gli utenti abilitati alla messaggistica unificata, è necessario configurare l'autenticazione tra i server Exchange e il server del partner fax. È necessario che i server Exchange siano in grado di autenticare l'origine dei messaggi provenienti dal server del partner fax. Tutti i messaggi non autenticati che si presume provengano da un server del partner fax non verranno elaborati da un server di Exchange.

Per autenticare la connessione dal server del partner fax ai server Exchange, è possibile utilizzare:

  - TLS reciproca

  - Convalida dell'ID mittente

  - Connettore dedicato di ricezione

Un connettore di ricezione dovrebbe essere sufficiente per autenticare i server del partner fax distribuiti nell'organizzazione. Il connettore di ricezione farà in modo che il server di Exchange consideri l'intero traffico proveniente dal server del partner fax come autenticato.

È necessario che il connettore di ricezione sia configurato su un server di Exchange utilizzato dal server del partner fax per inviare messaggi fax SMTP. A tale scopo, è necessario che sia configurato con i seguenti valori:

  - *AuthMechanism: ExternalAuthoritative*

  - *PermissionGroups: ExchangeServers, PartnersFax*

  - *RemoteIPRanges: {the fax server's IP address}*

  - *RequireTLS: False*

  - *EnableAuthGSSAPI: False*

  - *LiveCredentialEnabled: False*

Per ulteriori informazioni, vedere [Connettori](connectors-exchange-2013-help.md).

Se il server del partner fax invia il traffico di rete al server di Exchange di una rete pubblica, ad esempio un server del partner fax basato su un servizio ospitato su cloud, si consiglia di autenticare il server del partner fax utilizzando un controllo dell'ID mittente. Con questo tipo di autenticazione, l'indirizzo IP da cui proviene il messaggio fax è autorizzato a inviare messaggi di posta elettronica per conto del dominio del partner fax da cui si presuppone provenga il messaggio. DNS viene utilizzato per archiviare i record dell'ID mittente (o record SPF) mentre i partner fax devono pubblicare i record SPF nella zona DNS di ricerca diretta. Exchange convalida gli indirizzi IP eseguendo una query verso DNS. Tuttavia, per poter eseguire la query a DNS, è necessario che l'agente ID mittente sia in esecuzione su un server Cassette postali.

Inoltre, è possibile utilizzare TLS per crittografare il traffico di rete o TLS reciproca per la crittografia e l'autenticazione tra il server del partner fax e i server di Exchange.

