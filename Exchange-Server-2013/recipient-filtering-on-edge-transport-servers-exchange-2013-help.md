---
title: 'Filtro destinatari nei server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Filtro destinatari nei server Trasporto Edge
ms:assetid: 994eefd9-3903-41e6-a882-1e333d6d2d18
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123891(v=EXCHG.150)
ms:contentKeyID: 50481268
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtro destinatari nei server Trasporto Edge

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-05-07_

Il filtro destinatari è una funzionalità di protezione dalla posta indesiderata di Microsoft Exchange Server 2013 che fa affidamento sull'intestazione RCPT TO SMTP per determinare l'eventuale azione da eseguire su un messaggio in arrivo. Il filtro destinatari viene eseguito dall'agente Filtro destinatario.

L'agente Filtro destinatario consente di bloccare i messaggi in base alle caratteristiche del destinatario specificato nell'organizzazione. Inoltre, consente di impedire l'accettazione dei messaggi nei seguenti scenari:

  - **Destinatari inesistenti**   È possibile impedire che vengano recapitati messaggi a destinatari non inclusi nella rubrica dell'organizzazione. Ad esempio, è possibile interrompere il recapito a nomi account utilizzati spesso in modo errato, quali administrator@contoso.com o support@contoso.com.

  - **Liste di distribuzione limitate**   È possibile impedire il recapito di posta Internet a liste di distribuzione che devono essere utilizzate solo da utenti interni.

  - **Cassette postali che non devono mai ricevere messaggi da Internet**   È possibile impedire il recapito di posta Internet a una specifica cassetta postale o alias utilizzato all'interno dell'organizzazione, ad esempio Helpdesk.

L'agente Filtro destinatario agisce sui destinatari archiviati in una delle seguenti origini dati o in entrambe:

  - **Elenco destinatari bloccati**   Un elenco definito dall'amministratore di destinatari che non devono mai ricevere messaggi da Internet.

  - **Ricerca destinatari**   Interroga Active Directory per verificare che il destinatario esista nell'organizzazione. Su un server Trasporto Edge, Ricerca destinatari richiede l'accesso alle informazioni di Active Directory fornite da EdgeSync all'istanza locale di Active Directory Lightweight Directory Services (AD LDS).

Quando si abilita l'agente Filtro destinatario, viene eseguita una delle azioni riportate di seguito sui messaggi in arrivo in base alle caratteristiche dei destinatari. Tali destinatari sono indicati dall'intestazione RCPT TO.

  - Se il messaggio in arrivo contiene un destinatario presente nell'elenco destinatari bloccati, il server di Exchange invia un errore di sessione SMTP `550 5.1.1 User unknown` al server di invio.

  - Se il messaggio in arrivo contiene un destinatario che non corrisponde ad alcun destinatario in Ricerca destinatari, il server di Exchange invia un errore di sessione SMTP `550 5.1.1 User unknown` al server di invio.

  - Se il destinatario non è presente nell'elenco destinatari bloccati ma è incluso in Ricerca destinatari, il server di Exchange invia una risposta SMTP `250 2.1.5 Recipient OK` al server di invio e il messaggio viene elaborato dal successivo agente di protezione dalla posta indesiderata della catena.

**Sommario**

Configuring recipient lookup

Tarpitting functionality

Multiple namespaces

## Configurazione della ricerca dei destinatari

Uno dei modi più efficaci per ridurre la quantità di posta indesiderata consiste nel convalidare i destinatari prima di accettare i messaggi in arrivo da Internet. È possibile abilitare il blocco dei messaggi inviati ai destinatari che non esistono nell'organizzazione di Exchange e il blocco di destinatari specifici utilizzando il cmdlet **Set-RecipientFilterConfig** in Exchange Management Shell. Per ulteriori informazioni, vedere [Gestire il filtro destinatari nei server Trasporto Edge](manage-recipient-filtering-on-edge-transport-servers-exchange-2013-help.md).

Se si dispone di un server Trasporto Edge installato nella rete perimetrale, è buona norma configurare l'istanza di AD LDS in esecuzione sul server Trasporto Edge per la sincronizzazione con Active Directory. Per impostazione predefinita, AD LDS è installato e configurato nel server Trasporto Edge. Tuttavia, è necessario configurare AD LDS per comunicare con un server di catalogo globale unito a un dominio di Active Directory sottoscrivendo il server Trasporto Edge all'organizzazione. Per ulteriori informazioni, vedere [Utilizzare un Exchange 2010 o 2007 server Trasporto Edge di Exchange 2013](use-an-exchange-2010-or-2007-edge-transport-server-in-exchange-2013-exchange-2013-help.md).

Inizio pagina

## Funzionalità di tarpitting

La funzionalità di ricerca dei destinatari consente al server di invio di determinare se un indirizzo di posta elettronica è valido. Come specificato in precedenza, quando il destinatario di un messaggio in arrivo è un destinatario noto, il server di Exchange invia una risposta SMTP `250 2.1.5 Recipient OK` al server di invio. Questa funzionalità rappresenta un ambiente ideale per attacchi directory harvest.

Un *attacco directory harvest* è un tentativo di raccogliere indirizzi di posta elettronica validi da una determinata organizzazione in modo da poterli aggiungere a un database di posta indesiderata. Poiché l'invio di posta indesiderata è finalizzato a convincere gli utenti ad aprire tali messaggi di posta elettronica, gli utenti malintenzionati o gli *spammer* sono disposti a pagare per ottenere elenchi indirizzi attivi. Dal momento che il protocollo SMTP fornisce informazioni su mittenti noti e mittenti sconosciuti, uno spammer può scrivere un programma automatico che utilizza i nomi comuni o i termini del dizionario per creare indirizzi di posta elettronica per un dominio specifico. Il programma raccoglie tutti gli indirizzi di posta elettronica che restituiscono una risposta SMTP `250 2.1.5 Recipient OK` e ignora tutti gli indirizzi di posta elettronica che restituiscono un errore di sessione SMTP `550 5.1.1 User unknown`. Lo spammer può quindi vendere gli indirizzi di posta elettronica validi o utilizzarli come destinatari di messaggi indesiderati.

Per contrastare gli attacchi directory harvest, Exchange 2013 fornisce la funzionalità di tarpitting. Il *tarpitting* consiste nel ritardare artificialmente le risposte del server per specifici modelli di comunicazione SMTP che indicano grandi volumi di posta indesiderata o di altri messaggi non graditi. L'obiettivo della funzionalità di tarpitting consiste nel rallentare il processo di comunicazione per questo tipo di traffico di posta elettronica in modo da aumentare il costo sostenuto dall'utente o dall'organizzazione che invia la posta indesiderata. Questa funzionalità rende gli attacchi directory harvest troppo costosi per consentire di automatizzati in maniera efficace.

Se il tarpitting non è configurato, il server di Exchange restituisce immediatamente al mittente un errore di sessione SMTP `550 5.1.1 User unknown` quando un destinatario non è incluso nella ricerca dei destinatari. In alternativa, se il tarpitting è configurato, SMTP attende un numero di secondi specificato prima di restituire l'errore `550 5.1.1 User unknown`. Questa pausa nella sessione SMTP rende l'automatizzazione di un attacco directory harvest più difficile e meno conveniente dal punto di vista economico per lo spammer. Per impostazione predefinita, il tarpitting è configurato su 5 secondi per i connettori di ricezione.

Per configurare il tempo che deve trascorrere prima che SMTP restituisca l'errore `550 5.1.1 User unknown`, occorre impostare l'intervallo di tarpitting utilizzando il parametro *TarpitInterval* nel cmdlet **Set-ReceiveConnector**. La sintassi è:

    Set-ReceiveConnector <Receive Connector> -TarpitInterval <00:00:00 to 00:10:00>

Il valore predefinito è `00:00:05` o 5 secondi. Il nome del connettore di ricezione predefinito su un server Trasporto Edge è `Default internal receive connector <server name>`.

Prestare attenzione se si decide di modificare l'intervallo di tarpitting. Un intervallo eccessivamente lungo potrebbe determinare l'interruzione del flusso di posta ordinario, mentre un intervallo eccessivamente breve potrebbe non essere abbastanza efficace per contrastare un attacco directory harvest. È possibile modificare l'intervallo di tarpitting, ma si consiglia di apportare incrementi di dimensioni ridotte e verificare i risultati. Per esempio, se 5 secondi non è efficace, provare a modificare l'intervallo in 10 secondi.

Inizio pagina

## Spazi dei nomi multipli

L'agente filtro destinatario esegue ricerche dei destinatari solo per i domini autorevoli. Se l'organizzazione accetta e inoltra messaggi per conto di un altro dominio configurato come dominio di inoltro interno o esterno, l'agente Filtro destinatario non esegue una ricerca sui destinatari in questi domini. Tuttavia, se il destinatario è specificato nell'elenco destinatari bloccati, il destinatario sarà tuttora bloccato dall'agente Filtro destinatario.

È inoltre possibile configurare i domini accettati in locale su un server Trasporto Edge. Se il dominio è configurato come dominio di inoltro interno o esterno, l'agente Filtro destinatario sul server Trasporto Edge non esegue una ricerca sui destinatari in questi domini.

Inizio pagina

