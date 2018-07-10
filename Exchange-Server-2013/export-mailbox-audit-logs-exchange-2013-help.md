---
title: 'Esportare registri di controllo delle cassette postali: Exchange 2013 Help'
TOCTitle: Esportare registri di controllo delle cassette postali
ms:assetid: b458a95a-3321-4647-8884-cf97f8e7186a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150552(v=EXCHG.150)
ms:contentKeyID: 50479782
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esportare registri di controllo delle cassette postali

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-04-07_

Quando si abilita il controllo per una cassetta postale, in Microsoft Exchange vengono registrate informazioni nel *registro di controllo della cassetta postale* ogni qualvolta un utente diverso dal proprietario accede alla cassetta postale. Ogni voce del registro include informazioni relative a chi ha effettuato l'accesso alla cassetta postale e quando, alle azioni eseguite dall'utente non proprietario e al fatto che l'azione abbia avuto esito positivo. Le voci nel registro di controllo delle cassette postali vengono conservate per 90 giorni per impostazione predefinita. È possibile utilizzare il registro di controllo della cassetta postale per determinare se un utente diverso dal proprietario ha effettuato l'accesso a una cassetta postale.

Quando si esportano voci dal log di controllo della cassetta postale, in Microsoft Exchange le voci vengono salvate in un file XML e il file viene allegato a un messaggio di posta elettronica inviato ai destinatari specificati.

**Sommario**

Prima di iniziare

Configurare la registrazione di controllo della cassetta postale

Esportare i registri di controllo della cassetta postale

Visualizzare il registro di controllo della cassetta postale

Ulteriori informazioni

## Informazioni preliminari

  - Tempo stimato per il completamento di ciascuna procedura: il tempo è variabile. In Exchange Online il registro di controllo della cassetta postale viene inviato entro pochi giorni dopo l'esportazione.

  - In Exchange Online, è necessario utilizzare Windows PowerShell remoto per eseguire molte delle procedure in questo argomento. Per ulteriori informazioni, vedere [Connessione a Exchange Online tramite Remote PowerShell](https://technet.microsoft.com/it-it/library/jj984289\(v=exchg.150\)).

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Configurare la registrazione di controllo della cassetta postale

È necessario abilitare la registrazione di controllo della cassetta postale per ogni cassetta postale che si desidera controllare prima di poter esportare e visualizzare i registri di controllo della cassetta postale. È inoltre necessario configurare Microsoft Outlook Web App per consentire agli allegati XML di utilizzare Outlook Web App per accedere al registro di controllo della cassetta postale.

## Passaggio 1: Abilitare la registrazione di controllo della cassetta postale

È necessario abilitare la registrazione di controllo della cassetta postale per ogni cassetta postale per la quale si desidera eseguire un rapporto di accesso non proprietario. Se la registrazione di controllo non è abilitata per una cassetta postale, non si otterrà alcun risultato per tale cassetta dall'esportazione del registro di controllo della cassetta postale.

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo delle cassette postali" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Per abilitare la registrazione di controllo della cassetta postale per una sola cassetta postale, eseguire il comando in Shell:

    Set-Mailbox <Identity> -AuditEnabled $true

per abilitare la registrazione di controllo su tutte le cassette postali degli utenti di un'organizzazione, eseguire i comandi riportati di seguito.
```
$UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
```
```
$UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}
```

## Passaggio 2: Configurare Outlook Web App per consentire gli allegati XML

Quando si esporta il registro di controllo della cassetta postale, in Microsoft Exchange il registro di controllo, un file XML, viene allegato a un messaggio di posta elettronica. Per impostazione predefinita, tuttavia, in Outlook Web App gli allegati XML sono bloccati. Per accedere al registro di controllo esportato, utilizzare Microsoft Outlook per configurare Outlook Web App all'abilitazione degli allegati XML.

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di Outlook Web App" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Eseguire le procedure seguenti per consentire gli allegati XML in Outlook Web App. In Exchange Server 2013, utilizzare il valore `Default` per il parametro *Identity* .

1.  Eseguire il comando seguente per aggiungere all'elenco dei tipi di file consentiti in Outlook Web App XML.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -AllowedFileTypes @{add='.xml'}

2.  Eseguire il comando seguente per rimuovere XML dall'elenco dei tipi di file bloccati in Outlook Web App.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -BlockedFileTypes @{remove='.xml'}

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver configurato correttamente la registrazione di controllo della cassetta postale, eseguire le operazioni seguenti:

1.  eseguire il comando seguente per verificare la configurazione corretta della registrazione di controllo per le cassette postali.
    
        Get-Mailbox | FL Name,AuditEnabled
    
    Il valore `True` impostato per la proprietà *AuditEnabled* consente di verificare se la registrazione di controllo è abilitata.

2.  Eseguire il comando seguente per verificare che gli allegati XML siano consentiti in Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty AllowedFileTypes
    
    Verificare che `.xml` sia incluso nell'elenco dei tipi di file consentiti.

3.  Eseguire il comando seguente per verificare che gli allegati XML siano stati rimossi dall'elenco di file bloccati in Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty BlockedFileTypes
    
    Verificare che `.xml` non è incluso nell'elenco dei tipi di file bloccati.

Inizio pagina

## Esportare i registri di controllo della cassetta postale

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo dell'amministratore in sola visualizzazione" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

1.  Nell'interfaccia di amministrazione di Exchange (EAC) accedere a **Gestione conformità** \> **controllo**.

2.  Fare clic su **Esporta registri di controllo della cassetta postale**.

3.  Configurare i criteri di ricerca seguenti per l'esportazione delle voci dal registro di controllo della cassetta postale:
    
      - **Date di inizio e di fine**   Selezionare l'intervallo di date per le voci da includere nel file esportato.
    
      - **Cassette postali di cui cercare i registri di controllo**   Selezionare le cassette postali per cui recuperare le voci del registro di controllo.
    
      - **Tipo di accesso non proprietario**   Selezionare una delle opzioni seguenti per definire il tipo di accesso non proprietario per cui recuperare le voci:
        
          - **Tutti i non proprietari**   Consente di cercare l'accesso da parte di amministratori e utenti delegati all'interno dell'organizzazione e da parte di amministratori del datacenter Microsoft in Exchange Online.
        
          - **Utenti esterni**   Consente di cercare l'accesso solo da parte di amministratori del datacenter Microsoft.
        
          - **Amministratori e utenti delegati**   Consente di cercare l'accesso da parte di amministratori e utenti delegati all'interno dell'organizzazione.
        
          - **Amministratori**   Consente di cercare l'accesso da parte degli amministratori dell'organizzazione.
    
      - **Destinatari**   Selezionare gli utenti ai quali inviare il registro di controllo della cassetta postale.

4.  Fare clic su **Esporta**.
    
    In Microsoft Exchange vengono recuperate le voci del registro di controllo della cassetta postale che soddisfano i criteri di ricerca, tali voci vengono salvate in un file denominato SearchResult.xml, quindi il file XML viene allegato a un messaggio di posta elettronica inviato ai destinatari specificati.

## Come verificare se l'operazione ha avuto esito positivo

Accedere alla cassetta postale di cui è stato inviato il Registro di controllo delle cassette postali. Se è stata esportata nel Registro di controllo, si riceverà un messaggio inviato da Exchange. In Exchange Online, potrebbe richiedere qualche giorno a ricevere questo messaggio. Il Registro di controllo delle cassette postali (denominato SearchResult) verrà allegato al messaggio. Se è stato configurato correttamente Outlook Web App per consentire gli allegati XML, è possibile scaricare il file XML associato.

Inizio pagina

## Visualizzare il registro di controllo della cassetta postale

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo dell'amministratore in sola visualizzazione" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

Per salvare e visualizzare il file SearchResult XML:

1.  Accedere alla cassetta postale a cui è stato inviato il registro di controllo della cassetta postale.

2.  Nella Posta in arrivo aprire il messaggio con il file XML allegato inviato da Microsoft Exchange. Notare che il corpo del messaggio di posta elettronica contiene i criteri di ricerca.

3.  Fare clic sull'allegato e selezionare questa opzione per scaricare il file XML.

4.  Aprire il SearchResult in Microsoft Excel.

Inizio pagina

## Ulteriori informazioni

  - **Le voci nella cassetta postale del Registro di controllo**   Nell'esempio seguente viene illustrata una voce del Registro di controllo delle cassette postali contenuta nel file SearchResult. Ogni voce preceduto dal tag XML **\< evento \>** e termina con il **\< / evento \>** tag XML. Questa voce indica che l'amministratore cancellati il messaggio con l'oggetto "**notifica di conservazione per controversia conservazione**" dalla cartella elementi ripristinabili nella cassetta postale di David il 30 aprile 2010.
    
        <Event MailboxGuid="6d4fbdae-e3ae-4530-8d0b-f62a14687939" 
          Owner="PPLNSL-dom\david50001-1363917750" 
          LastAccessed="2010-04-30T11:01:55.140625-07:00" 
          Operation="HardDelete" 
          OperationResult="Succeeded" 
          LogonType="Admin"
         FolderId="0000000073098C3277988F4CB882F5B82EBF64610100A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000"
          FolderPathName="\Recoverable Items\Deletions"
          ClientInfoString="Client=OWA;Action=ViaProxy" 
          ClientIPAddress="10.196.241.168" 
          InternalLogonType="Owner"
          MailboxOwnerUPN="david@contoso.com"
          MailboxOwnerSid="S-1-5-21-290112810-296651436-1966561949-1151" 
          CrossMailboxOperation="false" 
          LogonUserDN="Administrator"
          LogonUserSid="S-1-5-21-290112810-296651436-1966561949-1149">
          <SourceItems>
           <ItemId="0000000073098C3277988F4CB882F5B82EBF64610700A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000A7C317F68C24304BBD18ABE1F185E79B00000026BD540"
            Subject="Notification of litigation hold"
            FolderPathName="\Recoverable Items\Deletions" /> 
          </SourceItems>
        </Event>

  - **Campi utili nella cassetta postale del Registro di controllo**   Ecco una descrizione dei campi utili nel Registro di controllo delle cassette postali. Consentano di identificare le informazioni specifiche relative a ogni istanza di accesso non proprietario di una cassetta postale.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Campo</th>
    <th>Descrizione</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Owner</strong></p></td>
    <td><p>Proprietario della cassetta postale a cui ha effettuato l'accesso un utente non-proprietario.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>LastAccessed</strong></p></td>
    <td><p>Data e ora in cui è stato effettuato l'accesso alla cassetta postale.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Operation</strong></p></td>
    <td><p>Azione eseguita dall'utente non proprietario. Per ulteriori informazioni, vedere la sezione &quot;Elementi registrati nel registro di controllo della cassetta postale&quot; in <a href="https://technet.microsoft.com/it-it/library/jj156300(v=exchg.150)">Ulteriori informazioni su come eseguire un rapporto di accesso non proprietario della cassetta postale</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OperationResult</strong></p></td>
    <td><p>Esito positivo o negativo dell'azione eseguita dall'utente non proprietario.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonType</strong></p></td>
    <td><p>Tipo di accesso non proprietario. Sono inclusi amministratore, delegato ed esterno.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>FolderPathName</strong></p></td>
    <td><p>Nome della cartella che conteneva il messaggio su cui ha agito l'utente non proprietario.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>ClientInfoString</strong></p></td>
    <td><p>Informazioni sul client di posta elettronica utilizzato dall'utente non proprietario per accedere alla cassetta postale.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ClientIPAddress</strong></p></td>
    <td><p>Indirizzo IP del computer utilizzato dall'utente non proprietario per accedere alla cassetta postale.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>InternalLogonType</strong></p></td>
    <td><p>Tipo di accesso dell'account utilizzato dall'utente non proprietario per accedere alla cassetta postale.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>MailboxOwnerUPN</strong></p></td>
    <td><p>Indirizzo di posta elettronica del proprietario della cassetta postale.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonUserDN</strong></p></td>
    <td><p>Nome visualizzato dell'utente non proprietario.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Subject</strong></p></td>
    <td><p>Riga dell'oggetto del messaggio di posta elettronica su cui ha agito l'utente non proprietario.</p></td>
    </tr>
    </tbody>
    </table>
    
    Inizio pagina

