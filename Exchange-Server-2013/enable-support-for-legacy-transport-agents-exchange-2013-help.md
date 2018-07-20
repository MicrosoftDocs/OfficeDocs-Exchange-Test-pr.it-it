---
title: 'Attivare il supporto per gli agenti di trasporto legacy: Exchange 2013 Help'
TOCTitle: Attivare il supporto per gli agenti di trasporto legacy
ms:assetid: 00617e87-7199-406e-b4a3-94378f657f1f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ591524(v=EXCHG.150)
ms:contentKeyID: 50479889
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attivare il supporto per gli agenti di trasporto legacy

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

In Microsoft Exchange Server 2013, gli agenti di trasporto che sono stati creati utilizzando Microsoft .NET Framework versione 4.0 sono supportati per impostazione predefinita. Exchange 2013 supporta gli agenti di trasporto che sono stati creati utilizzando versioni precedenti di .NET Framework, ma il supporto per questi agenti di trasporto legacy non è abilitato per impostazione predefinita. Per abilitare il supporto per gli agenti di supporto legacy, è necessario modificare il file XML di configurazione dell'applicazione appropriato. I file che è necessario modificare dipendono da dove è installato l'agente di trasporto:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Server</th>
<th>File di configurazione dell'applicazione</th>
<th>Servizio di Microsoft Windows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>server Accesso client</p></td>
<td><p>%ExchangeInstallPath%Bin\MSExchangeFrontendTransport.exe.config</p></td>
<td><p>Servizio Trasporto front-end di Microsoft Exchange (MSExchangeFrontendTransport)</p></td>
</tr>
<tr class="even">
<td><p>Server Cassette postali</p></td>
<td><ul>
<li><p>%ExchangeInstallPath%Bin\EdgeTransport.exe.config</p></li>
<li><p>%ExchangeInstallPath%Bin\MSExchangeTransport.exe.config</p></li>
</ul></td>
<td><p>Trasporto di Microsoft Exchange (MSExchangeTransport)</p></td>
</tr>
</tbody>
</table>


Il supporto per gli agenti di trasporto legacy è controllato da chiavi nei file di configurazione dell'applicazione. Per impostazione predefinita, nessuna delle chiavi richieste è presente nei file di configurazione. Sarà necessario aggiungerle manualmente. Nella seguente tabella viene illustrata dettagliatamente ciascuna chiave.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tasto</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>useLegacyV2RuntimeActivationPolicy</em></p></td>
<td><p>Questa chiave attiva o disattiva il supporto per gli agenti di trasporto legacy. I valori validi per questa chiave sono <code>true</code> o <code>false</code>. Se questa chiave non è specificata, il valore predefinito è <code>false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>supportedRuntime version</em></p></td>
<td><p>Questa chiave specifica la versione di Microsoft .NET Framework richiesta per l'agente. I valori validi per la chiave sono i seguenti:</p>
<ul>
<li><p><code>v4.0</code> oppure <code>v4.0.30319</code></p></li>
<li><p><code>v3.5</code> oppure <code>v3.5.21022</code></p></li>
<li><p><code>v3.0</code> oppure <code>v3.0.4506</code></p></li>
<li><p><code>v2.0</code> oppure <code>v2.0.50727</code></p></li>
</ul>
<p>Si specificano più valori utilizzando più istanze separate della chiave <em>supportedRuntime version</em>.</p>
<p>Quando si abilita il supporto dell'agente precedente utilizzando la chiave <em>useLegacyV2RuntimeActivationPolicy</em>, è sempre necessario specificare il valore <code>v4.0</code> oltre ai valori richiesti per l'agente di trasporto legacy.</p></td>
</tr>
</tbody>
</table>


## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Le autorizzazioni di Exchange non sono applicabili alle procedure descritte in questo argomento. Queste procedure vengono eseguite nel sistema operativo del server di Exchange.

  - Le modifiche che vengono salvate su un file di configurazione dell'applicazione vengono applicate dopo aver riavviato il servizio corrispondente.

  - Quando si riavvia uno dei servizi associati ai file di configurazione dell'applicazione, il flusso di posta sul server viene temporaneamente interrotto.

  - Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare il prompt dei comandi per configurare il supporto relativo agli agenti di trasporto legacy

Utilizzare la seguente procedura per abilitare il supporto per gli agenti di trasporto legacy:

1.  Nella finestra del prompt dei comandi, sul server di Exchange 2013 dove si desidera configurare il supporto dell'agente di trasporto legacy, aprire il file di configurazione dell'applicazione appropriato nel Blocco note utilizzando il comando seguente:
    
        Notepad %ExchangeInstallPath%Bin\<AppConfigFile>
    
    Ad esempio, per aprire il file EdgeTransport.exe.config su un server Cassette postali, utilizzare il comando seguente:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Posizionare la chiave *\</configuration\>* alla fine del file e incollare le chiavi seguenti prima della chiave *\</configuration\>*:
    
        <startup useLegacyV2RuntimeActivationPolicy="true">
           <supportedRuntime version="v4.0" />
           <supportedRuntime version="v3.5" />
           <supportedRuntime version="v3.0" />
           <supportedRuntime version="v2.0" />
        </startup>

3.  Al termine, salvare e chiudere il file di configurazione dell'applicazione.

4.  Ripetere i passaggi 1-3 per modificare gli altri file di configurazione dell'applicazione.

5.  Riavviare il servizio Windows associato eseguendo il comando riportato di seguito:
    
        net stop <service> && net start <service>
    
    Ad esempio, se il file EdgeTransport.exe.config è stato modificato, è necessario riavviare il servizio Trasporto utilizzando il comando seguente:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

6.  Ripetere il passaggio 5 per riavviare i servizi associati agli altri file di configurazione dell'applicazione modificati.

## Come verificare se l'operazione ha avuto esito positivo

Se gli agenti di trasporto legacy vengono installati correttamente questa procedura avrà avuto esito positivo. Se si tenta di installare un agente di trasporto legacy senza eseguire le procedure in questo argomento, si riceverà un messaggio di errore simile a quello riportato di seguito:

    Mixed mode assembly is built against version '<version>' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.

