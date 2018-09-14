---
title: 'Creare un gateway IP di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Creare un gateway IP di messaggistica unificata
ms:assetid: 542d6b50-147b-4cec-b54d-61c7b8fc0fc7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998045(v=EXCHG.150)
ms:contentKeyID: 50480616
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMIPGatewayWizardForm.CreateUMIPGatewayWizardPage
ms.translationtype: MT
---

# Creare un gateway IP di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-04-16_

Quando si crea un gateway IP di messaggistica unificata, si consente ai server di Exchange di connettersi a un nuovo gateway VoIP, PBX abilitato per SIP, IP PBX o a un session border controller (SBC). Subito dopo aver creato un gateway IP di messaggistica unificata, è necessario creare un nuovo gruppo di risposta di messaggistica unificata e associarlo al gateway IP. È possibile associare il gateway IP di messaggistica unificata a più dial plan di messaggistica unificata creando più gruppi di risposta di messaggistica unificata.

Per altre attività di gestione relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](https://docs.microsoft.com/it-it/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo dell'interfaccia di amministrazione di Exchange per la creazione di un gateway IP di messaggistica unificata

1.  
    
    In EAC accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata** e quindi fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella pagina **Nuovo gateway IP di messaggistica unificata** immettere le informazioni seguenti:
    
      - **Nome**   Utilizzare questa casella per specificare un nome univoco per il gateway IP di messaggistica unificata. Si tratta del nome che verrà visualizzato nell'interfaccia di amministrazione di Exchange. Qualora fosse necessario modificare il nome visualizzato del gateway IP di messaggistica unificata dopo la sua creazione, occorre innanzitutto eliminare il gateway IP di messaggistica unificata esistente e, quindi, crearne un altro con il nome corretto. Benché il nome del gateway IP di messaggistica unificata sia obbligatorio viene utilizzato solo ai fini della visualizzazione. Dal momento che l'organizzazione può utilizzare più gateway IP di messaggistica unificata, si consiglia di utilizzare nomi significativi per ognuno di essi. La lunghezza massima per il nome di un gateway IP di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Indirizzo**   È possibile configurare un gateway IP di messaggistica unificata con un indirizzo IP o un nome di dominio completo (FQDN). Utilizzare questa casella per specificare l'indirizzo IP configurato nel gateway VoIP, nel PBX abilitato per SIP, nel PBX IP o in SBC, oppure specificare un FQDN. Questa casella accetta solo FQDN validi immessi nel formato corretto.
        
        In questa casella è possibile immettere caratteri alfabetici e numerici. Sono supportati indirizzi IPv4, indirizzi IPv6 e nomi di dominio completi (FQDN). Se si desidera utilizzare MTLS (Mutual Transport Layer Security) tra un gateway IP di messaggistica unificata e un dial plan in funzione in modalità protetta o protetta con SIP, è necessario configurare il gateway IP di messaggistica unificata con un nome di dominio completo. È necessario configurarlo anche per rimanere in ascolto sulla porta 5061 e verificare che un gateway VoIP o un PBX IP sia stato configurato per l'ascolto delle richieste MTLS sulla porta 5061. Per configurare un gateway IP di messaggistica unificata, eseguire questo comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        Se si utilizza un FQDN, è inoltre necessario verificare che sia stato correttamente configurato un record host DNS per il gateway VoIP, affinché il nome host venga risolto in un indirizzo IP. Inoltre, se si utilizza un FQDN anziché un indirizzo IP, e la configurazione DNS per il gateway IP di messaggistica unificata è stata modificata, è necessario disabilitare e quindi abilitare di nuovo il gateway IP di messaggistica unificata per avere la certezza che le informazioni di configurazione del gateway IP di messaggistica unificata vengano aggiornate correttamente.
    
      - **Dial plan di messaggistica unificata**   Fare clic su **Sfoglia** per selezionare il dial plan di messaggistica unificata che si desidera associare al gateway IP di messaggistica unificata. Selezionando un dial plan di messaggistica unificata da associare a un gateway IP di messaggistica unificata, viene inoltre creato un gruppo di risposta di messaggistica unificata predefinito associato al dial plan di messaggistica unificata selezionato. Se non si seleziona alcun dial plan di messaggistica unificata, sarà necessario creare manualmente un gruppo di risposta di messaggistica unificata e successivamente associarlo al gateway IP di messaggistica unificata creato.

3.  
    
    Fare clic su **Salva**.

## Creazione di un gateway IP di messaggistica unificata tramite Shell

In questo esempio viene creato un gateway IP di messaggistica unificata denominato `MyUMIPGateway` che consente ai server di Exchange di iniziare ad accettare le chiamate provenienti da un gateway VoIP, PBX abilitato per SIP, IP PBX o SBC con indirizzo IP 10.10.10.1.

    New-UMIPGateway -Name MyUMIPGateway -Address 10.10.10.1

In questo esempio viene creato un gateway IP di messaggistica unificata denominato `MyUMIPGateway` che consente ai server di Exchange di iniziare ad accettare le chiamate provenienti da un gateway VoIP, PBX abilitato per SIP, IP PBX o SBC con FDQN MyUMIPGateway.contoso.com e in ascolto sulla porta 5061.

    New-UMIPGateway -Name MyUMIPGateway -Address "MyUMIPGateway.contoso.com" -Port 5061

In questo esempio viene creato un gateway IP di messaggistica unificata denominato `MyUMIPGateway` che impedisce al gateway IP di messaggistica unificata di accettare o inviare chiamate, di impostare un indirizzo IPv6 e di consentire al gateway IP di messaggistica unificata di utilizzare gli indirizzi IPv4 e IPv6.

    New-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

