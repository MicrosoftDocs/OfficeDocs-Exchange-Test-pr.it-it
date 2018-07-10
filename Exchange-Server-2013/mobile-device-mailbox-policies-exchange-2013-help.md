---
title: 'Criteri cassetta postale di dispositivo mobile: Exchange 2013 Help'
TOCTitle: Criteri cassetta postale di dispositivo mobile
ms:assetid: 9317b3bc-44a1-4e54-bc51-4f0b194b6a55
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123783(v=EXCHG.150)
ms:contentKeyID: 50481215
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criteri cassetta postale di dispositivo mobile

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-06-16_

In MicrosoftExchange Server 2013, è possibile creare criteri cassetta postale dei dispositivi mobili per applicare un insieme comune di criteri o impostazioni di protezione a una raccolta di utenti. Dopo aver distribuito Exchange ActiveSync nell'organizzazione di Exchange 2013, è possibile creare nuovi criteri cassetta postale dei dispositivi mobili oppure modificare quelli esistenti. All'installazione di Exchange 2013 viene creato un criterio cassetta postale dei dispositivi mobili predefinito. Questo criterio cassetta postale dei dispositivi mobili predefinito viene assegnato automaticamente a tutti gli utenti.


> [!IMPORTANT]
> I telefoni cellulari con Windows Phone 7 supportano solo un sottoinsieme di tutte le impostazioni dei criteri cassetta postale di Exchange ActiveSync. Per l'elenco completo, vedere Windows Phone 7 Synchronization.




> [!WARNING]
> Il lettore di impronte digitali iOS7 non è supportato come una password per il dispositivo. Se si abilita il lettore di impronte digitali per proteggere il dispositivo iOS7, sarà necessario creare e immettere una password qualora i criteri della cassetta postale del dispositivo mobile richiedano una password.



## Informazioni generali sui criteri cassetta postale dei dispositivi mobili

È possibile utilizzare i criteri cassetta postale dei dispositivi mobili per gestire molte impostazioni differenti. Ad esempio:

  - Richiesta di una password

  - Definizione della lunghezza minima per la password

  - Richiesta di un numero o di un carattere speciale all'interno della password

  - Impostazione del tempo di inattività di un dispositivo prima che venga richiesto all'utente di immettere nuovamente una password

  - Cancellazione di un dispositivo dopo un determinato numero di tentativi di immissione della password non riusciti

Per ulteriori informazioni sulle impostazioni configurabili, vedere Impostazioni dei criteri dei dispositivi mobili.

## Gestione dei criteri cassetta postale di Exchange ActiveSync

I criteri cassetta postale dei dispositivi mobili possono essere creati in Interfaccia di amministrazione di Exchange (EAC) o in Exchange Management Shell. Se si crea un criterio in EAC, è possibile configurare solo un sottoinsieme delle impostazioni disponibili. È possibile configurare le impostazioni restanti con Shell.

## Sincronizzazione di Windows Phone 7

Se nell'organizzazione sono presenti telefoni cellulari con Windows Phone 7 per questi telefoni si potrebbero verificare problemi di sincronizzazione se sono configurate alcune impostazioni dei criteri cassetta postale di Exchange ActiveSync. Per consentire ai telefoni cellulari con Windows Phone 7 di sincronizzarsi con una cassetta postale Exchange impostare la proprietà **AllowNonProvisionableDevices** su True o configurare solo i seguenti criteri cassetta postale di Exchange ActiveSync:

  - AllowSimplePassword

  - BlockInternetSharing

  - BlockRemoteDesktop

  - DisableDesktopSync

  - DisableIrDA

  - DisableRemovableStorage

  - DeviceWipeThreshold

  - MinPasswordLength

  - IdleTimeoutFrequencyValue

  - PasswordExpiration

  - PasswordHistory

  - PasswordRequired

## Impostazioni dei criteri cassetta postale per i dispositivi mobili

Nella tabella seguente sono riepilogate le impostazioni che è possibile specificare utilizzando i criteri cassetta postale dei dispositivi mobili.

### Impostazioni dei criteri cassetta postale dei dispositivi mobili

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Impostazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Consenti Bluetooth</p></td>
<td><p>Questa impostazione consente di specificare se un dispositivo mobile permette di eseguire connessioni Bluetooth. Le opzioni disponibili sono Disabilita, Solo mani libere e Consenti. Il valore predefinito è Consenti. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="even">
<td><p>Consenti browser</p></td>
<td><p>Questa impostazione consente di specificare se Pocket Internet Explorer è consentito sul dispositivo mobile. Questa impostazione non influisce sui browser di terze parti installati sul dispositivo mobile. Il valore predefinito è <code>$true</code>. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti fotocamera</p></td>
<td><p>Questa impostazione consente di specificare se è possibile utilizzare la fotocamera del dispositivo mobile. Il valore predefinito è <code>$true</code>. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="even">
<td><p>Consenti posta consumer</p></td>
<td><p>Specifica se l'utente di dispositivo mobile può configurare un account di posta elettronica personale (POP3 o IMAP4) sul dispositivo mobile. Il valore predefinito è <code>$true</code>. Questa impostazione non controllare l'accesso agli account di posta elettronica che utilizzano programmi di posta elettronica di terze parti di dispositivo mobile. Per modificare i valori di questa impostazione, è necessario la licenza di accesso Client di Exchange Enterprise.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti sincronizzazione desktop</p></td>
<td><p>Questa impostazione consente di specificare se il dispositivo mobile può essere sincronizzato con un PC tramite cavo, connessione Bluetooth o IrDA. Il valore predefinito è <code>$true</code>. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="even">
<td><p>Consenti gestione dispositivo esterno</p></td>
<td><p>Questa impostazione consente di specificare se un programma di gestione dei dispositivi esterni può gestire il dispositivo mobile.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti posta HTML</p></td>
<td><p>Questa impostazione consente di specificare se i messaggi di posta elettronica sincronizzati con il dispositivo mobile possono essere in formato HTML. Se è impostata su <code>$false</code>, tutti i messaggi di posta elettronica vengono convertiti in testo normale.</p></td>
</tr>
<tr class="even">
<td><p>Consenti condivisione Internet</p></td>
<td><p>Questa impostazione consente di specificare se il dispositivo mobile può essere utilizzato come modem per un computer desktop o portatile. Il valore predefinito è <code>$true</code>. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="odd">
<td><p>AllowIrDA</p></td>
<td><p>Questa impostazione consente di specificare se le connessioni a infrarossi sono consentite sul dispositivo mobile. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="even">
<td><p>Consenti aggiornamento OTA mobile</p></td>
<td><p>Questa impostazione consente di specificare se le impostazioni dei criteri cassetta postale dei dispositivi mobili possono essere inviate al dispositivo mobile su una connessione dati cellulare. Il valore predefinito è <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti dispositivi senza provisioning</p></td>
<td><p>Questa impostazione consente di specificare se i dispositivi mobili che potrebbero non supportare applicazione tutte le impostazioni dei criteri sono autorizzati a connettersi a Exchange 2013 utilizzando Exchange ActiveSync. Che consente di dispositivi mobili senza provisioning implicazioni di sicurezza. Ad esempio, alcuni dispositivi senza provisioning potrebbero non essere in grado di implementare i requisiti di password dell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p>Consenti POPIMAPEmail</p></td>
<td><p>Questa impostazione consente di specificare se l'utente può configurare un POP3 o con un account di posta elettronica IMAP4 sul dispositivo mobile. Il valore predefinito è <code>$true</code>. Questa impostazione non controllare l'accesso tramite programmi di posta elettronica di terze parti.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti desktop remoto</p></td>
<td><p>Questa impostazione consente di specificare se il dispositivo mobile può avviare una connessione desktop remoto. Il valore predefinito è <code>$true</code>. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="even">
<td><p>Consenti password semplice</p></td>
<td><p>Questa impostazione consente di abilitare o disabilitare l'utilizzo di una password semplice come 1111 o 1234. Il valore predefinito è <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti negoziazione algoritmo di crittografia S/MIME</p></td>
<td><p>Questa impostazione consente di specificare se l'applicazione di messaggistica sul dispositivo mobile può negoziare l'algoritmo di crittografia se il certificato del destinatario non supporti l'algoritmo di crittografia specificato.</p></td>
</tr>
<tr class="even">
<td><p>Consenti certificati software S/MIME</p></td>
<td><p>Questa impostazione consente di specificare se i certificati software S/MIME sono consentiti o meno sul dispositivo mobile.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti scheda di memoria</p></td>
<td><p>Questa impostazione consente di specificare se il dispositivo mobile può accedere alle informazioni archiviate su una scheda di memoria. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="even">
<td><p>Consenti invio messaggi di testo</p></td>
<td><p>Questa impostazione consente di specificare se è consentito inviare messaggi di testo dal dispositivo mobile. Il valore predefinito è <code>$true</code>. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti applicazioni non firmate</p></td>
<td><p>Questa impostazione consente di specificare se è possibile installare applicazioni non firmate sul dispositivo mobile. Il valore predefinito è <code>$true</code>. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="even">
<td><p>Consenti pacchetti di installazione non firmati</p></td>
<td><p>Questa impostazione consente di specificare se è possibile eseguire un pacchetto di installazione non firmato sul dispositivo mobile. Il valore predefinito è <code>$true</code>. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="odd">
<td><p>Consenti Wi-Fi</p></td>
<td><p>Questa impostazione consente di specificare se l'accesso Internet wireless è consentito sul dispositivo mobile. Il valore predefinito è <code>$true</code>. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="even">
<td><p>Password alfanumerica obbligatoria</p></td>
<td><p>Questa impostazione richiede una password con caratteri numerici e non numerici. Il valore predefinito è <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Elenco applicazioni approvate</p></td>
<td><p>Questa impostazione consente di archiviare un elenco di applicazioni approvate che è possibile eseguire sul dispositivo mobile. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
<tr class="even">
<td><p>Allegati abilitati</p></td>
<td><p>Questa impostazione consente di abilitare il download degli allegati nel dispositivo mobile. Il valore predefinito è <code>$true</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Crittografia del dispositivo abilitata</p></td>
<td><p>Questa impostazione consente di abilitare la crittografia nel dispositivo mobile. Non tutti i dispositivi mobili possono imporre la crittografia. Per ulteriori informazioni, vedere la documentazione del dispositivo e del sistema operativo per dispositivi mobili.</p></td>
</tr>
<tr class="even">
<td><p>Intervallo di aggiornamento criteri del dispositivo</p></td>
<td><p>Questa impostazione consente di specificare la frequenza con cui i criteri cassetta postale dei dispositivi mobili vengono inviati dal server al dispositivo mobile.</p></td>
</tr>
<tr class="odd">
<td><p>IRM abilitato</p></td>
<td><p>Questa impostazione consente di specificare se Information Rights Management (IRM) è abilitato sul dispositivo mobile.</p></td>
</tr>
<tr class="even">
<td><p>Dimensione massima allegati</p></td>
<td><p>Questa impostazione consente di controllare la dimensione massima degli allegati che possono essere scaricati sul dispositivo mobile. Il valore predefinito è Unlimited.</p></td>
</tr>
<tr class="odd">
<td><p>Filtro intervallo calendario massimo</p></td>
<td><p>Questa impostazione consente di specificare l'intervallo massimo di giorni del calendario sincronizzabili nel dispositivo mobile. Sono consentiti i seguenti valori:</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>Filtro intervallo posta elettronica massimo</p></td>
<td><p>Questa impostazione consente di specificare il numero massimo di giorni a disposizione per la sincronizzazione degli elementi di posta sul dispositivo mobile. Sono consentiti i seguenti valori:</p>
<ol>
<li><p>All</p></li>
<li><p>OneDay</p></li>
<li><p>ThreeDays</p></li>
<li><p>OneWeek</p></li>
<li><p>TwoWeeks</p></li>
<li><p>OneMonth</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Dimensione massima troncamento corpo posta elettronica</p></td>
<td><p>Questa impostazione consente di specificare la dimensione massima raggiunta la quale i messaggi di posta elettronica vengono troncati quando sincronizzati nel dispositivo mobile. Il valore è espresso in kilobyte (KB).</p></td>
</tr>
<tr class="even">
<td><p>Dimensione massima troncamento corpo HTML posta elettronica</p></td>
<td><p>Questa impostazione consente di specificare la dimensione massima raggiunta la quale i messaggi di posta elettronica HTML vengono troncati quando sincronizzati nel dispositivo mobile. Il valore è espresso in kilobyte (KB).</p></td>
</tr>
<tr class="odd">
<td><p>Tempo massimo di inattività prima del blocco</p></td>
<td><p>Questo valore consente di specificare l'intervallo di tempo durante il quale il dispositivo mobile può rimanere inattivo prima che venga richiesta la password per la riattivazione. È possibile immettere qualsiasi intervallo compreso tra 30 secondi e 1 ora. Il valore predefinito è 15 minuti.</p></td>
</tr>
<tr class="even">
<td><p>Numero massimo tentativi password non riusciti</p></td>
<td><p>Questa impostazione specifica il numero di tentativi che un utente può eseguire per immettere la password corretta per il dispositivo mobile. Digitare un numero intero compreso tra 4 e 16. Il valore predefinito è 8.</p></td>
</tr>
<tr class="odd">
<td><p>Numero minimo di caratteri complessi nella password</p></td>
<td><p>Questa impostazione specifica il numero di set di caratteri necessarie la password del dispositivo mobile. I set di caratteri sono:</p>
<ul>
<li><p>Lettere minuscole.</p></li>
<li><p>Lettere maiuscole.</p></li>
<li><p>Cifre da 0 a 9.</p></li>
<li><p>Caratteri speciali (ad esempio, punti esclamativi).</p></li>
</ul>
<p>Digitare un numero intero compreso tra 1 e 4. Il valore predefinito è 1.</p>
<p>Per i dispositivi Windows Phone 8, questa impostazione consente di specificare il numero dei set di caratteri necessarie la password. Ad esempio, il valore 3 richiede almeno un carattere da tutti e tre i set di caratteri.</p>
<p>Per i dispositivi Windows Phone 10, questa impostazione consente di specificare i requisiti di complessità delle password seguenti:</p>
<ol>
<li><p>Cifre.</p></li>
<li><p>Numeri e lettere minuscole.</p></li>
<li><p>Cifre, minuscole e lettere maiuscole.</p></li>
<li><p>Cifre, minuscole, lettere maiuscole e caratteri speciali.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><p>Lunghezza minima password</p></td>
<td><p>Questa impostazione consente di specificare il numero minimo di caratteri nella password del dispositivo mobile. Digitare un numero intero compreso tra 1 e 16. Il valore predefinito è 4.</p></td>
</tr>
<tr class="odd">
<td><p>Password abilitata</p></td>
<td><p>Questa impostazione consente di abilitare la password del dispositivo mobile.</p></td>
</tr>
<tr class="even">
<td><p>Scadenza password</p></td>
<td><p>Questa impostazione consente all'amministratore di configurare un intervallo di tempo trascorso il quale la password del dispositivo mobile deve essere modificata.</p></td>
</tr>
<tr class="odd">
<td><p>Cronologia password</p></td>
<td><p>Questa impostazione consente di specificare il numero di password già utilizzate che è possibile memorizzare nella cassetta postale dell'utente. L'utente non può riutilizzare una password memorizzata.</p></td>
</tr>
<tr class="even">
<td><p>Ripristino password abilitato</p></td>
<td><p>Quando questa impostazione è abilitata, il dispositivo mobile genera una password di ripristino che viene inviata al server. Se la password del dispositivo mobile viene dimenticata, è possibile utilizzare la password di ripristino per sbloccare il dispositivo mobile e abilitare la creazione di una nuova password.</p></td>
</tr>
<tr class="odd">
<td><p>Richiedi crittografia dispositivo</p></td>
<td><p>Questa impostazione consente di specificare se è richiesta la crittografia. Se impostato su <code>$true</code>, il dispositivo mobile deve supportare e implementare la crittografia per la sincronizzazione con il server.</p></td>
</tr>
<tr class="even">
<td><p>Richiedi messaggi S/MIME crittografati</p></td>
<td><p>Questa impostazione consente di specificare se i messaggi S/MIME devono essere crittografati. Il valore predefinito è <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p>Richiedi algoritmo di crittografia S/MIME</p></td>
<td><p>Questa impostazione consente di specificare l'algoritmo obbligatorio da utilizzare durante la crittografia dei messaggi S/MIME.</p></td>
</tr>
<tr class="even">
<td><p>Richiedi sincronizzazione manuale durante il roaming</p></td>
<td><p>Questa impostazione consente di specificare se il dispositivo mobile deve essere sincronizzato manualmente durante il roaming. Se si consente la sincronizzazione automatica durante il roaming i costi dei dati saranno superiori a quelli previsti per il piano dati del dispositivo mobile.</p></td>
</tr>
<tr class="odd">
<td><p>Richiedi algoritmo S/MIME firmato</p></td>
<td><p>Questa impostazione consente di specificare l'algoritmo obbligatorio da utilizzare durante la firma di un messaggio.</p></td>
</tr>
<tr class="even">
<td><p>Richiedi messaggi S/MIME firmati</p></td>
<td><p>Questa impostazione consente di specificare se il dispositivo mobile deve inviare messaggi S/MIME firmati.</p></td>
</tr>
<tr class="odd">
<td><p>Richiedi crittografia della scheda di memoria</p></td>
<td><p>Questa impostazione consente di specificare se la scheda di memoria deve essere crittografata. Non tutti i sistemi operativi di dispositivi mobili supportano la crittografia della scheda di memoria. Per ulteriori informazioni, vedere la documentazione del dispositivo mobile e del sistema operativo per dispositivi mobili.</p></td>
</tr>
<tr class="even">
<td><p>Elenco applicazioni InROM non approvate</p></td>
<td><p>Questa impostazione consente di specificare un elenco di applicazioni che non possono essere eseguite nella ROM. Per modificare i valori di questa impostazione, è necessaria la licenza Exchange Enterprise Client Access License.</p></td>
</tr>
</tbody>
</table>

