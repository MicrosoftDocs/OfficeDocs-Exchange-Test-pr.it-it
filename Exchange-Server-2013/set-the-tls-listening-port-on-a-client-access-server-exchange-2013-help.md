---
title: 'Impostare la porta di attesa TLS su un server Accesso Client: Exchange 2013 Help'
TOCTitle: Impostare la porta di attesa TLS su un server Accesso Client
ms:assetid: f4401923-61fa-4dc5-95f8-c0d2f515b2ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673576(v=EXCHG.150)
ms:contentKeyID: 50555696
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare la porta di attesa TLS su un server Accesso Client

 

_**Si applica a:** Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-17_

È possibile configurare la porta TLS (Transport Layer Security) utilizzata per ascoltare le richieste SIP su un server Accesso client che esegue il servizio di routing delle chiamate della messaggistica unificata di Microsoft Exchange. Per impostazione predefinita, quando si installa un server Accesso client, il numero della porta di ascolto TLS SIP è impostato su 5061.

È probabile che sia necessario configurare la porta per l'ascolto TLS su 5061, se lo si desidera:

  - Configurare l'impostazione di protezione VoIP su un dial plan di messaggistica unificata sulla modalità SIP protetta.

  - Configurare l'impostazione di protezione VoIP su un dial plan di messaggistica unificata sulla modalità protetta.

  - Eseguire l'integrazione con MicrosoftOffice Communications Server 2007 R2 o Microsoft Lync Server.

  - Utilizzare Mutual TLS per crittografare i dati di rete tra i server Accesso client, i server Cassette postali su cui è in esecuzione il servizio di messaggistica unificata di Microsoft Exchange, e i gateway VoIP, i PBX (Private Branch eXchange) abilitati a SIP (Session Initiation Protocol), gli IP PBX o gli SBC (Session Border Controller).

Se si desidera utilizzare Mutual TLS tra un gateway IP di messaggistica unificata e un dial plan che opera in modalità SIP protetta o modalità protetta, quando si crea il gateway IP di messaggistica unificata è necessario configurarlo con un nome di dominio completo e per l'ascolto sulla porta TCP 5061. È necessario, inoltre, verificare che tutti i gateway VoIP, i PBX abilitati a SIP, gli IP PBX e gli SBC siano stati configurati per l'ascolto delle richieste Mutual TLS sulla porta 5061.

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

## Configurazione della porta di ascolto TLS su un server Accesso client tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nella visualizzazione elenco, selezionare il server Exchange che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Exchange Server** fare clic su **Messaggistica unificata**.

4.  In **Impostazioni del servizio di messaggistica unificata**, sotto **Porta di ascolto TLS**, immettere il numero della porta TLS e fare clic su **Salva**.

## Configurazione della porta di TLS su un server Accesso client tramite Shell

Con questo esempio la porta di ascolto TLS sul server Accesso client `MyClientAccessServer` viene impostata su 5561.

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTlsListeningPort 5561

