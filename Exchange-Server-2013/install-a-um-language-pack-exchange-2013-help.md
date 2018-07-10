---
title: 'Installare un Language Pack di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Installare un Language Pack di messaggistica unificata
ms:assetid: ed14ffa5-c9b0-4367-b5da-564024b360ff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876951(v=EXCHG.150)
ms:contentKeyID: 50481988
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Installare un Language Pack di messaggistica unificata

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

Per rendere disponibile nell'elenco delle lingue disponibili di messaggistica unificata su un dial plan di messaggistica UNIFICATA o operatore automatico di messaggistica UNIFICATA una lingua, è innanzitutto necessario installare il language pack di messaggistica UNIFICATA appropriato. Installare il language pack in un server delle cassette postali in esecuzione il servizio messaggistica unificata di Exchange utilizzando il file eseguibile autoestraente specifiche del linguaggio o il comando **setup.exe /AddUmLanguagePack** . Prima di installare un language pack di messaggistica UNIFICATA, è innanzitutto necessario scaricarlo in una cartella locale sul server cassette postali. È possibile scaricare language pack di messaggistica UNIFICATA di [Exchange 2013 UM Language Pack Server](https://go.microsoft.com/fwlink/p/?linkid=266542). Non esiste un file eseguibile separato per ogni lingua.

Dopo avere installato il language pack di messaggistica UNIFICATA appropriato, è possibile visualizzare l'elenco dei language pack di messaggistica UNIFICATA installati visualizzando l'elenco a discesa nella pagina **Impostazioni** di un dial plan di messaggistica UNIFICATA o l'elenco a discesa **lingua dell'interfaccia di segreteria telefonica automatizzati** nella pagina **Generale** di un operatore automatico di messaggistica UNIFICATA. È inoltre possibile configurare la lingua predefinita per una lingua diversa da quella inglese (en-US) nel DIAL plan e gli operatori automatici.


> [!WARNING]
> I language pack di messaggistica UNIFICATA di Microsoft Exchange Server 2007 o Exchange&nbsp;2007 Service Pack 1 (SP1), SP2 o SP3 o Exchange 2010 Service Pack 1 SP1, Service Pack 2 o Service Pack 3 non possono essere utilizzati in un server cassette postali Exchange 2013.



Per ulteriori attività relative alle lingue di messaggistica unificata, vedere [Procedure di lingue, istruzioni e messaggi di saluto di messaggistica unificata](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Server cassette postali (servizio messaggistica UNIFICATA)" nel [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare che il server cassette postali sia installato in un computer diverso da quello del server Accesso Client o che il server Accesso Client e cassette postali si trovano nello stesso hardware.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare il file di messaggistica UNIFICATA di installazione di Language Pack (.exe) per installare un language pack di messaggistica UNIFICATA

1.  Dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=266542), scaricare il file specifici della lingua alla messaggistica UNIFICATA language pack (.exe) in una cartella locale sul server cassette postali.

2.  Fare doppio clic sul UMLanguagePack. file *\<CultureCode\>.exe* . Ad esempio, per il tedesco UM language pack, si può scaricare il file denominato UMLanguagePack.de DE.exe.

3.  
    
    Exchange 2013 Nell'Installazione guidata, nella pagina **Contratto** di licenza, leggere le condizioni del contratto, selezionare **accetto i termini del contratto di licenza** e quindi fare clic su **Avanti**.

4.  
    
    Nella pagina **Language Pack di messaggistica unificata**, verificare che sia elencata la lingua corretta nella finestra **Verranno installati i seguenti Language Pack di messaggistica unificata**, quindi scegliere **Installa**.

5.  Fare clic su **Fine** per completare l'installazione del supporto lingua della messaggistica unificata.

## Utilizzare setup.exe per installare un language pack di messaggistica UNIFICATA

In questo esempio consente di installare il giapponese (ja-JP) alla messaggistica UNIFICATA language pack che è stato scaricato nella cartella D:\\Exchange\\UMLanguagePacks in un server cassette postali.

    setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

In questo esempio consente di installare il Messico Spagnolo (es-MX) e tedesco (de-DE) alla messaggistica UNIFICATA language pack sono stati scaricati nella cartella D:\\Exchange\\UMLanguagePacks su un server cassette postali.

    setup.exe /AddUmLanguagePack:es-MX,de-DE /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms


> [!WARNING]
> Se non si utilizza il parametro /IAcceptExchangeServerLicenseTerms, verrà visualizzato l'errore seguente: Benvenuti installazione automatica di Microsoft Exchange Server 2013. Si desidera accettare le condizioni di licenza per installare Microsoft Exchange Server 2013. Per leggere il contratto di licenza, visitare http://go.microsoft.com/fwlink/p/?LinkId=150127. Accettare il contratto di licenza, aggiungere il parametro /IAcceptExchangeServerLicenseTerms al comando che è in esecuzione. Per ulteriori informazioni, eseguire il programma di installazione /?.



Per ulteriori informazioni sulle lingue disponibili di messaggistica UNIFICATA e i codici di lingua, vedere [Messaggi di saluto, istruzioni e lingue di messaggistica UNIFICATA](um-languages-prompts-and-greetings-exchange-2013-help.md).

