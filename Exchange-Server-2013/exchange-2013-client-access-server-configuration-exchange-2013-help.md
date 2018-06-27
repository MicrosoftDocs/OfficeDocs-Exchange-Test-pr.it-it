---
title: 'Configurazione del server Accesso client di Exchange 2013: Exchange 2013 Help'
TOCTitle: Configurazione del server Accesso client di Exchange 2013
ms:assetid: 01432ae4-2a00-44a4-a4dd-4eb8d7e6cfae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh529912(v=EXCHG.150)
ms:contentKeyID: 50479901
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurazione del server Accesso client di Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-07-25_

Dopo aver installato il server Accesso client di Exchange 2013, è possibile eseguire numerose attività di configurazione. Sebbene il server Accesso client di Exchange 2013 non gestisca l'elaborazione dei protocolli client, è necessario applicare a questo server numerose impostazioni, incluse quelle per directory virtuali e certificati.

## Configurazione dei certificati del server

In Exchange 2013, è possibile utilizzare la configurazione guidata dei certificati per richiedere un certificato digitale da un'autorità di certificazione. Dopo aver richiesto un certificato digitale, è necessario installarlo sul server Accesso client.

Non è necessario installare i certificati digitali sui server Cassette postali nell'organizzazione. Un certificato autofirmato è installato per impostazione predefinita sui server Cassette postali e non è necessario sostituirlo. I server Accesso client nell'organizzazione riconoscono implicitamente come attendibile il certificato sui server Cassette postali. Per ulteriori informazioni, vedere [Interfaccia utente per la gestione dei certificati in Exchange 2013](exchange-2013-certificate-management-ui-exchange-2013-help.md).

## Configurazione delle directory virtuali

Ci sono numerose impostazioni che è possibile configurare nelle directory virtuali per Rubrica offline, Servizi Web di Exchange, Exchange ActiveSync, Outlook Web App e l'interfaccia di amministrazione di Exchange. Per ulteriori informazioni sulla gestione delle directory virtuali, vedere [Gestione di directory virtuali](virtual-directory-management-exchange-2013-help.md). È possibile configurare le directory virtuali utilizzando i seguenti comandi.

  - Exchange 2013 fornisce due insiemi di impostazioni di connettività HTTP per la configurazione di Outlook via Internet in modo che gli amministratori possano configurare un endpoint interno ed esterno.
    
    Per configurare Outlook via Internet con un URL singolo per la connettività, è necessario fornire il nome host, indicare se è necessaria la protezione SSL e specificare un authpackage tramite il seguente comando in Exchange Management Shell:
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    
    Inoltre, è possibile specificare un endpoint raggiungibile esternamente utilizzando il seguente comando in Exchange Management Shell:
    
        Get-OutlookAnywhere | Set-OutlookAnywhere -InternalHostname "internalServer.contoso.com" -InternalClientAuthenticationMethod Ntlm -InternalClientsRequireSsl $true -ExternalHostname "externalServer.company.com" -ExternalClientAuthenticationMethod Basic -ExternalClientsRequireSsl $true -IISAuthenticationMethods Negotiate,NTLM,Basic
    

    > [!TIP]
    > Anche se Exchange 2013 supporta l'autenticazione HTTP della negoziazione per Outlook via Internet, deve essere utilizzato soltanto quando tutti i server dell'ambiente eseguono Exchange 2013.



  - Per configurare Exchange ActiveSync, utilizzare il seguente comando:
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2013>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl "https://mail.contoso.com/Microsoft-Server-ActiveSync"

  - Per configurare la directory virtuale di Servizi Web di Exchange, utilizzare il seguente comando:
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalUrl https://mail.contoso.com/EWS/Exchange.asmx

  - Per configurare la Rubrica offline, utilizzare il seguente comando:
    
        Set-OABVirtualDirectory -Identity "<CAS2013>\OAB (Default Web Site)" -ExternalUrl "https://mail.contoso.com/OAB"

  - Per configurare il punto di connessione del servizio (SCP, Service Connection Point), utilizzare il seguente comando.
    
        Set-ClientAccessServer -Identity <CAS2013> -AutoDiscoverServiceInternalURI https://autodiscover.contoso.com/AutoDiscover/AutoDiscover.xml

## Aggiornamento da Exchange 2007 e 2010 al server Accesso client

Utilizzare questa sezione per configurare l'accesso esterno ai protocolli sul server Accesso client di Exchange 2013. Eseguire i comandi di Exchange Management Shell nella seguente sezione relativa alla configurazione delle directory virtuali, così come nei comandi riportati di seguito.

Per configurare le directory virtuali per Exchange 2013, è necessario utilizzare i seguenti comandi.

1.  Per configurare un URL esterno per Outlook Web App, utilizzare il seguente comando in Exchange Management Shell.
    
        Set-OwaVirtualDirectory "<CAS2013>\OWA (Default Web Site)" -ExternalUrl https://mail.contoso.com/OWA
    
    In un prompt dei comandi, immettere i seguenti comandi dopo aver impostato la directory virtuale di Outlook Web App.
    
        Net stop IISAdmin /y
    
        Net start W3SVC

2.  Per configurare l'accesso esterno all'interfaccia di amministrazione di Exchange, utilizzare il seguente comando in Exchange Management Shell.
    
        Set-EcpVirtualDirectory "<CAS2013>\ECP (Default Web Site)" -ExternalUrl https://mail.contoso.com/ECP -InternalURL https://mail.contoso.com/ECP 

3.  Per configurare il servizio Disponibilità, utilizzare il seguente comando in Exchange Management Shell.
    
        Set-WebServicesVirtualDirectory -Identity "<CAS2013>\EWS (Default Web Site)" -ExternalURL https://mail.contoso.com/EWS/Exchange.asmx

Per verificare che l'URL esterno sia stato configurato correttamente per Exchange ActiveSync o Outlook Web App, è possibile utilizzare l'analizzatore connettività remota, uno strumento gratuito basato sul Web fornito da Microsoft. È possibile trovare l' analizzatore connettività remota [di seguito](http://go.microsoft.com/fwlink/?linkid=154308).

Per verificare che l'autenticazione sia stata configurata correttamente per Exchange ActiveSync o Outlook Web App, è anche possibile utilizzare l'Analizzatore connettività remota di Exchange.

Per verificare che l'accesso diretto ai file sia stato configurato correttamente per Outlook Web App, accedere come utente a Outlook Web App utilizzando l'opzione di computer pubblico, quindi provare ad accedere e a salvare un file allegato a un messaggio di posta elettronica.

## Configurazione dei protocolli sui server Accesso clienti di Exchange 2007

Per configurare le directory virtuali per Exchange 2007, è necessario utilizzare i seguenti comandi.

  - Per configurare l'URL esterno di una directory virtuale di Exchange ActiveSync, utilizzare il seguente comando in Exchange Management Shell.
    
        Set-ActiveSyncVirtualDirectory -Identity "<CAS2007>\Microsoft-Server-ActiveSync (Default Web Site)" -ExternalUrl https://mail.contoso.com/Microsoft-Server-ActiveSync

  - Per configurare l'URL esterno di una directory virtuale di Outlook Web App, utilizzare il seguente comando in Exchange Management Shell.
    
        Set-OwaVirtualDirectory -Identity "<CAS2007>\owa (Default Web Site)" -ExternalUrl https://legacy.contoso.com/owa

