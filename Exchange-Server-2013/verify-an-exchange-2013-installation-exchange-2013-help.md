---
title: "Verificare un'installazione di Exchange 2013: Exchange 2013 Help"
TOCTitle: Verificare un'installazione di Exchange 2013
ms:assetid: fdd20a2a-c8c1-4d17-b813-3c05d88a4411
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125254(v=EXCHG.150)
ms:contentKeyID: 50482132
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Verificare un'installazione di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

Dopo aver installato Microsoft Exchange Server 2013, è consigliabile verificare l'installazione eseguendo il cmdlet **Get-ExchangeServer** ed esaminando il file di log dell'installazione. Se il processo di installazione non riesce oppure se si verificano degli errori durante l'installazione, è possibile utilizzare i file di registro installazione per individuare l'origine del problema.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.

## Esecuzione di Get-ExchangeServer

Per verificare se l'installazione di Exchange 2013 è stata eseguita correttamente, eseguire il cmdlet **Get-ExchangeServer** in Exchange Management Shell. All'esecuzione di questo cmdlet, viene visualizzato un elenco di tutti i ruoli del server di Exchange 2013 installati sul server specificato.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-ExchangeServer](https://technet.microsoft.com/it-it/library/bb123873\(v=exchg.150\)).

## Analisi del file di log dell'installazione

Inoltre, per saperne di più sull'installazione e la configurazione di Exchange 2013, esaminare il file di log creato durante il processo di installazione.

Durante l'installazione, il programma di installazione di Exchange registra gli eventi nel log **Applicazione** di **Visualizzatore eventi** nei computer su cui è in esecuzione Windows Server 2008 R2 con Service Pack 1 (SP1) e Windows Server 2012. Esaminare il log **Applicazione** e verificare che non siano presenti messaggi di avviso o di errore correlati all'installazione di Exchange. I file di log contengono una cronologia di ogni azione eseguita dal sistema durante l'installazione di Exchange 2013 e degli eventuali errori che si sono verificati. Per impostazione predefinita, il metodo di registrazione è impostato su `Verbose`. Le informazioni sono disponibili per ogni ruolo del server installato.

Il file di log dell'installazione è disponibile nel percorso *\<system drive\>*\\ExchangeSetupLogs\\ExchangeSetup.log. La variabile *\<system drive\>* rappresenta la directory radice dell'unità in cui è installato il sistema operativo.

Il file di log dell'installazione tiene traccia dell'avanzamento di ogni operazione eseguita durante l'installazione e la configurazione di Exchange 2013. Il file contiene informazioni sullo stato dei controlli dei prerequisiti e dell'organizzazione del sistema che vengono eseguiti prima dell'avvio dell'installazione, sull'avanzamento dell'installazione dell'applicazione e sulle modifiche di configurazione apportate al sistema. Controllare questo file di registro per verificare che i ruoli del server siano stati installati correttamente.

Si consiglia di iniziare l'analisi del file di log dell'installazione dalla ricerca di eventuali erori. Se una voce indica che si è verificato un errore, leggere il testo associato per stabilire la causa dell'errore.

