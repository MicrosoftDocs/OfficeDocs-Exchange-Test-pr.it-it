---
title: 'Consente di visualizzare o configurare le directory virtuali di Outlook Web App: Exchange 2013 Help'
TOCTitle: Consente di visualizzare o configurare le directory virtuali di Outlook Web App
ms:assetid: 90babcf6-4486-4e01-9819-6d3ca4ed756c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298140(v=EXCHG.150)
ms:contentKeyID: 50481203
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Consente di visualizzare o configurare le directory virtuali di Outlook Web App

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-08-12_

È possibile utilizzare EAC o Shell per visualizzare o configurare le proprietà di una directory virtuale di Outlook Web App.


> [!WARNING]
> In Exchange Online, gli amministratori non possono visualizzare o configurare le directory virtuali di Outlook Web App.



Se si utilizza Shell per visualizzare le proprietà di una directory virtuale di Outlook Web App, le informazioni restituite sono un sottoinsieme di quelle disponibili. Ad esempio, se si utilizza il cmdlet **Get-OWAVirtualDirectory** per visualizzare le proprietà, in Exchange vengono restituite le seguenti informazioni:

  - Nome della directory virtuale

  - Nome del server

  - Versione del server Exchange

È, inoltre, possibile recuperare informazioni per una directory virtuale specifica su un server specifico utilizzando i parametri disponibili. Per ulteriori informazioni sui parametri del cmdlet **Get-OWAVirtualDirectory**, vedere [Get-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/aa998588\(v=exchg.150\)).

Se si utilizza EAC per visualizzare le proprietà di una directory virtuale di Outlook Web App, sarà possibile visualizzare la maggior parte delle proprietà per la directory virtuale visualizzata.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Directory virtuali di Outlook Web App" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per visualizzare o configurare le proprietà della directory virtuale di Outlook Web App

1.  In EAC, fare clic su **Server** \> **Directory virtuali**.
    
    È possibile utilizzare gli elenchi a discesa per selezionare il server e il tipo di directory virtuale. Per impostazione predefinita, sono visualizzati tutti i server e le directory virtuali.

2.  Nel riquadro dei risultati, selezionare la directory virtuale da visualizzare o modificare, quindi fare clic su **Modifica**.

3.  
    
    Nella scheda **Generale** è possibile visualizzare le proprietà del sito Web predefinito di Outlook Web App e specificare un URL esterno e uno interno. Visualizzare o selezionare le seguenti opzioni:
    
      - **Server**   (Di sola lettura.) **Server** visualizza il nome del server che ospita la directory virtuale di Outlook Web App.
    
      - **Versione**   (Di sola lettura.) **Versione** visualizza la versione del server di Exchange su cui si trova la directory virtuale.
    
      - **Sito Web**   (Di sola lettura.) **Sito Web** visualizza il nome del sito Web.
    
      - **Versione di Outlook Web App**   (sola lettura) **Versione di Outlook Web App** visualizza la versione del server di Exchange.
    
      - **Modificato**   (Di sola lettura.) **Modificato** visualizza data e ora dell'ultima modifica apportata alla directory virtuale.
    
      - **URL interno**   Utilizzare questa casella di testo per specificare l'URL utilizzato per accedere al sito Web da una rete interna. Un URL interno viene configurato automaticamente durante l'installazione di Exchange 2013. L'impostazione predefinita per l'URL interno per un server connesso a Internet o non connesso a Internet è https://\<Nome Computer\>/owa.
    
      - **URL esterno**   Utilizzare questa casella di testo per specificare l'URL utilizzato per accedere al sito Web da Internet. Per impostazione predefinita, **URL esterno** è vuoto. Per i server Accesso client connessi a Internet, **URL esterno** deve essere impostato sul valore pubblicato nel DNS per quel sito Active Directory. Per i server di Exchange 2013 non connessi a Internet, l'impostazione **URL esterno** deve restare vuota.

4.  
    
    Sulla scheda **Autenticazione**, specificare i metodi di autenticazione, il formato di accesso e il dominio di accesso.
    
      - **Utilizza uno o più metodi di autenticazione standard**   Selezionare tale opzione per utilizzare uno o più dei seguenti metodi di autenticazione standard:
        
        **Autenticazione integrata di Windows**   Questo metodo necessita che gli utenti dispongano di un nome di account utente e di una password di Windows Server 2008 o Windows Server 2012 validi per accedere alle informazioni. Agli utenti non vengono richiesti i relativi nomi account e password. Piuttosto, è il server a effettuare la negoziazione con i pacchetti di protezione di Windows installati nel computer client. L'autenticazione di Windows integrata abilita il server all'autenticazione degli utenti senza richiedere loro informazioni e senza trasmettere dati non crittografati attraverso la rete. Perché questo metodo funzioni, il computer client deve appartenere allo stesso dominio dei server che eseguono Exchange oppure a un dominio accreditato dal dominio in cui si trova il server di Exchange.
        
        **Autenticazione del digest per server di dominio di Windows**   Tale metodo trasmette le password attraverso la rete come valore hash per una maggiore protezione. L'autenticazione del digest può essere utilizzata solo nei domini di Windows Server 2008 e Windows Server 2012 per gli utenti che dispongono di un account archiviato in Active Directory. Per ulteriori informazioni sull'autenticazione del digest, vedere la documentazione di Windows Server.
        
        **Autenticazione di base (la password inviata non è crittografata)**   Tale metodo è un meccanismo di autenticazione semplice definito dalle specifiche HTTP che codifica il nome di accesso e la password dell'utente prima di inviare le credenziali dell'utente al server. Per accertarsi che la password sia il più possibile sicura, è consigliabile l'utilizzo della crittografia Secure Sockets Layer (SSL) tra i computer client e il server in cui è installato il ruolo del server Accesso client.
    
      - **Utilizza autenticazione basata su moduli**   L'autenticazione basata sui moduli fornisce una maggiore protezione per le directory virtuali di Outlook Web App. L'autenticazione basata sui moduli crea una pagina di accesso per Outlook Web App. È possibile configurare il tipo di prompt di accesso utilizzato dall'autenticazione basata sui moduli. Ad esempio, è possibile configurare un'autenticazione basata sui moduli per richiedere agli utenti di inserire i dati relativi al proprio dominio e nome utente nel formato dominio\\nome utente nella pagina di accesso a Outlook Web App.
        

        > [!IMPORTANT]
        > L'autenticazione basata sui moduli non richiede un canale protetto a meno che non sia abilitato il protocollo SSL.

        
        Selezionare una delle opzioni seguenti:
        
        **Dominio\\nome utente**   Viene richiesto all'utente di immettere il nome di dominio e il nome utente nel formato dominio\\nome utente. Ad esempio, per un utente chiamato Kweku nel dominio Contoso, l'accesso sarebbe contoso\\kweku.
        
        **Nome dell'entità utente**   Se viene specificato il formato di accesso per il nome dell'entità utente (UPN), il campo **Nome utente** nella pagina di accesso a Outlook Web App guida gli utenti durante l'immissione del proprio indirizzo di posta elettronica, ad esempio kweku@contoso.com. Se l'UPN di un utente non corrisponde all'indirizzo di posta elettronica, l'utente non può accedere a Outlook Web App utilizzando il prompt di accesso **PrincipalName**. Si consiglia di utilizzare il prompt di accesso **PrincipalName** solo se gli UPN degli utenti corrispondono ai relativi indirizzi di posta elettronica.
        
        **Solo nome utente**   L'utente deve immettere soltanto il nome utente, senza il nome di dominio, ad esempio Kweku. Se si utilizza il prompt di accesso **Solo nome utente** per l'autenticazione basata su moduli, è necessario specificare anche la proprietà **Dominio di accesso**. La proprietà **Dominio di accesso** determina il dominio predefinito da utilizzare quando un utente tenta di accedere a Outlook Web App. Ad esempio, se il dominio predefinito è Contoso e un utente del dominio denominato Kweku esegue l'accesso a Outlook Web App, è necessario immettere soltanto Kweku come nome utente. Il server utilizzerà il dominio predefinito Contoso. Se l'utente non è un membro del dominio Contoso, è necessario specificare il dominio e il nome utente.

5.  
    
    Sulla scheda **Funzionalità**, specificare le funzionalità che si desidera abilitare o disabilitare per gli utenti di Outlook Web App su una directory virtuale.
    

    > [!NOTE]
    > Le impostazioni delle funzionalità per i singoli utenti sostituiscono le impostazioni della directory virtuale. È possibile modificare le impostazioni di segmentazione per singoli utenti utilizzando il cmdlet <STRONG>Set-CASMailbox</STRONG> oppure i criteri delle cassette postali di Outlook Web App. Per ulteriori informazioni, vedere <A href="outlook-web-app-mailbox-policies-exchange-2013-help.md">Criteri cassetta postale di Outlook Web App</A>.

    
    Utilizzare le caselle di controllo per abilitare o disabilitare le funzionalità. Per impostazione predefinita sono visualizzate le funzionalità più comuni. Per vedere tutte le funzionalità che possono essere abilitate o disabilitate, fare clic su **Altre opzioni**.
    

    > [!NOTE]
    > L'opzione per abilitare o disabilitare la versione standard di Outlook Web App utilizzando la casella di controllo <STRONG>client Premium</STRONG> è diventata obsoleta e verrà rimossa dalle impostazioni. La versione standard di Outlook Web App è sempre abilitata.



6.  
    
    Nella scheda **Accesso ai file**, utilizzare le caselle di controllo per configurare le opzioni di visualizzazione e accesso ai file per gli utenti. L'accesso ai file consente a un utente di aprire o visualizzare il contenuto dei file allegati a un messaggio di posta elettronica.
    
    L'accesso ai file può essere controllato valutando se un utente ha effettuato l'accesso su un computer pubblico o privato. L'opzione destinata agli utenti per l'accesso a un computer privato o pubblico è disponibile solo se si utilizza l'autenticazione basata su moduli. Tutte le altre forme di autenticazione corrispondono, per impostazione predefinita, all'accesso a un computer privato.
    
      - **Accesso diretto ai file**   Selezionare questa casella di controllo per abilitare l'accesso diretto ai file. L'accesso diretto ai file consente agli utenti di aprire i file allegati ai messaggi di posta elettronica.
    
      - **Visualizzazione documenti WebReady**   Selezionare questa casella di controllo per consentire la conversione in HTML e la visualizzazione in un Web browser dei documenti supportati.
    
      - **Imponi visualizzazione documenti WebReady quando è disponibile un convertitore**   Selezionare questa casella di controllo se si desidera imporre la conversione in HTML e la visualizzazione in un Web browser dei documenti prima che gli utenti possano aprirli nell'applicazione di visualizzazione. È possibile aprire i documenti nell'applicazione di visualizzazione solo se l'accesso diretto ai file è stato abilitato.

7.  Fare clic su **Salva** per aggiornare il criterio.

## Configurazione delle proprietà della directory virtuale di Outlook Web App tramite Shell

In questo esempio, viene abilitata l'autenticazione basata sui moduli nella directory virtuale predefinita di Outlook Web App nel server Contoso.

    set-OwaVirtualDirectory -Identity "Contoso\owa (default web site)" -FormsAuthentication $true

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/bb123515\(v=exchg.150\)).

## Visualizzazione delle proprietà della directory virtuale di Outlook Web App tramite Shell

Questo esempio consente di visualizzare le proprietà di tutte le directory virtuali di Outlook Web App in tutti i siti Web di Internet Information Services (IIS) su tutti i computer in cui è installato il ruolo del server Accesso client in un'organizzazione di Exchange.

    Get-OWAVirtualDirectory

In questo esempio, è possibile visualizzare le proprietà di una directory virtuale di Outlook Web App sul sito Web IIS predefinito sul server Exchange locale.

    Get-OWAVirtualDirectory -identity "<Exchange Server Name>\owa (default web site)"

In questo esempio, è possibile visualizzare le proprietà di tutte le directory virtuali di Outlook Web App su un sito Web IIS su un determinato server di Exchange.

    Get-OWAVirtualDirectory -server <Exchange Server Name>

In questo esempio, è possibile visualizzare i valori delle proprietà per ogni directory virtuale di Outlook Web App in tutti i siti Web di IIS su tutti i server Accesso client di un'organizzazione di Exchange.

    Get-OWAVirtualDirectory | format-list

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-OwaVirtualDirectory](https://technet.microsoft.com/it-it/library/aa998588\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta modifica di una directory virtuale di Outlook Web App:

1.  In EAC, fare clic su **Server** \> **Directory virtuali** e scegliere una directory virtuale di Outlook Web App specifica.

2.  Fare clic sul pulsante **Modifica** per visualizzare le proprietà della directory virtuale.

3.  Fare clic su **Salva** o **Annulla** per chiudere la pagina delle proprietà.

