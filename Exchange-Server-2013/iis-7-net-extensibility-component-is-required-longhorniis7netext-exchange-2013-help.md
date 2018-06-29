---
title: 'Estendibilità .NET di IIS 7 componente è required_LonghornIIS7NetExt: Exchange 2013 Help'
TOCTitle: Estendibilità .NET di IIS 7 componente è required_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 50481135
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Estendibilità .NET di IIS 7 componente è required\_LonghornIIS7NetExt

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft®Installazione di Exchange Server 2010 non può continuare perché il componente di estendibilità .NET Internet Information Server (IIS) 7 richiesto non è installato nel server di destinazione.

Prima di Exchange 2010 è possibile utilizzare Windows PowerShell remoto, è necessario installare il componente IIS 7 .NET Extensibility sul server di destinazione.

Per risolvere questo errore, utilizzare Server Manager per installare il componente di estendibilità .NET 7 IIS nel server e quindi rieseguire il programma di installazione di Exchange 2010.

Installare il componente di estendibilità .NET di IIS 7 in Windows Server 2008 o Windows Server 2008 R2 mediante lo strumento Server Manager

1.  Fare clic su **Start**, scegliere **Strumenti di amministrazione** e quindi **Server Manager**.

2.  Nel riquadro di spostamento sinistro espandere **Ruoli** , quindi fare clic con il pulsante destro del mouse su **Server Web (IIS)** e scegliere **Aggiungi servizi ruolo**.

3.  Nel riquadro **Selezione servizi ruolo**, scorrere verso il basso per **Lo sviluppo di applicazioni**.

4.  Selezionare la casella di controllo in **Estendibilità .NET**.

5.  Fare clic su **Avanti** nel riquadro **Selezione servizi ruolo** e quindi fare clic su **Installa** il riquadro **Conferma selezioni**.

6.  Fare clic su **Chiudi** per chiudere la procedura guidata Aggiunta servizi ruolo.

