---
title: 'MAPI su HTTP: Exchange 2013 Help'
TOCTitle: MAPI su HTTP
ms:assetid: 4663b5db-5b30-4a5a-a302-be6fef7fe5da
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn635177(v=EXCHG.150)
ms:contentKeyID: 61202266
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# MAPI su HTTP

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-05-10_

Il MAPI (Messaging Application Programming Interface) su HTTP è un nuovo protocollo di trasporto implementato in MicrosoftExchange Server 2013 Service Pack 1 (SP1). Il MAPI su HTTP migliora l'affidabilità e la stabilità delle connessioni Outlook e Exchange spostando il livello di trasporto su modelli HTTP standard. In questo modo si consente un livello di visibilità superiore di errori di trasporto e recuperabilità avanzata. La funzionalità aggiuntiva include supporto per una funzione esplicita Sospendi o Riprendi. In questo modo si abilitano i client supportati a modificare le reti o a riprendere dalla sospensione durante il mantenimento delle stesso contesto di server.

L'implementazione del MAPI su HTTP non indica che si tratti dell'unico protocollo utilizzabile da Outlook per accedere a Exchange. I client Outlook che non dispongono della capacità di eseguire MAPI su HTTP possono comunque utilizzare Outlook via Internet (RPC su HTTP) per accedere a Exchange tramite server Accesso client abilitato per MAPI.

## Vantaggi di MAPI su HTTP

MAPI su HTTP offre i seguenti vantaggi per i client da cui è supportato:

  - Abilita future innovazioni nell'autenticazione utilizzando il protocollo basato su HTTP.

  - Fornisce tempi di riconnessione più veloci dopo un'interruzione di comunicazione perché solo le connessioni TCP (non connessioni RPC) devono essere ricostruite. Di seguito sono riportati alcuni esempi di un'interruzione di comunicazione:
    
      - Sospensione del dispositivo
    
      - Il passaggio da rete cablata a rete senza fili o cellulare

  - Offre un contesto di sessione non dipendente dalla connessione. Il server mantiene il contesto di sessione per un periodo di tempo configurabile, anche se l'utente cambia rete.

## Distribuzione di MAPI su HTTP

Considerare i requisiti seguenti per attivare MAPI su HTTP.

  - **Supportabilità** Verificare che siano supportate le versioni di configurazione desiderata.

  - **Prerequisiti** Verificare che l'ambiente sia stato aggiornato e preparato per MAPI su HTTP.

  - **Configurazione** Configurare le directory virtuali e attivare MAPI per l'organizzazione.

## Supporto

Utilizzare la matrice seguente per verificare che i client e i server supportino l'interfaccia MAPI su HTTP.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Prodotto</th>
<th>Exchange 2013 SP1</th>
<th>Exchange 2013 RTM</th>
<th>Exchange 2010 SP3</th>
<th>Exchange 2007 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 SP1</p></td>
<td><ul>
<li><p>MAPI su HTTP</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
<td><p>Outlook via Internet</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2013 RTM</p></td>
<td><p>Outlook via Internet</p></td>
<td><p>Outlook via Internet</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2010 SP2 e aggiornamenti KB2956191 e KB2965295 (14 aprile 2015)</p></td>
<td><ul>
<li><p>MAPI su HTTP<span></span></p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
<td><p>Outlook via Internet</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2010 SP2 e versioni precedenti</p></td>
<td><p>Outlook via Internet</p></td>
<td><p>Outlook via Internet</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Outlook via Internet</p></td>
<td><p>Outlook via Internet</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook via Internet</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Prerequisiti

Completare la procedura seguente per preparare client e server per il supporto MAPI su HTTP.

1.  Aggiornare i client Outlook a Outlook 2013 SP1 o Outlook 2010 SP2 e agli aggiornamenti KB2956191 e KB2965295 (14 aprile 2015).

2.  Aggiornare i server Accesso Client e cassette postali a Exchange 2013 SP1. Per informazioni sull'aggiornamento, vedere [Upgrade di Exchange 2013 all'aggiornamento cumulativo o Service Pack più recente](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md).
    

    > [!NOTE]
    > Tutti i server Accesso client devono essere aggiornati a Exchange 2013 SP1 prima di abilitare MAPI su HTTP. In caso contrario, Outlook potrebbe non riuscire a connettersi alle cassette postali.<BR>Il mancato aggiornamento dei server cassette postali in un Gruppo disponibilità database può causare ritardi nella posta elettronica e una richiesta da parte del client di riavviare Outlook in caso di failover del database.



3.  In tutti i server Exchange 2013, è necessario installare Microsoft.NET Framework 4.5.2. Per ulteriori informazioni, vedere [installazione di .NET Framework](https://go.microsoft.com/fwlink/p/?linkid=518380).

4.  In tutti i server Accesso client di Exchange 2013 SP1, aggiungere la variabile dell'ambiente Windows **COMPLUS\_DisableRetStructPinning** attraverso la seguente procedura.
    
    1.  In una finestra del prompt dei comandi, eseguire `systempropertiesadvanced` e fare clic su **Variabili d'ambiente**.
    
    2.  Nella sezione **Variabili di sistema**, fare clic su **Nuova** e inserire le seguenti informazioni.
        
          - **Nome della variabile** `COMPLUS_DisableRetStructPinning`
        
          - **Valore della variabile**   1
    
    3.  Al termine, fare clic sul pulsante **OK**.

## Configurazione

Completare la procedura seguente per configurare MAPI su HTTP per l'organizzazione.

1.  **Configurazione della directory virtuale**   Per impostazione predefinita, Exchange 2013 SP1 crea una directory virtuale per MAPI su HTTP. È possibile utilizzare il cmdlet **Set-MapiVirtualDirectory** per configurare la directory virtuale. È necessario configurare un URL interno, un URL esterno o entrambi. Per ulteriori informazioni, vedere [Set-MapiVirtualDirectory](https://technet.microsoft.com/it-it/library/dn595082\(v=exchg.150\)).
    
    Ad esempio, per configurare la directory virtuale MAPI predefinita sul server Exchange locale impostando un valore URL interno su https://contoso.com/mapi e il metodo di autenticazione su `Negotiate`, eseguire il seguente comando:
    
        Set-MapiVirtualDirectory -Identity "Contoso\mapi (Default Web Site)" -InternalUrl https://Contoso.com/mapi -IISAuthenticationMethods Negotiate

2.  **Configurazione certificato**   Il certificato digitale utilizzato dall'ambiente Exchange deve includere gli stessi valori *InternalURL* e *ExternalURL* definiti sulla directory virtuale MAPI. Per ulteriori informazioni sulla gestione certificati Exchange 2013, vedere [Certificati digitali e SSL](digital-certificates-and-ssl-exchange-2013-help.md). Assicurarsi che il certificato Exchange sia affidabile sulla workstation client Outlook e che non vi siano errori del certificato, in particolar modo quando si accede agli URL configurati sulla directory virtuale MAPI.

3.  **Aggiornamento regole server**   Verificare che i bilanciamenti del carico, i proxy inversi e i firewall siano configurati per consentire l'accesso a MAPI su directory virtuale HTTP.

4.  **Attivare MAPI su HTTP nell'organizzazione di Exchange**
    
    Eseguire il comando indicato di seguito:
    
        Set-OrganizationConfig -MapiHttpEnabled $true

## Verificare MAPI su connessioni HTTP

È possibile testare l'interfaccia MAPI end-to-end tramite connessione HTTP utilizzando il cmdlet **Test-OutlookConnectivity**. Per utilizzare il cmdlet **Test-OutlookConnectivity**, deve essere avviato il servizio Microsoft Exchange Health Manager (MSExchangeHM).

L'esempio seguente prova l'interfaccia MAPI su connessione HTTP dal server di Exchange denominato ContosoMail.

    Test-OutlookConnectivity -RunFromServerId ContosoMail -ProbeIdentity OutlookMapiHttpSelfTestProbe

Un test riuscito restituisce un output simile all'esempio seguente:

    MonitorIdentity                                          StartTime              EndTime                Result      Error     Exception
    ---------------                                          ---------              -------                ------      -----     ---------
    OutlookMapiHttp.Protocol\OutlookMapiHttpSelfTestProbe    2/14/2014 7:15:00 AM   2/14/2014 7:15:10 AM   Succeeded

Per ulteriori informazioni, vedere [Test-OutlookConnectivity](https://technet.microsoft.com/it-it/library/dd638082\(v=exchg.150\)).

I registri per MAPI su attività HTTP si trovano nelle posizioni seguenti:

  - %ExchangeInstallPath%Logging\\MAPI Address Book Service\\

  - %ExchangeInstallPath%Logging\\MAPI Client Access\\

  - %ExchangeInstallPath%Logging\\HttpProxy\\Mapi\\

## Gestire MAPI su HTTP

È possibile gestire la configurazione di MAPI su HTTP utilizzando i cmdlet seguenti:

  - [Set-MapiVirtualDirectory](https://technet.microsoft.com/it-it/library/dn595082\(v=exchg.150\))

  - [Get-MapiVirtualDirectory](https://technet.microsoft.com/it-it/library/dn595080\(v=exchg.150\))

  - [New-MapiVirtualDirectory](https://technet.microsoft.com/it-it/library/dn595081\(v=exchg.150\))

  - [Remove-MapiVirtualDirectory](https://technet.microsoft.com/it-it/library/dn595083\(v=exchg.150\))

