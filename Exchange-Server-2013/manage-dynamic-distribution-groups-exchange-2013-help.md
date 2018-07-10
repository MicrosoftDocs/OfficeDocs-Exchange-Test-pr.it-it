---
title: 'Gestione dei gruppi di distribuzione dinamici: Exchange 2013 Help'
TOCTitle: Gestione dei gruppi di distribuzione dinamici
ms:assetid: 8ef85d0a-41df-4b5c-b8e7-ca8d09c048ca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123722(v=EXCHG.150)
ms:contentKeyID: 50479846
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDynamicGroupWizardForm.CreateDynamicGroupInformationWizardPage
ms.translationtype: HT
---

# Gestione dei gruppi di distribuzione dinamici

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

I gruppi di distribuzione dinamici sono oggetti gruppo di Active Directory abilitati alla posta elettronica creati per accelerare l'invio di massa dei messaggi di posta elettronica e di altre informazioni all'interno di un'organizzazione di Microsoft Exchange.

Diversamente dai gruppi di distribuzione normali che contengono un set definito di membri, l'elenco di appartenenza per i gruppi di distribuzione dinamici viene calcolato in base ai filtri e alle condizioni definite dall'utente ogni volta che un messaggio viene inviato al gruppo. Quando un messaggio di posta elettronica viene inviato a un gruppo di distribuzione dinamico, viene recapitato a tutti i destinatari dell'organizzazione che soddisfano i criteri definiti per il gruppo.


> [!IMPORTANT]
> Un gruppo di distribuzione dinamico include qualsiasi destinatario in Active Directory con valori di attributo che soddisfano i criteri del filtro. Se le proprietà di un destinatario vengono modificate per soddisfare i criteri del filtro, il destinatario potrebbe involontariamente diventare un membro del gruppo e ricevere messaggi inviati al gruppo. Per ridurre le probabilità che si verifichi tale problema, è necessario adottare processi di provisioning degli account ben definiti e coerenti.



## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2-5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di distribuzione dinamici" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creare un gruppo di distribuzione dinamico

## Utilizzare EAC per creare un gruppo di distribuzione dinamico

1.  In EAC, individuare **Destinatari** \> **Gruppi** \> **Nuovo** \> **Gruppo di distribuzione dinamico**.

2.      
    Nella pagina **Nuovo gruppo di distribuzione dinamico**, completare le seguenti caselle:
    
      - **\* Nome visualizzato**   Utilizzare questa casella per digitare il nome visualizzato. Questo nome verrà visualizzato nella Rubrica condivisa, nella riga A: quando il messaggio di posta elettronica viene inviato a questo gruppo e nell'elenco Gruppi nell'interfaccia di amministrazione di Exchange. Il nome visualizzato è obbligatorio e deve essere un nome descrittivo facilmente riconoscibile dagli utenti. Inoltre, deve essere univoco nella foresta.
        

        > [!NOTE]
        > Il criterio di denominazione del gruppo non viene applicato ai gruppi di distribuzione dinamici.

    
      - **\* Alias**   Utilizzare questa casella per digitare il nome dell'alias per il gruppo. L'alias non può superare i 64 caratteri e deve essere univoco nella foresta. Quando un utente digita l'alias nella riga A: di un messaggio di posta elettronica, questo si risolve nel nome visualizzato del gruppo.
    
      - **Descrizione**   Utilizzare questa casella per descrivere lo scopo del gruppo. Questa descrizione viene visualizzata nella rubrica condivisa.
    
      - **Unità organizzativa**   È possibile selezionare un'unità organizzativa diversa da quella predefinita (che corrisponde all'ambito dei destinatari). Se l'ambito dei destinatari è impostato a livello di foresta, il valore predefinito è impostato sul contenitore di utenti nel dominio di Active Directory contenente il computer su cui è in esecuzione l'interfaccia di amministrazione di Exchange. Se l'ambito dei destinatari viene impostato su un dominio specifico, per impostazione predefinita verrà selezionato il contenitore di utenti del dominio in questione. Se infine come ambito dei destinatari si sceglie una specifica unità organizzativa, per impostazione predefinita verrà selezionata l'unità organizzativa specificata.
        
        Per selezionare un'unità organizzativa diversa, scegliere il pulsante **Sfoglia**. La finestra di dialogo visualizzerà tutte le unità organizzative presenti nella foresta all'interno dell'ambito specificato. Selezionare l'unità organizzativa desiderata e fare clic su **OK**.
    
      - **Proprietario**  Il proprietario di un gruppo di distribuzione dinamico è facoltativo. È possibile aggiungere proprietari facendo clic su **Sfoglia** e selezionando gli utenti dall'elenco.

3.      
    Utilizzare la sezione **Membri** per specificare i tipi di destinatari per il gruppo e configurare le regole che determineranno l'appartenenza. Selezionare una delle seguenti caselle:
    
      - **Tutti i tipi di destinatari**   Scegliere questa opzione per inviare messaggi che soddisfano i criteri definiti per questo gruppo a tutti i tipi di destinatario.
    
      - **Solo i seguenti tipi di destinatari**   I messaggi che soddisfano i criteri definiti per questo gruppo saranno inviati a uno o più dei seguenti tipi di destinatario:
        
          - **Utenti con cassette postali di Exchange**   Selezionare questa casella di controllo se si desidera includere gli utenti con cassette postali di Exchange. Gli utenti con cassette postali di Exchange sono gli utenti che dispongono di un account di dominio utente e una cassetta postale nell'organizzazione di Exchange.
        
          - **Utenti con indirizzi di posta elettronica esterni**   Selezionare questa casella di controllo se si desidera includere gli utenti con indirizzi di posta elettronica esterni. Gli utenti con account di posta elettronica esterni possiedono account di dominio utente in Active Directory, ma utilizzano account di posta elettronica esterni all'organizzazione. Ciò consente loro di essere inclusi nell'elenco indirizzi globale e aggiunti alle liste di distribuzione.
        
          - **Cassette postali per le risorse**   Selezionare questa casella di controllo se si desidera includere le cassette postali per le risorse di Exchange. Le cassette postali per le risorse consentono di gestire le risorse della società, ad esempio una sala conferenze o un veicolo aziendale, tramite una cassetta postale.
        
          - **Contatti con indirizzi di posta elettronica esterni**   Selezionare questa casella di controllo se si desidera includere i contatti con indirizzi di posta elettronica esterni. I contatti con indirizzi di posta elettronica esterni non possiedono account di dominio utente in Active Directory, ma il loro indirizzo di posta elettronica esterno è disponibile nell'elenco indirizzi globale.
        
          - **Gruppi abilitati alla posta**   Selezionare questa casella di controllo se si desidera includere i gruppi di protezione o i gruppi di distribuzione abilitati alla posta elettronica. I gruppi abilitati alla posta sono simili ai gruppi di distribuzione. I messaggi di posta elettronica inviati all'account di un gruppo abilitato alla posta elettronica saranno recapitati a diversi destinatari.

4.      
    Fare clic su **Aggiungi regola** per definire i criteri per l'appartenenza a questo gruppo.

5.  Selezionare uno dei seguenti attributi di destinatario dall'elenco a discesa e specificare un valore. Se il valore per l'attributo selezionato corrisponde al valore definito, il destinatario riceve un messaggio inviato a questo gruppo.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Attributo</th>
    <th>Invia messaggio a un destinatario se...</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Contenitore dei destinatari</strong></p></td>
    <td><p>L'oggetto destinatario risiede nel dominio o nell'unità organizzativa specificati.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Stato o provincia</strong></p></td>
    <td><p>Il valore specificato corrisponde alla proprietà Stato o provincia del destinatario.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Company</strong></p></td>
    <td><p>Il valore specificato corrisponde alla proprietà Azienda del destinatario.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Department</strong></p></td>
    <td><p>Il valore specificato corrisponde alla proprietà Reparto del destinatario.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Attributo personalizzatoN</strong> (dove N è un numero da 1 a 15)</p></td>
    <td><p>Il valore specificato corrisponde alla proprietà AttributoPersonalizzatoN del destinatario.</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!IMPORTANT]
    > I valori immessi per l'attributo selezionato devono corrispondere esattamente a quelli visualizzati nelle proprietà del destinatario. Ad esempio, se si immette <STRONG>Washington</STRONG> per <STRONG>Stato o provincia</STRONG>, ma il valore della proprietà del destinatario è <STRONG>WA</STRONG>, la condizione non risulta soddisfatta. Inoltre, per i valori di testo specificati non viene fatta distinzione tra maiuscole e minuscole. Ad esempio, se si specifica <STRONG>Contoso</STRONG> per l'attributo <STRONG>Azienda</STRONG>, i messaggi saranno inviati a un destinatario il cui valore relativo è <STRONG>contoso</STRONG>.



6.  Nella finestra **Specifica parole o frasi**, immettere il valore nella casella di testo. Fare clic su **Aggiungi**, quindi scegliere **OK**.

7.  Per aggiungere un'altra regola per definire i criteri di appartenenza, fare clic su **Aggiungi regola** sotto la regola precedentemente creata.
    

    > [!IMPORTANT]
    > Se si aggiungono più regole per definire l'appartenenza, un destinatario deve soddisfare i criteri di ogni regola per ricevere un messaggio inviato al gruppo. In altre parole, ogni regola è collegata alle altre con l'operatore booleano <STRONG>AND</STRONG>.



8.  Al termine, scegliere **Salva** per creare il gruppo di distribuzione dinamico.


> [!NOTE]
> Per specificare le regole per attributi diversi da quelli disponibili in EAC, è necessario utilizzare Shell per creare un gruppo di distribuzione dinamico. Va ricordato che le impostazioni per il filtro e le condizioni per i gruppi di distribuzione dinamici che dispongono di filtri di destinatari personalizzati possono essere gestite solo utilizzando Shell. Per un esempio di creazione di un gruppo di distribuzione dinamico con una query personalizzata, vedere la successiva sezione sull'utilizzo di Shell per creare un gruppo di distribuzione dinamico.



## Creazione di un gruppo di distribuzione dinamico tramite Shell

In questo esempio viene creato il gruppo di distribuzione dinamico "Mailbox Users DDG" contenente solo utenti di cassette postali.

    New-DynamicDistributionGroup -IncludedRecipients MailboxUsers -Name "Mailbox Users DDG" -OrganizationalUnit Users

In questo esempio, viene creato un gruppo di distribuzione dinamico con un filtro destinatario personalizzato. Il gruppo di distribuzione dinamico contiene tutti gli utenti di cassette postali su un server chiamato Server1.

    New-DynamicDistributionGroup -Name "Mailbox Users on Server1" -OrganizationalUnit Users -RecipientFilter {((RecipientTypeDetails -eq 'UserMailbox' -and ServerName -eq 'Server1'))}

In questo esempio, viene creato un gruppo di distribuzione dinamico con un filtro destinatario personalizzato. Il gruppo di distribuzione dinamico contiene tutti gli utenti di cassette postale che utilizzano il valore "FullTimeEmployee" nella proprietà **CustomAttribute10**.

    New-DynamicDistributionGroup -Name "Full Time Employees" -RecipientFilter {(RecipientTypeDetails -eq 'UserMailbox') -and (CustomAttribute10 -eq 'FullTimeEmployee')}

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [New-DynamicDistributionGroup](https://technet.microsoft.com/it-it/library/bb125127\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta creazione di un gruppo di distribuzione dinamico, effettuare una delle seguenti operazioni:

  - In EAC, individuare **Destinatari** \> **Gruppi**. Il nuovo gruppo di distribuzione dinamico è visualizzato nell'elenco dei gruppi. In **Tipo gruppo**, il tipo indicato è **Gruppo di distribuzione dinamico**.

  - In Shell, eseguire il comando riportato di seguito per visualizzare informazioni sul nuovo gruppo di distribuzione dinamico.
    
        Get-DynamicDistributionGroup | FL Name,RecipientTypeDetails,RecipientFilter,PrimarySmtpAddress

## Cambiare le proprietà del gruppo di distribuzione dinamico

## Utilizzare EAC per cambiare le proprietà del gruppo di distribuzione dinamico

1.  In EAC, individuare **Destinatari** \> **Gruppi**.

2.  Nell'elenco dei gruppi, fare clic sul gruppo di distribuzione dinamico da visualizzare o modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina delle proprietà del gruppo, fare clic su una delle sezioni indicate di seguito per visualizzare o modificare le proprietà.
    
      - Generale
    
      - Proprietà
    
      - Appartenenza
    
      - Gestione recapito
    
      - Approvazione del messaggio
    
      - Opzioni di posta elettronica
    
      - Avviso messaggio
    
      - Delega gruppo

## Generale

Utilizzare questa sezione per visualizzare o modificare le informazioni di base sul gruppo.

  - **\* Nome visualizzato**   Questo nome verrà visualizzato nella Rubrica, nei campi A: quando il messaggio di posta elettronica viene inviato a questo gruppo e nell'elenco Gruppi. Il nome visualizzato è obbligatorio e deve essere un nome descrittivo facilmente riconoscibile dagli utenti. Inoltre, deve essere univoco nel dominio in uso.

  - **\* Alias**   Questa è la parte dell'indirizzo di posta elettronica visualizzata a sinistra del simbolo di chiocciola (@). Se si modifica l'alias, verrà modificato anche l'indirizzo SMTP primario del gruppo in modo che contenga il nuovo alias. Inoltre, l'indirizzo di posta elettronica con il precedente alias verrà conservato come indirizzo proxy del gruppo.

  - **Descrizione**   Utilizzare questa casella per descrivere lo scopo del gruppo. Questa descrizione viene visualizzata nella rubrica e nel riquadro Dettagli dell'interfaccia di amministrazione di Exchange.

  - **Nascondi il gruppo dagli elenchi di indirizzi**   Selezionare questa casella di controllo per evitare che gli utenti vedano questo gruppo nella rubrica. Per inviare un messaggio di posta elettronica a questo gruppo, il mittente deve digitare l'alias o l'indirizzo di posta elettronica del gruppo nella riga A: o Cc: .

  - **Unità organizzativa**   Questa casella di sola lettura visualizza l'unità organizzativa (OU) contenente il gruppo di distribuzione dinamico. È necessario utilizzare Utenti e computer di Active Directory per spostare il gruppo in un'altra unità organizzativa.

## Proprietà

Utilizzare questa sezione per assegnare un proprietario al gruppo. Un gruppo di distribuzione dinamico può avere un solo proprietario. Il proprietario del gruppo viene visualizzato nella scheda **Gestito da** dell'oggetto in Utenti e computer di Active Directory.

È possibile aggiungere proprietari facendo clic su **Sfoglia** e selezionando un proprietario dall'elenco. Per rimuovere il proprietario, fare clic su **Cancella** e quindi su **Salva**.![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

## Appartenenza

Utilizzare questa sezione per cambiare i criteri utilizzati per determinare l'appartenenza al gruppo. È possibile eliminare o modificare le regole di appartenenza esistenti e aggiungere nuove regole. Per le procedure relative, vedere il Utilizzare EAC per creare un gruppo di distribuzione dinamico nelle procedure di configurazione dell'appartenenza durante l'utilizzo di EAC per creare un nuovo gruppo di distribuzione dinamico.

## Gestione recapito

Utilizzare questa sezione per gestire gli utenti che possono inviare posta elettronica a questo gruppo.

  - **Solo mittenti interni all'organizzazione**   Selezionare questa opzione per consentire l'invio di messaggi al gruppo solo ai mittenti dell'organizzazione. In questo modo, se un utente esterno all'organizzazione invia un messaggio di posta elettronica a questo gruppo, tale messaggio viene rifiutato. Questa impostazione è quella predefinita.

  - **Mittenti interni ed esterni all'organizzazione**   Selezionare questa opzione per consentire a tutti di inviare i messaggi al gruppo.
    
    È possibile limitare ulteriormente gli utenti che possono inviare messaggi al gruppo consentendo solo a mittenti specifici di inviare messaggi a questo gruppo. Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e quindi selezionare uno o più destinatari. I mittenti aggiunti a questo elenco saranno i soli a poter inviare posta al gruppo. I messaggi inviati da chiunque non sia presente nell'elenco verranno rifiutati.
    
    Per rimuovere un utente o un gruppo dall'elenco, selezionarlo nell'elenco, quindi fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").
    

    > [!IMPORTANT]
    > Se il gruppo è stato configurato per consentire l'invio di messaggi al gruppo solo da parte di mittenti all'interno dell'organizzazione, i messaggi di posta elettronica inviati da un contatto esterno saranno rifiutati, anche se il contatto è stato aggiunto a questo elenco.



## Approvazione del messaggio

Utilizzare questa sezione per impostare le opzioni di moderazione del gruppo. I moderatori approvano o rifiutano i messaggi inviati al gruppo prima che raggiungano i membri del gruppo.

  - **I messaggi inviati a questo gruppo sono stati approvati da un moderatore**   Per impostazione predefinita, questa casella di controllo non è selezionata. Se si seleziona questa casella di controllo, i moderatori del gruppo esaminano i messaggi in arrivo prima di procedere al relativo recapito. I moderatori del gruppo possono approvare o rifiutare i messaggi in arrivo.

  - **Moderatori del gruppo**   Per aggiungere moderatori al gruppo, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere un moderatore, selezionarlo, quindi fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi"). Se è stata selezionata l'opzione "I messaggi inviati a questo gruppo sono stati approvati da un moderatore" senza tuttavia aver selezionato alcun moderatore, i messaggi destinati al gruppo verranno inviati ai proprietari del gruppo per l'approvazione.

  - **Mittenti che non richiedono l'approvazione dei messaggi** Per aggiungere utenti o gruppi in grado di ignorare la moderazione del gruppo, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi"). Per rimuovere una utente o un gruppo, selezionarlo e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

  - **Seleziona notifiche di moderazione   **Utilizzare questa sezione per stabilire in che modo gli utenti vengono avvisati dell'approvazione del messaggio.
    
      - **Notificare a tutti i mittenti che i loro messaggi non sono stati approvati**   Questa è l'impostazione predefinita. Consente di notificare qualsiasi mittente, sia esso interno o esterno all'organizzazione, in merito alla non approvazione del messaggio che ha inviato.
    
      - **Notificare ai mittenti dell'organizzazione solo i messaggi non approvati**   Quando si seleziona questa opzione, solo gli utenti e i gruppi dell'organizzazione ricevono una notifica quando un messaggio che hanno inviato al gruppo non viene approvato da un moderatore.
    
      - **Non inviare alcuna notifica quando un messaggio non è approvato**   Se si seleziona questa opzione, non vengono inviate notifiche ai mittenti quando i loro messaggi non vengono approvati dai moderatori del gruppo.

## Opzioni di posta elettronica

Utilizzare questa sezione per visualizzare o modificare gli indirizzi di posta elettronica associati al gruppo. Ciò include gli indirizzi SMTP primari del gruppo e qualsiasi indirizzo proxy ad esso associato. L'indirizzo SMTP primario (chiamato anche *indirizzo di risposta*) viene visualizzato in grassetto nell'elenco degli indirizzi, con il valore **SMTP** maiuscolo nella colonna **Tipo**.

  - **Aggiungi **  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per aggiungere un nuovo indirizzo di posta elettronica per la cassetta postale. Selezionare uno dei seguenti tipi di indirizzo:
    
      - **SMTP**   Questo è il tipo di indirizzo predefinito. Fare clic su questo pulsante e quindi digitare il nuovo indirizzo SMTP nella casella **\* Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Per impostare il nuovo indirizzo SMTP come primario per il gruppo, selezionare la casella di controllo <STRONG>Imposta questo indirizzo come indirizzo di risposta</STRONG>.

    
      - **Tipo di indirizzo personalizzato**   Fare clic su questo pulsante e digitare uno dei tipi di indirizzi di posta elettronica non SMTP supportati nella casella **\* Indirizzo di posta elettronica**.
        

        > [!NOTE]
        > Ad eccezione degli indirizzi X.400, Exchange non convalida gli indirizzi personalizzati per una formattazione corretta. È necessario verificare che l'indirizzo personalizzato specificato sia conforme ai requisiti di formato per tale tipo di indirizzo.



  - **Modifica**   Per cambiare un indirizzo di posta elettronica associato al gruppo, selezionarlo nell'elenco e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").
    

    > [!NOTE]
    > Per impostare un indirizzo SMTP esistente come primario per il gruppo, selezionare la casella di controllo <STRONG>Imposta questo indirizzo come indirizzo di risposta</STRONG>.



  - **Rimuovi**   Per eliminare un indirizzo di posta elettronica associato al gruppo, selezionarlo nell'elenco e fare clic su **Rimuovi**![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi").

  - **Aggiorna automaticamente gli indirizzi sulla base del criterio dell'indirizzo di posta elettronica applicato a questo destinatario   **Selezionare questa casella di controllo per aggiornare automaticamente gli indirizzi di posta elettronica dei destinatari in base alle modifiche apportate ai criteri degli indirizzi di posta elettronica nell'organizzazione. Tale casella è selezionata per impostazione predefinita.

## Avviso messaggio

Utilizzare questa sezione per aggiungere un avviso per informare gli utenti dei problemi che potrebbero verificarsi se inviano un messaggio a questo gruppo. Un avviso messaggio è un testo che viene visualizzato sulla barra informazioni quando questo gruppo viene aggiunto nella riga A, Cc o Ccn di un nuovo messaggio di posta elettronica. Ad esempio, è possibile aggiungere un Avviso messaggio ai gruppi di grandi dimensioni per avvertire i mittenti potenziali che il messaggio verrà inviato a molte persone.


> [!NOTE]
> Gli avvisi messaggio possono includere tag HTML, ma gli script non sono consentiti. La lunghezza di un avviso messaggio personalizzato non può superare 175 caratteri visualizzati. I tag HTML non vengono conteggiati in tale limite.



## Delega gruppo

Utilizzare questa sezione per assegnare a un utente (chiamato *delegato*) le autorizzazioni necessarie per permettergli di inviare messaggi come gruppo o per conto del gruppo. È possibile assegnare le seguenti autorizzazioni:

  - **Invia come**   Questa autorizzazione consente al delegato di inviare i messaggi come gruppo. Una volta assegnata l'autorizzazione, il delegato può scegliere di aggiungere il gruppo nella riga **Da** per indicare che il messaggio è stato inviato dal gruppo.

  - **Invia per conto di**   Anche questa autorizzazione consente a un delegato di inviare messaggi per conto del gruppo. Una volta assegnata questa autorizzazione, il delegato ha la possibilità di aggiungere il gruppo alla riga **Da**. Il messaggio risulterà essere stato inviato dal gruppo e indicherà che è stato inviato dal delegato per conto del gruppo.

Per assegnare le autorizzazioni ai delegati, fare clic su **Aggiungi** sotto l'autorizzazione desiderata per visualizzare la pagina **Scegli il destinatario** che contiene un elenco di destinatari nell'organizzazione Exchange a cui può essere assegnata l'autorizzazione. Selezionare i destinatari desiderati, aggiungerli all'elenco e fare clic su **OK**. È inoltre possibile cercare uno specifico destinatario digitandone il nome nella casella di ricerca e quindi facendo clic su **Cerca**.

## Utilizzare Shell per cambiare le proprietà del gruppo di distribuzione dinamico

Utilizzare i cmdlet **Get-DynamicDistributionGroup** e **Set-DynamicDistributionGroup** per visualizzare e modificare le proprietà dei gruppi di distribuzione dinamici. I vantaggi dell'utilizzo di Shell sono la possibilità di cambiare le proprietà non disponibili in EAC e l'opportunità di modificare le proprietà per più gruppi. Per informazioni sui parametri corrispondenti alle proprietà del gruppo di distribuzione, consultare i seguenti argomenti:

  - [Get-DynamicDistributionGroup](https://technet.microsoft.com/it-it/library/bb124762\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/it-it/library/bb123796\(v=exchg.150\))

Ecco alcuni esempi dell'utilizzo di Shell per cambiare le proprietà del gruppo di distribuzione dinamico.

In questo esempio vengono modificati i seguenti parametri per tutti i gruppi di distribuzione dinamici nell'organizzazione:

  - Nascondere tutti i gruppi di distribuzione dinamici dalla rubrica

  - Impostare le dimensioni massime dei messaggi che possono essere inviati al gruppo su 5 MB

  - Abilitare la moderazione

  - Assegnare l'amministratore come moderatore del gruppo

<!-- end list -->

    Get-DynamicDistributionGroup -ResultSize unlimited | Set-DynamicDistributionGroup -HiddenFromAddressListsEnabled $true -MaxReceiveSize 5MB -ModerationEnabled $true -ModeratedBy administrator

In questo esempio viene aggiunto l'indirizzo di posta elettronica SMTP proxy, Seattle.Employees@contoso.com, al gruppo All Employees.

    Set-DynamicDistributionGroup -Identity "All Employees" -EmailAddresses SMTP:All.Employees@contoso.com, smtp:Seattle.Employees@contoso.com

## Come verificare se l'operazione ha avuto esito positivo

Per verificare la corretta modifica delle proprietà di un gruppo di distribuzione dinamico, effettuare le seguenti operazioni:

  - Nell'interfaccia di amministrazione di Exchange, selezionare il gruppo e quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica") per visualizzare la proprietà o la funzionalità modificata. A seconda della proprietà modificata, è possibile che questa venga visualizzata nel riquadro Dettagli del gruppo selezionato.

  - In Shell, utilizzare il cmdlet **Get-DynamicDistributionGroup** per verificare le modifiche. Uno dei vantaggi offerti dall'utilizzo di Shell è la possibilità di visualizzare più proprietà per più gruppi. Nel primo esempio, occorre eseguire il seguente comando per verificare i nuovi valori.
    
        Get-DynamicDistributionGroup -ResultSize unlimited | fl Name,HiddenFromAddressListsEnabled,MaxReceiveSize,ModerationEnabled,ModeratedBy
    
    Nell'esempio in alto in cui sono stati modificati i limiti dei messaggi, eseguire questo comando.
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

