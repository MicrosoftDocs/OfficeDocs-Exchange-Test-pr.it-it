---
title: 'Utilizzare Telnet per testare le comunicazioni SMTP: Exchange 2013 Help'
TOCTitle: Utilizzare Telnet per testare le comunicazioni SMTP
ms:assetid: 8a5f6715-baa4-48dd-8600-02c6b3d1aa9d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123686(v=EXCHG.150)
ms:contentKeyID: 52063085
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Utilizzare Telnet per testare le comunicazioni SMTP

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

In questo argomento viene descritto come utilizzare Telnet per eseguire la verifica della comunicazione SMTP (Simple Mail Transfer Protocol) tra i server di messaggistica. Per impostazione predefinita, SMTP è in ascolto sulla porta 25. Se si utilizza Telnet sulla porta 25, è possibile immettere i comandi SMTP utilizzati per connettersi a un server SMTP e inviare un messaggio esattamente come se la sessione Telnet si trovasse in un server di messaggistica SMTP. È possibile visualizzare l'esito positivo o negativo di ogni passaggio del processo di connessione e invio del messaggio.

Di seguito vengono descritti gli scenari di utilizzo di Telnet per la verifica della comunicazione SMTP in ingresso o in uscita dai server di trasporto presenti nell'organizzazione di Microsoft Exchange:

  - Connettersi al server Exchange connesso a Internet dell'organizzazione da un host ubicato all'esterno della rete perimetrale e inviare un messaggio di prova.

  - Connettersi a un server di messaggistica remoto dal server Exchange connesso a Internet dell'organizzazione e inviare un messaggio di prova.

Nella procedura di questo argomento viene illustrato come utilizzare il client Telnet, un componente compreso in Microsoft Windows. I client Telnet di terze parti possono richiedere una sintassi differente da quella del componente Telnet di Windows.

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 30 minuti

  - Le autorizzazioni di Exchange non sono applicabili alle procedure descritte in questo argomento. Queste procedure vengono eseguite nel sistema operativo del server di Exchange o di un computer client.

  - Le procedure di questo argomento sono consigliate per la connessione a e da server con connessione Internet che consentono connessioni anonime. La trasmissione dei messaggi tra server Exchange interni è crittografata e sottoposta ad autenticazione. Per utilizzare Telnet per la connessione al servizio di trasporto Hub su un server Cassette postali, sarà necessario creare un connettore di ricezione configurato per consentire l'accesso anonimo o l'autenticazione di base per ricevere messaggi. Se il connettore permette l'autenticazione di base, è necessario ricorrere a un'utilità per convertire le stringhe di testo, utilizzate per il nome utente e la password, nel formato Base64. Poiché con l'autenticazione di base il nome utente e la password sono facilmente individuabili, non è consigliabile utilizzare questo tipo di autenticazione senza crittografia.

  - Se si esegue la connessione a un server di messaggistica remoto, considerare l'opzione di eseguire le procedure di questo argomento sul server Exchange con connessione a Internet. Ciò consente di evitare il rifiuto del messaggio di prova da parte dei server di messaggistica remoti configurati per la convalida dell'indirizzo IP di origine, del corrispondente nome di dominio DNS (Domain Name System) e dell'indirizzo IP di ricerca inversa di qualsiasi host Internet che tenta di inviare un messaggio al server.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Come eseguire l'operazione?

## Passaggio 1: Installazione del client Telnet in Windows

Per impostazione predefinita, il client Telnet non è installato nella maggior parte dei client o versioni di server dei sistemi operativi Microsoft Windows. Per installarlo, vedere [Installare Client Telnet](https://go.microsoft.com/fwlink/p/?linkid=179054).

## Passaggio 2: Individuazione del nome di dominio completo o dell'indirizzo IP in un record MX di un server SMTP remoto tramite Nslookup

Per connettersi a un server SMTP di destinazione utilizzando Telnet sulla porta 25, è necessario utilizzare il nome di dominio completo (FQDN) o l'indirizzo IP del server SMTP. Se non si conosce il nome di dominio completo o l'indirizzo IP, il modo più semplice per ottenere queste informazioni è utilizzare lo strumento della riga di comando Nslookup per trovare il record MX del dominio di destinazione.

1.  Nel prompt dei comandi, digitare **nslookup** e premere INVIO. Il comando consente di aprire la sessione di Nslookup.

2.  Digitare **set type=mx**, quindi premere INVIO.

3.  Digitare **set timeout=20**, quindi premere INVIO. Per impostazione predefinita, i server DNS di Windows hanno un limite di timeout delle query DNS ricorsive di 15 secondi.

4.  Digitare il nome del dominio per cui si desidera trovare il record MX. Ad esempio, per trovare il record MX per il dominio fabrikam.com digitare, **fabrikam.com.** e premere INVIO.
    

    > [!NOTE]
    > Il punto finale (&nbsp;<STRONG>.</STRONG>&nbsp;) indica un nome di dominio completo. L'uso del punto finale impedisce l'aggiunta accidentale al nome di dominio di qualsiasi suffisso DNS predefinito configurato per la rete.

    
    L'output del comando sarà simile al seguente:

    ```powershell
        fabrikam.com mx preference=10, mail exchanger = mail1.fabrikam.com
        fabrikam.com mx preference=20, mail exchanger = mail2.fabrikam.com
        mail1.fabrikam.com internet address = 192.168.1.10
        mail2 fabrikam.com internet address = 192.168.1.20
    ```

    Come server di destinazione è possibile utilizzare qualsiasi nome host o indirizzo IP associato ai record MX. Un valore di preferenza più basso indica un server SMTP preferenziale. È possibile utilizzare più record MX e valori di preferenza diversi per il bilanciamento del carico e la tolleranza d'errore.

5.  Quando si è pronti a terminare la sessione Nslookup, digitare **exit** e premere INVIO.


> [!NOTE]
> Le restrizioni del firewall o del proxy Internet applicate alla rete interna dell'organizzazione potrebbero impedire l'utilizzo dello strumento Nslookup per eseguire query sui server DNS pubblici in Internet.



## Passaggio 3: Verifica della comunicazione SMTP tramite Telnet sulla porta 25

Nell'esempio riportato vengono utilizzati i seguenti valori:

  - **Server SMTP di destinazione**   mail1.fabrikam.com

  - **Dominio di origine**   contoso.com

  - **Indirizzo di posta elettronica del mittente**   chris@contoso.com

  - **Indirizzo di posta elettronica del destinatario**   kate@fabrikam.com

  - **Oggetto del messaggio**   Test Contoso

  - **Corpo del messaggio**   Messaggio di prova


> [!NOTE]
> <UL>
> <LI>
> <P>I comandi nel client Telnet non rilevano la distinzione tra maiuscole e minuscole. I verbi dei comandi SMTP sono resi al maiuscolo per maggiore chiarezza.</P>
> <LI>
> <P>Non è possibile utilizzare BACKSPACE dopo essersi connessi al server SMTP di destinazione durante la sessione di Telnet. Se si commette un errore durante la digitazione di un comando SMTP, è necessario premere INVIO e digitare nuovamente il comando. I comandi SMTP non riconosciuti e gli errori di sintassi causano la visualizzazione di un messaggio di errore simile al seguente:</P>
> ```powershell
>     500 5.3.3 Unrecognized command
> ```
> </LI></UL>



1.  Nel prompt dei comandi, digitare **telnet** e premere INVIO. Il comando consente di aprire la sessione di Telnet.

2.  Digitare **set localecho**, quindi premere INVIO. Questo comando opzionale consente di visualizzare i caratteri mentre vengono digitati. Questa impostazione potrebbe essere necessaria per alcuni server SMTP.

3.  Digitare **set logfile***\<nomefile\>*. Questo comando facoltativo consente alla sessione di Telnet di accedere al file di registro specificato. Se si specifica il solo nome file, il percorso del file di registro corrisponderà alla directory di lavoro corrente. Se si specifica nome file e percorso, quest'ultimo dovrà essere interno al computer locale. Sia il percorso che il nome file specificati devono essere immessi nel formato Microsoft DOS 8.3. Il percorso specificato deve essere già esistente. Se si specifica un file di registro inesistente, il file in questione verrà creato.

4.  Digitare **open mail1.fabrikam.com 25**, quindi premere INVIO.

5.  Digitare **EHLO contoso.com**, quindi premere INVIO.

6.  Digitare **MAIL FROM:chris@contoso.com**, quindi premere INVIO.

7.  Digitare **RCPT TO:kate@fabrikam.com NOTIFY=success,failure**, quindi premere INVIO. Il comando NOTIFY opzionale consente di definire gli specifici messaggi di notifica sullo stato del recapito (DSN) che il server SMTP di destinazione deve fornire al mittente. I messaggi DSN vengono definiti in RFC 1891. In questo caso, si sta richiedendo un messaggio DSN per il recapito riuscito o non riuscito di un messaggio.

8.  Digitare **DATA**, quindi premere INVIO. Si riceverà una risposta simile alla seguente:
    
    ```powershell
    354 Start mail input; end with <CLRF>.<CLRF>
    ```

9.  Digitare **Oggetto: Test Contoso** e quindi premere INVIO.

10. Premere INVIO. RFC 2822 richiede una riga vuota tra il campo di intestazione `Subject:` e il corpo del messaggio.

11. Digitare **Messaggio di prova** e quindi premere INVIO.

12. Premere INVIO, digitare un punto ( **.** ) e premere INVIO. Si riceverà una risposta simile alla seguente:
    
    ```powershell
    250 2.6.0 <GUID> Queued mail for delivery
    ```

13. Per disconnettersi dal server SMTP di destinazione, digitare **QUIT** e premere INVIO. Si riceverà una risposta simile alla seguente:
    
    ```powershell
    221 2.0.0 Service closing transmission channel
    ```

14. Per chiudere la sessione Telnet, digitare **quit** e premere INVIO.

## Passaggio 4: Valutazione dei risultati della sessione Telnet

In questa sezione vengono fornite informazioni sulle risposte che possono essere fornite ai seguenti comandi, utilizzati nell'esempio precedente:

  - Aprire mail1.fabrikam.com 25

  - EHLO contoso.com

  - MAIL FROM:chris@contoso.com

  - RCPT TO:kate@fabrikam.com NOTIFY=success,failure
    

    > [!NOTE]
    > I codici di risposta SMTP a tre cifre definiti in RFC 2821 sono gli stessi per tutti i server di messaggistica SMTP. Le descrizioni testuali potrebbero essere leggermente diverse per alcuni server di messaggistica SMTP.



## Aprire mail1.fabrikam.com 25

**Risposta positiva**   `220 mail1.fabrikam.com Microsoft ESMTP MAIL Service ready at <day-date-time>`

**Risposta di errore**   `Connecting to mail1.fabrikam.com...Could not open connection to the host, on port 25: Connect failed`

**Possibili motivi di errore**

  - Il server SMTP di destinazione non è disponibile.

  - Sono presenti restrizioni sul firewall di destinazione.

  - Sono presenti restrizioni sul firewall di origine.

  - È stato specificato un nome FQDN o un indirizzo IP non corretto per il server SMTP di destinazione.

  - È stato specificato un numero di porta non corretto.

## EHLO contoso.com

**Risposta positiva**   `250 mail1.fabrikam.com Hello [<sourceIPaddress>]`

**Risposta di errore**   `501 5.5.4 Invalid domain name`

**Possibili motivi di errore**   Sono presenti caratteri non validi nel nome di dominio. In alternativa, sono presenti restrizioni di connessione sul server SMTP di destinazione.


> [!NOTE]
> EHLO è il comando ESMTP definito in RFC 2821. I server ESMTP possono annunciare le funzionalità durante la connessione iniziale. Tali funzionalità includono la dimensione massima dei messaggi accettati e i metodi di autenticazione supportati. HELO indica il comando SMTP precedente definito in RFC 821. La maggior parte dei server di messaggistica SMTP supporta ESMTP ed EHLO.



## MAIL FROM:chris@contoso.com

**Risposta positiva**   `250 2.1.0 Sender OK`

**Risposta di errore**   `550 5.1.7 Invalid address`

**Possibili motivi di errore**   È presente un errore di sintassi nell'indirizzo di posta elettronica del mittente.

**Risposta di errore**   `530 5.7.1 Client was not authenticated`

**Possibili motivi di errore**   Il server di destinazione non accetta invii di messaggi anonimi. Viene visualizzato questo errore se si tenta di utilizzare Telnet per inviare un messaggio direttamente a un server Trasporto Hub.

## RCPT TO:kate@fabrikam.com NOTIFY=success,failure

**Risposta positiva**   `250 2.1.5 Recipient OK`

**Risposta di errore**   `550 5.1.1 User unknown`

**Possibili motivi di errore**   Il destinatario specificato non esiste nell'organizzazione.

