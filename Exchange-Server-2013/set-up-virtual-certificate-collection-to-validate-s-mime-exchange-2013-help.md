---
title: 'Impostare raccolta di certificati virtuali per convalidare S/MIME: Exchange 2013 Help'
TOCTitle: Impostare raccolta di certificati virtuali per convalidare S/MIME
ms:assetid: 04a616e6-197c-490c-ae8c-c8d5f0f0b3dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn626155(v=EXCHG.150)
ms:contentKeyID: 61213862
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare raccolta di certificati virtuali per convalidare S/MIME

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Come amministratore tenant, l'utente dovrà configurare una raccolta di certificati virtuali che verranno utilizzati per convalidare i certificati S/MIME. La raccolta di certificati virtuali viene configurata come un tipo di file di archivio dei certificati con un'estensione del nome file SST. Il file SST contiene tutti i certificati radice e intermedi utilizzati durante la convalida del certificato S/MIME.

## Creare e salvare un SST

È possibile utilizzare solo Shell per eseguire questa procedura. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)). Per informazioni su come usare Windows PowerShell per connettersi a Exchange Online, vedere [Connessione a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

In qualità di amministratore, è possibile creare il file SST esportando i certificati da un computer attendibile utilizzando il cmdlet `Export-Certificate` e specificando il tipo come SST. Per ulteriori informazioni cmdlet `Export-Certificate` , vedere l'argomento della Guida di riferimento [Esporta certificato](https://technet.microsoft.com/en-us/library/hh848628.aspx) .

Una volta che il file SST viene generato, utilizzare il cmdlet `Set-Smimeconfig` per salvarlo nell'archivio dei certificati virtuali utilizzando il parametro *-SMIMECertificateIssuingCA*. Esempio: `Set-SmimeConfig -SMIMECertificateIssuingCA (Get-Content filename.sst -Encoding Byte)`

## Assicurasi che un certificato sia valido

Exchange 2013 SP1 prima verifica il file SST e poi convalida il certificato. Se la convalida non riesce, controllerà l'archivio dei certificati della macchina locale per convalidare il certificato. Questo comportamento è nuovo per Exchange 2013 SP1 rispetto alle versioni precedenti di Exchange. In Exchange Online solo il SST verrà utilizzato per la convalida.

## Ulteriori informazioni

[S/MIME per la crittografia e firma dei messaggi](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)

[Get-SmimeConfig](https://technet.microsoft.com/it-it/library/dn554257\(v=exchg.150\))

