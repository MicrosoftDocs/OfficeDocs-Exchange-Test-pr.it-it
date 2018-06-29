---
title: 'Configurazione di Get-QueueDigest: Exchange 2013 Help'
TOCTitle: Configurazione di Get-QueueDigest
ms:assetid: f730c520-4ba5-4a15-8846-132bff500bb8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn505733(v=EXCHG.150)
ms:contentKeyID: 59634756
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione di Get-QueueDigest

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-12-16_

Il cmdlet **Get-QueueDigest** consente di visualizzare informazioni su alcune o tutte le code presenti nell'organizzazione di Exchange utilizzando un unico comando.

Per impostazione predefinita, i risultati restituiti dal cmdlet **Get-QueueDigest** risalgono da uno a due minuti prima. Questi valori sono controllati dalle impostazioni seguenti:

  - **QueueLoggingInterval key in EdgeTransport.exe.config**   Questa chiave specifica la frequenza con cui i dati della coda vengono registrati e resi disponibili per **Get-QueueDigest**. Il valore predefinito è `00:01:00` (un minuto). Per specificare un valore, immettere un intervallo di tempo: *hh:mm:ss* dove *h* = ore, *m* = minuti e *s* = secondi. Per impostazione predefinita, questa chiave non è presente nel file EdgeTransport.exe.config.

  - **QueueDiagnosticsAggregationInterval parameter on Set-TransportConfig**   Questo parametro consente di specificare la frequenza con cui i dati della coda vengono condivisi dai server Cassette postali. Il valore predefinito è `00:01:00` (un minuto). Per specificare un valore, immettere un intervallo di tempo: *hh:mm:ss* dove *h* = ore, *m* = minuti e *s* = secondi.

La somma dei valori della chiave **QueueLoggingInterval** e del parametro *QueueDiagnosticsAggregationInterval* determina il limite massimo di validità dei risultati restituiti da **Get-QueueDigest**.

**Get-QueueDigest**, inoltre, restituisce risultati differenti a seconda del tipo e dello stato della coda. Le code indicate di seguito, ad esempio, vengono visualizzate nei risultati finché contengono almeno un messaggio:

  - Coda di invio, coda non raggiungibile e coda di messaggi potenzialmente dannosi (code permanenti).

  - Code di recapito con stato Sospeso (code sospese manualmente da un amministratore).

Per impostazione predefinita, le code di recapito con stato Attivo, In fase di connessione, Pronto o Riprova vengono restituite nei risultati solo se contengono 10 o più messaggi. Questo valore è controllato dalla chiave **QueueLoggingThreshold** nel file EdgeTransport.exe.config. È possibile specificare un valore intero maggiore o minore. Per impostazione predefinita, questa chiave non è presente nel file EdgeTransport.exe.config.

## Informazioni preliminari

  - Tempo stimato per il completamento: 15 minuti

  - Per visualizzare le autorizzazioni di Exchange è necessario eseguire **Set-TransportConfig** in Exchange Management Shell. Vedere la voce "Configurazione del trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Le autorizzazioni di Exchange non sono valide per la modifica del file EdgeTransport.exe.config e il riavvio del servizio di trasporto di Microsoft Exchange. Queste procedure vengono eseguite nel sistema operativo del server di Exchange.

  - Le modifiche apportate al file EdgeTransport.exe.config hanno effetto dopo il riavvio del servizio di trasporto di Microsoft Exchange. Quando si riavvia il servizio, il flusso di posta sul server viene temporaneamente interrotto.

  - Qualsiasi impostazione personalizzata per singolo server apportata nei file di configurazione dell'applicazione XML di Exchange, ad esempio, i file web.config sui server Accesso client oppure il file EdgeTransport.exe.config sui server Cassette postali, verrà sovrascritta quando si installa un aggiornamento cumulativo di Exchange. Salvare queste informazioni in modo da poter facilmente riconfigurare il server dopo l'installazione. È necessario riconfigurare queste impostazioni dopo aver installato un aggiornamento cumulativo di Exchange.

  - Le modifiche apportate utilizzando **Set-TransportConfig** interessano tutti i server Cassette postali dell'organizzazione. Le modifiche apportate al file EdgeTransport.exe.config interessano solo il server Cassette postali locale.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione di Get-QueueDigest

1.  In una finestra del prompt dei comandi, aprire il file EdgeTransport.exe.config in Blocco note utilizzando il seguente comando:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Aggiungere una o più delle seguenti chiavi nella sezione `<appSettings>`.
    
        <add key="QueueLoggingThreshold" value="<integer>" />
        <add key="QueueLoggingInterval" value="<hh:mm:ss>" />
    
    Ad esempio, per impostare il valore di **QueueLoggingThreshold** su 1 e il valore di **QueueLoggingInterval** su 30 secondi, utilizzare i seguenti valori:
    
        <add key="QueueLoggingThreshold" value="1" />
        <add key="QueueLoggingInterval" value="00:00:30" />

3.  Al termine, salvare e chiudere il file EdgeTransport.exe.config.

4.  Riavviare il servizio di trasporto di Microsoft Exchange utilizzando il seguente comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

5.  Per modificare il valore del parametro *QueueDiagnosticsAggregationInterval* in Exchange Management Shell, utilizzare la seguente sintassi:
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval <hh:mm:ss>
    
    Per modificare il valore in 30 secondi, ad esempio, eseguire il comando seguente:
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval 00:00:30

## Verifica dell'esito positivo dell'operazione

Per verificare che **Get-QueueDigest** sia stato configurato correttamente, procedere come segue:

1.  Verificare i valori delle chiavi **QueueLoggingThreshold** e **QueueLoggingInterval** nel file EdgeTransport.exe.config. Se le chiavi non sono presenti, vengono utilizzati i valori predefiniti.

2.  Verificare il valore del parametro *QueueDiagnosticsAggregationInterval* eseguendo il comando riportato di seguito:
    
        Get-TransportConfig | Format-List *queue*

