---
title: 'Procedura guidata di configurazione ibrida: Exchange 2013 Help'
TOCTitle: Procedura guidata di configurazione ibrida
ms:assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh529921(v=EXCHG.150)
ms:contentKeyID: 50482144
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Procedura guidata di configurazione ibrida

 

_<strong>Si applica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Ultima modifica dell'argomento:</strong>2016-12-09_

In questo argomento viene fornita una panoramica del processo di configurazione di una distribuzione ibrida in Exchange, delle funzionalità di una distribuzione ibrida e delle opzioni disponibili. Viene inoltre illustrato il motore di configurazione ibrida, che esegue le operazioni di base necessarie per configurare e aggiornare una distribuzione ibrida.

Per ulteriori informazioni sulle distribuzioni ibride, vedere [Distribuzioni ibride di Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

**Sommario**

Processo di configurazione ibrida

Funzionalità di configurazione ibrida

Opzioni di configurazione ibrida

Motore di configurazione ibrida

## Processo di configurazione ibrida

In questa sezione viene offerta una breve panoramica del processo della procedura guidata di configurazione ibrida. La procedura guidata crea innanzitutto l'oggetto **HybridConfiguration** nell'organizzazione di Active Directory locale. Questo oggetto di Active Directory archivia le informazioni di configurazione per la distribuzione ibrida e viene aggiornato tramite la procedura guidata di configurazione ibrida. La procedura guidata raccoglie quindi i dati di configurazione della topologia locale esistente di Exchange e Active Directory, i dati di configurazione dell'organizzazione tenant di Office 365 e i dati di configurazione di Exchange Online, definisce vari parametri dell'organizzazione e quindi esegue una lunga sequenza di attività di configurazione, sia nell'organizzazione locale che nell'organizzazione di Exchange Online.


> [!IMPORTANT]
> Prima di utilizzare la procedura guidata della configurazione ibrida, è importante tenere presenti alcune considerazioni e prerequisiti. È necessario soddisfare i requisiti per le distribuzioni ibride indicati in<A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Prerequisiti per la distribuzione ibrida</A>. A questo punto è possibile utilizzare la procedura guidata di configurazione ibrida per configurare l'organizzazione di Exchange per la distribuzione ibrida.



Il processo di configurazione della distribuzione ibrida si articola nelle seguenti fasi generali:

1.  **Verifica dei prerequisiti ed esecuzione dei controlli della topologia**   La procedura guidata di configurazione ibrida verifica che l'organizzazione locale e l'organizzazione di Exchange Online siano in grado di supportare la distribuzione ibrida. Gli aspetti dell'organizzazione locale e dell'organizzazione di Exchange Online verificati e controllati dalla procedura guidata includono:
    
      - Versione dei server Exchange nell'organizzazione locale
    
      - Versione di Exchange Online
    
      - Presenza e configurazione della sincronizzazione con Active Directory
    
      - Domini federati e accettati
    
      - Relazioni di trust federativo e tra organizzazioni esistenti
    
      - Directory virtuali dei servizi Web
    
      - Certificati di Exchange

2.  **Credenziali dell'account di test**   Gli account di gestione ibrida designati dell'organizzazione locale e dell'organizzazione di Office 365 accedono all'organizzazione locale e all'organizzazione di Exchange Online al fine di raccogliere le informazioni necessarie per la verifica dei prerequisiti e apportare le modifiche alla configurazione dei parametri dell'organizzazione richieste per abilitare le funzionalità della distribuzione ibrida. La procedura guidata di configurazione ibrida verifica che tali account dispongano delle credenziali appropriate e che siano in grado di connettersi all'organizzazione locale e all'organizzazione di Exchange Online. Affinché la procedura guidata di configurazione ibrida possa completare tali attività, è necessario che gli account di gestione della distribuzione ibrida per l'organizzazione locale e l'organizzazione di Office 365 siano membri del gruppo di ruoli Gestione organizzazione.

3.  **Modifiche alla configurazione della distribuzione ibrida**   Dopo i test degli account di gestione della configurazione ibrida, le verifiche e i controlli della topologia, nonché la raccolta delle informazioni definite nel relativo processo, la procedura guidata di configurazione ibrida apporta le modifiche di configurazione necessarie per creare e abilitare la distribuzione ibrida. Tutte le modifiche apportate alla configurazione ibrida vengono automaticamente inserite nel registro di configurazione ibrida. Per impostazione predefinita, tale registro si trova nel server Cassette postali locale, in `%UserProfile%\AppData\Roaming\Microsoft\Exchange Hybrid Configuration`.
    

    > [!IMPORTANT]
    > Il flusso di posta in arrivo viene controllato da record MX dell'organizzazione. I messaggi di posta elettronica Internet in arrivo per una distribuzione ibrida non vengono configurati dalla procedura guidata della configurazione ibrida.



## Funzionalità di configurazione ibrida

Per impostazione predefinita, la procedura guidata di configurazione ibrida abilita automaticamente tutte le funzionalità della distribuzione ibrida a ogni esecuzione. Per disabilitare specifiche funzionalità della distribuzione ibrida è necessario utilizzare Exchange Management Shell e il cmdlet **Set-HybridConfiguration**. Le seguenti funzionalità della distribuzione ibrida sono abilitate per impostazione predefinita dalla procedura guidata:

  - **Condivisione delle informazioni sulla disponibilità**   La funzionalità di condivisione delle informazioni sulla disponibilità abilita la condivisione delle informazioni del calendario tra gli utenti dell'organizzazione locale e dell'organizzazione di Exchange Online. La condivisione delle informazioni sulla disponibilità viene abilitata nell'ambito della configurazione della condivisione federata e delle relazioni organizzative per l'organizzazione locale e l'organizzazione di Exchange Online. Per ulteriori informazioni, vedere [Condivisione](https://technet.microsoft.com/it-it/library/dd638083\(v=exchg.150\)).

  - **MailTips**   MailTips sono messaggi informativi visualizzati agli utenti mentre compongono un messaggio. Abilitando gli avvisi messaggi nella distribuzione ibrida, i mittenti locali o di Exchange Online possono adattare i messaggi che scrivono in modo da evitare situazioni spiacevoli o rapporti di mancato recapito (NDR) tra le organizzazioni. Per ulteriori informazioni, vedere [MailTips](https://technet.microsoft.com/it-it/library/jj649091\(v=exchg.150\)).

  - **Archiviazione online**   L'archiviazione online consente all'organizzazione di Exchange Online di ospitare archivi di posta elettronica sia per gli utenti locali che per quelli di Exchange Online. Per ulteriori informazioni, vedere [Configurare il servizio di archiviazione di Exchange Online](http://go.microsoft.com/fwlink/p/?linkid=266565).

  - **Reindirizzamento di Outlook sul Web**   Il reindirizzamento di Outlook sul Web fornisce un singolo URL comune per accedere sia alle cassette postali locali sia a quelle di Exchange Online. I server Accesso client reindirizzano automaticamente le richieste per Outlook sul Web ai server Cassette postali locali, oppure forniscono agli utenti un collegamento alle proprie cassette postali nell'organizzazione di Exchange Online.

  - **Reindirizzamento di Exchange ActiveSync**  Quando si sposta una cassetta postale dall'organizzazione di Exchange locale in Exchange Online, tutti i client che richiedono l'accesso alla cassetta postale devono essere aggiornati per l'utilizzo di Exchange Online, inclusi i dispositivi di Exchange ActiveSync. La maggior parte dei client di Exchange ActiveSync verrà automaticamente riconfigurata quando la cassetta postale viene spostata in Exchange Online. Per ulteriori informazioni, vedere [Impostazioni dispositivo Exchange ActiveSync con distribuzioni ibride di Exchange](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Protezione dei messaggi**    La protezione dei messaggi consente il recapito sicuro dei messaggi tra l'organizzazione locale e l'organizzazione di Exchange Online, tramite il protocollo Transport Layer Security (TLS). L'organizzazione locale e l'organizzazione di Exchange Online si autenticano reciprocamente tramite certificati digitali, l'oggetto e l'intestazione dei messaggi di posta elettronica, e la formattazione dei messaggi RTF viene mantenuta fra le organizzazioni.

## Opzioni di configurazione ibrida

La procedura guidata di configurazione ibrida permette di selezionare opzioni specifiche in molte aree della distribuzione ibrida. Se si desidera aggiornare specifiche opzioni di configurazione ibrida dopo la configurazione della distribuzione ibrida, è possibile utilizzare la procedura guidata di configurazione ibrida o Exchange Management Shell per selezionare opzioni di configurazione diverse.

Nella tabella seguente sono illustrate le opzioni principali che vengono modificate e configurate dalla procedura guidata di configurazione ibrida.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Area di configurazione</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Domini</p></td>
<td><p>La procedura guidata aggiunge un dominio accettato all'organizzazione locale per il flusso di posta ibrido e le richieste di individuazione automatica per l'organizzazione basata su cloud. Questo dominio, chiamato <em>dominio di coesistenza</em>, viene aggiunto come dominio proxy secondario a tutti i criteri degli indirizzi di posta elettronica che utilizzano modelli <em>PrimarySmtpAddress</em> per i domini selezionati nella procedura guidata di configurazione ibrida. Per impostazione predefinita, questo dominio è &lt;domain&gt;.mail.onmicrosoft.com.</p>
<p>È possibile visualizzare il dominio accettato eseguendo il comando seguente in Exchange Management Shell di Exchange Online.</p>
<pre><code>Get-AcceptedDomain | FL DomainName, IsCoexistenceDomain</code></pre></td>
</tr>
<tr class="even">
<td><p>Certificato di protezione della posta elettronica</p></td>
<td><p>La procedura guidata richiede la selezione di un certificato specifico emesso da un'Autorità di certificazione (CA) di terze parti, che viene utilizzato per autenticare e proteggere i messaggi di posta elettronica scambiati tra l'organizzazione locale e l'organizzazione di Exchange Online.</p></td>
</tr>
<tr class="odd">
<td><p>Condivisione federata di Exchange</p></td>
<td><p>La procedura guidata controlla se esiste già una relazione di autenticazione OAuth o una relazione di trust federativa con il sistema di autenticazione di Azure Active Directory configurata per l'organizzazione locale. Se presente, la relazione di autenticazione OAuth o di trust federativa esistente verrà utilizzata per supportare la distribuzione ibrida. Se non presente, la procedura guidata configura l'autenticazione OAuth o crea una relazione di trust federativa per l'organizzazione locale con il sistema di autenticazione di Azure AD, a seconda del tipo di configurazione di Exchange locale. La procedura guidata, inoltre, aggiunge tutti i domini selezionati nella procedura guidata di configurazione ibrida alla relazione di trust federativa se necessario.</p>
<p>Oltre alla configurazione della relazione di autenticazione OAuth o di trust federativa, la procedura guidata crea e configura anche relazioni organizzative sia per l'organizzazione locale che per l'organizzazione di Exchange Online. Queste relazioni organizzative consentono alla procedura guidata di abilitare diverse funzionalità della distribuzione ibrida incluse la condivisione delle disponibilità, reindirizzamento Outlook sul Web e MailTips.</p></td>
</tr>
<tr class="even">
<td><p>Flusso di posta</p></td>
<td><p>La procedura guidata consente di selezionare e configurare i server Exchange per gestire il trasporto sicuro della posta tra l'organizzazione locale e l'organizzazione di Exchange Online. In Exchange 2010, si tratta di un server Trasporto Hub. In Exchange 2013, si tratta di un server Accesso client. In Exchange 2016 e versioni successive, si tratta di un server Cassette postali.</p>
<p>La procedura guidata configura l'organizzazione di Exchange locale e l'organizzazione di Exchange Online per il routing della posta ibrida. Configurando connettori di invio e ricezione nuovi ed esistenti nell'organizzazione locale, nonché connettori in ingresso e in uscita in Exchange Online, la procedura guidata consente di scegliere se i messaggi in uscita recapitati su Internet dall'organizzazione di Exchange Online verranno inviati direttamente al destinatario di posta esterno o instradati tramite i server Exchange locali inclusi nella distribuzione ibrida.</p>

> [!IMPORTANT]
> Il flusso di posta in arrivo viene controllato da record MX dell'organizzazione. I messaggi di posta elettronica Internet in arrivo per una distribuzione ibrida non vengono configurati dalla procedura guidata della configurazione ibrida.


</td>
</tr>
</tbody>
</table>


## Motore di configurazione ibrida

Il motore di configurazione ibrida esegue le azioni principali necessarie per configurare e aggiornare una distribuzione ibrida. Responsabile dell'elaborazione delle azioni del cmdlet `Update-HybridConfiguration`, il motore di configurazione ibrida compara lo stato dell'oggetto *HybridConfiguration*Active Directory con la corrente Exchange locale e le impostazioni di configurazione di Exchange Online quindi esegue le attività necessarie per impostare la configurazione della distribuzione con i parametri definiti nell'oggetto *HybridConfiguration*Active Directory. Se la corrente Exchange locale e la configurazione della distribuzione di Exchange Online corrispondono alle impostazioni definite nell'oggetto *HybridConfiguration*Active Directory, non viene effettuata nessuna modifica dal motore di configurazione ibrida sia alle organizzazioni Exchange Online o locali.

Quando si aggiorna una distribuzione ibrida esistente, il motore di configurazione ibrida esegue i passi seguenti:

1.  Il cmdlet *Update-HybridConfiguration* determina l'avvio del motore di configurazione ibrida.

2.  Il motore di configurazione ibrida legge lo "stato desiderato" archiviato nell'oggetto `HybridConfiguration`Active Directory.

3.  Il motore di configurazione ibrida rileva i dati di topologia della configurazione corrente dall'organizzazione di Exchange locale.

4.  Il motore di configurazione ibrida rileva i dati di topologia e la configurazione corrente dall'organizzazione di Exchange Online.

5.  In base allo stato desiderato, ai dati di topologia e della configurazione corrente, il motore di configurazione ibrida determina la differenza tra l'organizzazione di Exchange locale e l'organizzazione di Exchange Online e quindi esegue le attività di configurazione necessarie per ottenere lo stato desiderato.

La figura seguente mostra un sommario di come il motore di configurazione ibrida recupera e modifica le impostazioni di configurazione dei server Exchange locali e di Exchange Online durante il processo di distribuzione ibrida.

![Flusso del motore di configurazione ibrida](images/Hh529921.7e01b239-b978-4377-9eac-aa5bc4561866(EXCHG.150).gif "Flusso del motore di configurazione ibrida")

