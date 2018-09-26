---
title: 'Configurare la registrazione nella tabella di routing: Exchange 2013 Help'
TOCTitle: Configurare la registrazione nella tabella di routing
ms:assetid: 7184f8f7-4eb8-468a-aafe-b2d72868f820
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201696(v=EXCHG.150)
ms:contentKeyID: 50480865
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la registrazione nella tabella di routing

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

La registrazione nella tabella di routing registra periodicamente un'istantanea della tabella di routing utilizzata da Microsoft Exchange Server 2013 per instradare i messaggi alle loro destinazioni finali.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Servizio Trasporto" e "Server Trasporto Edge" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È possibile utilizzare solo Shell per eseguire questa procedura.

  - Per configurare l'intervallo di tempo per il ricalcolo automatico della tabella di routing, modificare il file XML di configurazione dell'applicazione EdgeTransport.exe.config. Le modifiche salvate nel file vengono applicate quando il servizio di trasporto di Microsoft Exchange viene riavviato. Quando si riavvia il servizio, il flusso di posta sul server viene interrotto temporaneamente.

  - Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo di Shell per la configurazione della registrazione nella tabella di routing

Eseguire il comando indicato di seguito:

```powershell
    Set-TransportService <ServerIdentity> -RoutingTableLogMaxAge <dd.hh:mm:ss> -RoutingTableLogMaxDirectorySize <Size>  -RoutingTableLogPath <LocalFilePath>
```
In questo esempio vengono impostate le seguenti impostazioni per la registrazione nella tabella di routing sul server Cassette postali Mailbox01:

  - Imposta il percorso dei file di registro della tabella di routing su D:\\Routing Table Log. Notare che se la cartella non esiste, verrà creata automaticamente.

  - Imposta la dimensione massima della cartella di registro della tabella di routing su 70 MB.

  - Imposta la durata massima di un file di registro della tabella di routing su 45 giorni.

<!-- end list -->
```powershell
    Set-TransportService Mailbox01 -RoutingTableLogPath "D:\Routing Table Log" -RoutingTableLogMaxDirectorySize 70MB -RoutingTableLogMaxAge 45.00:00:00
```

> [!NOTE]
> Se il parametro <EM>RoutingTableLogMaxAge</EM> viene impostato su <CODE>00:00:00</CODE>, si evita che i file di registro della tabella di routing vengano rimossi automaticamente dopo un determinato periodo di tempo.



## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente configurato la registrazione nella tabella di routing, fare quanto segue:

1.  In Shell, utilizzare il seguente comando:

    ```powershell
        Get-TransportService <ServerIdentity> | Format-List RoutingTableLog*
    ```
2.  Verificare che i valori visualizzati siano quelli configurati.

## Utilizzo del prompt dei comandi per la configurazione dell'intervallo per il ricalcolo automatico della tabella di routing nel file EdgeTransport.exe.config

1.  In una finestra del prompt dei comandi, utilizzare il seguente comando per aprire il file di configurazione dell'applicazione EdgeTransport.exe.config in Blocco note:
    
    ```powershell
    Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

2.  Modificare la seguente chiave nella sezione `<appSettings>`.
    
    ```command line
    <add key="RoutingConfigReloadInterval" value="<hh:mm:ss>" />
    ```
    
    Ad esempio, per impostare l'intervallo per il ricalcolo automatico della tabella di routing su 10 ore, utilizzare il seguente valore:
    
    ```command line
    <add key="RoutingConfigReloadInterval" value="10:00:00" />
    ```

3.  Al termine, salvare e chiudere il file EdgeTransport.exe.config.

4.  Riavviare il servizio di trasporto di Microsoft Exchange utilizzando il seguente comando:
    ```powershell
        net stop MSExchangeTransport && net start MSExchangeTransport
    ```
## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente configurato l'intervallo per il ricalcolo automatico della tabella di routing, controllare che il registro di detta tabella venga aggiornato durante l'intervallo di tempo specificato.

Notare che la tabella di routing verrà ricalcolata e registrata prima del valore specificato dalla chiave *RoutingConfigReloadInterval* se si verifica una delle seguenti condizioni:

  - Viene rilevata una modifica della configurazione di routing. Ad esempio viene aggiunto, rimosso o modificato un connettore di invio o di ricezione oppure si verifica il rinnovo del token Kerberos ogni 6 ore.

  - Il servizio di trasporto di Microsoft Exchange viene avviato.

