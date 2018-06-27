---
title: 'Rimuovere un language pack di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Rimuovere un language pack di messaggistica unificata
ms:assetid: a2bc2753-2c25-4ea0-a9d5-e3d42a699c6c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124004(v=EXCHG.150)
ms:contentKeyID: 50481347
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere un language pack di messaggistica unificata

 

_**Si applica a:**Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-14_

È possibile utilizzare EAC o Shell per gestire le lingue di messaggistica unificata sui server Cassette postali che eseguono il servizio Messaggistica unificata di Microsoft Exchange. Tuttavia, per rimuovere una lingua dall'elenco in un dial plan di messaggistica unificata, è necessario rimuovere il Language Pack di messaggistica unificata appropriato dal server Cassette postali utilizzando il comando **Setup.exe /RemoveUmLanguagePack**. Dopo aver rimosso il Language Pack di messaggistica unificata dal server Cassette postali, la lingua non sarà disponibile in fase di configurazione di un dial plan o un operatore automatico di messaggistica unificata. È possibile visualizzare i Language Pack di messaggistica unificata installati visualizzando le proprietà del server Cassette postali o utilizzando il cmdlet **Get-UMService**.

Per ulteriori attività relative alle lingue di messaggistica unificata, vedere [Procedure di lingue, istruzioni e messaggi di saluto di messaggistica unificata](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Cassette postali (servizio Messaggistica unificata)" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare che sia installato un Language Pack di messaggistica unificata diverso da en-US.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzo di Setup.exe per rimuovere un Language Pack di messaggistica unificata

Al prompt dei comandi digitare quanto segue.

    Setup.exe /RemoveUmLanguagePack:<UmLanguagePackName>

Nel comando precedente, *\<UmLanguagePackName\>* è il nome del Language Pack di messaggistica unificata, ad esempio fr-FR.


> [!WARNING]
> Non è possibile utilizzare il file Setup.exe nella cartella \Bin per rimuovere un Language Pack di messaggistica unificata dopo aver installato eventuali aggiornamenti. È necessario utilizzare il file Setup.exe nel DVD di Exchange 2013 o nei file di origine scaricati. In caso contrario, si verifica il seguente errore: Mancata corrispondenza tra la versione dell'applicazione in esecuzione e quella dell'applicazione installata.


