---
title: 'Rapporti di controllo di Exchange: Exchange 2013 Help'
TOCTitle: Rapporti di controllo di Exchange
ms:assetid: 2b3e1529-1677-4564-be0b-ce22757ddc0d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150497(v=EXCHG.150)
ms:contentKeyID: 50479708
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rapporti di controllo di Exchange

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Utilizzare la registrazione di controllo per risolvere problemi di configurazione tenendo traccia di modifiche specifiche apportate dagli amministratori e consentire di soddisfare requisiti relativi alle normative, alla conformità e alle controversie. In Microsoft Exchange sono disponibili due tipi di registrazione di controllo:

  - *Registrazione di controllo dell'amministratore* consente di registrare qualsiasi azione in caso di un cmdlet di Exchange Management Shell, eseguite da un amministratore. Ciò consente di risolvere i problemi di configurazione o identificare la causa dei problemi correlati alla sicurezza o conformità. In Exchange Online, le azioni eseguite dagli amministratori di Microsoft e amministratori delegati, vengono registrate anche.

  - *Registrazione di controllo delle cassette postali* record quando si accede a una cassetta postale da un amministratore, un utente delegato o persona proprietario della cassetta postale. Ciò consente di determinare chi ha accesso a una cassetta postale ed è stata effettuata.

In questo argomento sono contenute le sezioni seguenti:

  - Export audit logs

  - Run auditing reports

  - Configure audit logging
    
      - Enable mailbox audit logging
    
      - Give users access to auditing reports
    
      - Configure Outlook Web App to allow XML attachments

## Esportare registri di controllo

**Gestione della conformità** \> pagina **controllo** nell'interfaccia di amministrazione di Exchange (EAC), è possibile cercare ed esportare le voci dall'amministratore di controllare il Registro di controllo delle cassette postali e registro.

  - **Esportare il Registro di controllo dell'amministratore**   Qualsiasi azione eseguita da un amministratore che si basa su un cmdlet della Shell e non inizia con i verbi **Get**, **Search**o **Test** viene registrata nel Registro di controllo dell'amministratore. Le voci del Registro di controllo includono il cmdlet è stato eseguito, il parametro e valori utilizzati con il cmdlet e quando l'operazione è riuscita. È possibile cercare ed esportare le voci nel Registro di controllo. Quando si esportano i risultati della ricerca, Microsoft Exchange salvarli in un file XML e lo collega a un messaggio di posta elettronica. Per ulteriori informazioni, vedere:
    
      - [Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)
    
      - [Visualizzare ed esportare log di controllo dell'amministratore esterno](https://technet.microsoft.com/it-it/library/dn505728\(v=exchg.150\))
    

    > [!NOTE]
    > Per impostazione predefinita, le voci del Registro di controllo admin vengono conservate per 90 giorni. Quando una voce è 90 giorni, viene eliminato. Questa impostazione non può essere modificata in un'organizzazione basata su cloud. Tuttavia, possono essere modificata in un'organizzazione di Exchange locale utilizzando il cmdlet <STRONG>Set-AdminAuditLog</STRONG> .



  - **Esportare registri di controllo delle cassette postali**   Quando controllo delle cassette postali è abilitata la registrazione per una cassetta postale, Microsoft Exchange archivia un record delle azioni eseguite sui dati della cassetta postale da non proprietari nel Registro di controllo delle cassette postali, viene archiviato in una cartella nascosta nella cassetta postale sottoposto a controllo. Controllo delle cassette postali registrazione inoltre possibile configurare per registrare le azioni di proprietario. Voci di questo registro indicano che si accede alla cassetta postale e quando le azioni eseguite e l'azione è stata eseguita correttamente. Quando esegue la ricerca per le voci di controllo delle cassette postali accedere ed esportarli, salvataggi di Microsoft Exchange la ricerca dei risultati in un file XML e lo collega a un messaggio di posta elettronica. Per ulteriori informazioni, vedere [Esportare registri di controllo delle cassette postali](export-mailbox-audit-logs-exchange-2013-help.md).

## Eseguire rapporti di controllo

Quando si esegue uno dei seguenti rapporti nella pagina **controllo** nell'interfaccia di amministrazione di Exchange, i risultati vengono visualizzati nel riquadro dei dettagli del rapporto.

  - **Eseguire un rapporto di accesso non proprietario della cassetta postale**   Utilizzare questo rapporto per individuare le cassette postali accessibile da un utente diverso da persona proprietario della cassetta postale. Per ulteriori informazioni, vedere [Eseguire un rapporto di accesso non proprietario della cassetta postale](run-a-non-owner-mailbox-access-report-exchange-online-help.md).

  - **Esegui il rapporto di un gruppo di ruoli amministratore**   Utilizzare questo rapporto per cercare le modifiche apportate ai gruppi di ruoli amministratore. Per ulteriori informazioni, vedere [Ricerca delle modifiche al gruppo di ruoli o i registri di controllo dell'amministratore](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

  - **Esegui un rapporto di individuazione e conservazione in locale**   Utilizzare questo rapporto per individuare le cassette postali conservate in locale o rimosse dalla conservazione in locale. Per ulteriori informazioni, vedere:
    
      - [Archiviazione sul posto e conservazione per controversia legale](in-place-hold-and-litigation-hold-exchange-2013-help.md)
    
      - [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md)

  - **Eseguire un rapporto di attesa di conservazione per controversia per cassetta postale**   Utilizzare questo rapporto per individuare le cassette postali che sono stati messi in o rimosse dalla conservazione per controversia legale. Per ulteriori informazioni, vedere.
    
      - [Eseguire un rapporto di attesa di conservazione per controversia per cassetta postale](run-a-per-mailbox-litigation-hold-report-exchange-2013-help.md)
    
      - [Conservazione in caso di dispute di una cassetta postale](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - **Eseguire il report del log di controllo amministrazione**   Utilizzare questo report per visualizzare le voci nel Registro di controllo. Invece di esportazione nel Registro di controllo, che può richiedere fino a 24 ore per ricevere un messaggio di posta elettronica, è possibile eseguire questo report in EAC. In questo report consente di registrare le modifiche di configurazione apportate dagli amministratori dell'organizzazione. Verranno visualizzate fino a 5000 voci su più pagine. Per limitare la ricerca, è possibile specificare un intervallo di date. Per ulteriori informazioni, vedere:
    
      - [Visualizzare il registro di controllo dell'amministratore](view-the-administrator-audit-log-exchange-2013-help.md)
    
      - [Registrazione controlli dell'amministratore](administrator-audit-logging-exchange-2013-help.md)

  - **Eseguire il report del log di controllo amministratore esterno**   In questo report è disponibile solo in Exchange Online e Exchange Online Protection. Le azioni eseguite dagli amministratori di Microsoft o gli amministratori delegati vengono registrati nel Registro di controllo dell'amministratore. Utilizzare il report del log di controllo amministratore esterno per la ricerca e visualizzare le azioni che gli amministratori all'esterno dell'organizzazione eseguire la configurazione dell'organizzazione Exchange Online. Per ulteriori informazioni, vedere [Visualizzare ed esportare log di controllo dell'amministratore esterno](https://technet.microsoft.com/it-it/library/dn505728\(v=exchg.150\)).

## Configurare la registrazione di controllo

Prima di poter creare i rapporti di controllo ed esportare i registri di controllo, è necessario configurare la registrazione di controllo per l'organizzazione.

## Abilitare la registrazione di controllo della cassetta postale

È necessario abilitare la registrazione di controllo della cassetta postale per ogni cassetta postale per la quale si desidera eseguire un rapporto di accesso non proprietario. Se la registrazione di controllo non è abilitata per una cassetta postale, la creazione di un rapporto o l'esportazione del registro di controllo della cassetta postale non produrrà alcun risultato per tale cassetta postale.

Per abilitare la registrazione di controllo della cassetta postale per una sola cassetta postale, utilizzare il seguente comando in Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Per abilitare il controllo su tutte le cassette postali degli utenti di un'organizzazione, eseguire i comandi riportati di seguito.

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

Per ulteriori informazioni sulla configurazione dei quali vengono registrate, vedere:

  - **Exchange 2013**    [Abilitare o disabilitare la registrazione per una cassetta postale di controllo delle cassette postali](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)

  - **Exchange Online** Abilitare il controllo in Office 365https://go.microsoft.com/fwlink/p/?LinkId=626109   

## Concessione agli utenti dell'accesso ai rapporti di controllo

Per impostazione predefinita, gli amministratori possono accedere e creare qualsiasi rapporto nella pagina Controllo nell'interfaccia di amministrazione di Exchange. Agli altri utenti, quali i responsabili record o il personale legale, occorre invece assegnare le autorizzazioni necessarie.

Il modo più semplice per fornire agli utenti l'accesso è per aggiungerli al gruppo di ruoli di gestione dei record. È inoltre possibile utilizzare Shell per assegnare un utente l'accesso alla pagina **controllo** nell'interfaccia di amministrazione di Exchange mediante l'assegnazione di ruolo registri di controllo per l'utente.

## Aggiunta di un utente al gruppo di ruoli Gestione record

1.  Accedere ad **Autorizzazioni** \> **Ruoli amministrativi**.

2.  Nell'elenco dei gruppi di ruoli, fare clic su **Gestione record**, quindi su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Membri**, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

4.  Nella finestra di dialogo **Seleziona membri**, scegliere l'utente. È possibile cercare un utente digitandone il nome visualizzato, completo o parziale, e facendo clic su **Cerca**![icona Cerca](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "icona Cerca"). È inoltre possibile ordinare l'elenco facendo clic sull'intestazione di colonna **Nome** o **Nome visualizzato**.

5.  Fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") e quindi su **OK** per tornare alla pagina del gruppo di ruoli.

6.  Fare clic su **Salva** per salvare la modifica al gruppo di ruoli.

Nel riquadro dei dettagli, l'utente è ora incluso nell'elenco **Membri** e può accedere alla pagina Controllo nell'interfaccia di amministrazione di Exchange, creare i rapporti di controllo ed esportare i registri di controllo.

## Assegnazione del ruolo Registri di controllo a un utente

Per assegnare il ruolo Registri di controllo a un utente, utilizzare il seguente comando.

    New-ManagementRoleAssignment -Role "Audit Logs" -User <Identity>

In questo modo l'utente potrà selezionare **Gestione conformità** \> **Controllo** nell'interfaccia di amministrazione di Exchange per creare un qualsiasi rapporto. Potrà inoltre esportare il registro di controllo della cassetta postale e visualizzare quello dell'amministratore.


> [!NOTE]
> Per consentire a un utente di creare i rapporti di controllo, ma non di esportare i registri di controllo, utilizzare il comando precedente per assegnargli il ruolo Registri di controllo in sola visualizzazione.



## Configurare Outlook Web App per consentire gli allegati XML

Quando si esporta il registro di controllo della cassetta postale o quello dell'amministratore, Microsoft Exchange allega il registro di controllo in formato XML a un messaggio di posta elettronica. Tuttavia, Outlook Web App blocca gli allegati XML per impostazione predefinita. Se si desidera utilizzare Outlook Web App per accedere a questi registri di controllo, è necessario configurare Outlook Web App per il supporto degli allegati XML.

Per consentire gli allegati XML in Outlook Web App, utilizzare il seguente comando.

    Set-OwaMailboxPolicy -Identity Default -AllowedFileTypes '.rpmsg','.xlsx','.xlsm','.xlsb','.tiff','.pptx','.pptm','.ppsx','.ppsm','.docx','.docm','.zip','.xls','.wmv','.wma','.wav','.vsd','.txt','.tif','.rtf','.pub','.ppt','.png','.pdf','.one','.mp3','.jpg','.gif','.doc','.bmp','.avi','.xml'

