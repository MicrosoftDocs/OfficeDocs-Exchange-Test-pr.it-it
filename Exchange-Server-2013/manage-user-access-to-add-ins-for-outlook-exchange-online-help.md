---
title: "Gestione dell'accesso degli utenti alle app per Outlook: Exchange 2013 Help"
TOCTitle: Gestione dell'accesso degli utenti alle app per Outlook
ms:assetid: e5833dec-a23a-439e-ac03-92671817bff8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ943757(v=EXCHG.150)
ms:contentKeyID: 52063110
ms.date: 05/05/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Gestione dell'accesso degli utenti alle app per Outlook

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2018-04-17_

È possibile utilizzare l'interfaccia di amministrazione di Exchange (EAC) o Exchange PowerShell per gestire l'accesso degli utenti ai componenti aggiuntivi per Outlook.

  - Con EAC è possibile gestire le impostazioni di accesso di base ai componenti aggiuntivi per gli utenti a livello organizzativo. Ad esempio, è possibile abilitare o disabilitare un componente aggiuntivo per gli utenti. È possibile, inoltre, specificare se un componente aggiuntivo è necessario o facoltativo per gli utenti.

  - Con Exchange Management Shell o PowerShell per Exchange Online, è possibile gestire tutte le impostazioni definibili in EAC e altre. Ad esempio, è possibile limitare la disponibilità a specifici utenti dell'organizzazione.

Per altre attività di gestione, vedere [App per Outlook](add-ins-for-outlook-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 5 minuti.

  - Per ulteriori informazioni sull'interfaccia di amministrazione di Exchange, vedere [Interfaccia di amministrazione di Exchange in Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md) o [Interfaccia di amministrazione di Exchange in Exchange Online](https://technet.microsoft.com/it-it/library/jj200743\(v=exchg.150\)).

  - Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)).Per informazioni su come usare Windows PowerShell per connettersi a Exchange Online, vedere [Connessione a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Componente aggiuntivo per Outlook" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Indicazione della disponibilità, abilitazione o disabilitazione di un componente aggiuntivo

## Utilizzo di EAC per specificare se un componente aggiuntivo è disponibile, abilitato o disabilitato

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Organizzazione** \> **Componenti aggiuntivi**.

2.  Nella visualizzazione elenco, selezionare il componente aggiuntivo di cui si desidera modificare le impostazioni, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Per impedire agli utenti di utilizzare il componente aggiuntivo, deselezionare la casella di controllo **Rendi il componente aggiuntivo disponibile agli utenti nell'organizzazione** e fare clic su **Salva**.

4.  Per consentire agli utenti di utilizzare il componente aggiuntivo, selezionare **Rendi il componente aggiuntivo disponibile agli utenti dell'organizzazione** e selezionare l'opzione desiderata.
    
      - **Facoltativa, abilitata per impostazione predefinita**: utilizzare questa impostazione per consentire agli utenti di disattivare il componente aggiuntivo.
    
      - **Facoltativa, disabilitata per impostazione predefinita**: utilizzare questa impostazione per consentire agli utenti di attivare il componente aggiuntivo.
    
      - **Obbligatoria, sempre abilitata. Gli utenti non possono disabilitare il componente aggiuntivo**: utilizzare questa impostazione se non si desidera che gli utenti disattivino il componente aggiuntivo.

5.  Fare clic su **Salva**.

## Utilizzo di Exchange PowerShell per specificare se un componente aggiuntivo è disponibile, abilitato o disabilitato

Innanzitutto, utilizzare il seguente comando per individuare i nomi visualizzati e gli ID di tutti i componenti aggiuntivi di Outlook installati per l'organizzazione.

    Get-App -OrganizationApp | Format-List DisplayName,AppId

Il valore **AppId** è un GUID che identifica il componente aggiuntivo (ad esempio, `fe93bfe1-7947-460a-a5e0-7a5906b51360`). Utilizzare il valore **AppId** per identificare e modificare le impostazioni del componente aggiuntivo.

Per disabilitare e nascondere un componente aggiuntivo da tutti gli utenti, sostituire *\<AppId\>* con il valore **AppId** effettivo ed eseguire il comando seguente:

    Set-App -Identity <AppId> -OrganizationApp -Enabled $false

Per abilitare un componente aggiuntivo per impostazione predefinita, e nello stesso tempo consentire agli utenti di disattivare l'opzione, sostituire *\<AppId\>* con il valore **AppId** effettivo ed eseguire il comando seguente:

    Set-App -Identity <AppId> -OrganizationApp -Enabled $true -DefaultStateForUser Enabled

Per disabilitare un componente aggiuntivo per impostazione predefinita, e nello stesso tempo consentire agli utenti di attivare l'opzione, sostituire *\<AppId\>* con il valore **AppId** effettivo ed eseguire il comando seguente:

    Set-App -Identity <AppId> -OrganizationApp -Enabled $true -DefaultStateForUser Disabled

Se si desidera che il componente aggiuntivo sia necessario per gli utenti, sostituire *\<AppId\>* con il valore **AppId** effettivo ed eseguire il comando seguente:

    Set-App -Identity <AppId> -OrganizationApp -Enabled $true -DefaultStateForUser AlwaysEnabled

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-App](https://technet.microsoft.com/it-it/library/jj218630\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente configurato un componente aggiuntivo, eseguire una delle seguenti procedure:

  - In EAC, passare a **Organizzazione** \> **Componenti aggiuntivi** ed esaminare i valori delle colonne **Utente predefinito** e **Fornito a**.

  - In PowerShell per Exchange Online, eseguire il comando seguente e verificare i valori delle proprietà **DefaultStateForUser** e **Enabled**:
    
        Get-App -OrganizationApp | Format-List DisplayName,AppId,Enabled,DefaultStateForUser

## Usare Exchange PowerShell per limitare la disponibilità di componenti aggiuntivi per utenti specifici

Per limitare la disponibilità di un componente aggiuntivo a utenti specifici, è possibile usare EAC. È possibile utilizzare soltanto Exchange Management Shell o PowerShell per Exchange Online.

Questo esempio limita il componente aggiuntivo LinkedIn con l'ipotetico **AppId** valore `ac83a9d5-5af2-446f-956a-c583adc94d5e` ai membri del gruppo di distribuzione denominato Marketing.

    $a = Get-DistributionGroupMember Marketing

    Set-App -Identity ac83a9d5-5af2-446f-956a-c583adc94d5e -OrganizationApp -ProvidedTo SpecificUsers -UserList $a.Identity -DefaultStateForUser Enabled

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-App](https://technet.microsoft.com/it-it/library/jj218630\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per verificare che è stata correttamente limitata disponibilità del componente aggiuntivo a utenti specifici, eseguire il comando seguente in Exchange PowerShell e verificare il valore delle proprietà **ProvidedTo** e **UserList**:

    Get-App -OrganizationApp | Format-List DisplayName,AppId,Enabled,DefaultStateForUser,ProvidedTo,UserList

