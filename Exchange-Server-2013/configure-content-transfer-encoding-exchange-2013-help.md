---
title: 'Configurare la codifica di trasferimento del contenuto: Exchange 2013 Help'
TOCTitle: Configurare la codifica di trasferimento del contenuto
ms:assetid: c4922362-18d4-42f7-9189-9076720eb1d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg144562(v=EXCHG.150)
ms:contentKeyID: 50481636
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la codifica di trasferimento del contenuto

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

La *codifica per il trasferimento del contenuto* definisce i metodi di codifica per trasformare i dati dei messaggi di posta elettronica binari nel formato di testo normale US-ASCII. Questa trasformazione consente al messaggio di passare attraverso i server di messaggistica SMTP precedenti che supportano solo messaggi in formato di testo US-ASCII. La codifica per il trasferimento del contenuto viene definita in RFC 2045. Il metodo di codifica è memorizzato nel campo di intestazione **Content-Transfer-Encoding** del messaggio. In Microsoft Exchange Server 2013 sono disponibili i metodi di codifica per il trasferimento del contenuto seguenti:

  - **7-bit**   Questo valore indica che i dati del corpo del messaggio sono già nel formato di testo normale US ASCII e non è stata applicata alcuna codifica al messaggio.

  - **Quoted-Printable (QP)**   Questo metodo di codifica utilizza caratteri US-ASCII stampabili per codificare i dati del corpo del messaggio. Se il testo del messaggio originale è principalmente in testo US-ASCII, la codifica QP garantisce risultati compatti e leggibili. Per impostazione predefinita, in Exchange 2013 viene utilizzato il metodo QP per la codifica dei dati binari dei messaggi.

  - **Base64**   Questo metodo di codifica si basa principalmente sullo standard PEM (Privacy-Enhanced Mail) definito in RFC 1421. La codifica Base64 utilizza il metodo di codifica con alfabeto a 64 caratteri e i caratteri di spaziatura interna di output definiti da PEM per codificare i dati del corpo del messaggio. La codifica Base64 crea un aumento prevedibile nelle dimensioni dei messaggi ed è ottimale per i dati binari e il testo diverso da US-ASCII.

Il metodo di codifica per il trasferimento del contenuto viene configurato utilizzando il parametro *ByteEncoderTypeFor7BitCharsets* nei cmdlet **Set-OrganizationConfig** e **Set-RemoteDomain**. Le impostazioni della codifica per il trasferimento del contenuto configurate con **Set-OrganizationConfig** si applicano a tutti i messaggi dell'organizzazione di Exchange. Le impostazioni della codifica per il trasferimento del contenuto configurate con **Set-RemoteDomain** si applicano solo ai messaggi inviati ai destinatari esterni nel dominio remoto.

Nella tabella seguente sono elencati i valori utilizzabili per impostare il metodo della codifica per il trasferimento.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro in <strong>Set-OrganizationConfig</strong></th>
<th>Parametro in <strong>Set-RemoteDomain</strong></th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p><code>Use7Bit</code></p></td>
<td><p>Utilizzare sempre la codifica 7-bit per HTML e testo normale. Questo è il valore predefinito.</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p><code>UseQP</code></p></td>
<td><p>Utilizzare sempre la codifica QP per HTML e testo normale.</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p><code>UseBase64</code></p></td>
<td><p>Utilizzare sempre la codifica Base64 per HTML e testo normale.</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p><code>UseQPHtmlDetectTextPlain</code></p></td>
<td><p>Utilizzare la codifica QP per HTML e testo normale, a meno che non sia abilitato il ritorno a capo nel testo normale. Se il ritorno a capo è abilitato, utilizzare la codifica a 7 bit per il testo normale.</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p><code>UseBase64HtmlDetectTextPlain</code></p></td>
<td><p>Utilizzare la codifica Base64 per HTML e testo normale, a meno che non sia abilitato il ritorno a capo nel testo normale. Se il ritorno a capo è abilitato nel testo normale, utilizzare la codifica Base64 per HTML e la codifica a 7 bit per il testo normale.</p></td>
</tr>
<tr class="even">
<td><p>13</p></td>
<td><p><code>UseQPHtml7BitTextPlain</code></p></td>
<td><p>Utilizzare sempre la codifica QP per HTML. Utilizzare sempre la codifica a 7 bit per il testo normale.</p></td>
</tr>
<tr class="odd">
<td><p>14</p></td>
<td><p><code>UseBase64Html7BitTextPlain</code></p></td>
<td><p>Utilizzare sempre la codifica Base64 per HTML. Utilizzare sempre la codifica a 7 bit per il testo normale.</p></td>
</tr>
</tbody>
</table>


Per informazioni dettagliate sul campo di intestazione **Content-Transfer-Encoding**, vedere la sezione "Concetti relativi alla struttura dei messaggi di posta elettronica" in [Conversione del contenuto](content-conversion-exchange-2013-help.md).

Per ulteriori informazioni sui domini remoti, vedere [Domini remoti](remote-domains-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Servizio di trasporto" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Configurazione del metodo di codifica per il trasferimento del contenuto per l'organizzazione tramite Shell

Per configurare il metodo di codifica per il trasferimento del contenuto, eseguire il comando seguente:

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets <Integer>

Ad esempio, per impostare il metodo di codifica per il trasferimento del contenuto su Base64, eseguire il comando riportato di seguito:

    Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets 2

## Configurazione del metodo di codifica per il trasferimento del contenuto per un dominio remoto tramite Shell

Per configurare il metodo di codifica per il trasferimento del contenuto per tutti i destinatari in un dominio remoto, eseguire il comando seguente:

    Set-RemoteDomain -ByteEncoderTypeFor7BitCharsets <Value>

Ad esempio, per impostare il metodo di codifica per il trasferimento del contenuto su Base64, eseguire il comando riportato di seguito:

    Set- RemoteDomain -ByteEncoderTypeFor7BitCharsets UseBase64

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver configurato correttamente la codifica per il trasferimento del contenuto, effettuare le operazioni seguenti:

1.  Inviare un messaggio di testo che contenga una combinazione di testo US-ASCII e dati binari oppure testo non US-ASCII a un account di prova interno o esterno. Utilizzare un account interno per verificare le impostazioni dell'organizzazione e uno esterno nel dominio remoto per verificare le impostazioni del dominio remoto.

2.  In un client di posta elettronica visualizzare il campo di intestazione **Content-Transfer-Encoding** nel messaggio e verificare che il metodo di codifica per il trasferimento del contenuto utilizzato per il messaggio corrisponda al metodo configurato.

