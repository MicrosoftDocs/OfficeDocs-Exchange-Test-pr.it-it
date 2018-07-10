---
title: Risoluzione dei problemi di integrità SiteMailbox impostare
TOCTitle: Risoluzione dei problemi di integrità SiteMailbox impostare
ms:assetid: ac00985c-c9a5-44bf-b152-4b99d8ae24ed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.scom.sitemailbox(v=EXCHG.150)
ms:contentKeyID: 53275538
ms.date: 03/07/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Risoluzione dei problemi di integrità SiteMailbox impostare

 

_**Si applica a:** Exchange Server 2013, Project Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-11_

Il set di integrità SiteMailbox monitora l'integrità generale e l'accessibilità delle cassette postali del sito nell'organizzazione.

Un avviso che specifica che SiteMailbox non è integro indica che il contenuto della cassetta postale di un utente non è in stato sincronizzato.

## Descrizione

Il sistema di monitoraggio SiteMailbox riceve risultati di sincronizzazione passivi dal servizio di sincronizzazione in background. Il sistema non utilizza probe. I risultati della sincronizzazione passiva vengono scritti nel sistema di monitoraggio SiteMailbox dopo ogni tentativo di sincronizzazione. Le sincronizzazioni vengono attivate anche quando si verificano i seguenti eventi:

  - Gli utenti accedono alle proprie cassette postali del sito utilizzando Outlook o Outlook Web App

  - Si esegue il comando **Update-SiteMailbox**

  - Si apre la finestra Opzioni di Outlook Web App e si fa clic sul pulsante **Avvia sincronizzazione** nella pagina **Stato sincronizzazione** per la cassetta postale del sito selezionata

Per ulteriori informazioni sul cmdlet Update-SiteMailbox vedere: [Update-SiteMailbox](https://technet.microsoft.com/it-it/library/jj218690\(v=exchg.150\))

Per ulteriori informazioni su probe e monitor, vedere [Prestazioni e lo stato dei server](https://technet.microsoft.com/it-it/library/jj150551\(v=exchg.150\)).

## Problemi comuni

Il servizio di monitoraggio della sincronizzazione in genere attiva un avviso quando si verificano problemi di sincronizzazione diffusi su tutto il sito. Non viene inviato alcun avviso quando non riesce la sincronizzazione di una singola cassetta postale. Per stabilire la causa di un avviso sopra la soglia per una singola cassetta postale si consiglia di esaminare i file di registro della sincronizzazione delle cassette postali del sito.

## Azione utente

È possibile che il servizio venga ripristinato dopo l'emissione dell'avviso. Di conseguenza, se si riceve un avviso indicante che il set di integrità non è in integro, verificare prima che il problema sia ancora presente. Se il problema ancora esiste, eseguire le azioni di ripristino appropriate delineate nelle sezioni seguenti.

## Verifica dell'esistenza del problema

1.  Identificare il nome del set di integrità e il nome del server nell'avviso.

2.  I dettagli del messaggio forniscono informazioni sulla causa esatta dell'avviso. Nella maggior parte dei casi, i dettagli del messaggio contengono informazioni di risoluzione dei problemi sufficienti ad identificare la causa principale. Se i dettagli del messaggio non sono chiari, procedere come segue:
    
    1.  Aprire Exchange Management Shell, quindi utilizzare il seguente comando per recuperare i dettagli del set di integrità che ha emesso l'avviso:
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Ad esempio, per recuperare i dettagli del set di integrità SiteMailbox su server1.contoso.com, utilizzare il seguente comando:
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "SiteMailbox"}
    
    2.  Esaminare l'output del comando per determinare quale controllo ha segnalato l'errore. Il valore **AlertValue** del controllo che ha emesso l'avviso sarà `Unhealthy`.

## Procedura di risoluzione dei problemi

Quando si riceve un avviso da un set di integrità, il messaggio di posta elettronica contiene le informazioni seguenti:

  - Nome del server che ha inviato l'avviso

  - Ora e data in cui si è verificato l'avviso

  - Meccanismo di autenticazione utilizzato e informazioni sulle credenziali

  - Traccia di eccezione completa dell'ultimo errore, inclusi i dati diagnostici e le informazioni specifiche dell'intestazione HTTP  
    
    **Nota**   È possibile utilizzare le informazioni contenute nella traccia di eccezione completa per risolvere il problema. L'eccezione generata dal probe contiene una Causa errore che descrive perché il probe non è riuscito.

**Errori di sincronizzazione in background**

Quando il processo di sincronizzazione in background non riesce, si potrebbe ricevere un avviso simile al seguente:

La sincronizzazione delle cassette postali del sito non è riuscita per almeno il 25%: 41 errori su 87 tentativi. Risultato sincronizzazione campione:

\[Messaggio: ll server remoto ha restituito un errore: (401) Non autorizzato.\]\[Tipo:System.Net.WebException\]

L'avviso viene attivato quando una percentuale costantemente elevata degli errori di sincronizzazione si è verificata durante le precedenti quattro ore. Per evitare falsi negativi, un avviso viene inviato solo quando le seguenti condizioni vengono soddisfatte entro un periodo di 15 minuti durante le precedenti quattro ore:

  - Si sono verificati almeno 20 errori entro un periodo di 15 minuti.

  - La percentuale di errori rispetto ai tentativi totali supera il 25 per cento in un periodo di 15 minuti.

Ogni cassetta postale del sito in Exchange è collegata a un sito SharePoint. Per ogni cassetta postale del sito in un determinato server Exchange che ospita il ruolo Cassette postali, il server sincronizza le informazioni correlate alla cassetta postale del sito da SharePoint.

Durante questo processo si verificano due tipi di sincronizzazione: sincronizzazione di appartenenza e sincronizzazione dei documenti. I metadati per questi processi di sincronizzazione hanno origine da servizi Web diversi. Inoltre, un determinato server Exchange potrebbe contenere cassette postali del sito collegate a diversi server o farm SharePoint. Di conseguenza, un avviso potrebbe originale da più server Cassette postali, a seconda delle seguenti condizioni:

1.  Modalità di distribuzione delle cassette postali attive nell'organizzazione

2.  I server SharePoint a cui sono collegate le cassette postali del sito attivamente utilizzate

3.  Se il server Cassette postali ha un volume di sincronizzazione sufficiente per soddisfare le soglie di avviso

Per risolvere il problema, il risultato della sincronizzazione campione nell'avviso potrebbe consentire di determinare la causa dell'errore. I dettagli dell'esito positivo o negativo di ogni tentativo di sincronizzazione è registrato nella cartella *\<directory di installazione di exExchangeSvrNoVersion\>*Logging\\TeamMailbox. Esaminare i file Microsoft.Exchange.ServiceHost\_TeamMailboxSyncLog\* più recenti cercando il termine **non riuscito**. È anche possibile utilizzare i cmdlet **Test-OAuthConnectivity**, **Test-SiteMailbox** e **Get-SiteMailboxDiagnostics** per approfondire la risoluzione dei problemi.

**Il servizio MSExchangeServiceHost non è in esecuzione.**

Se il servizio MSExchangeServiceHost non è in esecuzione si riceve un avviso simile al seguente:

Il servizio 'MSExchangeServiceHost' non è in esecuzione dopo i tentativi di ripristino. Il servizio potrebbe essere disabilitato o in loop di arresti anomali.

Per risolvere il problema, verificare che il servizio MSExchangeServiceHost sia in esecuzione sul server che ha inviato l'avviso. Se il servizio è in esecuzione, esaminare i registri degli eventi di Windows per cercare indicazioni sul motivo per cui il servizio potrebbe non essere stato in esecuzione in precedenza, ad esempio a causa di un controllo manuale o per ripetuti arresti anomali del servizio.

**Si è verificato un arresto anomalo del servizio MSExchangeServiceHost**

Se il servizio MSExchangeServiceHost si arresta in modo anomalo si riceve un avviso simile al seguente:

Il processo MSExchangeServiceHost si è arrestato in modo anomalo 3 volte negli ultimi 60 minuti.  
Messaggio Watson:

\<*Messaggio*\>

Per risolvere il problema, esaminare il registro degli eventi dell'applicazione Windows sul server che ha inviato l'avviso per gli eventi **4999** relativi al servizio MSExchangeServiceHost. Il testo dei dettagli può fornire informazioni sulla causa del problema.

## Per ulteriori informazioni

[Novità di Exchange 2013](https://technet.microsoft.com/it-it/library/jj150540\(v=exchg.150\))

[Cmdlet di Exchange 2013](https://technet.microsoft.com/it-it/library/bb124413\(v=exchg.150\))

