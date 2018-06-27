---
title: 'S/MIME per la crittografia e firma dei messaggi: Exchange 2013 Help'
TOCTitle: S/MIME per la crittografia e firma dei messaggi
ms:assetid: 887c710b-0ec6-4ff0-8065-5f05f74afef3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn626158(v=EXCHG.150)
ms:contentKeyID: 61213866
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# S/MIME per la crittografia e firma dei messaggi

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

S/MIME (Secure/Multipurpose Internet Mail Extensions) è un metodo diffuso o messaggi crittografati e con maggiore precisione un protocollo, per l'invio di firma digitale. S/MIME consente di crittografare i messaggi di posta elettronica e firmare digitalmente loro. Quando si utilizza S/MIME con un messaggio di posta elettronica, aiuta le persone che ricevono messaggio per assicurarsi che visualizzato nella posta in arrivo l'esatta del messaggio che ha avviato con il mittente. E facilita anche gli utenti che ricevono i messaggi per essere certi che il messaggio proviene solo dal mittente specifico e non da qualcuno FALSO il mittente. A tale scopo, S/MIME sono disponibili per i servizi di protezione di crittografia, ad esempio l'autenticazione, l'integrità del messaggio e non ripudio di origine (utilizzo delle firme digitali). Consente inoltre di migliorare la privacy e sicurezza dei dati (utilizzando la crittografia) per il servizio di posta elettronica. Per uno sfondo approfondito cronologia e architettura di S/MIME nel contesto di posta elettronica, vedere [Understanding S/MIME](https://go.microsoft.com/fwlink/?linkid=393948).

In qualità di amministratore, è possibile abilitare sicurezza basata su S/MIME per l'organizzazione se si dispongono delle cassette postali in Exchange 2013 SP1 o Exchange Online, una parte di Office 365. Utilizzare le istruzioni contenute negli argomenti riportati di seguito collegate con Exchange Management Shell per configurare S/MIME. Per utilizzare S/MIME nelle versioni supportate di Outlook o ActiveSync, con Exchange 2013 SP1 o Exchange Online, gli utenti dell'organizzazione devono disporre dati pubblicati per il servizio locale Active Directory dominio (AD DS) e i certificati emessi per scopi di crittografia e firma. Il dominio di Active Directory deve essere collocato nel computer in una posizione fisica che è possibile controllare e non a livello di struttura remoto o servizio basato su cloud in un punto qualsiasi su internet. Per ulteriori informazioni su Active Directory, vedere [Servizi di dominio Active Directory](https://go.microsoft.com/fwlink/?linkid=394064).

## Scenari supportati e considerazioni tecniche

Se l'organizzazione utilizza Exchange 2013 SP1 o Exchange Online, è possibile configurare S/MIME per utilizzare uno qualsiasi dei seguenti endpoint:

  - Outlook 2010

  - Outlook 2013

  - Outlook Web App

  - Exchange ActiveSync (EAS)

I passaggi da eseguire per configurare S/MIME con ogni endpoint differiscono lievemente a seconda dell'endpoint scelto. In genere, è necessario completare le seguenti operazioni:

  - Installare un'autorità di certificazione basato su Windows e configurare un'infrastruttura a chiave pubblica per l'emissione di certificati S/MIME. Sono inoltre supportati i certificati rilasciati dalle autorità di certificazione terze parti. Per ulteriori informazioni, vedere [Panoramica di servizi di Active Directory certificato](https://technet.microsoft.com/library/hh831740.aspx).

  - Pubblicare il certificato utente in un account AD DS locale negli attributi UserSMIMECertificate e/o UserCertificate.

  - Per le organizzazioni Exchange Online, sincronizzare i certificati utente da AD DS ad Azure Active Directory utilizzando una versione appropriata di DirSync. Questi certificati saranno quindi sincronizzati da Azure Active Directory alla directory Exchange Online e saranno utilizzati per la crittografia di un messaggio per un destinatario.

  - Configurare una raccolta di certificati virtuali per convalidare S/MIME. Queste informazioni vengono utilizzate da OWA per convalidare la firma di un messaggio di posta elettronica e per garantire che sia stato firmato da un certificato attendibile.

  - Configurare l'endpoint Outlook o EAS per utilizzare S/MIME.

## Configurare S/MIME con Outlook Web App

La configurazione di S/MIME per Exchange 2013 SP1 o Exchange Online con Outlook Web App prevede i seguenti passaggi chiave:

1.  [Configurare le impostazioni di S/MIME per Outlook Web App](configure-s-mime-settings-for-outlook-web-app-exchange-2013-help.md)

2.  [Impostare raccolta di certificati virtuali per convalidare S/MIME](set-up-virtual-certificate-collection-to-validate-s-mime-exchange-2013-help.md)

3.  [Sincronizzare i certificati dell'utente con Office 365 per S/MIME](https://technet.microsoft.com/it-it/library/dn626159\(v=exchg.150\)) Questo passaggio si applica solo a Exchange Online.

## Tecnologie di crittografia del messaggio correlato

Man mano che diventano più importanti della protezione dei messaggi, gli amministratori devono conoscere i principi e concetti di protezione dei messaggi. Questo understanding è particolarmente importante per la crescente varietà di protezione relative tecnologie, ad esempio S/MIME che sono diventati disponibili. Per ulteriori informazioni sui S/MIME e come funziona nel contesto di posta elettronica, vedere [Understanding S/MIME](https://go.microsoft.com/fwlink/?linkid=393948). Diverse tecnologie di crittografia integrati per assicurare la protezione per i messaggi in rest e in transito. S/MIME possono lavorare contemporaneamente con le seguenti tecnologie ma non si basa su di essi:

  -  
    **Transport Layer Security (TLS)** crittografa il tunnel o la route tra i server di posta elettronica per poter prevenire lo snooping e le intercettazioni telefoniche.

  -  
    **Secure Sockets Layer (SSL)** consente di crittografare la connessione tra il client di posta elettronica e i server di Office 365.

  -  
    **BitLocker** consente di crittografare i dati su un disco rigido in un centro dati in modo che se qualcuno ottiene accesso non autorizzato, è possibile leggerli.

## Confronto tra S/MIME e crittografia dei messaggi di Office 365

S/MIME richiede un'infrastruttura di pubblicazione e certificati viene spesso utilizzata nelle situazioni business to business e business to consumer. L'utente può scegliere se utilizzarli per ogni messaggio che inviano, controlla le chiavi di crittografia S/MIME. Programmi di posta elettronica, ad esempio Outlook ricerca una posizione di autorità radice attendibile del certificato per eseguire la firma digitale e verifica della firma. Office 365 la crittografia dei messaggi è un servizio di crittografia basata su criteri che può essere configurato dall'amministratore e non è un singolo utente, per crittografare i messaggi inviati a tutti gli utenti interni o esterni all'organizzazione. È un servizio online che si basa su Azure Rights Management (RMS) e non si basa su un'infrastruttura a chiave pubblica. Crittografia dei messaggi di Office 365 inoltre fornisce funzionalità aggiuntive, ad esempio consente di personalizzare la posta elettronica con il marchio dell'organizzazione. Per ulteriori informazioni sulla crittografia dei messaggi di Office 365, vedere [Office 365 Message Encryption](https://go.microsoft.com/fwlink/?linkid=392525).

## Ulteriori informazioni

[Outlook Web App](outlook-web-app-exchange-2013-help.md)

[Secure Mail (2000)](https://technet.microsoft.com/en-us/library/cc962043.aspx)

