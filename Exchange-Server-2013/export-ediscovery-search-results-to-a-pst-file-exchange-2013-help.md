---
title: 'Esportazione dei risultati della ricerca eDiscovery in un file PST: Exchange 2013 Help'
TOCTitle: Esportazione dei risultati della ricerca eDiscovery in un file PST
ms:assetid: bc47f5f9-d056-4b69-b669-ae65fad541c8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn440164(v=EXCHG.150)
ms:contentKeyID: 59634512
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Esportazione dei risultati della ricerca eDiscovery in un file PST

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-09-07_

Lo strumento eDiscovery Export disponibile nell'Interfaccia di amministrazione di Exchange (EAC) consente di esportare i risultati di una ricerca eDiscovery in locale in un file di dati di Outlook, denominato anche file PST. Gli amministratori possono distribuire i risultati della ricerca ad altri utenti all'interno dell'organizzazione, ad esempio un responsabile delle risorse umane, un gestore dei record oppure, in una controversia legale, alla controparte. Dopo aver esportato i risultati di una ricerca in un file PST, l'utente o altri possono aprirli in Outlook per visualizzare o stampare i messaggi restituiti in tali risultati. È possibile aprire i file PST anche in applicazioni eDiscovery e di reporting di terze parti. In questo argomento viene descritto come è possibile eseguire tali operazioni, oltre a come risolvere eventuali problemi riscontrati.

## Informazioni preliminari

  - Tempo stimato per il completamento: Il tempo necessario varia in base al numero e alle dimensioni dei risultati di ricerca da esportare.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "eDiscovery sul posto" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Il computer utilizzato per esportare i risultati della ricerca in un file PST deve soddisfare i seguenti requisiti di sistema:
    
      - Windows 7 a 32 o 64 bit e versioni successive
    
      - Microsoft .NET Framework 4.7
    
      - Browser supportato:
        
          - Internet Explorer 10 e versioni successive
            
            OPPURE
        
          - Mozilla Firefox o Google Chrome. Se è in uso uno di questi browser, accertarsi di installare l'estensione *ClickOnce*. Per installare il componente aggiuntivo ClickOnce, vedere la pagina relativa ai [componenti aggiuntivi Mozilla ClickOnce](https://addons.mozilla.org/it-it/firefox/search/?q=clickonce%26cat=1%2c0%26appver=%26platform=) o a [ClickOnce per Google Chrome](https://chrome.google.com/webstore/search/clickonce?_category=extensions).

  - È necessaria una cassetta postale attiva associata all'account da esportare.

  - Verificare che le impostazioni Intranet locali siano configurate correttamente in Internet Explorer. Verificare che **https://\*.outlook.com** sia aggiunto alla zona Intranet locale.

  - Verificare che i seguenti URL non siano elencati nella zona dei siti attendibili:
    
      - https://\*.outlook.com
    
      - https://r4.res.outlook.com
    
      - https://\*.res.outlook.com

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Esportazione dei risultati della ricerca eDiscovery sul posto in un file PST tramite Interfaccia di amministrazione di Exchange

1.  Accedere a **Gestione conformità** \> **eDiscovery e archiviazione sul posto&**.

2.  Nella visualizzazione elenco selezionare la ricerca eDiscovery locale di cui si desidera esportare i risultati, quindi fare clic su **Esporta in un file PST**.
    
    ![Esportazione in un file PST](images/Dn440164.1ebee2ac-89b3-49fa-b70c-a07c9a65f958(EXCHG.150).gif "Esportazione in un file PST")  

3.  Nella finestra **Strumento eDiscovery per esportazione PST** effettuare le seguenti operazioni:
    
      - Fare clic su **Sfoglia** per specificare la posizione in cui si desidera scaricare il file PST.
    
      - Selezionare la casella di controllo **Abilita deduplicazione** per escludere i messaggi duplicati. Il file PST conterrà una sola istanza di un messaggio.
    
      - Selezionare la casella di controllo **Includi elementi senza funzioni di ricerca** per includere elementi non ricercabili, ad esempio messaggi con allegati di tipi di file non indicizzabili da parte di Ricerca di Exchange. Gli elementi non ricercabili vengono esportati in un file PST separato.
        

        > [!IMPORTANT]
        > Se si includono gli elementi senza funzioni di ricerca quando si esportano i risultati della ricerca di eDiscovery si impiegherà di più quando le cassette postali contengono un numero elevato di questo tipo di elementi. Per ridurre il tempo necessario per l'esportazione dei risultati di ricerca e per evitare grandi file di esportazione PST, considerare i seguenti suggerimenti: 
        > <UL>
        > <LI>
        > <P>Creare più ricerche di eDiscovery in modo che ogni ricerca abbia un numero inferiore di cassette postali di origine.</P>
        > <LI>
        > <P>Se si esporta tutto il contenuto della cassetta postale entro un intervallo di date specifico (senza specificare alcuna parola chiave nei criteri di ricerca), allora tutti gli elementi senza funzioni di ricerca all'interno dell'intervallo di date verranno inclusi automaticamente nei risultati della ricerca. Pertanto, non selezionare la casella di controllo <STRONG>Includi elementi senza funzioni di ricerca</STRONG>.</P></LI></UL>



4.  Fare clic su **Start** per esportare i risultati della ricerca in un file PST.
    
    Viene visualizzata una finestra contenente informazioni relative allo stato del processo di esportazione.

## Ulteriori informazioni

  - È possibile ridurre le dimensioni dei file di esportazione PST esportando solamente gli elementi senza funzione di ricerca. A tale scopo, creare o modificare una ricerca, specificare una data di inizio futura, quindi rimuovere tutte le parole chiave dalla casella **Parole chiave**. Nessun risultato della ricerca verrà restituito. Quando si copiano o esportano i risultati della ricerca e si seleziona la casella di controllo **Includi elementi senza funzioni di ricerca**, solo gli elementi senza funzioni di ricerca verranno copiati nella cassetta postale di individuazione o esportati in un file PST.

  - Se si attiva la deduplicazione, tutti i risultati della ricerca vengono esportati in un file PST. Se invece non si attiva la deduplicazione, viene esportato un file PST separato per ciascuna cassetta postale inclusa nella ricerca. Come indicato in precedenza, gli elementi non ricercabili vengono esportati in un file PST separato.

  - Oltre al file PST contenente i risultati della ricerca, vengono esportati anche altri due file:
    
      - Un file di configurazione (file in formato .txt) contenente informazioni sulla richiesta di esportazione PST, ad esempio il nome della ricerca eDiscovery esportata, la data e l'ora dell'esportazione, l'abilitazione o meno delle opzioni relative alla deduplicazione e agli elementi non ricercabili, la query di ricerca e le cassette postali di origine in cui è stata eseguita la ricerca.
    
      - Un registro dei risultati della ricerca (file in formato .csv) contenente una voce per ciascun messaggio restituito nei risultati della ricerca. Ciascuna voce identifica la cassetta postale di origine in cui si trova il messaggio. Se l'opzione di deduplicazione è stata abilitata, è possibile identificare tutte le cassette postali contenenti un messaggio duplicato.

  - Il nome della ricerca costituisce la prima parte del nome di ciascun file esportato. Al nome file di ciascun file PST e al registro dei risultati vengono aggiunte anche la data e l'ora della richiesta di esportazione.

  - Per ulteriori informazioni sulla deduplicazione e sugli elementi non ricercabili, vedere:
    
      - [Estimate, preview, and copy search results](in-place-ediscovery-exchange-2013-help.md)
    
      - [Elementi non ricercabili in Exchange eDiscovery](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

  - Per esportare i risultati della ricerca eDiscovery da eDiscovery Center in SharePoint o SharePoint Online, vedere [Esportazione di contenuto da eDiscovery e creazione di report](https://go.microsoft.com/fwlink/p/?linkid=324757).

## Risoluzione dei problemi


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Sintomo</th>
<th>Possibile causa</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Impossibile eseguire l'esportazione in un file PST.</p></td>
<td><ul>
<li><p>Non esiste alcuna cassetta postale attiva associata all'account. Per esportare il file PST, è necessario disporre di un account attivo.</p></li>
<li><p>La versione di Internet Explorer non è aggiornata. Provare ad aggiornare IE alla versione 10 o successiva. In alternativa, utilizzare un browser diverso.</p></li>
<li><p>I criteri di ricerca immessi nella query <strong>Filtro basato sui criteri</strong> non sono corretti. Ad esempio, viene immesso un nome utente anziché un indirizzo di posta elettronica. Per ulteriori informazioni su come filtrare in base ai criteri, vedere <a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">Modificare una ricerca eDiscovery In locale</a>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Impossibile esportare i risultati della ricerca in un determinato computer. L'esportazione funziona come previsto su un computer diverso.</p></td>
<td><p>Sono state salvate le credenziali di Windows errate in <strong>Gestione credenziali</strong>. Cancellare le credenziali e accedere di nuovo.</p></td>
</tr>
<tr class="odd">
<td><p>Lo strumento di esportazione di file PST eDiscovery non si avvia.</p></td>
<td><p>Le impostazioni della zona Intranet locale sono configurate correttamente in Internet Explorer. Verificare che *.outlook.com, *.office365.com, *.sharepoint.com e *.onmicrosoft.com siano aggiunti ai siti attendibili della zona Intranet locale.</p>
<p>Per aggiungere tali siti alla zona attendibile in IE, vedere <a href="https://windows.microsoft.com/it-it/windows/security-zones-adding-removing-websites#1tc=windows-7">Zone di sicurezza: aggiunta o rimozione di siti Web</a>.</p></td>
</tr>
</tbody>
</table>

