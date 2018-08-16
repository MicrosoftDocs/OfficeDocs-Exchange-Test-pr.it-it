---
title: 'Metodi/tecniche per pacchetti di regole corrispondenti: Exchange 2013 Help'
TOCTitle: Metodi e le tecniche per pacchetti di regole corrispondenti
ms:assetid: 09fe9278-d077-452c-b7e5-729b3dc70b1b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ674702(v=EXCHG.150)
ms:contentKeyID: 50479971
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Metodi e le tecniche per pacchetti di regole corrispondenti

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-07-28_

In questo argomento vengono descritte le tecniche per associare criteri e elementi in evidenza per la prevenzione della perdita di dati in un file XML progettato per contenere un pacchetto personalizzato di regole per i tipi di informazioni sensibili. Dopo aver formattato il file XML, è possibile importare il file utilizzando l'interfaccia di amministrazione di Exchange o Exchange Management Shell come aiuto nella creazione della propria soluzione DLP di Microsoft Exchange Server 2013. Prima di poter utilizzare uno dei metodi di corrispondenza descritti, è necessario avere già avviato un file XML DLP. Per ulteriori informazioni relative alla definizione dei propri modelli DLP e file XML, vedere [Definire modelli DLP e tipi di informazione propri](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

## L'elemento Match

L'elemento `Match` è utilizzato negli elementi `Pattern` e `Evidence` per rappresentare la parola chiave sottostante, regex o funzione che deve essere confrontata. La definizione dell'elemento match è archiviata all'esterno dell'elemento `Rule` e vi si fa riferimento tramite il necessario attributo `idRef`. Più elementi `Match` possono essere inclusi in una definizione Pattern che può essere inclusa direttamente nell'elemento `Pattern` o combinata utilizzando l'elemento `Any` per definire la semantica di corrispondenza.

    <?xml version="1.0" encoding="utf-8"?>
    <Rules packageId="...">
            ...
    <Entity id="...">
      <Pattern confidenceLevel="85">
                 <IdMatch idRef="FormattedSSN" />
                 <Match idRef="USDate" />
                 <Match idRef="USAddress" />
      </Pattern>
    </Entity>
            ...
             <Keyword id="FormattedSSN "> ... </Keyword>
             <Regex id=" USDate "> ... </Regex>
             <Regex id="USAddress"> ... </Regex>
            ...
    
    </Rules>

## Definizione di corrispondenza basata su parola chiave

Un comune requisito di una regola è la corrispondenza basata sul riconoscimento di espressioni stringa parola chiave. Questa operazione viene eseguita utilizzando l'elemento `Keyword`. L'elemento Keyword dispone di un attributo "id" che viene utilizzato come riferimento nelle corrispondenti regole di entità o affinità. Ad un singolo elemento Keyword possono far riferimento più regole dell'entità e dell'affinità.

L'abbinamento può essere eseguita utilizzando una corrispondenza esatta o gli algoritmi di corrispondenza di base di word. Corrispondenza esatta viene utilizzato un algoritmo tra maiuscole e minuscole che esegue una ricerca per il testo nella lingua specificata. Corrispondenza di una parola si applica un algoritmo di corrispondenza in base ai limiti di word. I termini da far corrispondere possono essere incluso inline nella definizione della parola chiave utilizzando l'elemento secondaria termini.


> [!TIP]
> Utilizzare lo stile di corrispondenza basato su costanti piuttosto che su regex per migliori livelli di prestazioni ed efficienza. Utilizzare la corrispondenza regex solo nei casi in cui le corrispondenze basate su costanti non sono sufficienti ed è necessaria la flessibilità garantita dalle espressioni regolari.



    <Keyword id="Word_Example">
        <Group matchStyle="word">
           <Term>card verification</Term>
           <Term>cvn</Term>
           <Term>cid</Term>
           <Term>cvc2</Term>
           <Term>cvv2</Term>
           <Term>pin block</Term>
           <Term>security code</Term>
        </Group>
    </Keyword>
    ...
    <Keyword id="String_Example">
        <Group matchStyle="string">
           <Term>card</Term>
           <Term>pin</Term>
           <Term>security</Term>
        </Group>
    </Keyword>

## Definizione di corrispondenze basate su espressioni regolare

Un altro metodo comune di corrispondenza si basa su espressioni regolari. La flessibilità della corrispondenza di espressioni regolari la rende una scelta comune nella realizzazione di corrispondenze di dati ad esempio numero della patente di guida, indirizzi. La comune sintassi delle espressioni regolari viene utilizzata per definire i modelli regex. Questa tabella mostra esempi di alcune delle più comuni espressioni regolari disponibili.


> [!TIP]
> Utilizzare lo stile di corrispondenza basato su costanti piuttosto che su regex per migliori livelli di prestazioni ed efficienza. Utilizzare la corrispondenza regex solo nei casi in cui le corrispondenze basate su costanti non sono sufficienti ed è necessaria la flessibilità garantita dalle espressioni regolari.




<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Simbolo</th>
<th>Significato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>c</p></td>
<td><p>Controlla la corrispondenza letterale del carattere c una sola volta, tranne quando è un carattere speciale.</p></td>
</tr>
<tr class="even">
<td><p>^</p></td>
<td><p>Controlla la corrispondenza all'inizio di una riga.</p></td>
</tr>
<tr class="odd">
<td><p>.</p></td>
<td><p>Controlla la corrispondenza con qualsiasi carattere che non è una nuova linea.</p></td>
</tr>
<tr class="even">
<td><p>$</p></td>
<td><p>Controlla la corrispondenza alla fine di una riga.</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>OR logico tra espressioni.</p></td>
</tr>
<tr class="even">
<td><p>()</p></td>
<td><p>Gruppi di sottoespressioni.</p></td>
</tr>
<tr class="odd">
<td><p>[]</p></td>
<td><p>Definizione di una classe di caratteri.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>Controlla la corrispondenza all'espressione precedente zero o più volte.</p></td>
</tr>
<tr class="odd">
<td><p>+</p></td>
<td><p>Controlla la corrispondenza all'espressione precedente una o più volte.</p></td>
</tr>
<tr class="even">
<td><p>?</p></td>
<td><p>Controlla la corrispondenza dell'espressione precedente zero o più volte.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n</em>}</p></td>
<td><p>Controlla la corrispondenza all'espressione precedente <em>n</em> volte.</p></td>
</tr>
<tr class="even">
<td><p>{<em>n,</em>}</p></td>
<td><p>Controlla la corrispondenza all'espressione precedente almeno <em>n</em> volte.</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n, m</em>}</p></td>
<td><p>Controlla la corrispondenza all'espressione precedente almeno <em>n</em> volte e più di <em>m</em> volte.</p></td>
</tr>
<tr class="even">
<td><p>\d</p></td>
<td><p>Controlla la corrispondenza di una cifra.</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>Controlla la corrispondenza di un carattere che non è una cifra.</p></td>
</tr>
<tr class="even">
<td><p>\w</p></td>
<td><p>Controlla la corrispondenza di un carattere alfanumerico, compreso il carattere di sottolineatura.</p></td>
</tr>
<tr class="odd">
<td><p>\W</p></td>
<td><p>Controlla la corrispondenza di un carattere che non è un carattere alfanumerico.</p></td>
</tr>
<tr class="even">
<td><p>\s</p></td>
<td><p>Controlla la corrispondenza di un carattere di spazio (\t, \n, \r o \f).</p></td>
</tr>
<tr class="odd">
<td><p>\S</p></td>
<td><p>Controlla la corrispondenza a un carattere non di spazio.</p></td>
</tr>
<tr class="even">
<td><p>\t</p></td>
<td><p>Tabulazione.</p></td>
</tr>
<tr class="odd">
<td><p>\n</p></td>
<td><p>Nuova linea.</p></td>
</tr>
<tr class="even">
<td><p>\r</p></td>
<td><p>Ritorno a capo.</p></td>
</tr>
<tr class="odd">
<td><p>\f</p></td>
<td><p>Alimentazione foglio.</p></td>
</tr>
<tr class="even">
<td><p>\<em>m</em></p></td>
<td><p>Esc <em>m</em>, dove <em>m</em> è uno dei meta caratteri descritti sopra: ^, ., $, |, (), [], *, +, ?, \, o /.</p></td>
</tr>
</tbody>
</table>


L'elemento Regex ha un attributo "id" che viene utilizzato come riferimento nelle regole dell'entità o dell'affinità corrispondenti. Ad un singolo elemento Regex possono far riferimento più regole entità e affinità. L'espressione Regex è definita come il valore dell'elemento Regex.

    <Regex id="CCRegex">
         \bcc\#\s|\bcc\#\:\s
    </Regex>
    ...
    <Regex id="ItinFormatted">
        (?:^|[\s\,\:])(?:9\d{2})[- ](?:[78]\d[-       ]\d{4})(?:$|[\s\,]|\.\s)
    </Regex>
    ...
    <Regex id="NorthCarolinaDriversLicenseNumber">
        (^|\s|\:)(\d{1,8})($|\s|\.\s)
    </Regex>

## Combinazione di più elementi di corrispondenza

Una comune tecnica per aumentare l'affidabilità della corrispondenza è definire la semantica tra più elementi Match, ad esempio che si devono verificare una o più corrispondenze. L'elemento Any consente la definizione di una logica basata tra più corrispondenze. L'elemento Any può essere utilizzato come sottoelemento dell'elemento Pattern. Contiene uno o più elementi figlio Match e definisce la logica della corrispondenza tra loro. Vedere gli esempi di codice XML seguenti per gli elementi Any con tutte le corrispondenze, logica "not" e conteggio corrispondenza esatta.

L'attributo opzionale minMatches può essere utilizzato (predefinito = 1) per definire il numero minimo di elementi Match che devono essere verificati per soddisfare la corrispondenza. Similmente, l'attributo opzionale maxMatches può essere utilizzato (predefinito = numero di elementi figlio Match) per definire il numero massimo di elementi Match che devono essere verificati per soddisfare la corrispondenza. Queste condizioni vengono utilizzate combinando operatori logici basati sull'utilizzo degli attributi minMatches e maxMatches, consentendo le seguenti semantiche:

  - Controlla la corrispondenza di tutti gli elementi figlio Match
    
    Non controllare la corrispondenza di nessun elemento figlio Match
    
    Controlla la corrispondenza di un sottogruppo esatto di elementi Match

<!-- end list -->

```
    <Any minMatches="3" maxMatches="3">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>
```
```
    <Any maxMatches="0">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>
```
```
    <Any minMatches="1" maxMatches="1">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>
```

## Aumento del livello di affidabilità con maggiore evidenza

Per le regole basate su entità, un'altra opzione per migliorare l'affidabilità è definire più elementi Pattern, ciascuno con un numero crescente di evidenze avvaloranti. Questo si ottiene utilizzando minMatches e maxMatches per l'elemento Any per creare modelli indipendenti con livello di affidabilità crescente basato sull'aumento del numero di evidenze avvaloranti. Esempio:

  - se viene trovata una parte di prova convalidante: livello di probabilità del 65%

  - se due parti: livello di probabilità del 75%

  - se tre parti: livello di probabilità del 85%

<!-- end list -->

    <Entity id="..." patternsProximity="300" >
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Any maxMatches="1">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="75">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="2" maxMatches="2">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="85">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="3">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity>

## Esempio: Regola codice di previdenza sociale statunitense

Questa sezione include una descrizione introduttiva per la realizzazione di una regola che controlla la corrispondenza del codice di previdenza sociale statunitense. Si inizierà con una descrizione di come identificare i contenuti che corrispondono al codice di previdenza sociale. Un codice di previdenza sociale si considera trovato se:

1.  Il Regex corrisponde a un codice di previdenza sociale formattato (ed è nell'intervallo SSN valido)

2.  Evidenza avvalorante   nelle vicinanze deve trovarsi uno dei seguenti:
    
    1.  Parola chiave corrispondente {previdenza sociale, Soc Sec, SSN, SSNS, SSN \#, SS\#, SSID}
    
    2.  Testo che rappresenta un indirizzo statunitense
    
    3.  Testo che rappresenta una data
    
    4.  Testo che rappresenta un nome

Quindi, tradurre la descrizione nella rappresentazione dello schema della regola:

    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77"
             patternsProximity="300" RecommendedConfidence="85">
        <Pattern confidenceLevel="85">
          <IdMatch idRef="FormattedSSN" />
          <Any minMatches="1">
              <Match idRef="SSNKeywords" />
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
        </Pattern>
    </Entity>

## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Definire modelli DLP e tipi di informazione propri](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[Importare un modello di criteri DLP personalizzato da un file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

