---
title: 'Connettori di ricezione: Exchange 2013 Help'
TOCTitle: Connettori di ricezione
ms:assetid: 17751a60-39fe-433f-84d2-bfc14ff4ba51
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996395(v=EXCHG.150)
ms:contentKeyID: 50480113
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Connettori di ricezione

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

I connettori di ricezione controllano il flusso di messaggi in ingresso nell'organizzazione di Exchange. Sono configurati su computer che utilizzano Microsoft Exchange Server 2013 con il servizio Trasporto oppure nel servizio Front-end su un server Accesso client. Possono essere creati nell'interfaccia di amministrazione di Exchange o in Exchange Management Shell.

Per impostazione predefinita, i connettori di ricezione necessari per il flusso di posta interno vengono creati automaticamente quando si installa un server Accesso client o un server Cassette postali.

I server di Exchange 2013 che utilizzano il servizio Trasporto hanno bisogno dei connettori di ricezione per poter ricevere messaggi da Internet, da client di posta elettronica e da altri server di posta elettronica. Un connettore di ricezione controlla le connessioni in ingresso nell'organizzazione Exchange.

Ciascun connettore di ricezione è in ascolto delle connessioni in ingresso che corrispondono alle impostazioni del connettore di ricezione. Un connettore di ricezione attende le connessioni ricevute tramite un determinato indirizzo IP locale, una porta e da un intervallo di indirizzi IP specificato. È possibile creare un connettore di ricezione per controllare quali server ricevono messaggi da un determinato indirizzo IP o intervallo di indirizzi IP e per configurare determinate proprietà dei connettori per i messaggi ricevuti da un determinato indirizzo IP, quale un indirizzo che consente messaggi di dimensioni maggiori o più destinatari per messaggio. È anche possibile assegnare un ambito al connettore di ricezione utilizzando il parametro *TlsCertificateName* del cmdlet **Set-ReceiveConnector**, che consente di specificare il certificato da utilizzare per il connettore.

I connettori di ricezione vengono applicati a un solo server e determinano in che modo tale server attende le connessioni. Quando si crea un connettore di ricezione su un server Cassette postali che utilizza il servizio Trasporto, tale connettore viene archiviato in Active Directory come oggetto figlio del server su cui è stato creato.

Nel caso in cui fossero necessari ulteriori connettori di ricezione per scenari specifici, è possibile crearli utilizzando l'interfaccia di amministrazione di Exchange o Exchange Management Shell. Ciascun connettore di ricezione deve utilizzare una combinazione univoca di binding di indirizzi IP, assegnazioni di numeri di porta e intervalli di indirizzi IP remoti dai quali accettare la posta.

Per ulteriori informazioni sulla creazione di un connettore esterno, vedere [Le procedure di connettore di ricezione](receive-connector-procedures-exchange-2013-help.md).

**Sommario**

Connettori di ricezione predefiniti creati durante l'installazione

Connettori di ricezione predefiniti creati su un server Cassette postali che utilizza il servizio Trasporto

Connettori di ricezione predefiniti creati su un server Trasporto front-end

Tipi di connettore di ricezione

Gruppi di autorizzazioni per il connettore di ricezione

Specifiche del tipo di connettore di ricezione

Autorizzazioni del connettore di ricezione

Impostazioni di autenticazione del connettore di ricezione

Nuove funzionalità del connettore di ricezione in Exchange 2013

## Connettori di ricezione predefiniti creati durante l'installazione

Determinati connettori di ricezione vengono creati per impostazione predefinita quando si installa il ruolo del server Cassette postali.

## Connettori di ricezione predefiniti creati su un server Cassette postali che utilizza il servizio Trasporto

Quando si installa un ruolo del server Cassette postali che utilizza il servizio Trasporto, vengono creati due connettori di ricezione. Non è necessario alcun connettore di ricezione aggiuntivo per normali operazioni e nella maggior parte dei casi non è necessario modificare la configurazione dei connettori di ricezione predefiniti. Tali connettori sono:

  - **\<nome server\> predefinito**   Accetta le connessioni dai server Cassette postali che utilizzano il servizio Trasporto e dai server Edge.

  - **Nome server \<nome server\>**   Accetta connessioni dai front-end. In genere, i messaggi vengono inviati a un server front-end su SMTP.

A ogni connettore è assegnato un valore *TransportRole*. È possibile utilizzarlo per determinare il ruolo nel quale viene eseguito il connettore. Può essere utile nei casi in cui si eseguono più ruoli su un singolo server. Nel caso dei connettori di ricezione precedentemente menzionati, il relativo valore *TransportRole* è **HubTransport**.

Per visualizzare i connettori di ricezione predefiniti e i relativi valori dei parametri, è possibile utilizzare il cmdlet [Get-ReceiveConnector](https://technet.microsoft.com/it-it/library/aa998618\(v=exchg.150\)).

## Connettori di ricezione predefiniti creati su un server Trasporto front-end

Durante l'installazione, vengono creati tre connettori di ricezione sul server Trasporto front-end o Accesso client. Il connettore di ricezione Front-end predefinito è configurato in modo da accettare comunicazioni SMTP da tutti gli intervalli di indirizzi IP. Inoltre, è disponibile un connettore di ricezione che può agire come un proxy per traffico in uscita per i messaggi inviati al server Front-end dai server Cassette postali. Infine, è disponibile un connettore di ricezione sicuro configurato in modo da accettare messaggi crittografati con TLS (Transport Layer Security). Tali connettori sono:

  - **\<nome server\> front-end predefinito**   Accetta connessioni da mittenti SMTP sulla porta 25. Si tratta del comune punto di ingresso della messaggistica nell'organizzazione.

  - **\<nome server\> front-end proxy per traffico in uscita**   Accetta i messaggi da un connettore di invio su un server back-end, con proxy front-end abilitato.

  - **\<Nome server\> front-end client**   Accetta connessioni protette, con la crittografia TLS (Transport Layer Security) applicata.

In un'installazione tipica, non sono necessari ulteriori connettori di ricezione.

## Tipi di connettore di ricezione

Il tipo determina le impostazioni di sicurezza per ciascun connettore di ricezione.

Le impostazioni di protezione per un connettore di ricezione specificano le autorizzazioni concesse alle sessioni che si connettono al connettore di ricezione e i meccanismi di autenticazione supportati.

Quando si utilizza Interfaccia di amministrazione di Exchange per configurare un connettore di ricezione, la nuova pagina del connettore di ricezione richiede di selezionare il tipo di connettore. A seconda della selezione, i parametri vengono impostati per una conformità con la configurazione scelta. Procedure specifiche contengono ulteriori informazioni sulle impostazioni del tipo di connettore di ricezione. Esempi di queste procedure sono disponibili in [Creare un connettore di ricezione per la ricezione di posta elettronica da Internet](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md) e [Creare un connettore di ricezione protetto per la ricezione di posta elettronica da un partner](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md).

## Gruppi di autorizzazioni per il connettore di ricezione

Un gruppo di autorizzazioni è un insieme predefinito di autorizzazioni concesso a identità di sicurezza conosciute e assegnato a un connettore di ricezione. Tra le identità di sicurezza sono compresi utenti, computer e gruppi di protezione. L'utilizzo di gruppi di autorizzazioni semplifica la configurazione delle autorizzazioni sui connettori di ricezione. Questa proprietà **PermissionGroups** consente di definire i gruppi o i ruoli ai quali è consentito inoltrare messaggi al connettore di ricezione nonché le autorizzazioni assegnate a tali gruppi.

I gruppi di autorizzazioni includono *Anonymous*, *ExchangeUsers*, *ExchangeServers*, *ExchangeLegacyServers* e *Partner*.

## Specifiche del tipo di connettore di ricezione

Il tipo determina i gruppi di autorizzazioni predefiniti assegnati al connettore di ricezione e i meccanismi di autenticazione predefiniti disponibili per l'autenticazione della sessione. Nell'elenco seguente, sono riportati i tipi disponibili:

1.  **Client**   Generalmente utilizzato per effettuare il collegamento ai client senza utilizzare Microsoft Office Outlook. È possibile utilizzare l'autenticazione TLS.

2.  **Personalizzato**   Utilizzato, in genere, in uno scenario tra foreste o in uno scenario in cui l'organizzazione riceve messaggi da un agente di trasferimento messaggi SMTP.

3.  **Interno**   Utilizzato per la comunicazione tra i server che utilizzano il servizio Trasporto o tra i server Cassette postali che utilizzano il servizio Trasporto e agenti di trasferimento di terze parti.

4.  **Internet**   Utilizzato per ricevere la posta SMTP da Internet.

5.  **Partner**   Utilizzare questo tipo quando si desidera configurare una comunicazione sicura con un partner.

Ciascun tipo è indicato per un determinato scenario di connessione. Selezionare il tipo che dispone delle impostazioni predefinite più adatte alla configurazione desiderata. È possibile modificare le autorizzazioni utilizzando i cmdlet **Add-ADPermission** e **Remove-ADPermission**. Per ulteriori informazioni, vedere i seguenti argomenti:

  - [Add-ADPermission](https://technet.microsoft.com/it-it/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/it-it/library/aa996048\(v=exchg.150\))

## Autorizzazioni del connettore di ricezione

Le autorizzazioni del connettore di ricezione vengono assegnate a identità di sicurezza quando si specificano i gruppi di autorizzazioni per il connettore. Quando un'identità di sicurezza stabilisce una sessione con un connettore di ricezione, le autorizzazioni del connettore di ricezione determinano se accettare la sessione e come elaborare i messaggi ricevuti. È possibile impostare le autorizzazioni del connettore di ricezione utilizzando l'interfaccia di amministrazione di Exchange o il parametro *PermissionGroups* con il cmdlet **Set-ReceiveConnector** in Shell. Per modificare le autorizzazioni predefinite per un connettore di ricezione, è possibile utilizzare anche il cmdlet **Add-ADPermission**.

[Autorizzazioni del connettore di ricezione](receive-connector-permissions-exchange-2013-help.md) contiene una tabella in cui sono riportati le entità di sicurezza e i tipi di autorizzazione nel dettaglio.

## Impostazioni di autenticazione del connettore di ricezione

In EMC le impostazioni di autenticazione per un connettore di ricezione vengono utilizzate per specificare i meccanismi di autenticazione supportati dal server di trasporto Exchange 2013. In Shell, utilizzare il parametro *AuthMechanisms* per specificare i meccanismi di autenticazione supportati. Per un connettore di ricezione è possibile specificare più meccanismi di autenticazione. Per altre informazioni, vedere [Meccanismi di autenticazione connettore di ricezione](receive-connector-authentication-mechanisms-exchange-2013-help.md).

## Nuove funzionalità del connettore di ricezione in Exchange 2013

In Exchange 2013 sono state aggiunte le seguenti funzionalità:

  - Il parametro *TlsCertificateName* consente di specificare l'autorità di certificazione (CA) locale che ha emesso il certificato da utilizzare per la protezione messaggi. Aiuta a ridurre al minimo il rischio di certificati fraudolenti.

  - Il parametro *TransportRole* consente di specificare il ruolo del server associato a questo connettore. Viene utilizzato principalmente per specificare il ruolo del server quando si ospitano più ruoli server su un unico computer.

Vedere [New-ReceiveConnector](https://technet.microsoft.com/it-it/library/bb125139\(v=exchg.150\)) per ulteriori informazioni su questi parametri e altri parametri relativi ai connettori di ricezione.

