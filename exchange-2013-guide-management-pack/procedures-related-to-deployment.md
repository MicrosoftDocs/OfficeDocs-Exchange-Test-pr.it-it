---
title: Procedure relative alla distribuzione
TOCTitle: Procedure relative alla distribuzione
ms:assetid: 6b7682bd-fe3d-43b9-a7db-66c0ac17656f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn195909(v=EXCHG.150)
ms:contentKeyID: 53275562
ms.date: 08/30/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Procedure relative alla distribuzione

 

_**Ultima modifica dell'argomento:** 2013-04-17_

Questa sezione contiene le procedure che è possibile utilizzare come riferimento durante l'utilizzo di Exchange Server 2013 Management Pack. Per le procedure successive alla distribuzione, vedere[Procedures related to post-deployment operation](procedures-related-to-post-deployment-operation.md).

## Verificare lo stato di distribuzione dell'agente

Prima di importare Exchange Server 2013 Management Pack, verificare che gli agenti SCOM sui server Exchange siano operativi e che l'integrità del sistema operativo venga segnalata correttamente in SCOM.

L'account utente deve essere membro del ruolo Amministratori di Operations Manager per eseguire questa procedura.

1.  Accedere al server SCOM e aprire la console SCOM.

2.  Fare clic su **Monitoraggio**, quindi scegliere **Computer Windows**.

3.  Assicurarsi che tutti i server Exchange mostrino **Integro**.

![Agenti integri nella console SCOM](images/Dn195909.7d1ff0bb-419e-40dc-babf-5fa2fb7229a8(EXCHG.150).png "Agenti integri nella console SCOM")

## Verificare la configurazione proxy agente

Prima di importare Exchange Server 2013 Management Pack, verificare che il proxy agente sia attivato per l'individuazione in SCOM. Altrimenti gli agenti sui server Exchange non segnaleranno lo stato di integrità di Exchange. È necessario verificare la configurazione per tutti gli Exchange Server.

L'account utente deve essere membro del ruolo Amministratori di Operations Manager per eseguire questa procedura.

1.  Accedere al server SCOM e aprire la console SCOM.

2.  Nella Console operatore, fare clic su **Amministrazione**.

3.  Fare clic su **Gestito tramite agente**. Fare clic con il pulsante destro del mouse sul server di Exchange, quindi selezionare **Proprietà**.

4.  Nella scheda **Sicurezza**, verificare che la casella di controllo **Consenti a questo agente di funzionare come proxy e individuare oggetti gestiti sugli altri computer** sia selezionata.

5.  Fare clic su **OK**.

## Verificare la configurazione protezione agente

Poiché Exchange 2013 è stato testato in un determinato modello di protezione, l'esecuzione dell'agente SCOM su server Exchange in un account diverso da **LocalSystem** non è supportato. Se si esegue l'agente in un account diverso da LocalSystem, le transazioni sintetiche riporteranno errori di esecuzione. È inoltre possibile riscontrare altri problemi.

L'account utente deve essere membro del gruppo di ruoli Gestione server per eseguire questa procedura.

1.  Eseguire l'accesso al server Exchange.

2.  Selezionare **Start** \> **Strumenti di amministrazione** \> **Servizi**.

3.  Scorrere l'elenco di dispositivi per individuare il servizio **Gestione di System Center**.

4.  Verificare che la colonna **Connessione** mostri **Sistema locale**.

5.  Se la colonna **Connessione** mostra altro, modificare l'accesso al servizio in Sistema locale.
    
    1.  Fare clic con il pulsante destro del mouse sul servizio **Gestione di System Center** e selezionare **Proprietà**.
    
    2.  Selezionare la scheda **Connessione**.
    
    3.  Fare clic sull'opzione **account di sistema locale**.
    
    4.  Fare clic su **OK**.

