---
title: 'Creazione di una cassetta postale condivisa: Exchange 2013 Help'
TOCTitle: Creazione di una cassetta postale condivisa
ms:assetid: d34bc827-1e83-4a7f-a219-8ba9c19fe24b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150570(v=EXCHG.150)
ms:contentKeyID: 50481753
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creazione di una cassetta postale condivisa

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**Ultima modifica dell'argomento:** 2016-12-09_

**Tempo stimato per il completamento: 5 minuti**

Cassette postali condivise semplifica per un gruppo di persone nella società per monitorare e inviare la posta elettronica da un account comune, ad esempio info@contoso.com o support@contoso.com. Quando una persona nel gruppo risponde a un messaggio inviato per la cassetta postale condivisa, il posta elettronica probabilmente è stato inviato per la cassetta postale condivisa non da singoli utenti.


> [!IMPORTANT]
> Se si utilizza Office 365 per aziende, è consigliabile creare la cassetta postale condivisa nell'interfaccia di amministrazione di Office 365. 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=834766">Creare cassette postali condivise in Office 365</A></P></LI></UL>



Se l'organizzazione utilizza un ambiente ibrido di Exchange, è consigliabile utilizzare l'interfaccia di amministrazione di Exchange locale (EAC) per creare e gestire le cassette postali condivise. Per ulteriori informazioni sulle cassette postali condivise, vedere [Cassette postali condivise](shared-mailboxes-exchange-2013-help.md).

## Creazione di una cassetta postale condivisa tramite EAC

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Cassette postali utenti" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

1.  Accedere a **Destinatari** \> **Condivisa** \> **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Compilare i campi obbligatori:
    
      - **Nome visualizzato**
    
      - **Indirizzo di posta elettronica**

3.  Per concedere le autorizzazioni Accesso completo o Invia come, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"), quindi selezionare gli utenti a cui si desidera concedere le autorizzazioni. È possibile utilizzare il tasto **CTRL** per selezionare più utenti. In caso di dubbi su quali autorizzazioni utilizzare, vedere Which permission should you use? più avanti in questo argomento.
    

    > [!NOTE]
    > L'autorizzazione Accesso completo consente a un utente di aprire la cassetta postale, modificare gli elementi in essa contenuti e crearne di nuovi. L'autorizzazione Invia come consente a utenti diversi dal proprietario della cassetta postale di inviare messaggi di posta elettronica dalla cassetta postale condivisa. Entrambe le autorizzazioni sono necessarie per il funzionamento corretto della cassetta postale condivisa.



4.  Fare clic su **Salva** per salvare le modifiche e creare la cassetta postale condivisa.

## Utilizzo dell'interfaccia di amministrazione di Exchange per modificare la delega dell'accesso alle cassette postali

1.  Accedere a **Destinatari** \> **Condivisa** \> **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Fare clic su **Delega cassette postali**

3.  Per concedere o rimuovere le autorizzazioni Accesso completo o Invia come, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") o **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi"), quindi selezionare gli utenti a cui si desidera concedere le autorizzazioni.
    

    > [!NOTE]
    > L'autorizzazione Accesso completo consente a un utente di aprire la cassetta postale, modificare gli elementi in essa contenuti e crearne di nuovi. L'autorizzazione Invia come consente a utenti diversi dal proprietario della cassetta postale di inviare messaggi di posta elettronica dalla cassetta postale condivisa. Entrambe le autorizzazioni sono necessarie per il funzionamento corretto della cassetta postale condivisa.



4.  Fare clic su **Salva** per salvare le modifiche.

## Utilizzare una cassetta postale condivisa

Per informazioni su come gli utenti possono accedere e utilizzare cassette postali condivise, vedere quanto segue:

  - [Aprire e utilizzare una cassetta postale condivisa in 2016 Outlook e Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=834764)

  - [Aprire e utilizzare una cassetta postale condivisa in Outlook sul web per le aziende](https://go.microsoft.com/fwlink/p/?linkid=834766)

## Creazione di una cassetta postale condivisa tramite Shell

Con questo esempio viene creata la cassetta postale condivisa Sales Department e vengono concesse le autorizzazioni Accesso completo e Invia per conto di per il gruppo di protezione MarketingSG. Agli utenti membri del gruppo di protezione verranno concesse le autorizzazioni per la cassetta postale.


> [!NOTE]
> In questo esempio si presuppone che sia già stato creato il gruppo di sicurezza MarketingSG e che tale gruppo sia abilitato all'utilizzo della posta. Vedere <A href="manage-mail-enabled-security-groups-exchange-2013-help.md">Gestire gruppi di sicurezza abilitati alla posta elettronica</A>.



    New-Mailbox -Shared -Name "Sales Department" -DisplayName "Sales Department" -Alias Sales | Set-Mailbox -GrantSendOnBehalfTo MarketingSG | Add-MailboxPermission -User MarketingSG -AccessRights FullAccess -InheritanceType All

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-Mailbox](https://technet.microsoft.com/it-it/library/aa997663\(v=exchg.150\)).

## Autorizzazioni da utilizzare

È possibile utilizzare le seguenti autorizzazioni con una cassetta postale condivisa.

  - **Accesso completo**   L'autorizzazione Accesso completo consente all'utente di accedere alla cassetta postale condivisa e agire come proprietario di tale cassetta postale. Dopo aver eseguito l'accesso alla cassetta postale condivisa, l'utente può creare voci di calendario, leggere, visualizzare, eliminare e modificare messaggi di posta elettronica, creare attività e contatti. Un utente con autorizzazione Accesso completo non può tuttavia inviare messaggi di posta elettronica dalla cassetta postale condivisa, a meno che non disponga anche dell'autorizzazione Invia come o Invia per conto di.

  - **Invia come** L'autorizzazione Invia come consente a un utente di rappresentare la cassetta postale per l'invio della posta elettronica. Se ad esempio Kweku accede alla cassetta postale condivisa del reparto marketing e invia un messaggio di posta elettronica, tale messaggio verrà visualizzato come inviato dal reparto marketing.

  - **Invia per conto di** L'autorizzazione Invia per conto di consente a un utente di inviare messaggi di posta elettronica per conto della cassetta postale condivisa. Se ad esempio John accede alla cassetta postale dell'edificio reception 32 e invia un messaggio di posta elettronica, i destinatari visualizzeranno tale messaggio come inviato da "John per conto dell'edificio reception 32". Non è possibile utilizzare EAC per concedere l'autorizzazione Invia per conto di. A tale fine è necessario utilizzare il [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) cmdlet con il parametro *GrantSendonBehalf*.

## Ulteriori informazioni

Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


