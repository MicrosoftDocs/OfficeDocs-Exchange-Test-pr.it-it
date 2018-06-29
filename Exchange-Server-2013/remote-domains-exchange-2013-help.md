---
title: 'Domini remoti: Exchange 2013 Help'
TOCTitle: Domini remoti
ms:assetid: 10fb7d62-4d78-40a3-82db-d62bcd27ba42
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996309(v=EXCHG.150)
ms:contentKeyID: 50480068
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Domini remoti

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2015-04-07_

È possibile creare le voci di dominio remoto per definire le impostazioni per il trasferimento dei messaggi tra l'organizzazione di Microsoft Exchange Server 2013 e i domini esterni all'organizzazione Exchange. Quando si crea una voce del dominio remoto, controllare i tipi di messaggi inviati a tale dominio. È inoltre possibile applicare criteri di formato di messaggio e set di caratteri accettabile per i messaggi inviati dagli utenti all'interno dell'organizzazione al dominio remoto. Le impostazioni per i domini remoti sono le impostazioni di configurazione globali per l'organizzazione Exchange.

Impostazioni del dominio remoto vengono applicate ai messaggi durante la classificazione nel servizio di trasporto sui server cassette postali. Quando si verifica la risoluzione dei destinatari, il dominio del destinatario viene confrontato con i domini remoti configurati. Se una configurazione del dominio remoto blocca un tipo di messaggio specifico vengano inviate a destinatari compresi nel dominio, il messaggio verrà eliminato. Se si specifica un particolare formato di messaggio per il dominio remoto, vengono modificate le intestazioni dei messaggi e del contenuto. Le impostazioni si applicano a tutti i messaggi che vengono elaborati dall'organizzazione Exchange.


> [!NOTE]
> Se si configurano le impostazioni dei messaggi per utente, le impostazioni per utente per ignorare la configurazione dell'organizzazione.



Per impostazione predefinita, non esiste una voce del dominio remoto. Lo spazio degli indirizzi di dominio viene configurato come un asterisco (\*). Ciò rappresenta tutti i domini remoti. Se non si crea le voci di dominio remoto aggiuntive, tutti i messaggi inviati a tutti i destinatari in tutti i domini remoti sono le stesse impostazioni applicate alle stesse.

Quando si configurano i domini remoti, è possibile impedire determinati tipi di messaggi vengano inviate a tale dominio. Questi tipi di messaggio sono messaggi fuori sede, messaggi di risposta automatica, rapporti di mancato recapito (NDR) e notifiche di inoltro riunione. Se si dispone di un ambiente a più foreste, è possibile consentire l'invio di tali tipi di messaggi per i domini. Tuttavia, se è stato identificato un dominio da quale posta indesiderata proviene, è possibile bloccare l'invio di tali tipi di messaggi per i domini remoti.

**Sommario**

Formato del messaggio

Impostazioni delle risposte automatiche

Controllo delle informazioni di rapporto di mancato recapito

## Formato del messaggio

È possibile specificare il formato del messaggio e il set di caratteri da utilizzare per i messaggi di posta elettronica inviati a domini remoti. Queste impostazioni possono essere utili per verificare che sia compatibile con il sistema di posta elettronica destinatario posta elettronica inviato da mittenti nel dominio al dominio remoto. Se, ad esempio, la presenza di sistema di messaggistica del dominio remoto Exchange, è possibile specificare per utilizzare sempre Exchange RTF RICH text format (). Per ulteriori informazioni, vedere [Conversione del contenuto](content-conversion-exchange-2013-help.md).

## Impostazioni delle risposte automatiche

In Exchange 2013, gli utenti possono specificare diverse risposte automatiche per i destinatari interni ed esterni. Inoltre, i tipi di risposte automatiche disponibili nell'organizzazione dipendono inoltre dalla versione Outlook Microsoft in uso.

In Exchange 2013, esistono due tipi di risposte automatiche:

  - **Esterno**   Supportato da Exchange 2013 e Exchange 2010. Possono essere impostati solo da Outlook 2010 o Office Outlook 2007 o utilizzando Microsoft OfficeOutlook Web App.

  - **Interno**   Supportato da Exchange 2013 e Exchange 2010. Possono essere impostati solo da Outlook 2010 o Outlook 2007 o utilizzando Outlook Web App.

Nella tabella seguente vengono descritte le varie combinazioni di client e server e i tipi di risposte automatiche che possono essere utilizzati in ogni scenario.

**Supporto di client e server per le risposte automatiche**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Versione del client</th>
<th>Versione di Exchange</th>
<th>Risposte automatiche supportate</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2010 o Outlook 2007</p></td>
<td><p>Exchange 2013 Exchange 2010 Exchange 2007</p></td>
<td><p>Interni, esterni</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013 Exchange 2010 Exchange 2007</p></td>
<td><p>Interni, esterni</p></td>
</tr>
</tbody>
</table>


## Controllo delle informazioni di rapporto di mancato recapito

Come accennato all'inizio di questo argomento, è possibile impedire rapporti di mancato recapito non verrà inviato a un dominio remoto. Per bloccare i rapporti di mancato recapito non verrà inviato a un dominio remoto, è possibile impedire le informazioni contenute nel rapporto di mancato recapito escano dalla tua organizzazione, limitando così la certezza che un utente malintenzionato può ottenere sull'organizzazione. Tuttavia, si impedisce inoltre mittenti legittimi ricevere rapporti di mancato recapito, causando confusione e la perdita di produttività.

Exchange 2013 viene fornita con controllo granulare sul contenuto di un rapporto di mancato recapito destinate a un dominio remoto. Con Exchange 2013, è possibile consentire a un dominio remoto, rapporti di mancato recapito durante la rimozione di tutte le informazioni di diagnostiche. In questo modo, è comunque possibile impedire le informazioni sulla distribuzione Exchange escano dalla tua organizzazione mentre contemporaneamente fornendo le notifiche di rapporto di mancato recapito per i mittenti esterni.

Questa funzionalità è controllata con il parametro *NDRDiagnosticInfoEnabled* nel cmdlet **Set-RemoteDomain** . Poiché questa impostazione è configurabile per ogni dominio remoto, è possibile applicare diverse impostazioni in base alle esigenze. Ad esempio, è possibile scegliere di rimuovere le informazioni di diagnostica del rapporto di mancato recapito per il dominio remoto predefinito, ma Consenti complete informazioni di diagnostica rapporto di mancato recapito per i domini remoti che rappresentano i partner.

Per ulteriori informazioni su questa nuova impostazione, vedere [Set-RemoteDomain](https://technet.microsoft.com/it-it/library/aa997857\(v=exchg.150\)).

