---
title: 'Pianificazione per la messaggistica unificata: Exchange 2013 Help'
TOCTitle: Pianificazione per la messaggistica unificata
ms:assetid: 942788b1-b19d-40b3-a52e-2e1fef8df3f9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ674306(v=EXCHG.150)
ms:contentKeyID: 50481231
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Pianificazione per la messaggistica unificata

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2016-12-09_

Quando si pianifica la distribuzione della messaggistica unificata, necessario valutare diversi fattori per avere successo. È necessario comprendere i diversi elementi della messaggistica unificata, nonché ogni componente e funzione, in modo tale da poter pianificare nel modo adeguato l'infrastruttura di messaggistica unificata e la relativa distribuzione. Destinare del tempo alla pianificazione e allo studio di questi fattori consente di evitare eventuali problemi durante la distribuzione della Messaggistica unificata nell'organizzazione.

La messaggistica unificata potrebbe essere distribuita in una nuova organizzazione di Exchange, oppure potrebbe essere in corso l'aggiornamento da una soluzione di segreteria telefonica legacy o di terze parti. Se si effettua l'aggiornamento, occorre decidere se convertire i dispositivi che accettano protocolli di telefonia basati su circuiti in una rete dati che utilizza IP o se si preferisce distribuire una soluzione di VoIP aziendale come Microsoft Lync Server. Questo è solo il primo passaggio per la preparazione alla comprensione e alla distribuzione della messaggistica unificata per l'organizzazione.

## Pianificazione del sistema di segreteria telefonica

La messaggistica unificata mette a disposizione la segreteria telefonica, il fax e la messaggistica di posta elettronica in un archivio accessibile da un telefono, dal computer di un utente o da un dispositivo mobile. Gli utenti possono accedere ai messaggi vocali, alla posta elettronica, alle informazioni del calendario e ai contatti personali che si trovano nella loro cassetta postale di Exchange da client di posta elettronica quali Outlook e Outlook Web App.

I server Accesso client su cui è in esecuzione il servizio Router chiamate di messaggistica unificata di Microsoft Exchange e i server Cassette postali con il servizio Messaggistica unificata di Microsoft Exchange sono progettati per fornire le funzionalità di segreteria telefonica agli utenti dell'organizzazione.

I server Cassette postali fanno affidamento sui server Accesso client per inoltrare il traffico SIP dalle chiamate in ingresso e per stabilire una connessione con un gateway VoIP, un IP-PBX o un Session Border Controller (SBC), al fine di accettare il traffico multimediale RTP/SRTP. Tutti i messaggi vocali e fax sono inviati dal servizio Messaggistica unificata di Microsoft Exchange su un server Cassette postali per il recapito alla cassetta postale dell'utente. Affinché un utente possa utilizzare le funzionalità di segreteria telefonica con la messaggistica unificata, è necessario che disponga di una cassetta postale di Exchange.

## Pianificazione della distribuzione della messaggistica unificata

In genere, più la topologia della messaggistica unificata è semplice, più saranno semplici la distribuzione e la manutenzione della messaggistica unificata. Occorre installare il minor numero possibile di server Accesso client e Cassette postali e creare il minor numero possibile di componenti di messaggistica unificata (quali dial plan, operatori automatici e criteri cassetta postale di messaggistica unificata) sufficienti per il supporto del proprio business e degli obiettivi dell'organizzazione. Le grandi aziende con ambienti di rete e di telefonia complessi, più unità aziendali o altre strutture complesse richiedono una maggiore pianificazione rispetto alle organizzazioni più piccole, le quali presentano esigenze di messaggistica unificata relativamente semplici.

Di seguito sono presentate alcune aree da prendere in considerazione per la pianificazione della messaggistica unificata nell'organizzazione:

  - **Requisiti dell'organizzazione**   Valutare le esigenze aziendali, l'utilità della distribuzione di un sistema di segreteria telefonica, la rete fisica e la topologia aziendale, nonché i requisiti di sicurezza per l'organizzazione.

  - **Requisiti di telefonia**   Rivedere la telefonia esistente, la rete a commutazione di circuito e il sistema di segreteria telefonica.

  - **Requisiti di rete**   Analizzare la topologia di rete, la progettazione dell'attuale rete IP a commutazione di pacchetto, compresi i punti di connettività LAN e WAN, e i dispositivi.

  - **Active Directory (servizio directory)**   Ispezionare l'implementazione corrente e il progetto, valutando come integrare la messaggistica unificata.

  - **Modello di distribuzione**   Stabilire se si desidera una distribuzione di messaggistica unificata ibrida, solo online o locale.

  - **Requisiti di Exchange**   Determinare quanto segue:
    
      - Quanti utenti utilizzeranno la segreteria telefonica.
    
      - Quali funzionalità e servizi di messaggistica unificata si intende distribuire, quali chiamate simultanee, accesso interno ed esterno per gli utenti, fax in arrivo, anteprima della segreteria telefonica e così via.
    
      - Il numero di server Accesso client e Cassette postali che è necessario distribuire.
    
      - I requisiti e le quote di archiviazione per gli utenti della segreteria telefonica.
    
      - Il design migliore per la disponibilità elevata e la resilienza del sito. Sono inclusi i requisiti di sistema della messaggistica unificata, che offrono una distribuzione di messaggistica unificata con disponibilità e scalabilità elevate, e i requisiti hardware di sistema per garantire le prestazioni.

  - **Integrazione con dispositivi e componenti di telefonia**   Stabilire se utilizzare le attrezzature di telefonia tradizionali o Microsoft Lync Server. Valutare se inserire gateway VoIP, attrezzature di telefonia e server Accesso client e Cassette postali, nonché se si desidera abilitare VoIP aziendale nell'organizzazione.

## Collegamento della rete di telefonia

La messaggistica unificata richiede di integrare la distribuzione di Exchange Server con il sistema di telefonia esistente o con Microsoft Lync Server. Occorre valutare attentamente l'infrastruttura di telefonia esistente e Microsoft Lync Server, seguendo i passaggi di pianificazione corretti per distribuire e gestire la segreteria telefonica della messaggistica unificata in maniera corretta.

**Gateway VoIP**   La scelta del gateway VoIP, dell'IP-PBX, del PBX abilitato per SIP o dell'SBC corretto è solo il primo passo nell'integrazione della rete di telefonia con la messaggistica unificata. È necessario configurare questi dispositivi per lavorare con la messaggistica unificata, distribuire i server Accesso client e Cassette postali richiesti e creare e configurare tutti i componenti di messaggistica unificata necessari. Questi componenti consentono di effettuare la connessione dalla rete con protocollo basato su circuiti alla rete dati IP e di abilitare la segreteria telefonica per gli utenti.

**Microsoft Lync Server**   La messaggistica unificata può utilizzare Microsoft Lync Server per combinare funzionalità di messaggistica vocale, messaggistica istantanea, presenza avanzata, conferenza audio/video e posta elettronica in un ambiente di comunicazione integrato e intuitivo. L'integrazione di messaggistica unificata e Microsoft Lync Server offre i seguenti vantaggi:

  - Notifiche di presenza avanzate, disponibili per numerose applicazioni, che consentono di informare gli utenti sulla disponibilità dei contatti.

  - Integrazione di messaggistica immediata, messaggistica vocale, conferenze, posta elettronica e altri metodi di comunicazione che consentono agli utenti di selezionare la modalità più appropriata alle loro attività. Gli utenti possono anche passare da una modalità all'altra.

  - Disponibilità di metodi di comunicazione alternativi da qualsiasi postazione dotata di una connessione Internet.

  - Un client intelligente (Microsoft Lync) per telefonia, messaggistica istantanea e conferenze.

  - Modalità di utilizzo coerenti tra dispositivi diversi.

Per ulteriori informazioni su Microsoft Lync Server, vedere [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).


> [!NOTE]
> La pianificazione e la distribuzione della messaggistica unificata possono porre alcune sfide. A seconda dell'esperienza tecnica con Exchange e i sistemi di segreteria telefonica, è possibile voler ottenere l'assistenza di uno specialista nella messaggistica unificata. Uno specialista nella messaggistica unificata di Exchange garantisce la transizione agevole da un sistema di segreteria telefonica legacy o di terze parti alla messaggistica unificata di Exchange. Per eseguire una nuova distribuzione o l'aggiornamento di un sistema di segreteria telefonica legacy, è necessario conoscere in maniera approfondita i gateway VoIP, i PBX e la messaggistica unificata. Per ulteriori informazioni su come contattare uno specialista della messaggistica unificata, vedere <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Specialisti della messaggistica unificata di Microsoft Exchange Server 2013</A> (informazioni in lingua inglese).



## Fasi di distribuzione

Per la messaggistica unificata sono disponibili molte opzioni di distribuzione. Ciascuna opzione ha in comune diverse fasi che sono necessarie per creare un sistema modulare e ad alta disponibilità per un gran numero di utenti. Questi passaggi sono i seguenti:

1.  Distribuire e configurare i componenti di telefonia o Microsoft Lync Server con la messaggistica unificata.

2.  Verificare che siano stati installati correttamente i ruoli del server Accesso client e Cassette postali necessari per la messaggistica unificata.

3.  Creare e configurare i componenti di messaggistica unificata richiesti, tra cui dial plan, gateway IP, gruppi di risposta e criteri cassetta postale di messaggistica unificata.

4.  Eseguire le attività successive alla distribuzione, come l'ottenimento dei certificati per TLS reciproco, la creazione di operatori automatici di messaggistica unificata e la configurazione del servizio fax.

Per ulteriori informazioni sulla distribuzione di messaggistica unificata, vedere [Distribuzione della messaggistica unificata di Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md).

Se si integra l'ambiente di messaggistica unificata con Microsoft Lync Server, è necessario tenere presenti altre considerazioni di pianificazione. Per ulteriori informazioni, vedere [Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

