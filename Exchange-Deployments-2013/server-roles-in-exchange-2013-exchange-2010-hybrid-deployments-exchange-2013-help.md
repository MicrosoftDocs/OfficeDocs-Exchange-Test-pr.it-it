---
title: 'Ruoli server nelle distribuzioni ibride di Exchange 2013/Exchange 2010: Exchange 2013 Help'
TOCTitle: Ruoli server nelle distribuzioni ibride di Exchange 2013/Exchange 2010
ms:assetid: 7d774948-94f9-4405-af2b-0c67c0405c0f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn393966(v=EXCHG.150)
ms:contentKeyID: 59634764
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ruoli server nelle distribuzioni ibride di Exchange 2013/Exchange 2010

Questo argomento è in fase di definizione.  

_<strong>Si applica a:</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>Ultima modifica dell'argomento:</strong>2017-02-16_

Quando si configura una distribuzione ibrida in un'organizzazione Exchange 2010, è necessario installare almeno un server Exchange 2013 con i ruoli server Accesso client e Cassette postali nell'organizzazione Exchange 2010 esistente. I server Accesso client e Cassette postali di Exchange 2013 coordinano le comunicazioni tra l'organizzazione Exchange 2010 locale e l'organizzazione Exchange Online. Queste comunicazioni comprendono le funzionalità di trasporto dei messaggi e messaggistica tra le organizzazioni locali e le organizzazioni Exchange Online.

È consigliabile installare più di un server Exchange 2013 nell'organizzazione locale per aumentare l'affidabilità e la disponibilità delle funzioni della distribuzione ibrida.

## Ruoli server in una distribuzione ibrida

Di seguito viene fornita una breve panoramica dei ruoli server di Exchange 2013 in una distribuzione ibrida:

  - **Ruolo server Accesso client**   Il ruolo server Accesso client di Exchange 2013 continua a fornire molte delle funzioni tipicamente fornite dai server Accesso client di Exchange 2010 nell'organizzazione, ma offre anche funzionalità aggiuntive necessarie per supportare una distribuzione ibrida e la coesistenza con Exchange 2010. Il server Accesso client, inoltre, gestisce i messaggi di posta protetti inviati dall'organizzazione Exchange Online all'organizzazione locale e presenta funzioni di gestione di regole di trasporto, criteri di journaling e recapito dei messaggi ai server Cassette postali in una distribuzione ibrida. Nel server Accesso client viene configurato un connettore di ricezione dedicato per supportare il trasporto ibrido sicuro della posta. Tutta la connettività dei client, tra cui l'accesso client Outlook, Outlook Web App e Outlook via Internet, passa attraverso il ruolo del server Accesso client. Anche le funzionalità per le relazioni dell'organizzazione tra organizzazioni locali e Exchange Online, come la condivisione delle informazioni sulla disponibilità, sono gestite dal ruolo del server Accesso client.
    
    Per ulteriori informazioni, vedere [Server Accesso client](https://technet.microsoft.com/it-it/library/dd298114\(v=exchg.150\)).

  - **Ruolo server Cassette postali**   Il ruolo server Cassette postali di Exchange 2013 gestisce i messaggi di posta protetti inviati all'organizzazione Exchange Online dall'organizzazione locale. Sebbene non avvenga di frequente, può anche ospitare cassette postali dei destinatari locali e comunicare con l'organizzazione Exchange Online tramite proxy per mezzo del server Accesso client locale. Nel ruolo del server Cassette viene configurato per impostazione predefinita un connettore di invio dedicato per supportare il trasporto ibrido sicuro della posta.
    
    Per ulteriori informazioni, vedere [Server Cassette postali](https://technet.microsoft.com/it-it/library/jj150491\(v=exchg.150\)).

A seconda della configurazione desiderata per la distribuzione ibrida, un server di Exchange 2013 può richiedere l'installazione di uno o entrambi questi ruoli del server:

  - **Server di Exchange singolo**   Se si decide di installare un singolo server di Exchange nell'organizzazione locale, è necessario installare i ruoli del server Accesso client e Cassette postali in tale server.

  - **Più server di Exchange**   Se si decide di installare più server di Exchange nell'organizzazione locale, è possibile installare i ruoli del server su server distinti nell'organizzazione locale. Ad esempio, è possibile installare un server di Exchange 2013 con i ruoli Cassette postali e Accesso client e un altro server Exchange con il solo ruolo Accesso client. Per la configurazione del server ibrido è tuttavia consigliabile installare i ruoli server Accesso client e Cassette postali in *ogni* server Exchange 2013 distribuito nell'organizzazione locale.

Per ulteriori informazioni sulla pianificazione della capacità di Exchange, vedere [Understanding Multiple Server Role Configurations in Capacity Planning](https://go.microsoft.com/fwlink/?linkid=266576).

## Funzionalità dei server Exchange nelle distribuzioni ibride

I server Exchange forniscono varie funzionalità importanti per l'organizzazione locale in una distribuzione ibrida:

  - **Federazione**   I server Exchange 2013 e Exchange 2010 consentono di creare una relazione di trust federativa per l'organizzazione locale con Microsoft Federation Gateway. Microsoft Federation Gateway è un servizio gratuito basato su cloud fornito da Microsoft che agisce come gestore di trust tra l'organizzazione locale e l'organizzazione tenant Office 365. Federazione è un requisito per creare una relazione organizzativa tra l'organizzazione locale e le organizzazioni Exchange Online.
    
    Per ulteriori informazioni, vedere [Federazione](https://technet.microsoft.com/it-it/library/dd335047\(v=exchg.150\)).

  - **Relazioni dell'organizzazione**   I server di Exchange 2013 con ruolo server Accesso client permettono di creare relazioni dell'organizzazione tra le organizzazioni locale ed Exchange Online. Le relazioni dell'organizzazione sono necessarie per molti altri servizi in una distribuzione ibrida, tra cui la condivisione delle informazioni di disponibilità del calendario, la verifica messaggi e gli spostamenti delle cassette postali tra le organizzazioni locali e Exchange Online.
    
    Per ulteriori informazioni, vedere [Condivisione](https://technet.microsoft.com/it-it/library/dd638083\(v=exchg.150\)).

  - **Trasporto dei messaggi**   I server Exchange 2013 con i ruoli server Accesso client e Cassette postali sono responsabili del trasporto dei messaggi in una distribuzione ibrida. I connettori di invio e ricezione vengono utilizzati come endpoint di connessione per i messaggi esterni in arrivo e consentono il recapito dei messaggi in uscita verso Internet e l'organizzazione di Exchange Online.
    
    Per ulteriori informazioni, vedere [Opzioni di trasporto nelle distribuzioni ibride di Exchange 2013/Exchange 2010](transport-options-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md).

  - **Sicurezza del trasporto messaggi**   I server Exchange 2013 con i ruoli server Accesso client e Cassette postali proteggono i messaggi scambiati fra l'organizzazione locale e l'organizzazione Exchange Online utilizzando la funzionalità di protezione del dominio di Exchange 2013. La sicurezza può essere aumentata utilizzando l'autenticazione reciproca tramite il protocollo TLS e la crittografia delle comunicazioni tramite messaggio.
    
    Per ulteriori informazioni, vedere [Informazioni sulla protezione del dominio](https://go.microsoft.com/fwlink/p/?linkid=266581).

  - **Outlook Web App**   I server di Exchange 2013 con il ruolo server Accesso client supportano la configurazione di un singolo endpoint URL per le connessioni esterne alle cassette postali locali e di Exchange Online. Per le cassette postali locali, i server Accesso client vengono configurati per soddisfare le richieste di Outlook Web App. Per le cassette postali dell'organizzazione di Exchange Online, i server Accesso client vengono configurati per visualizzare automaticamente un collegamento all'endpoint Outlook Web App nell'organizzazione Exchange.
    
    Per ulteriori informazioni, vedere [Outlook Web App](https://technet.microsoft.com/it-it/library/jj657718\(v=exchg.150\)).

## Topologia dei server Exchange

Se si sceglie di aggiungere ulteriori server Exchange 2013 per supportare la distribuzione ibrida, il server Exchange verrà distribuito come qualsiasi altro server nell'organizzazione Exchange 2010 esistente. La configurazione dell'organizzazione Exchange 2010 locale esistente per una distribuzione ibrida non richiede alcuna topologia particolare per il server di Exchange. Tuttavia, è necessario installare Exchange 2010 Service Pack 3 (SP3) su server Exchange 2010 e installare inoltre l'aggiornamento cumulativo Exchange 2013 1 (CU1) o superiore per abilitare la compatibilità e la piena funzionalità ibrida con Office 365.

La seguente tabella descrive brevemente i cambiamenti nei servizi dopo la configurazione di una distribuzione ibrida.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Servizio</th>
<th>Prima della distribuzione ibrida</th>
<th>Dopo la distribuzione ibrida</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Trasporto dei messaggi (in ingresso e in uscita)</p></td>
<td><p>Server Accesso client di Exchange 2010</p></td>
<td><p>Server Accesso client di Exchange 2013 o servizio Exchange Online Protection (EOP) incluso in Office 365</p></td>
<td><p>Il record MX (Mail Exchanger) per il dominio rimarrà invariato o sarà aggiornato in modo da puntare a EOP.</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App URL pubblico</p></td>
<td><p>Server Accesso client di Exchange 2010</p></td>
<td><p>Server Accesso client di Exchange 2013</p></td>
<td><p>I server Accesso client di Exchange 2013 eseguono il proxy delle le richieste di Outlook Web App per le cassette postali locali per i server Accesso client di Exchange 2010. Le richieste di Outlook Web App per le cassette postali ospitate su Exchange Online riceveranno un collegamento all'URL di Outlook Web App di Exchange Online.</p></td>
</tr>
</tbody>
</table>


## Software del server Exchange

Exchange 2013 CU1 o superiore consente di abilitare la funzionalità di distribuzione ibrida tramite la procedura guidata di configurazione ibrida. Per installare ulteriori server Exchange 2013 CU1 o superiori, è possibile utilizzare qualunque supporto di Exchange 2013.

Per informazioni su come scaricare la versione più recente di Exchange 2013, vedere [Aggiornamenti per Exchange 2013](https://technet.microsoft.com/library/jj907309).


> [!IMPORTANT]
> Quando si configura una distribuzione ibrida con Exchange 2013 o 2010 e Office 365, è necessaria una licenza per il server ibrido. Per ottenere gratuitamente un codice Product Key per Exchange Server da utilizzare nella configurazione della distribuzione ibrida, utilizzare lo <A href="https://aka.ms/hybridkey">strumento codice Product Key dell'edizione ibrida</A>.


