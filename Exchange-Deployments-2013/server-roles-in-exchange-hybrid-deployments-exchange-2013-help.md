---
title: 'Ruoli del server nelle distribuzioni ibride di Exchange: Exchange 2013 Help'
TOCTitle: Ruoli del server nelle distribuzioni ibride di Exchange
ms:assetid: 7a7eaf17-d2b0-4d62-90a2-45a0d2faca54
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659051(v=EXCHG.150)
ms:contentKeyID: 50482146
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ruoli del server nelle distribuzioni ibride di Exchange

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

È possibile configurare le distribuzioni ibride in base a Exchange 2013 e Exchange 2016. I ruoli da configurare per supportare una distribuzione ibrida dipendono dalla versione di Exchange in uso.

## Distribuzione ibrida di Exchange 2016

Durante la configurazione di una distribuzione ibrida in un'organizzazione di Exchange 2016, non è necessario installare server di Exchange aggiuntivi nell'organizzazione di Exchange esistente. I server Cassette postali coordinano le comunicazioni fra l'organizzazione di Exchange 2016 esistente e l'organizzazione di Exchange Online. Queste comunicazioni comprendono le funzionalità di trasporto dei messaggi e messaggistica tra le organizzazioni locali e le organizzazioni Exchange Online. È consigliabile installare più di un server di Exchange nell'organizzazione locale per aumentare l'affidabilità e la disponibilità delle funzioni della distribuzione ibrida.

Exchange 2016 dispone di un solo ruolo del server obbligatorio, il ruolo Cassette postali. Oltre a ospitare le cassette postali dei destinatari locali, il ruolo Cassette postali esegue tutte le funzioni necessarie per supportare una distribuzione ibrida con Exchange Online. Tra l'altro, gestisce tutti i messaggi di posta elettronica protetti scambiati fra l'organizzazione locale e l'organizzazione di Exchange Online, oltre a gestire le regole di trasporto, i criteri di inserimento nel journal e il recapito dei messaggi alle cassette postali degli utenti in una distribuzione ibrida. Tutte le funzionalità relative alle relazioni dell'organizzazione e alla connettività dei client, come la condivisione delle informazioni sulla disponibilità, vengono gestite anche dal server Cassette postali.

Ulteriori informazioni sulla pianificazione della capacità di Exchange 2016 sono disponibili nel post di blog [Dimensionamento delle distribuzioni di Exchange 2016](http://go.microsoft.com/fwlink/p/?linkid=301990).

## Distribuzione ibrida di Exchange 2013

Durante la configurazione di una distribuzione ibrida in un'organizzazione di Exchange 2013, non è necessario installare server di Exchange aggiuntivi nell'organizzazione di Exchange esistente. I server Accesso client e Cassette postali coordinano le comunicazioni fra l'organizzazione di Exchange 2013 esistente e l'organizzazione di Exchange Online. Queste comunicazioni comprendono le funzionalità di trasporto dei messaggi e messaggistica tra le organizzazioni locali e le organizzazioni Exchange Online. È consigliabile installare più di un server di Exchange nell'organizzazione locale per aumentare l'affidabilità e la disponibilità delle funzioni della distribuzione ibrida.

Questa è una breve panoramica dei ruoli del server Exchange 2013 in una distribuzione ibrida:

  - **Ruolo del server Accesso client**   Il ruolo del server Accesso client continua a fornire essenzialmente la stessa funzionalità offerta dai server Accesso client nell'organizzazione di Exchange 2013 con poche aggiunte necessarie per supportare una distribuzione ibrida. Il server Accesso client gestisce anche tutti i messaggi di posta elettronica protetti scambiati fra l'organizzazione locale e l'organizzazione di Exchange Online, oltre a gestire le regole di trasporto, i criteri di inserimento nel journal e il recapito dei messaggi alle cassette postali degli utenti in una distribuzione ibrida. Per impostazione predefinita, nel server Accesso client viene configurato un connettore di ricezione dedicato per supportare il trasporto ibrido sicuro della posta. Tutta la connettività dei client, tra cui l'accesso client Outlook, Outlook Web App e Outlook via Internet, passa attraverso il ruolo del server Accesso client. Anche le funzionalità per le relazioni dell'organizzazione tra organizzazioni locali e Exchange Online, come la condivisione delle informazioni sulla disponibilità, sono gestite dal ruolo del server Accesso client.
    
    Per ulteriori informazioni, vedere [Server Accesso client](https://technet.microsoft.com/it-it/library/dd298114\(v=exchg.150\)).

  - **Ruolo del server Cassette postali**   Il ruolo del server Cassette postali ospita le cassette postali dei destinatari locali e comunica tramite proxy con l'organizzazione di Exchange Online attraverso il server Accesso client locale. Per impostazione predefinita, nel ruolo del server Cassette viene configurato un connettore di invio dedicato per supportare il trasporto ibrido sicuro della posta.
    
    Per ulteriori informazioni, vedere [Server Cassette postali](https://technet.microsoft.com/it-it/library/jj150491\(v=exchg.150\)).

A seconda della configurazione desiderata per la distribuzione ibrida, un server di Exchange 2013 può richiedere l'installazione di uno o entrambi questi ruoli del server:

  - **Server di Exchange singolo**   Se si decide di installare un singolo server di Exchange nell'organizzazione locale, è necessario installare i ruoli del server Accesso client e Cassette postali in tale server.

  - **Più server di Exchange**   Se si decide di installare più server di Exchange nell'organizzazione locale, è possibile installare i ruoli del server su server distinti nell'organizzazione locale. Ad esempio, è possibile installare un server Exchange con i ruoli del server Cassette postali e Accesso client e un altro server Exchange con il solo ruolo del server Accesso client. Per la configurazione del server ibrido è tuttavia consigliabile installare i ruoli del server Accesso client e Cassette postali in *ogni* server distribuito nell'organizzazione locale.

Per ulteriori informazioni sulla pianificazione della capacità di Exchange 2013, vedere [Understanding Multiple Server Role Configurations in Capacity Planning](http://go.microsoft.com/fwlink/?linkid=266576).

## Funzionalità dei server Exchange nelle distribuzioni ibride

I server Exchange forniscono varie funzionalità importanti per l'organizzazione locale in una distribuzione ibrida:

  - **Federazione**   I server di Exchange consentono di creare una relazione di trust federativa per l'organizzazione locale con Microsoft Federation Gateway. Microsoft Federation Gateway è un servizio gratuito basato su cloud fornito da Microsoft che agisce come gestore di trust tra l'organizzazione locale e l'organizzazione di Office 365. Federazione è un requisito per creare una relazione organizzativa tra l'organizzazione locale e le organizzazioni Exchange Online.
    
    Per ulteriori informazioni, vedere [Federazione](https://technet.microsoft.com/it-it/library/dd335047\(v=exchg.150\)).

  - **Relazioni dell'organizzazione**   I server di Exchange 2013 con ruolo del server Accesso client e i server di Exchange 2016 con ruolo Cassette postali permettono di creare relazioni dell'organizzazione tra le organizzazioni locale e di Exchange Online. Le relazioni dell'organizzazione sono necessarie per molti altri servizi in una distribuzione ibrida, tra cui la condivisione delle informazioni di disponibilità del calendario, la verifica messaggi e gli spostamenti delle cassette postali tra le organizzazioni locali e Exchange Online.
    
    Per ulteriori informazioni, vedere [Condivisione](https://technet.microsoft.com/it-it/library/dd638083\(v=exchg.150\)).

  - **Trasporto dei messaggi**   I server di Exchange con i ruoli del server Accesso client e Cassette postali sono responsabili del trasporto dei messaggi in una distribuzione ibrida. I connettori di invio e ricezione vengono utilizzati come endpoint di connessione per i messaggi esterni in arrivo e consentono il recapito dei messaggi in uscita verso Internet e l'organizzazione di Exchange Online.
    
    Per ulteriori informazioni, vedere [Opzioni di trasporto nelle distribuzioni ibride di Exchange](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Sicurezza del trasporto messaggi**   I server di Exchange con i ruoli del server Accesso client e Cassette postali proteggono i messaggi scambiati fra l'organizzazione locale e l'organizzazione di Exchange Online utilizzando la funzionalità di protezione del dominio di Exchange. La sicurezza può essere aumentata utilizzando l'autenticazione reciproca tramite il protocollo TLS e la crittografia delle comunicazioni tramite messaggio.
    
    Per ulteriori informazioni, vedere [Informazioni sulla protezione del dominio](http://go.microsoft.com/fwlink/p/?linkid=266581).

  - **Outlook sul web (noto come Outlook Web App in Exchange 2013)**   I server di Exchange 2013 con ruolo Accesso client e i server di Exchange 2016 con ruolo Cassette postali supportano la configurazione di un singolo endpoint URL per le connessioni esterne alle cassette postali locali e di Exchange Online. Per le cassette postali locali, i server di Exchange vengono configurati per soddisfare le richieste di Outlook sul Web. Per le cassette postali dell'organizzazione di Exchange Online, i server di Exchange vengono configurati per visualizzare automaticamente un collegamento all'endpoint Outlook sul Web nell'organizzazione Exchange Online.
    
    Per ulteriori informazioni, vedere [Outlook Web App](https://technet.microsoft.com/it-it/library/jj657718\(v=exchg.150\)).

