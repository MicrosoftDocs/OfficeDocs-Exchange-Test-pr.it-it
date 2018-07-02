---
title: 'Gestire un gateway IP di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Gestire un gateway IP di messaggistica unificata
ms:assetid: 387e540f-8c59-42d2-a423-99fcf97e00aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997283(v=EXCHG.150)
ms:contentKeyID: 50480354
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMIPGatewayGeneralPropertyPageControl
ms.translationtype: MT
---

# Gestire un gateway IP di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

Una volta creato un gateway IP di messaggistica unificata, è possibile visualizzare o configurare diverse impostazioni. Ad esempio, è possibile configurare l'indirizzo IP o un nome di dominio completo (FQDN), configurare le impostazioni delle chiamate in uscita e abilitare o disabilitare l'indicatore di messaggio in attesa.

Per altre attività di gestione relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione di un gateway IP di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Visualizzazione o configurazione delle proprietà del gateway IP di messaggistica unificata tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**. Nella visualizzazione elenco, selezionare il gateway IP di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  
    
    Utilizzare la pagina **Gateway IP di messaggistica unificata** per visualizzare e configurare le impostazioni per il gateway IP di messaggistica unificata. È possibile visualizzare o configurare le seguenti impostazioni:
    
      - **Stato**   In questo campo di sola visualizzazione, viene riportato lo stato del gateway IP di messaggistica unificata.
    
      - **Nome**   Utilizzare questa casella per specificare un nome univoco per il gateway IP di messaggistica unificata. Si tratta del nome che verrà visualizzato nell'interfaccia di amministrazione di Exchange. Qualora fosse necessario modificare il nome visualizzato del gateway IP di messaggistica unificata dopo la sua creazione, occorre innanzitutto eliminare il gateway IP di messaggistica unificata esistente e, quindi, crearne un altro con il nome corretto. Benché il nome del gateway IP di messaggistica unificata sia obbligatorio viene utilizzato solo ai fini della visualizzazione. Dal momento che l'organizzazione può utilizzare più gateway IP di messaggistica unificata, si consiglia di utilizzare nomi significativi per ognuno di essi. La lunghezza massima per il nome di un gateway IP di messaggistica unificata è di 64 caratteri e può contenere spazi.
    
      - **Indirizzo**   È possibile configurare un gateway IP di messaggistica unificata con un indirizzo IP o un nome di dominio completo (FQDN). Utilizzare questa casella per specificare l'indirizzo IP o nome di dominio completo configurato nel gateway VoIP, nel PBX abilitato per SIP, IP PBX o in SBC.
        
        In questa casella è possibile immettere caratteri alfabetici e numerici. Sono supportati indirizzi IPv4, indirizzi IPv6 e nomi di dominio completi (FQDN). Se si utilizza un nome di dominio completo, è necessario anche verificare di aver configurato correttamente un record host DNS per il gateway VoIP in modo tale che il nome host venga risolto correttamente in un indirizzo IP. Inoltre, se si utilizza un FQDN anziché un indirizzo IP, e la configurazione DNS per il gateway IP di messaggistica unificata è stata modificata, è necessario disabilitare e quindi abilitare di nuovo il gateway IP di messaggistica unificata per avere la certezza che le informazioni di configurazione del gateway IP di messaggistica unificata vengano aggiornate correttamente.
        
        Se si desidera utilizzare MTLS (Mutual Transport Layer Security) tra un gateway IP di messaggistica unificata e un dial plan in funzione in modalità protetta o protetta con SIP, è necessario configurare il gateway IP di messaggistica unificata con un nome di dominio completo. È necessario configurarlo anche per l'ascolto sulla porta 5061 e verificare che qualsiasi gateway IP o IP PBX sia stato configurato per l'ascolto delle richieste MTLS sulla porta 5061. Per configurare un gateway IP di messaggistica unificata, eseguire questo comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
    
      - **Consenti chiamate in uscita tramite questo gateway IP di messaggistica unificata**   Selezionare tale casella di controllo per consentire al gateway IP di messaggistica unificata di accettare ed elaborare le chiamate in uscita. Tale impostazione non influisce sul trasferimento delle chiamate o sulle chiamate in entrata da un gateway VoIP.
        
        Quando si crea un gateway IP di messaggistica unificata, questa impostazione è abilitata per impostazione predefinita. Se si disabilita tale impostazione, gli utenti associati al dial plan non saranno in grado di effettuare chiamate in uscita tramite il gateway VoIP, IP PBX, o SBC definito nel campo **Indirizzo**.
    
      - **Consenti indicatore di messaggi in attesa**   Selezionare tale casella di controllo per consentire l'invio di notifiche sui sistemi di caselle vocali agli utenti per le chiamate derivanti dal gateway IP di messaggistica unificata. Tale impostazione consente al gateway IP di messaggistica unificata di ricevere e inviare messaggi SIP NOTIFY per gli utenti. Questa 'impostazione viene abilitata per impostazione predefinita e consente di inviare notifiche sui messaggi in attesa agli utenti.
        
        L'indicatore di messaggi in attesa può far riferimento a qualsiasi meccanismo indicante l'esistenza di un nuovo messaggio o di un messaggio non ascoltato. È possibile trovare la segnalazione che è arrivato un nuovo messaggio vocale in Posta in arrivo in client quali Outlook e Outlook Web App. Può avere la forma di un SMS o di un messaggio di testo inviato a un cellulare registrato, di una chiamata esterna effettuata da un server di Exchange a un numero preconfigurato o di un telefono da scrivania accesa per un utente.

## Configurazione delle proprietà di un gateway IP di messaggistica unificata tramite Shell

In questo esempio, viene modificato l'indirizzo IP di un gateway IP di messaggistica unificata denominato `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

Con questo esempio viene impedito al gateway IP di messaggistica unificata denominato `MyUMIPGateway` di accettare le chiamate in arrivo e non vengono consentite le chiamate in uscita.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com -Status 2 -OutcallsAllowed $false

Con questo esempio il gateway IP di messaggistica unificata viene abilitato alla funzione di simulatore del gateway VoIP e può essere utilizzato con il cmdlet **Test-UMConnectivity**.

    Set-UMIPGateway -Identity MyUMIPGateway -Simulator $true


> [!IMPORTANT]
> Trascorre un periodo di latenza prima che tutte le modifiche apportate alla configurazione di un gateway IP di messaggistica unificata vengano replicate a tutti i server di Exchange presenti nello stesso dial plan di messaggistica unificata del gateway IP di messaggistica unificata.



In questo esempio, al gateway IP di messaggistica unificata di nome `MyUMIPGateway` viene impedito di accettare chiamate in arrivo, le chiamate in uscita vengono bloccate, viene impostato un indirizzo IPv6 e al gateway IP di messaggistica unificata viene consentito di utilizzare sia indirizzi IPv4 che indirizzi IPv6.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## Visualizzazione delle proprietà di un gateway IP di messaggistica unificata tramite Shell

In questo esempio, viene visualizzato un elenco formattato di tutti i gateway IP di messaggistica unificata della foresta Active Directory.

    Get-UMIPGateway |Format-List

Nel secondo esempio vengono visualizzate le proprietà per un gateway IP di messaggistica unificata denominato `MyUMIPGateway`.

    Get-UMIPGateway -Identity MyUMIPGateway

Nel terzo esempio vengono visualizzati tutti i gateway IP di messaggistica unificata, compresi i simulatori di gateway VoIP della foresta Active Directory.

    Get-UMIPGateway -IncludeSimulator $true

