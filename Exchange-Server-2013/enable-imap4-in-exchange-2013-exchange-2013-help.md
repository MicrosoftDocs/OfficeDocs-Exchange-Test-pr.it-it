---
title: 'Abilitazione di IMAP4 in Exchange 2013: Exchange 2013 Help'
TOCTitle: Abilitazione di IMAP4
ms:assetid: c1ae10dd-14da-4400-b38d-2aeafde8abe6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124489(v=EXCHG.150)
ms:contentKeyID: 50481589
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Abilitazione di IMAP4 in Exchange 2013

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-06-02_

Informazioni su come abilitare la connettività client IMAP4 in Exchange 2016 utilizzando Microsoft Management Console (MMC) o Exchange Management Shell (EMS).

Quando si installa Exchange Server 2016, la connettività client IMAP4 non è abilitata. Per abilitare la connettività client IMAP4, è necessario avviare due servizi IMAP, il servizio IMAP4 di Microsoft Exchange e il servizio back-end IMAP4 di Microsoft Exchange. Quando si abilita IMAP4, Exchange 2016 accetta le comunicazioni client IMAP4 non protette sulla porta 143 e sulla porta 993 utilizzando SSL (Secure Sockets Layer).

I servizi backend IMAP4 e IMAP4 si gestiscono sullo stesso computer Exchange 2016 che esegue il ruolo del server Cassette postali. In Exchange 2016, i servizi Accesso client fanno parte del ruolo del server Cassette postali, quindi non è più necessario gestirli separatamente.

Per ulteriori informazioni su come configurare POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni POP3 e IMAP4" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Quale operazione si desidera effettuare?

## Utilizzo di Microsoft Management Console (MMC) per abilitare IMAP4

Sul computer che esegue il ruolo del server Cassette postali:

1.  Nello snap-in **Servizi**, nell'albero della console, scegliere **Servizi (computer locale)**.

2.  Nel riquadro dei risultati, fare clic con il pulsante destro del mouse su **Microsoft Exchange - IMAP4**, quindi su **Proprietà**.

3.  Nel riquadro dei risultati fare clic con il pulsante destro del mouse su **Microsoft Exchange - back-end IMAP4**, quindi su **Proprietà**.

4.  Nella scheda **Generale**, in **Tipo di avvio**, selezionare **Automatico** e quindi scegliere **Applica**.

5.  In **Stato del servizio** fare clic su **Avvia** e quindi su **OK**.

## Utilizzo di Exchange Management Shell per abilitare IMAP4

Sul computer che esegue il ruolo del server Cassette postali:

1.  Impostare il servizio IMAP4 di Microsoft Exchange per l'avvio automatico.
    
        Set-service msExchangeIMAP4 -startuptype automatic

2.  Avviare il servizio IMAP4 di Microsoft Exchange.
    
        Start-service msExchangeIMAP4

3.  Impostare il servizio back-end IMAP4 di Microsoft Exchange per l'avvio automatico.
    
        Set-service msExchangeIMAP4BE -startuptype automatic

4.  Avviare il servizio back-end IMAP4 di Microsoft Exchange.
    
        Start-service msExchangeIMAP4BE

## Come verificare se l'operazione ha avuto esito positivo

Sul server Cassette postali di Exchange 2016, aprire Windows Task Manager. Nella scheda **Servizi**, lo stato di **MSExchangeIMAP4** e **MSExchangeIMAP4BE** verrà visualizzato come **In esecuzione** se IMAP4 è abilitato.

