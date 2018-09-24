---
title: 'Impostare i limiti delle connessioni per POP3: Exchange 2013 Help'
TOCTitle: Impostare i limiti delle connessioni per POP3
ms:assetid: 512d61c2-2a34-4813-92a9-875339d3388b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997988(v=EXCHG.150)
ms:contentKeyID: 50555588
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare i limiti delle connessioni per POP3

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-28_

È possibile utilizzare l'interfaccia di amministrazione di Exchange o Shell per gestire i limiti di connessione POP3 per l'organizzazione.

Se vengono specificati i limiti di connessione per POP3, è possibile selezionare i limiti di connessione per il server, un indirizzo IP o un utente specifico.

Per ulteriori informazioni su POP3, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni POP3" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Impostazione dei limiti di connessione POP3 per un server, un indirizzo IP o un utente tramite EMC

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** **\>** **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **POP3**.

4.  Scorrere verso il basso e fare clic su **Altre opzioni**.

5.  In **Limiti connessione**, utilizzare le seguenti impostazioni:
    
      - **Numero massimo di connessioni**   Specifica il numero totale di connessioni che il server specificato accetterà. Tra queste sono incluse le connessioni autenticate e non autenticate. Il valore predefinito è 2.147.483.647. I valori consentiti sono compresi tra 1 e 2.147.483.647.
    
      - **Numero massimo di connessioni da un solo indirizzo IP**   Specifica il numero di connessioni che il server Accesso client accetterà da un solo indirizzo IP. Il valore predefinito è 2.147.483.647. I valori consentiti sono compresi tra 1 e 2.147.483.647.
    
      - **Numero massimo di connessioni da un singolo utente**   Specifica il numero massimo di connessioni che il server accetterà da un particolare utente. Il valore predefinito è 16. I valori consentiti sono compresi tra 1 e 2.147.483.647.
    
      - **Dimensione massima comando (byte)**   specifica la dimensione massima di un singolo comando. Le dimensioni predefinite corrispondono a 512. I valori consentiti sono compresi tra 40 e 1.024.

6.  Fare clic su **Applica**, quindi su **OK** per salvare le modifiche.

Una volta impostati i limiti di connessione, è necessario riavviare i servizi POP3. Per informazioni su come riavviare i servizi POP3, vedere [Avviare e arrestare i servizi POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Impostazione dei limiti di connessione POP3 per un server, un indirizzo IP o un utente tramite Shell

In questo esempio viene impostato il limite di connessione per un server.

```powershell
Set-PopSettings -Identity CAS01 -MaxConnections Value
```

In questo esempio viene impostato il limite di connessione per un indirizzo IP.

```powershell
Set-PopSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value
```

In questo esempio viene impostato il limite di connessione per un utente.
```powershell
    Set-PopSettings -MaxConnectionsPerUser Value 
```
In questo esempio viene impostata la dimensione massima del comando.

```powershell
Set-PopSettings -MaxCommandSize Value
```

Una volta impostati i limiti di connessione, è necessario riavviare i servizi POP3. Per informazioni su come riavviare i servizi POP3, vedere [Avviare e arrestare i servizi POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-PopSettings](https://technet.microsoft.com/it-it/library/aa997154\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta impostazione dei limiti di connessione, effettuare una delle seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** **\>** **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **POP3**.

4.  Scorrere verso il basso e fare clic su **Altre opzioni**.

5.  Sotto **Limiti connessione**, verificare che le impostazioni di connessione siano corrette.

Oppure

1.  Eseguire il seguente comando in Shell.
    
    ```powershell
        Get-PopSettings | format-list
    ```

2.  Verificare che le impostazioni di connessione siano corrette.

## Ulteriori informazioni

Una volta impostati i limiti di connessione POP3 per un server, un indirizzo IP o un utente, è possibile anche effettuare le seguenti operazioni:

[Abilitazione di POP3 in Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[Impostare limiti di timeout di connessione per POP3](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

