---
title: 'Creazione di un gruppo di risposta di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Creazione di un gruppo di risposta di messaggistica unificata
ms:assetid: 43ecb1ec-5f82-4516-9010-de8f954d3758
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa997679(v=EXCHG.150)
ms:contentKeyID: 50555577
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMHuntGroupWizardForm.CreateUMHuntGroupWizardPage1
ms.translationtype: MT
---

# Creazione di un gruppo di risposta di messaggistica unificata

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-04-16_

Un gruppo di risposta di messaggistica unificata è una rappresentazione logica di un gruppo di risposta PBX o IP PBX. Un gruppo di risposta di messaggistica unificata può essere utilizzato come una connessione o collegamento tra un dial plan e un gateway IP di messaggistica unificata.


> [!NOTE]
> Se si associa un dial plan di messaggistica unificata con il gateway IP di messaggistica unificata durante la creazione di un gateway di messaggistica unificata, verrà creato anche un gruppo di risposta di messaggistica unificata.




> [!NOTE]
> Per modificare le impostazioni del gruppo di risposta di messaggistica unificata, è necessario eliminare il gruppo di risposta e crearne un altro con le impostazioni corrette.



Per altre attività di gestione relative ai gruppi di risposta di messaggistica unificata, vedere [Procedure gruppo di risposta di messaggistica unificata](um-hunt-group-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di risposta di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - È indispensabile confermare la creazione di un gateway IP di messaggistica unificata prima di eseguire queste procedure. Per la procedura dettagliata, vedere [Creare un gateway IP di messaggistica unificata](create-a-um-ip-gateway-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Creazione di un gruppo di risposta di messaggistica unificata tramite EMC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Gruppi di risposta di messaggistica unificata**, fare clic su **Nuovo**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

3.  Nella pagina **Nuovo gateway IP di messaggistica unificata**, immettere le informazioni seguenti:
    
      - **Nome**   Utilizzare questa casella per creare il nome visualizzato per il gruppo di risposta di messaggistica unificata. Il nome di un gruppo di risposta di messaggistica unificata è obbligatorio e deve essere univoco, ma viene utilizzato solo per la visualizzazione in EAC e Shell. Se si desidera modificare il nome visualizzato del gruppo di risposta dopo la creazione, è necessario eliminare il gruppo di risposta esistente e crearne uno con il nome desiderato.
        
        Se l'organizzazione utilizza più gruppi di risposta, si consiglia di utilizzare nomi significativi per i gruppi di risposta. La lunghezza massima per il nome di un gruppo di risposta di messaggistica unificata è di 64 caratteri e può contenere spazi. Tuttavia, non può contenere i seguenti caratteri: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Gateway IP di messaggistica unificata**   Utilizzare questa casella per specificare il gateway IP di messaggistica unificata. Fare clic su **Sfoglia** per selezionare il gateway IP di messaggistica unificata e scegliere **OK**.
    
      - **Identificatore pilota**   Utilizzare questa casella di testo per specificare una stringa che identifichi l'identificatore pilota configurato per il sistema PBX o IP PBX.
        
        Questa casella può essere compilata con un numero di interno o con un URI (Uniform Resource Identifier) SIP (Session Initiated Protocol). La casella accetta caratteri alfanumerici. Per PBX legacy, si utilizza un valore numerico come identificatore pilota. Tuttavia, alcuni IP PBX possono utilizzare URI SIP.

4.  
    
    Fare clic su **Salva**.

## Creazione di un gruppo di risposta di messaggistica unificata tramite Shell

In questo esempio, viene creato un gruppo di risposta di messaggistica unificata denominato `MyUMHuntGroup` con un identificatore pilota 12345.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 12345 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

In questo esempio, viene creato un gruppo di risposta di messaggistica unificata denominato `MyUMHuntGroup` con più identificatori pilota.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialplan MyUMDialPlan -UMIPGateway MyUMIPGateway

