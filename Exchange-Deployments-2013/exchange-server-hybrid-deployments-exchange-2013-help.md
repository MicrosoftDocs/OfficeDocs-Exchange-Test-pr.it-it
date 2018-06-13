---
title: 'Distribuzioni ibride di Exchange Server: Exchange 2013 Help'
TOCTitle: '@NoTitle'
ms:assetid: 59e32000-4fcf-417f-a491-f1d8f9aeef9b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ200581(v=EXCHG.150)
ms:contentKeyID: 50482149
ms.date: 05/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Distribuzioni ibride di Exchange Server

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2018-04-16_

**Riepilogo:** informazioni utili per pianificare una distribuzione ibrida di Exchange.

La distribuzione ibrida offre alle organizzazioni la possibilità di estendere al cloud le numerose funzionalità e il controllo amministrativo che hanno nell'organizzazione Microsoft Exchange locale. Una distribuzione ibrida consente di ottenere l'aspetto e l'esperienza di interazione trasparente di una singola organizzazione di Exchange, combinando un'organizzazione di Exchange locale e un'organizzazione di Exchange Online in Microsoft Office 365. Può inoltre essere utilizzata come passaggio intermedio per la transizione completa a un'organizzazione di Exchange Online.

**Sommario**

Funzionalità della distribuzione ibrida di Exchange

Considerazioni relative alla distribuzione ibrida di Exchange

Componenti di una distribuzione ibrida di Exchange

Esempio di distribuzione ibrida

Aspetti da considerare prima di configurare una distribuzione ibrida

Terminologia chiave

Documentazione sulla distribuzione ibrida di Exchange

## Funzionalità della distribuzione ibrida di Exchange

Una distribuzione ibrida mette a disposizione le seguenti funzionalità:

  - Instradamento sicuro della posta tra organizzazioni locali e organizzazioni di Exchange Online.

  - Routing della posta con uno spazio dei nomi di dominio condiviso. Ad esempio, lo stesso dominio SMTP @contoso.com viene utilizzato sia dalle organizzazioni di Exchange Online che da quella locale.

  - Un elenco indirizzi globale unificato, denominato anche "rubrica condivisa".

  - Condivisione delle informazioni sulla disponibilità e sul calendario tra organizzazioni locali e organizzazioni di Exchange Online.

  - Controllo centralizzato del flusso di posta in ingresso e in uscita. È possibile configurare tutti i messaggi di Exchange in ingresso e in uscita in modo che siano instradati attraverso l'organizzazione locale di Exchange.

  - Un unico URL Outlook sul Web per le organizzazioni locali e di Exchange Online.

  - Possibilità di spostare le cassette postali esistenti dall'organizzazione locale all'organizzazione di Exchange Online. Se necessario, anche le cassette postali di Exchange Online possono essere nuovamente spostate nell'organizzazione locale.

  - Gestione centralizzata delle cassette postali tramite l'interfaccia locale di amministrazione di Exchange.

  - Monitoraggio e suggerimenti per i messaggi, ricerca in più cassette postali tra le organizzazioni locali e le organizzazioni di Exchange Online.

  - Archiviazione dei messaggi basata su cloud per le cassette postali di Exchange locali. Con a una distribuzione ibrida è possibile utilizzare l'archiviazione in Exchange Online. Per ulteriori informazioni su Archiviazione Exchange Online, vedere [Servizi aggiuntivi di Microsoft Office 365](https://go.microsoft.com/fwlink/p/?linkid=233231).

## Considerazioni relative alla distribuzione ibrida di Exchange

Prima di implementare una distribuzione ibrida di Exchange, tenere presenti le seguenti considerazioni:

  - **Requisiti di distribuzione ibrida** Prima di configurare una distribuzione ibrida, è necessario verificare che l'organizzazione locale soddisfi tutti i prerequisiti necessari per una corretta distribuzione. Per ulteriori informazioni, vedere [Prerequisiti per la distribuzione ibrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - **Client di Exchange ActiveSync**  Quando si sposta una cassetta postale dall'organizzazione di Exchange locale in Exchange Online, tutti i client che richiedono l'accesso alla cassetta postale devono essere aggiornati per l'utilizzo di Exchange Online, inclusi i dispositivi di Exchange ActiveSync. La maggior parte dei client di Exchange ActiveSync verrà automaticamente riconfigurata quando la cassetta postale viene spostata in Exchange Online. Tuttavia, alcuni dispositivi precedenti potrebbero non essere aggiornati correttamente. Per ulteriori informazioni, vedere [Impostazioni dispositivo Exchange ActiveSync con distribuzioni ibride di Exchange](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Autorizzazioni delle cassette postali**  Le autorizzazioni delle cassette postali locali (ad esempio Invia come, Accesso completo, Invia per conto di) e le autorizzazioni delle cartelle, applicate in modo esplicito alle cassette postali, vengono incluse nella migrazione a Exchange Online. Le autorizzazioni delle cassette postali (non esplicite) ereditate e le autorizzazioni concesse agli oggetti che non sono abilitati alla posta in Exchange Online non vengono migrate. È necessario verificare che tutte le autorizzazioni siano concesse in modo esplicito e che tutti gli oggetti siano abilitati alla posta prima della migrazione. È pertanto necessario pianificare la configurazione di queste autorizzazioni in Office 365, se opportuno per la propria organizzazione. Nel caso delle autorizzazioni Invia come, se si tenta di inviare l'utente e la risorsa come se non fossero spostati contemporaneamente, è necessario aggiungere in modo esplicito l'autorizzazione Invia come in Exchange Online tramite il cmdlet **Add-RecipientPermission**.

  - **Supporto relativo alle autorizzazioni per le cassette postali cross-premise** Le distribuzioni ibride di Exchange supportano l'utilizzo delle autorizzazioni di Accesso completo e Invia per conto di tra le cassette postali in un'organizzazione di Exchange locale e le cassette postali in Office 365. Altri passaggi sono necessari per le autorizzazioni Invia come. Inoltre, per alcune operazioni di configurazione aggiuntive potrebbe essere necessario il supporto di autorizzazioni delle cassette postali cross-premise a seconda della versione di Exchange installata nell'organizzazione locale. Per ulteriori informazioni, vedere [Delegate mailbox permissions](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md) in [Autorizzazioni nelle distribuzioni ibride di Exchange](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md) e [Configurare Exchange in modo da supportare le autorizzazioni per cassette postali con delega in una distribuzione ibrida](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md).
    

    > [!NOTE]
    > A partire da febbraio 2018, verrà rilasciata la funzionalità di supporto per i diritti Accesso completo, Invia per conto di per le cartelle tra foreste. La procedura di rilascio dovrebbe essere completata entro aprile 2018.



  - **Offboarding**  Nell'ambito delle attività continuative di gestione dei destinatari, potrebbe essere necessario spostare di nuovo nell'ambiente locale le cassette postali di Exchange Online.
    
    Per ulteriori informazioni su come spostare le cassette postali in una distribuzione ibrida basata su Exchange 2010, vedere [Spostare una cassetta postale di Exchange Online nell'organizzazione locale](https://technet.microsoft.com/it-it/library/hh882527\(v=exchg.150\)).
    
    Per ulteriori informazioni su come spostare le cassette postali in una distribuzione ibrida basata su Exchange 2013 o versione successiva, vedere [Spostare le cassette postali tra le organizzazioni locali e di Exchange Online nelle distribuzioni ibride](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md).

  - **Impostazioni di inoltro delle cassette postali** Le cassette postali possono essere configurate automaticamente affinché inoltrino la posta che ricevono a un'altra cassetta postale. L'inoltro delle cassette postali è supportato in Exchange Online, ma la configurazione di inoltro non viene copiata in Exchange Online durante la migrazione della cassetta postale. Prima di migrare una cassetta postale in Exchange Online, verificare di esportare la configurazione di inoltro per ogni cassetta postale. La configurazione di inoltro viene archiviata nelle proprietà `DeliverToMailboxAndForward`, `ForwardingAddress` e `ForwardingSmtpAddress` in ogni cassetta postale.

## Componenti di una distribuzione ibrida di Exchange

Una distribuzione ibrida coinvolge diversi componenti e servizi:

  - **Server di Exchange**  È necessario configurare almeno un server di Exchange nell'organizzazione locale se si desidera configurare una distribuzione ibrida. Se si esegue Exchange 2013 o una versione meno recente, è necessario installare almeno un server che esegue i ruoli Cassetta postale e Accesso client. Se si esegue Exchange 2016 o versioni successive, deve essere installato almeno un server che esegue il ruolo Cassette postali. Se necessario, i server Trasporto Edge di Exchange possono essere installati in una rete perimetrale e supportare un flusso di posta sicura con Office 365.
    

    > [!NOTE]
    > L'installazione dei server di Exchange che eseguono i ruoli server Cassette postali o Accesso client in una rete perimetrale non è supportata.



  - **Microsoft Office 365**   Il servizio Office 365 include un'organizzazione Exchange Online nell'ambito della sottoscrizione. Le organizzazioni che configurano una distribuzione ibrida devono acquistare una licenza per ogni cassetta postale che viene migrata nell'organizzazione di Exchange Online o creata all’interno di questa.

  - **Procedura guidata di configurazione ibrida**Exchange include una procedura guidata di configurazione ibrida per semplificare il processo di configurazione di una distribuzione ibrida, che comprende un'organizzazione di Exchange locali e un'organizzazione di Exchange Online.
    
    Per ulteriori informazioni, vedere [Procedura guidata di configurazione ibrida](hybrid-configuration-wizard-exchange-2013-help.md).

  - **Sistema di autenticazione di Azure AD**   Il sistema di Azure Active Directory (AD) è un servizio basato sul cloud gratuito che agisce come trust broker tra l'organizzazione Exchange 2016 locale e l'organizzazione Exchange Online. Le organizzazioni locali che configurano una distribuzione ibrida devono avere una relazione di trust federativa con il sistema di autenticazione Windows Azure AD. La relazione di trust federativa può essere creata manualmente durante la configurazione delle funzionalità di condivisione federata tra un'organizzazione di Exchange locale e altre organizzazioni di Exchange federate oppure nell'ambito della configurazione di una distribuzione ibrida con la procedura guidata per la configurazione ibrida. Quando si attiva il proprio account del servizio Office 365, viene automaticamente configurato un trust federativo con il sistema di autenticazione Windows Azure AD per il tenant di Office 365.
    
    Per ulteriori informazioni, vedere: [Sistema di autenticazione Azure AD](https://go.microsoft.com/fwlink/p/?linkid=135986)

  - **Sincronizzazione con Azure Active Directory**   La sincronizzazione di Azure AD usa Azure AD Connect per replicare le informazioni di Active Directory locale per gli oggetti abilitati alla posta nell'organizzazione di Office 365, per supportare l'elenco indirizzi globale unificato. Le organizzazioni che configurano una distribuzione ibrida devono distribuire Azure AD Connect in un server locale distinto per sincronizzare Active Directory locale con Office 365.
    
    Per ulteriori informazioni, vedere: [Azure AD Connect - Panoramica](https://go.microsoft.com/fwlink/p/?linkid=203007)

Terminologia chiave

## Esempio di distribuzione ibrida

Nello scenario seguente viene mostrata una topologia di esempio che fornisce una panoramica di una distribuzione tipica di Exchange 2016. Contoso, Ltd. è un'organizzazione a foresta singola che include un singolo dominio in cui sono installati due controller di dominio e un server Exchange 2016. Gli utenti remoti di Contoso utilizzano Outlook sul Web per connettersi a Exchange 2016 tramite Internet, controllare le proprie cassette postali e accedere al proprio calendario di Outlook.

![È configurata la distribuzione di Exchange locale prima della distribuzione ibrida con Office 365](images/JJ200581.dad133ae-d18a-42ec-8f0a-dd1de391200e(EXCHG.150).png "È configurata la distribuzione di Exchange locale prima della distribuzione ibrida con Office 365")

Si supponga che l'amministratore di rete di Contoso abbia deciso di configurare una distribuzione ibrida. Distribuisce e configura un server Azure AD Connect necessario e decide di utilizzare la funzionalità di sincronizzazione delle password di Azure AD Connect per consentire agli utenti di utilizzare le stesse credenziali per il proprio account di rete e per quello di Office 365. Dopo aver completato i prerequisiti di distribuzione ibrida e utilizzato la procedura guidata per la configurazione ibrida per selezionare le relative opzioni, la nuova topologia presenta la seguente configurazione:

  - Gli utenti utilizzeranno le stesse credenziali per accedere all'organizzazione locale e a quella di Exchange Online ("Single Sign-On").

  - Le cassette postali utente che risiedono nell'organizzazione locale e nell'organizzazione di Exchange Online utilizzeranno lo stesso dominio per gli indirizzi di posta elettronica. Ad esempio, sia le cassette postali che risiedono nell'organizzazione locale, sia quelle che risiedono nell'organizzazione di Exchange Online utilizzeranno @contoso.com per gli indirizzi di posta elettronica degli utenti.

  - Tutta la posta in uscita viene recapitata in Internet dall'organizzazione locale. Tale organizzazione controlla il trasporto di tutti i messaggi e costituisce un punto di inoltro per l'organizzazione di Exchange Online ("trasporto centralizzato della posta").

  - Gli utenti dell'organizzazione locale e dell'organizzazione di Exchange Online possono condividere le informazioni di disponibilità del calendario. Le relazioni dell'organizzazione configurate per entrambe le organizzazioni consentono inoltre la verifica dei messaggi cross-premise, Suggerimenti messaggio e la ricerca di messaggi.

  - Gli utenti dell'organizzazione locale e dell'organizzazione di Exchange Online utilizzano lo stesso URL per connettersi alle cassette postali via Internet.

![È configurata la distribuzione di Exchange locale dopo la distribuzione ibrida con Office 365](images/JJ200581.e8681849-f15d-4d0e-b77e-6105b6096c4b(EXCHG.150).png "È configurata la distribuzione di Exchange locale dopo la distribuzione ibrida con Office 365")

Se si confronta la configurazione dell'attuale organizzazione di Contoso con la configurazione della distribuzione ibrida, è possibile notare che in quest'ultima sono stati aggiunti server e servizi che supportano una maggiore comunicazione e funzionalità condivise tra l'organizzazione locale e l'organizzazione di Exchange Online. Di seguito è illustrata una panoramica delle modifiche che la distribuzione ibrida ha apportato rispetto all'organizzazione Exchange locale iniziale.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Configurazione</th>
<th>Prima della distribuzione ibrida</th>
<th>Dopo la distribuzione ibrida</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Posizione delle cassette postali</p></td>
<td><p>Solo cassette postali locali.</p></td>
<td><p>Cassette postali locali e in Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Trasporto dei messaggi</p></td>
<td><p>I server Cassette postali locali gestiscono tutto il routing dei messaggi in ingresso e in uscita.</p></td>
<td><p>I server Cassette postali locali gestiscono il routing dei messaggi interni tra l'organizzazione locale e l'organizzazione di Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook sul Web</p></td>
<td><p>I server Cassette postali locali ricevono tutte le richieste di Outlook sul Web e visualizzano le informazioni relative alle cassette postali.</p></td>
<td><p>I server Cassette postali reindirizzano le richieste di Outlook sul Web ai server Cassette postali di Exchange 2016 locali oppure forniscono un link per accedere a Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Elenco indirizzi globale unificato per entrambe le organizzazioni</p></td>
<td><p>Non applicabile; solo organizzazione singola.</p></td>
<td><p>Il server di sincronizzazione Active Directory locale replica le informazioni su Active Directory per gli oggetti abilitati alla posta in Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Single-Sign on utilizzato per entrambe le organizzazioni</p></td>
<td><p>Non applicabile; solo organizzazione singola.</p></td>
<td><p>Active Directory locale e Office 365 usano lo stesso nome utente e la stessa password per le cassette postali locali o in Office 365.</p></td>
</tr>
<tr class="even">
<td><p>Relazione organizzativa stabilita e trust federativo con il sistema di autenticazione di Azure AD</p></td>
<td><p>È possibile configurare una relazione di trust con il sistema di autenticazione di Azure AD e relazioni organizzative con altre organizzazioni di Exchange federate.</p></td>
<td><p>È necessaria una relazione di trust con il sistema di autenticazione di Azure AD. Le relazioni organizzative vengono stabilite tra l'organizzazione locale e quella di Office 365.</p></td>
</tr>
<tr class="odd">
<td><p>Condivisione informazioni sulla disponibilità</p></td>
<td><p>Condivisione delle informazioni sulla disponibilità solo tra gli utenti locali.</p></td>
<td><p>Condivisione delle informazioni sulla disponibilità tra gli utenti locali e quelli di Office 365.</p></td>
</tr>
</tbody>
</table>


## Aspetti da considerare prima di configurare una distribuzione ibrida

Dopo avere acquisito familiarità con il concetto di distribuzione ibrida, è necessario considerare attentamente alcuni aspetti importanti. La configurazione di una distribuzione ibrida potrebbe influire su più aree nella rete e nell'organizzazione di Exchange correnti.

## Sincronizzazione delle directory e Single Sign-On

La sincronizzazione di Active Directory tra le organizzazioni locali e di Office 365, che viene eseguita ogni tre ore da un server che esegue Azure Active Directory Connect, è un requisito per la configurazione di una distribuzione ibrida. La sincronizzazione delle directory consente ai destinatari delle organizzazioni di visualizzarsi reciprocamente all’interno dell’elenco indirizzi globale. Inoltre, sincronizza i nomi utente e le password, consentendo agli utenti di eseguire l'accesso con le stesse credenziali sia nell'organizzazione locale che in quella di Office 365.


> [!NOTE]
> Se si sceglie di configurare Azure AD Connect con AD FS, i nomi utente e le password degli utenti locali verranno comunque sincronizzati con Office 365 per impostazione predefinita. Tuttavia, gli utenti si autenticheranno con Active Directory locale tramite AD FS come metodo di autenticazione principale. Nel caso in cui AD FS non riesca a connettere l'utente ad Active Directory locale per qualsiasi motivo, i client tenteranno di eseguire il fallback e l'autenticazione con i nomi utente e le password sincronizzati con Office 365.



Per impostazione predefinita, tutti i clienti di Azure Active Directory e Office 365 presentano un limite predefinito di 50.000 oggetti (utenti, contatti abilitati alla posta elettronica e gruppi). Questo limite determina il numero di oggetti che è possibile creare nell'organizzazione di Office 365. Quando si verifica il primo dominio, questo limite di oggetti viene automaticamente aumentato a 300.000 oggetti. Se si dispone di un dominio verificato e si devono sincronizzare più di 300.000 oggetti o non ci sono domini da verificare e si devono sincronizzare più di 50.000 oggetti, sarà necessario contattare il supporto di Azure Active Directory per richiedere un incremento della quota di oggetti massima.

Oltre a un server che esegue Azure AD Connect, è inoltre necessario distribuire un server proxy dell'applicazione Web se si sceglie di configurare AD FS. Questo server deve essere inserito nella rete perimetrale e fungerà da intermediario tra il server Azure AD Connect interno e Internet. Il server proxy dell'applicazione Web deve accettare le connessioni da client e server su Internet mediante la porta TCP 443.

## Gestione della distribuzione ibrida

Per gestire una distribuzione ibrida in Exchange 2016 si utilizza una singola console unificata che permette di gestire sia l'organizzazione locale che l'organizzazione di Exchange Online. L'*interfaccia di amministrazione di Exchange*, che sostituisce Exchange Management Console e il Pannello di controllo di Exchange, permette di connettere e configurare funzionalità per entrambe le organizzazioni. La prima volta che si esegue la procedura guidata di configurazione ibrida viene richiesto di connettersi all'organizzazione di Exchange Online. Per connettere l'interfaccia di amministrazione di Exchange all'organizzazione di Exchange Online è necessario utilizzare un account di Office 365 membro del gruppo di ruoli Gestione organizzazione.

## Certificati

I certificati digitali SSL (Secure Sockets Layer) svolgono un ruolo importante nella configurazione della distribuzione ibrida. poiché contribuiscono a proteggere le comunicazioni tra il server ibrido locale e l'organizzazione di Exchange Online. I certificati costituiscono un requisito per la configurazione di vari tipi di servizi. Se già si utilizzano i certificati digitali nell'organizzazione Exchange, potrebbe essere necessario modificare i certificati in modo da includere altri domini o acquistare certificati aggiuntivi da un'Autorità di certificazione (CA) attendibile. Se i certificati non sono già in uso, sarà necessario acquistare uno o più da un'Autorità di certificazione (CA) attendibile.

Per ulteriori informazioni, vedere: [Requisiti dei certificati per le distribuzioni ibride](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)

## Larghezza di banda

La connessione di rete a Internet influirà direttamente sulle prestazioni di comunicazione tra l'organizzazione locale e l'organizzazione di Office 365. Ciò si verifica in particolare quando si spostano le cassette postali dal server di Exchange 2016 locale all'organizzazione di Office 365. Il tempo necessario per completare lo spostamento delle cassette postali dipenderà dalla larghezza di banda di rete disponibile, dalle dimensioni della cassetta postale e dal numero di cassette postali spostate in parallelo. Inoltre, anche altri servizi di Office 365, quali SharePoint Server 2016 e Skype for Business, possono influire sulla larghezza di banda a disposizione dei servizi di messaggistica.

Prima di spostare le cassette postali in Office 365, è necessario effettuare le seguenti operazioni:

  - Determinare la dimensione media delle cassette postali che verranno spostate in Office 365.

  - Determinare la velocità di connessione e trasmissione media per la connessione a Internet dall'organizzazione locale.

  - Calcolare la velocità media di trasferimento prevista e pianificare di conseguenza gli spostamenti della cassetta postale.

Per ulteriori informazioni su [Rete](https://go.microsoft.com/fwlink/p/?linkid=280178)

## Messaggistica unificata

La messaggistica unificata (UM) è supportata in una distribuzione ibrida tra l'organizzazione locale e quella di Office 365. La soluzione di telefonia locale deve essere in grado di comunicare con Office 365. A questo scopo potrebbe essere necessario acquistare hardware e software aggiuntivi.

Se si desidera spostare le cassette postali dall'organizzazione locale a quella di Office 365, e le cassette postali sono configurate per la messaggistica unificata, sarà necessario configurare la messaggistica unificata nella distribuzione ibrida prima di spostare le cassette postali. Se si spostano le cassette postali prima di aver configurato la messaggistica unificata, quelle cassette postali non avranno più accesso alla funzionalità di messaggistica unificata.

Per ulteriori informazioni, vedere: [Configurare la messaggistica unificata in una distribuzione ibrida](https://go.microsoft.com/fwlink/p/?linkid=842271)

## Information Rights Management

IRM (Information Rights Management) consente agli utenti di applicare modelli AD RMS (Active Directory Rights Management Services) ai messaggi da loro inviati. I modelli AD RMS possono essere utili per impedire la divulgazione di informazioni riservate permettendo agli utenti di stabilire chi può aprire un messaggio protetto da diritti e quali operazioni potrà eseguire una volta aperto.

In una distribuzione ibrida IRM richiede la pianificazione, la configurazione manuale dell'organizzazione di Office 365 e informazioni sulla modalità con cui i client utilizzano i server AD RMS, a seconda che le cassette postali risiedano nell'organizzazione locale o nell'organizzazione di Exchange Online.

Per ulteriori informazioni, vedere: [IRM nelle distribuzioni ibride di Exchange](irm-in-exchange-hybrid-deployments-exchange-2013-help.md)

## Dispositivi mobili

I dispositivi mobili sono supportati in una distribuzione ibrida. Se Exchange ActiveSync è già abilitato nei server esistenti, questi ultimi continueranno a reindirizzare le richieste dai dispositivi mobili alle cassette postali che risiedono nel server Cassette postali locale. Per i dispositivi mobili che si connettono a cassette postali esistenti che vengono spostate dall'organizzazione locale a Office 365, i profili di Exchange ActiveSync verranno aggiornati automaticamente per connettersi a Office 365 nella maggior parte dei telefoni. Tutti i dispositivi mobili che supportano Exchange ActiveSync devono essere compatibili con una distribuzione ibrida.

Per ulteriori informazioni, vedere: [Cellulari](https://go.microsoft.com/fwlink/p/?linkid=206387)

## Requisiti client

Per garantire un'esperienza migliore e prestazioni ottimali nella distribuzione ibrida, è consigliabile utilizzare Outlook 2016 o Outlook 2013 nei client. I client anteriori a Outlook 2010 non sono supportati nelle distribuzioni ibride o con Office 365.

## Licenze per Office 365

Per creare cassette postali o spostarle in Office 365, è necessario iscriversi alla versione per le aziende di Office 365 e disporre delle licenze necessarie. Quando ci si iscrive a Office 365, si riceve un numero specifico di licenze che possono essere assegnate alle nuove cassette postali o a quelle spostate dall'organizzazione locale. Ogni cassetta postale in Office 365 deve disporre di una licenza.

## Servizi di protezione da virus e posta indesiderata

Alle cassette postali spostate in Office 365 viene automaticamente fornita una protezione da virus e posta indesiderata tramite Exchange Online Protection (EOP), un servizio offerto da Office 365. Se si sceglie di eseguire il routing di tutta la posta Internet in ingresso attraverso il servizio EP, potrebbe essere necessario acquistare altre licenze EOP. È consigliabile valutare attentamente se la protezione EOP dell'organizzazione di Office 365 è sufficiente a soddisfare anche le esigenze di protezione da virus e posta indesiderata dell'organizzazione locale. Se si utilizza una protezione per l'organizzazione locale, può essere necessario aggiornare o configurare le soluzioni di protezione da virus e posta indesiderata affinché possano garantire la massima protezione per l'intera organizzazione.

Per ulteriori informazioni, vedere: [Protezione antispam e antimalware](https://technet.microsoft.com/it-it/library/jj200731\(v=exchg.150\))

## Cartelle pubbliche

Office 365 supporta le cartelle pubbliche, e le cartelle pubbliche locali possono essere migrate in Office 365. Inoltre, le cartelle pubbliche in Office 365 possono essere spostate nell'organizzazione Exchange 2016 locale. Sia gli utenti locali, sia gli utenti di Office 365 possono accedere alle cartelle pubbliche che si trovano nella loro organizzazione utilizzando Outlook sul Web, Outlook 2016, Outlook 2013 o Outlook 2010 SP2. La configurazione e l'accesso alle cartelle pubbliche locali esistenti per le cassette postali di un'organizzazione locale non cambiano quando si configura una distribuzione ibrida.

Per ulteriori informazioni, vedere: [Cartelle pubbliche](https://technet.microsoft.com/it-it/library/jj150538\(v=exchg.150\))

## Accessibilità

Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure nell'elenco di controllo, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](https://technet.microsoft.com/it-it/library/jj150484\(v=exchg.150\)).

## Terminologia chiave

Nell'elenco seguente vengono fornite le definizioni dei componenti di base associati alle distribuzioni ibride in Exchange 2013.

  - **trasporto posta centralizzato**  
    L'opzione di configurazione ibrida in cui tutti i messaggi Internet in ingresso e in uscita di Exchange Online vengono instradati tramite l'organizzazione Exchange locale. Questa opzione di routing viene configurata nella procedura guidata di configurazione ibrida. Per ulteriori informazioni, vedere [Opzioni di trasporto nelle distribuzioni ibride di Exchange](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md).

<!-- end list -->

  - **dominio di coesistenza**  
    Un dominio accettato, aggiunto all'organizzazione locale per il flusso di posta ibrido e le richieste di individuazione automatica del servizio di Office 365. Questo dominio viene aggiunto come dominio proxy secondario a tutti i criteri degli indirizzi di posta elettronica che utilizzano modelli *PrimarySmtpAddress* per i domini selezionati nella procedura guidata di configurazione ibrida. Per impostazione predefinita, questo dominio è \<domain\>.mail.onmicrosoft.com.

<!-- end list -->

  - ***HybridConfiguration* Oggetto Active Directory**  
    L'oggetto Active Directory nell'organizzazione locale che contiene i parametri di configurazione ibrida desiderati, definiti in base alle selezioni effettuate nella procedura guidata di configurazione ibrida. Il motore di configurazione ibrida utilizza questi parametri per la configurazione delle impostazioni locali e di Exchange Online allo scopo di abilitare le funzionalità ibride. Il contenuto dell'oggetto *HybridConfiguration* viene reimpostato ogni volta che viene eseguita la procedura guidata di configurazione ibrida.

<!-- end list -->

  - **motore di configurazione ibrida**  
    Il motore di configurazione ibrida esegue le azioni principali necessarie per configurare e aggiornare una distribuzione ibrida. Il motore di configurazione ibrida confronta lo stato dell'oggetto Active Directory *HybridConfiguration* con le impostazioni di configurazione correnti di Exchange locale ed Exchange Online, quindi esegue le attività necessarie per associare le impostazioni di configurazione della distribuzione ai parametri definiti nell'oggetto Active Directory *HybridConfiguration*. Per ulteriori informazioni, vedere [Hybrid Configuration Engine](hybrid-configuration-wizard-exchange-2013-help.md).

<!-- end list -->

  - **procedura guidata per il motore di configurazione ibrida (HCW)**  
    Strumento adattivo disponibile in Exchange che guida gli amministratori nella configurazione della distribuzione ibrida tra le organizzazioni locali e di Exchange Online. La procedura guidata consente di definire i parametri di configurazione ibrida nell'oggetto *HybridConfiguration* e indica al motore di configurazione ibrida di eseguire le attività di configurazione necessarie ad abilitare le funzionalità ibride definite. Per ulteriori informazioni, vedere [Procedura guidata di configurazione ibrida](hybrid-configuration-wizard-exchange-2013-help.md).

<!-- end list -->

  - **Distribuzione ibrida basata su Exchange 2010**  
    Distribuzione ibrida configurata utilizzando Service Pack 3 (SP3) per server Exchange Server 2010 locali come endpoint di collegamento tra Office 365 e i servizi di Exchange Online. Opzione di distribuzione ibrida per le organizzazioni locali Exchange 2010, Exchange Server 2007 ed Exchange Server 2003.

<!-- end list -->

  - **Distribuzione ibrida basata su Exchange 2013**  
    Distribuzione ibrida configurata utilizzando i server di Exchange 2013 locali come endpoint di collegamento tra Office 365 e i servizi di Exchange Online. Opzione di distribuzione ibrida per le organizzazioni locali Exchange 2013, Exchange 2010 ed Exchange 2007.

<!-- end list -->

  - **Distribuzione ibrida basata su Exchange 2016**  
    Distribuzione ibrida configurata utilizzando i server di Exchange 2016 locali come endpoint di collegamento tra Office 365 e i servizi di Exchange Online. Opzione di distribuzione ibrida per le organizzazioni locali Exchange 2016, Exchange 2013 ed Exchange 2010.

<!-- end list -->

  - **trasporto posta protetto**  
    Funzionalità di distribuzione ibrida configurata automaticamente che consente la messaggistica protetta tra le organizzazioni locali ed Exchange Online. I messaggi vengono crittografati e autenticati utilizzando la protezione Transport Layer Security (TLS) con un certificato selezionato nella procedura guidata di configurazione ibrida. Il tenant di Office 365 è l'endpoint delle connessioni di trasporto ibride con origine nell'organizzazione locale ed è l'origine delle connessioni di trasporto ibride verso l'organizzazione locale da Exchange Online.

Terminologia chiave

## Documentazione sulla distribuzione ibrida di Exchange

Nella tabella seguente sono disponibili collegamenti ad argomenti che illustrano i concetti e la gestione delle distribuzioni ibride in Microsoft Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Argomento</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hybrid-configuration-wizard-exchange-2013-help.md">Procedura guidata di configurazione ibrida</a></p></td>
<td><p>Informazioni sull'utilizzo della procedura guidata di configurazione ibrida e del motore di configurazione ibrida per la configurazione di una distribuzione ibrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployment-prerequisites-exchange-2013-help.md">Prerequisiti per la distribuzione ibrida</a></p></td>
<td><p>Informazioni aggiuntive sui prerequisiti delle distribuzioni ibride, incluse le organizzazioni di Exchange Server compatibili, i requisiti di Office 365 e altri requisiti di configurazione locali.</p></td>
</tr>
<tr class="odd">
<td><p><a href="certificate-requirements-for-hybrid-deployments-exchange-2013-help.md">Requisiti dei certificati per le distribuzioni ibride</a></p></td>
<td><p>Ulteriori informazioni sui requisiti per i certificati digitali nelle distribuzioni ibride.</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md">Opzioni di trasporto nelle distribuzioni ibride di Exchange</a></p></td>
<td><p>Ulteriori informazioni sulle opzioni di trasporto dei messaggi in entrata e in uscita nelle distribuzioni ibride.</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md">Transport routing nelle distribuzioni ibride di Exchange</a></p></td>
<td><p>Ulteriori informazioni sulle opzioni di routing dei messaggi in entrata e in uscita in una distribuzione ibrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md">Gestione ibrida nelle distribuzioni ibride di Exchange</a></p></td>
<td><p>Ulteriori informazioni sulla gestione della distribuzione ibrida con l'interfaccia di amministrazione di Exchange e Exchange Management Shell.</p></td>
</tr>
<tr class="odd">
<td><p><a href="shared-free-busy-in-exchange-hybrid-deployments-exchange-2013-help.md">Condivisione delle informazioni sulla disponibilità nelle distribuzioni ibride di Exchange</a></p></td>
<td><p>Ulteriori informazioni sulla condivisione delle informazioni sulla disponibilità fra l'organizzazione locale e l'organizzazione di Exchange Online in una distribuzione ibrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-roles-in-exchange-hybrid-deployments-exchange-2013-help.md">Ruoli del server nelle distribuzioni ibride di Exchange</a></p></td>
<td><p>Ulteriori informazioni sul funzionamento dei ruoli dei server di Exchange in una distribuzione ibrida.</p></td>
</tr>
<tr class="odd">
<td><p><a href="irm-in-exchange-hybrid-deployments-exchange-2013-help.md">IRM nelle distribuzioni ibride di Exchange</a></p></td>
<td><p>Ulteriori informazioni sul funzionamento di Information Rights Management in una distribuzione ibrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="permissions-in-exchange-hybrid-deployments-exchange-2013-help.md">Autorizzazioni nelle distribuzioni ibride di Exchange</a></p></td>
<td><p>Ulteriori informazioni sulle modalità con cui un distribuzione ibrida utilizza un controllo di accesso basato sui ruoli per gestire le autorizzazioni.</p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">Server Trasporto Edge con distribuzioni ibride</a></p></td>
<td><p>Ulteriori informazioni sui server Trasporto Edge di Exchange e su come vengono implementati e utilizzati in una distribuzione ibrida.</p></td>
</tr>
<tr class="even">
<td><p><a href="single-sign-on-with-hybrid-deployments-exchange-2013-help.md">Accesso Single Sign-On con distribuzioni ibride</a></p></td>
<td><p>Ulteriori informazioni su come il Single Sign-On utilizza la sincronizzazione password e la funzione di AD FS in una distribuzione ibrida.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployment-procedures-exchange-2013-help.md">Procedure di distribuzione ibrida</a></p></td>
<td><p>Procedure per la creazione e la modifica di distribuzioni ibride per organizzazioni di Exchange Online e locali.</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2010-exchange-2013-help.md">Distribuzioni ibride con Exchange 2013 ed Exchange 2010</a></p></td>
<td><p>Ulteriori informazioni sulle distribuzioni ibride basate su Exchange 2013 con le organizzazioni di Exchange 2010.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2007-exchange-2013-help.md">Distribuzioni ibride con Exchange 2013 ed Exchange 2007</a></p></td>
<td><p>Ulteriori informazioni sulle distribuzioni ibride basate su Exchange 2013 con le organizzazioni di Exchange 2007.</p></td>
</tr>
</tbody>
</table>


## Nuovo utente di Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Piccola icona per LinkedIn Learning" alt="Piccola icona per LinkedIn Learning" /> <strong>Nuovo utente di Office 365?</strong><br />
Sono disponibili esercitazioni video gratuite per <a href="https://support.office.com/it-it/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> grazie a LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

