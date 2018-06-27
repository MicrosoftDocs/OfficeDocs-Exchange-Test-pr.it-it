---
title: "Configurare l'indirizzo IP: Exchange 2013 Help"
TOCTitle: Configurare l'indirizzo IP
ms:assetid: 100541c1-2297-4c46-9602-b304736541a8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb266940(v=EXCHG.150)
ms:contentKeyID: 50480059
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare l'indirizzo IP

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-11_

Prima di creare un gateway IP di messaggistica unificata, è necessario impostare l'indirizzo IP o il nome di dominio completo (FQDN) sul gateway VoIP, sul PBX IP o sul session border controller (SBC) in uso. Quindi, impostare l'indirizzo IP o il nome di dominio completo quando si crea il gateway IP di messaggistica unificata. È possibile modificare l'indirizzo IP o il nome di dominio completo in un secondo momento.

È possibile configurare l'indirizzo IP o il nome di dominio completo utilizzando Interfaccia di amministrazione di Exchange o Shell. In Interfaccia di amministrazione di Exchange, la casella **Indirizzo** nella pagina **Gateway IP di messaggistica unificata** può accettare un indirizzo IPv4, un indirizzo IPv6 o un nome di dominio completo. È anche possibile utilizzare il parametro *Address* nel cmdlet **Set-UMIPGateway** in Shell per impostare un indirizzo IP IPv4, un indirizzo IPv6 o un nome di dominio completo. Se si crea un gateway IP di messaggistica unificata utilizzando un nome di dominio completo, è necessario creare i record HOST A appropriati nella zona di ricerca diretta DNS. Se si modifica la configurazione DNS per il gateway IP di messaggistica unificata, è necessario disabilitare e quindi riabilitare il gateway IP di messaggistica unificata affinché le informazioni di configurazione del gateway sia aggiornino correttamente.

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

## Configurazione dell'indirizzo IP su un gateway IP di messaggistica unificata tramite Interfaccia di amministrazione di Exchange

1.  In Interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, selezionare il gateway IP di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Gateway IP di messaggistica unificata**, nella casella **Indirizzo**, immettere l'indirizzo IP per il gateway VoIP, PBX IP o session border controller (SBC).

3.  Fare clic su **Salva** per salvare le modifiche.


> [!IMPORTANT]
> Se si utilizza un nome di dominio completo invece di un indirizzo IP sul gateway IP di messaggistica unificata, verificare che siano stati creati i record DNS corretti.



## Configurazione dell'indirizzo IP su un gateway IP di messaggistica unificata tramite Shell

Con questo esempio viene configurato un gateway IP di messaggistica unificata denominato `MyUMIPGateway`, utilizzando l'indirizzo IP 10.10.10.1.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

Con questo esempio viene configurato, utilizzando l'indirizzo IP 10.10.10.1, un gateway IP di messaggistica unificata denominato `MyUMIPGateway` che ascolta le richieste SIP sulla porta TCP 5061.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.10 -Port 5061

In questo esempio, viene impedito al gateway IP di messaggistica unificata denominato `MyUMIPGateway` di accettare chiamate in ingresso e in uscita, viene impostato un indirizzo IPv6 e viene consentito al gateway IP di messaggistica unificata di utilizzare gli indirizzi IPv4 e IPv6.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

