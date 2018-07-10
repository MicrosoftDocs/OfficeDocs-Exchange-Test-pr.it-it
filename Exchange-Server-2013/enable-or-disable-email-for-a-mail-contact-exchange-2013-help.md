---
title: 'Attivare o disattivare la posta elettronica per un contatto di posta elettronica: Exchange 2013 Help'
TOCTitle: Attivare o disattivare la posta elettronica per un contatto di posta elettronica
ms:assetid: ca47441f-1aa4-4958-aba5-18d51e59837e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124552(v=EXCHG.150)
ms:contentKeyID: 50555681
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attivare o disattivare la posta elettronica per un contatto di posta elettronica

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-12-05_

È possibile disabilitare la posta elettronica per un contatto di posta esistente nell'organizzazione di Exchange. Quando si disabilita la posta elettronica per un contatto, questo viene rimosso da Exchange e dalla rubrica dell'organizzazione. Se il contatto di posta è un membro di un gruppo di distribuzione, non riceverà più i messaggi inviati al gruppo. Gli attributi di Exchange verranno inoltre rimossi dall'oggetto contatto abilitato alla posta in Active Directory, ma il contatto e i relativi attributi non di Exchange (quali le informazioni di contatto oppure organizzazione) verranno conservati in Active Directory.

Dopo aver disabilitato la posta elettronica per un contatto di posta, è possibile riabilitare il contatto alla posta tramite il cmdlet **Enable-MailContact** in Shell. È anche possibile utilizzare questo cmdlet per abilitare alla posta qualsiasi contatto di Active Directory.

Per le attività di gestione aggiuntive relative ai contatti di posta, vedere [Gestire i contatti di posta](manage-mail-contacts-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento di ciascuna procedura: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Contatti di posta elettronica" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata?

## Disabilitare la posta elettronica per un contatto di posta

Come affermato in precedenza, quando si disabilita la posta elettronica per un contatto di posta, gli attributi di Exchange vengono rimossi dall'oggetto contatto di Active Directory corrispondente anche se il contatto viene conservato. Il contatto di posta viene rimosso dall'elenco di contatti relativo in EAC, ma è possibile visualizzare e gestire l'oggetto contatto di Active Directory corrispondente utilizzando Utenti e computer di Active Directory oppure i cmdlet **Get-Contact** e **Set-Contact** in Shell.

## Disabilitazione della posta elettronica per un contatto di posta tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**.

2.  Dall'elenco dei contatti fare clic sul contatto di posta per cui si desidera disabilitare la posta elettronica.

3.  Fare clic su **Altro**![Icona Ulteriori opzioni](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icona Ulteriori opzioni"), quindi su **Disabilita**.

4.  Viene visualizzato un avviso che richiede all'utente di confermare la disabilitazione del contatto di posta selezionato. Scegliere **Sì** per disabilitarlo.

Il contatto di posta elettronica verrà rimosso dall'elenco dei contatti.

## Disabilitazione della posta elettronica per un contatto di posta tramite Shell

Con questo esempio viene disabilitata la posta elettronica per il contatto di posta Neil Black.

    Disable-MailContact -Identity "Neil Black"

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Disable-MailContact](https://technet.microsoft.com/it-it/library/aa997465\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta disabilitazione della posta elettronica per un contatto di posta, effettuare una delle seguenti operazioni:

1.  In EAC accedere a **Destinatari** \> **Contatti** e verificare che il contatto di posta non sia più presente nell'elenco.

2.  In Utenti e computer di Active Directory fare clic con il pulsante destro del mouse sul contatto, quindi scegliere **Proprietà**. Nella scheda **Generali** tenere presente che la casella **Posta elettronica** è vuota. In questo modo si verifica che il contatto non è abilitato alla posta.

3.  In Shell, utilizzare il seguente comando.
    
        Get-MailContact
    
    Il contatto per cui è stata disabilitata la posta non verrà restituito nei risultati poiché il cmdlet restituisce solo i contatti abilitati alla posta.

4.  In Shell, utilizzare il seguente comando.
    
        Get-Contact
    
    Il contatto per cui è stata disabilitata la posta elettronica viene restituito nei risultati poiché il cmdlet restituisce tutti gli oggetti contatto di Active Directory.

## Abilitazione alla posta dei contatti tramite Shell

È possibile utilizzare il cmdlet **Enable-MailContact** per abilitare all'utilizzo della posta i contatti esistenti di Active Directory. È possibile abilitare alla posta un singolo contatto o utilizzare un file CSV per abilitare alla posta più contatti.

## Abilitazione alla posta di un singolo contatto tramite Shell

Con questo esempio viene abilitato alla posta il contatto Rene Valdes. È necessario fornire un indirizzo di posta elettronica esterno.

    Enable-MailContact -Identity "Rene Valdes" -ExternalEmailAddress renev@tailspintoys.com

## Utilizzare Shell e un file CSV per abilitare alla posta più contatti

Quando si abilitano in blocco i contatti alla posta, si esporta innanzitutto l'elenco dei contatti non abilitati alla posta in un file CSV (valori delimitati da virgole), quindi si aggiungono gli indirizzi di posta elettronica esterni al file CSV utilizzando un editor di testo quale Notepad oppure un'applicazione per fogli di calcolo come Microsoft Excel. Il file CSV aggiornato viene poi utilizzato nel comando Shell per abilitare alla posta i contatti elencati nel file.

1.  Eseguire il comando seguente per esportare un elenco di contatti esistenti non abilitati alla posta in un file sul desktop dell'amministratore denominato Contacts.csv.
    
        Get-Contact | Where { $_.RecipientType -eq "Contact" } | Out-File "C:\Users\Administrator\Desktop\Contacts.csv"
    
    Il file risultante sarà simile al seguente.
    
        Name
        Walter Harp
        James Alvord
        Rainer Witt
        Susan Burk
        Ian Tien
        ...

2.  Aggiungere l'intestazione di colonna denominata **EmailAddress**, quindi aggiungere un indirizzo di posta elettronica per ciascun contatto nel file. Il nome e l'indirizzo di posta elettronica esterno per ciascun contatto devono essere separati da una virgola. Il file CSV aggiornato dovrebbe essere simile al seguente.
    
        Name,EmailAddress
        James Alvord,james@contoso.com
        Susan Burk,sburk@tailspintoys.com
        Walter Harp,wharp@tailspintoys.com
        Ian Tien,iant@tailspintoys.com
        Rainer Witt,rainerw@fourthcoffee.com
        ...

3.  Eseguire il comando seguente per utilizzare i dati nel file CSV per abilitare alla posta i contatti elencati nel file.
    
        Import-CSV C:\Users\Administrator\Desktop\Contacts.csv | ForEach-Object {Enable-MailContact -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    Nei risultati del comando vengono visualizzate le informazioni relative ai nuovi contatti abilitati alla posta elettronica.

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare la corretta abilitazione alla posta dei contatti di Active Directory, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**. I nuovi contatti di posta vengono visualizzati nell'elenco dei contatti. In **Tipo di contatto**, il tipo è **Contatto di posta**.
    

    > [!NOTE]
    > Per visualizzare i nuovi contatti di posta, potrebbe essere necessario fare clic su <STRONG>Aggiorna</STRONG><IMG title="Icona Aggiorna" alt="Icona Aggiorna" src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif">.



  - In Shell, eseguire il seguente comando per visualizzare le informazioni relative ai nuovi contatti di posta.
    
        Get-MailContact | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

