---
title: 'Imposta porta attesa TCP su un server Accesso Client: Exchange 2013 Help'
TOCTitle: Impostare la porta di attesa TCP su un server Accesso Client
ms:assetid: 5f48f21a-d8d4-48b2-868f-9a3647693841
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673530(v=EXCHG.150)
ms:contentKeyID: 50555599
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare la porta di attesa TCP su un server Accesso Client

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-09_

È possibile configurare la porta TCP utilizzata per l'ascolto delle richieste SIP in un server Accesso Client che eseguono il servizio Microsoft Exchange Unified Messaging routing delle chiamate. Per impostazione predefinita, quando si installa un server Accesso Client, il numero di porta in attesa SIP TCP è impostato su 5060 e il server Accesso Client viene avviato in modalità TCP. La porta di attesa TCP SIP non può essere configurata tramite l'interfaccia di amministrazione di Exchange. È necessario configurare il numero di porta in attesa SIP TCP utilizzando il cmdlet **Set-UMCallRouterSettings** .

È necessario configurare la porta di attesa TCP 5061 se il gateway VoIP, IP PBX o session border controller (sbc) sono configurati per utilizzare una porta TCP diversa dalla SIP standard 5060.

È possibile configurare solo le porte TLS e TCP dei server Accesso client; non è possibile configurare le porte per un server Cassette postali di Exchange 1023. Tuttavia, è possibile utilizzare il cmdlet **Set-UMService** per configurare le porte di ascolto TCP e TLS per i server di messaggistica unificata di Exchange 2010.

Per ulteriori attività relative ai server Messaggistica unificata e Accesso client, vedere [Procedure di servizi di messaggistica unificata](um-services-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Server Accesso client (servizio di routing delle chiamate di messaggistica unificata)" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Verificare di aver installato correttamente i server Accesso client e Cassette postali.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per configurare la porta di attesa TCP in un server Accesso Client

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server Exchange che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Exchange Server** fare clic su **Messaggistica unificata**.

4.  **Le impostazioni di routing delle chiamate di messaggistica unificata**, **porta di attesa TCP**, immettere il numero di porta TCP e fare clic su **Salva**.

## Utilizzo della Shell per configurare la porta di attesa TCP in un server Accesso Client

In questo esempio imposta la porta di attesa TCP su un server Accesso Client denominato `MyClientAccessServer` a 5566.

```powershell
Set-UMCallRouterSettings -Server MyClientAccessServer -SipTCPListeningPort 5566
```

