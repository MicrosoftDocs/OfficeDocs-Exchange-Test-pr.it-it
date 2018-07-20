---
title: 'Creazione di un criterio cassetta postale di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Creazione di un criterio cassetta postale di messaggistica unificata
ms:assetid: 7f20874b-c46c-4505-9a78-f63eacb578ff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123510(v=EXCHG.150)
ms:contentKeyID: 50555627
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMMailboxPolicyWizardForm.CreateUMMailboxPolicyWizardPage
ms.translationtype: MT
---

# Creazione di un criterio cassetta postale di messaggistica unificata

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-03-08_

È possibile creare un criterio cassetta postale di messaggistica unificata per applicare una serie comune di impostazioni di messaggistica unificata, come le impostazioni dei criteri del PIN o le restrizioni di composizione, a un gruppo di cassette postali abilitate per la messaggistica unificata. I criteri cassetta postale di messaggistica unificata collegano un utente abilitato alla messaggistica unificata a un dial plan di messaggistica unificata e applicano un insieme di criteri o di impostazioni di protezione comune a un gruppo di cassette postali abilitate alla messaggistica unificata. I criteri cassetta postale di messaggistica unificata sono utili per l'applicazione e la standardizzazione delle impostazioni di configurazione della messaggistica unificata per utenti abilitati alla messaggistica unificata.

Per impostazione predefinita, quando si crea un dial plan di messaggistica unificata, viene creato anche un criterio cassetta postale di messaggistica unificata. Dopo aver distribuito la messaggistica unificata nell'organizzazione, potrebbe essere necessario creare e configurare dei criteri di messaggistica unificata aggiuntivi o modificare quelli già esistenti.

Per le attività di gestione aggiuntive relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Creazione di un criterio cassetta postale di messaggistica unificata tramite l'interfaccia di amministrazione di Exchange

1.  
    
    Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassetta postale messaggistica unificata** fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Nuovo criterio cassetta postale di messaggistica unificata**, nella casella **Nome** immettere il nome del nuovo criterio cassetta postale di messaggistica unificata.
    
    Questa casella consente di specificare un nome univoco per il criterio cassetta postale di messaggistica unificata. Si tratta del nome che verrà visualizzato in EAC. Qualora fosse necessario modificare il nome visualizzato del criterio cassetta postale di messaggistica unificata dopo la relativa creazione, occorre in primo luogo eliminare il criterio cassetta postale di messaggistica unificata esistente e, quindi, crearne un altro con il nome corretto. Non è possibile eliminare un criterio cassetta postale di messaggistica unificata se ad esso sono associati utenti abilitati alla messaggistica unificata.
    
    Il nome del criterio cassetta postale di messaggistica unificata è obbligatorio, ma viene utilizzato solo per la visualizzazione. Dal momento che l'organizzazione può utilizzare più criteri cassetta postale di messaggistica unificata, si consiglia di utilizzare nomi significativi per ognuno di essi. La lunghezza massima per il nome di un criterio cassetta postale di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.

4.  Fare clic su **Salva** per salvare il nuovo criterio cassetta postale di messaggistica unificata. Quando viene salvato il criterio cassetta postale di messaggistica unificata, vengono abilitate tutte le impostazioni predefinite inclusi i criteri PIN, le funzionalità della posta vocale e le impostazioni del sistema di caselle vocali protette. Per personalizzare o modificare le impostazioni predefinite, utilizzare il cmdlet **Set-UMMailbox** che consente di modificare le impostazioni del criterio cassetta postale di messaggistica unificata appena creato.

## Creazione di un criterio cassetta postale di messaggistica unificata tramite Shell

In questo esempio, viene creato un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy` associato al dial plan di messaggistica unificata denominato `MyUMDialPlan`.

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

