---
title: 'Firewall intestazioni: Exchange 2013 Help'
TOCTitle: Firewall intestazioni
ms:assetid: 9b148f7b-47a9-4379-a55b-8d5310c1772f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232136(v=EXCHG.150)
ms:contentKeyID: 52063088
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Firewall intestazioni

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

In Microsoft Exchange Server 2013, *il firewall dell'intestazione* è un meccanismo che consente di rimuovere campi di intestazione specifici dai messaggi in arrivo e in uscita. Esistono due tipi diversi di campi dell'intestazione che sono interessati dal firewall dell'intestazione:

  - **X-header**   Un *X-header* è un campo dell'intestazione definito dall'utente, non ufficiale. I campi X-Header non sono menzionati in modo specifico nell'RFC-2822, ma l'utilizzo di un campo di intestazione non definito che inizia con **X-** è ormai una prassi accettata per aggiungere campi di intestazione non ufficiali al messaggio. Le applicazioni di messaggistica, quali protezione posta indesiderata, antivirus e server di messaggistica, possono aggiungere "X-Header" propri al messaggio. In Exchange, i campi X-header contengono informazioni dettagliate relative alle azioni eseguite sul messaggio dal servizio di trasporto, ad esempio il livello di probabilità di posta indesiderata (SCL, Spam Confidence Level), i risultati del filtro contenuto e lo stato di elaborazione delle regole. Rendere queste informazioni note a fonti non autorizzate potrebbe rappresentare una minaccia per la protezione.

  - **Intestazioni di routing**   Le intestazioni di routing sono campi di intestazione SMTP standard definiti in RFC 2821 e RFC 2822. Le intestazioni di routing contrassegnano un messaggio utilizzando le informazioni sui diversi server di messaggistica utilizzati per recapitare il messaggio al destinatario. Le intestazioni di routing che sono inserite nei messaggi da utenti malintenzionati possono rappresentare in modo erroneo il percorso di routing effettuato da un messaggio per raggiungere un destinatario.

Il firewall dell'intestazione impedisce lo spoofing dei campi X-header relativi ad Exchange rimuovendoli dai messaggi in ingresso nell'organizzazione di Exchange provenienti da origini non attendibili. Il firewall dell'intestazione impedisce la diffusione dei campi X-header relativi ad Exchange rimuovendoli dai messaggi in uscita inviati a destinazioni non attendibili esterne all'organizzazione di Exchange. Il firewall dell'intestazione impedisce inoltre lo spoofing delle intestazioni di routing standard utilizzate per tenere traccia della cronologia di routing di un messaggio.

**Sommario**

Message header fields affected by header firewall in Exchange

How header firewall is applied to Receive connectors and Send connectors

Header firewall for inbound messages on Receive connectors

Header firewall for outbound messages on Send connectors

Header firewall for other message sources

Organization X-headers and forest X-headers in Exchange

## Campi delle intestazioni di messaggi interessati dal firewall dell'intestazione in Exchange

I seguenti tipi di X-header e intestazioni di routing sono interessati dal firewall dell'intestazione:

  - **X-header dell'organizzazione**   Questi campi di X-header iniziano con **X-MS-Exchange-Organization-**.

  - **X-header della foresta**   Questi campi X-header iniziano con **X-MS-Exchange-Forest-**.
    
    Per esempi sugli X-header dell'organizzazione e della foresta, vedere la sezione Organization X-headers and forest X-headers in Exchange alla fine di questo argomento.

  - **Received: routing headers**   Un'istanza diversa di questo campo di intestazione viene aggiunta all'intestazione del messaggio da ogni server di messaggistica che ha accettato e inoltrato il messaggio al destinatari. L'intestazione **Received:**  in genere include il nome del server di messaggistica e il timestamp della data.

  - **Resent-\*: routing headers**   I campi di intestazione Inviato nuovamente sono campi di intestazione informativi che possono essere utilizzati per determinare se un messaggio è stato inoltrato da un utente. Sono disponibili i seguenti campi di intestazione Inviato nuovamente: **Resent-Date:** , **Resent-From:** , **Resent-Sender:** , **Resent-To:** , **Resent-Cc:** , **Resent-Bcc:**  e **Resent-Message-ID:** . I campi **Resent-** nuovamente vengono utilizzati allo scopo di visualizzare il messaggio al destinatario come se fosse stato inviato direttamente dal mittente originale. Il destinatario può visualizzare l'intestazione del messaggio per individuare chi ha inoltrato il messaggio.

Exchange utilizza due modalità diverse per applicare il firewall intestazioni alle X-header organizzazione e foresta e alle intestazioni di routing presenti nei messaggi:

  - Le autorizzazioni vengono assegnate ai connettori di invio o di ricezione che possono essere utilizzati per mantenere o rimuovere tipi specifici di intestazioni nei messaggi quando il messaggio passa attraverso il connettore.

  - Il firewall dell'intestazione viene implementato automaticamente per tipi specifici delle intestazioni nei messaggi durante altri tipi di invio del messaggio.

Inizio pagina

## Come viene applicato il firewall dell'intestazione ai connettori di ricezione e invio

Il firewall intestazioni viene applicato ai messaggi che passano attraverso i connettori di invio e di ricezione in base ad autorizzazioni specifiche che vengono assegnate ai connettori.

Se l'autorizzazione viene assegnata al connettore di ricezione o di invio, il firewall intestazioni non viene applicato ai messaggi che passano attraverso il connettore. I campi delle intestazioni interessati sono mantenuti nei messaggi.

Se l'autorizzazione non viene assegnata al connettore di ricezione o di invio, il firewall intestazioni viene applicato ai messaggi che passano attraverso il connettore. I campi delle intestazioni interessati sono rimossi dai messaggi.

Nella seguente tabella vengono descritte le autorizzazioni sui connettori di invio e di ricezione, utilizzati per applicare il firewall intestazioni e i campi delle intestazioni interessati.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo connettore</th>
<th>Autorizzazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Connettore di ricezione</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong></p></td>
<td><p>Questa autorizzazione interessa i campi X-header dell'organizzazione che iniziano con <strong>X-MS-Exchange-Organization-</strong> nei messaggi in ingresso.</p></td>
</tr>
<tr class="even">
<td><p>Connettore di ricezione</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><p>Questa autorizzazione interessa i campi X-header foresta che iniziano con <strong>X-MS-Exchange-Forest-</strong> nei messaggi in ingresso.</p></td>
</tr>
<tr class="odd">
<td><p>Connettore di ricezione</p></td>
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>L'autorizzazione interessa i campi intestazioni <strong>Received:</strong> e <strong>Resent-*:</strong> nei messaggi in ingresso.</p></td>
</tr>
<tr class="even">
<td><p>Connettore di invio</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong></p></td>
<td><p>Questa autorizzazione interessa i campi X-header dell'organizzazione che iniziano con <strong>X-MS-Exchange-Organization-</strong> nei messaggi in uscita.</p></td>
</tr>
<tr class="odd">
<td><p>Connettore di invio</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><p>Questa autorizzazione interessa i campi X-header foresta che iniziano con <strong>X-MS-Exchange-Forest-</strong> nei messaggi in uscita.</p></td>
</tr>
<tr class="even">
<td><p>Connettore di invio</p></td>
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>L'autorizzazione interessa i campi intestazioni <strong>Received:</strong> e <strong>Resent-*:</strong> nei messaggi in uscita.</p></td>
</tr>
</tbody>
</table>


## Firewall intestazioni per messaggi in ingresso su connettori di ricezione

Nella seguente tabella viene descritta l'applicazione predefinita delle autorizzazioni del firewall intestazioni sui connettori di ricezione.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Autorizzazione</th>
<th>Entità di sicurezza predefinite di Exchange a cui è stata assegnata l'autorizzazione</th>
<th>Gruppo di autorizzazioni con entità di sicurezza come membri</th>
<th>Tipo di utilizzo predefinito che consente di assegnare i gruppi di autorizzazioni al connettore di ricezione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Organization</strong> e <strong>Ms-Exch-Accept-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Server Trasporto Hub</p></li>
<li><p>Server Trasporto Edge</p></li>
<li><p>Exchange Server</p>

> [!NOTE]
> solo sui server Trasporto Hub


</li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Account utente anonimi</p></td>
<td><p><strong>Anonimo</strong></p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Account utente autenticati</p></td>
<td><p><strong>ExchangeUsers</strong></p></td>
<td><p><code>Client</code> (non disponibile nei server Trasporto Edge)</p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Server Trasporto Hub</p></li>
<li><p>Server Trasporto Edge</p></li>
<li><p>Exchange Server</p>

> [!NOTE]
> solo server Trasporto Hub


</li>
<li><p>Server protetti esternamente</p></li>
</ul></td>
<td><p><strong>ExchangeServers</strong></p></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Accept-Headers-Routing</strong></p></td>
<td><p>Account server partner</p></td>
<td><p><strong>Partner</strong></p></td>
<td><p><code>Internet</code> e <code>Partner</code></p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Firewall intestazioni su connettori di ricezione

Per applicare il firewall dell'intestazione ai messaggi in uno scenario del connettore di ricezione personalizzato, utilizzare uno dei seguenti metodi:

  - Create il connettore di ricezione con un tipo di utilizzo che applica automaticamente il firewall intestazioni ai messaggi. Tenere presente che è possibile impostare il tipo di utilizzo durante la creazione del connettore di ricezione.
    
      - Per rimuovere X-header dell'organizzazione o foresta dai messaggi, creare un connettore di ricezione e selezionare un tipo di utilizzo diverso da `Internal`.
    
      - Per rimuovere le intestazioni di routing dai messaggi, eseguire una delle operazioni seguenti:
        
          - Creare un connettore di ricezione e selezionare il tipo di utilizzo `Custom`. Non assegnare gruppi di autorizzazioni al connettore di ricezione.
        
          - Modificare un connettore di ricezione esistente e impostare il parametro *PermissionGroups*sul valore `None`.
        
        Tenere presente che se si dispone di un connettore di ricezione senza gruppi di autorizzazioni associati, sarà necessario aggiungere entità di sicurezza al connettore di ricezione come descritto nell'ultimo passaggio.

  - Utilizzare il cmdlet **Remove-ADPermission** per rimuovere l'autorizzazione **Ms-Exch-Accept-Headers-Organization**, l'autorizzazione **Ms-Exch-Accept-Headers-Forest** e l'autorizzazione **Ms-Exch-Accept-Headers-Routing** dall'entità di sicurezza configurata sul connettore di ricezione. Questo metodo non funziona se l'autorizzazione è stata assegnata all'entità di sicurezza tramite un gruppo di autorizzazioni sul connettore di ricezione, perché non è possibile modificare l'assegnazione delle autorizzazioni o l'appartenenza al gruppo del gruppo di autorizzazioni.

  - Utilizzare il cmdlet **Add-ADPermission** per aggiungere le appropriate entità di sicurezza necessarie per il flusso di posta sul connettore di ricezione. Verificare che alle entità di sicurezza siano assegnate le autorizzazioni **Ms-Exch-Accept-Headers-Organization**, **Ms-Exch-Accept-Headers-Forest** e **Ms-Exch-Accept-Headers-Routing**. Se necessario, utilizzare il cmdlet **Add-ADPermission** per negare le autorizzazioni **Ms-Exch-Accept-Headers-Organization**, **Ms-Exch-Accept-Headers-Forest** e **Ms-Exch-Accept-Headers-Routing** alle entità di sicurezza configurate sul connettore di ricezione.

Per ulteriori informazioni, vedere gli argomenti seguenti:

  - [Connettori di ricezione](receive-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/it-it/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/it-it/library/aa996048\(v=exchg.150\))

Inizio pagina

## Firewall intestazioni per messaggi in uscita su connettori di invio

Nella seguente tabella viene descritta l'applicazione predefinita delle autorizzazioni del firewall intestazioni sui connettori di invio.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Autorizzazione</th>
<th>Entità di sicurezza predefinite di Exchange a cui è stata assegnata l'autorizzazione</th>
<th>Tipo di utilizzo predefinito che consente di assegnare i gruppi di autorizzazioni al connettore di invio</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Organization</strong> e <strong>Ms-Exch-Send-Headers-Forest</strong></p></td>
<td><ul>
<li><p>Server Trasporto Hub</p></li>
<li><p>Server Trasporto Edge</p></li>
<li><p>Exchange Server</p>

> [!NOTE]
> solo sui server Trasporto Hub


</li>
<li><p>Server protetti esternamente</p></li>
<li><p>Gruppi di protezione universali <strong>ExchangeLegacyInterop</strong></p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><ul>
<li><p>Server Trasporto Hub</p></li>
<li><p>Server Trasporto Edge</p></li>
<li><p>Exchange Server</p>

> [!NOTE]
> solo sui server Trasporto Hub


</li>
<li><p>Server protetti esternamente</p></li>
<li><p>Gruppi di protezione universali <strong>ExchangeLegacyInterop</strong></p></li>
</ul></td>
<td><p><code>Internal</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Account utente anonimo</p></td>
<td><p><code>Internet</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Ms-Exch-Send-Headers-Routing</strong></p></td>
<td><p>Server partner</p></td>
<td><p><code>Partner</code></p></td>
</tr>
</tbody>
</table>


Inizio pagina

## Firewall intestazioni su connettori di invio

Per applicare il firewall dell'intestazione ai messaggi in uno scenario del connettore di invio personalizzato, utilizzare uno dei seguenti metodi:

  - Create il connettore di invio con un tipo di utilizzo che applica automaticamente il firewall intestazioni ai messaggi. Tenere presente che è possibile impostare il tipo di utilizzo durante la creazione del connettore di invio.
    
      - Per rimuovere X-header dell'organizzazione o foresta dai messaggi, creare un connettore di invio e selezionare un tipo di utilizzo diverso da `Internal` o `Partner`.
    
      - Per rimuovere le intestazioni di routing dai messaggi, creare un connettore di invio e selezionare il tipo di utilizzo `Custom`. L'autorizzazione **Ms-Exch-Send-Headers-Routing** viene assegnata a tutti i tipi di utilizzo del connettore di invio ad eccezione di `Custom`.

  - Rimuovere un'entità di sicurezza che assegna le autorizzazioni **Ms-Exch-Send-Headers-Organization**, **Ms-Exch-Send-Headers-Forest** e **Ms-Exch-Send-Headers-Routing** dal connettore.

  - Utilizzare il cmdlet **Remove-ADPermission** per rimuovere le autorizzazioni **Ms-Exch-Send-Headers-Organization**, **Ms-Exch-Send-Headers-Forest** e **Ms-Exch-Send-Headers-Routing** da una delle entità di sicurezza configurate sul connettore di invio.

  - Utilizzare il cmdlet **Add-ADPermission** per negare le autorizzazioni **Ms-Exch-Send-Headers-Organization**, **Ms-Exch-Send-Headers-Forest** e **Ms-Exch-Send-Headers-Routing** a una delle entità di sicurezza configurate sul connettore di invio.

Per ulteriori informazioni, vedere gli argomenti seguenti:

  - [Connettori di invio](send-connectors-exchange-2013-help.md)

  - [Add-ADPermission](https://technet.microsoft.com/it-it/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/it-it/library/aa996048\(v=exchg.150\))

Inizio pagina

## Firewall intestazioni per altre origini del messaggio

I messaggi possono entrare nella pipeline di trasporto di un server Cassette postali o in un server Trasporto Edge senza utilizzare i connettori di invio o i connettori di ricezione. Il firewall intestazioni viene applicato alle altre origini dei messaggi descritte nell'elenco seguente:

  - **Directory di prelievo e di directory di riesecuzione**   La directory di prelievo viene utilizzata dagli amministratori o dalle applicazioni per inviare i file dei messaggi. La directory di riesecuzione viene utilizzata per inviare nuovamente i messaggi esportati dalle code dei messaggi di Exchange. Per ulteriori informazioni sulle directory di prelievo e di riesecuzione, vedere [Directory di prelievo e directory di riesecuzione](pickup-directory-and-replay-directory-exchange-2013-help.md).
    
    I campi X-header dell'organizzazione, X-header della foresta e intestazioni di routing vengono rimossi dai file dei messaggi nella directory di prelievo.
    
    Le intestazioni di routing vengono mantenute nei messaggi inviati dalla directory di riesecuzione.
    
    La rimozione dai messaggi o il mantenimento di X-header dell'organizzazione e della foresta viene controllato dal campo dell'intestazione **X-CreatedBy:**  nel file del messaggio:
    
      - Se il valore di **X-CreatedBy:**  è `MSExchange15`, i campi X-header dell'organizzazione e X-header della foresta vengono mantenuti nei messaggi.
    
      - Se il valore di **X-CreatedBy:**  non è `MSExchange15`, i campi X-header dell'organizzazione e X-header della foresta vengono rimossi dai messaggi.
    
      - Se il campo dell'intestazione **X-CreatedBy:**  non esiste nel file dei messaggi, i campi X-header dell'organizzazione e X-header della foresta vengono rimossi dai messaggi.

  - **Directory di destinazione**   La directory di destinazione viene utilizzata dai connettori esterni sui server Cassette postali per inviare i messaggi ai server di messaggistica che non utilizzano il protocollo SMTP per il trasferimento dei messaggi. Per ulteriori informazioni sui connettori esterni, vedere [Connettori esterni](foreign-connectors-exchange-2013-help.md).
    
    I campi X-header dell'organizzazione e X-header della foresta vengono rimossi dai file dei messaggi prima di essere inseriti nella directory di destinazione.
    
    Le intestazioni di routing vengono mantenute nei messaggi inviati dalla directory di destinazione.

  - **Trasporto cassette postali**   Il servizio Trasporto cassette postali esiste sui server Cassette postali per trasmettere messaggi a e da cassette postali sui server Cassette postali. Per ulteriori informazioni sul servizio Trasporto cassette postali, vedere [Flusso di posta](mail-flow-exchange-2013-help.md).
    
    I campi X-header dell'organizzazione, X-header della foresta e intestazioni di routing vengono rimossi dai messaggi in uscita inviati dalle cassette postali dal servizio Invio trasporto cassette postali.
    
    Le intestazioni di routing vengono mantenute per i messaggi in ingresso ai destinatari delle cassette postali dal servizio Recapito trasporto cassette postali. Le seguenti intestazioni X-header dell'organizzazione vengono mantenute per i messaggi in ingresso ai destinatari delle cassette postali dal servizio Recapito trasporto cassette postali:
    
      - **X-MS-Exchange-Organization-SCL**
    
      - **X-MS-Exchange-Organization-AuthDomain**
    
      - **X-MS-Exchange-Organization-AuthMechanism**
    
      - **X-MS-Exchange-Organization-AuthSource**
    
      - **X-MS-Exchange-Organization-AuthAs**
    
      - **X-MS-Exchange-Organization-OriginalArrivalTime**
    
      - **X-MS-Exchange-Organization-OriginalSize**

  - **Messaggi DSN**   I campi X-header dell'organizzazione, X-header della foresta e intestazioni di routing vengono rimossi dal messaggio originale o all'intestazione del messaggio originale allegata al messaggio DSN. Per ulteriori informazioni sui messaggi DSN, vedere [DSN e NDR in Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

  - **Invio agente di trasporto**   I campi X-header dell'organizzazione, X-header della foresta e intestazioni di routing vengono mantenuti nei messaggi inviati dagli agenti di trasporto.

Inizio pagina

## X-header dell'organizzazione e X-header della foresta in Exchange

Il servizio Trasporto sui server Cassette postali o i server Trasporto Edge inseriscono campi X-header personalizzati nell'intestazione del messaggio.

I campi X-header dell'organizzazione iniziano con **X-MS-Exchange-Organization-**. I campi X-header della foresta iniziano con **X-MS-Exchange-Forest-**. La seguente tabella descrive alcuni campi X-header dell'organizzazione e campi X-header della foresta utilizzati nei messaggi in un'organizzazione Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>X-Header</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Forest-RulesExecuted</strong></p></td>
<td><p>Regole di trasporto elaborate nel messaggio.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-Antispam-Report</strong></p></td>
<td><p>Riepilogo dei risultati del filtro protezione da posta indesiderata applicato al messaggio dall'agente filtro contenuto.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthAs</strong></p></td>
<td><p>Specifica l'origine di autenticazione. Questo campo X-header è sempre presente quando si analizza la protezione di un messaggio. I valori possibili sono <code>Anonymous</code>, <code>Internal</code>, <code>External</code> o <code>Partner</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthDomain</strong></p></td>
<td><p>Compilato durante l'autenticazione di tipo dominio protetto. Il valore è FQDN del dominio remoto autenticato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-AuthMechanism</strong></p></td>
<td><p>Specifica il meccanismo di autenticazione per l'invio del messaggio. Il valore è un numero esadecimale a due cifre.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-AuthSource</strong></p></td>
<td><p>Specifica il nome di dominio completo (FQDN) del server che ha valutato l'autenticazione del messaggio per conto dell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Journal-Report</strong></p></td>
<td><p>Identifica i rapporti del journal nel trasporto. Appena il messaggio lascia il servizio di trasporto, l'intestazione diventa <strong>X-MS-Journal-Report</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalArrivalTime</strong></p></td>
<td><p>Identifica l'ora in cui il messaggio è entrato per la prima volta nell'organizzazione di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Sender</strong></p></td>
<td><p>Identifica il mittente originale di un messaggio in quarantena quando entra per la prima volta nell'organizzazione Exchange.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-OriginalSize</strong></p></td>
<td><p>Identifica la dimensione originale di un messaggio in quarantena quando entra per la prima volta nell'organizzazione Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Original-Scl</strong></p></td>
<td><p>Identifica il livello SCL originale di un messaggio in quarantena quando entra per la prima volta nell'organizzazione Exchange.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-PCL</strong></p></td>
<td><p>Identifica il livello di probabilità di phishing. I valori possibili per il livello di probabilità di phishing sono compresi fra 1 e 8. Un valore superiore indica un messaggio sospetto. Per ulteriori informazioni, vedere <a href="anti-spam-stamps-exchange-2013-help.md">Contrassegni filtro posta indesiderata</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-Quarantine</strong></p></td>
<td><p>Indica che il messaggio è stato messo in quarantena nella cassetta postale di quarantena della posta indesiderata e che è stata inviata una notifica sullo stato del recapito (DSN, Delivery Status Notification). Può anche indicare che il messaggio è stato messo in quarantena e rilasciato dall'amministratore. Questo campo X-header impedisce che il messaggio rilasciato venga inviato nuovamente alla cassetta postale di quarantena della posta indesiderata. Per ulteriori informazioni, vedere <a href="release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md">Versione messaggi dalla cassetta postale di quarantena della posta indesiderata in quarantena</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>X-MS-Exchange-Organization-SCL</strong></p></td>
<td><p>Identifica il livello SCL del messaggio. I valori SCL possibili sono compresi fra 0 e 9. Un valore superiore indica un messaggio sospetto. Con il valore speciale -1 il messaggio viene escluso dall'elaborazione da parte dell'agente filtro contenuto. Per ulteriori informazioni, vedere <a href="content-filtering-exchange-2013-help.md">Filtro contenuto</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>X-MS-Exchange-Organization-SenderIdResult</strong></p></td>
<td><p>Contiene i risultati dell'agente ID mittente. L'agente ID mittente utilizza SPF (Sender Policy Framework) per confrontare l'indirizzo IP di origine del messaggio con il dominio utilizzato nell'indirizzo di posta elettronica del mittente. I risultati dell'ID mittente vengono utilizzati per calcolare il livello di probabilità di posta indesiderata di un messaggio. Per ulteriori informazioni, vedere <a href="sender-id-exchange-2013-help.md">ID mittente</a>.</p></td>
</tr>
</tbody>
</table>


Inizio pagina

