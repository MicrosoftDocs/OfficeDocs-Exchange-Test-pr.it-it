---
title: 'Configurazione del flusso della posta Internet tramite un server Trasporto Edge sottoscritto: Exchange 2013 Help'
TOCTitle: Configurazione del flusso della posta Internet tramite un server Trasporto Edge sottoscritto
ms:assetid: d12ea770-99ce-4ab4-a373-96f2554641fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb738158(v=EXCHG.150)
ms:contentKeyID: 61183415
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione del flusso della posta Internet tramite un server Trasporto Edge sottoscritto

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-08_

Per definire la posta elettronica Internet attraverso un server Trasporto Edge, sottoscrivere il server Trasporto Edge in un sito Active Directory. In questo modo, vengono creati automaticamente i connettori di invio necessari per il flusso di posta Internet:

  - Un connettore di invio configurato per inviare messaggi di posta elettronica in uscita a tutti i domini Internet.

  - Un connettore di invio configurato per l'invio di posta elettronica in ingresso dal server Trasporto Edge al server di cassette postali di Exchange 2013.

Se non si desidera la sottoscrizione del server Trasporto Edge a un sito di Active Directory, è possibile creare manualmente i connettori di invio necessari per stabilire il flusso di posta tra il server di cassette postali e il server Trasporto Edge. Per ulteriori informazioni, vedere [Configurare il flusso della posta Internet tramite un server Trasporto Edge senza utilizzare EdgeSync](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md). Tuttavia, si consiglia di effettuare la sottoscrizione del server Trasporto Edge al sito di Active Directory quando possibile.

## Informazioni preliminari

  - Tempo stimato per il completamento: 20 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "EdgeSync" e "Server Trasporto Edge" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Prima di sottoscrivere un server Trasporto Edge alla propria organizzazione, è necessario configurare i domini autorevoli e i criteri degli indirizzi di posta elettronica per l'organizzazione di Exchange.

  - Abilitare la porta LDAP 50636/TCP protetta tramite il firewall che separa la rete perimetrale dell'utente dall'organizzazione di Exchange. Il server Trasporto Edge deve essere in grado di comunicare con tutti i server di cassette postali di Exchange 2013 nel sito sottoscritto di Active Directory.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configurazione del flusso della posta Internet tramite un server Trasporto Edge sottoscritto

1.  Nel server Trasporto Edge, creare il file di sottoscrizione a Edge utilizzando la sintassi seguente.
    
        New-EdgeSubscription -FileName <FileName>.xml [-Force]
    
    Nell'esempio riportato di seguito, viene creato un fil di sottoscrizione a Edge denominato EdgeSubscriptionInfo.xml e che si trova nella cartella C:\\Documenti. Il parametro *Force* annulla i comandi di conferma del prompt che verranno disabilitati e avvisa sulla sovrascrittura dei dati di configurazione sul server Trasporto Edge.
    
        New-EdgeSubscription -FileName "C:\My Documents\EdgeSubscriptionInfo.xml" -Force

2.  Copiare il file di sottoscrizione a Edge creato in un server di cassetta postale del sito Active Directory al quale si sta sottoscrivendo il server Trasporto Edge.

3.  Sul server di cassetta postale, utilizzare la seguente sintassi per importare il file di sottoscrizione a Edge.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "<FileName>.xml" -Encoding Byte -ReadCount 0)) -Site <SiteName>
    
    In questo esempio viene importato il file di sottoscrizione a Edge denominato EdgeSubscriptionInfo.xml dalla cartella D:\\Dati e viene sottoscritto il server Trasporto Edge nel sito Active Directory denominato "Default-First-Site-Name".
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "D:\Data\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -Site "Default-First-Site-Name"
    

    > [!NOTE]
    > È possibile utilizzare il parametro <EM>CreateInternetSendConnector</EM> o <EM>CreateInboundSendConnector</EM> per impedire la creazione automatica di uno o di entrambi i connettori di invio necessari. Per ulteriori informazioni, vedere <A href="edge-subscriptions-exchange-2013-help.md">Sottoscrizioni Edge</A>.



4.  Sul server di cassetta postale, eseguire il seguente comando per avviare la prima sincronizzazione di EdgeSync.
    
        Start-EdgeSynchronization

5.  Al termine dell'operazione, si consiglia di eliminare il file di sottoscrizione a Edge sia del server Trasporto Edge che da quello di cassetta postale. Tale file comprende informazioni relative alle credenziali utilizzate per il processo di comunicazione LDAP.

