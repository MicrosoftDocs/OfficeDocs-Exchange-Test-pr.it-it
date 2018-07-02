---
title: 'Configurare un nome di dominio completo: Exchange 2013 Help'
TOCTitle: Configurare un nome di dominio completo
ms:assetid: af093f87-59b7-44a8-a9a2-8f17f0cc7db8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423553(v=EXCHG.150)
ms:contentKeyID: 50481419
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare un nome di dominio completo

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2012-11-09_

È possibile configurare un gateway IP di messaggistica unificata con un indirizzo IP o un nome di dominio completo (FQDN). Quando si crea un gateway IP di messaggistica unificata, è necessario definire l'indirizzo IP del nome di dominio completo configurato nel gateway VoIP, PBX IP o SBC (Session Border Controller) in uso. È possibile modificare l'indirizzo IP o il nome di dominio completo dopo aver creato il gateway IP di messaggistica unificata.

Se si crea un gateway IP di messaggistica unificata utilizzando un nome di dominio completo, è necessario creare i record HOST (A) corretti nella zona di ricerca diretta del DNS. Se si crea un gateway IP di messaggistica unificata utilizzando un nome di dominio completo (FQDN) e la configurazione DNS del gateway IP di messaggistica unificata viene modificata, è necessario disabilitare e quindi abilitare il gateway IP di messaggistica unificata per garantire che le informazioni di configurazione vengano aggiornate correttamente.

Se si desidera utilizzare MTLS (Mutual Transport Layer Security) tra un gateway IP di messaggistica unificata e un dial plan in funzione in modalità protetta o protetta con SIP, è necessario configurare il gateway IP di messaggistica unificata con un nome di dominio completo. È necessario configurarlo anche per l'ascolto sulla porta 5061 e verificare che un gateway VoIP, un PBX IP o SBC sia stato configurato per l'ascolto delle richieste MTLS sulla porta 5061. Per configurare un gateway IP di messaggistica unificata, eseguire questo comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.

Per altre attività di gestione relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione di un gateway IP di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Configurazione di un nome di dominio completo tramite EAC

1.  In Interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, selezionare il gateway IP di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Gateway IP di messaggistica unificata** in **Indirizzo** immettere il nome di dominio completo per il gateway VoIP, PBX abilitato a SIP, PBX IP o SBC.

3.  Fare clic su **Salva**.


> [!IMPORTANT]
> Quando si utilizza un nome di dominio completo invece che un indirizzo IP sul gateway IP di messaggistica unificata, verificare che siano stati creati i record DNS corretti.



## Configurazione di un nome di dominio completo tramite Shell

Con questo esempio viene configurato un gateway IP di messaggistica unificata denominato `MyUMIPGateway` utilizzando il nome di dominio completo voipgateway.contoso.com.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com

Con questo esempio viene configurato un gateway IP di messaggistica unificata denominato `MySBC` con nome di dominio completo sbc.contoso.com che ascolta le richieste SIP sulla porta TCP 5061.

    Set-UMIPGateway -Identity MySBC -Address sbc.contoso.com -Port 5061

