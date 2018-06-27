---
title: 'Indirizzi SMTP in formato non Supported_SMTPAddressLiteral: Exchange 2013 Help'
TOCTitle: Indirizzi SMTP in formato non Supported_SMTPAddressLiteral
ms:assetid: b8b55917-d81f-4c0a-ad65-7bb10ac58df8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.smtpaddressliteral(v=EXCHG.150)
ms:contentKeyID: 50481527
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Indirizzi SMTP in formato non Supported\_SMTPAddressLiteral

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Perché il criterio destinatario specificato viene utilizzato un formato di indirizzo Simple Mail Transfer Protocol (SMTP) non supportato, non può continuare l'installazione di Microsoft Exchange Server 2007 ed Exchange Server 2010.

Il programma di installazione di Exchange 2007 ed Exchange 2010 richiede che tutti gli indirizzi SMTP utilizzati per i criteri degli indirizzi di posta elettronica non contengono valori letterali indirizzo IP, ad esempio: *user@\[10.10.1.1\]*.

Per risolvere questo problema, modificare il valore dell'indirizzo SMTP nel criterio destinatario in modo che non contiene un indirizzo IP letterale. Sostituire numeri (10.10.1.1) dell'indirizzo IP letterale e parentesi quadre (\[\]) con il formato di denominazione del sistema DNS (Domain Name), ad esempio: *user@contoso.com*, quindi eseguire nuovamente il programma di installazione di Exchange.

Per ulteriori informazioni sulla gestione dei criteri relativi ai destinatari in Exchange Server 2007, vedere "Gestione di posta elettronica criteri degli indirizzi" ([https://go.microsoft.com/fwlink/?LinkId=86653](https://go.microsoft.com/fwlink/?linkid=86653)).

Per ulteriori informazioni sulla gestione dei criteri relativi ai destinatari in Exchange Server 2010, vedere "Gestione di posta elettronica criteri degli indirizzi" ([https://go.microsoft.com/fwlink/?LinkId=179519](https://go.microsoft.com/fwlink/?linkid=179519)).

