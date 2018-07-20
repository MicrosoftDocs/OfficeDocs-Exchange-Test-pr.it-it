---
title: 'Componenti di compatibilità con IIS 6 non installed_LonghornIIS6MgmtConsoleNotInstalled: Exchange 2013 Help'
TOCTitle: Componenti di compatibilità con IIS 6 non installed_LonghornIIS6MgmtConsoleNotInstalled
ms:assetid: 8358eafb-def7-4b8d-8fe1-623bc5a0e20e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.longhorniis6mgmtconsolenotinstalled(v=EXCHG.150)
ms:contentKeyID: 50481078
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Componenti di compatibilità con IIS 6 non installed\_LonghornIIS6MgmtConsoleNotInstalled

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft®Il programma di installazione di Exchange Server 2007 non possono continuare il tentativo di installare il ruolo del server Server accesso Client, il ruolo del server cassette postali o gli strumenti di amministrazione di Exchange 2007 nei sistemi operativi Windows seguenti:

  - Windows Server 2008 R2

  - Windows Server 2008

  - Windows 7 (strumenti di amministrazione solo)

  - Windows Vista (strumenti di amministrazione solo)

Questo problema si verifica perché non sono installati i componenti di compatibilità Metabase di Internet Information Server (IIS) 6 e la Console di gestione IIS 6.

Installazione di Exchange 2007 è necessario che il computer in cui si sta installando il ruolo del server Accesso Client di Exchange 2007, il ruolo del server cassette postali o gli strumenti di amministrazione di Exchange 2007 con il componente di compatibilità Metabase di IIS 6 e installato il componente di IIS 6 Management Console.

Per risolvere questo problema, installare il componente di compatibilità Metabase di IIS 6 nel computer di destinazione e quindi rieseguire il programma di installazione di Microsoft Exchange.

Installare i componenti di compatibilità IIS 6.0 Management in Windows Server 2008 R2 o Windows Server mediante lo strumento Server Manager

1.  Fare clic sul pulsante **Start**, scegliere **Strumenti di amministrazione** e quindi **Server Manager**.

2.  Nel riquadro di spostamento espandere **ruoli**, destro del mouse sul **Server Web (IIS)** e quindi fare clic su **Aggiungi servizi ruolo**.

3.  Nel riquadro **Selezione servizi ruolo**, scorrere verso il basso per **Compatibilità Gestione IIS 6**.

4.  Fare clic per selezionare le caselle di controllo **Compatibilità Metabase di IIS 6**, **Compatibilità WMI con IIS 6** e **IIS 6 Management Console**.

5.  Nel riquadro **Selezione servizi ruolo** fare clic su **Avanti**.

6.  Nel riquadro **Conferma selezioni** fare clic su **Installa**.

7.  Fare clic su **Chiudi** per chiudere la procedura guidata Aggiunta servizi ruolo.

Installare i componenti di compatibilità IIS 6.0 Management in Windows 7 o Windows Vista dal Pannello di controllo

1.  Fare clic su **Start**, scegliere **Pannello di controllo**, fare clic su **programmi e funzionalità** e quindi fare clic su **funzionalità di Windows attivare o disattivare**.

2.  Aprire **Internet Information Services**.

3.  Aprire **Strumenti di gestione Web**.

4.  Aprire **6.0 Management Compatibility di IIS**.

5.  Fare clic per selezionare le caselle di controllo **compatibilità Metabase di IIS 6 e IIS 6 configurazione**, **Compatibilità WMI con IIS 6** e **IIS 6 Management Console**.

6.  Fare clic su **OK**.

