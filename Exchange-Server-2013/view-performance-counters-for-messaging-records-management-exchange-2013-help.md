---
title: 'Contatori prestaz. visualizz. per gestione record mess.: Exchange 2013 Help'
TOCTitle: Contatori delle prestazioni di visualizzazione per la gestione dei record di messaggistica
ms:assetid: ec374d31-2797-4f8b-8c96-3839d01a662c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb397227(v=EXCHG.150)
ms:contentKeyID: 51407439
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contatori delle prestazioni di visualizzazione per la gestione dei record di messaggistica

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2009-12-09_

È possibile utilizzare Monitoraggio affidabilità e prestazioni di Windows (Perfmon.exe) per selezionare e visualizzare i contatori delle prestazioni per la gestione dei record di messaggistica (MRM). Utilizzando i contatori delle prestazioni è possibile monitorare l'Assistente cartelle gestite mentre esegue processi della gestione record di messaggistica che impiegano molte risorse.

Per un elenco dei contatori delle prestazioni per la gestione record di messaggistica, vedere [Contatori delle prestazioni per la gestione dei record di messaggistica](performance-counters-for-https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/messaging-records-management).

Per informazioni sulle altre attività relative al monitoraggio della gestione record di messaggistica, vedere [Gestione dei record di messaggistica di monitoraggio](monitoring-https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/messaging-records-management).

## Utilizzo di Monitoraggio affidabilità e prestazioni di Windows per visualizzare i contatori delle prestazioni per la gestione record di messaggistica

Per eseguire questa procedura, è necessario utilizzare un account che disponga della delega di appartenenza al gruppo Administrators locale.

1.  Per avviare Monitoraggio affidabilità e prestazioni di Windows, fare clic su **Start**, **Esegui** e digitare **Perfmon**.

2.  Nella struttura ad albero della console, individuare **Strumenti di monitoraggio** \> **Performance Monitor**.

3.  Fare clic sul pulsante con il segno più (+) sulla barra degli strumenti. Viene visualizzata la finestra di dialogo **Aggiungi contatori**.

4.  Nell'elenco **Utilizza contatori del computer locale**, scegliere una delle seguenti opzioni:
    
      - Se si sta eseguendo questa procedura su un computer locale, selezionare **\<Computer locale\>**. Questa è la selezione predefinita.
    
      - Se la procedura viene eseguita in remoto, selezionare il server da monitorare.

5.  Nell'elenco dei contatori delle prestazioni, espandere **Assistenti di MSExchange - Per database** o **Assistente cartelle gestite di MSExchange**.

6.  Selezionare i contatori delle prestazioni da monitorare.

7.  Per i contatori delle prestazioni sotto **Assistenti di MSExchange - Per database**, fare clic su **Tutte le istanze** in **Istanze dell'oggetto selezionato** per visualizzare i contatori per tutti i database delle cassette postali. In alternativa, per specificare uno o più database delle cassette postali, selezionare le istanze dall'elenco.

8.  Per aggiungere i contatori selezionati in modo che appaiono in Monitoraggio affidabilità e prestazioni di Windows e per iniziare a raccogliere dati sulle prestazioni, fare clic su **Aggiungi**.

