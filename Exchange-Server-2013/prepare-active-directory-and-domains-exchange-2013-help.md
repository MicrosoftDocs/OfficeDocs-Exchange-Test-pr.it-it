---
title: 'Preparazione di Active Directory e dei domini: Exchange 2013 Help'
TOCTitle: Preparazione di Active Directory e dei domini
ms:assetid: f895e1ce-d766-4352-ac46-ec959c9954a9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125224(v=EXCHG.150)
ms:contentKeyID: 50482057
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Preparazione di Active Directory e dei domini

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Prima di installare Microsoft Exchange Server 2013, è necessario preparare la foresta Active Directory e i relativi domini. Per Exchange è necessario preparare Active Directory in modo da poter archiviare le informazioni sulle cassette postali degli utenti e la configurazione dei server Exchange nell'organizzazione. Se non si ha dimestichezza con le foreste e i domini Active Directory, controllare [Panoramica di Servizi di domino Active Directory](https://go.microsoft.com/fwlink/p/?linkid=399226).


> [!NOTE]
> Se si tratta della prima installazione di Exchange nell'ambiente in uso o si dispone già delle versioni precedenti di Exchange Server, è necessario predisporre Active Directory per Exchange 2013. È possibile vedere <A href="exchange-2013-active-directory-schema-changes-exchange-2013-help.md">Modifiche allo schema di Active Directory in Exchange 2013</A> per informazioni dettagliate sulle nuove classi e sui nuovi attributi dello che Exchange 2013 aggiunge ad Active Directory, inclusi quelli forniti con i Service Pack e con gli aggiornamenti cumulativi (CU).



Esistono due modi per preparare Active Directory per Exchange. Il primo consiste nell'utilizzo della procedura guidata di installazione di Exchange 2013 che esegue l'operazione automaticamente. Se la distribuzione di Active Directory è ridotta, e non si dispone di un team separato che gestisce Active Directory, è consigliabile utilizzare la procedura guidata. L'account utilizzato dovrà essere un membro dei gruppi di protezione Schema Admins ed Enterprise Admins. Per ulteriori informazioni su come utilizzare l'installazione guidata, controllare [Installazione di Exchange 2013 utilizzando l'installazione guidata](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).

In caso di distribuzione di Active Directory a livello più ampio, o se Active Directory è gestito da un team a parte, fare riferimento a questo argomento. La procedura fornita in questo argomento fornisce maggiore controllo su ciascuna fase della preparazione e su quali utenti possono eseguire ciascun passaggio. Ad esempio, è possibile che gli amministratori di Exchange non dispongano delle autorizzazioni necessarie per estendere lo schema Active Directory.

Che cosa è necessario sapere prima di iniziare

1\. Estendere lo schema di Active Directory

2\. Preparazione di Active Directory

3\. Preparazione dei domini Active Directory

Come verificare se l'operazione ha avuto esito positivo

Preparazione di Active Directory per Exchange Vedere [Modifiche in Active Directory con l'installazione di Exchange 2013](what-changes-in-active-directory-when-exchange-2013-is-installed-exchange-2013-help.md)

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Almeno 10-15 minuti (senza includere la replica di Active Directory), in base alle dimensioni dell'organizzazione e al numero di domini figlio.

  - Il computer utilizzato per eseguire questi passaggi deve soddisfare i [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md). Inoltre, la foresta di Active Directory deve soddisfare i requisiti indicati nella sezione "Server di rete e di directory" in [Requisiti di sistema di Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md).

  - Se l'organizzazione dispone di più domini Active Directory, si consiglia quanto segue:
    
      - Eseguire i comandi indicati di seguito da un sito Active Directory con un server Active Directory da ogni dominio.
    
      - Installare il primo server Exchange in un sito Active Directory con un server di catalogo globale scrivibile da ogni dominio.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 1\. Estendere lo schema di Active Directory

Il primo passaggio per preparare l'organizzazione a Exchange 2013 consiste nell'estendere lo schema di Active Directory. Exchange consente di archiviare una grande quantità di informazioni in Active Directory ma per poterlo fare, deve aggiungere e aggiornare classi, attributi, e altri elementi. Se si desidera conoscere quali sono le modifiche apportate durante l'estensione dello schema, vedere [Modifiche allo schema di Active Directory in Exchange 2013](exchange-2013-active-directory-schema-changes-exchange-2013-help.md).

Prima di estendere lo schema, esistono alcuni aspetti da tenere presenti:

  - L'account utilizzato per l'accesso dovrà essere un membro dei gruppi di protezione Schema Admins ed Enterprise Admins.

  - Il computer utilizzato per eseguire il comando per estendere lo schema deve trovarsi nello stesso dominio Active Directory e sito del master schema.

  - Se si utilizza il parametro *DomainController*, accertarsi di utilizzare il nome del controller di dominio master schema.

  - L'unico modo per estendere lo schema per Exchange consiste nell'utilizzare la procedura fornita in questo argomento oppure l'installazione di Exchange 2013. Non sono supportati altri modi di estensione dello schema.


> [!TIP]
> Se non si dispone di un team distinto che gestisce lo schema Active Directory, è possibile ignorare questo passaggio e andare direttamente al Preparazione di Active Directory. Se lo schema non viene esteso nel passaggio 1, i comandi del passaggio 2 consentiranno l'estensione automatica dello schema. Se si decide di ignorare il passaggio 1, si applicano le informazioni da tenere presenti fornite in precedenza.



Quando si è pronti, effettuare le seguenti operazioni per estendere lo schema Active Directory. Se si dispone di più foreste Active Directory, assicurarsi di aver effettuato l'accesso alla foresta giusta.

1.  Assicurarsi che il computer sia pronto per l'esecuzione dell'installazione di Exchange 2013. Per conoscere i requisiti necessari per l'installazione, vedere la sezione [Active Directory preparation](exchange-2013-prerequisites-exchange-2013-help.md) in [Prerequisiti di Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2.  Aprire una finestra di prompt dei comandi Windows e accedere alla posizione in cui sono stati scaricati i file di installazione di Exchange.

3.  Eseguire il seguente comando per estendere lo schema:
    
        Setup.exe /PrepareSchema /IAcceptExchangeServerLicenseTerms

Quando l'installazione ha completato l'estensione dello schema, sarà necessario attendere che Active Directory replichi le modifiche a tutti i controller di dominio. Se si desidera controllare il processo di replica, è possibile utilizzare lo strumento `repadmin`. `Repadmin` è incluso come parte della funzionalità Strumenti per Servizi di dominio Active Directory in Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2. Per ulteriori informazioni sull'utilizzo di questo strumento, vedere [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879).

## 2\. Preparazione di Active Directory

Una volta esteso lo schema Active Directory, è possibile preparare le altre parti di Active Directory per Exchange 2013. Durante questo passaggio, tramite Exchange verranno creati contenitori, oggetti e altri elementi in Active Directory che saranno utilizzati per archiviare le informazioni. L'insieme di tutti i contenitori, oggetti, attributi e altri elementi di Exchange è denominato *organizzazione di Exchange*.

Prima di preparare Active Directory per Exchange, esistono alcuni aspetti da tenere presenti:

  - L'account utilizzato per l'accesso deve essere un membro del gruppo di protezione Enterprise Admins. Se è stata ignorata la fase 1 poiché si desidera estendere lo schema con il comando *PrepareAD*, l'account utilizzato deve essere anche membro del gruppo di protezione Schema Admins.

  - Il computer utilizzato per eseguire il comando deve trovarsi nello stesso dominio Active Directory e sito del master schema. Sarà inoltre necessario contattare tutti i domini della foresta sulla porta TCP 389.

  - Prima di eseguire questo passaggio, attendere che le modifiche eseguite nel passaggio 1 siano state replicate a tutti i controller di dominio tramite Active Directory.

Quando si esegue il comando di seguito per preparare Active Directory per Exchange, è necessario dare un nome all'organizzazione di Exchange. Questo nome viene utilizzato internamente da Exchange e in genere non è visibile agli utenti. Spesso, il nome utilizzato per l'organizzazione è il nome della società in cui viene installato Exchange. Il nome utilizzato non influisce sulla funzionalità di Exchange e non determina le scelte degli indirizzi di posta elettronica. È possibile utilizzare qualsiasi nome, se si tiene presente quanto indicato di seguito:

  - È possibile utilizzare tutte lettere maiuscole o minuscole dalla A alla Z.

  - È possibile utilizzare i numeri da 0 a 9.

  - Il nome può contenere degli spazi purché non si trovino all'inizio e alla fine.

  - È possibile utilizzare un trattino o una lineetta nel nome.

  - Il nome può contenere un massimo di 64 caratteri, ma non può essere vuoto.

  - Il nome non può essere modificato una volta impostato.

Quando si è pronti, effettuare le seguenti operazioni per preparare Active Directory per Exchange. Se il nome dell'organizzazione che si desidera utilizzare contiene degli spazi, racchiuderlo tra virgolette (").

1.  Aprire una finestra di prompt dei comandi Windows e accedere alla posizione in cui sono stati scaricati i file di installazione di Exchange.

2.  Eseguire il comando riportato di seguito:
    
        Setup.exe /PrepareAD /OrganizationName:"<organization name>" /IAcceptExchangeServerLicenseTerms

Dopo che l'installazione ha completato la preparazione di Active Directory per Exchange, sarà necessario attendere che le modifiche vengano replicate a tutti i controller di dominio tramite Active Directory. Se si desidera controllare il processo di replica, è possibile utilizzare lo strumento `repadmin`. `repadmin` è incluso come parte della funzionalità Strumenti per Servizi di dominio Active Directory in Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2. Per ulteriori informazioni sull'utilizzo di questo strumento, vedere [Repadmin](https://go.microsoft.com/fwlink/p/?linkid=257879).

## 3\. Preparazione dei domini Active Directory

Il passaggio finale per approntare Active Directory per Exchange consiste nel preparare ciascuno dei domini Active Directory in cui sarà installato Exchange o nei quali saranno collocati gli utenti abilitati alla posta elettronica. Questo passaggio consente la creazione di contenitori e gruppi di sicurezza aggiuntivi, e l'impostazione di autorizzazioni che consentano l'accesso da parte di Exchange.

Se si dispone di più domini nella foresta Active Directory, è possibile prepararli in due modi. Selezionare l'opzione che corrisponde maggiormente all'operazione che si desidera eseguire. Se si dispone di un solo dominio, è possibile ignorare questo passaggio perché il dominio è stato già preparato utilizzando il comando *PrepareAD* nel passaggio 2.

## Preparare tutti i domini nella foresta di Active Directory

Per preparare tutti i domini di Active Directory, è possibile utilizzare il parametro *PrepareAllDomains* quando si esegue l'installazione. Con l'installazione, tutti i domini Exchange nella foresta Active Directory verranno preparati automaticamente.

Prima di preparare tutti i domini della foresta Active Directory, tenere presente quanto segue:

  - L'account utilizzato deve essere un membro del gruppo di protezione Enterprise Admins.

  - Attendere che le modifiche eseguite nel passaggio 2 siano state replicate a tutti i controller di dominio tramite Active Directory. In caso contrario, è possibile che si verifichi un errore quando si tenta di preparare il dominio.

Una volta pronti, eseguire la procedura indicata di seguito per preparare tutti i domini della foresta Active Directory per Exchange.

1.  Aprire una finestra di prompt dei comandi Windows e accedere alla posizione in cui sono stati scaricati i file di installazione di Exchange.

2.  Eseguire il comando riportato di seguito:
    
        Setup.exe /PrepareAllDomains /IAcceptExchangeServerLicenseTerms

## Scelta dei domini di Active Directory che desidera preparare

Se si desidera scegliere quali domini Active Directory preparare, è possibile utilizzare il parametro *PrepareDomain* quando si esegue l'installazione. Se si utilizza il parametro *PrepareDomain*, è necessario includere il nome di dominio completo (FQDN) del dominio che si desidera preparare.

Prima di preparare i domini della foresta Active Directory, tenere presente quanto segue:

  - L'account utilizzato necessita di autorizzazioni in base al momento in cui è stato creato il dominio.
    
      - **Dominio creato prima dell'esecuzione di PrepareAD**   Se il dominio è stato creato **prima** dell'esecuzione del comando *PrepareAD* nel passaggio 2 precedente, l'account utilizzato deve essere un membro del gruppo Domain Admins nel dominio che si desidera preparare.
    
      - **Dominio creato dopo l'esecuzione di PrepareAD**   Se il dominio è stato creato **prima** dell'esecuzione del comando *PrepareAD* nel passaggio 2 precedente, l'account utilizzato deve 1) essere un membro del gruppo di ruoli Gestione organizzazione 2) essere membro del gruppo Domain Admins nel dominio che si desidera preparare.

  - Attendere che le modifiche eseguite nel passaggio 2 siano state replicate a tutti i controller di dominio tramite Active Directory. In caso contrario, è possibile che si verifichi un errore quando si tenta di preparare il dominio.

  - È necessario preparare tutti i domini in cui verrà installato un server Exchange. Sarà inoltre necessario preparare qualsiasi dominio conterrà utenti abilitati alla posta elettronica, persino se questi domini non conterranno alcun server Exchange.

  - Non è necessario eseguire il comando *PrepareDomain* nel dominio in cui è stato eseguito il comando *PrepareAD*. Il comando *PrepareAD* prepara automaticamente tale dominio.

Una volta pronti, eseguire la procedura indicata di seguito per preparare un singolo dominio della foresta Active Directory per Exchange.

1.  Aprire una finestra di prompt dei comandi Windows e accedere alla posizione in cui sono stati scaricati i file di installazione di Exchange.

2.  Eseguire il comando riportato di seguito. Includere il nome FQDN del dominio che si desidera preparare. Se si desidera preparare il dominio in cui si esegue il comando, non è necessario includere il nome FQDN.
    
        Setup.exe /PrepareDomain:<FQDN of the domain you want to prepare> /IAcceptExchangeServerLicenseTerms

3.  Ripetere i passaggi per ciascun dominio Active Directory in cui si installerà un server Exchange oppure in cui verranno collocati gli utenti abilitati alla posta elettronica.

## Come verificare se l'operazione ha avuto esito positivo

Dopo aver eseguito tutti i passaggi precedenti, è possibile verificare che tutte le operazioni siano state eseguite correttamente. A tale scopo, si utilizzerà uno strumento denominato Active Directory Service Interfaces Editor (ADSI Edit). ADSI Edit è incluso come parte della funzionalità Strumenti per Servizi di dominio di Active Directory in Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2. Per ulteriori informazioni su ADSI Edit, vedere [ADSI Edit (adsiedit.msc)](https://go.microsoft.com/fwlink/p/?linkid=294644).


> [!WARNING]
> Non modificare mai i valori in ADSI Edit, a meno che non sia indicato dal supporto tecnico Microsoft. La modifica dei valori in ADSI Edit può danneggiare in modo irreparabile l'organizzazione Exchange e Active Directory.



Dopo che Exchange ha esteso lo schema Active Directory e prepara Active Directory per Exchange, vengono aggiornate alcune proprietà che confermano il completamento dell'aggiornamento. Utilizzare le informazioni nell'elenco seguente per accertarsi che i valori di queste proprietà sono corretti. Ogni proprietà deve corrispondere al valore (riportato nella tabella) relativo alla versione di Exchange 2013 che si sta installando.

  - Nel contesto dei nomi **Schema**, verificare che la proprietà **rangeUpper** in **ms-Exch-Schema-Verision-Pt** sia impostata sul valore visualizzato per la versione di Exchange 2013 in uso nella tabella in Versioni di Active Directory di Exchange 2013.
    
     

  - Nel contesto dei nomi **Configurazione**, verificare che la proprietà **objectVersion** nel contenitore CN=\<*organizzazione*\>, in CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*dominio*\> sia impostata sul valore visualizzato per la versione di Exchange 2013 uso, nella tabella Versioni di Active Directory di Exchange 2013.
    
     

  - Nel contesto dei nomi **Predefinito**, verificare che la proprietà **objectVersion** nel contenitore **Oggetti di sistema di Microsoft Exchange** in DC=\<*dominio radice* sia impostata sul valore visualizzato per la versione di Exchange 2013 in uso, nella tabella in Versioni di Active Directory di Exchange 2013.
    
     

È anche possibile controllare il log dell'installazione di Exchange per verificare che preparazione di Active Directory sia stata completata correttamente. Per ulteriori informazioni, vedere [Verificare un'installazione di Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md). Non sarà possibile utilizzare il cmdlet **Get-ExchangeServer** indicato nell'argomento [Verificare un'installazione di Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md) fino al completamento dell'installazione di almeno un ruolo del server Cassette postali e di un ruolo server Accesso client in un sito Active Directory.

## Versioni di Active Directory di Exchange 2013

Nella tabella seguente vengono mostrati gli oggetti di Exchange 2013 di Active Directory che vengono aggiornati ogni volta che si installa una nuova versione di Exchange 2013. Per verificare che durante l'installazione di Exchange 2013 sia stato effettuato l'aggiornamento di Active Directory, è possibile confrontare le versioni degli oggetti con i valori forniti nella tabella di seguito.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Versione di Exchange</th>
<th>rangeUpper</th>
<th>objectVersion</th>
<th>objectVersion</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Contesto dei nomi</strong></p></td>
<td><p> </p></td>
<td><p>Schema</p></td>
<td><p>Default</p></td>
<td><p>Configuration</p></td>
</tr>
<tr class="even">
<td><p><strong>Container</strong></p></td>
<td><p> </p></td>
<td><p>ms-Exch-Schema-Version-Pt</p></td>
<td><p>Oggetti di sistema di Microsoft Exchange</p></td>
<td><p>CN=&lt;<em>your organization</em>&gt;, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=&lt;<em>domain</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU10 e versioni successive</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>16130</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU9</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU8</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 CU7</p></td>
<td><p>15312</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2013 CU6</p></td>
<td><p>15303</p></td>
<td><p>13236</p></td>
<td><p>15965</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU5</p></td>
<td><p>15300</p></td>
<td><p>13236</p></td>
<td><p>15870</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 SP1</p></td>
<td><p>15292</p></td>
<td><p>13236</p></td>
<td><p>15844</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU3</p></td>
<td><p>15283</p></td>
<td><p>13236</p></td>
<td><p>15763</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 CU2</p></td>
<td><p>15281</p></td>
<td><p>13236</p></td>
<td><p>15688</p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Exchange 2013 CU1</p></td>
<td><p>15254</p></td>
<td><p>13236</p></td>
<td><p>15614</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Exchange 2013 RTM</p></td>
<td><p>15137</p></td>
<td><p>13236</p></td>
<td><p>15449</p></td>
</tr>
</tbody>
</table>

