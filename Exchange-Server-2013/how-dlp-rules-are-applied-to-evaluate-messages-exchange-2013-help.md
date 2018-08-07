---
title: 'Modalità applicazione regole DLP per valutazione messaggi: Exchange 2013 Help'
TOCTitle: Modalità di applicazione delle regole DLP per la valutazione dei messaggi
ms:assetid: 1ac77020-26ff-410c-ab09-4f28a99d67a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn329050(v=EXCHG.150)
ms:contentKeyID: 56269662
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modalità di applicazione delle regole DLP per la valutazione dei messaggi

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile impostare regole per i dati sensibili nei criteri di prevenzione della perdita di dati (DLP) di Microsoft Exchange per rilevare dati molto specifici nei messaggi di posta elettronica. In questo argomento viene illustrato il modo in cui vengono applicate le regole e valutati i messaggi. Se si comprende il modo in cui vengono applicate le regole è possibile evitare interruzioni del flusso di lavoro per gli utenti di posta elettronica e ottenere un elevato livello di accuratezza dei rilevamenti DLP. Ad esempio, si pensi a una regola relativa ai dati della carta di credito forniti da Microsoft. Quando si attiva una regola di trasporto o un criterio DLP, l'agente regole di trasporto di Exchange confronta tutti i messaggi inviati dagli utenti con i set di regole creati.

## Stabilire con precisione le proprie esigenze

Si supponga di dover intervenire sui dati delle carte di credito presenti nei messaggi. Questo argomento non copre le azioni eseguite su tali dati una volta individuati. Per saperne di più, vedere [Posta azioni delle regole del flusso di Exchange Online](https://technet.microsoft.com/it-it/library/jj919237\(v=exchg.150\)). Innanzitutto è necessario stabilire con la massima certezza possibile che le informazioni rilevate in un messaggio corrispondano effettivamente ai dati di una carta di credito e non a un gruppo di numeri simile, ad esempio un codice prenotazione o la targa di un veicolo. A tale scopo, è opportuno chiarire che le seguenti informazioni devono essere classificate come carta di credito.

**    Margie’s Travel,  
    Ho ricevuto i dati della carta di credito per Spencer.  
    Spencer Badillo  
    Visa: 4111 1111 1111 1111  
    Scadenza: 2/2012  
    Aggiornare il suo profilo di viaggio.**

Le seguenti informazioni, invece, non devono essere classificate come carta di credito.

**    Ciao Alex,  
    Anch'io dovrei essere alle Hawaii. Il mio codice prenotazione è 1234 1234 1234 1234. Arriverò a marzo.  
    Saluti, Lisa**

Il frammento XML seguente mostra come le esigenze espresse precedentemente siano definite in una regola per le informazioni sensibili fornita con Exchange e integrata in uno dei modelli di criteri DLP forniti.

    <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>

## Corrispondenza con il modello nella soluzione

La definizione di regola XML mostrata in precedenza include la corrispondenza con il modello, migliorando la probabilità che la regola rilevi solo le informazioni importanti e non altri dati confusi correlati. Per ulteriori informazioni sullo schema XML per i modelli e le regole DLP, vedere [Definire modelli DLP e tipi di informazione propri](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

Nella regola per le carte di credito è presente una sezione del codice XML per i modelli, che include la corrispondenza con un identificativo principale e alcuni ulteriori elementi avvaloranti. Di seguito vengono spiegati questi tre requisiti:

1.  `<IdMatch idRef="Func_credit_card" />  `: richiede una corrispondenza di una funzione, carta di credito intestata, che sia definita internamente. Questa funzione include una coppia di convalide:
    
    1.  Corrisponde a un'espressione regolare (in questa istanza per 16 cifre) che potrebbe includere anche varianti come, ad esempio un delimitatore spazio o trattino, in modo che vengano considerate valide anche le corrispondenze **4111 1111 1111 1111** e **4111-1111-1111-1111**.
    
    2.  Valuta l'algoritmo di checksum di Lhun rispetto al numero di 16 cifre per garantire che la probabilità che si tratti di un numero di carta di credito sia alta.
    
    3.  Richiede una corrispondenza obbligatoria, dopodiché viene valutato l'elemento avvalorante.

2.  `<Any minMatches="1">  `: in questa sezione viene indicata che la presenza di almeno uno dei seguenti elementi di prova è necessaria.

3.  L'elemento avvalorante può essere una corrispondenza di uno dei seguenti:
    
    `<Match idRef="Keyword_cc_verification" />`
    
    `<Match idRef="Keyword_cc_name" />`
    
    `<Match idRef="Func_expiration_date" />`
    
    Tali elementi indicano semplicemente un elenco di parole chiave per carte di credito, i nomi delle carte di credito o che è necessaria una data di scadenza. La data di scadenza viene definita e valutata internamente come altra funzione.

## Il processo di valutazione del contenuto rispetto alle regole

I cinque passaggi delineati rappresentano le azioni eseguite da Exchange per confrontare la regola con i messaggi di posta elettronica. Per l'esempio di regola per le carte di credito, vengono compiuti i seguenti passaggi.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Passaggio</th>
<th>Azione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1. Get Content</p></td>
<td><p>Spencer Badillo</p>
<p>Visa: 4111 1111 1111 1111</p>
<p>Scadenza: 2/2012</p></td>
</tr>
<tr class="even">
<td><p>2. Analisi dell'espressione regolare</p></td>
<td><p>4111 1111 1111 1111 -&gt; è stato rilevato un numero a 16 cifre</p></td>
</tr>
<tr class="odd">
<td><p>3. Analisi funzione</p></td>
<td><ul>
<li><p>4111 1111 1111 1111 -&gt; checksum di corrispondenze</p></li>
<li><p>1234 1234 1234 1234 -&gt; non corrisponde</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>4. Prova aggiuntiva</p></td>
<td><ol>
<li><p>La parola chiave Visa si trova vicino il numero.</p></li>
<li><p>Un'espressione regolare per una data (2/2012) si trova vicino il numero.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>5. Verdetto</p></td>
<td><ol>
<li><p>È presente un'espressione regolare corrispondente a un checksum</p></li>
<li><p>Ulteriori prove aumentano la confidenza.</p></li>
</ol>
<p></p></td>
</tr>
</tbody>
</table>


Il modo in cui questa regola è impostata da Microsoft impone che perché una corrispondenza alla regola sia valida l'elemento avvalorante, ad esempio le parole chiave, sia parte del contenuto del messaggio di posta elettronica. In tal modo nel contenuto del seguente messaggio non sarebbe individuato un numero di carta di credito:

**    Margie’s Travel,  
    Ho ricevuto le informazioni aggiornate per Spencer.  
    Spencer Badillo  
    4111 1111 1111 1111  
    Aggiornare il suo profilo di viaggio.**

È possibile utilizzare una regola personalizzata che definisca un modello senza prove aggiuntive, come indicato nell'esempio successivo. In questo caso verrebbero rilevati solo i messaggi con numeri di carta di credito e senza prove avvaloranti.

``` 
      <Pattern confidenceLevel="85">
         <IdMatch idRef="Func_credit_card" />
      </Pattern>
    </Entity>
```

L'esempio delle carte di credito illustrato in questo articolo può essere esteso ad altre informazioni sensibili. Per un elenco completo delle regole fornite da Microsoft in Exchange, utilizzare il cmdlet [Get-ClassificationRuleCollection](https://technet.microsoft.com/it-it/library/jj218696\(v=exchg.150\)) in Exchange Management Shell nel modo seguente:
```
$rule_collection = Get-ClassificationRuleCollection
```
```
$rule_collection[0].SerializedClassificationRuleCollection | Set-Content oob_classifications.xml -Encoding byte
```

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Regole del flusso (regole di trasporto) di posta in Exchange Online](https://technet.microsoft.com/it-it/library/jj919238\(v=exchg.150\))

[Utilizzo di PowerShell con Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/it-it/library/bb123778\(v=exchg.150\))

[Exchange Online PowerShell](https://technet.microsoft.com/it-it/library/jj200677\(v=exchg.150\))

