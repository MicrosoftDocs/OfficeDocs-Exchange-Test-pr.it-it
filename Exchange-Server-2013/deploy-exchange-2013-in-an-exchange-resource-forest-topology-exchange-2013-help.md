---
title: 'Distribuzione di Exchange 2013 in una topologia a foresta risorsa Exchange: Exchange 2013 Help'
TOCTitle: Distribuzione di Exchange 2013 in una topologia a foresta risorsa Exchange
ms:assetid: 537a7b2b-d002-40a6-84ae-fd02635f9e23
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998031(v=EXCHG.150)
ms:contentKeyID: 51407364
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Distribuzione di Exchange 2013 in una topologia a foresta risorsa Exchange

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento viene illustrato come distribuire Microsoft Exchange 2013 in una topologia a foresta risorsa Exchange. Un insieme di strutture dedicato Exchange è l'acronimo di una foresta di risorse Exchange. In questo argomento si presuppone che non si dispone di una topologia Exchange 2013 esistente.

Nella figura riportata di seguito viene mostrata un'organizzazione di Exchange con una foresta di risorse.

**Esempio di un'organizzazione di Exchange con una foresta di risorse di Exchange**

![Organizzazione di Exchange complessa con foresta di risorse](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "Organizzazione di Exchange complessa con foresta di risorse")

## Che cosa è necessario sapere prima di iniziare

Per eseguire la procedura seguente in Exchange 2013, verificare di che disporre di quanto segue:

  - Sono disponibili le due foreste di Active Directory riportate di seguito:
    
      - Una foresta contiene gli account utente per l'organizzazione. In questa procedura, la foresta è denominata *foresta degli account*.
    
      - Un insieme di strutture non contiene gli account utente e non sono ancora disponibili Exchange installato. In questa procedura foresta viene chiamata la *foresta di Exchange*. Utilizzare la procedura per installare Exchange 2013 nella foresta.

  - È stato configurato correttamente sistema DNS (Domain Name) per la risoluzione dei nomi tra foreste all'interno dell'organizzazione. Per verificare di aver DNS configurato correttamente, eseguire il ping ogni foresta dalle altre foreste o insiemi di strutture all'interno dell'organizzazione. Per ulteriori informazioni sulla configurazione di DNS, vedere la [Guida operativa di server DNS](https://go.microsoft.com/fwlink/p/?linkid=282295).

## Distribuzione di Exchange 2013 in una topologia di foresta di risorse di Exchange

1.  Un controller di dominio nella foresta Exchange, creare una relazione di trust unidirezionale in uscita in modo che la foresta Exchange considera attendibile la foresta di account. Per ulteriori informazioni, vedere [creare un trust unidirezionale in uscita, per entrambi i lati della relazione di trust](https://go.microsoft.com/fwlink/p/?linkid=69130).
    

    > [!NOTE]
    > Sebbene sia consigliabile creare un trust tra foreste, è possibile creare sia un trust tra foreste sia un trust esterno. Se si crea un trust esterno, durante la creazione di cassette postali collegate nel Passaggio&nbsp;3, nella pagina <STRONG>Account principale</STRONG> della Creazione guidata nuova cassetta postale è necessario specificare un account utente che può accedere al controller di dominio nella foresta trusted. Non è possibile utilizzare le credenziali con cui è stato eseguito l'accesso. Se si creano cassette postali collegate utilizzando il cmdlet <STRONG>New-Mailbox</STRONG>, è necessario specificare un account utente che possa accedere al controller di dominio nella foresta trusted utilizzando il parametro <EM>LinkedCredential</EM>.



2.  Nella foresta Exchange installare Exchange 2013. Installare Exchange allo stesso modo venisse eseguita nello scenario relativo a una singola foresta. Per ulteriori informazioni su come installare Exchange 2013, vedere uno degli argomenti seguenti:
    
      - [Distribuire una nuova installazione di Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)
    
      - [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

3.  Nella foresta Exchange per ogni utente nella foresta di account che dispone di una cassetta postale nella foresta di Exchange creare una cassetta postale è associata a un account esterno. Per ulteriori informazioni, vedere [Gestire le cassette postali collegate](manage-linked-mailboxes-exchange-2013-help.md).

