---
title: 'Dati di replica EdgeSync: Exchange 2013 Help'
TOCTitle: Dati di replica EdgeSync
ms:assetid: c7dd137d-7ed4-4f16-9895-f354c449cf9b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232177(v=EXCHG.150)
ms:contentKeyID: 61183414
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dati di replica EdgeSync

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

Quando si distribuisce un server Trasporto Edge, non è necessario accedere ad Active Directory. Per l'esecuzione di ricerche dei destinatari e di attività di aggregazione dell'elenco indirizzi attendibili e per l'implementazione della sicurezza del dominio utilizzando l'autenticazione Mutual TLS (Transport Layer Security), il server Trasporto Edge richiede i dati che risiedono in Active Directory. Questi dati vengono replicati sul server Trasporto Edge utilizzando EdgeSync e il server Trasporto Edge memorizza tutte le informazioni replicate in Active Directory Lightweight Directory Services (AD LDS).

Questo argomento è incentrato su dati replicati da Active Directory a AD LDS sul server Trasporto Edge sottoscritto su un sito di Active Directory. Per ulteriori informazioni su EdgeSync e sulle sottoscrizioni di Edge, vedere [Sottoscrizioni Edge](edge-subscriptions-exchange-2013-help.md).

Quattro tipi di dati vengono replicati su AD LDS e utilizzati dal server Trasporto Edge:

Edge Subscription information

Configuration information

Recipient information

Topology information

## Informazioni sulla sottoscrizione di Edge

Exchange 2013 estende gli schemi di Active Directory e di AD LDS per fornire gli attributi per l'oggetto **ms-Exch-ExchangeServer** per rappresentare i dati necessari per il controllo del processo di sincronizzazione EdgeSync. Questi attributi forniscono 3 funzioni a EdgeSync:

  - Fornitura e gestione automatica delle credenziali utilizzate per garantire la sicurezza della connessione LDAP tra il server di cassetta postale e il server Trasporto Edge sottoscritto.

  - Gestione del processo di blocco e sblocco della sincronizzazione che garantisce che un solo server per volta tenterà di sincronizzarsi con un singolo server Trasporto Edge. Per ulteriori informazioni sul processo di blocco e sblocco, vedere [Sottoscrizioni Edge](edge-subscriptions-exchange-2013-help.md).

  - Ottimizzazione della sincronizzazione di EdgeSync al fine di gestire un record sullo stato corrente della sincronizzazione. La visualizzazione dello stato di sincronizzazione consente di evitare procedure eccessive di sincronizzazione manuale.

Nella seguente tabella vengono elencate le estensioni dello schema specifiche delle sottoscrizioni di Edge. I valori assegnati a questi attributi vengono gestiti dalla sottoscrizione a Edge ed EdgeSync. Non possono essere modificati manualmente.

### Estensioni dello schema di sottoscrizione di Edge

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome attributo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ms-Exch-Server-EKPK-Public-Key</strong></p></td>
<td><p>La chiave pubblica corrente per il certificato utilizzato dal server. Questo valore viene memorizzato sia dai server Trasporto Edge che dai server di cassette postali. La chiave pubblica viene utilizzata per crittografare le credenziali utilizzate per autenticare il server durante la comunicazione LDAP e SMTP.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-EdgeSync-Credential</strong></p></td>
<td><p>L'elenco di credenziale utilizzate da EdgeSync per stabilire una sessione LDAP autenticata con AD LDS. Sui server di cassette postali, tale attributo contiene soltanto le credenziali che il server di cassette postali utilizza per autenticare i server Trasporto Edge sottoscritti. Sui server Trasporto Edge, questo attributo contiene le credenziali di ciascun server di cassette postali nel sito di Active Directory sottoscritto che partecipa alla sincronizzazione EdgeSync. Questo attributo è presente soltanto sui server di cassette postali che eseguono la sincronizzazione EdgeSync e sui server Trasporto Edge sottoscritti.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ms-Exch-Edge-Sync-Lease</strong></p></td>
<td><p>Utilizzato per gestire i rapporti tra i server di cassette postali quando più di un server di cassetta postale tenta di eseguire la replica sul medesimo server Trasporto Edge.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-Edge-Sync-Status</strong></p></td>
<td><p>Presente solo in AD LDS sull'oggetto server Trasporto Edge. Consente di registrare lo stato della replica in un'istanza di AD LDS e di includere le relative informazioni.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Informazioni sulla configurazione

Quando si sottoscrive un server Trasporto Edge all'organizzazione, è possibile gestire gli oggetti di configurazione comuni al server Trasporto Edge e all'organizzazione di Exchange direttamente dall'organizzazione. Queste modifiche vengono quindi replicate sul server Trasporto Edge utilizzando EdgeSync. Questo processo consente di garantire la coerenza della configurazione in tutti i server coinvolti nell'elaborazione del messaggio.

Nel server Trasporto Edge deve essere gestito anche un sottoinsieme di dati di configurazione per l'organizzazione di Exchange. Durante la sincronizzazione EdgeSync, i dati di configurazione necessari per il server Trasporto Edge vengono scritti nella partizione di configurazione di AD LDS. I dati di configurazione scritti in AD LDS comprendono:

  - **Server di cassette postali**   Il nome di dominio completo (FQDN) di ciascun server di cassette postali nel sito sottoscritto di Active Directory viene reso disponibile nell'archivio AD LDS locale sul server Trasporto Edge. Queste informazioni vengono utilizzate per creare un elenco di server Smart host per il connettore di invio in entrata.

  - **Domini accettati**   Tutti i domini autorevoli, di inoltro interno e di inoltro esterno, configurati per l'organizzazione di Exchange, vengono scritti in AD LDS. Quando i domini accettati sono disponibili sul server Trasporto Edge, l'organizzazione di Exchange può eseguire il filtro dei domini e rifiutare il traffico SMTP non valido verso l'organizzazione appena possibile. Per ulteriori informazioni sui domini accettati, vedere [Domini accettati](accepted-domains-exchange-2013-help.md).

  - **Classificazioni dei messaggi**   Se le classificazioni dei messaggi sono disponibili sul server Trasporto Edge, gli agenti di trasporto e la conversione del contenuto possono agire sulle classificazioni del messaggio nella rete perimetrale. Ad esempio, l'agente di filtro degli allegati può applicare la classificazione relativa all'allegato rimosso quando effettua l'operazione, inviando un testo informativo a un utente di Microsoft Outlook o a un utente di Outlook Web App per comunicare al destinatario cosa si è verificato. Gli agenti sviluppati per l'utilizzo in applicazioni di terze parti possono utilizzare le classificazioni dei messaggi in modo simile.

  - **Domini remoti**   Tutte le voci di dominio remoto configurate per l'organizzazione di Exchange vengono scritte in AD LDS. Le voci di dominio remoto consentono di controllare le impostazioni dei messaggi fuori sede e le impostazioni del formato dei messaggi per un dominio remoto. Per ulteriori informazioni sui domini remoti, vedere [Domini remoti](remote-domains-exchange-2013-help.md).

  - **Connettori di invio**   Per impostazione predefinita, la creazione di una sottoscrizione Edge crea automaticamente i connettori di invio necessari per l'abilitazione del flusso di posta end-to-end tra l'organizzazione di Exchange e Internet nel momento di sottoscrizione del server Trasporto Edge. Tutti i connettori di invio esistenti sul server Trasporto Edge vengono eliminati. Se si desidera configurare connettori di invio aggiuntivi, è possibile configurarli nell'organizzazione di Exchange e selezionare la sottoscrizione di Edge come server di origine per il connettore. Per ulteriori informazioni, vedere [Sottoscrizioni Edge](edge-subscriptions-exchange-2013-help.md).

  - **Server SMTP interni**   Il valore dell'attributo *InternalSMTPServers* viene memorizzato nell'oggetto **TransportConfig** sia per l'organizzazione di Exchange sia per il server Trasporto Edge locale. Durante la sincronizzazione EdgeSync, il valore memorizzato nell'oggetto server Trasporto Edge locale viene sovrascritto dal valore memorizzato in questo oggetto per l'organizzazione di Exchange. Questo attributo consente di specificare un elenco di indirizzi IP del server SMTP interno o intervalli di indirizzi IP che devono essere ignorati dall'ID mittente e dal filtro connessioni.

  - **Elenco di domini protetti**   Gli attributi *TLSReceiveDomainSecureList* e *TLSSendDomainSecureList* vengono memorizzati nell'oggetto **TransportConfig** sia per l'organizzazione di Exchange sia per il server Trasporto Edge locale. Durante la sincronizzazione EdgeSync, il valore memorizzato nell'oggetto server Trasporto Edge locale viene sovrascritto dal valore memorizzato in questo oggetto per l'organizzazione di Exchange. Questi attributi consentono di specificare l'elenco dei domini remoti configurati per l'autenticazione TLS reciproca.

Inizio pagina

## Informazioni sui destinatari

Informazioni sui destinatari che vengono replicate in AD LDS includono soltanto un sottoinsieme di attributi dei destinatari. Vengono replicati soltanto i dati necessari al server Trasporto Edge per eseguire determinate attività di protezione dalla posta indesiderata. Le informazioni sui destinatari replicate in AD LDS includono:

  - **Destinatari   **L'elenco dei destinatari nell'organizzazione di Exchange viene replicato in AD LDS. Ogni destinatario viene identificato da un GUID Active Directory assegnato. Se si configura l'account di un destinatario per rifiutare la posta proveniente dall'esterno dell'organizzazione, il destinatario non viene replicato in AD LDS. Se si disattiva o elimina la cassetta postale di un destinatario, quella cassetta postale non viene più replicata in AD LDS.

  - **Indirizzi proxy**   Tutti gli indirizzi proxy assegnati a ogni destinatario vengono replicati in AD LDS come dati con hash. Si tratta di un hash unidirezionale che utilizza Secure Hash Algorithm (SHA)-256. SHA-256 genera un digest del messaggio a 256 bit dei dati originali. L'archiviazione degli indirizzi proxy come dati con hash garantisce una migliore sicurezza delle informazioni nel caso in cui il server Trasporto Edge o AD LDS risultino compromessi. Gli indirizzi proxy vengono utilizzati quando il server Trasporto Edge esegue le attività di protezione da posta indesiderata o di ricerca del destinatario.

  - **Elenco Mittenti attendibili, elenco Mittenti bloccati ed elenco Destinatari attendibili**   Gli elenchi Mittenti attendibili, Mittenti bloccati e Destinatari attendibili, definiti nell'istanza di Outlook di ciascun destinatario, vengono aggregati e replicati in AD LDS. Queste impostazioni vengono memorizzate nel database delle cassette postali in cui risiede la cassetta postale del destinatario. Una raccolta di elenchi di indirizzi attendibili dell'utente di Outlook è costituita dai dati combinati provenienti dall'elenco Mittenti attendibili, dall'elenco Destinatari attendibili, dall'elenco Mittenti bloccati e da contatti esterni. Se i dati sulla raccolta degli elenchi indirizzi attendibili sono disponibili in AD LDS, il server Trasporto Edge è in grado di visualizzare correttamente i mittenti, riducendo il sovraccarico operativo del filtro della posta. Queste informazioni vengono inviate come dati hash.
    

    > [!IMPORTANT]
    > Anche se i dati dei destinatari attendibili vengono archiviati in Outlook e possono essere aggregati nella raccolta degli elenchi indirizzi attendibili sull'istanza di AD&nbsp;LDS nel server Trasporto Edge, la funzionalità del filtro contenuto non agisce sui dati dei destinatari attendibili.



  - **Impostazioni per la posta indesiderata per destinatario**   È possibile utilizzare il cmdlet **Set-Mailbox** per assegnare le impostazioni di soglia per la posta indesiderata per ciascun destinatario in modo che siano diverse dalle impostazioni per la posta indesiderata dell'organizzazione. Le impostazioni per la posta indesiderata per ciascun destinatario configurate sovrascrivono le impostazioni per l'intera organizzazione. Con la replica di queste impostazioni in AD LDS, le impostazioni per destinatario possono essere analizzate prima che il messaggio venga inoltrato all'organizzazione di Exchange. Queste informazioni vengono inviate come dati con hash.

Inizio pagina

## Informazioni sulla topologia

Le informazioni sulla topologia includono la notifica dei nuovi server Trasporto Edge sottoscritti o le sottoscrizioni di Edge rimosse. Questi dati vengono aggiornati ogni cinque minuti.

Inizio pagina

