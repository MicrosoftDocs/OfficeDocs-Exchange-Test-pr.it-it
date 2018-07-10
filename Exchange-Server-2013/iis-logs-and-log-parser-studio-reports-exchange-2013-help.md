---
title: 'Log Parser Studio rapporti e registri di IIS: Exchange 2013 Help'
TOCTitle: Log Parser Studio rapporti e registri di IIS
ms:assetid: 01fa67d4-dc02-4c5f-93af-6da7b97d282f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn904092(v=EXCHG.150)
ms:contentKeyID: 63907498
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Log Parser Studio rapporti e registri di IIS

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

## Analisi dei report di Log Parser Studio

Log Parser Studio è un'utilità che consente di cercare e creazione di report da diversi tipi di file di registro, inclusi quelli per Internet Information Services (IIS). Che si basa sul Log Parser 2.2 e si dispone di un'interfaccia utente completa per la creazione e la gestione delle query SQL correlate.

[Scaricare Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524244) e quindi leggere i post di blog [Introduzione a Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524243).

Tenere presente che in Exchange 2013, tutto il traffico di IIS. Ciò significa che analisi dei registri IIS il sistema ideale per ottenere un'immagine completa del numero di connessioni da raggiungere un server, delle informazioni sul protocollo sulle connessioni e degli utenti che sono la maggior parte dei influire sulle prestazioni. Oltre 20 nuovi rapporti sono stati sviluppati per Log Parser Studio allo scopo di risoluzione dei problemi relativi alle prestazioni di Exchange 2013.

## Creazione di report per Exchange 2013 problemi di prestazioni a Log Parser Studio

Per ottenere una conoscenza completa di carico complessiva nell'ambiente di Exchange 2013, utilizzare la creazione di report seguenti e confrontare i numeri in ogni server.

Un file con estensione zip contenente i report a Log Parser Studio elencati di seguito e altri report relativi alla risoluzione dei problemi, può essere [scaricato da questo](https://go.microsoft.com/fwlink/p/?linkid=524245).

  - **IIS: richieste all'ora**. Feed nei registri IIS dal sito Web predefinito (W3SVC1 directory) o il sito Web di back-end (W3SVC2 directory), ma non entrambi contemporaneamente.

  - **ACTIVESYNC\_WP: client da %**. Calcola tutte le richieste di ActiveSync suddivise per agente utente e la percentuale di ogni client e il numero totale di richieste.

  - **ACTIVESYNC\_WP: richieste all'ora (con estensione CSV)**. Elencare le richieste di ActiveSync all'ora e invia i risultati in un file CSV.

  - **ACTIVESYNC\_WP: richieste per utente (con estensione CSV)**. Vengono elencate le richieste di ActiveSync per utente e i risultati vengono inviati a un file CSV.

  - **ACTIVESYNC\_WP: richieste per utente (in alto 10K)**. Vengono elencate le richieste di ActiveSync per utente per 10.000 utenti principali.

  - **ACTIVESYNC\_WP: dall'alto gli interlocutori (con estensione CSV)**. Vengono elencati i principali client ActiveSync dal più alto minimo conteggio delle richieste e invia i risultati in un file CSV.

  - **EWS\_WP: client da %**. Calcola tutte le richieste di servizi Web Exchange suddivise per agente utente e la percentuale di ogni client e il numero totale di richieste.

  - **EWS\_WP: richieste all'ora (con estensione CSV)**. Elenca il numero totale di richieste di servizi Web Exchange all'ora.

  - **EWS\_WP: richieste per utente (con estensione CSV)**. Vengono elencate le richieste di servizi Web Exchange per utente e i risultati vengono inviati a un file CSV.

  - **EWS\_WP: richieste per utente (in alto 10K)**. Vengono elencate le richieste di servizi Web Exchange per utente per 10.000 utenti principali.

  - **EWS\_WP: dall'alto gli interlocutori (con estensione CSV)**. Sono elencati i client di servizi Web Exchange superiore dalla proprietà superiore al conteggio delle richieste di minimo.

  - **OLA\_WP: errori, per utente all'ora, al giorno**. Outlook via Internet tramite un numero di richieste di utenti.

  - **OLA\_WP: richieste all'ora**. Elencare le richieste di Outlook via Internet per ora.

  - **OLA\_WP: richieste all'ora per utente**. Elencare le richieste di Outlook via Internet all'ora per utente.

  - **OLA\_WP: richieste per utente (con estensione CSV)**. Elencare richieste di Outlook via Internet per utente.

  - **OLA\_WP: richieste per utente (in alto 10K)**. Elencare richieste di Outlook via Internet per utente per gli utenti principali 10.000.

  - **OLA\_WP: dall'alto gli interlocutori**. Sono elencati i principali Outlook via Internet client da quella più elevata per più basso conteggio delle richieste.

  - **OWA\_WP: client da %**. Calcola tutte le richieste OWA suddivise per agente utente e la percentuale di ogni client al numero totale di richieste.

  - **OWA\_WP: richieste all'ora (con estensione CSV)**. Elencare le richieste di OWA all'ora e invia i risultati in un file CSV.

  - **OWA\_WP: richieste per utente (con estensione CSV)**. Vengono elencate le richieste OWA per utente e invia i risultati in un file CSV.

  - **OWA\_WP: richieste per utente (in alto 10K)**. Vengono elencate le richieste OWA per utente per 10.000 utenti principali.

  - **OWA\_WP: dall'alto gli interlocutori (con estensione CSV)**. Vengono elencati i principali client OWA dal più alto minimo conteggio delle richieste e invia i risultati in un file CSV.

