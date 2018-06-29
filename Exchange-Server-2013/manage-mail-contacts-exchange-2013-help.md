---
title: 'Gestire i contatti di posta: Exchange 2013 Help'
TOCTitle: Gestire i contatti di posta
ms:assetid: 74c72aed-e9ff-4927-8eb7-c08a86e79ae0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998858(v=EXCHG.150)
ms:contentKeyID: 50479750
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailContactWizardForm.NewMailContactIntroductionWizardPage
ms.translationtype: MT
---

# Gestire i contatti di posta

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2017-10-04_

I contatti di posta sono oggetti del servizio directory abilitati all'utilizzo della posta che contengono informazioni su persone o organizzazioni esistenti all'esterno dell'organizzazione di Exchange o Exchange Online. Ciascun contatto di posta dispone di un indirizzo di posta elettronica esterno. Per ulteriori informazioni sui contatti di posta, vedere [Destinatari](recipients-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creazione di un contatto di posta

## Creazione di un contatto di posta tramite interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**.

2.  Fare clic su **Nuovo** ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") \> **Contatto di posta**.

3.  Completare le seguenti caselle sulla pagina **Nuovo contatto di posta**:
    
      - **Nome**   Utilizzare questa casella per digitare il nome del contatto.
    
      - **Iniziali**   Utilizzare questa casella per digitare le iniziali del contatto.
    
      - **Cognome**   Utilizzare questa casella per digitare il cognome del contatto.
    
      - **\* Nome visualizzato**   Utilizzare questa casella per digitare un nome visualizzato per il contatto. Questo è il nome che compare nell'elenco dei contatti nell'interfaccia di amministrazione di Exchange e nella rubrica dell'organizzazione. Per impostazione predefinita, questa casella contiene i nomi immessi nelle caselle **Nome di battesimo**, **Iniziali** e **Cognome**. Se queste caselle non sono state utilizzate, è necessario digitare un nome in questa casella perché è obbligatoria. Il nome non può superare i 64 caratteri.
    
      - **\* Nome**   Utilizzare questa casella per digitare un nome per il contatto. Si tratta del nome elencato nel servizio directory. Come per il nome visualizzato, per impostazione predefinita, questa casella contiene i nomi immessi nelle caselle **Nome di battesimo**, **Iniziali** e **Cognome**. Se queste caselle non sono state utilizzate, è necessario digitare un nome in questa casella perché è obbligatoria. Il nome non può superare i 64 caratteri.
    
      - **\* Alias** Utilizzare questa casella per specificare un alias (64 caratteri o meno) per il contatto. Questa casella è obbligatorio.
    
      - **\* Indirizzo di posta elettronica esterno**   Utilizzare questa casella per immettere l'account di posta elettronica esterno per il contatto. Questa casella è obbligatoria. I messaggi di posta elettronica inviati al contatto vengono inoltrati a questo indirizzo di posta elettronica.
    
      - **Unità organizzativa**   È possibile selezionare un'unità organizzativa diversa da quella predefinita, che corrisponde all'ambito dei destinatari. Se l'ambito dei destinatari è impostato a livello di foresta, il valore predefinito è impostato sul contenitore di utenti nel dominio contenente il computer su cui è in esecuzione l'interfaccia di amministrazione di Exchange. Se l'ambito dei destinatari viene impostato su un dominio specifico, per impostazione predefinita verrà selezionato il contenitore di utenti del dominio in questione. Se infine come ambito dei destinatari si sceglie una specifica unità organizzativa, per impostazione predefinita verrà selezionata l'unità organizzativa specificata.
        
        Per selezionare un'unità organizzativa diversa, scegliere il pulsante **Sfoglia**. La finestra di dialogo visualizzerà tutte le unità organizzative presenti nella foresta all'interno dell'ambito specificato. Selezionare l'unità organizzativa desiderata e fare clic su **OK**.
        

        > [!NOTE]
        > La casella <STRONG>Unità organizzativa</STRONG> è disponibile solamente in Exchange Server 2013. Non è disponibile in Exchange Online.



4.  Al termine, fare clic su **Salva**.

## Creazione di un contatto di posta tramite Shell

In questo esempio, viene creato un contatto di posta per Debra Garcia in Exchange Server 2013.

    New-MailContact -Name "Debra Garcia" -ExternalEmailAddress dgarcia@tailspintoys.com -OrganizationalUnit Users

In questo esempio, viene creato un contatto di posta per Alan Shen in Exchange Online.

    New-MailContact -Name "Alan Shen" -ExternalEmailAddress alans@fourthcoffee.com

In questo esempio, viene abilitato alla posta un contatto esistente denominato Karen Toh in Exchange Server 2013.

    Enable-MailContact -Identity "Karen Toh" -ExternalEmailAddress ktoh@tailspintoys.com

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione del contatto di posta, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**. Il nuovo contatto di posta viene visualizzato nell'elenco dei contatti. In **Tipo di contatto**, il tipo è **Contatto di posta**.

  - In Shell, eseguire il seguente comando per visualizzare le informazioni relative al nuovo contatto di posta.
    
        Get-MailContact <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## Modifica delle proprietà del contatto di posta

## Utilizzare l'interfaccia di amministrazione di Exchange per modificare le proprietà del contatto di posta

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**.

2.  Nell'elenco dei contatti di posta, fare clic sul contatto di posta del quale si vogliono modificare le proprietà e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Sulla pagina delle proprietà del contatto di posta, fare clic su una delle seguenti sezioni per visualizzare o modificare le proprietà.
    
      - General
    
      - Contact Information
    
      - Organization
    
      - Email Options (non disponibile in Exchange Online).
    
      - MailTip

## Generale

Utilizzare la sezione **Generale** per visualizzare o modificare le informazioni di base sul contatto di posta.

  - **Nome**, **Iniziali**, **Cognome**

  - **\* Nome**   Questo è il nome che compare in Active Directory. Se viene modificato, non può superare i 64 caratteri.

  - **\* Nome visualizzato**   Questo nome viene visualizzato nella rubrica dell'organizzazione, nelle righe A e Da del messaggio di posta elettronica e nell'elenco delle cassette postali. Questo nome non può contenere spazi vuoti prima o dopo il nome visualizzato.

  - **\* Alias**   Questo è l'alias del contatto di posta. Se viene modificato, deve essere univoco nell'organizzazione e deve essere lungo 64 caratteri o meno.

  - **\* Indirizzo di posta elettronica esterno**   Questo è l'indirizzo SMTP primario del contatto e il suo account di posta elettronica esterno. I messaggi di posta elettronica inviati al contatto vengono inoltrati a questo indirizzo di posta elettronica.

  - Fare clic su **Altre opzioni** per visualizzare l'unità organizzativa che contiene l'account del contatto di posta. Per spostare l'account in un'unità organizzativa (OU) diversa, è necessario utilizzare Utenti e computer di Active Directory.

## Informazioni di contatto

Utilizzare la sezione **Informazioni di contatto** per visualizzare o modificare le informazioni di contatto del destinatario, quali ad esempio indirizzo di posta e numeri di telefono. Queste informazioni vengono visualizzate nella rubrica.

## Organizzazione

Utilizzare la sezione **Organizzazione** per registrare informazioni dettagliate sul ruolo del contatto di posta nell'organizzazione. Queste informazioni vengono visualizzate nella rubrica. Inoltre, è possibile creare il diagramma di un'organizzazione virtuale a cui è possibile accedere dai client di posta elettronica quali Outlook.

  - **Titolo**   Questa casella di testo consente di visualizzare o modificare il titolo del contatto.

  - **Reparto**   Utilizzare questa casella per visualizzare o modificare il nome del reparto in cui lavora il contatto. È possibile utilizzare questa casella per creare condizioni del destinatario per i gruppi di distribuzione dinamici e gli elenchi di indirizzi.

  - **Società**   Utilizzare questa casella peri visualizzare o modificare la società per cui lavora il contatto. È anche possibile utilizzare questa casella per creare condizioni del destinatario per i gruppi di distribuzione dinamici.

  - **Manager**   Per aggiungere un manager, fare clic su **Sfoglia**. In **Seleziona responsabile**, selezionare una persona e quindi fare clic su **OK**.

  - **Superiore diretto**   Questo campo non può essere modificato. Un *subalterno* è un destinatario che risponde a un manager specifico. Se è stato specificato un responsabile per il destinatario, quest'ultimo verrà visualizzato come subalterno nei dettagli della cassetta postale del responsabile. Ad esempio, Toby gestisce Ann e Spencer, che sono contatti di posta. perciò Toby è specificato nella casella **Manager** nelle proprietà organizzazione per Ann e Spencer, e Ann e Spencer compaiono nella casella **Subalterni** nelle proprietà della cassetta postale di Toby.

## Opzioni di posta elettronica

Utilizzare la sezione **Opzioni di posta elettronica** per aggiungere o rimuovere indirizzi proxy per il contatto di posta o per modificare gli indirizzi proxy esistenti. L'indirizzo SMTP primario dell'utente di posta viene visualizzato anche in questa sezione, ma non può essere modificato. Per modificarlo è necessario modificare l'indirizzo di posta elettronica esterno del contatto nella sezione **Generale**.


> [!NOTE]
> La sezione <STRONG>Opzioni posta elettronica</STRONG> è disponibile solamente in Exchange Server 2013. Non è disponibile in Exchange Online.



## Avviso messaggio

Utilizzare la sezione **Avviso messaggio** per aggiungere un avviso per informare gli utenti dei problemi che potrebbero verificarsi se inviano un messaggio a questo destinatario. Un avviso messaggio è un testo che viene visualizzato sulla barra informazioni quando questo destinatario viene aggiunto nella riga A, Cc o Ccn di un nuovo messaggio di posta elettronica.


> [!NOTE]
> Gli avvisi messaggio possono includere tag HTML, ma gli script non sono consentiti. La lunghezza di un avviso messaggio personalizzato non può superare 175 caratteri visualizzati. I tag HTML non vengono conteggiati in tale limite.



## Modificare le proprietà di un contatto di posta tramite Shell

Le proprietà di un contatto di posta sono archiviate sia in Active Directory che in Exchange. In generale, utilizzare i cmdlet **Get-Contact** e **Set-Contact** per visualizzare e modificare l'organizzazione e le informazioni delle proprietà del contatto. Utilizzare i cmdlet **Get-MailContact** e **Set-MailContact** per visualizzare o modificare le proprietà relative alla posta elettronica, quali ad esempio indirizzi di posta elettronica, avvisi messaggio, attributi personalizzati e per specificare se il contatto è nascosto negli elenchi di indirizzi.

Per ulteriori informazioni, vedere i seguenti argomenti:

  - [Get-Contact](https://technet.microsoft.com/it-it/library/aa998258\(v=exchg.150\))

  - [Set-Contact](https://technet.microsoft.com/it-it/library/bb124535\(v=exchg.150\))

  - [Get-MailContact](https://technet.microsoft.com/it-it/library/bb124717\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/it-it/library/aa995950\(v=exchg.150\))

Di seguito vengono forniti alcuni esempi dell'utilizzo di Shell per modificare le proprietà del contatto di posta.

In questo esempio vengono configurate le proprietà Titolo, Reparto, Società e Manager per il contatto di posta Kai Axford.

    Set-Contact "Kai Axford" _-Title Consultant -Department "Public Relations" -Company Fabrikam -Manager "Karen Toh"

In questo esempio viene impostata la proprietà CustomAttribute1 su un valore di PartTime per tutti i contatti di posta e vengono nascosti negli elenchi di indirizzi dell'organizzazione.

    Get-MailContact | Set-MailContact -CustomAttribute1 PartTime -HiddenFromAddressListsEnabled $true

In questo esempio viene impostata la proprietà CustomAttribute15 su un valore di TemporaryEmployee per tutti i contatti di posta nel reparto Pubbliche relazioni.

    Get-Contact -Filter "Department -eq 'Public Relations'" | Set-MailContact -CustomAttribute15 TemporaryEmployee

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente modificato le proprietà per un contatto di posta, fare quanto segue:

  - Nell'interfaccia di amministrazione Exchange selezionare il contatto di posta e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare le proprietà modificate.

  - In Shell, utilizzare i cmdlet **Get-Contact** e **Get-MailContact** per verificare le modifiche. Uno dei vantaggi offerti dall'utilizzo di Shell è la possibilità di visualizzare più proprietà per più contatti di posta. Nell'esempio precedente dove per tutti i contatti di posta la proprietà CustomAttribute1 era impostata su PartTime ed erano nascosti negli elenchi indirizzi, eseguire il seguente comando per verificare le modifiche.
    
        Get-MailContact | Fl Name,CustomAttribute1,HiddenFromAddressListsEnabled
    
    Nell'esempio precedente dove per tutti i contatti di posta la proprietà CustomAttribute15 era impostata su reparto Pubbliche relazioni, eseguire il seguente comando per verificare le modifiche.
    
        Get-Contact -Filter "Department -eq 'Public Relations'" | Get-MailContact | FL Name,CustomAttribute15

## Modifica collettiva dei contatti di posta

È possibile utilizzare l'interfaccia di amministrazione di Exchange per modificare le proprietà selezionate di più contatti di posta. Quando si selezionano due o più contatti di posta dall'elenco contatti nell'interfaccia di amministrazione di Exchange, le proprietà che possono essere modificate collettivamente vengono elencate nel riquadro dei dettagli. Quando si modifica una di queste proprietà, la modifica viene applicata a tutti i destinatari selezionati.

Quando si modificano collettivamente i contatti di posta, è possibile modificare le seguenti aree di proprietà:

  - **Informazioni contatto**   Modificare le proprietà condivise quali indirizzo, CAP e città.

  - **Organizzazione**   Modificare le proprietà condivise quali nome del reparto, ragione sociale e responsabile a cui riportano i contatti o gli utenti di posta selezionati.

## Utilizzare l'interfaccia di amministrazione di Exchange per modificare collettivamente i contatti di posta

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Contatti**.

2.  Nell'elenco dei contatti, selezionare due o più contatti di posta. Non è possibile modificare in blocco un insieme di contatti e utenti di posta.
    

    > [!TIP]
    > Per selezionare più contatti di posta contigui tenere premuto MAIUSC e fare clic sul primo contatto, quindi fare clic sull'ultimo contatto che si vuole modificare. Per selezionare più contatti non contigui, tenere premuto CTRL e fare clic su ciascun contatto che si vuol modificare.



3.  Nel riquadro Dettagli, in **Modifica in blocco**, fare clic su **Aggiorna** in **Informazioni contatto** oppure **Organizzazione**.

4.  Apportare le modifiche nella pagina delle proprietà e quindi salvare le modifiche.

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta modifica collettiva dei contatti di posta, effettuare una delle seguenti operazioni:

  - Nell'interfaccia di amministrazione Exchange selezionare i contatti di posta modificati collettivamente e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare le proprietà modificate.

  - In Shell, utilizzare il cmdlet **Get-Contact** per verificare le modifiche. Ad esempio, si presuppone che sia stata utilizzata la funzionalità di modifica collettiva nell'interfaccia di amministrazione di Exchange per modificare il manager e l'ufficio di tutti i contatti di posta di una società fornitrice denominata A. Datum Corporation. Per verificare le modifiche, è possibile utilizzare il seguente comando in Shell.
    
        Get-Contact -ResultSize unlimited -Filter {(Company -eq 'Adatum')} | fl Name,Office,Manager


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Piccola icona per LinkedIn Learning" alt="Piccola icona per LinkedIn Learning" /> <strong>Nuovo utente di Office 365?</strong><br />
Sono disponibili esercitazioni video gratuite per <a href="https://support.office.com/it-it/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a> grazie a LinkedIn Learning.</p></td>
</tr>
</tbody>
</table>

