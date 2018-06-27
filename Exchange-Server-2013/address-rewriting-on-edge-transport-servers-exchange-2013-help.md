---
title: 'Indirizzo riscrittura su server Trasporto Edge: Exchange 2013 Help'
TOCTitle: Indirizzo riscrittura su server Trasporto Edge
ms:assetid: 23f1eaf6-247a-4671-ad72-aae19d9b511d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996806(v=EXCHG.150)
ms:contentKeyID: 61060525
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Indirizzo riscrittura su server Trasporto Edge

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-03-09_

La riscrittura degli indirizzi modifica gli indirizzi di posta elettronica di mittenti e destinatari nei messaggi che entrano o escono dall'organizzazione attraverso i server Trasporto Edge. Due agenti di trasporto nel server Trasporto Edge offrono la funzionalità di riscrittura: l'agente di riscrittura degli indirizzi dei messaggi in ingresso e l'agente di riscrittura degli indirizzi dei messaggi in uscita. Il motivo principale della riscrittura degli indirizzi nei messaggi in uscita è quello di presentare un unico e uniforme dominio di posta elettronica ai destinatari esterni. Il motivo principale della riscrittura degli indirizzi nei messaggi in entrata è quello di recapitare i messaggi al destinatario corretto.

La *voce di riscrittura degli indirizzi*, creata dall'utente, specifica gli indirizzi interni (gli indirizzi di posta elettronica da modificare) e gli indirizzi esterni (gli indirizzi di posta elettronica finali desiderati). È possibile specificare se gli indirizzi di posta elettronica devono essere riscritti nei messaggi in entrata e in uscita o solo nei messaggi in uscita. È possibile creare voci di scrittura degli indirizzi per un solo utente (da chris@contoso.com a support@contoso.com), per tutti gli utenti in un solo dominio (da contoso.com a fabrikam.com) o per gli utenti in più sottodomini con eccezioni (da \*.fabrikam.com a contoso.com, ad eccezione di legal.fabrikam.com).


> [!IMPORTANT]
> Indipendentemente da come si pianifica di utilizzare la riscrittura degli indirizzi, è necessario verificare che gli indirizzi di posta elettronica risultanti siano univoci nell'organizzazione per non creare duplicati. Infatti, la riscrittura degli indirizzi non consente di verificare l'univocità di un indirizzo di posta elettronica riscritto.



**Sommario**

Address rewriting scenarios

Message properties modified by address rewriting

What address rewriting doesn't change

Considerations for outbound-only address rewriting

Considerations for inbound and outbound address rewriting

Considerations for rewriting addresses in multiple domains

Priority of address rewrite entries

Digitally signed, encrypted, and rights-protected messages

## Scenari per la riscrittura degli indirizzi

Gli scenari seguenti sono esempi di come è possibile utilizzare la riscrittura degli indirizzi:

  - **Consolidamento del gruppo**   Alcune organizzazioni segmentano le proprie aziende interne in domini separati basati su requisiti tecnici o aziendali. In una configurazione simile, è possibile che i messaggi di posta elettronica siano visualizzati come provenienti da gruppi separati o persino da organizzazioni separate.
    
    Nel seguente esempio viene descritto come un'organizzazione, Contoso, Ltd., può nascondere i propri sottodomini interni ai destinatari esterni:
    
      - I messaggi in uscita dai domini northamerica.contoso.com, europe.contoso.com e asia.contoso.com vengono riscritti per essere visualizzati come tutti provenienti da un singolo dominio contoso.com. Tutti i messaggi vengono riscritti nel transito tramite i server Trasporto Edge che forniscono la connettività SMTP tra l'intera organizzazione e Internet.
    
      - I messaggi in arrivo ai destinatari di contoso.com vengono inoltrati dal server Trasporto Edge al server Cassette postali. Il messaggio viene recapitato al destinatario corretto in base all'indirizzo proxy configurato nella cassetta postale del destinatario.

  - **Fusioni e acquisizioni**   È possibile continuare a gestire un'azienda acquisita come unità aziendale separata, ma l'amministratore di posta elettronica può utilizzare la riscrittura degli indirizzi per consentire la visualizzazione delle due organizzazioni come una singola organizzazione integrata.
    
    Nell'esempio seguente viene descritto come Contoso, Ltd. può nascondere il dominio di posta elettronica della società appena acquisita, Fourth Coffee:
    
      - Contoso, Ltd. desidera che tutti i messaggi in uscita dall'organizzazione di Fourth Coffee vengano visualizzati come provenienti da contoso.com. Tutti i messaggi provenienti da entrambe le organizzazioni vengono inviati tramite i server Trasporto Edge a Contoso, Ltd., dove vengono riscritti da *utente*@fourthcoffee.com a *utente*@contoso.com.
    
      - I messaggi in entrata a *utente*@contoso.com vengono riscritti e indirizzati alle cassette postali di *utente*@fourthcoffee.com. I messaggi in entrata inviati a *user*@fourthcoffee.com vengono indirizzati direttamente ai server di posta elettronica di Fourth Coffee.

  - **Partner**   Molte organizzazioni utilizzano partner esterni per fornire servizi per i propri clienti, per altre organizzazioni o per l'organizzazione stessa. Per evitare confusione, l'organizzazione potrebbe sostituire il dominio di posta elettronica dell'organizzazione partner con il proprio dominio di posta.
    
    Nel seguente esempio viene descritto come Contoso, Ltd. può nascondere un dominio di posta elettronica di un partner:
    
      - Contoso, Ltd. fornisce supporto per l'organizzazione Wingtip Toys di grandi dimensioni. Wingtip Toys desidera offrire un'esperienza di posta elettronica uniforme ai propri clienti e richiede che tutti i messaggi provenienti dal personale di supporto presso Contoso, Ltd. vengano visualizzati come provenienti da Wingtip Toys. Tutti i messaggi in uscita relativi a Wingtip Toys vengono inviati tramite i server Trasporto Edge, quindi tutti gli indirizzi contoso.com vengono riscritti per essere visualizzati come indirizzi wingtiptoys.com.
    
      - I messaggi in ingresso per support@wingtiptoys.com vengono accettati dai server Trasporto Edge di Wingtip Toy, riscritti, quindi instradati all'indirizzo di posta elettronica support@contoso.com.

Inizio pagina

## Proprietà del messaggio modificato dalla riscrittura degli indirizzi

Un messaggio di posta elettronica SMTP standard è costituito da una *busta del messaggio* e dal contenuto del messaggio. La busta del messaggio contiene le informazioni necessarie per la trasmissione e il recapito del messaggio tra i server di posta elettronica SMTP. Il contenuto del messaggio include i campi di intestazione del messaggio (denominati collettivamente *intestazione del messaggio*) e il corpo del messaggio. La busta del messaggio è descritta in RFC 2821, mentre l'intestazione del messaggio è descritta in RFC 2822.

Quando il mittente crea un messaggio di posta elettronica e lo invia per il recapito, il messaggio contiene le informazioni di base necessarie per la conformità agli standard SMTP, quali mittente, destinatario, data e ora di creazione del messaggio, campo oggetto facoltativo e corpo del messaggio facoltativo. Queste informazioni sono contenute nel messaggio stesso e, per definizione, nell'intestazione del messaggio.

Il server di posta del mittente genera una busta per il messaggio utilizzando le informazioni su mittente e destinatario presenti nell'intestazione del messaggio. Trasmette poi il messaggio a Internet per il recapito al server di posta del destinatario. I destinatari non vedono mai la busta del messaggio, perché viene generata dal processo di trasmissione del messaggio e non è parte integrante di questo.

La riscrittura degli indirizzi cambia un indirizzo di posta elettronica riscrivendo i campi specifici nell'intestazione del messaggio o nella busta del messaggio. La riscrittura degli indirizzi modifica diversi campi nei messaggi in uscita ma solo un campo nei messaggi di posta elettronica in ingresso. Nella tabella seguente vengono mostrati i campi di intestazione SMTP riscritti nei messaggi in ingresso e in uscita.

### Campi del messaggio riscritti nei messaggi in ingresso e in uscita

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del campo</th>
<th>Percorso</th>
<th>Messaggi in uscita</th>
<th>Messaggi in ingresso</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MAIL FROM</strong></p></td>
<td><p>Busta del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
<tr class="even">
<td><p><strong>RCPT TO</strong></p></td>
<td><p>Busta del messaggio</p></td>
<td><p>Non riscritto</p></td>
<td><p>Riscritto</p></td>
</tr>
<tr class="odd">
<td><p><strong>A</strong></p></td>
<td><p>Intestazione del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
<tr class="even">
<td><p><strong>Cc</strong></p></td>
<td><p>Intestazione del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
<tr class="odd">
<td><p><strong>Da</strong></p></td>
<td><p>Intestazione del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
<tr class="even">
<td><p><strong>Mittente</strong></p></td>
<td><p>Intestazione del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reply-To</strong></p></td>
<td><p>Intestazione del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
<tr class="even">
<td><p><strong>Body Return-Receipt-To</strong></p></td>
<td><p>Intestazione del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
<tr class="odd">
<td><p><strong>Body Disposition-Notification-To</strong></p></td>
<td><p>Intestazione del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
<tr class="even">
<td><p><strong>Resent-From</strong></p></td>
<td><p>Intestazione del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
<tr class="odd">
<td><p><strong>Resent-Sender</strong></p></td>
<td><p>Intestazione del messaggio</p></td>
<td><p>Riscritto</p></td>
<td><p>Non riscritto</p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Cosa non modifica la riscrittura degli indirizzi

La riscrittura degli indirizzi non modifica i campi dell'intestazione del messaggio che interromperebbero la funzionalità SMTP. Ad esempio, la modifica di alcuni campi dell'intestazione potrebbe incidere sul rilevamento di loop di routing, determinare l'invalidazione della firma o rendere illeggibile un messaggio protetto da diritti. Pertanto, i seguenti campi dell'intestazione non vengono modificati dalla riscrittura degli indirizzi.

  - **Return-Path**

  - **Received**

  - **Message-ID**

  - **X-MS-TNEF-Correlator**

  - **Content-Type Boundary=string**

  - Campi dell'intestazione all'interno delle parti del corpo MIME

La riscrittura degli indirizzi ignora i domini che non sono controllati dall'organizzazione di Exchange. In altre parole, la riscrittura degli indirizzi non riscrive i campi dell'intestazione che contengono domini per i quali l'organizzazione di Exchange non è autorevole. La riscrittura di tali domini può provocare una forma non controllabile di inoltro del messaggio.

Inoltre, la riscrittura degli indirizzi non modifica i campi di intestazione dei messaggi incorporati in altri messaggi. I mittenti e i destinatari si aspettano che i messaggi incorporati rimangano intatti e vengano recapitati senza modifiche, fino a quando nei messaggi non vengono attivate le regole di trasporto implementate tra il mittente e il destinatario.

Inizio pagina

## Considerazioni per la riscrittura degli indirizzi solo in uscita

La riscrittura degli indirizzi solo in uscita in un server Trasporto Edge modifica l'indirizzo di posta elettronica del mittente non appena il messaggio esce dall'organizzazione di Exchange. È possibile configurare la riscrittura degli indirizzi solo in uscita per un solo utente (da chris@contoso.com a support@contoso.com) o per tutti gli utenti in un solo dominio (da contoso.com a fabrikam.com). È necessario configurare la riscrittura degli indirizzi solo in uscita per gli utenti in più sottodomini (da \*.fabrikam.com a .contoso.com).

L'indirizzo di poste elettronica riscritto deve essere configurato come indirizzo proxy nei destinatari interessati. Ad esempio, se laura@sales.contoso.com viene riscritto in laura@contoso.com, l'indirizzo proxy laura@contoso.com deve essere configurato nella cassetta postale di Laura. In questo modo le risposte e i messaggi in arrivo vengono recapitati correttamente.

Inizio pagina

## Considerazioni per la riscrittura degli indirizzi in ingresso e in uscita

La riscrittura degli indirizzi in ingresso e in uscita o *bidirezionale* in un server Trasporto Edge modifica l'indirizzo di posta elettronica del mittente nei messaggi che entrano nell'organizzazione di Exchange.

È possibile configurare la riscrittura degli indirizzi solo in uscita per un solo utente (da chris@contoso.com a support@contoso.com) e per tutti gli utenti in un solo dominio (da contoso.com a fabrikam.com). È possibile configurare la riscrittura degli indirizzi bidirezionale per gli utenti in più sottodomini (da \*. fabrikam.com a contoso.com).

Inizio pagina

## Considerazioni per la riscrittura degli indirizzi di posta elettronica in più domini

Quando i domini o sottodomini interni vengono semplificati in un unico dominio esterno, è necessario considerare i seguenti fattori:

  - **Verificare gli alias univoci**   Tutti gli alias di posta elettronica (la parte a sinistra del segno @) devono essere univoci in tutti i sottodomini. Ad esempio, se è presente un joe@sales.contoso.com, non può esserci joe@marketing.contoso.com perché l'indirizzo di posta elettronica riscritto per entrambi gli utenti sarebbe joe@contoso.com.

  - **Aggiungere indirizzi proxy**   L'indirizzo di posta elettronica riscritto deve essere configurato come indirizzo proxy per tutti i mittenti interessati nei domini interessati. Ad esempio, se joe@sales.contoso.com viene riscritto come joe@contoso.com, è necessario aggiungere l'indirizzo proxy joe@contoso.com alla cassetta postale di Joe. In questo modo le risposte e i messaggi in arrivo vengono recapitati correttamente.

  - **Contatti di posta per organizzazioni non di Exchange**   Se si stanno riscrivendo gli indirizzi di organizzazioni di un sistema di posta non Exchange, è necessario creare contatti di posta elettronica in Exchange che rappresentino gli utenti nel sistema di posta non di Exchange. I contatti di posta elettronica devono contenere gli indirizzi di posta elettronica originali e gli indirizzi di posta elettronica riscritti. Ad esempio, se joe@unix.contoso.com viene riscritto come joe@contoso.com, è necessario creare un contatto di posta con joe@unix.contoso.com come indirizzo di posta elettronica esterno e joe@contoso.com come indirizzo proxy.

## Verificare gli alias univoci

Quando si riscrivono indirizzi di posta elettronica in più sottodomini, è necessario assicurarsi che tutti gli alias di posta elettronica siano univoci in tutti i sottodomini. Ad esempio, si consideri la seguente configurazione:

Gli utenti riportati di seguito appartengono ai sottodomini sales.contoso.com, marketing.contoso.com e research.contoso.com:

  - maria@sales.contoso.com

  - chris@sales.contoso.com

  - david@marketing.contoso.com

  - brian@marketing.contoso.com

  - chris@research.contoso.com

  - adam@research.contoso.com

Si supponga che si desideri riscrivere i sottodomini sales.contoso.com, marketing.contoso.com e research.contoso.com in un unico dominio contoso.com.

Quando gli indirizzi di posta elettronica in ogni sottodominio vengono riscritti, si verifica un conflitto tra chris@sales.contoso.com e chris@research.contoso.com perché entrambi gli indirizzi di posta elettronica vengono riscritti come chris@contoso.com. Per risolvere il problema, è necessario modificare l'indirizzo di posta elettronica di uno dei destinatari interessati. Ad esempio, è possibile modificare chris@research.contoso.com in christopher@research.contoso.com così che l'indirizzo di posta elettronica venga riscritto come christopher@contoso.com.

Inizio pagina

## Priorità delle voci di riscrittura degli indirizzi

Se l'indirizzo di posta elettronica di un utente corrisponde a più voci di riscrittura degli indirizzi, l'indirizzo di posta elettronica viene riscritto solo una volta in base alla corrispondenza più simile. Il seguente elenco descrive l'ordine di priorità delle voci di riscrittura degli indirizzi dalla priorità più elevata alla priorità più bassa:

1.  **Indirizzi di posta elettronica singoli**   Una voce di riscrittura degli indirizzi è configurata per riscrivere l'indirizzo di posta elettronica da john@contoso.com a support@contoso.com.

2.  **Mapping di un dominio o di un sottodominio**   Una voce di riscrittura degli indirizzi è configurata per riscrivere tutti gli indirizzi di posta elettronica contoso.com come northwindtraders.com o tutti gli indirizzi sales.contoso.com come contoso.com.

3.  **Semplificazione del dominio**   Una voce di riscrittura degli indirizzi è configurata per riscrivere gli indirizzi di posta elettronica \*.contoso.com come contoso.com.

Ad esempio, si consideri un server Trasporto Edge dove le seguenti voci di riscrittura degli indirizzi in uscita sono configurate:

  - gli indirizzi di posta elettronica \*.contoso.com vengono riscritti come contoso.com

  - gli indirizzi di posta elettronica japan.sales.contoso.com vengono riscritti come contoso.jp

Se masato@japan.sales.contoso.com invia un messaggio di posta elettronica, l'indirizzo viene riscritto come masato@contoso.jp, perché la voce corrisponde di più all'indirizzo di posta elettronica del mittente.

Inizio pagina

## Messaggi con firma digitale, crittografati e protetti da diritti

La riscrittura degli indirizzi non dovrebbe interessare la maggior parte dei messaggi firmati, crittografati o protetti da diritti. Se la riscrittura degli indirizzi dovesse invalidare o in altro modo modificare lo stato di sicurezza di questi tipi di messaggi, la riscrittura degli indirizzi non viene applicata.

I seguenti valori possono essere riscritti perché le informazioni non fanno parte della firma, della crittografia o della protezione dei diritti del messaggio:

  - Campi nella busta del messaggio

  - Intestazioni principali del corpo del messaggio

I seguenti valori non possono essere riscritti perché le informazioni non fanno parte della firma, della crittografia o della protezione dei diritti del messaggio:

  - Campi dell'intestazione che si trovano all'interno delle parti del corpo MIME che possono essere firmate

  - Il parametro della stringa limite del tipo di contenuto MIME

Inizio pagina

