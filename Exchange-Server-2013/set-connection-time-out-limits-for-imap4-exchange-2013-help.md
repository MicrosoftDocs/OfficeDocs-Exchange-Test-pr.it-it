---
title: 'Impostare limiti di timeout di connessione per IMAP4: Exchange 2013 Help'
TOCTitle: Impostare limiti di timeout di connessione per IMAP4
ms:assetid: 6b6a5bd1-a878-4a70-8e21-14d5042a58f1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998665(v=EXCHG.150)
ms:contentKeyID: 50555610
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare limiti di timeout di connessione per IMAP4

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-28_

È possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per configurare i limiti di timeout per le connessioni IMAP4 inattive autenticate e non autenticate.

Per ulteriori informazioni su IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni IMAP4" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Impostazione dei limiti di timeout delle connessioni per IMAP4 tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** **\>** **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **IMAP4**.

4.  Scorrere verso il basso e fare clic su **Altre opzioni**.

5.  Sotto **Impostazioni timeout**, utilizzare le seguenti impostazioni:
    
      - **Timeout autenticato (secondi)**    Specifica il tempo di attesa prima della chiusura di una connessione inattiva autenticata. Il valore predefinito è 1.800. I valori consentiti sono compresi tra 30 e 86.400.
    
      - **Timeout non autenticato (secondi)**    Specifica il tempo di attesa prima della chiusura di una connessione inattiva non autenticata. Il valore predefinito è 60. I valori consentiti sono compresi tra 30 e 3.600.

6.  Fare clic su **Applica**, quindi su **OK** per salvare le modifiche.

Dopo avere impostato i limiti di timeout delle connessioni per IMAP4, è necessario riavviare i servizi IMAP4 affinché le impostazioni abbiano effetto. Per informazioni su come riavviare i servizi IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Impostazione dei limiti di timeout delle connessioni per IMAP4 tramite Shell

In questo esempio viene impostato il limite di timeout per connessioni autenticate inattive.

    Set -ImapSettings -Identity CAS01 -AuthenticatedConnectionTimeout TimeValue

In questo esempio viene impostato il limite di timeout per connessioni non autenticate inattive.

    Set -ImapSettings -Identity CAS01 -PreAuthenticatedConnectionTimeout TimeValue

Dopo avere impostato i limiti di timeout delle connessioni per IMAP4, è necessario riavviare i servizi IMAP4 affinché le impostazioni abbiano effetto. Per informazioni su come riavviare i servizi IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ImapSettings](https://technet.microsoft.com/it-it/library/aa998252\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta impostazione dei limiti di connessione, effettuare una delle seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** **\>** **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **IMAP4**.

4.  Scorrere verso il basso e fare clic su **Altre opzioni**.

5.  Sotto **Impostazioni timeout**, verificare che le impostazioni di connessione siano corrette.

Oppure

1.  Eseguire il seguente comando in Shell.
    
        Get-ImapSettings | format-list

2.  Verificare che le impostazioni di connessione siano corrette.

## Ulteriori informazioni

Dopo aver impostato i limiti di timeout per l'autenticazione IMAP4, è possibile anche effettuare le seguenti operazioni:

[Abilitazione di IMAP4 in Exchange 2013](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Impostare i limiti delle connessioni per IMAP4](set-connection-limits-for-imap4-exchange-2013-help.md)

