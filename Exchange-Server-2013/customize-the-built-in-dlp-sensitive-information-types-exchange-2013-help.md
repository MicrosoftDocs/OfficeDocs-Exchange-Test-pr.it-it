---
title: 'Personalizza tipi info. riservate DLP incorporati: Exchange 2013 Help'
TOCTitle: Personalizzare i tipi di informazioni riservate DLP incorporati
ms:assetid: 3f8bf141-2e7c-4ea7-b102-dfd6c41539da
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn781122(v=EXCHG.150)
ms:contentKeyID: 62757562
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Personalizzare i tipi di informazioni riservate DLP incorporati

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-05-26_

Durante la ricerca di informazioni riservate nel messaggio di posta elettronica, è necessario descrivere in che cos'è chiamato una *regola di*tali informazioni. Prevenzione della perdita di dati (DLP) include un pacchetto di 51 regole per i tipi più comuni di informazioni riservate che è possibile utilizzare immediatamente. Per utilizzare queste regole, è necessario includerli in un criterio. È possibile che si desidera modificare queste regole predefinite per soddisfare esigenze specifiche della propria organizzazione ed è possibile farlo creando un tipo di informazioni riservate personalizzate. In questo argomento viene illustrato come personalizzare il file XML che contiene l'insieme di regole esistente per rilevare una vasta gamma di possibili informazioni carta di credito.

È possibile eseguire in questo esempio viene e applicare ad altri tipi di informazioni riservate incorporati. Per un elenco di tipi di informazioni riservate predefinite e le definizioni XML, vedere l'argomento [Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) .

In questa sezione viene descritto nelle sezioni seguenti per le personalizzazioni regola XML:

  - Esportazione XML di regole corrente

  - Individuare la regola che si desidera modificare nel file XML

  - Modificare il codice XML e creare un nuovo tipo di informazioni riservate

  - Richiedono minore ulteriori prove

  - Cercare parole chiave specifiche dell'organizzazione

  - Caricare la regola

Per informazioni su quali sono le diverse parti di regole e quali vengono, vedere Glossario di termini alla fine di questo argomento.

## Esportare il file XML delle regole corrente

Per esportare il file XML, è necessario utilizzare il Exchange Management Shell o. Per Exchange Server 2013, vedere [Utilizzo di PowerShell con Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/it-it/library/bb123778\(v=exchg.150\)). Per Exchange Online, vedere [Connessione a Exchange Online tramite Remote PowerShell](https://technet.microsoft.com/it-it/library/jj984289\(v=exchg.150\)).

1.  Exchange Management Shell o Exchange Online PowerShell, digitare **Get-ClassificationRuleCollection** per visualizzare le regole dell'organizzazione sullo schermo. Se è stato creato il proprio, si verrà visualizzato solo l'impostazione predefinita, le regole predefinite, denominate "Pacchetto Microsoft Rule."

2.  Archiviare le regole dell'organizzazione in una in una variabile digitando **$ruleCollections = Get-ClassificationRuleCollection**. Archiviare un elemento in una variabile rende facilmente disponibile più avanti in un formato che può essere utilizzato per i comandi di PowerShell remoti.

3.  Rendere un file XML formattato con tutti i dati digitando **Set-Content - path "C:\\custompath\\exportedRules.xml"-Encoding Byte-valore $ruleCollections.SerializedClassificationRuleCollection**. (**Set-content** è la parte del cmdlet che scrive il codice XML nel file).
    

    > [!IMPORTANT]
    > Accertarsi di utilizzare il percorso del file in cui è memorizzato in realtà il pacchetto di regole. <STRONG>C:\custompath\</STRONG> è un segnaposto.



## Individuare la regola che si desidera modificare nel file XML

I cmdlet sopra esportata l'intera *raccolta di regole*, contenente le regole 51 predefinite che offriamo. Successivamente sarà necessario cercare specifici per la regola per numero di carta di credito da modificare.

1.  Utilizzare un editor di testo per aprire il file XML esportato nella sezione precedente.

2.  Scorrimento verso il basso per il tag **\<Rules\>** , che corrisponde all'inizio della sezione contenente regole DLP. (Dal momento che questo file XML contiene le informazioni per l'insieme di regole intera, contenga altre informazioni nella parte superiore che è necessario scorrere per ottenere le regole precedenti.)

3.  Cercare **Func\_credit\_card** trovare la definizione della regola il numero di carta di credito. (Nel file XML, i nomi delle regole non possono contenere spazi, in modo che gli spazi in genere vengono sostituiti con caratteri di sottolineatura e i nomi delle regole vengono abbreviati in alcuni casi. Un esempio di questo oggetto è regola numerica di previdenza sociale statunitense, ovvero abbreviato "SSN." La regola di carta di credito XML dovrebbe essere simile nell'esempio di codice.
    
        <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085"
               patternsProximity="300" recommendedConfidence="85">
              <Pattern confidenceLevel="85">
               <IdMatch idRef="Func_credit_card" />
                <Any minMatches="1">
                  <Match idRef="Keyword_cc_verification" />
                  <Match idRef="Keyword_cc_name" />
                  <Match idRef="Func_expiration_date" />
                </Any>
              </Pattern>
            </Entity>

Dopo aver individuato la definizione della regola il numero di carta di credito nel file XML, è possibile personalizzare il XML della regola per soddisfare le esigenze. (Per un aggiornamento per le definizioni XML, vedere Glossario di termini alla fine di questo argomento).

## Modificare il codice XML e creare un nuovo tipo di informazioni riservate

È necessario innanzitutto creare un nuovo tipo di informazioni riservate, in quanto non è possibile modificare direttamente le regole predefinite. È possibile eseguire un'ampia gamma di operazioni con tipi di informazioni riservate personalizzate, come descritto nella [Sviluppo di pacchetti di regole di informazioni riservate](technical-description-of-xml-schema-for-dlp-rule-packages.md). In questo esempio, è sarà mantenere semplice e solo rimuovere l'elemento avvalorante e aggiungere parole chiave per la regola di numero di carta di credito.

Tutte le definizioni di regole XML sono basate sul modello generale seguente. È necessario copiare e incollare la definizione del numero di carta di credito XML nel modello di modificare alcuni valori (si noti i segnaposto "..." nell'esempio seguente) e quindi caricare il codice XML modificato come una nuova regola che può essere utilizzata nei criteri.

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id=". . .">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id=". . ." /> 
        <Details defaultLangCode=". . .">
          <LocalizedDetails langcode=" . . . ">
             <PublisherName>. . .</PublisherName>
             <Name>. . .</Name>
             <Description>. . .</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
       <!-- Paste the Credit Card Number rule definition here.--> 
    
          <LocalizedStrings>
             <Resource idRef=". . .">
               <Name default="true" langcode=" . . . ">. . .</Name>
               <Description default="true" langcode=". . ."> . . .</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

A questo punto, è necessario qualcosa di simile al seguente XML. Poiché i pacchetti di regole e le regole vengono identificate in base al GUID univoco, è necessario generare due GUID: una per il pacchetto di regole e una per sostituire il GUID della regola di numero di carta di credito. (Il GUID per l'ID di entità nell'esempio di codice seguente è quella per la definizione della regola incorporata, che si desidera sostituire con uno nuovo). Esistono diversi modi per generare i GUID, ma è possibile procede facilmente in PowerShell digitando **\[guid\]::NewGuid()**.

    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id="8aac8390-e99f-4487-8d16-7f0cdee8defc">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id="8d34806e-cd65-4178-ba0e-5d7d712e5b66" />
        <Details defaultLangCode="en">
          <LocalizedDetails langcode="en">
            <PublisherName>Contoso Ltd.</PublisherName>
            <Name>Financial Information</Name>
            <Description>Modified versions of the Microsoft rule package</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f"
           patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    
          <LocalizedStrings>
             <Resource idRef="db80b3da-0056-436e-b0ca-1f4cf7080d1f"> 
    <!-- This is the GUID for the preceding Credit Card Number entity because the following text is for that Entity. -->
               <Name default="true" langcode="en-us">Modified Credit Card Number</Name>
               <Description default="true" langcode="en-us">Credit Card Number that looks for additional keywords, and another version of Credit Card Number that doesn't require keywords (but has a lower confidence level)</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>

## Rimuovere il requisito di elemento avvalorante da un tipo di informazioni riservate

Dopo aver creato un nuovo tipo di informazioni riservate che si è in grado di caricare all'ambiente Exchange, il passaggio successivo consiste per rendere più specifica la regola. Modificare la regola in modo che esegua solo per un numero di 16 cifre che passa il valore di checksum ma che non richiede ulteriori prove (avvalorante) (ad esempio le parole chiave). A tale scopo, è necessario rimuovere la parte di codice XML Cerca elemento avvalorante. Elemento avvalorante è molto utile per ridurre i falsi positivi in quanto in genere non esistono alcune parole chiave o una data di scadenza trova vicino il numero di carta di credito. Se si rimuovono tale prove, è opportuno modificare la modalità che si è trovato un numero di carta di credito abbassando **confidenceLevel**, ovvero 85 nell'esempio.

    <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="300"
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
          </Pattern>
        </Entity>

## Cercare parole chiave specifiche dell'organizzazione

È possibile richiedere l'elemento avvalorante ma si desidera che le parole chiave diverse o aggiuntive, e magari che si desidera modificare la posizione in cui cercare di prova. È possibile modificare **patternsProximity** per espandere o ridurre la finestra per l'elemento avvalorante intorno al numero di 16 cifre. Per aggiungere le parole chiave, è necessario definire un elenco delle parole chiave e farvi riferimento all'interno della regola. Il codice XML seguente aggiunge le parole chiave "scheda società" e "Contoso scheda" in modo che i messaggi che contengono le frasi all'interno di 150 caratteri di un numero di carta di credito verranno identificato come un numero di carta di credito.

    <Rules>
    <! -- Modify the patternsProximity to be "150" rather than "300." -->
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="150" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
    <!-- Add the following XML, which references the keywords at the end of the XML sample. -->
              <Match idRef="My_Additional_Keywords" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    <!-- Add the following XML, and update the information inside the <Term> tags with the keywords that you want to detect. -->
        <Keyword id="My_Additional_Keywords">
          <Group matchStyle="word">
            <Term caseSensitive="false">company card</Term>
            <Term caseSensitive="false">Contoso card</Term>
          </Group>
        </Keyword>

## Caricare la regola

Per caricare la regola, è necessario eseguire le operazioni seguenti.

1.  Salvarlo come file XML con la codifica Unicode. Ciò è importante in quanto la regola non funziona se il file verrà salvato con una codifica diversa.

2.  Connettersi a PowerShell Exchange Management Shell o Exchange Online. Per Exchange Server 2013, vedere [Utilizzo di PowerShell con Exchange 2013 (Exchange Management Shell)](https://technet.microsoft.com/it-it/library/bb123778\(v=exchg.150\)). Per Exchange Online, vedere [Connessione a Exchange Online tramite Remote PowerShell](https://technet.microsoft.com/it-it/library/jj984289\(v=exchg.150\)).

3.  Exchange Management Shell o Exchange Online PowerShell, digitare **New-ClassificationRuleCollection - FileData (Get-Content - Path "C:\\custompath\\MyNewRulePack.xml"-Encoding Byte)**.
    

    > [!IMPORTANT]
    > Accertarsi di utilizzare il percorso del file in cui è archiviato effettivamente il pacchetto di regole. <STRONG>C:\custompath\</STRONG> è un segnaposto.



4.  Conferma, digitare **s** e quindi premere **INVIO**.

5.  Verificare che la nuova regola è stata caricata digitando **Get-DataClassification**, che ora visualizzato il nome della regola.

Per iniziare a utilizzare la nuova regola per il rilevamento di informazioni riservate, è necessario aggiungere una regola a un criterio DLP. Per informazioni su come aggiungere una regola a un criterio, vedere [Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md).

## Glossario di termini

Queste sono le definizioni dei termini che si sono verificati durante la procedura.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Termine</th>
<th>Definizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Entity</p></td>
<td><p>Entità sono cosiddetta tipi di informazioni riservate, ad esempio numeri di carta di credito. Ogni entità dispone di un GUID come il relativo ID. Se si copia un GUID e cercarlo nel file XML, è possibile trovare la definizione della regola XML e tutte le traduzioni localizzate della regola XML. È inoltre possibile trovare questa definizione individuando il GUID per la conversione e quindi cercare il GUID.</p></td>
</tr>
<tr class="even">
<td><p>Funzioni</p></td>
<td><p>Il file XML fa riferimento <strong>Func_credit_card</strong>, ovvero una funzione nel codice compilato. Vengono utilizzate per eseguire regexes complessi e verificare che il nostro regole predefinite deve corrispondere checksum.) Perché ciò avviene nel codice, alcune delle variabili non vengono visualizzati nel file XML.</p></td>
</tr>
<tr class="odd">
<td><p>IdMatch</p></td>
<td><p>Questo è l'identificatore che rappresenta il motivo di ricerca, ad esempio, un numero di carta di credito. Per ulteriori informazioni su questa e sui tag <strong>Match</strong> nelle <a href="technical-description-of-xml-schema-for-dlp-rule-packages.md">regole di entità</a>.</p></td>
</tr>
<tr class="even">
<td><p>Elenchi di parole chiave</p></td>
<td><p>File XML fa riferimento anche <strong>keyword_cc_verification</strong> e <strong>keyword_cc_name</strong>, ovvero gli elenchi delle parole chiave da cui stiamo cercando corrispondenze all'interno di <strong>patternsProximity</strong> per l'entità. Queste attualmente non sono visualizzate nel file XML.</p></td>
</tr>
<tr class="odd">
<td><p>Modello</p></td>
<td><p>Il motivo contiene l'elenco dei quali il tipo sensibile Cerca. Sono incluse le parole chiave, regexes e funzioni interne (che eseguono le attività come la verifica checksum). Tipi di informazioni riservate possono avere più modelli con confidences univoco. Ciò è utile quando si crea un tipo di informazioni riservate che restituisce un confidenza elevata se viene trovato l'elemento avvalorante e una probabilità inferiore se viene trovato senza alcuna elemento avvalorante.</p></td>
</tr>
<tr class="even">
<td><p>Motivo confidenceLevel</p></td>
<td><p>Questo è il livello di probabilità che il motore DLP è stata trovata una corrispondenza. Questo livello di probabilità è associato a una corrispondenza per il modello se vengono soddisfatti i requisiti del criterio. Questa è la misura delle probabilità è necessario considerare se mediante il trasporto di Exchange regole (ETRs).</p></td>
</tr>
<tr class="odd">
<td><p>patternsProximity</p></td>
<td><p>Quando si trova effetto simile a un formato numero di carta di credito, <strong>patternsProximity</strong> è prossimità attorno a tale numero di cui verrà esaminato per elemento avvalorante.</p></td>
</tr>
<tr class="even">
<td><p>recommendedConfidence</p></td>
<td><p>Si tratta del livello probabilità che è consigliabile per questa regola. Probabilità consigliate si applica a entità e le affinità. Per le entità, questo numero non viene mai valutato <strong>confidenceLevel</strong> per il motivo. Si tratta semplicemente un suggerimento per scegliere un livello di probabilità se si desidera applicare uno. Per affinità, <strong>confidenceLevel</strong> del criterio di ricerca deve essere maggiore del numero di <strong>recommendedConfidence</strong> per un'azione ETR da richiamare. <strong>recommendedConfidence</strong> è il confidenza livello predefinito utilizzato in ETRs che consente di richiamare un'azione. Se si desidera, è possibile modificare manualmente il ETR da richiamare base off livello di probabilità del criterio, in realtà.</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

  - [Modalità di applicazione delle regole DLP per la valutazione dei messaggi](how-dlp-rules-are-applied-to-evaluate-messages-exchange-2013-help.md)

  - [Creare un criterio DLP personalizzato](create-a-custom-dlp-policy-exchange-2013-help.md)

  - [Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

