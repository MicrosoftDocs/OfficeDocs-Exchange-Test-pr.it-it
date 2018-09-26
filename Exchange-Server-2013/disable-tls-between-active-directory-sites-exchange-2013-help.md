---
title: 'Disabilitare TLS tra siti Active Directory: Exchange 2013 Help'
TOCTitle: Disabilitare TLS tra siti Active Directory
ms:assetid: 1e1a0acf-24e7-4f94-9b33-603a4e0a812c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd876856(v=EXCHG.150)
ms:contentKeyID: 52063049
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare TLS tra siti Active Directory

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-19_

Microsoft Exchange Server 2013 supporta la disabilitazione di TLS per le comunicazioni SMTP tra i server Cassette postali in alcune topologie in cui vengono utilizzati i dispositivi WOC che comprimono il traffico SMTP.

Questo argomento offre istruzioni dettagliate su come configurare il servizio di trasporto nei server Cassette postali per disabilitare TLS e per garantire che la topologia di instradamento di Active Directory sia configurata per instradare correttamente i messaggi. Per ulteriori informazioni su questo scenario, vedere [Scenario: Configurare Exchange per supportare i controller di ottimizzazione della WAN](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di questa attività: 60 minuti.

  - Anche se i singoli passaggi di configurazione in questo scenario possono essere completati con meno diritti, per completare tutte le attività dello scenario end-to-end, l'account deve essere un membro del gruppo di ruoli Gestione organizzazione.

  - Verificare di disabilitare TLS solo sulle connessioni che passano attraverso i dispositivi WOC.

  - Questa procedura richiede che Exchange 2013 sia visualizzata in più siti di Active Directory, con almeno un sito connesso ad altri siti tramite un collegamento WAN.

  - Questa procedura richiede che i dispositivi WOC vengano distribuiti per comprimere il traffico SMTP tramite un collegamento WAN.

  - Questa procedura richiede che esista un percorso del flusso di messaggi logico per Exchange che passi sul collegamento WAN in cui sono distribuiti i dispositivi WOC.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Per saperne di più

## Passaggio 1: utilizzare Shell per configurare il servizio di trasporto nel server Cassette postali affinché utilizzi l'autenticazione a Exchange Server downgrade

Per configurare il servizio di trasporto in un server Cassette postali per utilizzare l'autenticazione al server Exchange downgrade, eseguire il seguente comando:

```powershell
Set-TransportService <ServerIdentity> -UseDowngradedExchangeServerAuth $true
```

In questo esempio la modifica di configurazione viene apportata al server Mailbox01.

```powershell
Set-TransportService Mailbox01 -UseDowngradedExchangeServerAuth $true
```

## Passaggio 2: creare un connettore di ricezione dedicato nel server Cassette postali per il sito di Active Directory di destinazione

## Creazione del connettore di ricezione tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Flusso di posta** \> **Connettori di ricezione**,quindi fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

2.  Nella prima pagina della procedura guidata **Nuovo connettore di ricezione**, immettere i seguenti valori
    
      - **Nome**   Immettere un valore descrittivo.
    
      - **Tipo**   Interno
    
    Al termine, scegliere il pulsante **Avanti**.

3.  Nella seconda pagina della procedura guidata **Nuovo connettore di ricezione**, nella sezione **Impostazioni remote**, immettere l'indirizzo IP o gli intervalli di indirizzi IP per il sito di Active Directory di destinazione. Al termine, fare clic su **Fine**.

## Utilizzo di Shell per creare un connettore di ricezione

Per creare un connettore di ricezione nel server Cassette postali, eseguire il comando riportato di seguito:

```powershell
    New-ReceiveConnector -Name <Name> -Server <ServerIdentity> -RemoteIPRanges <IPAddressRange> -Internal
```

In questo esempio viene creato il connettore di ricezione denominato WAN nel server Mailbox01 con le seguenti impostazioni:

  - Il parametro *RemoteIPRanges* è impostato su 10.0.2.0/24. Questo intervallo di indirizzi IP deve corrispondere al sito di Active Directory remoto da cui il connettore di ricezione riceverà le connessioni non crittografate. Se esiste più di una subnet IP nel sito remoto, è possibile immetterle tutte separandole con la virgola.

  - Il tipo di utilizzo è impostato su Interno.

<!-- end list -->

```powershell
New-ReceiveConnector -Name WAN -Server Hub01 -RemoteIPRanges 10.0.2.0/24 -Internal
```

## Passaggio 3: utilizzare Shell per disabilitare TLS nel connettore di ricezione dedicato

Per disabilitare TLS su un singolo connettore di ricezione, eseguire il comando riportato di seguito:

```powershell
Set-ReceiveConnector <ReceiveConnectorIdentity> -SuppressXAnonymousTLS $true
```

In questo esempio viene disabilitato TLS sul connettore di ricezione WAN nel server Cassette postali denominato Mailbox01.

```powershell
Set-ReceiveConnector Mailbox01\WAN -SuppressXAnonymousTLS $true
```

## Passaggio 4: utilizzare Shell per designare i siti di Active Directory come siti hub

Per designare un sito di Active Directory come sito hub, eseguire il comando riportato di seguito:

```powershell
Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true
```

È necessario effettuare questa procedura una volta in ogni sito di Active Directory che contiene server Cassette postali che partecipano nel traffico non crittografato.

Con questo esempio il sito di Active Directory denominato Central Office Site 1 viene configurato come sito hub.

```powershell
Set-AdSite "Central Office Site 1" -HubSiteEnabled $true
```

## Passaggio 5: utilizzare Shell per configurare il percorso di instradamento meno costoso attraverso la connessione WAN

A seconda di come vengono configurati i costi del collegamento al sito IP in Active Directory, questo passaggio potrebbe non essere necessario. È necessario verificare che il collegamento di rete con i dispositivi WOC distribuiti si trovino nel percorso di instradamento meno costoso. Per visualizzare i costi del collegamento al sito di Active Directory e i costi del collegamento a sito specifico per Exchange, eseguire il seguente comando:

```powershell
Get-AdSiteLink
```

Se il collegamento di rete con i dispositivi WOC distribuiti si trova nel percorso di instradamento meno costoso, sarà necessario assegnare un costo specifico per Exchange al collegamento al sito IP specifico per garantire che i messaggi vengano instradati correttamente. Per ulteriori informazioni su questo particolare problema, vedere la sezione relativa alla configurazione dei costi del collegamento al sito di Active Directory specifico per Exchange" in [Scenario: Configurare Exchange per supportare i controller di ottimizzazione della WAN](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md).

In questo esempio viene configurato un costo specifico di Exchange pari a 15 sul collegamento al sito IP denominato Branch Office 2-Branch Office 1.

```powershell
Set-AdSiteLink "Branch Office 2-Branch Office 1" -ExchangeCost 15
```

