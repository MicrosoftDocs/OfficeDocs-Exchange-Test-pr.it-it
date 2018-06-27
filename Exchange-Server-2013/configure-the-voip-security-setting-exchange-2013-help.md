---
title: 'Configurare le impostazioni di protezione VoIP: Exchange 2013 Help'
TOCTitle: Configurare le impostazioni di protezione VoIP
ms:assetid: b5335654-c766-4f3f-883c-f31263e1d9c1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201721(v=EXCHG.150)
ms:contentKeyID: 50481485
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare le impostazioni di protezione VoIP

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2014-10-16_

È possibile abilitare Voice over protezione IP (VoIP) per un dial plan di messaggistica unificata (UM). Per impostazione predefinita, quando viene creato un dial plan di messaggistica unificata, utilizza la modalità protetta o Nessuna crittografia. Server di Exchange possono rispondere alle chiamate per un o più dial plan di messaggistica unificata e possono rispondere alle chiamate di dial plan con diverse impostazioni di protezione VoIP. In Office 365 ed Exchange Online protetto modalità è obbligatorio e non può essere disattivata.

Quando si configura un dial plan da utilizzare protocollo SIP (Session Initiation) con protezione o modalità protetta, server di Exchange che rispondere alle chiamate per il dial plan di messaggistica unificata consentirà di crittografare il traffico (per modalità SIP protetta) o i canali multimediali in tempo reale RTP (Transport Protocol) e (per la modalità protetta) il traffico di segnalazione SIP di segnalazione SIP.


> [!IMPORTANT]
> Per organizzazioni locali e ibride distribuzioni, quando si configura il SipTCPListeningPort, SipTLSListeningPort o UMStartUpMode in un server Accesso Client che eseguono il servizio Microsoft Exchange Unified Messaging routing delle chiamate o un server cassette postali in esecuzione il servizio messaggistica unificata di Exchange, è necessario configurare correttamente le regole di Windows Firewall per consentire il traffico di rete SIP e RTP.



Per altre attività di gestione relative ai dial plan di messaggistica unificata, vedere [Procedure di messaggistica unificata dial plan](um-dial-plan-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Dial plan di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzare EAC per configurare la protezione VoIP su un dial plan di messaggistica unificata

1.  In EAC, accedere a **Messaggistica unificata** \> **Dial plan della messaggistica unificata** di Exchange, selezionare il dial plan di messaggistica unificata in cui si desidera modificare la protezione VoIP e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Nuovo dial plan di messaggistica unificata** fare clic su **Configura**.

3.  In **Generale**, in **modalità di protezione VoIP**, selezionare una delle opzioni seguenti:
    
      - **SIP protetta**
    
      - **Non protetta** (impostazione predefinita)
    
      - **Secured**

4.  Fare clic su **Salva**.

## Utilizzo della Shell per configurare la protezione VoIP su un dial plan di messaggistica unificata

In questo esempio consente di configurare un dial plan denominato `MySecureDialPlan` per crittografare il traffico SIP e RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Secured

In questo esempio consente di configurare un dial plan di messaggistica unificata denominato `MySecureDialPlan` per crittografare SIP ma non crittografare il traffico RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity SIPsecured

In questo esempio consente di configurare un dial plan di messaggistica unificata denominato `MySecureDialPlan` non crittografare il traffico SIP e RTP.

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Unsecured

