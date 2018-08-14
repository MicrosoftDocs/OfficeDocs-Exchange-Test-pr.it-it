---
title: 'Gestire gruppi di sicurezza abilitati alla posta elettronica: Exchange 2013 Help'
TOCTitle: Gestire gruppi di sicurezza abilitati alla posta elettronica
ms:assetid: 80b3b537-4786-4d02-9202-44e373811a25
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123521(v=EXCHG.150)
ms:contentKeyID: 50479758
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire gruppi di sicurezza abilitati alla posta elettronica

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2017-10-04_

I gruppi di protezione abilitati all'utilizzo della posta elettronica possono essere utilizzati per distribuire i messaggi e per garantire le autorizzazioni di accesso alle risorse in Active Directory. Per ulteriori informazioni, vedere [Destinatari](recipients-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2-5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di distribuzione" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creare un gruppo di sicurezza abilitato alla posta elettronica

## Utilizzare EAC per creare un gruppo di sicurezza

1.  In EAC, individuare **Destinatari** \> **Gruppi**.

2.  Fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") \> **Gruppo di sicurezza**.

3.  Nella pagina **Nuovo gruppo di sicurezza**, completare i seguenti campi:
    
      - **\* Nome visualizzato**   Utilizzare questa casella per digitare il nome visualizzato. Questo nome verrà visualizzato nella Rubrica condivisa, nella riga A: quando il messaggio di posta elettronica viene inviato a questo gruppo e nell'elenco Gruppi nell'interfaccia di amministrazione di Exchange. Il nome visualizzato è obbligatorio e deve essere un nome descrittivo facilmente riconoscibile dagli utenti. Inoltre, deve essere univoco nella foresta.
        

        > [!NOTE]
        > Se viene applicato un criterio di denominazione dei gruppi, è necessario attenersi ai vincoli di denominazione specificati per la propria organizzazione. Per ulteriori informazioni, vedere <A href="create-a-distribution-group-naming-policy-exchange-2013-help.md">Creare un gruppo di distribuzione dei criteri di denominazione</A>. Se si desidera sovrascrivere il criterio di denominazione dei gruppi dell'organizzazione, vedere <A href="override-the-distribution-group-naming-policy-exchange-2013-help.md">Eseguire l'override del gruppo di distribuzione dei criteri di denominazione</A>.

    
      - **\* Alias**   Utilizzare questa casella per digitare l'alias per il gruppo di sicurezza. L'alias non può contenere più di 64 caratteri e deve essere univoco nella foresta. Quando un utente digita l'alias nella riga A: di un messaggio di posta elettronica, questo si risolve nel nome visualizzato del gruppo.
    
      - **Descrizione**   Utilizzare questa casella per descrivere lo scopo del gruppo di sicurezza.
    
      - **Unità organizzativa**   È possibile selezionare un'unità organizzativa diversa da quella predefinita (che corrisponde all'ambito dei destinatari). Se l'ambito dei destinatari è impostato a livello di foresta, il valore predefinito è impostato sul contenitore di utenti nel dominio di Active Directory contenente il computer su cui è in esecuzione l'interfaccia di amministrazione di Exchange. Se l'ambito dei destinatari viene impostato su un dominio specifico, per impostazione predefinita verrà selezionato il contenitore di utenti del dominio in questione. Se infine come ambito dei destinatari si sceglie una specifica unità organizzativa, per impostazione predefinita verrà selezionata l'unità organizzativa specificata.
        
        Per selezionare un'unità organizzativa diversa, scegliere il pulsante **Sfoglia**. La finestra di dialogo visualizzerà tutte le unità organizzative presenti nella foresta all'interno dell'ambito specificato. Selezionare l'unità organizzativa desiderata e quindi fare clic su **OK**.
    
      - **\* Proprietari**   Per impostazione predefinita, l'utente che crea un gruppo ne diventa proprietario. Ogni gruppo deve presentare almeno un proprietario. È possibile aggiungere proprietari facendo clic su **Aggiungi**.
    
      - **Membri**   Utilizzare questa sezione per aggiungere membri e specificare se è necessaria l'approvazione per unirsi al gruppo o abbandonarlo.
        
        I proprietari di un gruppo non sono tenuti a esserne membri. Utilizzare **Aggiungi proprietari di gruppi come membri** per aggiungere o rimuovere i proprietari come membri.
        
        Per aggiungere membri al gruppo, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Al termine dell'aggiunta dei membri, fare clic su **OK** per tornare alla pagina **Nuovo gruppo di sicurezza**.
        
        Selezionare la casella di controllo **È richiesta l'approvazione del proprietario** se si desidera che i proprietari dei gruppi ricevano le richieste utente di iscrizione al gruppo. Se si seleziona questa opzione, i membri possono essere rimossi soltanto dai proprietari dei gruppi.

4.  Al termine, scegliere **Salva** per creare il gruppo di sicurezza.


> [!NOTE]
> Per impostazione predefinita, tutti i nuovi gruppi di sicurezza abilitati alla posta elettronica richiedono l'autenticazione di tutti i mittenti. Questo impedisce ai mittenti esterni di inviare messaggi ai gruppi di sicurezza abilitati alla posta elettronica. Per consentire a un gruppo di sicurezza abilitato alla posta elettronica di accettare i messaggi da tutti i mittenti, occorre modificare le impostazioni di restrizione di recapito dei messaggi per il gruppo.



## Creazione di un gruppo di protezione tramite Shell

In questo esempio viene creato un gruppo di sicurezza con alias fsadmin e nome File Server Managers. Il gruppo di sicurezza viene creato nell'unità organizzativa predefinita; chiunque può unirsi al gruppo senza l'approvazione dei proprietari del gruppo.

    New-DistributionGroup -Name "File Server Managers" -Alias fsadmin -Type security

Per ulteriori informazioni sull'utilizzo di Shell per creare gruppi di sicurezza abilitati alla posta elettronica, vedere [New-DistributionGroup](https://technet.microsoft.com/it-it/library/aa998856\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione di un gruppo di sicurezza abilitato alla posta elettronica, effettuare una delle seguenti operazioni:

  - In EAC, individuare **Destinatari** \> **Gruppi**. Il nuovo gruppo di sicurezza abilitato alla posta elettronica è visualizzato nell'elenco dei gruppi. In **Tipo di gruppo**, il tipo è **Gruppo di sicurezza**.

  - In Shell, eseguire il comando riportato di seguito per visualizzare informazioni sul nuovo gruppo di sicurezza abilitato alla posta elettronica.
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## Cambiare le proprietà del gruppo di sicurezza abilitato alla posta elettronica

## Utilizzare EAC per modificare le proprietà del gruppo di sicurezza abilitato alla posta elettronica

1.  In EAC, individuare **Destinatari** \> **Gruppi**.

2.  Nell'elenco dei gruppi, fare clic sul gruppo di sicurezza da visualizzare o modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del gruppo, fare clic su una delle sezioni indicate di seguito per visualizzare o modificare le proprietà.
    
      - General
    
      - Proprietà
    
      - Appartenenza
    
      - Approvazione di appartenenza
    
      - Gestione recapito
    
      - Approvazione del messaggio
    
      - Opzioni di posta elettronica
    
      - MailTip
    
      - Delega gruppo

## Generale

Utilizzare questa sezione per visualizzare o modificare le informazioni di base sul gruppo.

  - **\* Nome visualizzato**   Questo nome verrà visualizzato nella Rubrica, nei campi A: quando il messaggio di posta elettronica viene inviato a questo gruppo e nell'elenco Gruppi. Il nome visualizzato è obbligatorio e deve essere un nome descrittivo facilmente riconoscibile dagli utenti. Inoltre, deve essere univoco nel dominio in uso.

  - **\* Alias**   Questa è la parte dell'indirizzo di posta elettronica visualizzata a sinistra del simbolo di chiocciola (@). Se si modifica l'alias, verrà modificato anche l'indirizzo SMTP primario del gruppo in modo che contenga il nuovo alias. Inoltre, l'indirizzo di posta elettronica con il precedente alias verrà conservato come indirizzo proxy del gruppo.

  - **Descrizione**   Utilizzare questa casella per descrivere lo scopo del gruppo. Questa descrizione viene visualizzata nella rubrica e nel riquadro Dettagli dell'interfaccia di amministrazione di Exchange.

  - **Nascondi il gruppo dagli elenchi di indirizzi**   Selezionare questa casella di controllo per evitare che gli utenti vedano questo gruppo nella rubrica. Se la casella di controllo è selezionata, un mittente deve digitare l'alias o l'indirizzo di posta elettronica del gruppo nella riga A: o Cc: per inviare messaggi di posta elettronica al gruppo.
    

    > [!TIP]
    > Può essere opportuno nascondere i gruppi di sicurezza, in quanto vengono in genere utilizzati per assegnare autorizzazioni ai membri del gruppo e non per inviare messaggi di posta elettronica.



  - **Unità organizzativa**   Questa casella di sola lettura visualizza l'unità organizzativa (OU) contenente il gruppo di sicurezza. È necessario utilizzare Utenti e computer di Active Directory per spostare il gruppo in un'altra unità organizzativa.

## Proprietà

Utilizzare questa sezione per assegnare i proprietari del gruppo. Il proprietario del gruppo può aggiungere membri al gruppo nonché approvare o rifiutare le richieste di unione al gruppo. Per impostazione predefinita, la persona che crea un gruppo ne diventa proprietario. Ogni gruppo deve presentare almeno un proprietario.

È possibile aggiungere proprietari facendo clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). È possibile rimuovere un proprietario selezionandolo e facendo clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

## Appartenenza

Utilizzare questa sezione per aggiungere o rimuovere membri. I proprietari di un gruppo non sono tenuti a esserne membri. Nella sezione **Membri**, è possibile aggiungere i membri facendo clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere un membro è possibile selezionare un utente nell'elenco dei membri e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

## Approvazione dell'appartenenza

Utilizzare questa sezione per specificare se è necessaria l'approvazione del proprietario per unirsi al gruppo. Se si seleziona la casella di controllo **È richiesta l'approvazione del proprietario**, il proprietario o i proprietari del gruppo riceveranno un messaggio di posta elettronica che richiede l'approvazione per l'unione al gruppo. Come affermato in precedenza, solo i proprietari possono rimuovere i membri dal gruppo.


> [!NOTE]
> Questa opzione non funzionerà con i gruppi di protezione abilitati alla posta elettronica a causa di limitazioni relative alla sicurezza.



## Gestione recapito

Utilizzare questa sezione per gestire gli utenti che possono inviare posta elettronica a questo gruppo.

  - **Solo mittenti interni all'organizzazione**   Selezionare questa opzione per consentire l'invio di messaggi al gruppo solo ai mittenti dell'organizzazione. In questo modo, se un utente esterno all'organizzazione invia un messaggio di posta elettronica a questo gruppo, tale messaggio sarà rifiutato. Questa impostazione è quella predefinita.

  - **Mittenti interni ed esterni all'organizzazione**   Selezionare questa opzione per consentire a tutti di inviare i messaggi al gruppo.
    
    È possibile limitare ulteriormente gli utenti che possono inviare messaggi al gruppo consentendo solo a mittenti specifici di inviare messaggi a questo gruppo. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e quindi selezionare uno o più destinatari. I mittenti aggiunti a questo elenco saranno i soli a poter inviare posta al gruppo. I messaggi inviati da chiunque non sia presente nell'elenco verranno rifiutati.
    
    Per rimuovere un utente o un gruppo dall'elenco, selezionarlo nell'elenco, quindi fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").
    

    > [!IMPORTANT]
    > Se il gruppo è stato configurato per consentire l'invio di messaggi al gruppo solo da parte di mittenti all'interno dell'organizzazione, i messaggi di posta elettronica inviati da un contatto esterno saranno rifiutati, anche se il contatto è stato aggiunto a questo elenco.



## Approvazione del messaggio

Utilizzare questa sezione per impostare le opzioni di moderazione del gruppo. I moderatori approvano o rifiutano i messaggi inviati al gruppo prima che raggiungano i membri del gruppo.

  - **I messaggi inviati a questo gruppo sono stati approvati da un moderatore**   Per impostazione predefinita, questa casella di controllo non è selezionata. Se si seleziona questa casella di controllo, i moderatori del gruppo esamineranno i messaggi in arrivo prima di procedere al relativo recapito. I moderatori del gruppo possono approvare o rifiutare i messaggi in arrivo.

  - **Moderatori del gruppo**   Per aggiungere moderatori al gruppo, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere un moderatore, selezionarlo, quindi fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi"). Se è stata selezionata l'opzione "I messaggi inviati a questo gruppo sono stati approvati da un moderatore" senza tuttavia aver selezionato alcun moderatore, i messaggi destinati al gruppo saranno inviati ai proprietari del gruppo per l'approvazione.

  - **Mittenti che non richiedono l'approvazione dei messaggi**   Per aggiungere utenti o gruppi in grado di ignorare la moderazione del gruppo, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere una utente o un gruppo, selezionarlo e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

  - **Seleziona notifiche di moderazione** Utilizzare questa sezione per stabilire in che modo gli utenti vengono avvisati dell'approvazione del messaggio.
    
      - **Notificare a tutti i mittenti che i loro messaggi non sono stati approvati**   Questa è l'impostazione predefinita. I mittenti interni ed esterni all'organizzazione riceveranno una notifica in merito alla mancata approvazione dei loro messaggi.
    
      - **Notifica ai mittenti nell'organizzazione se i rispettivi messaggi non vengono approvati**   Selezionando questa opzione, solo gli utenti o i gruppi nell'organizzazione ricevono una notifica quando un messaggio che hanno inviato al gruppo non viene approvato da un moderatore.
    
      - **Non inviare alcuna notifica quando un messaggio non è approvato**   Se si seleziona questa opzione, non vengono inviate notifiche ai mittenti quando i loro messaggi non vengono approvati dai moderatori del gruppo.

## Opzioni di posta elettronica

Utilizzare questa sezione per visualizzare o modificare gli indirizzi di posta elettronica associati al gruppo. Ciò include gli indirizzi SMTP primari del gruppo e qualsiasi indirizzo proxy ad esso associato. L'indirizzo SMTP primario (chiamato anche *indirizzo di risposta*) viene visualizzato in grassetto nell'elenco degli indirizzi, con il valore **SMTP** maiuscolo nella colonna **Tipo**.

  - **Aggiungi**  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere un nuovo indirizzo di posta elettronica per la cassetta postale. Selezionare uno dei seguenti tipi di indirizzo:
    
      - **SMTP**   Questo è il tipo di indirizzo predefinito. Fare clic su questo pulsante e quindi digitare il nuovo indirizzo SMTP nella casella **\* Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Per impostare il nuovo indirizzo SMTP come primario per il gruppo, selezionare la casella di controllo <STRONG>Imposta questo indirizzo come indirizzo di risposta</STRONG>. Questa casella di controllo viene visualizzata solo se la casella di controllo <STRONG>Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario</STRONG> non è selezionata.

    
      - **Tipo di indirizzo personalizzato**   Fare clic su questo pulsante e digitare uno dei tipi di indirizzi di posta elettronica non SMTP supportati nella casella **\* Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Fatta eccezione per gli indirizzi X.400, Exchange non convalida gli indirizzi personalizzati per verificarne la corretta formattazione. È necessario verificare che l'indirizzo personalizzato specificato sia conforme ai requisiti di formato per tale tipo di indirizzo.



  - **Modifica**   Per cambiare un indirizzo di posta elettronica associato al gruppo, selezionarlo nell'elenco e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    

    > [!NOTE]
    > Per impostare un indirizzo SMTP esistente come primario per il gruppo, selezionare la casella di controllo <STRONG>Imposta questo indirizzo come indirizzo di risposta</STRONG>. Come affermato in precedenza, questa casella di controllo viene visualizzata solo se la casella di controllo <STRONG>Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario</STRONG> non è selezionata.



  - **Rimuovi**   Per eliminare un indirizzo di posta elettronica associato al gruppo, selezionarlo nell'elenco e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

  - **Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario** Selezionare questa casella di controllo per aggiornare automaticamente gli indirizzi di posta elettronica dei destinatari in base alle modifiche apportate ai criteri degli indirizzi di posta elettronica nell'organizzazione. La casella è selezionata per impostazione predefinita.

## MailTip

Utilizzare questa sezione per aggiungere un avviso per informare gli utenti dei problemi che potrebbero verificarsi se inviano un messaggio a questo gruppo. Un avviso messaggio è un testo che viene visualizzato sulla barra informazioni quando questo gruppo viene aggiunto nella riga A, Cc o Ccn di un nuovo messaggio di posta elettronica. Ad esempio, è possibile aggiungere un Avviso messaggio ai gruppi di grandi dimensioni per avvertire i mittenti potenziali che il messaggio verrà inviato a molte persone.


> [!NOTE]
> Gli avvisi messaggio possono includere tag HTML, ma gli script non sono consentiti. La lunghezza di un avviso messaggio personalizzato non può superare 175 caratteri visualizzati. I tag HTML non vengono conteggiati in tale limite.



## Delega gruppo

Utilizzare questa sezione per assegnare a un utente (chiamato *delegato*) le autorizzazioni necessarie per permettergli di inviare messaggi come gruppo o per conto del gruppo. È possibile assegnare le seguenti autorizzazioni:

  - **Invia come**   Questa autorizzazione consente al delegato di inviare i messaggi come gruppo. Una volta assegnata l'autorizzazione, il delegato può scegliere di aggiungere il gruppo nella riga **Da** per indicare che il messaggio è stato inviato dal gruppo.

  - **Invia per conto di**   Anche questa autorizzazione consente a un delegato di inviare messaggi per conto del gruppo. Una volta assegnata questa autorizzazione, il delegato ha la possibilità di aggiungere il gruppo alla riga **Da**. Il messaggio risulterà essere stato inviato dal gruppo e indicherà che è stato inviato dal delegato per conto del gruppo.

Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi** sotto l'autorizzazione desiderata per visualizzare la pagina **Scegli il destinatario** che contiene un elenco di destinatari nell'organizzazione Exchange a cui può essere assegnata l'autorizzazione. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare un destinatario specifico digitandone il nome nella casella di ricerca e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca").

## Utilizzare Shell per cambiare le proprietà del gruppo di sicurezza

Utilizzare i cmdlet **Get-DistributionGroup** e **Set-DistributionGroup** per visualizzare e modificare le proprietà dei gruppi di sicurezza. I vantaggi dell'utilizzo di Shell sono la possibilità di cambiare le proprietà non disponibili in EAC e l'opportunità di modificare le proprietà per più gruppi di sicurezza. Per informazioni sui parametri corrispondenti alle proprietà del gruppo di distribuzione, consultare i seguenti argomenti:

  - [Get-DistributionGroup](https://technet.microsoft.com/it-it/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/it-it/library/bb124955\(v=exchg.150\))

Ecco alcuni esempi dell'utilizzo di Shell per cambiare le proprietà del gruppo di sicurezza.

In questo esempio viene visualizzato un elenco di tutti i gruppi di sicurezza nell'organizzazione.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')}

In questo esempio viene modificato l'indirizzo SMTP primario (detto anche indirizzo per le risposte) per il gruppo di sicurezza Seattle Administrators, da admins@contoso.com a seattle.admins@contoso.com. L'indirizzo per le risposte precedente sarà conservato come indirizzo proxy.

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.admins@contoso.com,smtp:admins@contoso.com

In questo esempio tutti i gruppi di sicurezza nell'organizzazione vengono nascosti dalla rubrica.

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} | Set-DistributionGroup -HiddenFromAddressListsEnabled $true

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta modifica delle proprietà di un gruppo di sicurezza, effettuare le seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, selezionare il gruppo e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare la proprietà o la funzionalità modificata. A seconda della proprietà modificata, è possibile che questa venga visualizzata nel riquadro Dettagli del gruppo selezionato.

  - In Shell, utilizzare il cmdlet **Get-DistributionGroup** per verificare le modifiche. Uno dei vantaggi offerti dall'utilizzo di Shell è la possibilità di visualizzare più proprietà per più gruppi. Nell'esempio precedente, dove tutti i gruppi di sicurezza sono stati nascosti dalla rubrica, eseguire il seguente comando per verificare il nuovo valore.
    
        Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} |
         fl Name,HiddenFromAddressListsEnabled


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

