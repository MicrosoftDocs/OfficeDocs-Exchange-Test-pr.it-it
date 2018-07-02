---
title: 'Eseguire un rapporto di accesso non proprietario della cassetta postale: Exchange 2013 Help'
TOCTitle: Eseguire un rapporto di accesso non proprietario della cassetta postale
ms:assetid: dbbef170-e726-4735-abf1-2857db9bb52d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150575(v=EXCHG.150)
ms:contentKeyID: 50479803
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eseguire un rapporto di accesso non proprietario della cassetta postale

 

_**Si applica a:** Exchange Online_

_**Ultima modifica dell'argomento:** 2016-12-09_

Non-proprietario della cassetta postale accesso Report nell'interfaccia di amministrazione di Exchange (EAC) sono elencate le cassette postali che sono state eseguite da un utente diverso da persona proprietario della cassetta postale. Quando si accede a una cassetta postale di un utente non proprietario, Microsoft Exchange registra informazioni su questa azione in un registro di controllo delle cassette postali che viene archiviato come messaggio di posta elettronica in una cartella nascosta nella cassetta postale da controllare. Le voci di registro verranno visualizzate come risultati di ricerca e includere un elenco delle cassette postali a cui si accede a un utente non proprietario, che ha accesso alla cassetta postale e, le azioni eseguite l'utente non proprietario, e l'azione è stata eseguita correttamente. Per impostazione predefinita, le voci nel Registro di controllo delle cassette postali vengono conservate per 90 giorni.

Quando si abilita cassetta postale registrazione di controllo per una cassetta postale di Microsoft Exchange azioni specifiche di registri non proprietari, inclusi gli amministratori sia gli utenti, viene chiamati *delega agli utenti*, che sono stati assegnati autorizzazioni a una cassetta postale. È inoltre possibile limitare la ricerca agli utenti interni o esterni all'organizzazione.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo delle cassette postali" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Abilitare la registrazione di controllo della cassetta postale

È necessario abilitare per ciascuna cassetta postale che si desidera eseguire un rapporto di accesso non proprietario della cassetta postale per la registrazione di controllo delle cassette postali. Se il controllo delle cassette postali non è abilitata la registrazione, si non si ottengono risultati quando si esegue un report.

Per abilitare la registrazione per una singola cassetta postale di controllo delle cassette postali, eseguire il seguente comando Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Ad esempio, per abilitare il controllo delle cassette postali per un utente denominato Florence Flipo, eseguire il comando seguente.

    Set-Mailbox "Florence Flipo" -AuditEnabled $true

Per abilitare il controllo su tutte le cassette postali degli utenti di un'organizzazione, eseguire i comandi riportati di seguito.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## Come verificare se l'operazione ha avuto esito positivo?

Eseguire il comando seguente per verificare di aver configurato correttamente cassetta postale di registrazione di controllo.

    Get-Mailbox | FL Name,AuditEnabled

Il valore `True` impostato per la proprietà *AuditEnabled* consente di verificare se la registrazione di controllo è abilitata.

Torna all'inizio

## Eseguire un rapporto di accesso non proprietario della cassetta postale

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Gestione conformità** \> **Controllo**.

2.  Fare clic su **Esegui un report di accesso non proprietario della cassetta postale**.
    
    Per impostazione predefinita, Microsoft Exchange viene eseguito il report per l'accesso non proprietario per tutte le cassette postali nell'organizzazione negli ultimi due settimane. Le cassette postali elencate nei risultati della ricerca sono state abilitate per la cassetta postale di registrazione di controllo.

3.  Per visualizzare l'accesso non proprietario per una specifica cassetta postale, selezionare la cassetta postale dall'elenco delle cassette postali. Visualizzare i risultati di ricerca nel riquadro dei dettagli.


> [!TIP]
> Come limitare i risultati della ricerca Selezionare la data di inizio e la data di fine, o entrambe, e selezionare le cassette postali specifiche in cui eseguire la ricerca. Fare clic su <STRONG>Cerca</STRONG> per eseguire nuovamente il rapporto.



## Ricerca per specifici tipi di accesso non proprietario

È inoltre possibile specificare il tipo di accesso non proprietario, denominato anche il tipo di accesso, effettuare una ricerca. Di seguito sono le opzioni:

  - **Tutti i non proprietari**    Cercare l'accesso per gli amministratori e utenti delegati all'interno dell'organizzazione. Include inoltre dell'accesso utenti esterni all'organizzazione.

  - **Utenti esterni**    Cercare l'accesso da parte di utenti esterni all'organizzazione.

  - **Amministratori e utenti delegati**   Consente di cercare l'accesso da parte di amministratori e utenti delegati all'interno dell'organizzazione.

  - **Amministratori**   Consente di cercare l'accesso da parte degli amministratori dell'organizzazione.

Torna all'inizio

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare che è stato eseguito correttamente un rapporto di accesso non proprietario della cassetta postale, controllare il riquadro dei risultati di ricerca. Cassette postali che è stato eseguito il report per vengono visualizzate nel riquadro. Se non sono disponibili risultati per una specifica cassetta postale, è possibile non è stato access da un utente non proprietario oppure che accesso non proprietario non ha avuto luogo nell'intervallo di date specificato. Come descritto in precedenza, è necessario verificare che la registrazione di controllo è stata abilitata per le cassette postali che si desidera eseguire la ricerca per l'accesso da non proprietari.

Torna all'inizio

## Che cosa viene registrato nel Registro di controllo delle cassette postali?

Quando si esegue un report di accesso non proprietario della cassetta postale, le voci dal Registro di controllo delle cassette postali vengono visualizzate nei risultati della ricerca in EAC. Ogni voce del report contiene informazioni:

  - Ha avuto accesso alla cassetta postale e quando

  - Le azioni eseguite l'utente non proprietario

  - Il messaggio interessato e il relativo percorso della cartella

  - L'azione è stata eseguita correttamente

Nella tabella seguente vengono riportate le azioni eseguite dagli non proprietari che possono essere registrati dalla cassetta postale di registrazione di controllo. Della tabella, un **Sì** indica che l'azione può essere registrata per quel tipo di accesso e **No** indica che non è possibile registrare un'azione. Un asterisco (**\***) indica che l'azione viene registrata per impostazione predefinita, quando la registrazione di controllo delle cassette postali è abilitata per la cassetta postale. Se si desidera tenere traccia delle operazioni che non sono connessi per impostazione predefinita, è necessario utilizzare PowerShell per abilitare la registrazione di tali azioni.


> [!NOTE]
> Un amministratore è stata assegnata l'autorizzazione accesso completo alla cassetta postale dell'utente viene considerato un utente delegato.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Azione</th>
<th>Descrizione</th>
<th>Amministratore</th>
<th>Utente delegato</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Copy</strong></p></td>
<td><p>Messaggio copiato in un'altra cartella.</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><strong>Create</strong></p></td>
<td><p>Elemento creato nella cartella Calendario, Contatti, Note o Attività nella cassetta postale; ad esempio, viene creata una nuova convocazione di riunione. La creazione della cartella o del messaggio non viene sottoposta a controllo.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderBind</strong></p></td>
<td><p>È stata eseguita una cartella delle cassette postali.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p><strong>Elimina definitivamente</strong></p></td>
<td><p>Messaggio eliminato dalla cartella Elementi ripristinabili.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
</tr>
<tr class="odd">
<td><p><strong>MessageBind</strong></p></td>
<td><p>Messaggio visualizzato nel riquadro di anteprima o aperto.</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><strong>Move</strong></p></td>
<td><p>Messaggio spostato in un'altra cartella.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p><strong>Spostare gli elementi eliminati</strong></p></td>
<td><p>Messaggio spostato nella cartella Posta eliminata.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p><strong>Invia come</strong></p></td>
<td><p>Messaggio inviato utilizzando l'autorizzazione SendAs. Ciò significa che un altro utente ha inviato il messaggio come se provenisse dal proprietario della cassetta postale.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Invia per conto di</strong></p></td>
<td><p>Messaggio inviato utilizzando l'autorizzazione SendOnBehalf. Ciò significa che un altro utente ha inviato il messaggio per conto del proprietario della cassetta postale. Il messaggio indicherà al destinatario per conto di chi è stato inviato il messaggio e chi ha effettivamente inviato il messaggio.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="even">
<td><p><strong>Elimina temporaneamente</strong></p></td>
<td><p>Messaggio eliminato dalla cartella Posta eliminata.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Aggiorna</strong></p></td>
<td><p>Messaggio modificato.</p></td>
<td><p>Sì*</p></td>
<td><p>Sì*</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> *&nbsp;Controllo eseguito per impostazione predefinita, se per la cassetta postale è abilitato il controllo.



Torna all'inizio

