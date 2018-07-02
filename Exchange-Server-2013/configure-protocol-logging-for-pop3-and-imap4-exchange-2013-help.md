---
title: 'Configurare la registrazione del protocollo POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Configurare la registrazione del protocollo POP3 e IMAP4
ms:assetid: 451b337b-cb6b-4460-8687-be0b19c469bc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997690(v=EXCHG.150)
ms:contentKeyID: 50555580
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la registrazione del protocollo POP3 e IMAP4

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-27_

È possibile utilizzare Shell per abilitare, disabilitare o modificare le impostazioni della registrazione di protocollo per POP3 e IMAP4. Per impostazione predefinita, la registrazione del protocollo non è abilitata.

La registrazione di protocollo consente di verificare le connessioni POP3 e IMAP4 nell'ambiente Exchange. Ciò può essere utile se si risolvono problemi relativi alle prestazioni POP3 o IMAP4. Per ulteriori informazioni, vedere [Registrazione del protocollo POP3 e IMAP4](protocol-logging-for-pop3-and-imap4-exchange-2013-help.md). Per ulteriori informazioni su POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni POP3" e \&quot;Impostazioni IMAP4\&quot; nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Abilitazione della registrazione del protocollo per POP3 o IMAP4 tramite Shell

In questo esempio, viene abilitata la registrazione del protocollo per IMAP4 o POP3 sul server Accesso client CAS01.

    Set-ImapSettings -Server "CAS01" -ProtocolLogEnabled $true
    Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true


> [!NOTE]
> Una volta modificate le opzioni di registrazione del protocollo per POP3 o IMAP4, è necessario riavviare il servizio in uso: POP3 o IMAP4. Per informazioni su come riavviare i servizi POP3 e IMAP4, vedere <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Avviare e arrestare i servizi POP3</A> e <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Avviare e arrestare i servizi IMAP4</A>.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ImapSettings](https://technet.microsoft.com/it-it/library/aa998252\(v=exchg.150\)) e [Set-PopSettings](https://technet.microsoft.com/it-it/library/aa997154\(v=exchg.150\)).

## Disabilitazione della registrazione del protocollo per POP3 o IMAP4 tramite Shell

In questo esempio, viene disabilitata la registrazione del protocollo per IMAP4 o POP3 sul server Accesso client CAS01.

    Set-ImapSettings -Server "CAS01" -protocolLogEnabled $false
    Set-PopSettings -Server "CAS01" -protocolLogEnabled $false


> [!NOTE]
> Una volta specificate le opzioni di registrazione del protocollo per POP3 o IMAP4, è necessario riavviare il servizio in uso: POP3 o IMAP4. Per informazioni su come riavviare i servizi POP3 e IMAP4, vedere <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Avviare e arrestare i servizi POP3</A> e <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Avviare e arrestare i servizi IMAP4</A>.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ImapSettings](https://technet.microsoft.com/it-it/library/aa998252\(v=exchg.150\)) e [Set-PopSettings](https://technet.microsoft.com/it-it/library/aa997154\(v=exchg.150\)).

## Modifica della registrazione del protocollo per POP3 o IMAP4 tramite Shell

Per modificare le impostazioni di registrazione per POP3 o IMAP4, eseguire i cmdlet **Set-ImapSettings** o **Set-PopSettings** con uno o più dei seguenti parametri.

  - *LogFileLocation*   Questo parametro consente di specificare il percorso dei file di registro del protocollo POP3 o IMAP4. Per impostazione predefinita, i file di log del protocollo POP3 si trovano nella directory C:\\Programmi\\Microsoft\\Exchange Server\\V15\\Logging\\Pop3. In questo esempio, viene attivata la registrazione del protocollo POP3 sul server Accesso client CAS01. La directory di registrazione del protocollo POP3 viene cambiata in C:\\Pop3Logging.
    
        Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true -LogFileLocation "C:\Pop3Logging"

  - *LogFileRollOverSettings*   Questo parametro consente di definire la frequenza con cui la registrazione del protocollo POP3 o IMAP4 crea un nuovo file di registro. Per impostazione predefinita, viene creato un nuovo file di registro ogni giorno. I valori possibili sono:
    
    Hourly
    
    Daily
    
    Weekly
    
    Monthly
    
    Questa impostazione si applica solo quando il valore del parametro *LogPerFileSizeQuota* è impostato su zero. In questo esempio la registrazione del protocollo POP3 viene modificata sul server Accesso Client CAS01 per creare un nuovo file di registro ogni ora.
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 0 -LogFileRollOverSettings Hourly

  - *LogPerFileSizeQuota*   Questo parametro consente di definire la dimensione massima, in byte, di un file di registro del protocollo POP3 o IMAP4. Per impostazione predefinita, questo valore è impostato su zero. Se il valore è impostato su zero, viene creato un nuovo file di registro del protocollo con la frequenza specificata dal parametro *LogFileRollOverSettings*.
    
    In questo esempio, viene modificata la registrazione del protocollo POP3 sul server Accesso client CAS01 in modo da creare un nuovo file di registro quando un file di registro raggiunge i 2 MB.
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 2000000
    
    In questo esempio, viene modificata la registrazione del protocollo POP3 sul server Accesso client CAS01 in modo da utilizzare lo stesso file di registro indipendentemente dalle dimensioni e dalla data di creazione.
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota unlimited


> [!NOTE]
> Una volta specificate le opzioni di registrazione del protocollo per POP3 o IMAP4, è necessario riavviare il servizio in uso: POP3 o IMAP4. Per informazioni su come riavviare i servizi POP3 e IMAP4, vedere <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">Avviare e arrestare i servizi POP3</A> e <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">Avviare e arrestare i servizi IMAP4</A>.



Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-ImapSettings](https://technet.microsoft.com/it-it/library/aa998252\(v=exchg.150\)) e [Set-PopSettings](https://technet.microsoft.com/it-it/library/aa997154\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Eseguire il seguente comando in Shell per verificare le impostazioni di registrazione del protocollo POP3. Se la registrazione del protocollo POP3 è abilitata il valore per il parametro *ProtocolLogEnabled* è `True`. Se la registrazione del protocollo POP3 è disabilitata, il valore è `False`. È anche possibile assicurarsi che i valori per i parametri *LogFileLocation*, *LogPerFileSizeQuota* e *LogFileRollOverSettings* siano corretti.

    Get-PopSettings | format-list

Eseguire il seguente comando in Shell per verificare le impostazioni di registrazione del protocollo IMAP4. Se la registrazione del protocollo IMAP4 è abilitata il valore per il parametro *ProtocolLogEnabled* è `True`. Se la registrazione del protocollo IMAP4 è disabilitata, il valore è `False`. È anche possibile assicurarsi che i valori per i parametri *LogFileLocation*, *LogPerFileSizeQuota* e *LogFileRollOverSettings* siano corretti.

    Get-ImapSettings | format-list

## Ulteriori informazioni

Una volta configurate le impostazioni di registrazione del protocollo per POP3 e IMAP4, è possibile anche:

[Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md)

[Avviare e arrestare i servizi POP3](start-and-stop-the-pop3-services-exchange-2013-help.md)

