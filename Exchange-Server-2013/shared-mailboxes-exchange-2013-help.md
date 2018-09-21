---
title: 'Cassette postali condivise: Exchange 2013 Help'
TOCTitle: Cassette postali condivise
ms:assetid: 1d71c01b-e261-408e-a633-1d1c9d00032a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150498(v=EXCHG.150)
ms:contentKeyID: 50480172
ms.date: 01/02/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cassette postali condivise

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-06-04_

Informazioni sulla cassetta postale condivisa di Exchange in Microsoft Exchange Server 2013, sui motivi per utilizzarla e su come convertire una cassetta postale delegata in una cassetta postale condivisa di Exchange.

Una cassetta postale condivisa è una cassetta postale che può essere utilizzata da più utenti per leggere e inviare messaggi di posta elettronica. Le cassette postali condivise possono essere utilizzate anche per fornire un calendario comune, permettendo a più utenti di pianificare e visualizzare i periodi di vacanza e i turni di lavoro.

Le cassette postali condivise non sono supportate sui dispositivi mobili.

**Di seguito sono indicati i motivi per cui configurare una cassetta postale condivisa?**

  - Fornisce un indirizzo di posta elettronica generico (ad esempio info@contoso.com o sales@contoso.com), che può essere utilizzato dai clienti per ottenere informazioni sull'azienda.

  - Consente al personale dei reparti che forniscono servizi centralizzati ai dipendenti (ad esempio i reparti assistenza, risorse umane o servizi stampa) di rispondere alle domande dei dipendenti.

  - Permette a più utenti di monitorare e rispondere ai messaggi di posta elettronica inviati a un indirizzo di posta elettronica (ad esempio un indirizzo utilizzato in modo specifico dal servizio assistenza).

## Informazioni sulle cassette postali condivise

Una cassetta postale condivisa è un tipo di cassetta postale utente priva di un suo proprio nome utente e password. Come risultato, gli utenti non possono accedervi direttamente. Per accedere ad una cassetta postale condivisa, agli utenti devono prima essere concesse le autorizzazioni Invia come o Accesso completo per la cassetta postale. Successivamente, gli utenti accedono alla propria cassetta postale poi accedono alla cassetta postale condivisa aggiungendola al proprio profilo Outlook. In Exchange 2003 e versioni precedenti, le cassette postali condivise erano una cassetta postale standard a cui l'amministratore poteva concedere l'accesso delegato. A partire da Exchange 2007, le cassette postali condivise sono diventate un tipo di destinatario a sé stante:

  - **RecipientType:**  UserMailbox

  - **RecipientTypeDetails:**  SharedMailbox

Nelle versioni precedenti di Exchange, la creazione di una cassetta postale condivisa era un processo in più fasi in cui era necessario utilizzare Exchange Management Shell per completare alcune delle attività. In Exchange 2013, si può utilizzare l'interfaccia di amministrazione di Exchange (EAC) per creare una cassetta postale condivisa in un solo passaggio. Per ulteriori informazioni, vedere [Creazione di una cassetta postale condivisa](create-a-shared-mailbox-exchange-2013-help.md). L'interfaccia di amministrazione di Exchange dispone di un'area funzionalità dedicata completamente alle cassette postali condivise. È sufficiente andare a **Destinatari** \> **Cassette postali condivise** per visualizzare tutte le attività relative alle cassette postali condivise.

È possibile utilizzare le seguenti autorizzazioni con una cassetta postale condivisa.

  - **Accesso completo**   L'autorizzazione Accesso completo consente all'utente di accedere alla cassetta postale condivisa e agire come proprietario di tale cassetta postale. Dopo aver eseguito l'accesso alla cassetta postale condivisa, l'utente può creare voci di calendario, leggere, visualizzare, eliminare e modificare messaggi di posta elettronica, creare attività e contatti. Un utente con autorizzazione Accesso completo non può tuttavia inviare messaggi di posta elettronica dalla cassetta postale condivisa, a meno che non disponga anche dell'autorizzazione Invia come o Invia per conto di.

  - **Invia come** L'autorizzazione Invia come consente a un utente di rappresentare la cassetta postale per l'invio della posta elettronica. Se ad esempio Kweku accede alla cassetta postale condivisa del reparto marketing e invia un messaggio di posta elettronica, tale messaggio verrà visualizzato come inviato dal reparto marketing.

  - **Invia per conto di** L'autorizzazione Invia per conto di consente a un utente di inviare messaggi di posta elettronica per conto della cassetta postale condivisa. Se ad esempio John accede alla cassetta postale dell'edificio reception 32 e invia un messaggio di posta elettronica, i destinatari visualizzeranno tale messaggio come inviato da "John per conto dell'edificio reception 32". Non è possibile utilizzare EAC per concedere l'autorizzazione Invia per conto di. A tale fine è necessario utilizzare il [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) cmdlet con il parametro *GrantSendonBehalf*.

## Conversione delle cassette postali condivise

Nelle versioni precedenti di Exchange, si poteva utilizzare una cassetta postale standard come cassetta postale delegata. Se si dispone di cassette postali delegate, si può utilizzare Shell per convertire quelle cassette postali delegate in cassette postali condivise. Per ulteriori informazioni, vedere [Conversione di una cassetta postale](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-user-mailboxes/convert-a-mailbox).

