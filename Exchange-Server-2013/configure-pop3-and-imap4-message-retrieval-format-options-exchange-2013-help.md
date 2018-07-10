---
title: 'Configurare opzioni di formato per il recupero messaggi POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Configurare opzioni di formato per il recupero messaggi POP3 e IMAP4
ms:assetid: 481096e0-4492-46c2-8ca8-bdf84a84531e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997869(v=EXCHG.150)
ms:contentKeyID: 50555583
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare opzioni di formato per il recupero messaggi POP3 e IMAP4

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile configurare il recupero del formato dei messaggi per gli utenti che si collegano alla posta elettronica utilizzando POP3 e IMAP4. È possibile configurare le opzioni di recupero dei messaggi al livello di server tramite l'interfaccia di amministrazione di Exchange o Shell e, a livello di utente, tramite Shell.

Per ulteriori informazioni su POP3 e IMAP4, vedere [POP3 e IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Impostazioni POP3" e \&quot;Impostazioni IMAP4\&quot; nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Impostazione del formato di recupero messaggi POP3 al livello di server

## Impostazione del formato di recupero messaggi POP3 al livello di server tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **POP3**.

4.  Sotto **Formato MIME del messaggio**, scegliere tra le seguenti impostazioni:
    
      - Testo
    
      - HTML
    
      - HTML e testo alternativo
    
      - Enriched text
    
      - Enriched text e testo alternativo
    
      - Best body format
    
      - TNEF

5.  Fare clic su **Salva**.

Dopo avere impostato le impostazioni del formato di recupero dei messaggi per POP3, è necessario riavviare i servizi POP3 affinché le impostazioni abbiano effetto. Per informazioni su come riavviare i servizi POP3, vedere[Avviare e arrestare i servizi POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

## Impostazione del formato di recupero messaggi POP3 al livello di server tramite Shell

In questo esempio viene impostata l'opzione formato recupero messaggi solo di testo per tutti gli utenti POP3 sul server CAS01.

    Set-PopSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

È possibile scegliere una delle seguenti impostazioni. È possibile specificare il valore per il parametro *MessageRetrievalMimeFormat* utilizzando un valore numerico o una stringa di testo.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato del messaggio</strong></p></td>
<td><p><strong>Valore</strong></p></td>
</tr>
<tr class="even">
<td><p>Testo</p></td>
<td><p><code>0</code> oppure <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> oppure <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML e testo alternativo</p></td>
<td><p><code>2</code> oppure <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched text</p></td>
<td><p><code>3</code> oppure <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched text e testo alternativo</p></td>
<td><p><code>4</code> oppure <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best body format</p></td>
<td><p><code>5</code> oppure <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> oppure <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Dopo avere impostato le impostazioni del formato di recupero dei messaggi per POP3, è necessario riavviare i servizi POP3 affinché le impostazioni abbiano effetto. Per informazioni su come riavviare i servizi POP3, vedere[Avviare e arrestare i servizi POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-PopSettings](https://technet.microsoft.com/it-it/library/aa997154\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Effettuare le seguenti operazioni per verificare di aver impostato correttamente le impostazioni di recupero messaggi POP3 su un server.

1.  Eseguire il seguente comando in Shell.
    
        Get-PopSettings | format-list

2.  Verificare che l'impostazione *MessageRetrievalMimeFormat* sia corretta.

## Impostazione del formato di recupero messaggi IMAP4 al livello di server

## Impostazione del formato di recupero messaggi IMAP4 al livello di server tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Server** \> **Server**.

2.  Nell'elenco dei server, selezionare il server Accesso client, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del server, fare clic su **IMAP4**.

4.  Sotto **Formato MIME del messaggio**, scegliere tra le seguenti impostazioni:
    
      - Testo
    
      - HTML
    
      - HTML e testo alternativo
    
      - Enriched text
    
      - Enriched text e testo alternativo
    
      - Best body format
    
      - TNEF

5.  Fare clic su **Salva**.

Dopo avere impostato le impostazioni del formato di recupero dei messaggi per IMAP4, è necessario riavviare i servizi IMAP4 affinché le impostazioni abbiano effetto. Per informazioni su come riavviare i servizi IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

## Impostazione del formato di recupero messaggi IMAP4 al livello di server tramite Shell

In questo esempio viene impostata l'opzione formato recupero messaggi solo di testo per tutti gli utenti IMAP4 sul server CAS01.

    Set-ImapSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

È possibile scegliere una delle seguenti impostazioni. È possibile specificare il valore per il parametro *MessageRetrievalMimeFormat* utilizzando un valore numerico o una stringa di testo.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato del messaggio</strong></p></td>
<td><p><strong>Valore</strong></p></td>
</tr>
<tr class="even">
<td><p>Testo</p></td>
<td><p><code>0</code> oppure <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> oppure <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML e testo alternativo</p></td>
<td><p><code>2</code> oppure <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched text</p></td>
<td><p><code>3</code> oppure <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched text e testo alternativo</p></td>
<td><p><code>4</code> oppure <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best body format</p></td>
<td><p><code>5</code> oppure <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> oppure <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Dopo avere impostato le impostazioni del formato di recupero dei messaggi per IMAP4, è necessario riavviare i servizi IMAP4 affinché le impostazioni abbiano effetto. Per informazioni su come riavviare i servizi IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ImapSettings](https://technet.microsoft.com/it-it/library/aa998252\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Effettuare le seguenti operazioni per verificare di aver impostato correttamente le impostazioni di recupero messaggi IMAP4 su un server.

1.  Eseguire il seguente comando in Shell.
    
        Get-ImapSettings | format-list

2.  Verificare che l'impostazione *MessageRetrievalMimeFormat* sia corretta.

## Impostazione del formato di recupero messaggi POP3 per un utente

## Impostazione del formato di recupero di messaggi POP3 per un utente tramite Shell

In questo esempio viene impostato il formato di recupero dei messaggi solo di testo per l'accesso POP3 per `USER01`.

    Set-CASMailbox -Identity USER01 -PopMessagesRetrievalMimeFormat TextOnly

È possibile scegliere una delle seguenti impostazioni. È possibile specificare il valore per il parametro *PopMessagesRetrievalMimeFormat* utilizzando un valore numerico o una stringa di testo.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato del messaggio</strong></p></td>
<td><p><strong>Valore</strong></p></td>
</tr>
<tr class="even">
<td><p>Testo</p></td>
<td><p><code>0</code> oppure <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> oppure <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML e testo alternativo</p></td>
<td><p><code>2</code> oppure <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched text</p></td>
<td><p><code>3</code> oppure <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched text e testo alternativo</p></td>
<td><p><code>4</code> oppure <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best body format</p></td>
<td><p><code>5</code> oppure <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> oppure <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Dopo aver impostato le impostazioni del formato di recupero dei messaggi per POP3, è necessario riavviare i servizi POP3 affinché le impostazioni abbiano effetto. Per informazioni su come riavviare i servizi POP3, vedere[Avviare e arrestare i servizi POP3](start-and-stop-the-pop3-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Effettuare le seguenti operazioni per verificare di aver impostato correttamente le opzioni di formato recupero messaggi POP3 per un utente.

1.  Eseguire il seguente comando in Shell.
    
        Get-CAS Mailbox <identity> | format-list

2.  Verificare che il valore per *PopMessagesRetrievalMimeFormat* sia corretto.

## Impostazione del formato di recupero messaggi IMAP4 per un utente

## Impostazione del formato di recupero di messaggi IMAP4 per un utente tramite Shell

In questo esempio viene impostato il formato di recupero dei messaggi solo di testo per l'accesso IMAP4 per `USER01`.

    Set-CASMailbox -Identity USER01 -ImapMessagesRetrievalMimeFormat TextOnly

È possibile specificare il valore per il parametro *ImapMessagesRetrievalMimeFormat* utilizzando un valore numerico o una stringa di testo.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Formato del messaggio</strong></p></td>
<td><p><strong>Valore</strong></p></td>
</tr>
<tr class="even">
<td><p>Testo</p></td>
<td><p><code>0</code> oppure <code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> oppure <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML e testo alternativo</p></td>
<td><p><code>2</code> oppure <code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Enriched text</p></td>
<td><p><code>3</code> oppure <code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>Enriched text e testo alternativo</p></td>
<td><p><code>4</code> oppure <code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best body format</p></td>
<td><p><code>5</code> oppure <code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> oppure <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


Dopo aver impostato le impostazioni del formato di recupero dei messaggi per IMAP4, è necessario riavviare i servizi IMAP4 affinché le impostazioni abbiano effetto. Per informazioni su come riavviare i servizi IMAP4, vedere [Avviare e arrestare i servizi IMAP4](start-and-stop-the-imap4-services-exchange-2013-help.md).

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Effettuare le seguenti operazioni per verificare di aver impostato correttamente le opzioni di formato recupero messaggi IMAP4 per un utente.

1.  Eseguire il seguente comando in Shell.
    
        Get-CAS Mailbox <identity> | format-list

2.  Verificare che il valore per *ImapMessagesRetrievalMimeFormat* sia corretto.

## Ulteriori informazioni

Dopo aver impostato il formato di recupero dei messaggi per gli utenti IMAP4 e POP3, è possibile anche:

[Abilitare o disabilitare l'accesso POP3 per un utente](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[Abilitazione o disabilitazione dell'accesso IMAP4 per un utente](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

[Configurare le opzioni di calendario per IMAP4](configure-calendar-options-for-imap4-exchange-2013-help.md)

[Configurare le opzioni di calendario per POP3](configure-calendar-options-for-pop3-exchange-2013-help.md)

