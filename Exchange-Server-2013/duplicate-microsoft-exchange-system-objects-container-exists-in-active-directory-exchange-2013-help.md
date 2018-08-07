---
title: 'Contenitore Microsoft Exchange System Objects dupl. in AD: Exchange 2013 Help'
TOCTitle: Contenitore di Microsoft Exchange System Objects duplicati esiste in Active Directory
ms:assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.adiniterrorrule(v=EXCHG.150)
ms:contentKeyID: 50481725
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Contenitore di Microsoft Exchange System Objects duplicati esiste in Active Directory

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2013-02-18_

L'installazione di Microsoft Exchange Server 2013 non può continuare perché è stato rilevato un contenitore Oggetti di sistema di Microsoft Exchange duplicato nel contesto dei nomi di dominio di Active Directory. Quando in fase di installazione viene duplicato un contenitore Oggetti di sistema di Microsoft Exchange duplicato, è necessario eliminare il contenitore prima di poter proseguire con l'installazione. Se esiste un contenitore Oggetti di sistema di Microsoft Exchange duplicato, non è possibile risolvere il problema eseguendo di nuovo **DomainPrep**. È necessario identificare ed eliminare il contenitore duplicato.

Per risolvere il problema, procedere come segue:

1.  Accedere al controller di dominio con credenziali amministrative.

2.  In **Strumenti di amministrazione**, fare clic su **Utenti e computer di Active Directory**.

3.  Nel riquadro della console di gestione **Utenti e computer di Active Directory**, dal menu della barra degli strumenti fare clic su **Visualizza** e scegliere **Avanzate**.

4.  Individuare il contenitore Oggetti di sistema di Microsoft Exchange duplicato.

5.  Verificare in tale contenitore non siamo presenti oggetti di Active Directory validi.

6.  Fare clic con il pulsante destro del mouse sul contenitore e scegliere **Elimina**.

7.  Confermare l'eliminazione facendo clic su **Sì** nella finestra di dialogo di Active Directory.


> [!NOTE]
> Se si desidera che la modifica venga immediatamente replicata, è necessario avviare manualmente la replica tra i controller di dominio.



Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.

