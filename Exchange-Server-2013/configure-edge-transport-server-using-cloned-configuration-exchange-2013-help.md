---
title: 'Configurare il server Trasporto Edge utilizzando una configurazione clonata: Exchange 2013 Help'
TOCTitle: Configurare il server Trasporto Edge utilizzando una configurazione clonata
ms:assetid: 0bbc83e3-e5e8-4480-a8a6-15f035360856
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996008(v=EXCHG.150)
ms:contentKeyID: 61183403
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il server Trasporto Edge utilizzando una configurazione clonata

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-13_

È possibile utilizzare gli script di Exchange Management Shell forniti (al percorso %ExchangeInstallPath%Scripts) per duplicare la configurazione di un server Trasporto Edge. Questo processo viene definito *configurazione clonata*. Per *configurazione clonata* si intende la distribuzione dei nuovi server Trasporto Edge in base alle informazioni sulla configurazione di un server di origine configurato in precedenza. Le informazioni sulla configurazione del server di origine precedentemente configurato vengono copiate ed esportate in un file XML, che viene quindi importato nel server di destinazione. Per una panoramica di questo processo, vedere [Configurazione clonata del server Trasporto Edge](edge-transport-server-cloned-configuration-exchange-2013-help.md).

Le informazioni sulla configurazione del server Trasporto Edge vengono archiviate in Active Directory Lightweight Directory Services (AD LDS) e non vengono replicate tra più server Trasporto Edge. Mediante la configurazione clonata, è possibile garantire che ogni server Trasporto Edge distribuito nella rete perimetrale utilizzi la stessa configurazione.

Due script di Shell vengono utilizzati per eseguire attività di configurazione clonata:

  - **ExportEdgeConfig.ps1**   Esporta tutte le impostazioni configurate dall'utente e i dati dal server Edge Transport e li archivia in un file XML.

  - **ImportEdgeConfig.ps1**   Durante il passo di convalida della configurazione, lo script ImportEdgeConfig.ps1 consente di esaminare il file XML esportato per verificare se le impostazioni di esportazione specifiche del server sono valide per il server di destinazione. Se le impostazioni devono essere modificate, lo script scrive le impostazioni non valide in un file di risposta che viene modificato per specificare le informazioni sul server di destinazione utilizzate durante l'operazione di configurazione dell'importazione. Durante l'operazione di configurazione dell'importazione, lo script importa tutte le impostazioni configurate dall'utente e i dati archiviati nel file XML intermedio creato dallo script ExportEdgeConfig.ps1.

Entrambi questi script si trovano nella cartella %ExchangeInstallPath%Scripts.

## Informazioni preliminari

  - Tempo stimato per il completamento di questa attività: 30 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Trasporto Edge" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - La configurazione clonata non duplica le impostazioni di sottoscrizione Edge di un server. I certificati di EdgeSync non vengono clonati. È necessario eseguire il processo EdgeSync in modo indipendente per ciascun server Trasporto Edge. EdgeSync sovrascrive le modifiche incluse nelle informazioni di configurazione clonate e nelle informazioni sulla replica di EdgeSync.

  - Se i connettori di invio vengono configurati per l'utilizzo delle credenziali, la password viene scritta nel file XML intermedio come stringa crittografata. È possibile utilizzare il parametro *-key* con gli script ImportEdgeConfig.ps1 e ExportEdgeConfig.ps1 per specificare la stringa a 32 byte da utilizzare per la crittografia e la decrittografia della password. Se non si utilizza il parametro *-key*, viene utilizzata una chiave di crittografia predefinita.

  - È possibile utilizzare solo Shell per eseguire questa procedura. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione

## Passaggio 1: esportare i dati di configurazione del server di origine in un file nel server di origine

1.  Copiare lo script ExportEdgeConfig.ps1 nella cartella radice del profilo utente nel server di origine.

2.  Per esportare i dati di configurazione del server di origine in un file nel server di origine, utilizzare la seguente sintassi.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"<configuration file>"
    
    Ad esempio, per esportare i dati di configurazione del server di origine nel file C:\\CloneConfigData.xml, eseguire il comando seguente.
    
        ./ExportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml"

## Come verificare se l'operazione ha avuto esito positivo?

Si potrà sapere se i dati di configurazione di origine sono stati correttamente esportati in un file quando si riceverà il messaggio di conferma, "I dati di configurazione di Edge sono stati esportati correttamente in: \<output file path\>".

## Passaggio 2: convalidare il file di configurazione e creare un file di risposta nel server di destinazione

1.  Copiare il file di configurazione del server di origine esportato nel passaggio precedente nel server Trasporto Edge di destinazione.

2.  Copiare lo script ImportEdgeConfig.ps1 nella cartella radice del profilo utente nel server di destinazione.

3.  Per convalidare il file di configurazione e utilizzare i risultati per creare un file di risposta nel server di destinazione, utilizzare la seguente sintassi.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"<configuration file>" -IsImport $false -CloneConfigAnswer:"<answer file>"
    
    Ad esempio, per convalidare il file di configurazione C:\\CloneConfigData.xml e creare il file di risposta C:\\CloneConfigAnswer.xml, eseguire il comando seguente.
    
        ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $false -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

4.  Aprire il file di risposta e modificare le impostazioni non valide per il server di destinazione. Se non è necessaria alcuna modifica, il file di risposta non conterrà alcuna voce. Salvare le modifiche.

## Come verificare se l'operazione ha avuto esito positivo?

Si avrà conferma di aver convalidato correttamente il file di configurazione e creato un file di risposta quando verrà visualizzato il messaggio di conferma "Il file di risposta è stato creato correttamente".

## Passaggio 3: importare il file di configurazione nel server di destinazione

Per importare il file di configurazione nel server di destinazione, utilizzare la seguente sintassi.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"<Configuration file>" -IsImport $true -CloneConfigAnswer:"<answer file>"

Ad esempio, per importare il file di configurazione C:\\CloneConfigData.xml utilizzando il file di risposta C:\\CloneConfigAnswer.xml, eseguire il comando seguente.

    ./ImportEdgeConfig.ps1 -CloneConfigData:"C:\CloneConfigData.xml" -IsImport $true -CloneConfigAnswer:"C:\CloneConfigAnswer.xml"

## Come verificare se l'operazione ha avuto esito positivo?

Sarà possibile sapere di aver importato correttamente il file di configurazione nel server di destinazione quando verrà visualizzato il messaggio di conferma, "I dati di configurazione di Edge sono stati importati correttamente".

