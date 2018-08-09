---
title: 'Importa/esporta certificati messaggistica unificata: Exchange 2013 Help'
TOCTitle: Importare o esportare i certificati per la messaggistica unificata
ms:assetid: ee688c33-2e08-47e7-95fc-04ba10238341
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn205143(v=EXCHG.150)
ms:contentKeyID: 54652892
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Importare o esportare i certificati per la messaggistica unificata

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-12-18_

È possibile utilizzare EAC o Shell per importare o esportare certificati autofirmati, di infrastruttura con chiave pubblica (PKI) interna o commerciali di terze parti. Per la messaggistica unificata, è possibile utilizzare uno di questi certificati per il servizio di messaggistica unificata di Microsoft Exchange e il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange. È possibile utilizzare lo stesso certificato per entrambi i servizi oppure un certificato diverso per ogni servizio.

L'importazione dei certificati per Exchange può essere utile per:

  - Importare un certificato che era stato esportato in un file.

  - Importare un file di certificato PKI che era stato generato da un'autorità di certificazione interna.

  - Importare un certificato commerciale di terze parti.

L'esportazione di un certificato esistente dall'archivio certificati sul server Exchange locale può essere utile per:

  - Esportare il certificato affinché possa essere importato su un altro server Exchange.

  - Esportare il certificato affinché possa essere importato in un gateway VoIP, in un IP PBX o in un PBX abilitato a SIP.

  - Esportare il certificato in modo da eseguire il backup di certificato e relativa chiave privata.

Per ulteriori attività relative alla gestione dei certificati per la messaggistica unificata, vedere [Distribuzione di certificati per le procedure di messaggistica unificata](deploying-certificates-for-um-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione dei certificati" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) e "Servizio di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md). È necessario, inoltre, accedere utilizzando un account appartenente al gruppo di amministratori locale del computer.

  - Prima di esportare un certificato, utilizzare il cmdlet **Get-ExchangeCertificate** per verificare che l'attributo *PrivateKeyExportable* sul certificato sia impostato su `$true`.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Esportazione di un certificato tramite EAC

1.  In EAC, fare clic su **Server** \> **Certificati** \> **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni"), quindi fare clic su **Esporta certificato di Exchange**.

2.  Nella pagina **Esporta certificato di Exchange**, nella casella **File di destinazione dell'esportazione**, immettere il nome del file del certificato.

3.  Nella casella **Password**, immettere la password da utilizzare per proteggere la chiave privata e fare clic su **OK**.

## Utilizzo di Shell per esportare un certificato

In questo esempio il certificato con Identificazione personale A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC viene esportato in un file dopo la richiesta di immissione di nome utente e password.

    $file = Export-ExchangeCertificate -Thumbprint A36DE2B9B62980A717EBD0C3052F5F0B08FBFFCC -BinaryEncoded:$true -Password (Get-Credential).password

Con questo esempio viene effettuato quanto segue:

1.  Utilizza il cmdlet **Get-ExchangeCertificate** per trovare il certificato da esportare.

2.  Utilizza il cmdlet **Export-ExchangeCertificate** per impostare la password per il certificato.

3.  Emette il certificato in un file dopo che sono stati immessi nome utente e password.

<!-- end list -->
```
$file = Get-ExchangeCertificate -DomainName umcorp.northwindtraders.com | Export-ExchangeCertificate -BinaryEncoded:$true -Password (Get-Credential).password
```
```
Set-Content -Path "d:\umcerts\selfsigned.pfx" -Value $file.FileData =Encoding Byte
```

## Importazione di un certificato tramite EAC

1.  In EAC, fare clic su **Server** \> **Certificati** \> **Altre opzioni**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni"), quindi fare clic su **Importa certificato di Exchange**.

2.  Nella pagina **Importa certificato di Exchange**, nella casella **File da importare**, immettere il percorso della cartella condivisa e il nome del file del certificato. Se il certificato è protetto con una password, immettere la password nella casella **Password** e fare clic su **Avanti**.

3.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per selezionare i server a cui applicare il certificato, quindi fare clic su **OK**. Per rimuovere un server dalla visualizzazione elenco, fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi") e quindi su **Fine**.

## Importazione di un certificato tramite Shell

In questo esempio un certificato viene importato dal file del certificato d:\\certificates\\exchange\\SelfSignedUMCert.pfx dopo aver immesso nome utente e password.

    Import-ExchangeCertificate -FileData ([Byte[]]$(Get-Content -Path d:\certificates\exchange\SelfSignedUMCert.pfx -Encoding Byte -ReadCount 0)) -Password:(Get-Credential).password

