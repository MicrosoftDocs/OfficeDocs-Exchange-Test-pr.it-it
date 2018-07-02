---
title: 'IRM nelle distribuzioni ibride di Exchange: Exchange 2013 Help'
TOCTitle: IRM nelle distribuzioni ibride di Exchange
ms:assetid: ba6ec48b-8f79-4807-b74b-fd442bbbe82f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ659052(v=EXCHG.150)
ms:contentKeyID: 50482152
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IRM nelle distribuzioni ibride di Exchange

 

_<strong>Si applica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2016-12-09_

**Riepilogo:**  come funziona IRM in un ambiente ibrido di Exchange e come configurare IRM affinché funzioni tra i server Exchange locali ed Exchange Online.

Information Rights Management (IRM) consente di evitare la fuga di informazioni riservate fornendo una protezione continua online e offline dei messaggi di posta elettronica e relativi allegati. IRM è supportato sia dall'organizzazione locale di Exchange sia da Exchange Online in Office 365 per le grandi aziende. Tuttavia, esistono delle differenze tra le due implementazioni ed è necessario configurare IRM nell'organizzazione di Exchange Online prima che gli utenti dell'organizzazione possano utilizzarlo.

IRM utilizza Active Directory Rights Management Services (AD RMS), che è un componente di Windows Server 2008 e versione successiva. AD RMS consente agli utenti di creare contenuto protetto da diritti, come ad esempio messaggi di posta elettronica e allegati, quindi definire come tale contenuto può essere utilizzato e a chi viene distribuito. Gli utenti possono specificare modelli che determinano come può essere utilizzato il contenuto. Ad esempio, un utente può specificare che un determinato messaggio di posta elettronica non può essere inviato ad altri destinatari e che le informazioni di quel messaggio non possono essere copiate.

Ulteriori informazioni su IRM sono disponibili in Exchange 2010 nell'argomento: [Informazioni su Information Rights Management](https://technet.microsoft.com/it-it/library/dd638140\(v=exchg.141\).aspx).

Ulteriori informazioni su IRM sono disponibili in Exchange 2013 e Exchange 2016 nell'argomento [Information Rights Management](https://technet.microsoft.com/it-it/library/dd638140\(v=exchg.150\)).

Ulteriori informazioni su AD RMS sono disponibili nell'argomento [Panoramica di Active Directory Rights Management Services](http://go.microsoft.com/fwlink/p/?linkid=215243).

## Differenze tra IRM in Exchange locale ed Exchange Online

La funzionalità IRM disponibile nell'organizzazione Exchange locale potrebbe essere diversa da quella disponibile nell'organizzazione di Exchange Online. Nella tabella che segue è riportato un riepilogo delle funzionalità disponibili in ciascuna organizzazione. Ulteriori informazioni su queste funzionalità sono disponibili nell'argomento: [Information Rights Management](https://technet.microsoft.com/it-it/library/dd638140\(v=exchg.150\)).

### Funzionalità IRM disponibili

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Disponibile in Exchange 2007 e versioni precedenti</th>
<th>Disponibile in Exchange 2010</th>
<th>Disponibile in Exchange Online ed Exchange 2013 e versioni successive</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Protezione manuale dei messaggi in Outlook</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Protezione manuale dei messaggi in Outlook Web App</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Visualizzazione dei messaggi protetti tramite IRM in Outlook</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Visualizzazione dei messaggi protetti tramite IRM in Outlook Web App</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Agente di prelicenza IRM</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Modelli dei criteri RMS</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Decrittografia di trasporto</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Decrittografia dei rapporti del journal</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Decrittografia di ricerca e individuazione di Exchange</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p>Regole di protezione automatiche di Outlook</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Regole di protezione automatiche del trasporto</p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
</tr>
</tbody>
</table>


## IRM nelle distribuzioni ibride

Exchange utilizza i server AD RMS nella foresta Active Directory nella quale è installato il server Exchange. Per i server Exchange locali viene utilizzato il server AD RMS locale. Per l'organizzazione di Exchange Online vengono utilizzati i server AD RMS gestiti nell'ambito dei datacenter Office 365. La configurazione di AD RMS utilizzata da ciascuna organizzazione di Exchange è indipendente da ogni altra distribuzione di AD RMS.

La configurazione di AD RMS, e pertanto anche la configurazione di IRM, non viene automaticamente replicata tra l'organizzazione di Exchange locale e l'organizzazione di Exchange Online. Gli eventuali modelli AD RMS definiti non vengono automaticamente copiati nell'organizzazione di Exchange Online. Se si desidera che gli stessi modelli AD RMS siano disponibili anche nell'organizzazione di Exchange Online, è necessario esportarli manualmente dall'organizzazione locale e applicarli all'organizzazione di Office 365. Vedere la sezione relativa alla Configurazione di IRM nelle distribuzioni ibride più avanti in questo argomento.

## Prestazioni

La configurazione di IRM che viene applicata a un utente dipende dal client utilizzato dall'utente e dal percorso della sua cassetta postale. Nella tabella che segue viene riportato il server AD RMS che verrà utilizzato da un utente.

### Server AD RMS attivo

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Cassetta postale locale</th>
<th>Cassetta postale di Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Client desktop di Outlook</p></td>
<td><p>AD RMS locale</p></td>
<td><p>AD RMS locale</p></td>
</tr>
<tr class="even">
<td><p>Outlook sul Web</p></td>
<td><p>AD RMS locale</p></td>
<td><p>AD RMS di Exchange Online</p></td>
</tr>
<tr class="odd">
<td><p>Dispositivo ActiveSync</p></td>
<td><p>AD RMS locale</p></td>
<td><p>AD RMS di Exchange Online</p></td>
</tr>
</tbody>
</table>


A seconda della configurazione di AD RMS applicata alle organizzazioni locale e di Exchange Online, è possibile che un utente che utilizza Outlook 2007 e Outlook sul Web possa vedere modelli AD RMS differenti. Per questo motivo, si consiglia caldamente di applicare gli stessi modelli sia all'organizzazione locale che all'organizzazione di Exchange Online.

Non dovrebbero esserci differenze nell'esperienza IRM per gli utenti dei client Outlook, a prescindere che la loro cassetta postale si trovi nell'organizzazione locale o Exchange Online.

Un utente di Outlook sul Web la cui cassetta postale si trova su un server di Exchange locale sarà in grado di aprire i messaggi protetti da diritti soltanto dopo aver installato il componente aggiuntivo Rights Management per Internet Explorer. L'utente non potrà comunque rispondere ai messaggi o creare nuovi messaggi protetti da diritti.

Un utente di Outlook sul Web la cui cassetta postale si trova in Exchange Online potrà aprire i messaggi protetti da diritti senza dover installare alcun software aggiuntivo; potrà inoltre rispondere ai messaggi e creare nuovi messaggi protetti da diritti.

## Funzionalità del server

I server Exchange locali utilizzano l'agente di prelicenza AD RMS per decrittografare i messaggi protetti da diritti, in modo tale che gli utenti non debbano fornire credenziali per aprire quei messaggi. Il server Exchange locale contatta il server AD RMS locale per verificare i criteri e diritti di utilizzo e per richiedere l'autorizzazione a decrittografare il messaggio.

L'organizzazione Exchange Online fornisce diverse funzionalità IRM aggiuntive che utilizzano AD RMS di Exchange Online. Queste funzionalità, come la decrittografia dei rapporti del journal, rendono il contenuto dei messaggi protetti da diritti disponibile per ulteriori elaborazioni da parte dei servizi Exchange. Ad esempio, il contenuto decrittografato di un messaggio inserito nel journal può essere salvato, insieme al messaggio protetto da diritti originale, per agevolare le attività di individuazione. Inoltre, i modelli IRM possono essere automaticamente applicati ai messaggi utilizzando le regole di protezione o le regole di trasporto di Outlook per garantire che i messaggi siano conformi ai criteri di protezione delle informazioni applicati dall'organizzazione.

## Configurazione di IRM nelle distribuzioni ibride

IRM in Exchange richiede che AD RMS sia distribuito nella foresta di Active Directory nella quale risiede il server Exchange. La configurazione di AD RMS non viene automaticamente sincronizzata tra l'organizzazione locale e l'organizzazione Exchange Online. È necessario esportare manualmente la configurazione AD RMS, nota come dominio di pubblicazione trusted, dal server AD RMS locale e importarla nell'organizzazione Exchange Online. Il dominio di pubblicazione trusted contiene la configurazione di AD RMS, inclusi i modelli, necessaria all'organizzazione Exchange Online per utilizzare IRM.

Per ulteriori informazioni, vedere [Considerazioni sul dominio di pubblicazione trusted AD RMS](http://go.microsoft.com/fwlink/?linkid=215244).

Oltre ad applicare la configurazione AD RMS locale all'organizzazione Exchange Online, è necessario verificare che i server AD RMS possano essere contattati dai client Outlook e ActiveSync all'esterno della rete locale. Ciò è necessario se si desidera che questi client possano accedere ai messaggi protetti da diritti all'esterno della rete locale.

Una volta configurata la rete locale ed esportati i dati del dominio di pubblicazione trusted, occorre configurare l'organizzazione di Exchange Online importando i dati del dominio di pubblicazione trusted e abilitando IRM.


> [!NOTE]
> Ogni volta che si modifica la configurazione AD&nbsp;RMS locale, è necessario applicare manualmente la nuova configurazione all'organizzazione di Exchange Online. Per eseguire questa operazione, esportare i dati del dominio di pubblicazione trusted dal server AD&nbsp;RMS locale e importarli nell'organizzazione Exchange.



## Configurazione di IRM nelle distribuzioni ibride di Exchange

Se si utilizza IRM nell'organizzazione di Exchange locale e si desidera che anche gli utenti di Exchange Online utilizzino IRM, è necessario eseguire le seguenti operazioni:

1.  Configurare il server Active Directory Rights Management Services (AD RMS) locale.

2.  Abilitare IRM nell'organizzazione di Exchange Online.

3.  Distribuire i modelli AD RMS agli utenti nell'organizzazione di Exchange Online.

## Come configurare i server AD RMS locali?

Per configurare IRM in una distribuzione ibrida è necessario utilizzare Windows PowerShell per accedere al server AD RMS locale. Per ulteriori informazioni, vedere: [Utilizzo di Windows PowerShell per amministrare AD RMS](http://go.microsoft.com/fwlink/p/?linkid=214938)

Procedere come segue per esportare i dati di un dominio di pubblicazione trusted (TPD) dal proprio server AD RMS locale e configurare l'accesso al server AD RMS per i client esterni.

1.  Esportare dati TPD dalla propria organizzazione locale. Per ulteriori informazioni, vedere: [Esportazione di un dominio di pubblicazione trusted](http://go.microsoft.com/fwlink/p/?linkid=214942)

2.  Configurare l'accesso ad un server AD RMS da client esterni. Per ulteriori informazioni, vedere: [Aggiungere un URL del cluster Extranet](http://go.microsoft.com/fwlink/p/?linkid=214945)

## Come abilitare IRM nell'organizzazione di Exchange Online?

Dopo aver esportato i dati TPD da un server AD RMS locale, è necessario importare quei dati nell'organizzazione di Exchange Online e abilitare IRM.

1.  Nell'organizzazione di Exchange Online, importare i dati TPD.
    
        Import-RMSTrustedPublishingDomain -FileData $( [Byte[]] (Get-Content -Encoding Byte -Path "<Path to exported TPD file>" -ReadCount 0))

2.  Abilitare IRM nell'organizzazione di Exchange Online.
    
        Set-IRMConfiguration -InternalLicensingEnabled $True

## Come distribuire modelli AD RMS nell'organizzazione di Exchange Online?

Dopo aver abilitato IRM nell'organizzazione di Exchange Online è necessario distribuire i modelli AD RMS importati. Gli utenti e le funzionalità di Exchange Online indicati di seguito utilizzano i modelli di AD RMS:

  - Utenti di Outlook sul Web

  - Utenti di Exchange ActiveSync

  - Regole di trasporto

  - Decrittografia dei rapporti del journal

  - Regole di protezione di Outlook

<!-- end list -->

1.  Nell'organizzazione di Exchange Online, recuperare un elenco dei modelli AD RMS.
    
        Get-RMSTemplate -Type All

2.  Distribuire i modelli AD RMS agli utenti e alle funzionalità nell'organizzazione di Exchange Online.
    
        Set-RMSTemplate <template name> -Type Distributed
    

    > [!NOTE]
    > Non è possibile modificare il modello AD RMS "Non inoltrare".



3.  Ripetere il passo 2 per ciascun modello AD RMS che si vuole distribuire.

## Come verificare se l'operazione ha avuto esito positivo?

Gli utenti di Outlook sul Web dovrebbero essere in grado di applicare i modelli AD RMS ai nuovi messaggi. Gli utenti di Outlook sul Web e Exchange ActiveSync dovrebbero essere in grado di leggere i messaggi a cui sono applicati modelli di AD RMS. Inoltre, tutti i modelli di AD RMS importati dall'organizzazione locale dovrebbero essere elencati quando si esegue il cmdlet **Get-RMSTemplate**.

Eseguire il comando riportato di seguito nell'organizzazione di Exchange Online.

    Get-RMSTemplate 

Per ulteriori informazioni, vedere: [Information Rights Management in Outlook Web App](https://technet.microsoft.com/it-it/library/dd876891\(v=exchg.150\))

