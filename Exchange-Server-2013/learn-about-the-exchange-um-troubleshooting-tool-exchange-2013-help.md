---
title: 'Informazioni su Exchange UM Troubleshooting Tool: Exchange 2013 Help'
TOCTitle: Informazioni su Exchange UM Troubleshooting Tool
ms:assetid: cc11bf5e-2c87-4495-b2ad-3e9a6bc81dbc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg584301(v=EXCHG.150)
ms:contentKeyID: 56269838
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Informazioni su Exchange UM Troubleshooting Tool

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

I Microsoft Exchange 2010 unificata strumento di risoluzione dei problemi di messaggistica è un cmdlet di Management Shell Exchange denominato **Test-ExchangeUMCallFlow**. È possibile utilizzare lo strumento di condurre una serie di test diagnostici per la messaggistica unificata (UM) nella propria organizzazione. Se uno dei test non riesce, lo strumento di report il motivo per le soluzioni possibili e degli errori risolvere il problema. È possibile utilizzare solo la risoluzione dei problemi di strumento di messaggistica UNIFICATA in Exchange 2010 server o versioni successive.

È possibile utilizzare lo strumento per la risoluzione dei problemi di messaggistica unificata per provare il corretto funzionamento della posta vocale nelle distribuzioni locali e cross-premise. È possibile utilizzare questo strumento nelle distribuzioni del servizio di messaggistica unificata con Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server 2010 o versioni successive, oppure nelle distribuzioni del servizio di messaggistica unificata che comprendono gateway VoIP, IP Private Branch eXchange (IP PBX) o session border controller (SBC).


> [!NOTE]
> Lo strumento per la risoluzione dei problemi di messaggistica unificata viene utilizzato per le attività di test e risoluzione dei problemi. Il cmdlet <STRONG>Test-UMConnectivity</STRONG> viene invece utilizzato per il monitoraggio. Il cmdlet <STRONG>Test-UMConnectivity</STRONG> viene utilizzato con i Management Pack SCOM (System Center Operations Manager) che vengono a loro volta utilizzati per il monitoraggio dei server Messaggistica unificata Exchange 2010, dei server Accesso client di Exchange 2013, dei server Cassette postali e dei componenti di telefonia. Il cmdlet <STRONG>Test-UMConnectivity</STRONG> esegue le prove SIP locali e le prove di accesso locali alle cassette postali e può essere eseguito come un'attività SCOM.



Per scaricare lo strumento messaggistica UNIFICATA di risoluzione dei problemi, vedere [Unified Messaging Troubleshooting dello strumento di](https://go.microsoft.com/fwlink/p/?linkid=182625).

**Sommario**

Panoramica

UM troubleshooting architecture

VoIP gateway and IP PBX deployments

Office Communications Server R2 and Microsoft Lync Server deployments

Installing the UM Troubleshooting Tool

Cmdlet parameters

## Panoramica

Lo strumento per la risoluzione dei problemi di messaggistica unificata semplifica le attività di prova e risoluzione dei problemi delle distribuzioni della messaggistica unificata. Quando viene eseguito lo strumento per la risoluzione dei problemi di messaggistica unificata, esso genera automaticamente una serie di file di traccia che vengono archiviati nella directory C:\\Users\\%UserProfile%\\AppData\\Roaming\\Microsoft Exchange 2010 UM Troubleshooting. Lo strumento genera i seguenti file di traccia:

  - **UMTool\_Collaboration**   Include le tracce dello stack RTC.

  - **UMTool\_DiagnosticLog**   Elenca tutte le prove che sono state eseguite e i loro risultati.

  - **UMTool\_S4**   Include le tracce degli stack di segnalazione S4.

  - **UMTool\_SIPMessageLogs**   Include le tracce SIP complete per la chiamata alle prove effettuata.

Lo strumento per la risoluzione dei problemi di messaggistica unificata esegue direttamente la connessione a un SBC (Session Border Controller) locale, se ne esiste uno, oppure a un SBC presente in un datacenter ed emula una chiamata in arrivo, come se la chiamata arrivasse da un PBX attraverso un gateway VoIP o un IP PBX. Lo strumento per la risoluzione dei problemi di messaggistica unificata può essere utilizzato per la diagnostica:

  - Impostazioni errate nelle distribuzioni di messaggistica unificata locali o cross-premise, nell'ambito delle quali viene distribuito Office Communications Server 2007 R2 o Microsoft Lync Server.

  - Impostazioni errate nelle apparecchiature di telefonia locali che includono dispositivi gateway VoIP e PBX o IP PBX.

  - Problemi di configurazione del DNS (Domain Name System).

  - Emissioni di certificati durante l'utilizzo di dial plan SIP con protezione o di messaggistica unificata con protezione.

  - Problemi di segnalazione e supporti per il DTMF (noto anche come multifrequenza) e per l'audio.

Se lo strumento per la risoluzione dei problemi di messaggistica unificata rileva un errore di configurazione, ne riporta la ragione e le possibili soluzioni . Gli errori che lo strumento per la risoluzione dei problemi di messaggistica unificata è in grado di rilevare e riportare quando viene utilizzato in una distribuzione locale sono i seguenti:

  - Raggiunto il limite massimo di chiamate

  - L'utente non è abilitato per la messaggistica unificata.

  - Impossibile trovare il gateway IP, il dial plan o le informazioni sul gruppo di risposta per la messaggistica unificata.

  - Il tipo di sicurezza non corrisponde a quello del dial plan della messaggistica unificata.

  - Non ci sono processi di lavoro disponibili per elaborare la chiamata.

  - I servizi di messaggistica unificata o di routing di chiamate di messaggistica unificata vengono arrestati.

  - Impossibile trovare la foresta Active Directory.

  - Spazio su disco esaurito.

  - Nella richiesta sono state utilizzate intestazioni SIP non valide.

  - È stata effettuata una chiamata a un server Office Communications Server 2007 R2 o un server Lync Server.

  - Il gateway IP di messaggistica unificata (UM) è disabilitato.

  - L'URI dell'utente chiamato non è valido.

Gli errori che lo strumento per la risoluzione dei problemi di messaggistica unificata è in grado di rilevare e riportare quando viene utilizzato in una distribuzione cross-premise sono i seguenti:

  - L'utente non è abilitato per la messaggistica unificata.

  - Il gateway IP di messaggistica unificata (UM) è disabilitato.

  - L'URI dell'utente non è valido.

  - Il tipo di sicurezza non corrisponde a quello del dial plan della messaggistica unificata.

  - Nella richiesta sono state utilizzate intestazioni SIP non valide.

  - Impossibile trovare il gateway IP, il dial plan o le informazioni sul gruppo di risposta per la messaggistica unificata.

Lo strumento per la risoluzione dei problemi di messaggistica unificata invia un file campione .wav per 15 secondi. Una volta che il file audio e il flusso audio RTP sono stati inviati e riprodotti, lo strumento riporta le metriche per la qualità audio per rilevare problemi audio relativi alla connettività di rete, come, ad esempio, perdita media dei pacchetti e instabilità. Questi report includono anche i dati sulla qualità del flusso di messaggi da e verso un server Messaggistica unificata. I dati sono i seguenti:

  - Network Mean Opinion Score (NMOS)

  - Codec

  - Latenza in millisecondi (ms)

  - Instabilità in millisecondi (ms)

  - % di pacchetti persi

  - La classificazione e i livelli NMOS che verranno utilizzati per determinare la qualità dell'audio sono:
    
      - NMOS minore di 2 = Scarsa
    
      - NMOS maggiore di 2 ma minore di 3 = Media
    
      - NMOS maggiore di 3 ma minore di 4 = Buona
    
      - NMOS maggiore di 4 ma minore di 5 = Eccellente

Lo strumento per la risoluzione dei problemi di messaggistica unificata supporta i test della messaggistica unificata che utilizzano le chiamate protette, SIP con protezione e non protette. Se si scelgono le chiamate protette o SIP con protezione, l'identificazione digitale del certificato utilizzato viene verificata per stabilire se il certificato è scaduto e per determinare il tipo di certificato utilizzato per le comunicazioni TLS (Transport Layer Security). Il certificato viene utilizzato per identificare correttamente e garantire l'identità del computer remoto. Se viene selezionata la chiamata protetta o SIP con protezione, lo strumento per la risoluzione dei problemi di messaggistica unificata verifica se sono soddisfatte le seguenti condizioni:

  - Il certificato locale è stato trovato nell'archivio del computer locale.

  - Il certificato in uso è attendibile.

  - Il nome di destinazione specificato nel certificato è valido.

  - Il certificato è scaduto.

  - Il computer remoto considera attendibile il certificato.

  - Il certificato è stato revocato.

  - Il certificato non dispone del tipo Utilizzo chiavi avanzato.

È possibile eseguire lo strumento per la risoluzione dei problemi di messaggistica unificata in modalità Gateway o SIPClient, a seconda che si tratti della distribuzione di Office Communications Server 2007 R2 o Lync Server oppure a seconda che con i server Messaggistica unificata siano utilizzati i gateway VoIP e PBX o gli IP PBX. Quando viene utilizzata la modalità Gateway o SIPClient, lo strumento per la risoluzione dei problemi di messaggistica unificata supporta l'effettuazione di chiamate con i seguenti formati. Il formato utilizzato dipende dal tipo di URI del dial plan di messaggistica unificata:

  - Interno telefonico   425-555-1010

  - Numeri telefonici E.164   +1 (425) 555-1010

  - Indirizzi SIP   tonysmith@contoso.com

Quando viene utilizzata la modalità SIPClient, lo strumento per la risoluzione dei problemi di messaggistica unificata effettua una chiamata promemoria vocale. Si tratta di una chiamata che non fa squillare un telefono o un endpoint UC (Unified Communications). Infatti, invia la chiamata direttamente alla posta vocale.. Quando lo strumento per la risoluzione dei problemi di messaggistica unificata viene eseguito in modalità SIPClient, esso determina:

  - Quale utente di destinazione viene chiamato.

  - Se la chiamata SIP è stata stabilita correttamente.

  - Se la chiamata SIP è stata accettata da un server Messaggistica unificata di Exchange 2010 o Mailbox Exchange 2013.

  - Se è stata ricevuta la corretta sequenza DTMF.

  - Se il file di diagnostica .wav è stato inviato e ricevuto da un server Messaggistica unificata di Exchange 2010 o Mailbox Exchange 2013.

  - Le metriche utilizzate al momento del ricevimento del flusso audio o di messaggi.

Lo strumento per la risoluzione dei problemi di messaggistica unificata emula le chiamate in arrivo ed esegue una serie di prove diagnostiche che aiutano gli amministratori locali e gli amministratori tenant a verificare il flusso delle chiamate in relazione alla risposta a tali chiamate e l'identificazione degli eventuali errori di configurazione. Sebbene sia possibile utilizzare lo strumento per la risoluzione dei problemi di messaggistica unificata in scenari di risposta alle chiamate, non è però possibile utilizzarlo per provare i seguenti tipi di chiamate:

  - Chiamate Outlook Voice Access, incluse le chiamate che accedono alla posta vocale, alla posta elettronica, al calendario, alla directory, ai contatti personali o alle opzioni personali

  - Operatori automatici di messaggistica unificata

  - Ascolta al telefono

  - Regole ricezione chiamata

  - Fax

  - Provisioning del prompt

Inizio pagina

## Architettura della risoluzione dei problemi di messaggistica unificata

Lo strumento per la risoluzione dei problemi di messaggistica unificata può essere utilizzato non solo per la risoluzione dei problemi, la diagnostica e la correzione degli errori di configurazione nelle distribuzioni cross-premise diverse, ma anche nelle distribuzioni di messaggistica unificata locali. Nelle distribuzioni cross-premise, lo strumento convalida anche le configurazioni SBC locali. L'amministratore è in grado di provare tutti i componenti di messaggistica unificata utilizzati, inclusi gli SBC.

## Distribuzioni di PBX IP e gateway VoIP

Nell'esempio seguente la modalità Gateway viene utilizzata per testare il flusso delle chiamate in un ambiente che non include Office Communications Server 2007 R2 o Lync Server. Nell'esempio viene testata l'apparecchiatura telefonica, inclusi i gateway VoIP, i sistemi PBX e IP PBX e i componenti di messaggistica unificata. In questo esempio viene impostata la modalità di sicurezza VoIP (Voice over IP) su Non protetta, viene utilizzato l'indirizzo IP 10.1.1.1 come hop successivo e viene incluso un numero di interno nelle informazioni sulla deviazione.

```powershell
Test-ExchangeUMCallFlow -Mode Gateway -VoIPSecurity Unsecured -NextHop 10.1.1.1 -Diversion 12345
```

Inizio pagina

## Distribuzioni di Office Communications Server 2007 R2 e Microsoft Lync Server

È possibile utilizzare lo strumento per la risoluzione dei problemi di messaggistica unificata nelle distribuzioni locali e cross-premise che includono Office Communications Server 2007 R2 o Microsoft Lync Server, quando è impostata la modalità SIPClient. In questo esempio viene utilizzata la modalità SIPClient e viene testato il flusso delle chiamate con un dial plan di messaggistica unificata protetto in un ambiente con server Office Communications Server 2007 R2 o Lync Server. Per impostazione predefinita, quando si utilizza lo strumento di risoluzione dei problemi di messaggistica unificata, vengono utilizzate le credenziali dell'utente attualmente connesso al computer. Quando si esegue l'esempio sotto riportato, all'utente viene richiesto di specificare le credenziali che desidera utilizzare per l'esecuzione dello strumento per la risoluzione dei problemi di messaggistica unificata. Per ulteriori informazioni, vedere [Impostare le credenziali da utilizzare con la messaggistica UNIFICATA di risoluzione dei problemi di strumento di Exchange](set-the-credentials-to-use-with-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).

    Test-ExchangeUMCallFlow -Mode SIPClient -VoIPSecurity Secured -CallingParty tony@contoso.com -CalledParty david@contoso.com -Credential $get

## Installazione dello strumento di risoluzione dei problemi di messaggistica unificata

È possibile installare lo strumento di risoluzione dei problemi di messaggistica unificata su un server Messaggistica unificata locale o su un altro computer a 64 bit.

  - Il sistema operativo Windows 7 o Windows 8.

  - Il sistema operativo Windows Server 2008 o Windows Server 2008 R2.

  - I sistemi operativi Windows Server 2012 o Windows Server 2012 R2.

Se si sta utilizzando lo strumento di risoluzione dei problemi di messaggistica unificata su una versione a 64 bit di Windows 7 o Windows 8 oppure sull'edizione a 64 bit di Windows Server 2008, per poter installare lo strumento di risoluzione dei problemi di messaggistica unificata devono essere già installati i seguenti componenti:

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1) vedere [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    

    > [!NOTE]
    > Se lo strumento verrà eseguito su un computer Windows Vista o Windows Server 2008, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=178998">aggiornamento Microsoft .NET Framework 3.5 per Windows Server 2008 x64 e Windows Vista x64,</A>.



  - Windows Gestione remota Windows (WinRM) 2.0 e Windows PowerShell V2 (Windows6.0-KB968930.msu)   Vedere l'articolo 968930 della Microsoft Knowledge Base [Pacchetto di Windows Management Framework Core (Windows PowerShell 2.0 e 2.0 di gestione remota Windows)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Microsoft Unified Communications Managed API 2.0 Core Runtime (Ucmaruntimewebdownloadx64) vedere [Unified Communications Managed API 2.0, Core Runtime (64 bit)](https://go.microsoft.com/fwlink/p/?linkid=198175).

Lo strumento messaggistica UNIFICATA la risoluzione dei problemi (**Test-ExchangeUMCallFlow** cmdlet) non è incluso nel Exchange 2010 SP1 DVD download che include solo Exchange 2010 o supporto di installazione di Exchange 2013. Tuttavia è possibile scaricare lo strumento messaggistica UNIFICATA di risoluzione dei problemi dall' [Area Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625).

Per ulteriori informazioni, vedere [Installazione dello strumento di risoluzione dei problemi di messaggistica unificata di Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).

Inizio pagina

## Parametri cmdlet

Le tabella che segue include i parametri che è possibile utilizzare con il cmdlet **Test-ExchangeUMCallFlow** e le relative descrizioni. È anche possibile utilizzare il comando Shell `Get-help Test-ExchangeUMCallFlow -detailed` per trovare le informazioni dettagliate inerenti ciascun parametro utilizzabile con il cmdlet **Test-ExchangeUMCallFlow**, insieme a una serie di esempi di utilizzo.

### Parametri

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>CalledParty</em></p></td>
<td><p>Il parametro <em>CalledParty</em> consente di specificare l'URI SIP dell'utente di Office Communications Server 2007 R2 o Lync Server che è stato abilitato per Enterprise Voice. Si tratta dell'utente al quale il cmdlet <strong>Test-ExchangeUMCallFlow</strong> effettua la chiamata vocale , ad esempio: <code>-CalledParty tonysmith@contoso.com</code>. Utilizzare questo parametro se si esegue lo strumento in modalità SIPClient.</p></td>
</tr>
<tr class="even">
<td><p><em>CallingParty</em></p></td>
<td><p>Il parametro <em>CallingParty</em> consente di specificare l'URI SIP dell'utente di Office Communications Server 2007 R2 o Lync Server che è stato abilitato per Enterprise Voice. Si tratta dell'utente che sta effettuando la chiamata in arrivo, ad esempio: <code>-CallingParty tonysmith@contoso.com</code>. Utilizzare questo parametro se si esegue lo strumento in modalità SIPClient.</p></td>
</tr>
<tr class="odd">
<td><p><em>Diversion</em></p></td>
<td><p>Il parametro <em>Diversion</em> indica la stringa che deve essere inviata come informazioni sulla deviazione per la chiamata in arrivo. Possono essere sotto forma di intestazione sulla deviazione o sulla cronologia delle informazioni. Le informazioni sulla deviazione incluse nella chiamata in arrivo possono essere un numero di interno o includere anche altre informazioni sulla deviazione.</p>
<p>Quando si forniscono informazioni sulla deviazione come un'intestazione di cronologia, verificare quanto segue:</p>
<ul>
<li><p>Sono disponibili almeno due voci differenti con parti utente differenti.</p></li>
<li><p>L'ultima voce contiene il numero pilota del dial plan di messaggistica unificata associato dell'utente.</p></li>
<li><p>La penultima voce contiene il numero di estensione dell'utente abilitato alla messaggistica unificata. Tale voce deve includere anche il testo motivo appropriato. Tale testo deve rappresentare la sequenza di escape appropriata in base alle regole di escape del parametro dell'URL standard.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>Il parametro <em>Mode</em> consente di specificare se deve essere utilizzata la modalità gateway VoIP, IP PBX o Office Communications Server R2 o Lync Server. È possibile specificare la modalità Gateway quando la distribuzione della messaggistica unificata include gateway VoIP o IP PBX o la modalità SIPClient, se la distribuzione include Office Communications Server 2007 R2 o Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>NextHop</em></p></td>
<td><p>Il parametro <em>NextHop</em> consente di specificare l'indirizzo IP o il nome di dominio completo dell'hop successivo e può anche includere la porta TCP dell'hop successivo a cui deve collegarsi il cmdlet <strong>Test-ExchangeUMCallFlow</strong> durante l'emulazione del gateway VoIP o IP PBX. Quando si include la porta TCP, è necessario specificare la porta 5060 per la modalità Non protetta oppure la porta 5061 per la modalità SIP con protezione. Ad esempio: <code>gateway.contoso.com:5061</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateThumbprint</em></p></td>
<td><p>Il parametro <em>CertificateThumbprint</em> consente di specificare l'identificazione digitale del certificato utilizzato per TLS (Transport Layer Security). Questa identificazione è obbligatoria se sul dial plan della messaggistica unificata è configurata la modalità Protetta o SIP con protezione. Questa identificazione digitale del certificato è il certificato esportato dal gateway VoIP, IP PBX o SBC. Inoltre, il computer su cui è installato lo strumento di risoluzione dei problemi di messaggistica unificata e che viene utilizzato per verificare il flusso delle chiamate deve considerare attendibile l'autorità di certificazione dell'hop successivo.</p></td>
</tr>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p>Il parametro <em>Credential</em> indica le credenziali che verranno utilizzate per eseguire il cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>HuntGroup</em></p></td>
<td><p>Il parametro <em>HuntGroup</em> consente di specificare il gruppo di risposta di messaggistica unificata associato al gateway VoIP emulato. In genere si tratta di un numero di interno. Utilizzare questo parametro se si esegue lo strumento in modalità Gateway.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoIPSecurity</em></p></td>
<td><p>Il parametro <em>VoIPSecurity</em> consente di specificare la modalità di sicurezza quando si utilizza il cmdlet in modalità Gateway. È possibile utilizzare una delle seguenti modalità di sicurezza VoIP:</p>
<ul>
<li><p>Protetta (TLS/SRTP)</p></li>
<li><p>Non protetta (TCP/RTP) (predefinita)</p></li>
<li><p>SIP con protezione (TLS/RTP)</p></li>
</ul></td>
</tr>
</tbody>
</table>


Inizio pagina

