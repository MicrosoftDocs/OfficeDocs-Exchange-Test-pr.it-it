---
title: 'Il nome di dominio completo del computer corrisponde a un destinatario policy_ServerFQDNMatchesSMTPPolicy: Exchange 2013 Help'
TOCTitle: Il nome di dominio completo del computer corrisponde a un destinatario policy_ServerFQDNMatchesSMTPPolicy
ms:assetid: f3ea61f8-1788-4cbf-814e-f7c088c1ac47
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.serverfqdnmatchessmtppolicy(v=EXCHG.150)
ms:contentKeyID: 50482040
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Il nome di dominio completo del computer corrisponde a un destinatario policy\_ServerFQDNMatchesSMTPPolicy

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Non può continuare l'installazione di Microsoft® Exchange Server 2007 perché il nome di dominio completo (FQDN) del computer locale corrisponde all'indirizzo Simple Mail Transfer Protocol (SMTP) di un criterio destinatario.

Il programma di installazione di Microsoft Exchange richiede che il nome FQDN del server in un'organizzazione di Exchange non corrispondono tutti gli indirizzi SMTP dei criteri relativi ai destinatari nella stessa organizzazione di Exchange.

Se il nome di dominio COMPLETO di un computer corrisponde all'indirizzo SMTP di un criterio destinatario, tale corrispondenza può causare la posta elettronica SMTP il failover ed essere bloccata nelle code di agente di trasferimento Messaggi.

Per risolvere questo problema, rinominare il computer locale o rimuovere o rinominare il criterio destinatario e rieseguire il programma di installazione di Microsoft Exchange.

Per rinominare il computer locale

1.  Aprire **sistema** nel **Pannello di controllo**.

2.  Nella scheda **Nome computer** fare clic su **Cambia** .

3.  Sotto il **nome del Computer**, digitare un nuovo nome per il computer e quindi fare clic su **OK**. Verrà chiesto di specificare un nome utente e password dell'utente per rinominare il computer nel dominio.

4.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà del sistema**. Verrà richiesto di riavviare il computer per applicare le modifiche.


> [!IMPORTANT]
> Se il computer in cui si desidera rinominare è un controller di dominio, vedere "Rinominare un controller di dominio" (<A href="https://go.microsoft.com/fwlink/?linkid=66828">https://go.microsoft.com/fwlink/?LinkId=66828</A>).



Per modificare il criterio indirizzo SMTP del destinatario

1.  Avviare Exchange System Manager.

2.  Fare clic su **organizzazione**, fare clic su **destinatari** e quindi fare clic su **Recipient Policies**.

3.  Fare doppio clic sul criterio che si desidera modificare.

4.  Fare clic sulla scheda **Indirizzi di posta elettronica** e quindi modificare l'indirizzo SMTP appropriato

Per ulteriori informazioni sui problemi di denominazione criterio destinatario, vedere l'articolo della Microsoft Knowledge Base 288175 "XCON: criterio destinatario non può corrispondere al nome FQDN di un Server nell'organizzazione, 5.4.8 rapporti di mancato recapito" ([http://go.microsoft.com/fwlink/?linkid=3052\&kbid=288175](http://go.microsoft.com/fwlink/?linkid=3052&kbid=288175)).

