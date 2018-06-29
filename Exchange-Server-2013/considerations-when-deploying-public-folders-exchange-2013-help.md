---
title: 'Considerazioni sulla distribuzione delle cartelle pubbliche: Exchange 2013 Help'
TOCTitle: Considerazioni sulla distribuzione delle cartelle pubbliche
ms:assetid: 2e416eed-b88f-45db-a482-1232fd2610fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn957481(v=EXCHG.150)
ms:contentKeyID: 65012468
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Considerazioni sulla distribuzione delle cartelle pubbliche

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-07-12_

Sebbene esistano numerosi vantaggi dell'utilizzo delle cartelle pubbliche di Exchange 2013, esistono alcuni aspetti da considerare prima di implementarle nell'organizzazione.

## Considerazioni sulla distribuzione per le cartelle pubbliche

In questo articolo sono i fattori da considerare prima di distribuire le cartelle pubbliche nell'organizzazione, soprattutto se si prevede di disporre di un numero elevato di cartelle pubbliche. Exchange 2013 supporta fino a 1 milione di cartelle pubbliche.

  - Attività in una cartella pubblica un impatto significativo sul direttamente il carico che viene inserito nella cassetta postale di cartelle pubbliche in cui si trova la cartella. Per evitare problemi di connettività client, ad esempio latenza elevata o l'impossibilità di accedere a una cartella pubblica, è consigliabile che eseguire le operazioni seguenti:
    
      - Non consentire a cassette postali delle cartelle pubbliche di superare il 50% del limite di dimensione della cassetta postale. In questo caso è consigliabile utilizzare lo script `Split-PublicFolderMailbox.ps1` disponibile nella cartella C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts sul server Exchange 2013 per spostare alcune cartelle pubbliche in una nuova cassetta postale di cartelle pubbliche.
    
      - È consigliabile spostare le cartelle pubbliche utilizzati frequentemente per una cassetta postale di cartelle pubbliche dedicato.
    
      - Escludere le cartelle pubbliche utilizzati frequentemente da rendere disponibili gerarchia delle cartelle pubbliche. È possibile eseguire questo impostando la proprietà *IsExcludedFromServingHierarchy* della cassetta postale cartelle pubbliche utilizzando i cmdlet **Set-Mailbox** .
    
      - Per organizzazioni di grandi dimensioni con numero di cartelle pubbliche, è consigliabile aggiungere cassette postali di cartelle pubbliche aggiuntive per la distribuzione del carico delle richieste di gerarchia di cartelle pubbliche.

  - Effettuare la cassetta postale di cartelle pubbliche primaria in un gruppo DAG per aumentare la disponibilità della cassetta postale. La cassetta postale di cartelle pubbliche primaria è copia autorevole della gerarchia di cartelle pubbliche.

  - Posizionare le cassette postali di cartelle pubbliche secondaria in un gruppo DAG o eseguire il backup di cassette postali domande.

  - Posizionare le cassette postali di cartelle pubbliche nella posizione geografica più vicino agli utenti che accedono al contenuto delle cartelle pubbliche in essi.

  - Migliorare i tempi di accesso di gerarchia di cartelle pubbliche utilizzando la proprietà DefaultPublicFolderMailbox per le cassette postali degli utenti per specificare una cassetta postale di cartelle pubbliche in prossimità di esse. Ciò impedisce gli utenti di recupero della gerarchia di cartelle pubbliche da una cassetta postale di cartelle pubbliche in altre aree geografiche.

  - Nelle distribuzioni con oltre 50 cassette postali delle cartelle pubbliche secondarie, è consigliabile non memorizzare il contenuto delle cartelle pubbliche nella cassetta postale delle cartelle pubbliche primaria. Si dedica alla cassetta postale di cartelle pubbliche primaria alla sincronizzazione della gerarchia con le cassette postali di cartelle pubbliche secondaria.

  - Exchange 2013 non supporta più database delle cartelle pubbliche. Di conseguenza, gli utenti di Outlook Web App con le cassette postali di Exchange 2013 non potranno accedere alle cartelle pubbliche di Exchange 2010 o Exchange 2007. Gli utenti di Exchange 2013 possono accedere alle cartelle pubbliche di Exchange 2010 o Exchange 2007 utilizzando Outlook o Outlook per Mac.

  - Outlook Web App è supportato, ma con limitazioni. È possibile aggiungere e rimuovere cartelle pubbliche preferite ed eseguire operazioni a livello di elemento, ad esempio la creazione e l'eliminazione di post, nonché la risposta ai post. Tuttavia, non è possibile creare o eliminare cartelle pubbliche da Outlook Web App. Inoltre, solo le cartelle pubbliche Posta, Post, Calendario e Contatti possono essere aggiunte all'elenco dei preferiti in Outlook Web App.

  - Sebbene sia possibile eseguire una ricerca di testo completo del contenuto della cartella pubblica, questo non può essere ricercato in cartelle pubbliche e il contenuto non è indicizzato da Ricerca di Exchange.

  - È necessario utilizzare Outlook 2007 o versione successiva per accedere alle cartelle pubbliche su server Exchange 2013.

  - I criteri di conservazione non sono supportati per le cassette postali delle cartelle pubbliche.

