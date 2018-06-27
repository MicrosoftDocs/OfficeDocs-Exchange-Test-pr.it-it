---
title: 'Suffisso DNS primario manca: Exchange 2013 Help'
TOCTitle: Suffisso DNS primario manca
ms:assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.fqdnmissing(v=EXCHG.150)
ms:contentKeyID: 61202265
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suffisso DNS primario manca

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2014-01-15_

Microsoft Exchange Server 2013 il programma di installazione non può proseguire perché non è stato configurato il primario (DNS) il suffisso DNS per il computer che si sta installando Exchange su.

Per risolvere questo problema, aggiungere un suffisso DNS primario del computer utilizzando la procedura seguente e quindi eseguire nuovamente l'installazione.


> [!IMPORTANT]
> Modifica del nome del computer o il suffisso DNS primario dopo l'installazione di Exchange 2013 non è supportata.



1.  Accedere al computer in cui si desidera installare il ruolo Trasporto Edge come un utente membro del gruppo Amministratori locale.

2.  Aprire il **Pannello di controllo** e fare doppio clic su **Sistema**.

3.  Nella sezione **Impostazioni relative a nome computer, dominio e gruppo di lavoro**, fare clic su **Cambia impostazioni**.

4.  Nella finestra **Proprietà del sistema**, assicurarsi che la scheda **Nome computer** sia selezionata e quindi fare clic su **Modifica…**.

5.  Nella pagina **Cambiamenti dominio/nome computer** fare clic su **Altro...**.

6.  In **Suffisso DNS primario del computer**, immettere il nome dominio DNS per il server Trasporto Edge. Ad esempio, contoso.com.

7.  Fare clic su **OK** per chiudere ciascuna finestra.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.

