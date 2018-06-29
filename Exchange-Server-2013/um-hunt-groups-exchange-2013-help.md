---
title: 'Gruppi di risposta di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Gruppi di risposta di messaggistica unificata
ms:assetid: 026129a1-b0b5-410a-bed6-2d49f85205b3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa995918(v=EXCHG.150)
ms:contentKeyID: 50555530
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gruppi di risposta di messaggistica unificata

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-18_

Un gruppo di risposta telefonico consente di distribuire le chiamate telefoniche da un singolo numero a più numeri di interno o di telefono. Nella messaggistica unificata, un gruppo di risposta di messaggistica unificata è una rappresentazione logica di un gruppo di risposta telefonico e collega un gateway IP di messaggistica unificata a un dial plan di messaggistica unificata.

Per informazioni sulle attività di gestione relative ai gruppi di risposta di messaggistica unificata? vedere [Procedure gruppo di risposta di messaggistica unificata](um-hunt-group-procedures-exchange-2013-help.md).

**Sommario**

What is a hunt group

What is a pilot number

What is a UM hunt group

## Definizione di gruppo di risposta

*Gruppo di risposta* è un termine utilizzato per descrivere un gruppo di numeri di interno PBX o IP PBX condivisi dagli utenti. I gruppi di risposta vengono utilizzati per distribuire efficacemente le chiamate in entrata o in uscita nell'ambito di una specifica unità aziendale. Creando e definendo un gruppo di risposta si riducono al minimo le possibilità che l'utente di una chiamata in arrivo riceva il segnale di occupato quando la chiamata viene ricevuta.

I gruppi di risposta vengono utilizzati per individuare una linea, un numero di interno o un canale libero quando si riceve una chiamata. Le chiamate vengono "trasferite" alla prima linea disponibile quando la linea telefonica principale è occupata o non vi è stata risposta. La parte chiamante riceverà il segnale di occupato o ascolterà un messaggio vocale solo se nessun numero di interno del gruppo è libero. Ad esempio, un sistema PBX o IP PBX può essere configurato per contenere 10 numeri di interni per il reparto vendite. I 10°numeri di interno delle vendite vengono configurati come unico gruppo di risposta.

Le impostazioni di un gruppo di risposta semplice includono nome, numero di interno, elenco dei membri del gruppo disponibili e il metodo di selezione del gruppo di risposta. Il metodo di selezione del gruppo di risposta determina l'ordine di presentazione delle chiamate in arrivo ai membri del gruppo di risposta.

I sistemi PBX o IP PBX possono utilizzare diversi algoritmi o metodi per individuare una linea, un numero di interno o un canale libero. ad esempio:

  - **Gruppo di risposta o emissione di un segnale per tutti i numeri di interno**    Quando il numero di interno di un gruppo di risposta riceve una chiamata in arrivo, i sistemi PBX o IP PBX emettono un segnale per tutti i numeri di interno del gruppo.

  - **Inizio dal numero più basso o ricerca lineare**   Impostazione predefinita nella maggior parte dei sistemi PBX e IP PBX. In base a questo metodo, le chiamate vengono instradate alla prima linea libera in ordine sequenziale, iniziando dalla prima linea del gruppo. Questa configurazione è utilizzata per lo più nei telefoni multilinea delle piccole imprese.

  - **Round robin o ricerca circolare**   In base a questo metodo, le chiamate vengono instradate alla prima linea libera, iniziando dalla linea successiva a quella che ha gestito per ultima una chiamata. Quando le chiamate vengono distribuite utilizzando il metodo "round robin", se una chiamata viene recapitata alla linea 1, la chiamata successiva verrà indirizzata alla linea 2, la successiva ancora alla linea 3 e così via. Questo processo continua anche se una delle precedenti linee è ormai libera. Una volta esaurito il gruppo di risposta, la ricerca ricomincerà dalla prima linea. Le linee vengono ignorate solo se ancora occupate con una chiamata precedente. La ricerca circolare o round robin distribuiscono uniformemente i disservizi legati alle chiamate, riducendo al minimo le possibilità di gravi interruzioni del servizio.

  - **Ricerca in base alla linea libera più a lungo o in base alla distribuzione uniforme**    Con questo metodo, la chiamata viene instradata alla prima linea disponibile del gruppo che è risultata libera più a lungo. In questo metodo viene presa in considerazione la durata della chiamata su una linea, che risulta pertanto occupata, anziché l'eventuale disponibilità della linea. Questo metodo viene in genere utilizzato nei grandi call center in cui è il personale a rispondere alle chiamate in arrivo e il carico viene distribuito uniformemente nel gruppo dei numeri di interno.

È possibile configurare uno o più gruppi di risposta. Ogni gruppo di risposta deve includere almeno due linee. Se un numero è già in uso in un gruppo di risposta, non sarà disponibile in un altro gruppo.

Di seguito sono riportati esempi di gruppi di risposta alle chiamate telefoniche semplici e delle modalità operative.

**Esempio 1**

Il numero di interno 300 (numero pilota) è programmato in modo che a una chiamata in arrivo squillino i numeri di interno 301, quindi 302, 303 e infine 304.

1.  Il numero di interno 301 è occupato.

2.  Il numero di interno 302 squilla e non risponde.

3.  Il numero di interno 303 risponde alla chiamata.

4.  Il numero di interno 304 è libero e disponibile per una chiamata in arrivo.

**Esempio 2**

Il numero di interno 1000 (numero pilota) è programmato in modo che a una chiamata in arrivo squillino tutti i numeri di interno dal 2000 al 2003 contemporaneamente:

1.  Il numero di interno 2000 è libero.

2.  Il numero di interno 2001 è libero.

3.  Il numero di interno 2002 è libero.

4.  Il numero di interno 2003 risponde alla chiamata in arrivo.

Inizio pagina

## Definizione di numero pilota

In una rete telefonica, un sistema PBX o IP PBX può essere configurato per un singolo gruppo di risposta o per più gruppi di risposta. Ogni gruppo di risposta creato in un sistema PBX o IP PBX deve essere associato a un *numero pilota*. Utilizzando il numero pilota è possibile eliminare i segnali di occupato e instradare le chiamate in arrivo ai numeri di interno disponibili. Il sistema PBX o IP-PBX utilizza il numero pilota per individuare il gruppo di risposta e quindi il numero di interno telefonico che ha ricevuto la chiamata in arrivo e i numeri di interno assegnati al gruppo di risposta. Se non viene definito un numero pilota, il sistema PBX o IP PBX non può individuare il numero dal quale è stata ricevuta la chiamata in arrivo.

Un numero pilota è l'indirizzo, l'interno o la posizione del gruppo di risposta all'interno del sistema PBX o IP PBX. In genere, si tratta di un numero di interno vuoto o di un unico numero di interno di un gruppo di risposta costituito da numeri di interno a cui non è associata una persona o un telefono. Ad esempio, si può configurare un gruppo di risposta in un sistema PBX o IP-PBX in modo che contenga i numeri di interni 4100, 4101, 4102, 4103, 4104 e 4105. Il numero pilota del gruppo di risposta è configurato come interno 4100. Quando si riceve una chiamata nel numero di interno 4100, il sistema PBX o IP PBX cerca il successivo numero di interno disponibile per individuare il numero al quale indirizzare la chiamata. In questo esempio, il sistema PBX o IP PBX utilizzerà l'algoritmo di ricerca programmato per cercare i numeri di interno 4101, 4102, 4103, 4104 e 4105.

Grazie al numero pilota è possibile eliminare i segnali di occupato e instradare le chiamate in arrivo ai numeri di interno disponibili. Nella messaggistica unificata, il numero pilota PBX o IP PBX viene utilizzato come obiettivo. Se nessun numero di interno del gruppo di risposta risponde a una chiamata in arrivo, la chiamata viene instradata al server Cassette postali che esegue il servizio Messaggistica unificata di Microsoft Exchange.

Inizio pagina

## Definizione di gruppo di risposta di messaggistica unificata

I gruppi di risposta di messaggistica unificata sono fondamentali per il funzionamento del sistema di messaggistica unificata. Il gruppo di risposta di messaggistica unificata è una rappresentazione logica di un gruppo di risposta PBX o IP PBX esistente. Viene utilizzato per collegare un gateway IP di messaggistica unificata a un dial plan dello stesso tipo. Un singolo gruppo di riposta di messaggistica unificata può anche collegare più gateway IP di messaggistica unificata a un dial plan dello stesso tipo. Per impostazione predefinita, quando si crea un gateway IP di messaggistica unificata e lo si associa a un dial plan dello stesso tipo, viene creato un gruppo di risposta di messaggistica unificata, con la possibilità di creare altri gruppi di risposta. È necessario creare almeno un gruppo di risposta di messaggistica unificata.

I gruppi di risposta di messaggistica unificata vengono utilizzati per individuare il gruppo di risposta del sistema PBX o IP PBX dal quale è stata ricevuta la chiamata. Il numero pilota definito per un gruppo di risposta nel sistema PBX o IP PBX deve essere definito anche per il gruppo di risposta di messaggistica unificata. Il numero pilota viene utilizzato per associare le informazioni presentate per le chiamate in arrivo utilizzando le informazioni sulla segnalazione del SIP (Session Initiation Protocol) riportate nel messaggio vocale. Il numero pilota consente al server Exchange di interpretare la chiamata e il relativo dial plan in modo da instradare correttamente la chiamata. L'assenza di un gruppo di risposta impedisce ai server Exchange di individuare l'origine o la posizione della chiamata in arrivo. Individuando la posizione delle chiamate in arrivo, i server Exchange possono accettare le informazioni sull'intestazione della chiamata passate dal gateway VoIP, dai sistemi IP PBX o PBX abilitato per SIP. È estremamente importante configurare correttamente i gruppi di risposta di messaggistica unificata, perché le chiamate in arrivo che non corrispondono al numero pilota definito per il gruppo di risposta di messaggistica unificata non avranno risposta e il routing non sarà eseguito correttamente.

Nel caso di distribuzioni locali o ibride, quando si crea un gruppo di risposta di messaggistica unificata, tutti i server Accesso client e di cassette postali vengono abilitati per la comunicazione con un gateway VoIP, un sistema IP PBX o PBX abilitato per SIP, indipendentemente dal fatto che siano stati aggiunti o meno a un dial plan di messaggistica unificata. Questa situazione si verifica poiché tutti i server Accesso client e Cassette postali rispondono alle chiamate in arrivo per tutti i dial plan, anziché per uno specifico dial plan di messaggistica unificata, come accadeva con il server Messaggistica unificata nelle versioni precedenti di Exchange. Se il gruppo di risposta di messaggistica unificata viene eliminato, il gateway IP di messaggistica unificata associato non sarà in grado di rispondere alle chiamate in arrivo da un gateway VoIP, un sistema IP PBX o PBX abilitato per SIP, né di consentire chiamate in uscita tramite il gateway VoIP, i sistemi IP PBX o PBX abilitati per SIP utilizzando il numero pilota specificato.

Tuttavia, nel caso di distribuzioni locali o ibride, se la messaggistica unificata viene integrata con Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server, è necessario aggiungere tutti i server Accesso client e Cassette postali a tutti i dial plan URI SIP creati per essere utilizzati con Communications Server 2007 R2 o Lync Server. Questo consente il corretto funzionamento del routing delle chiamate e la possibilità di effettuare chiamate esterne senza problemi.

Per ulteriori informazioni sui gateway IP di messaggistica unificata, vedere [Gateway IP di messaggistica unificata](um-ip-gateways-exchange-2013-help.md).

