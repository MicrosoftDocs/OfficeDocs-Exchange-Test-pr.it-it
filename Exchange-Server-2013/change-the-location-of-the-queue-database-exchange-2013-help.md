---
title: 'Modificare il percorso del database della coda: Exchange 2013 Help'
TOCTitle: Modificare il percorso del database della coda
ms:assetid: f170cb0c-04a9-4fa7-b594-206e3a787e14
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125177(v=EXCHG.150)
ms:contentKeyID: 51407429
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare il percorso del database della coda

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Una *coda* è una posizione temporanea per i messaggi in attesa di passare alla fase successiva dell'elaborazione. Ogni coda rappresenta un insieme logico di messaggi elaborato da un server di trasporto in base a un ordine specifico.

Come le versioni precedenti di Exchange, Microsoft Exchange Server 2013 utilizza un solo database ESE (Extensible Storage Engine) per l'archiviazione dei messaggi della coda. Tutte le diverse code sono archiviate in un unico database ESE. Le code esistono solo sui server Cassette postali o sui server Trasporto Edge.

Il percorso del database delle code e dei registri delle transazioni è controllato dalle chiavi nel file XML di configurazione dell'applicazione `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` Tale file è associato al servizio di trasporto di Microsoft Exchange. Nella seguente tabella viene illustrata dettagliatamente ciascuna chiave.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Chiave</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p>Questa chiave specifica il percorso dei file del database delle code. I file sono:</p>
<ul>
<li><p>Mail.que</p></li>
<li><p>Trn.chk</p></li>
</ul>
<p>Il percorso predefinito è <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p>Questa chiave specifica il percorso dei file di registro delle transazioni del database delle code. I file sono:</p>
<ul>
<li><p>Trn.log</p></li>
<li><p>Trntmp.log</p></li>
<li><p>Trn<em>nnn</em>.log</p></li>
<li><p>Trnres00001.jrs</p></li>
<li><p>Trnres00002.jrs</p></li>
<li><p>Temp.edb</p></li>
</ul>
<p>Tenere presente che Temp.edb viene utilizzato per verificare lo schema del database delle code all'avvio del servizio di trasporto di Microsoft Exchange. Benché Temp.edb non sia un file di registro delle transazioni, viene conservato nello stesso percorso dei file di registro delle transazioni.</p>
<p>Il percorso predefinito è <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
</tbody>
</table>


## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti.

  - Le autorizzazioni di Exchange non sono applicabili alle procedure descritte in questo argomento. Queste procedure vengono eseguite nel sistema operativo del server di Exchange.

  - All'arresto o al riavvio di del servizio di trasporto di Microsoft Exchange, il flusso di posta sul server è interrotto.

  - Quando si cambia il percorso posizione del database delle code o dei registri delle transazioni, i file di registro delle transazioni e del database delle code esistenti non vengono spostati. Un nuovo database delle code e nuovi registri delle transazioni vengono creati nel nuovo percorso e i file esistenti vengono lasciati nel vecchio percorso. Tuttavia, non vengono più utilizzati. Per riutilizzare i file del database delle code o i file di registro delle transazioni esistenti nel nuovo percorso, è necessario spostare i file esistenti nel nuovo percorso dopo l'arresto del servizio di trasporto Exchange ma prima dell'avvio del servizio.

  - Se la cartella di destinazione per i file di registro delle transazioni o del database delle code non esiste, verrà creata se alla cartella padre sono applicate le seguenti autorizzazioni:
    
      - Servizio di rete: controllo completo
    
      - Sistema: Controllo completo
    
      - Amministratori: Controllo completo

  - Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Operazione desiderata

## Utilizzo del prompt dei comandi per creare un nuovo database delle code e nuovi registri delle transazioni in un nuovo percorso

1.  Creare le cartelle in cui archiviare il database delle code e i registri delle transazioni. Accertarsi che vengano applicate le autorizzazioni corrette alle cartelle.

2.  In una finestra del prompt dei comandi, aprire il file EdgeTransport.exe.config in Blocco note utilizzando il seguente comando:
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

3.  Modificare le seguenti chiavi nella sezione `<appSettings>`.
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    Ad esempio, per creare un nuovo database delle code in D:\\Queue\\QueueDB e nuovi registri della transazioni in D:\\Queue\\QueueLogs, utilizzare il seguente comando:
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  Al termine, salvare e chiudere il file EdgeTransport.exe.config.

5.  Riavviare il servizio di trasporto di Microsoft Exchange utilizzando il seguente comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver creato correttamente un nuovo database delle code e nuovi registri delle transazioni in un nuovo percorso, procedere nel modo seguente:

1.  Verificare che i nuovi file del database Mail.que e Trn.chk esistano nel nuovo percorso.

2.  Verificare che i nuovi file di registro delle transazioni Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs e Temp.edb esistano nel nuovo percorso.

3.  Se è possibile eliminare il vecchio database delle code e i vecchi file di registro delle transazioni dal vecchio percorso dopo l'avvio del servizio di trasporto di Microsoft Exchange, tali file non vengono più utilizzati.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Inizio pagina

## Utilizzo del prompt dei comandi per spostare il database delle code e i nuovi registri delle transazioni esistenti in un nuovo percorso

Soltanto i casi di ripristino di emergenza in cui il servizio di trasporto di Microsoft Exchange non è stato arrestato correttamente oppure i casi di guasto all'unità disco rigido richiedono il ripristino e la modifica del percorso di un database delle code esistente e dei relativi registri delle transazioni.

In circostanze normali, non è necessario riutilizzare i registri delle transazioni esistenti. Un arresto ordinario del servizio di trasporto di Micoroft Exchange scrive tutte le voci dei registri delle transazioni non salvate nel database delle code. Viene utilizzata, inoltre, la registrazione circolare in modo che i registri delle transazioni che contengono modifiche del database applicate in precedenza non vengano conservati.

Utilizzare la seguente procedura per spostare il database delle code e i nuovi registri delle transazioni esistenti in un nuovo percorso:

1.  Creare le cartelle in cui archiviare il database delle code e i registri delle transazioni. Accertarsi che vengano applicate le autorizzazioni corrette alle cartelle.

2.  In una finestra del prompt dei comandi, aprire il file EdgeTransport.exe.config in Blocco note utilizzando il seguente comando:
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

3.  Modificare le seguenti chiavi nella sezione `<appSettings>`:
    
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    
    Ad esempio, per modificare il percorso del database delle code in D:\\Queue\\QueueDB e quello dei registri delle transazioni in D:\\Queue\\QueueLogs, utilizzare i seguenti valori:
    
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />

4.  Al termine, salvare e chiudere il file EdgeTransport.exe.config.

5.  Arrestare il servizio di trasporto di Microsoft Exchange utilizzando il seguente comando:
    
    ```powershell
net stop MSExchangeTransport
```

6.  Spostare i file del database esistenti Mail.que e Trn.chk dal percorso originale al nuovo percorso.

7.  Copiare i file di registro delle transazioni esistenti, Trn.log, Trntmp.log, Trn*nnnnn*.log, Trnres00001.jrs, Trnres00002.jrs e Temp.edb, dal vecchio al nuovo percorso.

8.  Avviare il servizio di trasporto di Microsoft Exchange utilizzando il seguente comando:
    
    ```powershell
net start MSExchangeTransport
```

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente spostato il database delle code e i registri delle transazioni esistenti nel nuovo percorso, procedere come segue:

1.  Verificare che i file del database delle code Mail.que e Trn.chk esistano nel nuovo percorso.

2.  Verificare che i file di registro delle transazioni Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs e Temp.edb esistano nel nuovo percorso.

3.  Verificare che non siano presenti file del database delle code o file di registro delle transazioni nel percorso originale.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Inizio pagina

