---
title: 'Imp. trovare record Host computer locale in database DNS: Exchange 2013 Help'
TOCTitle: Impossibile trovare il record Host per il computer locale nel database DNS
ms:assetid: 2f18cb65-29fe-4b72-8d68-52fd503d5673
ms:mtpsurl: https://technet.microsoft.com/it-it/library/ms.exch.setupreadiness.hostrecordmissing(v=EXCHG.150)
ms:contentKeyID: 50480257
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impossibile trovare il record Host per il computer locale nel database DNS

 

_**Si applica a:** Exchange Server_

_**Ultima modifica dell'argomento:** 2016-12-09_

L'installazione di Microsoft Exchange Server 2013 non può continuare. Impossibile trovare il record Host (A) per il computer nel database DNS (Domain Name System).

Per l'installazione di Exchange 2013 è necessario che il computer locale abbia un record HOST (A) valido registrato con il database DNS autorevole per il dominio.

Exchange dipende dai record Host DNS (A) per l'indirizzo IP del successivo server di destinazione interno o esterno.

Per risolvere questo problema:

  - Verificare che la configurazione di TCP/IP locale punti al server DNS appropriato. Per ulteriori informazioni, vedere [impostazioni TCP/IP configurare](https://go.microsoft.com/fwlink/p/?linkid=108281).

  - Utilizzare Nslookup.exe per verificare l'esistenza di record Host (A) nel server DNS. Per ulteriori informazioni, vedere [per verificare una risorsa in DNS siano presenti record](https://go.microsoft.com/fwlink/?linkid=63001).

Per informazioni sulla risoluzione dei nomi DNS, la risoluzione dei problemi e i record Host (A), vedere le seguenti risorse:

  - [Risoluzione dei problemi relativi a DNS](https://go.microsoft.com/fwlink/p/?linkid=294828)

  - [Gestione dei record di risorse](https://go.microsoft.com/fwlink/p/?linkid=294829)

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La ricerca ha prodotto i risultati desiderati? [Inviare un commento a Microsoft](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) indicando le informazioni desiderate.

