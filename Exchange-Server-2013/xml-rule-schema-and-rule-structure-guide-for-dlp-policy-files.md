---
title: 'Sviluppo di file modello per il criterio DLP: Exchange 2013 Help'
TOCTitle: Sviluppo di file modello per il criterio DLP
ms:assetid: 4b263547-aef4-4ee8-aa4f-fa64a5863189
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ674703(v=EXCHG.150)
ms:contentKeyID: 50480613
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Sviluppo di file modello per il criterio DLP

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Nella seguente panoramica, vengono illustrati i componenti di una definizione dello schema XML per i file modello del criterio di prevenzione della perdita di dati (DLP) e viene fornito anche un file di criteri di esempio in formato XML. Sarà utile comprendere l'architettura DLP generale e il processo di sviluppo delle regole prima di iniziare. Per ulteriori informazioni, vedere [Prevenzione della perdita di dati](https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention) e [Definire modelli DLP e tipi di informazione propri](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md).

Per semplificare l'uso e la gestione delle soluzioni per la prevenzione della perdita di dati, in Exchange Server 2013 viene introdotto un modello concettuale noto come criteri DLP e modello di criteri. I modelli di criteri DLP offrono una struttura preliminare del criterio DLP desiderato. Affinché possa essere valutato, un modello di criterio DLP deve incapsulare tutte le direttive e gli oggetti dati richiesti per soddisfare un determinato obiettivo per i criteri, quale una normativa o un'esigenza aziendale. Il modello non è specifico dell'ambiente. Si tratta, semplicemente, di una definizione o modello di un criterio che può essere fornito come parte della configurazione del prodotto o distribuito da partner e rivenditori di software indipendenti. Al contrario, i criteri DLP sono installazioni di runtime dei modelli specifici dell'ambiente di distribuzione. Il framework dei criteri di messaggistica esistente può incorporare criteri DLP tramite l'uso di regole di trasporto. Le regole di trasporto forniscono una notevole flessibilità nell'adattamento e nella definizione della ricchezza delle soluzioni DLP.

## Struttura e origini dei modelli di criteri

I modelli di criteri DLP sono, generalmente, influenzati da più origini, quali direttive di elaborazione basate sul server, criteri dei computer client o altri costrutti di criteri, come illustrato nell'immagine seguente:

![Fattori che influiscono sui modelli di criteri](images/JJ674703.12f48e4f-d7b8-4ddd-87e8-8477983252ec(EXCHG.150).gif "Fattori che influiscono sui modelli di criteri")

Per i modelli di criteri DLP, sono disponibili semplici operazioni di gestione sia su Exchange Management Shell sia su interfacce basate su Internet, quali l'Interfaccia di amministrazione di Exchange, che includono funzionalità di importazione, esportazione, eliminazione e realizzazione di query. Un criterio DLP viene creato facendo riferimento a un modello di criteri DLP come parte del processo di creazione. Tali modelli di criteri DLP possono fare riferimento ai criteri installati nel sistema, che sono archiviati nei servizi di dominio di Active Directory, oppure essere forniti direttamente come input da criteri forniti esternamente.

I modelli di criteri DLP sono rappresentati come documenti XML. Un singolo schema XML viene utilizzato anche per i criteri forniti all'interno e all'esterno di Exchange. La struttura concettuale del documento XML viene rappresentata nella tabella seguente, che mostra gli elementi principali. L'insieme delle definizioni dei componenti dei criteri consente di raggiungere più facilmente un determinato obiettivo per i criteri, quale una normativa o esigenza aziendale.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento strutturale</th>
<th>Significato o esempio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autore</p></td>
<td><p>Microsoft o Partner</p></td>
</tr>
<tr class="even">
<td><p>Versione</p></td>
<td><p>15.0.1.0</p></td>
</tr>
<tr class="odd">
<td><p>Nome criterio</p></td>
<td><p>PCI-DSS</p></td>
</tr>
<tr class="even">
<td><p>Descrizione</p></td>
<td><p>Il criterio DLP PCI-DSS consente di rilevare la presenza di informazioni sono soggette a PCI Data Security Standard (PCI DSS), incluse le informazioni su come carta di credito o numeri di carta di debito. Utilizzo di questo criterio non garantire la conformità alle normative. Al termine del test, apportare le modifiche di configurazione necessarie di Exchange in modo che la trasmissione di informazioni è conforme ai criteri dell'organizzazione. Ad esempio configurare TLS con i partner commerciali noti o aggiunta di azioni delle regole trasporto più restrittive, ad esempio l'aggiunta di protezione dei diritti per i messaggi che contengono questo tipo di dati.</p></td>
</tr>
<tr class="odd">
<td><p>Metadati</p></td>
<td><p>Tag per descrivere la normativa locale, il paese o la regione, le parole chiavi e altro ancora.</p></td>
</tr>
<tr class="even">
<td><p>Insieme di costrutti di criteri</p></td>
<td><ol>
<li><p>Definizioni delle regole di trasporto, quali condizioni e azioni.</p></li>
<li><p>Definizioni del comportamento client di posta elettronica che controllano le prestazioni dei client tramite notifiche interattive.</p></li>
<li><p>Facoltativamente, riferimenti di configurazione che devono essere coordinati con impostazioni client specifiche dell'ambiente.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Insieme di classificazioni dei dati</p></td>
<td><ol>
<li><p>Indica le affinità ed entità delle classificazioni.</p></li>
<li><p>Le entità dispongono di un conteggio e una probabilità, le affinità solo di una probabilità.</p></li>
<li><p>È dotato di una propria serie di schemi di classificazione e proprietà.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## Definizione del formato dei modelli di criteri

I modelli di criteri DLP sono rappresentati come documenti XML che aderiscono al seguente schema. L'XML distingue tra maiuscole e minuscole. Ad esempio, `dlpPolicyTemplates` funzionerà, al contrario di `DlpPolicyTemplates`.

    <?xml version="1.0" encoding="UTF-8"?>
    <dlpPolicyTemplates>
      <dlpPolicyTemplate id="F7C29AEC-A52D-4502-9670-141424A83FAB" mode="Audit" state="Enabled" version="15.0.2.0">
        <contentVersion>4</contentVersion>
        <publisherName>Microsoft</publisherName>
        <name>
          <localizedString lang="en">PCI-DSS</localizedString>
        </name>
        <description>
          <localizedString lang="en">Detects the presence of information subject to Payment Card Industry Data Security Standard (PCI-DSS) compliance requirements.</localizedString>
        </description>
        <keywords></keywords>
        <ruleParameters></ruleParameters>
        <ruleParameters/>
        <policyCommands>
          <!-- The contents below are applied/executed as rules directly in PS - -->
          <commandBlock>
            <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP Policy."]]>
          </commandBlock>
          <commandBlock>
            <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "%%DlpPolicyName%%" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP Policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]>
          </commandBlock>
        </policyCommands>
        <policyCommandsResources></policyCommandsResources>
      </dlpPolicyTemplate>
    </dlpPolicyTemplates>

Se un elemento nel parametro incluso nel file XML include uno spazio, il parametro deve essere messo tra virgolette, altrimenti non funzionerà. Nell'esempio riportato di seguito, il parametro che segue `-SentToScope` è accettabile e non include le virgolette perché è una stringa di caratteri continua senza spazi. Tuttavia, il parametro fornito per `Comments`, non verrà visualizzato nell'interfaccia di amministrazione di Exchange perché include spazi e non sono presenti virgolette.

    <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments Monitors payment card information sent inside the organization -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>

## Elemento LocalizedString

Il formato del modello offre la possibilità di individuare stringhe nel modello che potrebbero essere presentate all'utente finale come parte, ad esempio, della selezione dei tipi di modelli di criteri DLP installati. L'elemento LocalizedString può essere utilizzato per fornire più definizioni per i campi Nome e Descrizione.

## Nodo RuleParameters

Si tratta di una serie di parametri opzionali che devono essere forniti durante la fase di installazione dei modelli al momento della creazione di un criterio DLP per la mappatura di determinati oggetti di distribuzione. Ad esempio ,un gruppo di distribuzione effettiva disponibile nella distribuzione.

## Elemento DlpPolicyTemplate

Si tratta dell'elemento radice per il modello di criteri DLP ed è obbligatorio per tutti i modelli. Nella tabella seguente, sono elencati gli attributi disponibili:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome attributo</th>
<th>Obbligatorio?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Versione</p></td>
<td><p>Sì</p></td>
<td><p>La versione numero utilizzata in questo documento di modelli di criteri DLP.</p></td>
</tr>
<tr class="even">
<td><p>Stato</p></td>
<td><p>No</p></td>
<td><p>Configurazione predefinita opzionale per lo stato del criterio.</p></td>
</tr>
<tr class="odd">
<td><p>Modalità</p></td>
<td><p>No</p></td>
<td><p>Configurazione predefinita opzionale per la modalità del criterio.</p></td>
</tr>
<tr class="even">
<td><p>Id</p></td>
<td><p>No</p></td>
<td><p>Un GUID per identificare in modo univoco tale definizione del modello di criteri DLP nel seguente formato:&quot;A29C69BF-4F98-47F1-9A99-5771DFD2C27F&quot;.</p></td>
</tr>
</tbody>
</table>


Gli elementi figlio includono la seguente sequenza di elementi.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento figlio</th>
<th>(minimo, massimo)</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PublisherName</p></td>
<td><p>(1, 1)</p></td>
<td><p>Metadati per l'autore del modello</p></td>
</tr>
<tr class="even">
<td><p>Nome</p></td>
<td><p>(1, 1)</p></td>
<td><p>Nome localizzabile nome per questo modello.</p></td>
</tr>
<tr class="odd">
<td><p>Descrizione</p></td>
<td><p>(1, 1)</p></td>
<td><p>Descrizione localizzabile per questo modello.</p></td>
</tr>
<tr class="even">
<td><p>Parole chiave</p></td>
<td><p>(1, 1)</p></td>
<td><p>Elenco di parole chiave applicabile a questo modello. Un modello può avere un elenco di parole chiave vuoto.</p></td>
</tr>
<tr class="odd">
<td><p>RuleParameters</p></td>
<td><p>(0, 1)</p></td>
<td><p>Elenco di parametri di modello utilizzati nella definizione del criterio.</p></td>
</tr>
<tr class="even">
<td><p>PolicyCommands</p></td>
<td><p>(0, 1)</p></td>
<td><p>Elenco di definizioni delle regole di trasporto per questo criterio. Si tratta di un elemento opzionale.</p></td>
</tr>
</tbody>
</table>


## Modello di criteri DLP: PolicyCommands

Questa parte del modello di criteri contiene l'elenco dei comandi di Exchange Management Shell utilizzati per creare un'istanza della definizione dei criteri. Il processo di importazione eseguirà tutti i comandi come parte del processo di creazione dell'istanza. Comandi di criteri di esempio vengono forniti qui.

    <PolicyCommands>
        <!-- The contents below are applied/executed as rules directly in PS - -->
          <CommandBlock> <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "PCI-DSS" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP policy."]]></CommandBlock>
          <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
      </PolicyCommands> 

Il formato dei cmdlet è la sintassi dei cmdlet di Exchange Management Shell standard per i cmdlet utilizzati. I comandi vengono eseguiti in sequenza. Tutti i nodi dei comandi possono contenere un blocco di script che sarebbe composto da più comandi. Di seguito, è riportato un esempio che spiega come incorporare il pacchetto di regole di classificazione all'interno di un modello di criteri DLP, installando il pacchetto di regole come parte del processo di creazione dei criteri. Il pacchetto di regole di classificazione viene incorporato nel modello di criteri e, quindi, passato come parametro al cmdlet all'interno del modello:

``` 
<CommandBlock>
  <![CDATA[
$rulePack = [system.Text.Encoding]::Unicode.GetBytes('<?xml version="1.0" encoding="utf-16"?>
<rulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">

  <RulePack id="c3f021a3-c265-4dc2-b3a7-41a1800bf518">
    <Version major="1" minor="0" build="0" revision="0"/>
    <Publisher id="e17451d3-9648-4117-a0b1-493a6d5c73ad"/>
    <Details defaultLangCode="en-us">
      <LocalizedDetails langcode="en-us">
        <PublisherName>Contoso</PublisherName>
        <Name>Contoso Sample Rule Pack</Name>
        <Description>This is a sample rule package</Description>
      </LocalizedDetails>
    </Details>
  </RulePack>

  <Rules>
    <Entity id="7cc35258-6b35-4415-baff-a76d1a018980" patternsProximity="300" recommendedConfidence="85" workload="Exchange">     

      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_Contoso" />
        <Any minMatches="1">
          <Match idRef="Regex_conf" />
        </Any>
      </Pattern>
    </Entity>

    <Regex id="Regex_Contoso">(?i)(\bContoso\b)</Regex>
    <Regex id="Regex_conf">(?i)(\bConfidential\b)</Regex>

    <LocalizedStrings>
      <Resource idRef="7cc35258-6b35-4415-baff-a76d1a018980">
        <Name default="true" langcode="en-us">
          Confidential Information Rule
        </Name>
        <Description default="true" langcode="en-us">
          Sample rule pack - Detects Contoso confidential information
        </Description>
      </Resource>
    </LocalizedStrings>
  </Rules>

</RulePackage>

')


New-ClassificationRuleCollection -FileData $rulePack 
New-TransportRule -name "customEntity" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -MessageContainsDataClassifications @{Name="Confidential Information Rule"} -SetAuditSeverity High]]>
</CommandBlock> 
```

Gli elementi figlio includono la seguente sequenza ordinata di elementi.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Elemento figlio</th>
<th>(minimo, massimo)</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CommandBlock</p></td>
<td><p>(1, n)</p></td>
<td><p>Un blocco di comandi eseguito in PowerShell. I blocchi di comandi vengono eseguiti in sequenza.</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

[Prevenzione della perdita di dati](https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)

[Definire modelli DLP e tipi di informazione propri](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[Importare un modello di criteri DLP personalizzato da un file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

