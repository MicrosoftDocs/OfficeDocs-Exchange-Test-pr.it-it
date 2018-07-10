---
title: 'Configurare la porta di attesa: Exchange 2013 Help'
TOCTitle: Configurare la porta di attesa
ms:assetid: 200ecbd8-18c3-4594-9cc8-924b3ab4eca1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633457(v=EXCHG.150)
ms:contentKeyID: 50555554
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la porta di attesa

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile configurare la porta TCP utilizzata in ascolto per le richieste SIP (Session Initiation Protocol) su un gateway IP di messaggistica unificata. Per impostazione predefinita, quando si crea un gateway IP di messaggistica unificata, il numero della porta di ascolto TCP SIP è impostato su 5060. La porta di ascolto TCP SIP non può essere configurata o modificata utilizzando l'interfaccia di amministrazione di Exchange. È necessario configurare il numero della porta di ascolto TCP SIP utilizzando il cmdlet **Set-UMIPGateway**.

È possibile che sia necessario configurare la porta di ascolto TCP su 5061 se si desidera:

  - Impostare la protezione VoIP su SIP con protezione su un dial plan di messaggistica unificata.

  - Impostare la protezione VoIP su Protetta su un dial plan di messaggistica unificata.

  - Integrare con MicrosoftOffice Communications Server 2007 R2 o Microsoft Lync Server.

  - Utilizzare l'autenticazione Transport Layer Security reciproca (TLS reciproca) per crittografare i dati della rete tra server Exchange e un gateway VoIP, Private Branch eXchange (PBX) abilitato per SIP, IP PBX o session border controller (SBC).

Se si desidera utilizzare Mutual TLS tra un gateway e un dial plan che opera in modalità SIP protetta o modalità protetta, quando si crea il gateway IP di messaggistica unificata è necessario configurarlo con un nome di dominio completo e quindi utilizzare Shell per configurare il gateway IP di messaggistica unificata per l'ascolto sulla porta TCP 5061. È anche necessario verificare che tutti i gateway VoIP, PBX abilitati per SIP, PBX IP e SBC siano stati configurati per l'ascolto delle richieste Mutual TLS sulla porta 5061.


> [!IMPORTANT]
> Quando si crea un gateway IP di messaggistica unificata utilizzando un nome di dominio completo, è necessario creare i record HOST (A) corretti nella zona di ricerca diretta del DNS. Se si crea un gateway IP di messaggistica unificata utilizzando un nome di dominio completo (FQDN) e la configurazione DNS del gateway IP di messaggistica unificata viene modificata, è necessario disabilitare e quindi abilitare il gateway IP di messaggistica unificata per garantire che le informazioni di configurazione vengano aggiornate correttamente.



Per altre attività di gestione relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Prima di eseguire questa procedura, verificare che sia stato creato un dial plan di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione di un gateway IP di messaggistica unificata prima di eseguire questa procedura. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Utilizzare Shell per configurare la porta di ascolto TCP

In questo esempio viene configurato un gateway IP di messaggistica unificata denominato `MyUMIPGateway` con nome di dominio completo mTLS.MyUMIPGateway.contoso.com che ascolta le richieste SIP sulla porta TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address mTLS.MYUMIPGateway.contoso.com -Port 5061

In questo esempio viene configurato un gateway IP di messaggistica unificata denominato `MyUMIPGateway` con nome di dominio completo SIPSecured.MyUMIPGateway.contoso.com che ascolta le richieste SIP sulla porta TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address SIPSecured.MyUMIPGateway.contoso.com -Port 5061

In questo esempio viene configurato un gateway IP di messaggistica unificata denominato `MyUMIPGateway` con nome di dominio completo MyOCSUMIPGateway.contoso.com che ascolta le richieste SIP sulla porta TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address MyOCSUMIPGateway.contoso.com -Port 5061

