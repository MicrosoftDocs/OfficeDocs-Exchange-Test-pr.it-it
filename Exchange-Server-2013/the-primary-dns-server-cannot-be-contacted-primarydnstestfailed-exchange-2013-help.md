---
title: 'Server DNS primario non può essere contacted_PrimaryDNSTestFailed: Exchange 2013 Help'
TOCTitle: Server DNS primario non può essere contacted_PrimaryDNSTestFailed
ms:assetid: 5b39cb64-c8f1-4fd3-843b-ecd23f99fe3a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.primarydnstestfailed(v=EXCHG.150)
ms:contentKeyID: 50480750
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Server DNS primario non può essere contacted\_PrimaryDNSTestFailed

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

Il contenuto di questo argomento non è stato aggiornato per Microsoft Exchange Server 2013. Sebbene non sia stato aggiornato, può comunque essere applicabile anche a Exchange 2013. In caso di problemi, consultare le risorse della community riportate di seguito.

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Non può continuare l'installazione di Microsoft® Exchange Server 2007 non è possibile stabilire la comunicazione con il server principale del sistema DNS (Domain Name).

Installazione di Exchange 2007 è necessario che nel computer locale di comunicare con il database DNS rilevante per il dominio.

Microsoft Exchange dipende dal DNS per risolvere l'indirizzo IP del server di destinazione interni o esterni successivo.

Comunicazione con i server DNS primario può non riuscire per i motivi seguenti:

  - Configurazione di TCP/IP locale non si riferisce al server DNS appropriato.

  - Server DNS è inattivo o non raggiungibile a causa di un errore di rete o per altri motivi.

Per risolvere questo problema:

  - Verificare che la configurazione di TCP/IP locale punti al server DNS appropriato.

Per verificare la configurazione di TCP/IP locale

1.  Esaminare la configurazione di TCP/IP locale:
    
    Per ulteriori informazioni, vedere "Configurare TCP/IP da utilizzare DNS" ([https://go.microsoft.com/fwlink/?LinkId=68094](https://go.microsoft.com/fwlink/?linkid=68094)).

<!-- end list -->

  - Verificare che il server DNS sia in esecuzione e può essere contattato.

Per verificare che il server DNS sia in esecuzione e può essere contattato

1.  Verificare che il server DNS sia in esecuzione eseguendo una o più dei seguenti controlli:
    
      - Esaminare lo stato del server DNS dal programma di amministrazione DNS nel server DNS.
    
      - Riavviare il server DNS.
        
        Per ulteriori informazioni, vedere "Start, stop, sospendere o riavviare un server DNS" ([https://go.microsoft.com/fwlink/?LinkId=62999](https://go.microsoft.com/fwlink/?linkid=62999)).
    
      - Verificare i tempi di risposta di server DNS utilizzando il comando **nslookup**.
        
        Per ulteriori informazioni, vedere le istruzioni in "Verificare che il comando nslookup velocità di risposta dei server DNS" ([https://go.microsoft.com/fwlink/?LinkId=63000](https://go.microsoft.com/fwlink/?linkid=63000)).

