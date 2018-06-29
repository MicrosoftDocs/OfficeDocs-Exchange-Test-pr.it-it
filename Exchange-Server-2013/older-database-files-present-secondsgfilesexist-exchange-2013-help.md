---
title: 'Meno recente present_SecondSGFilesExist i file di database: Exchange 2013 Help'
TOCTitle: Meno recente present_SecondSGFilesExist i file di database
ms:assetid: fe2908e7-df8b-4f35-946a-cfbf8521e93a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.secondsgfilesexist(v=EXCHG.150)
ms:contentKeyID: 50482097
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Meno recente present\_SecondSGFilesExist i file di database

 

_**Si applica a:**Exchange Server_

_**Ultima modifica dell'argomento:**2012-06-05_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Non può continuare l'installazione di Microsoft® Exchange Server 2007 è stato rilevato file di database di Microsoft Exchange esistenti nel percorso di installazione di destinazione.

Installazione di Exchange 2007 è necessario che il percorso di installazione di destinazione sia vuoto dei file di database di Microsoft Exchange.

Per risolvere questo problema, rimuovere tutti i file esistenti da percorsi di installazione di destinazione e quindi rieseguire il programma di installazione.

Per eliminare i file di database di Exchange Server esistenti dal percorso di installazione di destinazione

1.  Nel Computer locale o in Esplora risorse, individuare il percorso di installazione di destinazione.
    

    > [!NOTE]
    > Per impostazione predefinita, i file di database si trovano:<BR>&lt; unitàsistema &gt;: \Program Server\Mailbox\First gruppo di archiviazione.



2.  Fare clic sui file da rimuovere e quindi scegliere **Elimina**.

3.  La finestra di dialogo **Conferma eliminazione File**, fare clic su **Sì**.

4.  Ripetere i passaggi 2 e 3 per tutti i file nei percorsi di installazione di destinazione.

