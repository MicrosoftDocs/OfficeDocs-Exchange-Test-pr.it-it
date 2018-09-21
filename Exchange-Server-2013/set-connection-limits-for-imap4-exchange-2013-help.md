---
title: 'Impostare i limiti delle connessioni per IMAP4: Exchange 2013 Help'
TOCTitle: Impostare i limiti delle connessioni per IMAP4
ms:assetid: 8e3aa366-e77c-4c70-b78d-ddbb178cb521
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123712(v=EXCHG.150)
ms:contentKeyID: 50555636
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare i limiti delle connessioni per IMAP4

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-28_

Per gestire i limiti di connessione IMAP4 per l'organizzazione, è possibile utilizzare l'interfaccia di amministrazione di Exchange o la shell.

Quando si specificano i limiti di connessione per IMAP4, è possibile selezionare i limiti di connessione per il server, per l'indirizzo IP o per un utente specifico.

Per ulteriori informazioni su IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni IMAP4" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Impostazione dei limiti di connessione IMAP4 per un server, un indirizzo IP o un utente tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** **\>** **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **IMAP4**.

4.  Scorrere verso il basso e fare clic su **Altre opzioni**.

5.  In **Limiti connessione**, utilizzare le seguenti impostazioni:
    
      - **Numero massimo di connessioni**   Consente di specificare il numero totale di connessioni accettate dal server specificato. Tra queste sono incluse le connessioni autenticate e non autenticate. Il valore predefinito è 2.147.483.647. I valori consentiti sono compresi tra 1 e 2.147.483.647.
    
      - **Numero massimo di connessioni da un solo indirizzo IP**   Consente di specificare il numero di connessioni che il server accetterà da un unico indirizzo IP. Il valore predefinito è 2.147.483.647. I valori consentiti sono compresi tra 1 e 2.147.483.647.
    
      - **Numero massimo di connessioni da un singolo utente**   Consente di specificare il numero di connessioni che il server accetterà da un determinato utente. Il valore predefinito è 16. I valori consentiti sono compresi tra 1 e 2.147.483.647.
    
      - **Dimensione massima comando (in byte)**   Consente di specificare la dimensione massima di un singolo comando. Le dimensioni predefinite corrispondono a 10.240. I valori consentiti sono compresi tra 1.024 e 16.384.

6.  Fare clic su **Applica**, quindi su **OK** per salvare le modifiche.

Dopo aver impostato i limiti di connessione, è necessario riavviare i servizi IMAP4. Per informazioni su come riavviare i servizi IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Impostazione dei limiti di connessione IMAP4 per un server, un indirizzo IP o un utente tramite Shell

In questo esempio viene impostato il limite di connessione per un server.

```powershell
Set-ImapSettings -Identity CAS01 -MaxConnections Value
```

In questo esempio viene impostato il limite di connessione per un indirizzo IP.

```powershell
Set-ImapSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value
```

In questo esempio viene impostato il limite di connessione per un utente.

```powershell
Set-ImapSettings -MaxConnectionsPerUser Value
```

In questo esempio viene impostata la dimensione massima del comando.

```powershell
Set-ImapSettings -MaxCommandSize Value
```

Dopo avere impostato i limiti di connessione, è necessario riavviare i servizi IMAP4. Per informazioni su come riavviare i servizi IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ImapSettings](https://technet.microsoft.com/it-it/library/aa998252\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta impostazione dei limiti di connessione, effettuare una delle seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** **\>** **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **IMAP4**.

4.  Scorrere verso il basso e fare clic su **Altre opzioni**.

5.  In **Limiti di connessione** verificare che le impostazioni di connessione siano corrette.

Oppure

1.  Eseguire il seguente comando in Shell.
    
    ```powershell
Get-ImapSettings | format-list
```

2.  Verificare che le impostazioni di connessione siano corrette.

## Ulteriori informazioni

Dopo aver impostato i limiti di connessione IMAP4 per un server, un indirizzo IP o un utente, è possibile anche effettuare le seguenti operazioni:

[Abilitazione di IMAP4 in Exchange 2013](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Impostare limiti di timeout di connessione per IMAP4](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

