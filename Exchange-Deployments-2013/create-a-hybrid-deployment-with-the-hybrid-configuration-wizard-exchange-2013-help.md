---
title: 'Creare una distribuzione ibrida con la procedura guidata di configurazione ibrida: Exchange 2013 Help'
TOCTitle: Creare una distribuzione ibrida con la procedura guidata di configurazione ibrida
ms:assetid: 997a25d3-7fb3-4d4e-bb28-defcbf542c99
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ200787(v=EXCHG.150)
ms:contentKeyID: 50482154
ms.date: 04/28/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Creare una distribuzione ibrida con la procedura guidata di configurazione ibrida

Questo argomento è in fase di definizione.  

_<strong>Si applica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2016-12-09_

Tramite una distribuzione ibrida è possibile estendere al cloud le numerose funzionalità e il controllo amministrativo disponibili nell'organizzazione di Exchange Server locale. La distribuzione ibrida offre anche supporto per una soluzione di archiviazione basata su cloud per le cassette postali locali, con Archiviazione Exchange Online, e può anche costituire un passaggio intermedio verso la migrazione completa delle cassette postali locali a Exchange Online.

In questo argomento viene illustrata la configurazione di una distribuzione ibrida per l'organizzazione di Exchange e l'organizzazione di Exchange Online in Office 365 per le imprese tramite la procedura guidata di configurazione ibrida. In questo argomento viene creata una distribuzione ibrida per un'organizzazione con la seguente configurazione:

  - L'organizzazione locale è un'organizzazione di Exchange a foresta singola locale.

  - L'organizzazione locale non utilizza un servizio Microsoft Exchange Online Protection (EOP) per la protezione locale.

  - Nell'organizzazione locale non sono distribuiti server Trasporto Edge. La procedura guidata di configurazione ibrida supporta la configurazione di server Trasporto Edge nell'ambito di una distribuzione ibrida, ma la configurazione di server Trasporto Edge tramite la procedura guidata non viene illustrata in questo argomento.


> [!IMPORTANT]
> Affinché la procedura guidata di configurazione ibrida venga eseguita correttamente e le caratteristiche della distribuzione ibrida funzionino come previsto, sono necessari alcuni prerequisiti importanti. Prima di utilizzare la procedura guidata di configurazione ibrida per creare e configurare una distribuzione ibrida, è necessario completare tutti i prerequisiti illustrati in <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Prerequisiti per la distribuzione ibrida</A>.<BR>Inoltre, l'<A href="http://technet.microsoft.com/exdeploy2013">Assistente per la distribuzione di Exchange Server</A> è uno strumento gratuito basato su Web che consente di configurare una distribuzione ibrida tra la propria organizzazione locale e Office 365, oppure di migrare completamente a Office 365. Dopo aver risposto a una serie di semplici domande dello strumento, quest'ultimo utilizzerà le risposte ottenute per creare un elenco di controllo personalizzato con le istruzioni per configurare la distribuzione ibrida. Si consiglia vivamente di utilizzare l'Assistente per la distribuzione per generare un elenco di controllo per la distribuzione ibrida personalizzato in base alle necessità della propria organizzazione.



Per le attività di gestione aggiuntive correlate alle distribuzioni ibride, vedere [Procedure di distribuzione ibrida](hybrid-deployment-procedures-exchange-2013-help.md).

Per ulteriori informazioni sulle distribuzioni ibride, vedere [Distribuzioni ibride di Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md). Per ulteriori informazioni su Office 365, vedere [Che cos'è Office 365](http://go.microsoft.com/fwlink/?linkid=266712).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 30 minuti
    

    > [!IMPORTANT]
    > La configurazione dei requisiti per una distribuzione ibrida richiede molto più del tempo stimato per completare la procedura guidata di configurazione ibrida illustrata in questo argomento. Ad esempio, l'iscrizione a Office 365 per le imprese, la configurazione della sincronizzazione con Active Directory e l'assegnazione di licenze di Exchange Online richiedono un impegno molto superiore in termini di tempo e possono anche includere modifiche alla topologia della rete. Per completare la configurazione della distribuzione ibrida end-to-end è necessario pianificare un tempo totale superiore a quello indicato per l'esecuzione di questa procedura.



  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Distribuzioni ibride" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](https://technet.microsoft.com/it-it/library/dd638114\(v=exchg.150\)).

  - È necessario eseguire la procedura guidata per la configurazione ibrida da un computer che esegue la versione più recente di una versione supportata di Exchange. I passaggi finali della procedura guidata per la configurazione ibrida per configurare l'autenticazione OAuth di Exchange devono essere eseguiti da un server di Exchange locale oppure da un qualunque server o workstation aggiunti al dominio. Inoltre, il processo di autenticazione OAuth funziona nel modo più appropriato tramite la versione desktop di Internet Explorer 11.x o versione superiore.

  - Leggere l'argomento [Distribuzioni ibride di Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md) e assicurarsi di avere identificato tutte le aree interessate dalla configurazione di una distribuzione ibrida.

  - Esaminare e completare tutti i requisiti di distribuzione ibrida illustrati in [Prerequisiti per la distribuzione ibrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

  - Lo strumento Microsoft Remote Connectivity Analyzer controlla la connettività esterna dell'organizzazione locale di Exchange e verifica che tale organizzazione sia pronta per la configurazione di una distribuzione ibrida. È consigliabile controllare l'organizzazione locale con lo strumento Remote Connectivity Analyzer prima di configurare la distribuzione ibrida con la procedura guidata apposita. Per ulteriori informazioni, vedere lo strumento [Remote Connectivity Analyzer](http://go.microsoft.com/fwlink/p/?linkid=167905).

  - È consigliabile configurare l'accesso Single Sign-On con la sincronizzazione password di Azure Active Directory Connect. Single Sign-On permette agli utenti di accedere a entrambe le organizzazioni, locale e di Exchange Online, con una singola combinazione di nome utente e password. Evita inoltre l'immissione delle credenziali agli utenti che accedono ai contenuti archiviati nell'organizzazione di Exchange Online quando utilizzano Archiviazione Exchange Online. Per ulteriori informazioni sulla sincronizzazione password, vedere [Sincronizzazione di Azure AD Connect: implementare la sincronizzazione password](http://go.microsoft.com/fwlink/p/?linkid=723513)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](https://technet.microsoft.com/it-it/library/jj150484\(v=exchg.150\)).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare l'interfaccia di amministrazione di Exchange e la procedura guidata di configurazione ibrida per creare una distribuzione ibrida

Per creare e configurare una distribuzione ibrida, utilizzare la procedura seguente:

1.  In un server Exchange dell'organizzazione locale, accedere al nodo **Ibrido** nell'interfaccia di amministrazione di Exchange.

2.  Nel nodo **Ibridi**, fare clic su **Configura** per immettere le credenziali di Office 365.
    

    > [!IMPORTANT]
    > Se l'organizzazione locale è situata in Cina e il tenant Office 365 è ospitato da 21Vianet, è necessario selezionare la casella di controllo <STRONG>L'organizzazione Office 365 è ospitata da 21Vianet</STRONG>. Se il tenant Office 365 è ospitato da 21Vianet e tale casella di controllo non è selezionata, la procedura guidata di configurazione ibrida non si connetterà al servizio 21Vianet, le credenziali dell'account di Office 365 non verranno riconosciute e la procedura guidata non potrà essere completata adeguatamente.



3.  Al prompt di accesso a Office 365, selezionare **Accedi a Office 365** e immettere le credenziali dell'account. L'account al quale si accede deve essere un amministratore globale in Office 365.

4.  Fare clic su **Configura** per avviare la procedura guidata di configurazione ibrida.

5.  Nella pagina **Download della procedure guidata di configurazione ibrida di Microsoft Office 365**, fare clic su **Fai clic qui** per scaricare la procedura guidata. Quando viene richiesto, fare clic su **Installa** nella finestra di dialogo **Installazione applicazione**.

6.  Fare clic su **Avanti** e quindi, nella sezione **Organizzazione di Exchange Server locale**, selezionare **Rileva un server che esegue Exchange 2013 CAS o Exchange 2016**. La procedura guidata tenterà di rilevare un server Exchange locale. Se la procedura guidata non rileva un server Exchange oppure se si desidera utilizzare un altro server, selezionare **Specificare un server che esegue Exchange 2013 CAS o Exchange 2016** e quindi specificare il nome FQDN interno di un server Cassette postali di Exchange.

7.  Nella sezione **Exchange Online di Office 365**, selezionare **Microsoft Office 365** e quindi fare clic su **Avanti**.

8.  Nella pagina **Credenziali**, nella sezione **Immettere le credenziali dell'account locale** selezionare **Usa le credenziali di Windows** affinché la procedura guidata utilizzi l'account al quale è stato eseguito l'accesso nella distribuzione locale di Active Directory e nei server Exchange. Se si desidera specificare un set di credenziali diverso, deselezionare **Usa le credenziali di Windows** e specificare il nome utente e la password dell'account di Active Directory da usare. Indipendentemente da cosa si seleziona, l'account utilizzato deve essere un membro del gruppo di sicurezza Enterprise Admins.

9.  Nella selezione **Immetti le credenziali di Office 365**, specificare il nome utente e la password di un account Office 365 dotato di autorizzazioni di amministratore globale. Fare clic su **Avanti**.

10. Nella pagina **Convalida connessioni e credenziali**, la procedura guidata consentirà di connettersi all'organizzazione locale e all'organizzazione di Office 365 per convalidare le credenziali ed esaminare la configurazione corrente di entrambe le organizzazioni. Al termine, fare clic su **Avanti**.

11. Nei **Domini ibridi**, selezionare i domini da includere nella distribuzione ibrida. Nella maggior parte delle distribuzioni è possibile lasciare la colonna **Individuazione automatica** impostata su **False** per ogni dominio. Selezionare **True** accanto a un dominio solo se è necessario imporre alla procedura guidata di utilizzare le informazioni di individuazione automatica di un determinato dominio. Fare clic su **Avanti**.
    

    > [!IMPORTANT]
    > Questo passaggio di selezione dei domini potrebbe non essere visualizzato durante l'esecuzione della procedura guidata di configurazione ibrida.<BR>Il passaggio non viene visualizzato se: 
    > <UL>
    > <LI>
    > <P>All'organizzazione tenant di Office&nbsp;365 è stato aggiunto un solo dominio accettato locale. Poiché si tratta dell'unico dominio disponibile per la configurazione della distribuzione ibrida, tale dominio viene selezionato automaticamente e il passaggio della procedura guidata non viene visualizzato.</P>
    > <LI>
    > <P>All'organizzazione tenant di Office&nbsp;365 non è stato aggiunto alcun dominio accettato locale. In questo caso, viene visualizzato un messaggio di errore ed è necessario aggiungere almeno un dominio all'organizzazione tenant di Office&nbsp;365 prima di continuare. A tale scopo è possibile utilizzare il portale amministrativo di Office&nbsp;365 o, facoltativamente, configurare Active Directory Federation Services (ADFS) nell'organizzazione locale.</P></LI></UL>Questo passaggio viene visualizzato se per l'organizzazione tenant di Office&nbsp;365 sono stati aggiunti più domini accettati locali.



12. Nella pagina **Trust federativo**, fare clic su **Abilita** e quindi fare clic su **Avanti**.

13. Nella pagina **Proprietà dominio**, fare clic su **Scegli Copia negli Appunti** per copiare negli Appunti le informazioni sul token di prova per i domini selezionati per essere inclusi nella distribuzione ibrida. Aprire un editor di testo, ad esempio il Blocco note, e incollare le informazioni del token per tali domini. Prima di continuare con la procedura guidata di configurazione ibrida, è necessario utilizzare queste informazioni per creare un record di testo per ogni dominio nel DNS pubblico in uso. Consultare la Guida dell'host DNS per informazioni sull'aggiunta di un record TXT alla propria zona DNS. Dopo che i record di testo sono stati creati e i record DNS sono stati replicati, fare clic su **Avanti**.

14. Nella pagina **Certificato trasporto**, nel campo **Seleziona un server di riferimento**, selezionare il server Exchange contenente il certificato configurato in precedenza nell'elenco di controllo.

15. Nel campo **Seleziona un certificato**, selezionare il certificato da utilizzare per il trasporto posta sicuro. Nell'elenco sono visualizzati i certificati digitali emessi da un'autorità di certificazione (CA) di terze parti installati nel server Cassette postali selezionato nel passaggio precedente. Fare clic su **Avanti**.

16. Nella pagina **FQDN organizzazione**, immettere l'FQDN accessibile dall'esterno per i server Exchange pubblici. Office 365 utilizza tale FQDN per configurare i connettori di servizio per il trasporto sicuro della posta fra le organizzazioni di Exchange, ad esempio "mail.contoso.com". Fare clic su **Avanti**.

17. Le impostazioni di configurazione della distribuzione ibrida sono state aggiornate e ora è possibile inziare a modificare i servizi di Exchange e la configurazione della distribuzione ibrida. Fare clic su **Aggiorna** per avviare il processo di configurazione. Durante l'esecuzione del processo di configurazione della distribuzione ibrida, la procedura guidata mostra le aree di funzionalità e servizi configurate per la distribuzione ibrida a mano a mano che vengono aggiornate.

18. La procedura guidata mostra un messaggio di completamento ed appare il pulsante **Chiudi**. Fare clic su **Chiudi** per completare il processo di configurazione della distribuzione ibrida e chiudere la procedura guidata.

## Configurare l'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online

Per le distribuzioni ibride miste Exchange 2013/2010 e Exchange 2013/2007, la connessione di autenticazione basata su OAuth della distribuzione ibrida tra Office 365 e le organizzazioni locali Exchange non è configurata tramite la procedura guidata di configurazione ibrida. Tali distribuzioni continuano ad utilizzare il processo di trust federativo per impostazione predefinita. Tuttavia, determinate funzionalità di Exchange 2013, come Gestione record di messaggistica (MRM), Archiviazione in locale di Exchange e eDiscovery in locale, sono disponibili solo all'interno dell'organizzazione tramite il nuovo protocollo di autenticazione OAuth di Exchange. È opportuno che tutte le organizzazioni miste Exchange 2013/2010 ed Exchange 2013/2007 che desiderano implementare tali funzionalità come parte di una nuova distribuzione ibrida con Exchange Online configurino l'autenticazione OAuth di Exchange dopo aver configurato la propria distribuzione ibrida con la procedura guidata di configurazione ibrida.

Per la procedura di configurazione dettagliata, vedere [Configurazione dell'autenticazione OAuth tra organizzazioni di Exchange ed Exchange Online](https://technet.microsoft.com/it-it/library/dn594521\(v=exchg.150\))

Per ulteriori informazioni sulle funzionalità di conformità e sicurezza di Exchange che utilizzano l'autenticazione OAuth, vedere:

  - [Utilizzo dell'autenticazione OAuth per supportare l'archiviazione nelle distribuzioni ibride di Exchange](https://technet.microsoft.com/it-it/library/dn689104\(v=exchg.150\))

  - [Utilizzo dell'autenticazione OAuth per supportare eDiscovery in un'implementazione ibrida di Exchange](https://technet.microsoft.com/it-it/library/dn497703\(v=exchg.150\))

## Come verificare se l'operazione ha avuto esito positivo?

Il completamento corretto della procedura guidata di configurazione ibrida costituisce una prima indicazione del fatto che i passaggi di configurazione della distribuzione ibrida sono stati eseguiti come previsto.

Per verificare ulteriormente che la distribuzione ibrida è stata creata e configurata correttamente, procedere come segue:

  - Eseguire il comando seguente in Exchange Management Shell per l'organizzazione locale. Verranno visualizzati i valori e le impostazioni di configurazione della distribuzione ibrida, le funzionalità ibride e gli endpoint di trasporto. Verificare che tali valori siano corretti.
    
        Get-HybridConfiguration

  - Esaminare il registro della configurazione ibrida per verificare che la procedura guidata di configurazione ibrida abbia eseguito tutti i passaggi di configurazione. Per impostazione predefinita, tale registro si trova in C:\\Programmi\\Microsoft\\Exchange Server\\V15\\Logging\\Update-HybridConfiguration nel server Cassette postali locale.

  - Spostare una cassetta postale esistente nell'organizzazione di Exchange Online per verificare il supporto della funzionalità di spostamento delle cassetti postali oppure creare una nuova cassetta postale utente nell'organizzazione di Exchange Online per testare la condivisione delle informazioni di disponibilità del calendario fra le due organizzazioni. Entrambe le operazioni sulle cassette postali consentono inoltre di testare e verificare che il recapito dei messaggi fra l'organizzazione locale e l'organizzazione di Exchange Online funzioni correttamente con le cassette postali e che i messaggi vengano recapitati in modo sicuro e gestiti come messaggi interni all'organizzazione di Exchange.
    
      - Utilizzare l'interfaccia di amministrazione di Exchange per accedere a **Enterprise** \> **Destinatari** \> **Cassette postali** e creare una nuova cassetta postale remota in Exchange Online.
    
      - Utilizzare l'interfaccia di amministrazione di Exchange per accedere a **Office 365** \> **Destinatari** \> **Migrazione** per spostare una cassetta postale esistente in Exchange Online.

