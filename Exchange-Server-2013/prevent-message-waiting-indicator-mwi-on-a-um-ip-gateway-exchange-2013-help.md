---
title: 'Impedire a messaggi in attesa indicatore (MWI) su un gateway IP di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Impedire a messaggi in attesa indicatore (MWI) su un gateway IP di messaggistica unificata
ms:assetid: 7af6d094-199f-4134-a25d-9fc7e9c05fe1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673536(v=EXCHG.150)
ms:contentKeyID: 50481026
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impedire a messaggi in attesa indicatore (MWI) su un gateway IP di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-21_

È possibile impedire l'invio agli utenti delle notifiche tramite posta vocale per le chiamate ricevute tramite un gateway IP di messaggistica unificata. Se abilitata, questa impostazione consente al gateway IP di messaggistica unificata di ricevere e inviare messaggi SIP NOTIFY per gli utenti. L'indicatore di messaggio in attesa (MWI) è abilitato per impostazione predefinita e consente l'invio delle notifiche di messaggio in attesa gli utenti, ma questo indicatore può essere disabilitato a seconda delle proprio esigenze.

Un indicatore di messaggio in attesa segnala a un utente la presenza di un messaggio vocale nuovo o non ascoltato. Viene visualizzato nella Posta in arrivo nei client quali Outlook e Outlook Web App. Può anche trattarsi di un SMS inviato a un cellulare registrato, una chiamata in uscita effettuata da un server Exchange a un numero configurato per la riproduzione dei nuovi messaggi oppure di una spia luminosa accesa sul telefono da scrivania di un utente.


> [!TIP]
> Le notifiche MWI possono anche essere abilitate e disabilitate sulla base di un criterio per le cassette postali di messaggistica unificata di un gruppo di utenti.



Per altre attività di gestione relative ai gateway IP di messaggistica unificata, vedere [Procedure di gateway IP di messaggistica unificata](um-ip-gateway-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gateway IP di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione di un gateway IP di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Disabilitazione di Message Waiting Indicator tramite l'interfaccia di amministrazione di Exchange

1.  Nell'Interfaccia di amministrazione di Exchange, andare a **Messaggistica unificata** \> **Gateway IP di messaggistica unificata**, selezionare il gateway IP di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Gateway IP di messaggistica unificata**, deselezionare la casella di controllo **Consenti l'indicatore di messaggi in attesa**.

3.  Fare clic su **Salva**.

## Disabilitazione di Message Waiting Indicator tramite Shell

In questo esempio, agli utenti associati al gateway IP di messaggistica unificata `MyUMIPGateway` con indirizzo IP 10.10.10.1 viene evitato di visualizzare l'indicatore di messaggio in attesa.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1 -MessageWaitingIndicatorAllowed $false

