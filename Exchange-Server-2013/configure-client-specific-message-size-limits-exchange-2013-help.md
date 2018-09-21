---
title: 'Configura dimensione max messaggi specifici del client: Exchange 2013 Help'
TOCTitle: Configurare la dimensione massima dei messaggi specifici del client
ms:assetid: fef9ca78-b68f-4342-ada0-881ab985ce3c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh529949(v=EXCHG.150)
ms:contentKeyID: 52063141
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la dimensione massima dei messaggi specifici del client

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-01-26_

In Microsoft Exchange Server 2013, esistono diversi limiti per le dimensioni dei messaggi che si applicano ai messaggi in transito nell'organizzazione Exchange. Per ulteriori informazioni, vedere [Limiti di dimensione dei messaggi](message-size-limits-exchange-2013-help.md).

Tuttavia, non esistono limiti della dimensione dei messaggi specifici del client che è possibile configurare per i client di posta elettronica e Outlook Web App che utilizzano ActiveSync o Servizi Web Exchange (EWS). Se si modificano i limiti di dimensione dei messaggi a livello di organizzazione di Exchange, è necessario verificare che la dimensione del messaggio i limiti per Outlook Web App, ActiveSync e servizi Web Exchange siano impostati di conseguenza. Configurare i valori nei file Web. config nei server Accesso Client e server cassette postali. Questi limiti sono descritte nelle tabelle seguenti.

### ActiveSync

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo del server</th>
<th>File di configurazione</th>
<th>Chiavi e valori predefiniti</th>
<th>Dimensioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accesso client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   Non è presente per impostazione predefinita (vedere commenti).</p></td>
<td><p>byte</p></td>
</tr>
<tr class="even">
<td><p>Accesso client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>KB</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;30000000 bytes&quot;</code>   Non è presente per impostazione predefinita (vedere commenti).</p></td>
<td><p>byte</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;10240&quot;</code></p></td>
<td><p>KB</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Sync\web.config</code></p></td>
<td><p><code>&lt;add key=&quot;MaxDocumentDataSize&quot; value=&quot;10240000&quot;&gt;</code></p></td>
<td><p>byte</p></td>
</tr>
</tbody>
</table>


**Commenti ActiveSync limiti**

Per impostazione predefinita, non esiste alcuna chiave *maxAllowedContentLength* nei file di `web.config` per ActiveSync. La dimensione massima dei messaggi per ActiveSync dipende dal valore **maxAllowedContentLength** applicato a tutti i siti web nel server. Il valore predefinito è 30000000 byte (30 MB). Per visualizzare i valori per ActiveSync sul server Accesso Client e server di cassette postali in Gestione IIS, procedere come segue:

1.  Effettuare una delle procedure seguenti:
    
      - Nel server Accesso Client, aprire **Gestione IIS**, accedere a **siti** \> **Default Web Site** e selezionare **Microsoft-Server-ActiveSync**.
    
      - Sui server cassette postali, aprire **Gestione IIS**, accedere a **siti** \> **Exchange Back-End** e selezionare **Microsoft-Server-ActiveSync**.

2.  Verificare la **Funzionalità di visualizzazione** sia selezionata e fare doppio clic su **Editor di configurazione** nella sezione **Gestione**.

3.  Fare clic sulla freccia a discesa nel campo di **sezione**, passare a **System. webServer** \> **sicurezza** e selezionare **requestFiltering**.

4.  Nei risultati di espandere **requestLimits** e verrà visualizzato **maxAllowedContentLength** e il valore predefinito 30000000 (byte).

Per modificare il valore **maxAllowedContentLength** , immettere un nuovo valore in byte e fare clic su **Applica**. È necessario modificare il valore sui server Accesso Client e sui server cassette postali. Dopo aver modificato il valore in Gestione IIS, una nuova chiave *maxAllowedContentLength* viene scritto il file `web.config` corrispondente (`%ExchangeInstallPath%FrontEnd\HttpProxy\Sync\web.config` sui server Accesso Client) e `%ExchangeInstallPath%ClientAccess\Sync\web.config` sui server cassette postali.

Per modificare la dimensione massima dei messaggi per i client ActiveSync, è necessario modificare il valore di *maxRequestLength* nel file `web.config` sul server Accesso Client e server cassette postali, *MaxDocumentDataSize* nel file `web.config` sui server cassette postali e *maxAllowedContentLength* in Gestione IIS sul server Accesso Client e server cassette postali.

### Servizi Web Exchange

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Gestire ruoli</th>
<th>File di configurazione</th>
<th>Chiavi e valori predefiniti</th>
<th>Dimensioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accesso client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>byte</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;67108864&quot;</code></p></td>
<td><p>byte</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\exchweb\ews\web.config</code></p></td>
<td><p>14 istanze di <code>maxReceivedMessageSize=&quot;67108864&quot;</code></p></td>
<td><p>byte</p></td>
</tr>
</tbody>
</table>


**Commenti relativi ai limiti di servizi Web Exchange**

  - Esistono 14 istanze separate del valore `maxReceivedMessageSize="67108864"` che corrispondono alle diverse combinazioni di scelta rapida (http e https) e i metodi di autenticazione.

  - Per modificare la dimensione massima dei messaggi per i client di servizi Web Exchange, è necessario modificare il valore di *maxAllowedContentLength* in `web.config` file e tutte le 14 occorrenze `maxReceivedMessageSize="67108864"` nel file `web.config` sui server cassette postali.

  - Nel file `web.config` sui server cassette postali, esistono inoltre due istanze del valore più `maxReceivedMessageSize="1048576"` per le associazioni **UMLegacyMessageEncoderSoap11Element** non è necessario modificare.

  - *maxRequestLength* è un'impostazione di ASP.NET in entrambi i file Web. config, ma non viene utilizzata dai servizi Web Exchange, in modo che non è necessario modificarla.

### Outlook Web App

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ruolo del server</th>
<th>File di configurazione</th>
<th>Chiavi e valori predefiniti</th>
<th>Dimensioni</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accesso client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>byte</p></td>
</tr>
<tr class="even">
<td><p>Accesso client</p></td>
<td><p><code>%ExchangeInstallPath%FrontEnd\HttpProxy\owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>KB</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxAllowedContentLength=&quot;35000000&quot;</code></p></td>
<td><p>byte</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p><code>maxRequestLength=&quot;35000&quot;</code></p></td>
<td><p>KB</p></td>
</tr>
<tr class="odd">
<td><p>Cassetta postale</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 istanze di <code>maxReceivedMessageSize=&quot;35000000&quot;</code></p></td>
<td><p>byte</p></td>
</tr>
<tr class="even">
<td><p>Cassetta postale</p></td>
<td><p><code>%ExchangeInstallPath%ClientAccess\Owa\web.config</code></p></td>
<td><p>2 istanze di <code>maxStringContentLength=&quot;35000000&quot;</code></p></td>
<td><p>byte</p></td>
</tr>
</tbody>
</table>


**Commenti Outlook Web App limiti**

  - Nel file `web.config` sui server cassette postali, esistono due istanze separate del valori `maxReceivedMessageSize="35000000"` e `maxStringContentLength="35000000"` corrispondenti ai binding http e https.

  - Per modificare la dimensione massima dei messaggi per i client Outlook Web App, è necessario modificare tutti i valori in entrambi i file, incluse le istanze di *maxReceivedMessageSize* e *maxStringContentLength* nel file `web.config` sui server cassette postali.

  - Nel file `web.config` sui server cassette postali, è inoltre disponibile un'istanza del valore `maxStringContentLength="102400"` per l'associazione **MsOnlineShellService** che non è necessario modificare.

Per tutti i limiti di dimensione dei messaggi, è necessario impostare valori maggiori delle dimensioni effettive da applicare. In tal modo si tiene conto dell'inevitabile aumento dei messaggi nel caso di codifica Base64 degli allegati o altri dati binari. La codifica Base64 causa un aumento di circa 33% della dimensione del messaggio, pertanto i valori specificati per i limiti dei messaggi devono essere circa il 33% più grandi della dimensione massima utilizzabile effettiva. Ad esempio, se si specifica un valore massimo di 64 MB, la dimensione massima realistica del messaggio sarà di circa 48 MB.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Le autorizzazioni di Exchange non sono applicabili alle procedure descritte in questo argomento. Queste procedure vengono eseguite nel sistema operativo del server di Exchange.

  - Le modifiche salvate nel file di configurazione Web.config vengono applicate dopo il riavvio di IIS.

  - Per consentire l'aumento del 33% della dimensione causato dalla codifica Base64, moltiplicare il nuovo valore di dimensione massimo in megabyte per 4/3. Per convertite il valore in kilobyte, moltiplicare per 1024. Per convertire il valore in byte, moltiplicare per 1048756 (1024\*1024). Tenere presente che l'aumento delle dimensioni causato dalla codifica Base64 potrebbe superare il 33%, e seconda di diversi fattori quali la dimensione, il tipo e la compressione dei file allegati e il client di posta elettronica utilizzato per inviare il messaggio.

  - Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzare il blocco note per configurare una dimensione massima dei messaggi specifici del client

1.  Aprire i file Web. config appropriati nel blocco note. Ad esempio, per aprire i file Web. config per i client Servizi Web Exchange, eseguire i comandi seguenti:
    
        Notepad %ExchangeInstallPath%ClientAccess\exchweb\ews\web.config
        Notepad %ExchangeInstallPath%FrontEnd\HttpProxy\ews\web.config

2.  Trovare i tasti pertinenti nei file Web. config appropriati, come descritto nelle tabelle in precedenza nell'argomento. Ad esempio, per i client Servizi Web Exchange, trovare la chiave *maxAllowedContentLength* nel file e tutte le 14 occorrenze il valore `maxReceivedMessageSize="67108864"` nel file `web.config` sui server cassette postali.
    
        <requestLimits maxAllowedContentLength="67108864" />
        ...maxReceivedMessageSize="67108864"...
    
    Ad esempio, per consentire una dimensione dei messaggi massima con codifica Base64 di circa 64 MB, modificare tutte le istanze di `67108864` in `89478486` (64\*4/3\*1048756):
    
        <requestLimits maxAllowedContentLength="89478486" />
        ...maxReceivedMessageSize="89478486"...

3.  Al termine, salvare e chiudere i file Web. config.

4.  Riavviare IIS utilizzando il seguente comando:
    
    ```powershell
IISReset /noforce
```

## Configurare la dimensione massima dei messaggi specifici del client dalla riga di comando

Anziché utilizzare il blocco note, è inoltre possibile configurare la dimensione massima dei messaggi specifici del client dalla riga di comando. Aprire un prompt dei comandi con privilegi elevati sul server Exchange (una finestra del Prompt aprire selezionare **Esegui come amministratore** ) ed eseguire comandi appropriati per i limiti di cui si desidera configurare.

**Note**:

  - I valori di dimensione nei comandi sono i valori predefiniti, pertanto sarà necessario per modificarli.

  - Prestare attenzione alla indica se il valore in byte o kilobyte.

**ActiveSync**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:30000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:system.web/httpRuntime /maxRequestLength:10240
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/Microsoft-Server-ActiveSync/" -section:appSettings /[key='MaxDocumentDataSize'].value:10240000

**Servizi Web Exchange**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSAnonymousHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSBasicHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSNegotiateHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecuritySymmetricKeyHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpsBinding'].httpsTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /customBinding.[name='EWSWSSecurityX509CertHttpBinding'].httpTransport.maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpsBinding'].maxReceivedMessageSize:67108864
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/ews/" -section:system.serviceModel/bindings /webHttpBinding.[name='EWSStreamingNegotiateHttpBinding'].maxReceivedMessageSize:67108864

**Outlook Web App**

    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Default Web Site/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.webServer/security/requestFiltering /requestLimits.maxAllowedContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.web/httpRuntime /maxRequestLength:35000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].maxReceivedMessageSize:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpsBinding'].readerQuotas.maxStringContentLength:35000000
    %windir%\system32\inetsrv\appcmd.exe set config "Exchange Back End/owa/" -section:system.serviceModel/bindings /webHttpBinding.[name='httpBinding'].readerQuotas.maxStringContentLength:35000000

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente configurato la dimensione massima dei messaggi specifici del client, è necessario inviare un messaggio di prova a e da una cassetta postale di cui si accede dal client interessati. È possibile provare gli allegati di dimensioni inferiori alcuni o uno degli allegati di grandi dimensioni in modo che i messaggi di prova vengono 33% circa rispetto al valore che è stato configurato. Ad esempio, un valore configurato MB 85 determina una dimensione massima dei messaggi realistico di circa 64 MB.

