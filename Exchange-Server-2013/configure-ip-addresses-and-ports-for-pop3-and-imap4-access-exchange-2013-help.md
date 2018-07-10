---
title: "Configurare gli indirizzi IP e porte per l'accesso POP3 e IMAP4: Exchange 2013 Help"
TOCTitle: Configurare gli indirizzi IP e porte per l'accesso POP3 e IMAP4
ms:assetid: 8292747b-6626-4d7f-ba73-1e17f5d99fa4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123530(v=EXCHG.150)
ms:contentKeyID: 50555619
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare gli indirizzi IP e porte per l'accesso POP3 e IMAP4

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-28_

L'interfaccia di amministrazione di Exchange e la shell consentono di configurare i servizi Microsoft Exchange POP3 e IMAP4 per l'utilizzo di indirizzi IP e porte diverse da quelle stabilite nelle impostazioni predefinite.


> [!NOTE]
> Immettere gli indirizzi&nbsp;IP e gli intervalli di indirizzi&nbsp;IP nel formato IPv4 (IPv4, Internet Protocol Version&nbsp;4), nel formato IPv6, (IPv6, Internet Protocol Version&nbsp;6) o in entrambi i formati. L'installazione predefinita di Windows Server 2008 prevede il supporto per IPv4 e IPv6.



Per ulteriori informazioni su POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni POP3" e "Impostazioni IMAP4" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Configurazione degli indirizzi IP e delle porte per POP3

## Configurazione degli indirizzi IP e delle porte per POP3 tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** **\>** **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **POP3**.

4.  In **Connessioni TLS o non crittografate** fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

5.  Nella pagina **Aggiungi indirizzo IP**, in **Indirizzo IP** scegliere una delle seguenti opzioni:
    
      - **Tutti gli indirizzi IPv4 disponibili**   Consente di utilizzare tutti gli indirizzi IP IPv4 per un server.
    
      - **Tutti gli indirizzi IPv6 disponibili**   Consente di utilizzare tutti gli indirizzi IP IPv6 per un server.
    
      - **Specifica l'indirizzo IP** Consente di utilizzare un indirizzo IP specifico.

6.  In **Porta** immettere un numero di porta o accettare la porta predefinita.

7.  Fare clic su **Salva** per salvare le modifiche.

Dopo aver configurato l'indirizzo IP e le impostazioni della porta per POP3, è necessario riavviare il servizio POP3 per rendere effettive le impostazioni. Per informazioni su come riavviare il servizio POP3, vedere[Avviare e arrestare i servizi POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Configurazione degli indirizzi IP e delle porte per POP3 tramite Shell

Con questo esempio vengono impostati l'indirizzo IP e la porta per la comunicazione con Exchange utilizzando POP3 con SSL (SSL, Secure Sockets Layer).

    Set-PopSettings -SSLBindings: IPaddress:Port

Con questo esempio vengono impostati l'indirizzo IP e la porta per la comunicazione con Exchange utilizzando POP3 senza alcuna crittografia o con la crittografia TLS (TLS, Transport Layer Security).

    Set-PopSettings -UnencryptedOrTLSBindings IPaddress:Port

Dopo aver configurato l'indirizzo IP e le impostazioni della porta per POP3, è necessario riavviare il servizio POP3 per rendere effettive le impostazioni. Per informazioni su come riavviare il servizio POP3, vedere[Avviare e arrestare i servizi POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-PopSettings](https://technet.microsoft.com/it-it/library/aa997154\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che l'indirizzo IP POP 3 e le impostazioni della porta siano state modificate su un server, procedere come segue.

1.  Eseguire il seguente comando in Shell.
    
        Get-PopSettings | format-list

2.  Verificare che le impostazioni di *UnencryptedOrTLSBindings* e *SSLBindings* siano corrette.

## Configurazione degli indirizzi IP e delle porte per IMAP4

## Configurazione degli indirizzi IP e delle porte per IMAP4 tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** **\>** **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **IMAP4**.

4.  Per configurare le impostazioni delle connessioni TLS o non crittografate, in **Connessioni TLS o non crittografate** fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per modificare le impostazioni delle connessioni SSL (Secure Sockets Layer), in **Connessioni SSL (Secure Sockets Layer)** fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

5.  Nella pagina **Aggiungi indirizzo IP**, in **Indirizzo IP** scegliere una delle seguenti opzioni:
    
      - **Tutti gli indirizzi IPv4 disponibili**   Consente di utilizzare tutti gli indirizzi IP IPv4 per un server.
    
      - **Tutti gli indirizzi IPv6 disponibili**   Consente di utilizzare tutti gli indirizzi IP IPv6 per un server.
    
      - **Specifica l'indirizzo IP** Consente di utilizzare un indirizzo IP specifico.

6.  In **Porta** immettere un numero di porta o accettare la porta predefinita.

7.  Fare clic su **Salva** per salvare le modifiche.

Dopo aver configurato l'indirizzo IP e le impostazioni della porta per IMAP4, è necessario riavviare i servizi IMAP4 per rendere effettive le impostazioni. Per informazioni su come riavviare i servizi IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Configurazione degli indirizzi IP e delle porte per IMAP4 tramite Shell

Con questo esempio vengono impostati l'indirizzo IP e la porta per la comunicazione con Exchange utilizzando IMAP4.

    Set-ImapSettings -SSLBindings: IPaddress:Port

Con questo esempio vengono impostati l'indirizzo IP e la porta per la comunicazione con Exchange utilizzando IMAP4 senza alcuna crittografia o con la crittografia TLS (Transport Layer Security).

    Set-ImapSettings -UnencryptedOrTLSBindings IPaddress:Port 

Dopo aver configurato l'indirizzo IP e le impostazioni della porta per IMAP4, è necessario riavviare il servizio IMAP4 per rendere effettive le impostazioni. Per informazioni su come riavviare il servizio IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ImapSettings](https://technet.microsoft.com/it-it/library/aa998252\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che l'indirizzo IP IMAP4 e le impostazioni della porta siano state modificate su un server, procedere come segue.

1.  Eseguire il seguente comando in Shell.
    
        Get-ImapSettings | format-list

2.  Verificare che le impostazioni di *UnencryptedOrTLSBindings* e *SSLBindings* siano corrette.

## Ulteriori informazioni

Una volta configurati gli indirizzi IP e le porte per POP3 e IMAP4, è possibile anche:

[Abilitazione di IMAP4 in Exchange 2013](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Abilitazione di POP3 in Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

