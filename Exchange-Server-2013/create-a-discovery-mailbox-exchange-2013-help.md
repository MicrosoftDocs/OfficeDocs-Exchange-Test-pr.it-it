---
title: 'Creazione di una cassetta postale di individuazione: Exchange 2013 Help'
TOCTitle: Creazione di una cassetta postale di individuazione
ms:assetid: bc20285d-35e2-4e49-9bd3-38abf96114ba
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638177(v=EXCHG.150)
ms:contentKeyID: 50481517
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Creazione di una cassetta postale di individuazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Microsoft Exchange Server 2013 il programma di installazione consente di creare una cassetta postale di individuazione per impostazione predefinita. In Exchange Online, per impostazione predefinita viene creata anche una cassetta postale di individuazione. Cassette postali di individuazione vengono utilizzate come cassette postali di destinazione per le ricerche [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md) in Interfaccia di amministrazione di Exchange (EAC). È possibile creare cassette postali di individuazione aggiuntive in base alle esigenze. Dopo aver creato una nuova cassetta postale di individuazione, è necessario assegnare le autorizzazioni accesso completo per gli utenti appropriati in modo che possano accedere i risultati della ricerca eDiscovery che vengono copiati nella cassetta postale di individuazione.


> [!WARNING]
> Una volta che un responsabile dell'individuazione ha copiato i risultati di una ricerca eDiscovery in una cassetta postale di individuazione, questa potrebbe contenere informazioni riservate. È necessario controllare l'accesso alle cassette postali di individuazione e assicurarsi che sia consentito solo agli utenti autorizzati.



Per ulteriori informazioni, vedere [Discovery mailboxes](in-place-ediscovery-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Creazione di cassette postali di individuazione" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Le cassette postali di individuazione dispongono di una quota di archiviazione delle cassette postali di 50 gigabyte (GB). Questo limite di archiviazione può essere aumentato.

  - È possibile utilizzare EAC per creare una cassetta postale di individuazione o assegnare autorizzazioni per l'accesso. È necessario utilizzare la Shell. In Office 365, utilizzare Remote PowerShell connessa all'organizzazione Exchange Online.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## (Facoltativo) Passaggio 1: Connessione a Exchange Online tramite remote PowerShell

È sufficiente eseguire questo passaggio se si dispone di un'organizzazione di Exchange Online o Office 365. Se si dispone di un'organizzazione Exchange Server 2013, andare al passaggio successivo, eseguire il comando in Exchange Management Shell.

1.  Nel computer locale, aprire Windows PowerShell ed eseguire il seguente comando.
    
        $UserCredential = Get-Credential
    
    Nella finestra di dialogo **Richiesta credenziali di Windows PowerShell**, digitare il nome utente e la password per l'account dell'amministratore globale Office 365 e fare clic su **OK**.

2.  Eseguire il comando riportato di seguito.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  Eseguire il comando riportato di seguito.
    
        Import-PSSession $Session

4.  Per verificare di essere connessi alla propria organizzazione Exchange Online, eseguire il seguente comando per visualizzare un elenco di tutte le cassette postali dell'organizzazione:
    
        Get-Mailbox

Per ulteriori informazioni o nel caso di problemi di connessione all'organizzazione Exchange Online, vedere [Connect a Exchange Online tramite remote PowerShell](https://go.microsoft.com/fwlink/p/?linkid=517283).

## Passaggio 2: Creare una cassetta postale di individuazione

In questo esempio viene creata una cassetta postale di individuazione denominata SearchResults.

    New-Mailbox -Name SearchResults -Discovery 

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [New-Mailbox](https://technet.microsoft.com/it-it/library/aa997663\(v=exchg.150\)).

Per visualizzare un elenco di tutte le cassette postali di individuazione in una organizzazione di Exchange, eseguire il seguente comando:

    Get-Mailbox -Resultsize unlimited -Filter {RecipientTypeDetails -eq "DiscoveryMailbox"}

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)).

## Passaggio 3: Assegnare le autorizzazioni a una cassetta postale di individuazione

È necessario assegnare in modo esplicito utenti o gruppi le autorizzazioni necessarie per aprire una cassetta postale di individuazione che sia stata creata. Utilizzare la sintassi seguente per assegnare un utente o gruppo le autorizzazioni per aprire una cassetta postale di individuazione e visualizzare i risultati di ricerca:

    Add-MailboxPermission <Name of the discovery mailbox> -User <Name of user or group> -AccessRights FullAccess -InheritanceType all

Ad esempio, il seguente comando consente di assegnare autorizzazioni di accesso completo al gruppo di gestori delle controversie. In questo modo, i membri del gruppo possono aprire la cassetta postale di individuazione denominata Controversia Fabrikam.

    Add-MailboxPermission "Fabrikam Litigation" -User "Litigation Managers" -AccessRights FullAccess -InheritanceType all

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Add-MailboxPermission](https://technet.microsoft.com/it-it/library/bb124097\(v=exchg.150\)).

## Ulteriori informazioni

  - Per impostazione predefinita, solo i membri del gruppo di ruoli Gestione individuazione dispongono delle autorizzazioni di accesso completo per la cassetta postale di ricerca individuazione predefinita. È necessario assegnare l'autorizzazione di accesso completo in modo esplicito al gruppo di ruoli Gestione individuazione se si desidera che i membri siano in grado di aprire la cassetta postale di individuazione creata.

  - Anche se visibili negli elenchi indirizzi di Exchange, gli utenti non possono inviare messaggi di posta elettronica a una cassetta postale di individuazione. Il recapito di messaggi di posta elettronica alle cassette postali di individuazione è proibito con le restrizioni di recapito. Ciò preserva l'integrità dei risultati di ricerca copiati in una cassetta postale di individuazione.

  - Una cassetta postale di individuazione non può essere reimpiegata o convertita in un altro tipo di cassetta postale.

  - È possibile rimuovere una cassetta postale di individuazione con la stessa procedura utilizzata per le altre cassette postali.

