---
title: 'Routing di trasporto nelle distribuzioni ibride di Exchange 2013/Exchange 2010: Exchange 2013 Help'
TOCTitle: Routing di trasporto nelle distribuzioni ibride di Exchange 2013/Exchange 2010
ms:assetid: 7346bff7-41e0-401c-bd31-34498561f4c4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn393964(v=EXCHG.150)
ms:contentKeyID: 59634758
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Routing di trasporto nelle distribuzioni ibride di Exchange 2013/Exchange 2010

 

_**Si applica a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-07-29_

In questo argomento vengono illustrate le opzioni di routing per i messaggi in arrivo da Internet e in uscita verso Internet.


> [!IMPORTANT]
> Non inserire server, servizi o dispositivi, in grado di elaborare o modificare il traffico SMTP, tra i server Exchange locali e Office 365. Il flusso di posta sicura tra l'organizzazione di Exchange locale e Office 365 dipende dalle informazioni contenute nei messaggi inviati tra le organizzazioni. Sono supportati i firewall che consentano il traffico SMTP sulla porta TCP 25 senza alcuna modifica. Se un server, un servizio o un dispositivo elabora un messaggio inviato tra l'organizzazione di Exchange locale e Office 365, queste informazioni vengono rimosse. In questo caso, il messaggio non verrà più considerato interno all'organizzazione e sarà soggetto ai filtri di posta indesiderata, alle regole di trasporto e di journal e ad altri criteri che potrebbero non essere applicati.




> [!NOTE]
> Gli esempi in questo argomento non includono l'aggiunta di server Trasporto Edge nella distribuzione ibrida. Le route seguite dai messaggi tra l'organizzazione locale, l'organizzazione di Exchange Online e Internet non vengono modificate quando si aggiunge un server Trasporto Edge. Il routing cambia solo all'interno dell'organizzazione locale. Per ulteriori informazioni sull'aggiunta di server Trasporto Edge a una distribuzione ibrida, vedere <A href="edge-transport-servers-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md">Server Trasporto Edge nelle distribuzioni ibride di Exchange 2013/Exchange 2010</A>.



## Messaggi in ingresso da Internet

Nell'ambito della pianificazione e della configurazione della distribuzione ibrida, è necessario decidere se tutti i messaggi provenienti da mittenti Internet devono essere instradati attraverso l'organizzazione locale o attraverso Exchange Online. Tutti i messaggi provenienti da mittenti Internet verranno inizialmente spediti all'organizzazione selezionata e quindi verranno instradati all'ubicazione della cassetta postale del destinatario. La decisione di instradare tutti i messaggi attraverso l'organizzazione locale o attraverso Exchange Online dipende da vari fattori, incluso se si vogliono applicare criteri di conformità a tutti i messaggi inviati a entrambe le organizzazioni, quante cassette postali sono presenti in ciascuna organizzazione e così via.

Il percorso seguito dai messaggi inviati ai destinatari nell'organizzazione locale e nell'organizzazione di Exchange Online dipende da come si decide di configurare il record MX nella distribuzione ibrida. Il metodo preferito è quello di configurare il record MX in modo che punti a Exchange Online Protection (EOP) in Office 365 poiché questa configurazione offre il filtro di posta indesiderata più accurato. La procedura guidata di configurazione ibrida non consente di configurare il routing per i messaggi in entrata da Internet, né per l'organizzazione locale né per l'organizzazione di Exchange Online. Se si desidera modificare la modalità di recapito dei messaggi in arrivo da Internet, è necessario configurare manualmente il record MX.

  - **Se si modifica il record MX in modo da puntare al servizio Microsoft Exchange Online Protection (EOP) in Office 365**   Si tratta della configurazione consigliata per le distribuzioni ibride. Tutti i messaggi inviati a qualsiasi destinatario in una qualsiasi delle due organizzazioni verranno instradati prima attraverso l'organizzazione di Exchange Online. Un messaggio indirizzato a un destinatario ubicato nell'organizzazione locale verrà prima instradato attraverso l'organizzazione Exchange Online e poi recapitato al destinatario nell'organizzazione locale. Questo instradamento è raccomandato anche se sono presenti più destinatari nell'organizzazione Exchange Online che in quella locale e se si desidera che EOP filtri i messaggi. Questa opzione di configurazione serve a Exchange Online Protection per fornire l'analisi e il blocco della posta indesiderata.

  - **Se il record MX continua a puntare all'organizzazione locale:**  Tutti i messaggi inviati a qualsiasi destinatario in una qualsiasi delle due organizzazioni verranno instradati prima attraverso l'organizzazione locale. Un messaggio indirizzato ad un destinatario in Exchange Online verrà prima instradato attraverso l'organizzazione locale e poi recapitato al destinatario in Exchange Online. Questa route può essere di aiuto per le organizzazioni dove esistono criteri di conformità che richiedono di far esaminare i messaggi inviati e ricevuti da una organizzazione da una soluzione di inserimento nel journal. Se si sceglie questa opzione, Exchange Online Protection non sarà in grado di analizzare in modo efficace i messaggi di posta indesiderata.

Per ulteriori informazioni, vedere [Procedure consigliate di flusso di posta per Exchange Online e Office 365 (panoramica)](https://technet.microsoft.com/it-it/library/jj937232\(v=exchg.150\)).

Leggere la sezione che corrisponde al modo in cui vengono instradati i messaggi inviati da Internet all'organizzazione locale e Exchange Online.

## Instradare i messaggi in arrivo da Internet attraverso l'organizzazione di Exchange Online

La procedura e il diagramma seguenti illustrano il percorso seguito dai messaggi in arrivo all'interno della distribuzione ibrida, se si decide di puntare il record MX al servizio EOP nell'organizzazione di Office 365. Il percorso dei messaggi varia a seconda che si scelga di abilitare o meno il trasporto centralizzato della posta.


> [!IMPORTANT]
> Può essere necessario acquistare una licenza EOP per ogni cassetta postale locale che riceve messaggi inviati prima a EOP e quindi instradati attraverso l'organizzazione di Exchange Online. Per ulteriori informazioni, contattare il proprio rivenditore Microsoft.



Se il trasporto centralizzato della posta è *disabilitato* (configurazione predefinita), i messaggi in arrivo da Internet vengono instradati come segue all'interno di una distribuzione ibrida:

1.  Un messaggio in ingresso viene inviato da un mittente su Internet ai destinatari chris@contoso.com e david@contoso.com. La cassetta postale di Chris si trova su un server Cassette postali di Exchange 2010 nell'organizzazione locale. La cassetta postale di David si trova in Exchange Online.

2.  Dal momento che entrambi i destinatari hanno indirizzi di posta elettronica contoso.com e il record MX per contoso.com punta a EOP, il messaggio viene recapitato a EOP.

3.  EOP indirizza a Exchange Online i messaggi per entrambi i destinatari.

4.  Exchange Online analizza i messaggi alla ricerca di virus ed effettua una ricerca per ogni destinatario. Tramite la ricerca viene determinato che la cassetta postale di Chris si trova nell'organizzazione locale, mentre quella di David si trova nell'organizzazione di Exchange Online.

5.  Exchange Online suddivide il messaggio in due copie. Una copia del messaggio viene inviata alla cassetta postale di David.

6.  Exchange Online restituisce la seconda copia a EOP.

7.  EOP invia il messaggio al server Accesso client di Exchange 2013 nell'organizzazione locale.

8.  Il server Accesso client di Exchange 2013 invia il messaggio attraverso il connettore gruppo di routing configurato tra il server Exchange 2013 e il server Trasporto Hub di Exchange 2010.

9.  Il server Cassette postali Exchange 2010 riceve il messaggio e lo invia alla cassetta postale di Chris. In questo esempio, i ruoli server Accesso client e Cassette postali sono installati nello stesso server Exchange 2013.

**Instradare la posta elettronica attraverso l'organizzazione Exchange Online sia per l'organizzazione locale che per l'organizzazione Exchange Online quando il trasporto centralizzato della posta è disabilitato (configurazione predefinita)**

![Posta in ingresso via EXO senza trasporto centralizzato](images/Dn393964.23b8c817-1bf1-4a00-b722-a78548c39cb0(EXCHG.150).png "Posta in ingresso via EXO senza trasporto centralizzato")

Se il trasporto centralizzato della posta è *abilitato*, i messaggi in arrivo da Internet vengono instradati come segue all'interno di una distribuzione ibrida:

1.  Un messaggio in ingresso viene inviato da un mittente su Internet ai destinatari chris@contoso.com e david@contoso.com. La cassetta postale di Chris si trova su un server Cassette postali di Exchange 2010 nell'organizzazione locale. La cassetta postale di David si trova in Exchange Online.

2.  Dal momento che entrambi i destinatari hanno indirizzi di posta elettronica contoso.com e il record MX per contoso.com punta a EOP, il messaggio viene recapitato a EOP e analizzato per individuare eventuali virus.

3.  Poiché il trasporto centralizzato della posta è abilitato, EOP instrada i messaggi per entrambi i destinatari al server Accesso client di Exchange 2013 locale.

4.  Il server Exchange 2013 esegue una ricerca per ogni destinatario. Tramite la ricerca viene determinato che la cassetta postale di Chris si trova nell'organizzazione locale, mentre quella di David si trova nell'organizzazione di Exchange Online.

5.  Il server Exchange 2013 suddivide il messaggio in due copie. Una copia del messaggio viene recapitata alla cassetta postale di Chris nel server Cassette postali Exchange 2010 locale.

6.  Il server Exchange 2013 restituisce la seconda copia a EOP.

7.  EOP invia il messaggio a Exchange Online.

8.  Exchange recapita il messaggio alla cassetta postale di David. In questo esempio, i ruoli Accesso client e Cassette postali sono installati sullo stesso server Exchange 2013.

**Instradare la posta elettronica attraverso l'organizzazione Exchange Online sia per l'organizzazione locale che per l'organizzazione Exchange Online quando il trasporto centralizzato della posta è abilitato**

![Posta in ingresso via EXO con trasporto centralizzato](images/Dn393964.8b664544-60d5-4251-90aa-d0797963889f(EXCHG.150).png "Posta in ingresso via EXO con trasporto centralizzato")

## Instradare i messaggi in arrivo da Internet attraverso l'organizzazione locale

La procedura e il diagramma seguenti illustrano il percorso seguito dai messaggi in arrivo da Internet all'interno della distribuzione ibrida, se si decide di mantenere il record MX puntato sull'organizzazione locale.

1.  Un messaggio in ingresso viene inviato da un mittente su Internet ai destinatari chris@contoso.com e david@contoso.com. La cassetta postale di Chris si trova su un server Cassette postali di Exchange 2010 nell'organizzazione locale. La cassetta postale di David si trova in Exchange Online.

2.  Dal momento che entrambi i destinatari hanno indirizzi di posta elettronica contoso.com e il record MX per contoso.com punta all'organizzazione locale, il messaggio viene recapitato a un server Trasporto Hub di Exchange 2010.

3.  Il server Cassette postali di Exchange 2010 esegue una ricerca di ogni destinatario utilizzando un server di catalogo globale locale. Tramite la ricerca nel catalogo globale, determina che la cassetta postale di Chris si trova nel server Cassette postali di Exchange 2010, mentre quella di David si trova nell'organizzazione di Exchange Online e presenta l'indirizzo di routing ibrido david@contoso.mail.onmicrosoft.com.

4.  Il server Cassette postali di Exchange 2010 suddivide il messaggio in due copie. Una copia del messaggio viene inviata alla cassetta postale di Chris.

5.  La seconda copia del messaggio viene inviata attraverso il connettore gruppo di routing configurato tra il server Exchange 2013 ed il server Exchange 2010.

6.  Il server Cassette postali di Exchange 2013 invia il messaggio a EOP tramite un connettore di invio configurato per utilizzare TLS. EOP riceve i messaggi inviati nell'organizzazione di Exchange Online.

7.  Il servizio EOP invia il messaggio all'organizzazione di Exchange Online, dove viene analizzato per individuare eventuali virus e posta indesiderata basata su contenuto quindi recapitato alla cassetta postale di David. In questo esempio, i ruoli Accesso client e Cassette postali sono installati sullo stesso server Exchange 2013.

**Instradare la posta elettronica attraverso l'organizzazione locale sia per le organizzazioni locali che per le organizzazioni Exchange Online**

![Posta in ingresso tramite organizzazioni locali](images/Dn393964.6fa63ea0-65f5-473a-b0e7-51a2e315286d(EXCHG.150).png "Posta in ingresso tramite organizzazioni locali")

## Messaggi in uscita verso Internet

Oltre a stabilire in che modo devono essere instradati i messaggi in ingresso indirizzati a destinatari nell'organizzazione, è anche possibile scegliere in che modo devono essere instradati i messaggi in uscita inviati dai destinatari Exchange Online. Quando si esegue la procedura guidata di configurazione ibrida, è possibile selezionare due opzioni:

  - **Non abilitare trasporto centralizzato della posta**   Questa opzione, che nella procedura guidata di configurazione ibrida è selezionata per impostazione predefinita, instrada direttamente su Internet i messaggi in uscita inviati dall'organizzazione di Exchange Online. Utilizzare questa opzione se non è necessario applicare criteri di conformità locali o altre regole di elaborazione ai messaggi inviati dai destinatari nell'organizzazione di Exchange Online.

  - **Abilita trasporto centralizzato della posta**   Quando si seleziona questa opzione, i messaggi in uscita inviati dall'organizzazione di Exchange Online vengono instradati attraverso l'organizzazione locale. Ad eccezione dei messaggi inviati ad altri destinatari nella stessa organizzazione Exchange Online, tutti gli altri messaggi in uscita inviati da destinatari nell'organizzazione Exchange Online vengono inviati attraverso l'organizzazione locale. In questo modo è possibile applicare le regole di conformità a questi messaggi ed eventuali altri processi o requisiti a tutti i destinatari, indipendentemente dal fatto che si trovino nell'organizzazione locale o di Exchange Online.
    

    > [!NOTE]
    > Il trasporto centralizzato della posta è consigliato solamente per le organizzazioni con specifiche esigenze di trasporto legate alla conformità. Nelle organizzazioni Exchange standard, è consigliabile non abilitare il trasporto centralizzato della posta.



I messaggi inviati dai destinatari locali vengono sempre inviati direttamente a destinatari Internet usando il DNS, indipendentemente dalla scelta effettuata nella procedura guidata di configurazione ibrida.

Nei passaggi e nel diagramma che seguono è presentato il percorso seguito dai messaggi in uscita inviati dai destinatari locali.

1.  Chris, proprietario di una cassetta postale su un server Cassette postali di Exchange 2010 locale, invia un messaggio a un destinatario esterno su Internet, erin@cpandl.com.

2.  Il server Cassette postali di Exchange 2010 invia il messaggio al server Trasporto Hub di Exchange 2010.

3.  Il server Trasporto Hub Exchange 2010 cerca il dominio cpandl.com nel record MX e invia il messaggio ai server di posta thecpandl.com su Internet.

**Messaggi da mittenti locali a destinatari Internet**

![Posta in uscita da organizzazioni locali](images/Dn393964.fdad1c2d-03a9-496b-9c4f-9d791a4adc80(EXCHG.150).png "Posta in uscita da organizzazioni locali")

Leggere la sezione che corrisponde al modo pianificato di instradare i messaggi inviati da utenti di organizzazioni Exchange Online a destinatari Internet.

## Recapitare i messaggi Internet da Exchange Online tramite il DNS (trasporto centralizzato della posta disabilitato)

La procedura e il diagramma seguenti illustrano il percorso seguito dai messaggi in uscita inviati dagli utenti di Exchange Online a un destinatario Internet, se nella procedura guidata di configurazione ibrida non è stata selezionata l'opzione **Abilita trasporto centralizzato della posta**, ovvero si utilizza la configurazione predefinita.

1.  David, che possiede una cassetta postale nell'organizzazione di Exchange Online, invia un messaggio a un destinatario Internet esterno, erin@cpandl.com.

2.  Exchange Online analizza i messaggi per individuare eventuali virus e invia il messaggio al servizio EOP di Exchange Online.

3.  EOP cerca il dominio cpandl.com nel record MX e invia il messaggio ai server di posta cpandl.com su Internet.

**Posta inviata dai mittenti di Exchange Online instradata direttamente su Internet quando il trasporto centralizzato della posta è disabilitato (configurazione predefinita)**

![Posta in uscita diretta da Exchange Online](images/Dn393964.1f7743de-94ef-4d03-a1ed-682739546ad0(EXCHG.150).png "Posta in uscita diretta da Exchange Online")

## Instradare i messaggi Internet da Exchange Online attraverso l'organizzazione locale (trasporto centralizzato della posta abilitato)

La procedura e il diagramma seguenti illustrano il percorso seguito dai messaggi in uscita inviati dagli utenti di Exchange Online a un destinatario Internet, se nella procedura guidata di configurazione ibrida è stata selezionata l'opzione **Abilita trasporto centralizzato della posta**.

1.  David, che possiede una cassetta postale nell'organizzazione di Exchange Online, invia un messaggio a un destinatario Internet esterno, erin@cpandl.com.

2.  Exchange Online analizza i messaggi per individuare eventuali virus e invia il messaggio a EOP.

3.  EOP è configurato per inviare tutti i messaggi Internet a un server locale, di conseguenza il messaggio viene instradato a un server Accesso client di Exchange 2013. Il messaggio viene inviato tramite TLS.

4.  Un server Accesso client di Exchange 2013 sottopone il messaggio di David a tutti i controlli configurati dall'amministratore (conformità, antivirus e così via).

5.  Il server Accesso client di Exchange 2013 invia il messaggio al server Trasporto Hub di Exchange 2010. In questo esempio, i ruoli server Accesso client e Cassette postali sono installati nello stesso server Exchange 2013.

6.  Il server Trasporto Hub di Exchange 2010 cerca il dominio cpandl.com nel record MX e invia il messaggio ai server di posta cpandl.com su Internet.

**Posta elettronica da mittenti Exchange Online instradata attraverso l'organizzazione locale quando il trasporto centralizzato della posta è abilitato**

![Posta in uscita per Exchange Online tramite organizzazioni locali](images/Dn393964.b60237c7-fc7a-472a-a7cd-f7b228cd64e2(EXCHG.150).png "Posta in uscita per Exchange Online tramite organizzazioni locali")

