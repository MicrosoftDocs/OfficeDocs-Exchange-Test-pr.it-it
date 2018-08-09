---
title: 'Abilita endpoint del Proxy MRS per spostamenti remoti: Exchange 2013 Help'
TOCTitle: Abilitare l'endpoint del Proxy MRS per gli spostamenti remoti
ms:assetid: 9840f712-127e-4c2d-bfe5-1b35cdb2a31b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn155787(v=EXCHG.150)
ms:contentKeyID: 54652878
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare l'endpoint del Proxy MRS per gli spostamenti remoti

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-07-02_

Il proxy del servizio di replica delle cassette postali (proxy MRS) facilita gli spostamenti di cassette postali tra foreste e le migrazioni di spostamento remote tra l'organizzazione Exchange in locale ed Exchange Online. In Exchange 2013 il proxy MRS è incluso nel ruolo del server Cassette postali (anche noto come *Server Cassette postali*). Durante le migrazioni e gli spostamenti remoti tra le foreste, un server Accesso client agisce come proxy per le richieste di spostamento in arrivo per il server Cassette postali. La capacità del server Accesso client di accettare queste richieste, per impostazione predefinita, è disabilitata. Per consentire al server Accesso client di accettare le richieste di spostamento in arrivo, è necessario abilitare l'endpoint del proxy MRS.

Il server Accesso client su cui abilitare l'endpoint del proxy MRS dipende dal tipo e dalla direzione di spostamento della cassetta postale.

  - **Spostamenti aziendali tra foreste**   Per gli spostamenti tra foreste iniziati dall'ambiente di destinazione (noti come tipo di spostamento *pull*), è necessario abilitare l'endpoint del proxy MRS sui server Accesso client nell'ambiente di origine. Per gli spostamenti tra foreste iniziati dall'ambiente di origine (noti come tipo di spostamento *push*), è necessario abilitare l'endpoint del proxy MRS sui server Accesso client nell'ambiente di destinazione.

  - **Migrazioni di spostamento remote tra l'organizzazione Exchange e Exchange Online** locali   Per le migrazioni di spostamento remote on-boarding e off-boarding, è necessario abilitare l'endpoint del proxy MRS sui server Accesso client nell'organizzazione locale.


> [!NOTE]
> Se si utilizza EAC per spostare le cassette postali, le migrazioni di spostamenti remote on-boarding e tra foreste sono di tipo pull, perché la richiesta è iniziata dall'ambiente di destinazione. Le migrazioni di spostamento remote off-boarding sono di tipo push, perché la richiesta è iniziata dall'ambiente di origine.



## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti per ogni server.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni per Servizi Web di Exchange" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Se è stato distribuito più di un server Accesso client nell'organizzazione Exchange, è necessario abilitare l'endpoint del proxy MRS su ciascuno di essi. Se si aggiungono ulteriori server Accesso client, assicurarsi di abilitare l'endpoint del proxy MRS sui nuovi server. Gli spostamenti tra foreste e le migrazioni di spostamento remote potrebbero non riuscire se l'endpoint del proxy MRS non è abilitato su tutti i server Accesso client.

  - Se non vengono eseguiti spostamenti tra foreste o migrazioni di spostamento remote, mantenere l'endpoint del proxy MRS disabilitato per ridurre la superficie soggetta ad attacchi dell'organizzazione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Utilizzare EAC per abilitare l'endpoint del proxy MRS

1.  In EAC, accedere a **Destinatari** \> **Server** \> **Directory virtuali**.

2.  Nell'elenco a discesa **Seleziona server**, selezionare il nome del server Accesso client su cui abilitare l'endpoint del proxy MRS. Oppure selezionare **Tutti i server** per visualizzare le directory virtuali su tutti i server Accesso client nell'organizzazione.

3.  Nell'elenco a discesa **Seleziona tipo**, selezionare **EWS** per visualizzare la directory virtuale di Exchange Web Service (EWS) per il server selezionato.

4.  Nell'elenco delle directory virtuali, fare clic su **EWS (Sito Web predefinito)** per il server Accesso client da configurare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

5.  Nella pagina proprietà **EWS (sito Web predefinito)**, selezionare la casella di controllo **Abilita Proxy MRS endpoint** e quindi fare clic su **Salva**.

## Utilizzare Shell per abilitare l'endpoint del proxy MRS

Il comando seguente consente di abilitare l'endpoint del proxy MRS su un server Accesso client denominato EXCH-SRV-01.

    Set-WebServicesVirtualDirectory -Identity "EXCH-SRV-01\EWS (Default Web Site)" -MRSProxyEnabled $true

Il comando seguente consente di abilitare l'endpoint del proxy MRS su un server Accesso client nell'organizzazione Exchange.

    Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -MRSProxyEnabled $true


> [!IMPORTANT]
> Come precedentemente affermato, l'endpoint del proxy MRS deve essere abilitato su tutti i server Accesso client nell'organizzazione. Eseguire il comando precedente dopo aver aggiunto un nuovo server Accesso client all'organizzazione.



## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta abilitazione dell'endpoint del proxy MRS, effettuare una delle seguenti operazioni:

1.  In EAC, accedere a **Destinatari** \> **Server** \> **Directory virtuali**.

2.  Nell'elenco delle directory virtuali, fare clic su **EWS (Sito Web predefinito)** e verificare nel riquadro dei dettagli che l'endpoint del proxy MRS sia abilitato.
    
    In alternativa, è possibile fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare la pagina delle proprietà **EWS (sito Web predefinito)** e verificare che sia selezionata la casella di controllo **Abilita Proxy MRS endpoint**.

Oppure

Eseguire il comando riportato di seguito in Shell:

    Get-WebServicesVirtualDirectory | FL Identity,MRSProxyEnabled

Verificare che il parametro *MRSProxyEnabled* sia impostato su `True`.

Un altro modo per verificare che l'endpoint del proxy MRS sia abilitato è quello di utilizzare il cmdlet **Test-MigrationServerAvailability** per verificare la capacità di comunicare con il server remoto che ospita le cassette postali da spostare, oppure nel caso di cassette postali Exchange Online off-boarding nell'organizzazione locale, un server nell'organizzazione locale. Per ulteriori informazioni, vedere [Test-MigrationServerAvailability](https://technet.microsoft.com/it-it/library/jj219169\(v=exchg.150\)).

Nell'esempio seguente viene verificata la connessione a un server nella foresta corp.contoso.com.
```
$Credentials = Get-Credential
```
```
Test-MigrationServerAvailability -ExchangeRemoteMove -Autodiscover -EmailAddress administrator@corp.contoso.com -Credentials $Credentials
```
Per eseguire correttamente il comando, l'endpoint del proxy MRS deve essere abilitato.

