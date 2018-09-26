---
title: 'Sviluppo di pacchetti di regole di informazioni riservate: Exchange 2013 Help'
TOCTitle: Sviluppo di pacchetti di regole di informazioni riservate
ms:assetid: c4ab8707-0839-4855-9390-3dbcb43475a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ674704(v=EXCHG.150)
ms:contentKeyID: 50481612
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sviluppo di pacchetti di regole di informazioni riservate

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-07-28_

Le istruzioni e lo schema XML presenti in questo argomento consentiranno di avviare la creazione dei file XML di base della prevenzione della perdita dati (DLP) che definiscono i tipi di informazioni riservate in un pacchetto di regole di classificazione. Dopo aver creato un file XML con formato corretto, è possibile importarlo utilizzando l'interfaccia di amministrazione di Exchange o Exchange Management Shell per creare una soluzione DLP di Microsoft Exchange Server 2013. Un file XML che è un modello di criteri DLP personalizzato può contenere l'XML, ovvero il pacchetto di regole di classificazione. Per una panoramica sulla definizione dei modelli DLP come file XML, vedere [Definire modelli DLP e tipi di informazione propri](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

**Sommario**

Overview of the rule authoring process

Rule description

Basic rule structure

Using local languages in your XML file

Classification rule pack XML schema definition

For more information

## Cenni preliminari sul processo di creazione della regola

Il processo di creazione della regola è composto dai seguenti passaggi generali.

1.  Preparazione di una serie di documenti di prova rappresentativi del loro ambiente di destinazione. Tra le caratteristiche principali da considerare per la serie di documenti di prova sono incluse: un sottoinsieme dei documenti deve contenere l'entità o l'affinità per cui viene creata la regola e un sottoinsieme dei documenti non deve contenere l'entità o l'affinità per cui viene creata la regola.

2.  Identificare le regole che soddisfano i requisiti di accettazione (precisione e richiamo) per individuare il contenuto qualificante. Questa operazione potrebbe richiedere lo sviluppo di più condizioni all'interno di una regola, associata alla logica booleana, che insieme soddisfano i requisiti di corrispondenza minimi per identificare i documenti di destinazione.

3.  Stabilire il livello di sicurezza consigliato per le regole basate sui requisiti di accettazione (precisione e richiamo). L'elemento della sicurezza consigliato può essere pensato come livello di sicurezza predefinito per la regola.

4.  Convalidare le regole creando con esse l'istanza di uno schema e monitorando il contenuto di prova campione. In base ai risultati, regolare le regole o il livello di sicurezza per ottimizzare il contenuto rilevato riducendo al minimo i falsi positivi e i negativi. Continuare con il ciclo di convalida e con le modifiche delle regole fino a raggiungere un livello di individuazione del contenuto soddisfacente per gli esempi positivi e negativi.

Per informazioni sulla definizione dello schema XML per i file modello del criterio, vedere [Sviluppo di file modello per il criterio DLP](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md).

## Descrizione delle regole

Per il motore di rilevamento delle informazioni riservate del criterio DLP è possibile creare due tipi di regole: Entità e affinità. La scelta del tipo di regola si basa sul tipo di logica di elaborazione che deve essere applicata all'elaborazione del contenuto, come descritto nelle sezioni precedenti. Le definizioni delle regole sono configurate in un documento XML nel formato descritto dallo schema XSD standardizzato delle regole. Le regole descrivono sia il tipo di contenuto da soddisfare che il livello di sicurezza in base a cui la corrispondenza descritta rappresenta il contenuto di destinazione. Il livello di sicurezza definisce la probabilità per l'entità di essere presente se viene trovato un criterio nel contenuto o la probabilità per l'affinità di essere presente se viene trovata una prova.

## Struttura di base delle regole

La definizione delle regole è costituita da tre componenti principali:

1.  **Entità**   definisce la logica di corrispondenza e calcolo per tale regola

2.  **Affinità**   definisce la logica di corrispondenza per la regola

3.  **Stringhe localizzate**   localizzazione per nomi di regole e descrizioni relative

Vengono utilizzati tre elementi di supporto aggiuntivi per definire i dettagli dell'elaborazione e con riferimento all'interno dei componenti principali: parola chiave, regex e funzione. L'utilizzo dei riferimenti consente di servirsi di una singola definizione degli elementi di supporto, come il codice fiscale, in più regole di entità o affinità. La struttura di base delle regole in formato XML può essere considerata come segue.
```xml
    <?xml version="1.0" encoding="utf-8"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
    
      <RulePack id="DAD86A92-AB18-43BB-AB35-96F7C594ADAA">
        <Version major="1" minor="0" build="0" revision="0"/>
        <Publisher id="619DD8C3-7B80-4998-A312-4DF0402BAC04"/>
        <Details defaultLangCode="en-us">
          <LocalizedDetails langcode="en-us">
            <PublisherName>DLP by EPG</PublisherName>
            <Name>CSO Custom Rule Pack</Name>
            <Description>This is a rule package for a EPG demo.</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
    
      <Rules>
    
        <!-- Employee ID -->
        <Entity id="E1CC861E-3FE9-4A58-82DF-4BD259EAB378" patternsProximity="300" recommendedConfidence="75">
          <Pattern confidenceLevel="75">
            <IdMatch idRef="Regex_employee_id" />
            <Match idRef="Keyword_employee" />
          </Pattern>
        </Entity>
    
        <Regex id="Regex_employee_id">(\s)(\d{9})(\s)</Regex>
        <Keyword id="Keyword_employee">
          <Group matchStyle="word">
            <Term>Identification</Term>
            <Term>Contoso Employee</Term>
          </Group>
        </Keyword>
    
    
        <LocalizedStrings>
    
          <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB378">
            <Name default="true" langcode="en-us">
              Employee ID
            </Name>
            <Description default="true" langcode="en-us">
              A custom classification for detecting Employee ID's
            </Description>
          </Resource>
    
        </LocalizedStrings>
      </Rules>
    </RulePackage>
```

## Regole dell'entità

Le regole dell'entità sono destinate a identificatori ben definiti, quali il codice fiscale, e sono rappresentate da una raccolta di schemi numerabili. Le regole dell'entità restituiscono un calcolo e il livello di sicurezza di una corrispondenza dove il calcolo indica il numero totale delle istanze dell'entità trovate e il livello di sicurezza indica la probabilità che l'entità specificata esista nel documento in questione. L'entità contiene l'attributo "id" come identificatore univoco. L'identificatore viene utilizzato per la localizzazione, il controllo delle versioni e l'esecuzione di query. L'id dell'entità deve essere un GUID e non può essere duplicato in altre entità o affinità. Viene indicato nella sezione delle stringhe localizzate.

Le regole dell'entità contengono l'attributo facoltativo patternsProximity (valore predefinito = 300) utilizzato quando si applica la logica booleana per specificare l'adiacenza di più schemi necessari a soddisfare la condizione. L'elemento Entity contiene uno o più elementi Pattern figlio, dove ogni modello è una rappresentazione distinta dell'entità (entità carta di credito o patente di guida). L'elemento Pattern ha un attributo obbligatorio confidenceLevel che rappresenta la precisione del modello in base al set di dati dell'esempio. L'elemento Pattern può avere tre elementi figlio:

1.  IdMatch: obbligatorio.

2.  Match

3.  Qualsiasi

Se gli elementi Pattern restituiscono il valore "true", il modello è soddisfatto. Il conteggio per l'elemento Entity equivale alla somma di tutti i conteggi dell'elemento Pattern rilevato.

![Formula matematica per il conteggio di entità](images/JJ674704.25309939-98bc-4460-8f89-8560bbad7981(EXCHG.150).gif "Formula matematica per il conteggio di entità")

dove k è il numero di elementi Pattern per Entity.

Un elemento Pattern deve avere esattamente un elemento IdMatch. IdMatch rappresenta l'identificatore che il modello deve soddisfare, ad esempio un numero di carta di credito o un ID contribuente individuale. Il conteggio per un modello è il numero di IdMatch soddisfatti con l'elemento Pattern. L'elemento IdMatch ancora la finestra di prossimità per gli elementi Match.

Un altro elemento secondaria facoltativo dell'elemento del modello è l'elemento di corrispondenza che rappresenta l'elemento avvalorante necessari per far corrispondere per supportare la ricerca di elemento IdMatch. Ad esempio, la regola confidenza superiore può richiedere che, oltre a trovare un numero di carta di credito, gli elementi aggiuntivi siano presenti nel documento, in una finestra di prossimità di carta di credito, quali indirizzo e il nome. Questi elementi aggiuntivi sarebbe rappresentati tramite l'elemento di corrispondenza o qualsiasi elemento (descritti in dettaglio nella sezione Matching Methods and Techniques). Più elementi corrispondenti possono essere inclusi nella definizione di un motivo che può essere inclusi direttamente nell'elemento motivo o combinati utilizzando qualsiasi elemento per definire la semantica corrispondente. Restituisce true se viene trovata una corrispondenza nella finestra di prossimità ancorata intorno al contenuto IdMatch.

Entrambi gli elementi IdMatch e Match non definiscono i dettagli del contenuto che deve essere soddisfatto ma vi fanno riferimento tramite l'attributo idRef. In questo modo viene favorita la possibilità di riutilizzo delle definizioni in più costrutti del modello.
```powershell
    <Entity id="..." patternsProximity="300" > 
        <Pattern confidenceLevel="85">
            <IdMatch idRef="FormattedSSN" />
            <Any minMatches="1">
                <Match idRef="SSNKeyword" />
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>  
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Match idRef="SSNKeyword" />
            <Any minMatches="1">        
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity> 
```

L'elemento dell'id entità, rappresentato nell'XML precedente da "..." deve essere un GUID e viene indicato nella sezione Stringhe localizzate.

## Finestra di prossimità dello schema dell'entità

L'entità conserva il valore dell'attributo facoltativo patternsProximity (intero, predefinito = 300) utilizzato per trovare gli schemi. Per ciascun modello il valore dell'attributo definisce la distanza (in caratteri Unicode) dalla posizione IdMatch per tutte le altre corrispondenze specificate per il modello. La finestra di prossimità viene ancorata dalla posizione IdMatch con la finestra che si estende a sinistra e a destra di IdMatch.

![Modello di testo con elementi corrispondenti richiamati](images/JJ674704.65d52989-f50f-4097-b39a-9612f860d727(EXCHG.150).gif "Modello di testo con elementi corrispondenti richiamati")

Nell'esempio in basso viene descritto in che modo la finestra di prossimità influisce sull'algoritmo di corrispondenza dove l'elemento SSN IdMatch richiede almeno 1 indirizzo, nome o data che convalidino le corrispondenze. Solo SSN1 e SSN4 generano una corrispondenza perché per SSN2 e SSN3 non viene trovata alcuna prova oppure ne viene trovata solo una parziale nella finestra di prossimità.

![Esempi di corrispondenza e non corrispondenza della regola di prossimità](images/JJ674704.8117deb3-d8c8-4d4e-a011-ac5f9990b08e(EXCHG.150).gif "Esempi di corrispondenza e non corrispondenza della regola di prossimità")

Si noti che il corpo del messaggio e tutti gli allegati vengono considerati come elementi indipendenti. Ciò significa che la finestra di prossimità non prolungano oltre la fine di ciascuno di questi elementi. Per ogni elemento (allegato o nel corpo), il idMatch e l'elemento avvalorante deve risiedere all'interno di ogni.

## Livello di sicurezza dell'entità

Il livello di sicurezza dell'elemento entità è la combinazione di tutti i livelli di sicurezza del modello soddisfatto. Vengono combinati utilizzando la seguente equazione:

![Formula matematica per il livello di probabilità dell'entità](images/JJ674704.9b8bb9c8-3ded-4ea5-a609-71d8034b1017(EXCHG.150).gif "Formula matematica per il livello di probabilità dell'entità")

dove k indica il numero di elementi Pattern per l'entità e un modello che non corrisponde restituisce un livello di sicurezza pari a 0.

Tornando all'esempio del codice della struttura dell'elemento entità, se entrambi gli schemi vengono soddisfatti, il livello di sicurezza dell'entità è 94,75% in base al calcolo seguente:

CLEntity= 1-\[(1-CLPattern1) x (1-CLPattern1)\]

*= 1-\[(1-0,85) x (1-0,65)\]*

*= 1-(0,15 x 0,35)*

*= 94.75%*

Analogamente, se solo il secondo schema genera una corrispondenza, il livello di sicurezza dell'entità è 65% in base al calcolo seguente:

CLEntity= 1 – \[(1 – CLPattern1) X (1 – CLPattern1)\]

*= 1 – \[(1 – 0) X (1 – 0,65)\]*

*= 1 – (1 X 0,35)*

*= 65%*

Questi valori di sicurezza vengono assegnati nelle regole per schemi individuali in base al set di documenti di prova convalidati come parte del processo di creazione della regola.

## Regole dell'affinità

Le regole dell'affinità sono destinate al contenuto senza identificatori ben definiti, ad esempio Sarbanes-Oxley o contenuti finanziari aziendali. Per questo contenuto non può essere trovato alcun identificatore coerente. L'analisi richiede invece di determinare se è presente una raccolta di prove. Le regole dell'affinità non restituiscono un calcolo, ma indicano se viene trovato e il livello di sicurezza associato. Il contenuto dell'affinità viene rappresentato come una raccolta di prove indipendenti. Evidenza è un'aggregazione di corrispondenze necessarie entro una determinata prossimità. Per la regola dell'affinità la prossimità viene definita dall'attributo evidencesProximity (il valore predefinito è 600) e il livello di sicurezza minimo dall'attributo thresholdConfidenceLevel.

Le regole dell'affinità contengono l'attributo id per l'identificatore univoco utilizzato per la localizzazione, il controllo delle versioni e l'esecuzione di query. A differenza delle regole dell'entità, poiché le regole dell'affinità non si basano su identificatori ben definiti, non contengono l'elemento IdMatch.

Ciascuna regola dell'affinità contiene uno o più elementi Evidence figlio che definiscono la prova che deve essere trovata e il livello di sicurezza che contribuisce alla regola dell'affinità. L'affinità non viene considerata trovata se il livello di sicurezza risultante è al di sotto del livello di soglia. Ciascuna prova rappresenta logicamente la prova convalidante per questo "tipo" di documento e l'attributo confidenceLevel è la precisione per la prova nel set di dati di prova.

Gli elementi Evidence hanno uno o più elementi figlio Match e Any. Se tutti gli elementi figlio Match e Any vengono soddisfatti, viene trovata la prova e il livello di sicurezza contribuisce al calcolo del livello di sicurezza delle regole. La stessa descrizione si applica agli elementi Match e Any per le regole di affinità e per le regole di entità.
```powershell
    <Affinity id="..." 
              evidencesProximity="1000"
              thresholdConfidenceLevel="65">
        <Evidence confidenceLevel="40">
            <Any> 
                <Match idRef="AssetsTerms" /> 
                <Match idRef="BalanceSheetTerms" /> 
                <Match idRef="ProfitAndLossTerms" /> 
            </Any> 
        </Evidence>
        <Evidence confidenceLevel="40">
            <Any minMatches="2"> 
                <Match idRef="TaxTerms" /> 
                <Match idRef="DollarAmountTerms" /> 
                <Match idRef="SECTerms" /> 
                <Match idRef="SECFilingFormTerms" /> 
                <Match idRef="DollarTotalRegex" /> 
            </Any> 
        </Evidence>
    </Affinity>
```

## Finestra di prossimità di affinità

La finestra di prossimità per l'affinità è calcolata in modo diverso rispetto agli schemi dell'entità. La prossimità dell'affinità segue un modello di finestra scorrevole. L'algoritmo di prossimità dell'affinità tenta di trovare il numero massimo di prove corrispondenti nella finestra data. Le prove nella finestra di affinità devono avere un livello di sicurezza maggiore rispetto alla soglia definita per la regola dell'affinità da trovare.

![Testo in prossimità di una corrispondenza della regola di affinità](images/JJ674704.2601ec86-0094-43fa-8d22-9d97f7465942(EXCHG.150).gif "Testo in prossimità di una corrispondenza della regola di affinità")

## Livello di sicurezza dell'affinità

Il livello di sicurezza dell'affinità equivale alla combinazione delle prove trovate all'interno della finestra di prossimità per la regola dell'affinità. Analogamente al livello di sicurezza della regola dell'entità, la differenza principale sta nell'applicazione della finestra di prossimità. Analogamente alle regole dell'entità, il livello di sicurezza dell'elemento Affinity è la combinazione di tutti i livelli di sicurezza delle prove soddisfatti, ma per la regola dell'affinità rappresenta solo la combinazione più elevata degli elementi di prova trovati all'interno della finestra di prossimità. I livelli di sicurezza delle prove sono combinati utilizzando la seguente equazione:

![Formula matematica per la probabilità della regola di affinità](images/JJ674704.8a5da4ca-af02-4c5a-ab60-0072dc7e7a0f(EXCHG.150).gif "Formula matematica per la probabilità della regola di affinità")

dove k è il numero di elementi di prova per l'affinità soddisfatti all'interno della finestra di prossimità.

Tornando all'esempio della figura 4 con la struttura della regola dell'affinità, se tutte e tre le prove vengono soddisfatte all'interno della finestra a scorrimento della prossimità, il livello di sicurezza dell'affinità è 85,6%, in base al calcolo in basso. Il risultato supera la soglia della regola dell'affinità, 65, determinando la corrispondenza della regola.

CLAffinità= 1 – \[(1 – CLEvidenza 1) X (1 – CLEvidenza 2) X (1 – CLEvidenza 2)\]

*= 1 – \[(1 – 0,6) X (1 – 0,4) X (1 – 0,4)\]*

*= 1 – (0,4 x 0,6 X 0,6)*

*= 85.6%*

![Esempio di corrispondenza della regola di affinità con probabilità elevata](images/JJ674704.e17b2e22-18c3-40c4-8f19-0993bb556675(EXCHG.150).gif "Esempio di corrispondenza della regola di affinità con probabilità elevata")

Con la stessa definizione della regola dell'esempio, se solo la prima prova corrisponde poiché la seconda prova non rientra nella finestra di prossimità, il livello di sicurezza dell'affinità più elevato è 60%, in base al calcolo in basso e la regola dell'affinità non corrisponde poiché la soglia di 65 non è stata soddisfatta.

CLAffinità= 1 – \[(1 – CLEvidenza 1) X (1 – CLEvidenza 2) X (1 – CLEvidenza 2)\]

*= 1 – \[(1 – 0,6) X (1 – 0) X (1 – 0)\]*

*= 1 – (0,4 x 1 X 1)*

*= 60%*

![Esempio di corrispondenza della regola di affinità con probabilità bassa](images/JJ674704.077095b1-6eb0-40df-b254-f33437725720(EXCHG.150).gif "Esempio di corrispondenza della regola di affinità con probabilità bassa")

## Regolazione dei livelli di sicurezza

Uno degli aspetti principali del processo di creazione della regola è la regolazione dei livelli di sicurezza per le regole dell'entità e dell'affinità. Dopo la creazione delle definizioni di regole, eseguire la regola sul contenuto rappresentativo e raccogliere i dati di accuratezza. Confrontare i risultati restituiti per ciascuno schema o prova in base ai risultati previsti per i documenti di prova.

![Tabella con confronto delle prove di corrispondenza della regola](images/JJ674704.25a7d9a1-d02f-447e-a88b-8e78bdc0413a(EXCHG.150).gif "Tabella con confronto delle prove di corrispondenza della regola")

Se le regole soddisfano i requisiti di accettazione, ossia se lo schema o la prova hanno una percentuale di sicurezza superiore alla soglia stabilita (ad esempio 75%), l'espressione di corrispondenza è completa e può essere spostata al passaggio successivo.

Se lo schema o la prova non soddisfano il livello di sicurezza, ripetere la creazione (aggiungendo ad esempio più prove convalidanti, rimuovendo o aggiungendo altri schemi/prove e così via) e ripetere il passaggio.

Quindi, regolare il livello di sicurezza per ciascuno schema o prova nelle regole basate sui risultati dal passaggio precedente. Per ciascuno schema o prova, aggregare il numero di veri positivi (TP), un sottoinsieme di documenti che contengono l'entità o l'affinità per cui la regola viene creata e che determina una corrispondenza e il numero di falsi positivi (FP), un sottoinsieme di documenti che non contengono l'entità o l'affinità per cui la regola viene creata e che hanno restituito una corrispondenza. Impostare il livello di sicurezza per ogni modello/prova mediante il seguente calcolo:

*Livello di sicurezza = veri positivi / (veri positivi + falsi positivi)*


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello o prova</th>
<th>Veri positivi</th>
<th>Falsi positivi</th>
<th>Livello di sicurezza</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>P1o E1</p></td>
<td><p>4</p></td>
<td><p>1</p></td>
<td><p>80%</p></td>
</tr>
<tr class="even">
<td><p>P2o E2</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Pno En</p></td>
<td><p>9</p></td>
<td><p>10</p></td>
<td><p>47%</p></td>
</tr>
</tbody>
</table>


## Utilizzo delle lingue locali nel file XML

Lo schema delle regole supporta l'archiviazione del nome e delle descrizione localizzati per ciascun elemento Entity e Affinity. Ciascun elemento Entity e Affinity deve contenere un elemento corrispondente nella sezione LocalizedStrings. Per localizzare ciascun elemento, includere un elemento Resource come figlio dell'elemento LocalizedStrings per archiviare nome e descrizioni per più impostazioni locali per ciascun elemento. L'elemento Resource include un attributo idRef obbligatorio che corrisponde all'attributo idRef per ciascun elemento localizzato. Gli elementi figlio Locale dell'elemento Resource contengono il nome e le descrizioni localizzati per ciascuna impostazione locale specificata.
```powershell
    <LocalizedStrings>
        <Resource idRef="guid">
            <Locale langcode="en-US" default="true"> 
                <Name>affinity name en-us</Name> 
                <Description>
                    affinity description en-us
                </Description> 
            </Locale> 
            <Locale langcode="de"> 
                <Name>affinity name de</Name> 
                <Description>
                    affinity description de
                </Description> 
            </Locale> 
        </Resource>
    </LocalizedStrings>
```
## Definizione dello schema XML per il pacchetto delle regole di classificazione
```powershell
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:mce="http://schemas.microsoft.com/office/2011/mce"
               targetNamespace="http://schemas.microsoft.com/office/2011/mce" 
               xmlns:xs="http://www.w3.org/2001/XMLSchema"
               elementFormDefault="qualified"
               attributeFormDefault="unqualified"
               id="RulePackageSchema">
      <xs:simpleType name="LangType">
        <xs:union memberTypes="xs:language">
          <xs:simpleType>
            <xs:restriction base="xs:string">
              <xs:enumeration value=""/>
            </xs:restriction>
          </xs:simpleType>
        </xs:union>
      </xs:simpleType>
      <xs:simpleType name="GuidType" final="#all">
        <xs:restriction base="xs:token">
          <xs:pattern value="[0-9a-fA-F]{8}\-([0-9a-fA-F]{4}\-){3}[0-9a-fA-F]{12}"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulePackageType">
        <xs:sequence>
          <xs:element name="RulePack" type="mce:RulePackType"/>
          <xs:element name="Rules" type="mce:RulesType">
            <xs:key name="UniqueRuleId">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueProcessorId">
              <xs:selector xpath="mce:Regex|mce:Keyword"></xs:selector>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueResourceIdRef">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:key>        
            <xs:keyref name="ReferencedRuleMustExist" refer="mce:UniqueRuleId">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:keyref>
            <xs:keyref name="RuleMustHaveResource" refer="mce:UniqueResourceIdRef">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:keyref>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="RulePackType">
        <xs:sequence>
          <xs:element name="Version" type="mce:VersionType"/>
          <xs:element name="Publisher" type="mce:PublisherType"/>
          <xs:element name="Details" type="mce:DetailsType">
            <xs:key name="UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="mce:LocalizedDetails"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:keyref name="DefaultLangCodeMustExist" refer="mce:UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="."/>
              <xs:field xpath="@defaultLangCode"/>
            </xs:keyref>
          </xs:element>
          <xs:element name="Encryption" type="mce:EncryptionType" minOccurs="0" maxOccurs="1"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="VersionType">
        <xs:attribute name="major" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="minor" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="build" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="revision" type="xs:unsignedShort" use="required"/>
      </xs:complexType>
      <xs:complexType name="PublisherType">
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="LocalizedDetailsType">
        <xs:sequence>
          <xs:element name="PublisherName" type="mce:NameType"/>
          <xs:element name="Name" type="mce:RulePackNameType"/>
          <xs:element name="Description" type="mce:OptionalNameType"/>
        </xs:sequence>
        <xs:attribute name="langcode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="DetailsType">
        <xs:sequence>
          <xs:element name="LocalizedDetails" type="mce:LocalizedDetailsType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="defaultLangCode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="EncryptionType">
        <xs:sequence>
          <xs:element name="Key" type="xs:normalizedString"/>
          <xs:element name="IV" type="xs:normalizedString"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="RulePackNameType">
        <xs:restriction base="xs:token">
          <xs:minLength value="1"/>
          <xs:maxLength value="64"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="NameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="1"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="OptionalNameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="0"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="RestrictedTermType">
        <xs:restriction base="xs:string">
          <xs:minLength value="1"/>
          <xs:maxLength value="512"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulesType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Entity" type="mce:EntityType"/>
            <xs:element name="Affinity" type="mce:AffinityType"/>
          </xs:choice>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Regex" type="mce:RegexType"/>
            <xs:element name="Keyword" type="mce:KeywordType"/>
          </xs:choice>
          <xs:element name="LocalizedStrings" type="mce:LocalizedStringsType"/>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="EntityType">
        <xs:sequence>
          <xs:element name="Pattern" type="mce:PatternType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="patternsProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="recommendedConfidence" type="mce:ProbabilityType"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="PatternType">
        <xs:sequence>
          <xs:element name="IdMatch" type="mce:IdMatchType"/>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="AffinityType">
        <xs:sequence>
          <xs:element name="Evidence" type="mce:EvidenceType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="evidencesProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="thresholdConfidenceLevel" type="mce:ProbabilityType" use="required"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="EvidenceType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="IdMatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="MatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="AnyType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="minMatches" type="xs:nonNegativeInteger" default="1"/>
        <xs:attribute name="maxMatches" type="xs:nonNegativeInteger" use="optional"/>
      </xs:complexType>
      <xs:simpleType name="ProximityType">
        <xs:restriction base="xs:positiveInteger">
          <xs:minInclusive value="1"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="ProbabilityType">
        <xs:restriction base="xs:integer">
          <xs:minInclusive value="1"/>
          <xs:maxInclusive value="100"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="WorkloadType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Exchange"/>
          <xs:enumeration value="Outlook"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RegexType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="id" type="xs:token" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="KeywordType">
        <xs:sequence>
          <xs:element name="Group" type="mce:GroupType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="xs:token" use="required"/>
      </xs:complexType>
      <xs:complexType name="GroupType">
        <xs:sequence>
          <xs:choice>
            <xs:element name="Term" type="mce:TermType" maxOccurs="unbounded"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="matchStyle" default="word">
          <xs:simpleType>
            <xs:restriction base="xs:NMTOKEN">
              <xs:enumeration value="word"/>
              <xs:enumeration value="string"/>
            </xs:restriction>
          </xs:simpleType>
        </xs:attribute>
      </xs:complexType>
      <xs:complexType name="TermType">
        <xs:simpleContent>
          <xs:extension base="mce:RestrictedTermType">
            <xs:attribute name="caseSensitive" type="xs:boolean" default="false"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="LocalizedStringsType">
        <xs:sequence>
          <xs:element name="Resource" type="mce:ResourceType" maxOccurs="unbounded">
            <xs:key name="UniqueLangCodeUsedInNamePerResource">
              <xs:selector xpath="mce:Name"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:key name="UniqueLangCodeUsedInDescriptionPerResource">
              <xs:selector xpath="mce:Description"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="ResourceType">
        <xs:sequence>
          <xs:element name="Name" type="mce:ResourceNameType" maxOccurs="unbounded"/>
          <xs:element name="Description" type="mce:DescriptionType" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="idRef" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="ResourceNameType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="DescriptionType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
    </xs:schema>
```
## Ulteriori informazioni

[Prevenzione della perdita di dati](https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Definire modelli DLP e tipi di informazione propri](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

