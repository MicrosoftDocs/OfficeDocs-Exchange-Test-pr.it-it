---
title: 'Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server: Exchange 2013 Help'
TOCTitle: Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server
ms:assetid: 96fcb0dd-79ee-4e55-9e59-3ee7fbe3c4a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb676409(v=EXCHG.150)
ms:contentKeyID: 50481248
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuzione di panoramica della messaggistica UNIFICATA di Exchange 2013 e Lync Server

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

La messaggistica unificata e Microsoft Lync Server possono essere distribuiti insieme per offrire agli utenti dell'organizzazione funzioni di messaggistica vocale e immediata (IM), disponibilità avanzata, conferenza audio e video, nonché un sistema integrato di gestione della messaggistica e della posta elettronica. La messaggistica unificata è utilizzata per fornire un risponditore automatico per la segreteria telefonica, Outlook Voice Access e servizi di operatore automatico. Microsoft Lync Server mette a disposizione funzionalità più avanzate disponibili in VoIP aziendale, quali la messaggistica immediata (IM), le conferenze e le chiamate in ingresso e in uscita. In questo argomento viene descritto come configurare la messaggistica unificata e Microsoft Lync Server per il supporto di queste funzionalità.


> [!TIP]
> Con la messaggistica unificata è inoltre possibile distribuire Microsoft Office Communications Server 2007 R2. In questo argomento, "Microsoft Lync Server" fa riferimento a Microsoft Lync Server 2010 o Microsoft Lync Server 2013.



Cerchi altre informazioni su Microsoft Lync Server? Vedere [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

**Sommario**

Deploying Exchange UM and Lync Server overview

Certificate configuration recommendations

Deployment steps

For more information

## Informazioni generali sulla distribuzione della messaggistica unificata di Exchange e di Lync Server

La messaggistica unificata combina la messaggistica vocale e la posta elettronica in una singola infrastruttura di messaggistica. VoIP aziendale di Microsoft Lync Server sfrutta l'infrastruttura di messaggistica unificata per offrire la segreteria telefonica, Outlook Voice Access, le notifiche di chiamata e gli operatori automatici.

Nell'elenco di seguito sono mostrati i passaggi di distribuzione semplificati per la messaggistica unificata e Lync Server. I dettagli su ogni passaggio sono disponibili più avanti in questo argomento.

1.  Installare Microsoft Lync Server nella stessa topologia in cui saranno installati i server Accesso client con il servizio Router chiamate di messaggistica unificata di Microsoft Exchange e i server Cassette postali con il servizio Messaggistica unificata di Microsoft Exchange. Verificare che sia stato creato almeno un pool di Lync.

2.  Installare un certificato valido e firmato da un'Autorità di certificazione (CA) pubblica o privata e ritenuta attendibile da Lync Server.

3.  Installare i server Accesso client e Cassette postali. Verificare l'installazione.

4.  Installare un certificato valido e firmato dalla stessa Autorità di certificazione del certificato installato sui server Lync.

5.  Creare e configurare un dial plan URI Session Initiation Protocol (SIP).

6.  Aggiungere tutti i server Accesso client e Cassette postali al dial plan URI SIP. Tuttavia, se sono presenti più dial plan URI SIP, è necessario aggiungere tutti i server Accesso client e Cassette postali a tutti i dial plan URI SIP.

7.  Eseguire lo script ExchUcUtil.ps1 dalla cartella \<cartella di installazione di Exchange\>\\Exchange Server\\Script su un server Cassette postali.
    

    > [!IMPORTANT]
    > Lo script ExchUcUtil.ps1 crea uno o più gateway IP di messaggistica unificata per l'integrazione di Lync. È necessario disabilitare le chiamate in uscita su tutti i gateway IP di messaggistica unificata, ad eccezione di quello creato dallo script. Questo comprende la disabilitazione delle chiamate in uscita sui gateway IP di messaggistica unificata creati prima dell'esecuzione dello script. Per disabilitare le chiamate in uscita su un gateway IP di messaggistica unificata, vedere <A href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">Disabilitare le chiamate in uscita sui gateway IP di messaggistica unificata</A>.



8.  Eseguire **OcsUmUtil.exe** dalla cartella %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support su un server Lync.

9.  Distribuire Mediation Server e i gateway multimediali.

10. Installare su Mediation Server un certificato valido e firmato dalla stessa Autorità di certificazione del certificato installato sui server Lync.

11. Abilitare gli utenti alla messaggistica unificata e a VoIP aziendale.

## Raccomandazioni per la configurazione dei certificati

È necessario disporre un certificato ritenuto attendibile da entrambi i computer su cui è in esecuzione Exchange e dai computer che eseguono Lync Server. In un ambiente con Lync Server e la messaggistica unificata, utilizzare le seguenti linee guida per distribuire un certificato attendibile:

  - Sui server Lync, sui server Accesso client, sui server Cassette postali, su Mediation Server e sui gateway multimediali, importare un certificato valido e firmato da un'Autorità di certificazione pubblica o privata. Deve essere un certificato commerciale di terze parti attendibile o un certificato di infrastruttura a chiave pubblica (PKI).

  - La procedura è meno complessa se si importa lo stesso certificato PKI o commerciale di terze parti su ogni server di Exchange. Installare questo certificato attendibile anche su ogni computer che esegue Microsoft Lync Server e Mediation Server. In questo modo la distribuzione del certificato risulterà meno complicata e verrà ridotto il carico amministrativo associato alla distribuzione dei certificati. Assicurarsi tuttavia di ottenere un certificato attendibile che supporta i nomi alternativi del soggetto (SAN).
    
    Durante la distribuzione di Transport Layer Security (TLS) con la messaggistica unificata, i certificati utilizzati sul server Accesso client e sul server Cassette postali devono entrambi contenere il nome di dominio completo (FQDN) del computer locale nel Nome soggetto del certificato. Per risolvere questo problema, utilizzare un certificato pubblico e importare il certificato su tutti i server Accesso client e Cassette postali, su tutti i gateway VoIP, sugli IP-PBX e su tutti i server Lync.
    
    Se la distribuzione include gateway VoIP o IP-PBX e se si utilizza un dial plan Con protezione o SIP con protezione, è richiesto un certificato attendibile tra i server Accesso client e Cassette postali e i gateway VoIP o gli IP-PBX. Un certificato attendibile è necessario anche se si utilizza una connessione SIP diretta. Se si utilizza un dial plan Con protezione o SIP con protezione, è possibile utilizzare sui server Lync ed Exchange lo stesso certificato attendibile utilizzato sui gateway VoIP o sugli IP-PBX.

  - Quando si stabilisce una connessione tra i server Accesso client e Cassette postali di Exchange e i server Microsoft Lync, i gateway SIP di terze parti o le apparecchiature telefoniche PBX (Private Branch eXchange), è necessario utilizzare un certificato valido e firmato da un'Autorità di ceritificazione (CA) interna o pubblica di terze parti per stabilire sessioni protette. È possibile utilizzare un singolo certificato in tutti i server Accesso client e Cassette postali, purché il certificato contenga i nomi di dominio completi (FQDN) di tutti i server Accesso client e Cassette postali presenti nell'elenco SAN. In alternativa, è possibile generare un certificato diverso per ogni server Accesso client e Cassette postali, con il nome di dominio completo del computer locale presente nel nome comune del soggetto (CN) o nell'elenco SAN del certificato per quel server. La messaggistica unificata di Exchange non supporta i certificati con caratteri jolly in Microsoft Lync Server.
    
    Per la collaborazione tra Lync Server ed Exchange è richiesto un nome soggetto senza caratteri jolly. La messaggistica unificata e Lync Server utilizzano il nome soggetto come mezzo per indicare che sono peer SIP attendibili. Lync Server necessita di un nome soggetto senza caratteri jolly anche in alcuni scenari di routing delle chiamate. Il nome di dominio completo deve essere utilizzato come valore "Rilasciato a".
    
    Per la messaggistica unificata di Exchange, l'inserimento di un carattere jolly nel nome del certificato non è supportato. È tuttavia possibile inserire un carattere jolly nel SAN.

Nella tabella di seguito sono mostrati i requisiti dei certificati per l'installazione e la configurazione dei certificati per la messaggistica unificata di Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topologia</th>
<th>Configurazione dei certificati</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accesso client e Cassette postali sullo stesso server (senza Lync 2010 o 2013; dial plan non SIP)</p></td>
<td><p>È richiesto un certificato tra i server Accesso client e Cassette postali. Si tratta dello stesso certificato utilizzato tra i server Accesso client e Cassette postali e il gateway VoIP, l'IP-PBX o l'SBC.</p></td>
</tr>
<tr class="even">
<td><p>Accesso client e Cassette postali su server diversi (senza Lync 2010 o 2013; dial plan non SIP)</p></td>
<td><p>È necessario un certificato. Il certificato sui server Accesso client e Cassette postali deve corrispondere. È inoltre richiesto un certificato tra i server Accesso client e Cassette postali e il gateway VoIP, l'IP-PBX o l'SBC. Può essere o meno lo stesso certificato utilizzato tra i server Accesso client e Cassette postali. Per i server Accesso client e Cassette postali è possibile eseguire il cmdlet <strong>Create-ExchangeCertificate</strong> da uno dei server.</p></td>
</tr>
<tr class="odd">
<td><p>Accesso client e Cassette postali sullo stesso server (con Lync 2010 o 2013 e dial plan SIP)</p></td>
<td><p>È necessario un certificato. I server Accesso Client e cassette postali devono avere lo stesso certificato di primo livello Lync 2010 o Server 2013.</p></td>
</tr>
<tr class="even">
<td><p>Accesso client e Cassette postali su server diversi (con Lync 2010 o 2013 e dial plan SIP)</p></td>
<td><p>È necessario un certificato. I server Accesso Client e cassette postali devono avere lo stesso certificato di primo livello Lync 2010 o Server 2013.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Fasi di distribuzione

Dopo aver installato i server richiesti nell'organizzazione, occorre eseguire una sequenza consigliata di passaggi nelle distribuzioni di Lync Server e della messaggistica unificata di Exchange per distribuire correttamente VoIP aziendale per gli utenti.

Per ulteriori informazioni su Microsoft Lync Server, vedere [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

È necessario completare i seguenti passaggi per configurare la messaggistica unificata per l'utilizzo con le funzionalità VoIP aziendale di Lync Server:

1.  Creare uno o più dial plan URI SIP di messaggistica unificata, ognuno corrispondente a un profilo località di Lync Server. È necessario creare un profilo località di Enterprise Voice per ogni dial plan di messaggistica unificata di Exchange. È possibile utilizzare il cmdlet **Get-UMDialPlan** per ottenere il nome di dominio completo di un dial plan URI SIP. Per ulteriori informazioni su come creare un dial plan URI SIP, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Quando si integrano la messaggistica unificata di Exchange e Lync Server, probabilmente non si riterrà necessario configurare le regole di composizione o i gruppi di regole di composizione nella messaggistica unificata di Exchange. Lync Server è progettato per il routing delle chiamate e la conversione dei numeri per gli utenti dell'organizzazione. Eseguirà queste operazioni quando le chiamate vengono effettuate dalla messaggistica unificata per conto degli utenti.



2.  Installare sui server Accesso client e Cassette postali un certificato valido e firmato da un'Autorità di certificazione pubblica o privata. Si tratta della stessa Autorità di certificazione utilizzata sui server Lync.

3.  Crittografare il traffico VoIP configurando il dial plan URI SIP come protetto con SIP o protetto.
    

    > [!WARNING]
    > Se si configura l'impostazione di protezione su SIP con protezione per richiedere la crittografia per il solo traffico SIP, questa impostazione non è sufficiente su un dial plan se il pool Front End è configurato per richiedere la crittografia (in pratica, il pool richiede la crittografia per il traffico SIP e RTP). Se le impostazioni di protezione del dial plan del pool non sono compatibili, tutte le chiamate alla messaggistica unificata di Exchange dal pool Front End avranno esito negativo, generando un errore che indica "Impostazione di protezione non compatibile".

    
    Sebbene un dial plan di messaggistica unificata possa essere configurato come SIP con protezione o Con protezione, è consigliabile configurare il dial plan come Con protezione per abilitare i dispositivi Lync Phone Edition in modo che funzionino correttamente. Questa operazione è consigliata a causa delle impostazioni predefinite del livello di crittografia configurate in Lync Server. Un dispositivo Lync Phone Edition sarà utilizzabile solo se le impostazioni di crittografia sono configurate come mostrato nella tabella di seguito. In questa tabella è illustrata la relazione tra le impostazioni di crittografia per Lync Server e i dial plan di messaggistica unificata.
    
    **Impostazioni di crittografia per Lync Phone Edition**
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Lync Server</th>
    <th>Dial plan di messaggistica unificata</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Crittografia necessaria (impostazione predefinita)</p></td>
    <td><p>Protetto</p></td>
    </tr>
    <tr class="even">
    <td><p>Crittografia opzionale</p></td>
    <td><p>SIP con protezione/Con protezione</p></td>
    </tr>
    <tr class="odd">
    <td><p>Nessuna crittografia</p></td>
    <td><p>SIP con protezione</p></td>
    </tr>
    </tbody>
    </table>


4.  Aggiungere tutti i server Accesso client e Cassette postali al dial plan SIP. Per consentire al server di rispondere alle chiamate in ingresso, è necessario aggiungere tutti i server di Exchange a un dial plan, se si desidera che questi rispondano alle chiamate da Lync Server.

5.  Impostare la modalità di avvio e la porta di ascolto TLS sui server Accesso client e Cassette postali aggiunti al dial plan URI SIP su Doppio, quindi riavviare il servizio Messaggistica unificata di MicrosoftExchange su ciascun server Cassette postali e il servizio Router chiamate di messaggistica unificata di MicrosoftExchange su ciascun server Accesso client.

6.  Creare e configurare un operatore automatico di messaggistica unificata. Per ulteriori informazioni, vedere [Configurare un operatore automatico di messaggistica unificata](set-up-a-um-auto-attendant-exchange-2013-help.md).

7.  Se si desidera abilitare gli utenti alla segreteria telefonica, creare un indirizzo SIP per gli utenti che utilizzeranno VoIP aziendale. Nella maggior parte dei casi, questo indirizzo SIP sarà lo stesso utilizzato quando un utente viene abilitato per VoIP aziendale. Per ulteriori informazioni, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Gli utenti associati a un dial plan URI SIP non sono in grado di ricevere i fax in entrata. perché le chiamate vocali e fax in entrata vengono instradate attraverso un Mediation Server e quest'ultimo non supporta i fax.



8.  Aprire Exchange Management Shell ed eseguire lo script exchucutil.ps1 dalla directory %Programmi%\\Microsoft\\Exchange Server\\V15\\Scripts. Lo script exchucutil.ps1 esegue le operazioni riportate di seguito:
    
      - Concede le autorizzazioni Lync Server per la lettura Exchange componenti Active Directory di messaggistica UNIFICATA, in particolare i dial plan URI SIP creati nell'attività precedente. Per ulteriori informazioni su come configurare le autorizzazioni in Active Directory, vedere [come utilizzare Modifica ADSI per applicare le autorizzazioni](https://go.microsoft.com/fwlink/p/?linkid=82751).
    
      - Consente di creare un gateway IP di messaggistica unificata per ogni pool Lync Server o per ogni server con Lync Server Standard Edition che ospita utenti abilitati per VoIP aziendale. Per ulteriori informazioni, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).
    
      - Creare un gruppo di risposta di messaggistica unificata di Exchange per ciascun gateway IP di messaggistica unificata. L'identificatore pilota del gruppo di risposta corrisponderà al nome del dial plan di messaggistica unificata associato al gateway IP di messaggistica unificata corrispondente. Il gruppo di risposta deve specificare il dial plan SIP di messaggistica unificata utilizzato con il gateway IP di messaggistica unificata.

9.  Abilitare gli utenti alla segreteria telefonica. Durante l'abilitazione, inserire un indirizzo SIP valido per l'utente e collegarlo a un dial plan SIP. Per ulteriori informazioni, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

Per configurare Lync Server per l'utilizzo con la messaggistica unificata di Exchange è inoltre necessario completare le seguenti attività:

  - Creare profili località o dial plan di Lync. Il nome del profilo località non deve necessariamente corrispondere al nome di dominio completo dei dial plan di messaggistica unificata corrispondenti.

  - Assegnare i profili località ai pool di Lync Server.

  - Distribuire e configurare i gateway multimediali o i Mediation Server. È inoltre necessario importare un certificato della stessa Autorità di certificazione attendibile utilizzata per i certificati sui server Accesso client e Cassette postali e Lync Server.

  - Definire l'utilizzo del telefono, creare e assegnare criteri vocali e definire il routing delle chiamate esterne.

  - Configurare gli utenti per VoIP aziendale e aggiungere un identificatore SIP e URI TEL.

  - Eseguire **ocsumutil.exe**, che crea gli oggetti contatto per Outlook Voice Access e per gli operatori automatici.
    

    > [!NOTE]
    > Quando si installa Lync Server, l'attributo <STRONG>msRTC-SIPLine</STRONG> viene aggiunto ad Active Directory. Se nell'ambiente non è stato installato Lync Server, l'attributo non viene aggiunto ad Active Directory e la risoluzione del nome dell'ID chiamante nei dial plan degli scenari a foresta singola e a più foreste non funzionerà correttamente, a meno che non vengano configurati gli indirizzi proxy di messaggistica unificata per gli utenti non abilitati alla messaggistica unificata.



Dopo aver configurato Lync Server e i server Messaggistica unificata, è necessario abilitare l'utente all'utilizzo di Lync Server e installare Lync sul computer client dell'utente.


> [!IMPORTANT]
> Durante l'integrazione della messaggistica unificata con Lync Server, le notifiche di chiamata senza risposta non sono disponibili per gli utenti la cui cassetta postale si trova su un server Cassette postali di Exchange 2007 o Exchange 2010. Una notifica di chiamata senza risposta viene generata quando un utente effettua la disconnessione prima che la chiamata sia inviata a un server Cassette postali.



Inizio pagina

## Ulteriori informazioni

Per ulteriori informazioni su come eseguire le attività da completare per Microsoft Lync Server, vedere [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

