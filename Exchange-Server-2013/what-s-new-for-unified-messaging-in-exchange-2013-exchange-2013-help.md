---
title: 'Novità per la messaggistica unificata di Exchange 2013: Exchange 2013 Help'
TOCTitle: Novità per la messaggistica unificata di Exchange 2013
ms:assetid: a444ef2d-d893-408e-adf9-c9d8a8b07593
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150545(v=EXCHG.150)
ms:contentKeyID: 50481315
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Novità per la messaggistica unificata di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

In Microsoft Exchange Server 2013 sono state migliorate le precedenti versioni di Exchange con l'introduzione di nuove funzionalità e modifiche architettoniche. La messaggistica unificata (UM) in Microsoft Exchange 2013 include lo stesso insieme di funzionalità di Exchange 2010 e Exchange 2007, anche se ora la messaggistica unificata non è più un ruolo del server separato. Ora è un componente delle funzionalità vocali offerte in Exchange 2013.

## Cambiamenti nell'architettura vocale

L'architettura di Exchange 2013 è diversa da quella di Exchange 2010 ed Exchange 2007. Nelle versioni precedenti della messaggistica unificata di Exchange, tutti i componenti per la messaggistica unificata erano inclusi su un server sul quale era installato il ruolo del server Messaggistica unificata. In Exchange 2013, tutti i componenti della messaggistica unificata sono suddivisi tra un server Accesso client con il servizio Router chiamate di messaggistica unificata di Microsoft Exchange e un server Cassette postali con il servizio Messaggistica unificata di Microsoft Exchange. Tutte le funzionalità, compresi i servizi e i processi di lavoro per la messaggistica unificata, si trovano su ciascun server Cassette postali, fatta eccezione per il server Accesso client che esegue il servizio Router chiamate di messaggistica unificata di Microsoft Exchange, che esegue il proxy delle chiamate in arrivo al server Cassette postali. Per ulteriori informazioni, vedere [Modifiche all'architettura VoIP](voice-architecture-changes-exchange-2013-help.md).

## Supporto per IPv6

Internet Protocol versione 6 (IPv6) è la versione più recente del protocollo IP. IPv6 ha lo scopo di colmare molte lacune di IPv4, cioè la precedente versione del protocollo. Proprio come in Exchange 2010, i server Accesso client e Cassette postali di Exchange 2013 supportano pienamente le reti IPv6. Per ulteriori informazioni, vedere [Supporto IPv6 in messaggistica unificata](ipv6-support-in-unified-messaging-exchange-2013-help.md).

## Supporto per l'API UCMA 4.0

A partire da Exchange 2010 Service Pack 1, il ruolo Messaggistica unificata fa affidamento su Unified Communications Managed API v2.0 (UCMA) per la segnalazione e i supporti. Pertanto, UCMA 2.0 è un prerequisito per la configurazione della messaggistica unificata di Exchange 2010. UCMA 2.0 viene scaricato separatamente e distribuito manualmente dagli amministratori sui server Messaggistica unificata che eseguono Exchange 2010 SP1 o versioni successive. Per Exchange 2013 è necessario UCMA 4.0. Tuttavia, visto che il server Messaggistica unificata non è più un ruolo del server separato in Exchange 2013, sono i server Accesso client e Cassette postali a richiedere UCMA 4.0.

UCMA 4.0 supporta nuove funzionalità nella messaggistica unificata, ad esempio l'utilizzo della stessa versione del modulo vocale sia per la sintesi vocale (TTS, Text-to-Speech) sia per il riconoscimento vocale automatico (ASR, Automatic Speech Recognition). La piattaforma utilizzata per Exchange 2013, .NET 4.0, include un singolo file di installazione e consente la compatibilità con le versioni precedenti dei server di messaggistica unificata (Exchange 2010 e Exchange 2007).

In Exchange 2010 SP2 e SP1, l'installazione di UCMA 2.0 deve essere eseguita prima di installare il Service Pack su un server Messaggistica unificata. Tuttavia, UCMA 2.0 presentava diverse limitazioni. UCMA 4.0 corregge molti di queste mancanze. In Exchange Server 2013, la messaggistica unificata continua a utilizzare UCMA. Tuttavia, il passaggio alla versione più recente di UCMA offre alcuni vantaggi:

  - La build più recente di UCMA integra gli hotfix e le patch.

  - UCMA richiede .NET 4.0, la piattaforma utilizzata da Exchange Server 2013. (UCMA 2.0 non supporta .NET 4.0.)

  - UCMA 4.0 supporta IPv6.

  - Distribuzione semplificata e automatizzata di UCMA 4.0. L'installazione di Exchange 2013 esegue un singolo controllo di UCMA 4.0.

  - L'installazione di UCMA 4.0 include tutti i prerequisiti per Exchange 2013.


> [!NOTE]
> UCMA 4.0 viene installato durante l'installazione di Exchange 2013. Per i dettagli su UCMA 4.0 e sui requisiti di installazione, vedere <A href="exchange-2013-prerequisites-exchange-2013-help.md">Prerequisiti di Exchange 2013</A>. Per eseguire l'aggiornamento alla versione più recente di UCMA, è necessario per prima cosa disinstallare le versioni precedenti di UCMA installate con Installazione applicazioni.



## Miglioramenti all'anteprima della casella vocale

Alcuni miglioramenti ai servizi di sintesi vocali sono offerti nella messaggistica unificata di Exchange Server 2013 grazie a Speech Engine 11.0 e UCMA 4.0. Sono inclusi miglioramenti della lingua e di generazione della grammatica. Inoltre, la messaggistica unificata di Exchange Server 2013 include diversi miglioramenti all'interfaccia utente, alla sicurezza e all'accuratezza di Anteprima segreteria telefonica. Per ulteriori informazioni, vedere [Miglioramenti alla segreteria telefonica preview](voice-mail-preview-enhancements-exchange-2013-help.md).

## Supporto dell'ID chiamante avanzato

Nelle versioni precedenti della messaggistica unificata di Exchange, un server Messaggistica unificata che riceveva una chiamata utilizzava l'ID chiamante per cercare l'identità del chiamante. Questa ricerca si estendeva ad Active Directory e ai contatti personali dell'utente di messaggistica unificata archiviati nella sua cassetta postale.

Gli utenti di Exchange sono spesso infastiditi dagli errori nell'identificazione dei contatti personali o di Exchange in base all'ID chiamante. Finora, per la ricerca era utilizzata solo la cartella dei contatti predefinita nella messaggistica unificata di Exchange. Tuttavia, è probabile che gli utenti di Exchange Server 2013 dispongano di contatti aggregati da social network esterni o di contatti aggiunti a cartelle univoche create manualmente. Exchange 2013 supporta l'aggregazione dei contatti da social network esterni, offre la possibilità di collegare più contatti che fanno riferimento alla stessa persona e utilizza i dati per presentare visualizzazioni incentrate sulla persona (anziché sul contatto). I contatti aggregati da reti esterne vengono inseriti nelle cartelle dei contatti insieme alle eventuali cartelle di contatti aggiuntive create dall'utente. Le funzionalità nella messaggistica unificata di Exchange 2013 estendono l'ambito della ricerca per includere le cartelle dei contatti personali e di Exchange create manualmente.

La ricerca dell'ID chiamante è integrata con l'aggregazione dei contatti, pertanto la ricerca viene eseguita anche sui contatti esterni. La proprietà PersonID, dove presente e impostata su un valore diverso da null, migliora l'esperienza dell'utente nella risoluzione dell'ID chiamante eliminando le corrispondenze duplicate con contatti associati alla stessa persona. Dal momento che la proprietà PersonID è la stessa per entrambi i risultati, la messaggistica unificata la considera come una corrispondenza a un unico contatto.

## Miglioramenti alla piattaforma di sintesi e riconoscimento vocale

La messaggistica unificata di Exchange Server 2013 introduce alcuni miglioramenti alla piattaforma di sintesi e riconoscimento vocale, ad esempio:

  - Miglioramenti e maggiore accuratezza dell'anteprima della casella vocale.

  - Supporto per la [piattaforma di riconoscimento vocale Microsoft – Runtime (versione 11.0)](https://go.microsoft.com/fwlink/p/?linkid=253196).

  - Generazione della grammatica vocale utilizzando la cassetta postale di sistema per un'organizzazione.

La messaggistica unificata di Exchange utilizza grammatiche di sintesi vocale statiche e dinamiche per riconoscere comandi, nomi di contatti nell'elenco indirizzi globale e nomi di contatti personali nella cassetta postale dell'utente. Oggi, in Exchange Server 2013, ogni server Cassette postali che esegue il servizio Messaggistica unificata di Microsoft Exchange genera più grammatiche per tutte le lingue di messaggistica unificata installate e le archivia nelle directory. Ciascun server Cassette postali archivia ogni possibile grammatica, generata in base al numero di dial plan, operatori automatici e lingue di messaggistica unificata installate.

I file di grammatica sono utilizzati come input per il processo di riconoscimento vocale e sono generati periodicamente. Il comando GGG.exe in Exchange 2007 ed Exchange 2010 rendeva possibile l'aggiornamento manuale dei file di grammatica senza attendere l'aggiornamento pianificato. In Exchange Server 2013, per gestire i problemi di scalabilità della generazione di grammatiche ASR per la messaggistica unificata, la generazione della grammatica GAL di sintesi vocale non avviene più sul server su cui è installato il ruolo del server Messaggistica unificata. L'operazione avviene invece periodicamente utilizzando Assistente cassette postali sul server Cassette postali in cui è in esecuzione il servizio Messaggistica unificata di Microsoft Exchange che ospita la cassetta postale di arbitraggio dell'organizzazione. Il file di grammatica per la sintesi vocale GAL viene archiviato nella cassetta postale di arbitraggio per un'organizzazione e successivamente scaricato in tutti i server Cassette postali nell'organizzazione di Exchange. Per impostazione predefinita, Assistente cassette postali viene eseguito ogni 24 ore. È possibile modificare la frequenza utilizzando il cmdlet **Set-MailboxServer**.

## Aggiornamenti dei cmdlet

In Exchange 2013, molti cmdlet di messaggistica unificata sono stati importati da Exchange 2010, ma sono state apportate modifiche ad alcuni di questi cmdlet e sono stati aggiunti nuovi cmdlet per le nuove funzionalità. Per ulteriori informazioni, vedere [Aggiornamenti del cmdlet messaggistica unificati](unified-messaging-cmdlet-updates-exchange-2013-help.md).

