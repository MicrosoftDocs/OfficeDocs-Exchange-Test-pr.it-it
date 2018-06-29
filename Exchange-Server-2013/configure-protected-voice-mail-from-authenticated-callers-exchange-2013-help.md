---
title: 'Configurare la posta vocale protetta da chiamanti autenticati: Exchange 2013 Help'
TOCTitle: Configurare la posta vocale protetta da chiamanti autenticati
ms:assetid: f69e94a7-9768-4445-9ded-e78d732bd623
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423560(v=EXCHG.150)
ms:contentKeyID: 52057353
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare la posta vocale protetta da chiamanti autenticati

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

È possibile configurare la messaggistica unificata per rispondere a una chiamata in ingresso e determinare quindi se applicherà la protezione ai messaggi vocali tramite la crittografia. Quando un messaggio vocale è protetto:

  - Il messaggio viene contrassegnato come Privato in Microsoft Outlook e Outlook Web App.

  - Il messaggio vocale può essere aperto solo dal destinatario del messaggio stesso.

  - Il destinatario può rispondere al messaggio vocale ma non può inoltrarlo a utenti non inclusi nel messaggio vocale originale.

Questa impostazione si applica ai messaggi vocali inviati agli utenti abilitati alla messaggistica unificata quando non rispondono al telefono. L'impostazione si applica anche quando i chiamanti accedono alla loro cassetta postale utilizzando Outlook Voice Access e successivamente creano e inviano un messaggio vocale.

Per ulteriori attività di gestione relative alla procedure del Sistema di caselle postali protette, vedere [Procedure della casella vocale protette](protected-voice-mail-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Utilizzo di EAC per configurare la protezione dei messaggi vocali provenienti da chiamanti autenticati

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata** \> **Sistema di caselle vocali protette**, sotto **Proteggi messaggio vocale da chiamati autenticati**, selezionare una delle seguenti opzioni:
    
      - **Nessuno**   Utilizzare questa impostazione se non si desidera applicare alcuna protezione ad alcun messaggio vocale inviato agli utenti abilitati alla messaggistica unificata.
    
      - **Privato**   Utilizzare questa impostazione quando si desidera che la messaggistica unificata applichi la protezione solo ai messaggi vocali contrassegnati come privati dal chiamante.
    
      - **Tutti**   Utilizzare questa impostazione se si desidera che la messaggistica unificata applichi la protezione a tutti i messaggi vocali, compresi quelli non contrassegnati come privati.

4.  Fare clic su **Salva**.

## Utilizzo di Shell per configurare la protezione dei messaggi vocali derivanti da chiamanti autenticati

Con questo esempio vengono protetti i messaggi vocali dai chiamanti autenticati nel criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy ProtectAuthenticatedVoiceMail -All

