---
title: 'Abilitazione di POP3 in Exchange 2013: Exchange 2013 Help'
TOCTitle: Abilitazione di POP3
ms:assetid: e226a5f1-429d-4046-b925-da6cc151709e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124934(v=EXCHG.150)
ms:contentKeyID: 50481941
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Abilitazione di POP3 in Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-03-28_

Informazioni su come abilitare la connettività client POP3 in Exchange 2016 utilizzando Microsoft Management Console (MMC) o Exchange Management Shell (EMS).

Quando si installa Exchange Server 2016, la connettività del client POP3 non è abilitata. Per abilitare la connettività client POP3, è necessario avviare due servizi POP3, i servizi Microsoft Exchange POP3 e Backend POP3 di Microsoft Exchange. Quando si abilita POP3, Exchange 2016 accetterà le comunicazioni client POP3 non protette sulle porte 110 e 995 utilizzando il protocollo SSL (Secure Sockets Layer).

I servizi backend POP3 e POP3 si gestiscono sullo stesso computer Exchange 2016 che esegue il ruolo del server Cassette postali. In Exchange 2016, i servizi Accesso client fanno parte del ruolo del server Cassette postali, quindi non è più necessario gestirli separatamente.

Per ulteriori informazioni su come configurare POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni POP3 e IMAP4" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo di Microsoft Management Console (MMC) per abilitare POP3

Sul computer che esegue il ruolo del server Cassette postali:

1.  Nello snap-in **Servizi**, nell'albero della console, scegliere **Servizi (computer locale)**.

2.  Nel riquadro dei risultati, fare clic con il pulsante destro del mouse su **Microsoft Exchange POP3**, quindi scegliere **Proprietà**.

3.  Nel riquadro dei risultati, fare clic con il pulsante destro del mouse su **Backend POP3 di Microsoft Exchange**, quindi scegliere **Proprietà**.

4.  Nella scheda **Generale**, in **Tipo di avvio**, selezionare **Automatico** e quindi scegliere **Applica**.

5.  In **Stato del servizio** fare clic su **Avvia** e quindi su **OK**.

## Abilitazione di POP3 tramite Exchange Management Shell

Sul computer che esegue il ruolo del server Cassette postali:

1.  Impostare il servizio POP3 di Microsoft Exchange per l'avvio automatico.
    
    ```powershell
        Set-service msExchangePOP3 -startuptype automatic
    ```

2.  Avviare il servizio Microsoft Exchange POP3.
    
    ```powershell
        Start-service msExchangePOP3
    ```

3.  Impostare il servizio Backend POP3 di Microsoft Exchange per l'avvio automatico.
    
    ```powershell
        Set-service msExchangePOP3BE -startuptype automatic
    ```

4.  Avviare il servizio Backend POP3 di Microsoft Exchange.
    
    ```powershell
        Start-service msExchangePOP3BE
    ```

## Come verificare se l'operazione ha avuto esito positivo

Sul server cassette postali di Exchange 2016, aprire Task Manager Windows. Nella scheda **Servizi** lo stato di **MSExchangePOP3** e **MSExchangePOP3BE** sarà visualizzato come **In esecuzione** se POP3 è abilitato.

