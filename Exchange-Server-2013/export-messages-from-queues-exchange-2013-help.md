---
title: 'Esportazione dei messaggi dalle code: Exchange 2013 Help'
TOCTitle: Esportazione dei messaggi dalle code
ms:assetid: 688b342c-f380-4fe0-afce-7e38cf490627
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998625(v=EXCHG.150)
ms:contentKeyID: 51407381
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esportazione dei messaggi dalle code

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-05-05_

Quando viene esportato un messaggio da una coda in un file, il messaggio non viene rimosso dalla coda. Una copia del messaggio viene eseguita nella posizione specificata come un file di testo normale. Il file risultante può essere visualizzato in un'applicazione, ad esempio un editor di testo o un'applicazione client di posta elettronica, oppure è possibile inviare nuovamente il file di messaggio utilizzando la directory di riesecuzione su qualsiasi altro server Cassette postali o Trasporto Edge all'interno o all'esterno dell'organizzazione di Exchange.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Code" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - È necessario che i messaggi siano sospesi per la corretta esecuzione del processo di esportazione. È possibile esportare messaggi da code di recapito, dalla coda non raggiungibile o dalla coda di messaggi potenzialmente dannosi. I messaggi nella coda dei messaggi potenzialmente dannosi sono già in stato sospeso. Non è possibile sospendere o esportare messaggi nella coda di invio.

  - Non è possibile utilizzare il Visualizzatore code nella Casella degli strumenti di Exchange per esportare messaggi. Tuttavia, è possibile utilizzare il Visualizzatore code per individuare, identificare e sospendere i messaggi prima di esportarli con Shell.

  - Verificare le informazioni seguenti sulla posizione della directory di destinazione per i file dei messaggi:
    
      - Prima di poter esportare messaggi, è necessario che la directory di destinazione esista. La directory non verrà creata automaticamente. Se non viene specificato un percorso assoluto, viene utilizzata la directory di lavoro corrente di Exchange Management Shell.
    
      - Il percorso può essere locale sul server Exchange o può essere un percorso Universal Naming Convention (UNC) per una condivisione su un server remoto.
    
      - È necessario che l'account in uso disponga dell'autorizzazione in **scrittura** sulla directory di destinazione.
    
      - Quando si specifica un nome file per i messaggi esportati, verificare di includere l'estensione eml in modo che i file possano essere aperti facilmente dalle applicazioni client di posta elettronica o elaborati correttamente dalla directory di riesecuzione.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Per saperne di più

## Utilizzare Shell per esportare uno specifico messaggio da una coda specifica

Per esportare un indirizzo di posta elettronica specifico da una coda specifica, eseguire il seguente comando:
```powershell
    Export-Message -Identity <MessageIdentity> | AssembleMessage -Path <FilePath>\<FileName>.eml
```

In questo esempio viene esportata una copia di un messaggio con valore **InternalMessageID** 1234 e che si trova nella coda di recapito di contoso.com sul server denominato Mailbox01 al file denominato export.eml nel percorso D:\\Contoso Export.
```powershell
    Export-Message -Identity Exchange01\Contoso.com\1234 | AssembleMessage -Path "D:\Contoso Export\export.eml"
```

## Utilizzare Shell per esportare tutti i messaggi da una coda specifica

Per esportare tutti i messaggi da una coda specifica e utilizzare il valore **InternetMessageID** di ogni messaggio come nome del file, utilizzare la seguente sintassi.
```powershell
    Get-Message -Queue <QueueIdentity> | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}
```

Tenere presente che il valore **InternetMessageID** contiene parentesi angolari (\> e \<), che devono essere rimosse poiché non consentite nei nomi dei file.

In questo esempio viene esportata una copia di tutti i messaggi dalla coda di recapito contoso.com sul server denominato Mailbox01 alla directory locale denominata D:\\Contoso Export.
```powershell
    Get-Message -Queue Mailbox01\Contoso.com | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}
```
## Utilizzare Shell per esportare i messaggi specifici da tutte le code in un server

Per esportare tutti i messaggi specifici da tutte le code su un server e utilizzare il valore **InternetMessageID** di ogni messaggio come nome del file, utilizzare la seguente sintassi.
```powershell
    Get-Message -Filter {<MessageFilter>} [-Server <ServerIdentity>] | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}
```

Tenere presente che il valore **InternetMessageID** contiene parentesi angolari (\> e \<), che devono essere rimosse poiché non consentite nei nomi dei file.

In questo esempio viene esportata una copia di tutti i messaggi dai mittenti nel dominio contoso.com da tutte le code sul server denominato Mailbox01 alla directory locale denominata D:\\Contoso Export.
```powershell
    Get-Message -Filter {FromAddress -like "*@contoso.com"} -Server Mailbox01 | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}
```

> [!NOTE]
> Se si omette il parametro <EM>Server</EM>, il comando funziona sul server locale.


