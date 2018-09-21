---
title: 'Attiva/disattiva posta per utente posta elettronica: Exchange 2013 Help'
TOCTitle: Attivare o disattivare la posta elettronica per un utente di posta elettronica
ms:assetid: 1e2571d4-ff84-4fda-bb1d-825e96e1bd26
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa996598(v=EXCHG.150)
ms:contentKeyID: 50555548
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attivare o disattivare la posta elettronica per un utente di posta elettronica

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-11-14_

È possibile disabilitare la posta elettronica per un utente di posta esistente nell'organizzazione di Exchange. Quando si disabilita la posta elettronica per un utente di posta, questo viene rimosso da Exchange e dalla rubrica. Se l'utente di posta elettronica è un membro di un gruppo di distribuzione, non riceverà più la posta inviata al gruppo. Inoltre, gli attrtibuti di Exchange vengono rimossi dall'oggetto utente in Active Directory, ma l'oggetto utente e i relativi attributi non Exchange (come le informazioni relative all'organizzazione e ai contatti) vengono conservate in Active Directory.

Dopo aver disabilitato la posta elettronica per un utente di posta, è possibile abilitare di nuovo l'utente all'utilizzo della posta tramite il cmdlet **Enable-MailUser** in Shell. È inoltre possibile utilizzare questo cmdlet per abilitare all'utilizzo della posta qualsiasi utente di Active Directory.


> [!NOTE]
> Gli utenti di posta (definiti anche <EM>utenti abilitati alla posta</EM>) sono diversi dagli utenti che hanno una cassetta postale nell'organizzazione. La differenza principale è che gli utenti di posta rappresentano gli utenti all'esterno dell'organizzazione di Exchange che hanno un indirizzo di posta esterno. Non hanno una cassetta postale nell'organizzazione. Per ulteriori informazioni sulle differenze tra gli utenti che hanno cassette postali nell'organizzazione e gli utenti di posta, vedere <A href="recipients-exchange-2013-help.md">Destinatari</A>.



Per le altre attività di gestione relative agli utenti di posta, vedere [Gestire gli utenti di posta](https://docs.microsoft.com/it-it/exchange/recipients-in-exchange-online/manage-mail-users).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Utenti di posta elettronica" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Disabilitazione della posta per un utente abilitato alla posta

Come indicato in precedenza, quando viene disabilitata la posta elettronica per un utente di posta, gli attributi di Exchange vengono eliminati dall'oggetto utente di posta corrispondente di Active Directory, ma l'utente viene conservato. L'utente di posta viene eliminato dall'elenco degli utenti di posta dell'interfaccia di amministrazione di Exchange, ma è possibile visualizzare e gestire l'oggetto contatto corrispondente di Active Directory utilizzando Utenti e computer di Active Directory o utilizzando i cmdlet**Get-MailUser** e **Set-Set-MailUser** in Shell.

## Utilizzo dell'interfaccia di amministrazione di Exchange per disabilitare un utente di posta

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**.

2.  Nell'elenco dei contatti, fare clic sull'utente di posta per il quale si desidera disabilitare la posta elettronica.

3.  Fare clic su **Altro**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni") quindi fare clic su **Disabilita**.

4.  Viene visualizzato un avviso di conferma per la rimozione del database delle cassette postali. Fare clic su **Sì** per disabilitarlo.

L'utente di posta verrà rimosso dall'elenco dei contatti.

## Utilizzo di Shell per disabilitare un utente di posta all'utilizzo della posta elettronica

In questo esempio viene disabilitata la posta per l'utente Yan Li abilitato alla posta.

    Disable-MailUser -Identity "Yan Li"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Disable-MailUser](https://technet.microsoft.com/it-it/library/aa998578\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che la posta elettronica sia stata disabilitata correttamente per un utente di posta, effettuare una delle seguenti operazioni:

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti** e verificare che l'utente di posta non vi sia più incluso.

2.  In Utenti e computer di Active Directory, fare clic con il pulsante destro del mouse sull'utente, quindi scegliere **Proprietà**. Sulla scheda **Generale**, si noti che la casella **Posta elettronica** è vuota. Ciò conferma che l'utente di posta non è abilitato alla posta elettronica.

3.  In Shell, utilizzare il seguente comando.
    
        Get-MailUser
    
    L'utente di posta per il quale è stato disabilitato l'utilizzo della posta elettronica non verrà restituito nei risultati poiché questo cmdlet restituisce solo gli utenti abilitati all'utilizzo della posta.

4.  In Shell, utilizzare il seguente comando.
    
        Get-User
    
    L'utente di posta che è stato disabilitato all'utilizzo della posta elettronica viene restituito nei risultati poiché questo cmdlet restituisce tutti gli oggetti utente di Active Directory.

## Abilitazione alla posta degli utenti tramite Shell

Utilizzare il cmdlet **Enable-MailUser** per abilitare all'utilizzo della posta gli utenti esistenti di Active Directory. È possibile abilitare all'utilizzo della posta un singolo utente oppure utilizzare un file CSV per abilitare all'utilizzo della posta più utenti.

## Utilizzo di Shell per abilitare alla posta un singolo utente

In questo esempio l'utente Sanjay Shah viene abilitato all'utilizzo della posta elettronica. È necessario fornire un indirizzo di posta elettronica esterno.

    Enable-MailUser -Identity "Sanjay Shah" -ExternalEmailAddress renev@tailspintoys.com

## Utilizzo di Shell e di un file CSV per abilitare alla posta più utenti

Quando si abilitano all'utilizzo della posta gli utenti in blocco, innanzitutto si esporta l'elenco degli utenti che non sono abilitati all'utilizzo della posta su un file CSV (valori separati da virgole), poi si aggiungono gli indirizzi di posta elettronica esterni al file CSV utilizzando un editor di testo, come Blocco note o un'applicazione che utilizza fogli elettronici come Microsoft Excel. Successivamente si utilizza il file CSV aggiornato nel comando Shell per abilitare all'utilizzo della posta gli utenti elencati nel file CSV.

1.  Utilizzare il comando seguente per esportare un elenco di utenti esistenti che non sono abilitati all'utilizzo della posta o che non hanno una cassetta postale nell'organizzazione su un file sul desktop dell'amministratore denominato UsersToMailEnable.csv.
    
        Get-User | Where { $_.RecipientType -eq "User" } | Out-File "C:\Users\Administrator\Desktop\UsersToMailEnable.csv"
    
    Il file ottenuto sarà simile al seguente.
    
        Name            RecipientType
        ----            -------------
        Guest           User
        krbtgt          User
        RMS_SERVICE     User
        David Pelton    User
        Kim Akers       User
        Janet Schorr    User
        Jeffrey Zang    User
        Spencer Low     User
        Toni Poe        User
        ...

2.  Apportare le modifiche seguenti al file CSV:
    
      - Eliminare tutti gli utenti che non si desidera abilitare all'utilizzo della posta dal file CSV. Ad esempio, si dovrebbero eliminare i primi tre elementi nell'esempio precedente perchè sono account predefiniti del sistema.
    
      - Eliminare la colonna **RecipientType** e tutte le istanze di `User`.
    
      - Aggiungere l'intestazione di colonna **EmailAddress** quindi aggiungere un indirizzo di posta elettronica per ciascun utente nel file. Il nome e l'indirizzo esterno di posta elettronica per ciascun utente deve essere separato da una virgola.
    
    Il file CSV aggiornato dovrebbe essere simile al seguente.
    
        Name,EmailAddress
        David Pelton,davidp@contoso.com
        Kim Akers,kakers@tailspintoys.com
        Janet Schorr,janet.schorr@adatum.com
        Jeffrey Zang,jzang@tailspintoys.com
        Spencer Low,spencerl@fouthcoffee.com
        Toni Poe,tonip@contoso.com
        ...

3.  Eseguire questo comando per utilizzare i dati nel file CSV per abilitare all'utilizzo della posta gli utenti elencati nel file.
    
        Import-CSV "C:\Users\Administrator\Desktop\UsersToMailEnable.csv" | ForEach-Object {Enable-MailUser -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    I risultati del comando visualizzano le informazioni sui nuovi utenti abilitati alla posta elettronica.

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver correttamente abilitato alla posta gli utenti di Active Directory, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**. I nuovi utenti di posta elettronica vengono visualizzati nell'elenco dei contatti. In **Tipo di contatto** il tipo è **Utente di posta**.
    

    > [!NOTE]
    > Per visualizzare i nuovi utenti di posta elettronica potrebbe essere necessario fare clic su <STRONG>Aggiorna</STRONG><IMG title="Icona Aggiorna" alt="Icona Aggiorna" src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif">.



  - In Shell utilizzare il comando seguente per visualizzare le informazioni sui nuovi utenti di posta.
    
        Get-MailUser | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

