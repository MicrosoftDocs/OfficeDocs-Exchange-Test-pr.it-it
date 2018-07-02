---
title: Importazione del Management Pack di Exchange Server 2013
TOCTitle: Importazione del Management Pack di Exchange Server 2013
ms:assetid: dc929928-61b8-448b-9ae5-d3fa73a18ee9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn195914(v=EXCHG.150)
ms:contentKeyID: 53275567
ms.date: 08/30/2014
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Importazione del Management Pack di Exchange Server 2013

 

_**Ultima modifica dell'argomento:**  2013-03-30_

Di seguito viene illustrata la procedura di importazione del Management Pack nella distribuzione SCOM.

## Prerequisiti

Prima di poter importare il Management Pack, verificare che le seguenti condizioni siano soddisfatte:

  - Si dispone di una delle seguenti versioni di System Center Operations Manager distribuita nell'organizzazione:
    
      - System Center Operations Manager 2012 RTM o versione successiva
    
      - System Center Operations Manager 2007 R2 o versione successiva

  - Sono già stati distribuiti gli agenti SCOM nei server Exchange. [Verificare lo stato di distribuzione dell'agente](procedures-related-to-deployment.md).

  - Gli agenti SCOM sui server Exchange vengono eseguiti con un account di sistema locale. [Verificare la configurazione protezione agente](procedures-related-to-deployment.md).

  - Gli agenti SCOM sui server Exchange sono configurati per agire come proxy e scoprire oggetti gestiti su altri computer. [Verificare la configurazione proxy agente](procedures-related-to-deployment.md).

  - L'account utente è un membro del ruolo Administrators di Operations Manager.

## Importazione del Management Pack di Exchange Server 2013

Per importare il Management Pack di Exchange 2013, procedere nel modo seguente. Con questa procedura si presume che sia stato estratto il contenuto del Management Pack su un'unità locale sul server SCOM (System Center Operations Manager). È possibile scaricare il Management Pack di Exchange Server 2013 da

1.  Accedere al server SCOM e scaricare il Management Pack di Exchange Server 2013 dall'[Area download Microsoft](http://go.microsoft.com/fwlink/p/?linkid=268587).

2.  Estrarre il contenuto del Management Pack in una cartella del sistema eseguendo il file `ExchangeServerManagementPack.msi`.

3.  Avviare la console di SCOM. Nella Console di SCOM, fare clic su **Amministrazione**.

4.  Fare clic con il pulsante destro del mouse sul nodo **Management Pack** e selezionare **Importa Management Pack**.

5.  Verrà visualizzata l'Importazione guidata Management Pack. Fare clic su **Aggiungi**, quindi scegliere il pulsante **Aggiungi da disco**.

6.  Verrà visualizzata la finestra di dialogo **Seleziona Management Pack da importare**. Individuare la directory in cui è stato estratto il Management Pack. Fare clic su `Microsoft.Exchange.15.mp` e selezionare **Apri**.

7.  Nella pagina **Seleziona Management Pack** è incluso il Management Pack di Exchange Server 2013. Fare clic su **Installa**.

8.  Viene visualizzata la pagina **Importa Management Pack** che mostra l'avanzamento dell'importazione. Se si verifica un problema in qualsiasi fase del processo di importazione, selezionare il Management Pack nell'elenco per visualizzare i dettagli sullo stato.

9.  Al termine dell'importazione, fare clic su **Chiudi**.

10. Fare clic su **Visualizza** e selezionare **Aggiorna** oppure premere F5 per visualizzare il Management Pack di Microsoft Exchange Server 2013 nell'elenco di Management Pack.

Ora che il Management Pack è stato impostato, vedere [Guida introduttiva a Exchange Server 2013 Management Pack](getting-started-with-exchange-server-2013-management-pack.md) per informazioni sul nuovo dashboard.

