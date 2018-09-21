---
title: 'Sposta cass. con script Prepare MoveRequest.ps1 in Shell: Exchange 2013 Help'
TOCTitle: Prepara le cassette postali per gli spostamenti tra foreste utilizzando lo script Prepare MoveRequest.ps1 in Shell
ms:assetid: 2cea59fb-69b7-4a2f-833f-de4d93cf1810
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee861103(v=EXCHG.150)
ms:contentKeyID: 50480245
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Prepara le cassette postali per gli spostamenti tra foreste utilizzando lo script Prepare MoveRequest.ps1 in Shell

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-11-22_

**Riepilogo:**  informazioni su come gestire spostamenti delle cassette postali tra foreste e migrazioni in Exchange 2013 utilizzando lo script Prepare MoveRequest.ps1 in Exchange Management Shell.

Microsoft Exchange 2013 supporta spostamenti e migrazioni utilizzando i cmdlet **New-MoveRequest** e **New-MigrationBatch** . È inoltre possibile spostare la cassetta postale tramite interfaccia di amministrazione di Exchange (EAC). È possibile spostare un Exchange 2010 o mailbox Exchange 2013 da un insieme di strutture Exchange origine a una foresta di destinazione Exchange 2013.

Per eseguire i cmdlet **New-MoveRequest** e **New-MigrationBatch**, è necessario che nella foresta di Exchange di destinazione sia disponibile un utente di posta elettronica dotato di un insieme minimo di attributi di Active Directory obbligatori.

Lo script Windows PowerShell campione descritto in questo argomento supporta tale attività tramite la sincronizzazione degli utenti di cassette postali da una foresta di Exchange 2013 di origine a foreste di Exchange 2013 di destinazione come utenti abilitati alla posta elettronica. Lo script copia gli attributi di Active Directory degli utenti di cassette postali della foresta di origine nella foresta di destinazione e utilizza il cmdlet **Update-Recipient** per abilitare gli oggetti di destinazione negli utenti abilitati alla posta elettronica.

Per ulteriori informazioni su come utilizzare e scrivere gli script, vedere [Scripting con Exchange Management Shell](https://technet.microsoft.com/it-it/library/bb123798\(v=exchg.150\)). Per ulteriori informazioni sulla preparazione per gli spostamenti tra foreste, vedere [Preparare le cassette postali per le richieste di spostamento tra foreste](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle richieste di spostamento remoto, vedere [Gestire spostamenti locali](manage-on-premises-moves-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Individuare lo script nel percorso seguente: Program Files\\Microsoft\\Exchange Server\\V15\\Scripts

  - Per eseguire lo script campione, è necessario disporre di quanto riportato di seguito:
    
      - Una Exchange foresta di origine, dove la cassetta postale si trova attualmente. Può trattarsi di una cassetta postale di Exchange 2010 o Exchange 2013.
    
      - Una foresta di destinazione con installato Exchange 2013, in cui verrà spostata la cassetta di postale.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso dello script Prepare-MoveRequest.ps1 per la preparazione delle cassette postali per gli spostamenti tra foreste

Eseguire lo script da Shell su un ruolo del server su cui è installato Exchange 2013 nella foresta di Exchange 2013 di destinazione. Lo script consente di copiare gli attributi delle cassette postali dalla foresta di origine.

Per assegnare credenziali di autenticazione specifiche per il controller di dominio della foresta remota, è innanzitutto necessario eseguire il cmdlet di **Get-Credential**Windows PowerShell e archiviare l'input dell'utente in una variabile temporanea. Quando si esegue il cmdlet **Get-Credential** , il cmdlet richiede il nome utente e la password dell'account utilizzato durante l'autenticazione con il controller di dominio della foresta remota. È possibile utilizzare la variabile temporanea quindi nello script per la preparazione MoveRequest.ps1. Per ulteriori informazioni sul cmdlet **Get-Credential** , vedere [Get-Credential](https://go.microsoft.com/fwlink/p/?linkid=142122).


> [!NOTE]
> Accertarsi di utilizzare due credenziali distinte per la foresta locale e la foresta remota quando si richiama lo script.



1.  Utilizzare i seguenti comandi per ottenere le credenziali per la foresta locale e la foresta remota.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  Eseguire i seguenti comandi per passare le informazioni sulle credenziali ai parametri *LocalForestCredential* e *RemoteForestCredential* nello script Prepare-MoveRequest.ps1.
    
        Prepare-MoveRequest.ps1 -Identity JohnSmith@Fabrikan.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials

## Gruppo di parametri dello script

Nella tabella seguente, è riportato il gruppo di parametri per lo script.

### Gruppo di parametri dello script Prepare-MoveRequest.ps1

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Il parametro <em>Identity</em> identifica in modo univoco una cassetta postale nella foresta di origine. L'identità può essere una qualsiasi tra le seguenti:</p>
<ul>
<li><p>Nome comune (CN)</p></li>
<li><p>Alias</p></li>
<li><p>Proprietà <strong>proxyAddress</strong></p></li>
<li><p>Proprietà <strong>objectGuid</strong></p></li>
<li><p>Proprietà <strong>DisplayName</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>RemoteForestCredential</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Il parametro <em>RemoteForestCredential</em> consente di specificare l'amministratore con le autorizzazioni per copiare dati dall'Active Directory della foresta di origine.</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoteForestDomainController</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Il parametro <em>RemoteForestDomainController</em> specifica un controller di dominio nella foresta di origine in cui si trova la cassetta postale.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableEmailAddressPolicy</em></p></td>
<td><p>Opzionale</p></td>
<td><p>Il parametro <em>DisableEmailAddressPolicy</em> indica se è necessario disabilitare il protocollo EAP (Extensible Authentication Protocol) durante la creazione di un oggetto <strong>MailUser</strong> nella foresta di destinazione.</p>
<p>Quando si specifica questo parametro, il protocollo EAP nella foresta di destinazione non verrà applicato.</p>

> [!NOTE]
> Quando si specifica questo parametro, l'oggetto <STRONG>MailUser</STRONG> non avrà la mappatura degli indirizzi di posta elettronica contrassegnata nel dominio della foresta locale. Questo viene generalmente contrassegnato da EAP.


</td>
</tr>
<tr class="odd">
<td><p><em>LinkedMailUser</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>L'opzione <em>LinkedMailUser</em> indica se creare o meno un oggetto MailUser associato nella foresta locale per l'utente della cassetta postale nella foresta remota.</p>
<p>Se viene fornita l'opzione, lo script crea un oggetto <strong>MailUser</strong> di destinazione associato alla cassetta postale di origine. Se l'opzione viene omessa, lo script crea un oggetto <strong>MailUser</strong>di destinazione regolare.</p></td>
</tr>
<tr class="even">
<td><p><em>LocalForestCredential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>LocalForestCredential</em> consente di specificare l'amministratore con autorizzazioni a scrivere dati nell'Active Directory della foresta di destinazione.</p>
<p>Si consiglia di specificare in modo esplicito questo parametro per evitare problemi di autorizzazioni Active Directory.</p>
<p>Se la foresta remota e quella locale hanno una relazione attendibile configurata, non utilizzare un account utente dalla foresta remota come credenziale della foresta locale, anche se l'account utente remoto potrebbe disporre delle autorizzazioni per modificare l'Active Directory nella foresta locale.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalForestDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>LocalForestDomainController</em> indica un controller di dominio nella foresta di destinazione in cui verrà creato l'utente abilitato alla posta elettronica.</p>
<p>Si consiglia di specificare tale parametro per evitare eventuali problemi di ritardo nella replica dei controller di dominio nella foresta locale che potrebbero verificarsi se si seleziona un controllo di dominio casuale.</p></td>
</tr>
<tr class="even">
<td><p><em>MailboxDeliveryDomain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>MailboxDeliveryDomain</em> indica un dominio autorevole della foresta di origine che consente allo script di selezionare la proprietà <strong>proxyAddress</strong> dell'utente della cassetta postale di origine corretto come proprietà <strong>targetAddress</strong> dell'utente abilitato alla posta elettronica di destinazione.</p>
<p>Per impostazione predefinita, l'indirizzo SMTP principale dell'utente della cassetta postale di origine è configurato come proprietà <strong>targetAddress</strong> dell'utente abilitato alla posta elettronica di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>OverWriteLocalObject</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>OverWriteLocalObject</em> è utilizzato per utenti creati dagli strumenti di migrazione di Active Directory. Le proprietà vengono copiate dal contatto di posta esistente al nuovo utente appena creato. Tuttavia, dopo questa copia, anche lo script copia le proprietà dall'utente nella foresta di origine all'utente di posta appena creato.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetMailUserOU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>TargetMailuserOU</em> indica l'unità organizzativa sotto cui verrà creato l'utente abilitato alla posta elettronica di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>UseLocalObject</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Il parametro <em>UseLocalObject</em> indica se convertire l'oggetto locale esistente nell'utente abilitato alla posta elettronica di destinazione obbligatorio se lo script rileva un oggetto nella foresta locale che va in conflitto con l'utente abilitato alla posta elettronica da creare.</p></td>
</tr>
</tbody>
</table>


## Esempi

In questa sezione, sono riportati diversi esempi su come utilizzare lo script Prepare-MoveRequest.ps1.

## Esempio: Singolo utente abilitato alla posta elettronica associato

In questo esempio, viene predisposto un singolo utente abilitato alla posta elettronica associato nella foresta locale, quando è presente un trust tra foreste tra le foreste remota e locale.

1.  Utilizzare i seguenti comandi per ottenere le credenziali per la foresta locale e la foresta remota.
    
        $LocalCredentials = Get-Credential
        $RemoteCredentials = Get-Credential

2.  Eseguire il seguente comando per passare le informazioni sulle credenziali ai parametri *LocalForestCredential* e *RemoteForestCredential* nello script Prepare-MoveRequest.ps1.
    
        Prepare-MoveRequest.ps1 -Identity JamesAlvord@Contoso.com -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $RemoteCredentials -LocalForestDomainController DC001.Contoso.com -LocalForestCredential $LocalCredentials -LinkedMailUser 

## Esempio: Pipelining

Questo esempio supporta il pipelining se si fornisce un elenco di identità delle cassette postali.

1.  Eseguire il comando riportato di seguito.
    
    ```powershell
$UserCredentials = Get-Credential
```

2.  Utilizzare il seguente comando per passare le informazioni sulle credenziali al parametro *RemoteForestCredential* allo script Prepare-MoveRequest.ps1.
    
        "IanP@Contoso.com", "JoeAn@Contoso.com" | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## Esempio: Utilizzare un file con estensione CSV per creare in un'unica operazione gli utenti abilitati alla posta elettronica

È possibile generare un file con estensione CSV contenente un elenco di identità di cassette postali derivanti dalla foresta di origine che consente di eseguire il pipeling del contenuto di questo file nello script per creare in un'unica operazione gli utenti abilitati alla posta elettronica di destinazione.

Ad esempio, il contenuto del file .csv può essere:

Identità

Ian@contoso.com

John@contoso.com

Cindy@contoso.com

In questo esempio, viene richiamato un file con estensione CSV per creare in un'unica operazione gli utenti abilitati alla posta elettronica di destinazione.

1.  Utilizzare il seguente comando per ottenere le credenziali per la foresta remota.
    
    ```powershell
$UserCredentials = Get-Credential
```

2.  Utilizzare il seguente comando per passare le informazioni sulle credenziali al parametro *RemoteForestCredential* allo script Prepare-MoveRequest.ps1.
    
        Import-Csv Test.csv | Prepare-MoveRequest.ps1 -RemoteForestDomainController DC001.Fabrikam.com -RemoteForestCredential $UserCredentials

## Comportamento di script per l'oggetto di destinazione

In questa sezione, viene illustrato il modo in cui lo script opera relativamente a diversi scenari per gli oggetti di destinazione.

## Duplicazione dell'oggetto abilitato alla posta elettronica di destinazione

Quando lo script tenta di creare un utente abilitato alla posta elettronica di destinazione dall'utente di cassetta postale di origine e rileva un oggetto abilitato alla posta elettronica duplicato, utilizza la seguente logica:

  - Se l'attributo **masterAccountSid** dell'utente della cassetta postale di origine corrisponde a qualsiasi attributo **objectSid** o **masterAccountSid** dell'oggetto di destinazione:
    
      - Se l'oggetto di destinazione non è abilitato alla posta elettronica, lo script restituisce un errore in quanto non supporta la conversione di un oggetto non abilitato alla posta elettronica in un utente abilitato alla posta elettronica.
    
      - Se l'oggetto di destinazione è abilitato alla posta elettronica, l'oggetto di destinazione è un duplicato.

  - Se un indirizzo nelle proprietà **proxyAddress** (solo smtp/x500) dell'utente della cassetta postale di origine corrisponde a un indirizzo nelle proprietà **proxyAddress** (solo smtp/x500) dell'oggetto di destinazione, allora l'oggetto di destinazione è un duplicato.

Lo script informa l'utente relativamente agli oggetti duplicati.

Se l'oggetto abilitato alla posta elettronica di destinazione è un contatto o un utente abilitato alla posta elettronica, creato molto probabilmente mediante una distribuzione della sincronizzazione dell'elenco indirizzi globale (GAL) (basata su Identity Lifecycle Management 2007 Service Pack 1) tra foreste, allora l'utente può eseguire nuovamente lo script con il parametro *UseLocalObject* per utilizzare l'oggetto abilitato alla posta elettronica di destinazione per la migrazione delle cassette postali.

## Utente abilitato alla posta elettronica

Se l'oggetto di destinazione è un utente abilitato alla posta elettronica, lo script copia i seguenti attributi dall'utente di cassetta postale di origine all'utente abilitato alla posta elettronica di destinazione:

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

Se è impostato il parametro *LinkedMailUser*, lo script copia l'attributo **objectSid**/**masterAccountSid** di origine.

## Contatto abilitato per la posta elettronica

Se l'oggetto di destinazione è un contatto abilitato per la posta elettronica, lo script elimina il contatto esistente e copia tutti i relativi attributi in un nuovo utente abilitato alla posta elettronica. Lo script copia anche i seguenti attributi dall'utente di cassetta postale di origine:

  - **msExchMailboxGUID**

  - **msExchArchiveGUID**

  - **msExchArchiveName**

  - **sAMAccountName**

  - **userAccountControl**(impostato su 514 //equivalente a 0x202, ACCOUNTDISABLE | NORMAL\_ACCOUNT)

  - **userPrincipalName**

Se è impostato il parametro *LinkedMailUser*, lo script copia l'attributo **objectSid**/**masterAccountSid** di origine.

## Attributo LegacyExchangeDN

Quando viene chiamato il cmdlet **Update-Recipient** per convertire l'oggetto di destinazione in un utente abilitato alla posta, viene generato un nuovo attributo **LegacyExchangeDN** per utente abilitati alla posta elettronica di destinazione. Lo script copia l'attributo **LegacyExchangeDN** dell'utente abilitato alla posta destinazione come un x500 indirizzo alle proprietà **proxyAddress** dell'utente della cassetta postale di origine.

