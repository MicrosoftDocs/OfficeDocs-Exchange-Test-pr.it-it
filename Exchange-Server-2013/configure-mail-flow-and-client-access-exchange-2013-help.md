---
title: 'Configurazione del flusso di posta e di Accesso client: Exchange 2013 Help'
TOCTitle: Configurazione del flusso di posta e di Accesso client
ms:assetid: 4acc7f2a-93ce-468c-9ace-d5f7eecbd8d4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ218640(v=EXCHG.150)
ms:contentKeyID: 50480545
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurazione del flusso di posta e di Accesso client

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Post-installazione delle attività per il flusso di posta e l'accesso client di Exchange Server 2013, nonché informazioni su come configurare un certificato SSL.

Dopo aver installato Microsoft Exchange Server 2013 nell'organizzazione, è necessario configurare Exchange Server 2013 per il flusso di posta e l'accesso client. Senza questi passaggi aggiuntivi, non sarà possibile inviare messaggi di posta elettronica su Internet e su client esterni quali Microsoft Office Outlook e i dispositivi ActiveSync non potranno connettersi all'organizzazione Exchange.

La procedura descritta in questo argomento presuppone una distribuzione di Exchange di base con un solo sito Active Directory e un unico spazio dei nomi SMTP (Simple Mail Transport Protocol).


> [!IMPORTANT]
> In questo argomento vengono utilizzati valori di esempio come Ex2013CAS, contoso.com, mail.contoso.com e 172.16.10.11. Sostituire i valori di esempio con i nomi server, gli FQDN e gli indirizzi IP dell'organizzazione.



Per ulteriori attività di gestione correlate a flusso di posta, client e dispositivi, vedere [Flusso di posta](mail-flow-exchange-2013-help.md) e [Client e dispositivi mobili](clients-and-mobile-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di questa attività: 50 minuti

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Finché non si configurerà un certificato SSL (Secure Socket Layer) sul server Accesso client, verranno ricevuti avvisi di certificato al momento della connessione al sito Web dell'interfaccia di amministrazione di Exchange. Questa operazione verrà illustrata più avanti in questo argomento.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!IMPORTANT]
> Ciascuna organizzazione deve disporre di almeno un server Accesso client e un server Cassette postali nella foresta di Active Directory. Inoltre, ogni sito di Active Directory che contiene un server Cassette postali deve contenere anche almeno un server Accesso client. Se si separano i ruoli del server, è consigliabile installare per primo il ruolo Cassette postali.




> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: Creare un connettore di invio

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Connettori di invio" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

Prima di poter inviare messaggi di posta elettronica su Internet, è necessario creare un connettore di invio sul server Cassette postali. Effettuare le seguenti operazioni.

1.  Aprire l'interfaccia di amministrazione di Exchange accedendo all'URL del server Accesso client. Ad esempio, https://Ex2013CAS/ECP.

2.  Immettere nome utente e password in **Nome dominio\\utente** e **Password**, quindi fare clic su **Accedi**.

3.  Andare a **Flusso di posta** \> **Connettori di invio**. Nella pagina **Connettori di invio**, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Nella procedura guidata **Nuovo connettore di invio**, specificare un nome per il connettore di invio, quindi selezionare **Internet**. Fare clic su **Avanti**.

5.  Verificare che l'opzione **Record MX associato con il dominio del destinatario** sia selezionata. Fare clic su **Avanti**.

6.  In **Spazio degli indirizzi**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Aggiungi dominio**, controllare che nel campo **Tipo** sia selezionato **SMTP**. Nel campo **Nome di dominio completo (FQDN)** immettere **\***. Fare clic su **Salva**.

7.  Verificare che la casella di controllo **Connettore di invio con ambito** sia deselezionata e fare clic su **Avanti**.

8.  In **Server di origine**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Nella finestra **Seleziona un server**, selezionare un server Cassette postali. Dopo aver selezionato il server, fare clic su **Aggiungi**, quindi su **OK**.

9.  Fare clic su **Fine**.


> [!NOTE]
> Al momento dell'installazione di Exchange 2013 viene creato un connettore di ricezione in ingresso predefinito. Questo connettore di ricezione accetta connessioni SMTP anonime da server esterni. Se si tratta della funzionalità desiderata, non è necessaria alcuna configurazione aggiuntiva. Se si desidera limitare le connessioni in ingresso da server esterni, modificare il connettore di ricezione <STRONG>Frontend predefinito &lt;Server Accesso client&gt;</STRONG> sul server Accesso client.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione di un connettore di invio in uscita, effettuare le seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, verificare che il nuovo connettore di invio sia visualizzato in **Flusso di posta** \> **Connettori di invio**.

2.  Aprire Outlook Web App e inviare un messaggio di posta elettronica a un destinatario esterno. Se il destinatario riceve il messaggio, il connettore di invio è stato configurato correttamente.

## Passaggio 2: Aggiungere i domini accettati aggiuntivi

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere La voce "Domini accettati" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

Per impostazione predefinita, quando si distribuisce una nuova organizzazione Exchange 2013 in una foresta Active Directory, Exchange utilizza il nome del dominio Active Directory in cui è stato eseguito Setup/PrepareAD. Se si desidera che i destinatari possano ricevere e inviare messaggi da e verso un altro dominio, è necessario aggiungere tale dominio come dominio accettato. Il dominio viene anche aggiunto come indirizzo SMTP primario nel criterio predefinito degli indirizzi di posta elettronica nel passaggio successivo.


> [!IMPORTANT]
> È necessario un record pubblico della risorsa MX DNS (Domain Name System) per ciascun dominio SMTP per il quale si accettano messaggi di posta elettronica da Internet. Ciascun record MX deve risolvere il server con accesso a Internet che riceve messaggi di posta elettronica per l'organizzazione.



1.  Aprire l'interfaccia di amministrazione di Exchange accedendo all'URL del server Accesso client. Ad esempio, https://Ex2013CAS/ECP.

2.  Immettere nome utente e password in **Nome dominio\\utente** e **Password**, quindi fare clic su **Accedi**.

3.  Andare a **Flusso di posta** \> **Domini accettati**. Nella pagina **Domini accettati**, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Nella procedura guidata **Nuovo dominio accettato**, specificare un nome per il dominio accettato.

5.  Nel campo **Dominio accettato**, specificare il dominio SMTP del destinatario che si desidera aggiungere, ad esempio contoso.com.

6.  Selezionare **Dominio autorevole**, quindi fare clic su **Salva**.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che la creazione di un dominio accettato sia stata eseguita correttamente, procedere come segue:

  - Nell'interfaccia di amministrazione di Exchange, verificare che il nuovo dominio accettato sia visualizzato in **Flusso di posta** \> **Domini accettati**.

## Passaggio 3: Configurare il criterio predefinito degli indirizzi di posta elettronica

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri degli indirizzi di posta elettronica" nell'argomento [Autorizzazioni per le rubriche e gli indirizzi di posta elettronica](email-address-and-address-book-permissions-exchange-2013-help.md).

Se nel passaggio precedente è stato aggiunto un dominio accettato e si desidera aggiungerlo a tutti i destinatari dell'organizzazione, è necessario aggiornare il criterio predefinito degli indirizzi di posta elettronica.

1.  Aprire l'interfaccia di amministrazione di Exchange accedendo all'URL del server Accesso client. Ad esempio, https://Ex2013CAS/ECP.

2.  Immettere nome utente e password in **Nome dominio\\utente** e **Password**, quindi fare clic su **Accedi**.

3.  Andare a **Flusso di posta** \> **Criteri degli indirizzi di posta elettronica**. Nella pagina **Criteri degli indirizzi di posta elettronica** selezionare **Criterio predefinito**, quindi scegliere il pulsante **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Nella pagina **Criterio predefinito degli indirizzi di posta elettronica**, fare clic su **Formato dell'indirizzo di posta elettronica**.

5.  In **Formato dell'indirizzo di posta elettronica**, selezionare l'indirizzo SMTP che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

6.  Nel campo **Parametri dell'indirizzo di posta elettronica** della pagina **Formato dell'indirizzo di posta elettronica**, specificare il dominio SMTP del destinatario che si desidera applicare a tutti i destinatari dell'organizzazione Exchange. Il dominio deve corrispondere al dominio accettato aggiunto nel passaggio precedente. Ad esempio, @contoso.com. Fare clic su **Salva**.

7.  Fare clic su **Salva**

8.  Nel riquadro dei dettagli del **Criterio predefinito**, fare clic su **Applica**.


> [!NOTE]
> Si consiglia di configurare un nome dell'entità utente (UPN) che corrisponda all'indirizzo di posta elettronica primario di ciascun utente. Se non si specifica un UPN corrispondente all'indirizzo di posta elettronica di un utente, quest'ultimo dovrà inserire manualmente il proprio dominio/nome utente o UPN oltre all'indirizzo di posta elettronica. Se l'UPN corrisponde all'indirizzo di posta elettronica, Outlook Web App, ActiveSync e Outlook assoceranno automaticamente l'indirizzo di posta elettronica all'UPN dell'utente.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione del criterio predefinito degli indirizzi di posta elettronica, effettuare le seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**.

2.  Selezionare una cassetta postale e, nel riquadro dei dettagli del destinatario, verificare che il campo **Cassetta postale utente** sia stato impostato su *\<alias\>*@*\<nuovo dominio accettato\>*. Ad esempio, david@contoso.com.

3.  È eventualmente possibile creare una nuova cassetta postale e verificare che ad essa venga assegnato un indirizzo di posta elettronica con il nuovo dominio accettato effettuando le seguenti operazioni:
    
    1.  Accedere a **Destinatari** \> **Cassette postali**, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e selezionare **Cassetta postale utente**.
    
    2.  Nella pagina della nuova cassetta postale utente, inserire le informazioni richieste per creare una nuova cassetta postale. Fare clic su **Salva**.
    
    3.  Selezionare la nuova cassetta postale e, nel riquadro dei dettagli del destinatario, verificare che il campo **Cassetta postale utente** sia stato impostato su *\<alias\>*@*\<nuovo dominio accettato\>*. Ad esempio, david@contoso.com.

## Passaggio 4: Configurazione degli URL esterni

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedereLa voce "*\<Servizio\>* impostazioni directory virtuale" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Prima che i client possano connettersi al nuovo server da Internet, è necessario configurare i domini interni, o URL, sulle directory virtuali del server Accesso client, quindi configurare i record DNS pubblici. Nella procedura riportata di seguito viene configurato lo stesso dominio esterno sull'URL esterno di ciascuna directory virtuale. Se si desidera configurare domini esterni diversi su uno o più URL esterni delle directory virtuali, è necessario effettuare una configurazione manuale. Per ulteriori informazioni, vedere [Gestione di directory virtuali](virtual-directory-management-exchange-2013-help.md).

1.  Aprire l'interfaccia di amministrazione di Exchange accedendo all'URL del server Accesso client. Ad esempio, https://Ex2013CAS/ECP.

2.  Immettere nome utente e password in **Nome dominio\\utente** e **Password**, quindi fare clic su **Accedi**.

3.  Accedere a **Server** \> **Server**, selezionare il nome del server Accesso client con connessione a Internet e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Selezionare **Outlook via Internet**.

5.  Nel campo **Specifica il nome dell'host esterno**, specificare il nome di dominio completo accessibile esternamente del server Accesso client. ad esempio, mail.contoso.com.

6.  A questo punto è anche possibile impostare il nome di dominio completo del server Accesso client accessibile internamente. Nel campo **Specifica il nome dell'host interno**, inserire il nome di dominio completo utilizzato nel passo precedente. ad esempio, mail.contoso.com.

7.  Fare clic su **Salva**.

8.  Andare a **Server** \> **Directory virtuali** e fare clic su **Configura il dominio di accesso esterno** ![Icona Configura](images/JJ218640.a9c33f23-3d44-44e7-a5d0-8446200c746e(EXCHG.150).gif "Icona Configura").

9.  In **Seleziona i server Accesso client da utilizzare con l'URL esterno**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")

10. Selezionare i server Accesso client da configurare e fare clic su **Aggiungi**. Dopo aver aggiunto tutti i server Accesso client da configurare, fare clic su **OK**.

11. In **Immetti il nome di dominio da utilizzare con i server Accesso client esterni**, digitare il dominio esterno che si desidera applicare. Ad esempio, mail.contoso.com. Fare clic su **Salva**.
    

    > [!NOTE]
    > Alcune organizzazioni preferiscono utilizzare un nome di dominio completo univoco per Outlook Web App al fine di proteggere gli utenti dalle modifiche al nome di dominio completo del server sottostante. Numerose organizzazioni utilizzano owa.contoso.com invece di mail.contoso.com come nome di dominio completo per Outlook Web App. Se si desidera configurare un nome di dominio completo univoco per Outlook Web App, fare quanto segue dopo aver completato il passo precedente. Questo elenco di controllo si basa sul presupposto che per Outlook Web App sia stato configurato un nome di dominio completo univoco. 
    > <OL>
    > <LI>
    > <P>Selezionare <STRONG>owa (sito Web predefinito)</STRONG> e fare clic su <STRONG>Modifica</STRONG>&nbsp;<IMG title="Icona Modifica" alt="Icona Modifica" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">.</P>
    > <LI>
    > <P>In <STRONG>URL esterno</STRONG>, digitare <STRONG>https://</STRONG>, quindi il nome di dominio completo univoco che si desidera utilizzare per Outlook Web App e infine aggiungere <STRONG>/owa</STRONG>. Ad esempio, https://owa.contoso.com/owa.</P>
    > <LI>
    > <P>Fare clic su <STRONG>Salva</STRONG>.</P>
    > <LI>
    > <P>Selezionare <STRONG>ecp (sito Web predefinito)</STRONG> e fare clic su <STRONG>Modifica</STRONG>&nbsp;<IMG title="Icona Modifica" alt="Icona Modifica" src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">.</P>
    > <LI>
    > <P>In <STRONG>URL esterno</STRONG>, digitare <STRONG>https://</STRONG>, quindi lo stesso nome di dominio completo specificato nel passo precedente per Outlook Web App e infine aggiungere <STRONG>/ecp</STRONG>. Ad esempio, https://owa.contoso.com/ecp.</P>
    > <LI>
    > <P>Fare clic su <STRONG>Salva</STRONG>.</P></LI></OL>



Dopo aver configurato l'URL esterno delle directory virtuali del server Accesso client, è necessario configurare i record DNS pubblici per l'individuazione automatica, Outlook Web App e il flusso di posta. I record DNS pubblici devono puntare all'indirizzo IP esterno o al nome di dominio completo del server Accesso client con connessione a Internet e utilizzare i nomi di dominio completo accessibili esternamente configurati sul server Accesso client. Di seguito sono riportati alcuni esempi di record DNS di cui si consiglia la creazione per abilitare il flusso di posta e la connettività dei client esterni.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Tipo di record DNS</th>
<th>Valore</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Contoso.com</p></td>
<td><p>MX</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Mail.contoso.com</p></td>
<td><p>A</p></td>
<td><p>172.16.10.11</p></td>
</tr>
<tr class="odd">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Autodiscover.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Mail.contoso.com</p></td>
</tr>
</tbody>
</table>


## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione dell'URL esterno sulle directory virtuali del server Accesso client, effettuare le seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Directory virtuali**.

2.  Nel campo **Seleziona server**, selezionare il server Accesso Client con connessione a Internet.

3.  Selezionare una directory virtuale quindi, nel riquadro dei dettagli di tale directory, verificare che il campo **URL esterno** contenga il nome di dominio completo e il servizio corretti come riportato di seguito:
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Directory virtuale</th>
    <th>Valore URL esterno</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Individuazione automatica</strong></p></td>
    <td><p>Nessun URL esterno visualizzato</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Per verificare di aver configurato correttamente i record DNS pubblici, fare quanto segue:

1.  Aprire un prompt dei comandi ed eseguire `nslookup.exe`.

2.  Passare a un server DNS che può eseguire una query sulla zona DNS pubblica.

3.  In `nslookup`, controllare il record di ciascun nome di dominio completo creato. Verificare che il valore restituito per ogni nome di dominio completo sia corretto.

4.  In `nslookup`, digitare `set type=mx` quindi controllare il dominio accettato aggiunto nel passaggio 1. Verificare che il valore restituito corrisponda al nome di dominio completo del server Accesso client.

## Passaggio 5: Configurazione degli URL interni

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedereLa voce "*\<Servizio\>* impostazioni directory virtuale" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Prima che i client possano connettersi al nuovo server tramite la rete Intranet, è necessario configurare i domini interni, o URL, sulle directory virtuali del server Accesso client, quindi configurare i record DNS privati.

È possibile scegliere se, per accedere al server Exchange, si desidera che gli utenti utilizzino lo stesso URL sulla rete Intranet e su Internet oppure URL diversi. La scelta dipende dallo schema di indirizzamento già presente o di prossima implementazione. Se si sta implementando un nuovo schema di indirizzamento, è consigliabile utilizzare lo stesso URL per gli URL interni ed esterni. L'utilizzo di uno stesso URL fa sì che gli utenti possano accedere più facilmente al server Exchange perché devono memorizzare un solo indirizzo. Indipendentemente dalla scelta fatta, è necessario configurare una zona DNS privata per lo spazio di indirizzi configurato. Per ulteriori informazioni sulla gestione delle zone DNS, vedere l'articolo su come [amministrare il server DNS](https://go.microsoft.com/fwlink/p/?linkid=190631).

Per ulteriori informazioni relative agli URL interni ed esterni sulle directory virtuali, vedere [Gestione di directory virtuali](virtual-directory-management-exchange-2013-help.md).

## Configurazione di URL interni ed esterni uguali

1.  Aprire Exchange Management Shell sul server Accesso client.

2.  Archiviare il nome host del server Accesso client in una variabile che verrà utilizzata nel passaggio successivo. Ad esempio, Ex2013CAS.
    
        $HostName = "Ex2013CAS"

3.  Utilizzare i seguenti comandi in Shell per configurare ciascun URL interno in modo che sia uguale all'URL esterno della directory virtuale.
    
        Set-EcpVirtualDirectory "$HostName\ECP (Default Web Site)" -InternalUrl ((Get-EcpVirtualDirectory "$HostName\ECP (Default Web Site)").ExternalUrl)
        
        Set-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)" -InternalUrl ((get-WebServicesVirtualDirectory "$HostName\EWS (Default Web Site)").ExternalUrl)
        
        Set-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)" -InternalUrl ((Get-ActiveSyncVirtualDirectory "$HostName\Microsoft-Server-ActiveSync (Default Web Site)").ExternalUrl)
        
        Set-OabVirtualDirectory "$HostName\OAB (Default Web Site)" -InternalUrl ((Get-OabVirtualDirectory "$HostName\OAB (Default Web Site)").ExternalUrl)
        
        Set-OwaVirtualDirectory "$HostName\OWA (Default Web Site)" -InternalUrl ((Get-OwaVirtualDirectory "$HostName\OWA (Default Web Site)").ExternalUrl)
        
        Set-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)" -InternalUrl ((Get-PowerShellVirtualDirectory "$HostName\PowerShell (Default Web Site)").ExternalUrl)

4.  Durante l'utilizzo di Shell, è possibile configurare anche la rubrica offline (OAB) per consentire all'individuazione automatica di selezionare la directory virtuale corretta per distribuire la rubrica offline. A tale scopo, eseguire i comandi riportati di seguito.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

Dopo aver configurato l'URL interno sulle directory virtuali del server Accesso client, è necessario configurare i record DNS privati per Outlook Web App e altri sistemi di connettività. In base alla configurazione, sarà necessario configurare i record DNS privati in modo che puntino all'indirizzo IP interno o esterno o al nome di dominio completo del server Accesso client. Di seguito sono riportati alcuni esempi di record DNS di cui si consiglia la creazione per abilitare la connettività dei client interni.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Tipo di record DNS</th>
<th>Valore</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
<tr class="even">
<td><p>Owa.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione dell'URL interno sulle directory virtuali del server Accesso client, procedere come segue:

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Directory virtuali**.

2.  Nel campo **Seleziona server**, selezionare il server Accesso Client con connessione a Internet.

3.  Selezionare una directory virtuale e fare clic su **Modifica** ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Verificare che nel campo **URL interno** sia presente il nome di dominio completo e il servizio corretti come indicato di seguito:
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Directory virtuale</th>
    <th>Valore URL interno</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Individuazione automatica</strong></p></td>
    <td><p>Nessun URL interno visualizzato</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://owa.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://mail.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://mail.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://mail.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://owa.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://mail.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Per verificare che i record DNS privati siano stati configurati correttamente, fare quanto segue:

1.  Aprire un prompt dei comandi ed eseguire `nslookup.exe`.

2.  Passare a un server DNS che può eseguire una query sulla zona DNS privata.

3.  In `nslookup`, controllare il record di ciascun nome di dominio completo creato. Verificare che il valore restituito per ogni nome di dominio completo sia corretto.

## Configurazione di URL interni ed esterni diversi

1.  Aprire l'interfaccia di amministrazione di Exchange accedendo all'URL del server Accesso client. Ad esempio, https://Ex2013CAS/ECP.

2.  Accedere a **Server** \> **Directory virtuali**.

3.  Nel campo **Seleziona server**, selezionare il server Accesso Client con connessione a Internet.

4.  Selezionare la directory virtuale che si desidera modificare, quindi fare clic su **Modifica** ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

5.  In **URL interno**, sostituire il nome host tra **https://** e la prima barra (**/**) con il nuovo nome di dominio completo che si desidera utilizzare. Ad esempio, se si desidera sostituire il nome di dominio completo della directory virtuale EWS Ex2013CAS.corp.contoso.com con internal.contoso.com, sostituire l'URL interno https://Ex2013CAS.corp.contoso.com/ews/exchange.asmx con https://internal.contoso.com/ews/exchange.asmx.

6.  Fare clic su **Salva**.

7.  Ripetere i passi 5 e 6 per ciascuna directory virtuale che si desidera modificare.
    

    > [!NOTE]
    > Gli URL interni delle directory virtuali di OWA e Pannello di controllo di Exchange devono essere uguali.<BR>Non è possibile impostare un URL interno per la directory virtuale di individuazione automatica.



8.  Infine, è necessario aprire Shell e configurare la rubrica offline (OAB) per consentire all'individuazione automatica di selezionare la directory virtuale corretta per distribuire la rubrica offline. A tale scopo, eseguire i comandi riportati di seguito.
    
        Get-OfflineAddressBook | Set-OfflineAddressBook -GlobalWebDistributionEnabled $True -VirtualDirectories $Null

Dopo aver configurato l'URL interno sulle directory virtuali del server Accesso client, è necessario configurare i record DNS privati per Outlook Web App e altri sistemi di connettività. In base alla configurazione, sarà necessario configurare i record DNS privati in modo che puntino all'indirizzo IP interno o esterno o al nome di dominio completo del server Accesso client. Di seguito viene fornito un esempio di un record DNS che è consigliabile creare per abilitare la connettività client interna se gli URL interni delle directory virtuali utilizzano internal.contoso.com.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>FQDN</th>
<th>Tipo di record DNS</th>
<th>Valore</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>internal.contoso.com</p></td>
<td><p>CNAME</p></td>
<td><p>Ex2013CAS.corp.contoso.com</p></td>
</tr>
</tbody>
</table>


## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta configurazione dell'URL interno sulle directory virtuali del server Accesso client, procedere come segue:

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Directory virtuali**.

2.  Nel campo **Seleziona server**, selezionare il server Accesso Client con connessione a Internet.

3.  Selezionare una directory virtuale e fare clic su **Modifica** ![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Verificare che nel campo **URL interno** sia presente il nome di dominio completo corretto. Ad esempio, potrebbe essere necessario impostare gli URL interni per l'utilizzo di internal.contoso.com.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Directory virtuale</th>
    <th>Valore URL interno</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Individuazione automatica</strong></p></td>
    <td><p>Nessun URL interno visualizzato</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ECP</strong></p></td>
    <td><p>https://internal.contoso.com/ecp</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>EWS</strong></p></td>
    <td><p>https://internal.contoso.com/EWS/Exchange.asmx</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Microsoft-Server-ActiveSync</strong></p></td>
    <td><p>https://internal.contoso.com/Microsoft-Server-ActiveSync</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>OAB</strong></p></td>
    <td><p>https://internal.contoso.com/OAB</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OWA</strong></p></td>
    <td><p>https://internal.contoso.com/owa</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>PowerShell</strong></p></td>
    <td><p>http://internal.contoso.com/PowerShell</p></td>
    </tr>
    </tbody>
    </table>


Per verificare che i record DNS privati siano stati configurati correttamente, fare quanto segue:

1.  Aprire un prompt dei comandi ed eseguire `nslookup.exe`.

2.  Passare a un server DNS che può eseguire una query sulla zona DNS privata.

3.  In `nslookup`, controllare il record di ciascun nome di dominio completo creato. Verificare che il valore restituito per ogni nome di dominio completo sia corretto.

## Passaggio 6: Configurazione di un certificato SSL

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione certificati" nell'argomento[Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

Alcuni servizi, ad esempio Outlook Anywhere ed Exchange ActiveSync, richiedono la configurazione dei certificati sul server Exchange 2013. La procedura riportata di seguito illustra come configurare un certificato SSL di un'autorità di certificazione (CA) di terze parti:

1.  Aprire l'interfaccia di amministrazione di Exchange accedendo all'URL del server Accesso client. Ad esempio, https://Ex2013CAS/ECP.

2.  Immettere nome utente e password in **Nome dominio\\utente** e **Password**, quindi fare clic su **Accedi**.

3.  Andare a **Server** \> **Certificati**. Nella pagina **Certificati**, accertarsi che il server Accesso client sia selezionato nel campo **Seleziona server**, quindi fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Nella procedura guidata **Nuovo certificato di Exchange**, selezionare **Crea la richiesta per un certificato emesso da un'autorità di certificazione**, quindi fare clic su **Avanti**.

5.  Specificare un nome per questo certificato e fare clic su **Avanti**.

6.  Se si desidera richiedere un certificato con caratteri jolly, selezionare **Richiedi un certificato con caratteri jolly** e specificare il dominio radice di tutti i sottodomini nel campo **Dominio radice**. Se non si desidera richiedere un certificato con caratteri jolly ma specificare ciascun dominio da aggiungere al certificato, lasciare vuota la pagina. Fare clic su **Avanti**.

7.  Fare clic su **Sfoglia** e specificare un server Exchange in cui archiviare il certificato. Il server selezionato deve essere il server Accesso Client con connessione a Internet. Fare clic su **Avanti**.

8.  Per ciascun servizio nell'elenco, verificare che i nomi dei server esterni o interni utilizzati dagli utenti per connettersi al server Exchange siano corretti. Esempio:
    
      - Se gli URL interni ed esterni sono uguali, **Outlook Web App (accesso da Internet)** e **Outlook Web App (accesso da Intranet)** devono entrambi indicare owa.contoso.com. **Rubrica offline (accesso da Internet)** e **Rubrica offline (accesso da Intranet)** devono entrambi indicare mail.contoso.com.
    
      - Se gli URL interni sono internal.contoso.com, **Outlook Web App (accesso da Internet)** deve indicare owa.contoso.com e **Outlook Web App (accesso da Intranet)** deve indicare internal.contoso.com.
    
    Questi domini saranno utilizzati per creare la richiesta di certificato SSL. Fare clic su **Avanti**.

9.  Aggiungere eventuali altri domini che si desidera includere nel certificato SSL.

10. Selezionare il dominio che si desidera sia il nome comune per il certificato e fare clic su **Imposta come nome comune**. Ad esempio, contoso.com. Fare clic su **Avanti**.

11. Inserire le informazioni sull'organizzazione. Queste informazioni saranno incluse nel certificato SSL. Fare clic su **Avanti**.

12. Specificare il percorso di rete in cui si desidera salvare questa richiesta di certificato. Fare clic su **Fine**.

Dopo aver salvato la richiesta di certificato, inoltrarla all'autorità di certificazione (CA). che può essere un'autorità di certificazione interna o di terze parti, in base all'organizzazione. I client che si connettono al server Accesso client devono considerare attendibile l'autorità di certificazione utilizzata. Dopo aver ricevuto il certificato dall'autorità di certificazione, completare i seguenti passaggi:

1.  Nella pagina **Server** \> **Certificati** dell'interfaccia di amministrazione di Exchange, selezionare la richiesta di certificato creata nei passaggi precedenti.

2.  Nel riquadro dei dettagli della richiesta di certificato, fare clic su **Completa** in **Stato**.

3.  Nella pagina Completa richiesta in sospeso, specificare il percorso al file del certificato SSL, quindi fare clic su **OK**.

4.  Selezionare il nuovo certificato appena creato, quindi scegliere **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

5.  Nella pagina del certificato fare clic su **Servizi**.

6.  Selezionare i servizi che si desidera assegnare a questo certificato. È necessario selezionare almeno **SMTP** e **IIS**. Fare clic su **Salva**.

7.  Se viene visualizzato l'avviso **Sovrascrivere il certificato SMTP predefinito esistente?**, fare clic su **Sì**.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che l'aggiunta di un nuovo certificato sia stata eseguita correttamente, procedere come segue:

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Server** \> **Certificati**.

2.  Selezionare il nuovo certificato e, nel riquadro dei dettagli del certificato, verificare che siano soddisfatte le seguenti condizioni:
    
      - In **Stato** viene visualizzato **Valido**
    
      - In **Assegnato ai servizi**, vengono mostrati almeno **IIS** e **SMTP**.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la configurazione del flusso di posta e dell'accesso client esterno, effettuare le seguenti operazioni:

1.  Creare un nuovo profilo in Outlook, su un dispositivo ActiveSync o in entrambi. Verificare che il nuovo profilo venga creato correttamente in Outlook o sul dispositivo mobile.

2.  In Outlook, o sul dispositivo mobile, inviare un nuovo messaggio a un destinatario esterno. Verificare che il destinatario esterno riceva il messaggio.

3.  Dalla cassetta postale del destinatario esterno, rispondere al messaggio appena inviato dalla cassetta postale di Exchange. Verificare che la cassetta postale di Exchange riceva il messaggio.

4.  Andare a https://owa.contoso.com/owa e verificare che non vi siano avvisi di certificato.

