---
title: 'Assegnare un criterio cassetta postale di messaggistica unificata: Exchange 2013 Help'
TOCTitle: Assegnare un criterio cassetta postale di messaggistica unificata
ms:assetid: c8da6cbe-3d22-4fff-8b5a-416b1c8adb6c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb201728(v=EXCHG.150)
ms:contentKeyID: 50481653
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Assegnare un criterio cassetta postale di messaggistica unificata

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2012-11-30_

Quando si abilita un utente alla messaggistica unificata e alla posta vocale, è necessario selezionare il criterio cassetta postale di messaggistica unificata che verrà associato alla cassetta postale dell'utente. È possibile modificare tale criterio dopo che l'utente è stato abilitato alla messaggistica unificata.

I criteri cassetta postale di messaggistica unificata vengono creati per applicare un insieme comune di criteri o impostazioni di protezione a un insieme di cassette postali di utenti abilitati alla messaggistica unificata. È possibile utilizzare tali criteri per applicare impostazioni quali:

  - Criteri PIN

  - Restrizioni di composizione

  - Altre proprietà generali dei criteri cassetta postale di messaggistica unificata


> [!NOTE]
> Ogni volta che si crea un dial plan di messaggistica unificata, viene creato un criterio cassetta postale di messaggistica unificata predefinito. È possibile eliminare i criteri cassetta postale di messaggistica unificata predefiniti oppure creare criteri aggiuntivi in base alle esigenze della propria organizzazione.



Per altre attività di gestione relative agli utenti abilitati alla posta vocale, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che l'utente sia abilitato alla messaggistica unificata. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Modifica del criterio cassetta postale di messaggistica unificata assegnato a un utente abilitato alla messaggistica unificata tramite EAC

1.  In Interfaccia di amministrazione di Exchange accedere a **Destinatari** \> **Cassette postali**.

2.  Nella visualizzazione Elenco selezionare la cassetta postale per la quale si desidera modificare il criterio cassetta postale di messaggistica unificata.

3.  Nel riquadro dei dettagli, sotto **Funzionalità telefoniche e vocali** \> **Messaggistica unificata** fare clic su **Visualizza dettagli**.

4.  Nella pagina **Cassetta postale di messaggistica unificata** fare clic su **Impostazioni della cassetta postale di messaggistica unificata**, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

5.  Nella pagina **Cassetta postale di messaggistica unificata** accanto \> a **Criterio cassetta postale di messaggistica unificata** fare clic su **Sfoglia** per individuare il criterio cassetta postale di messaggistica unificata dell'utente.

6.  Fare clic su **Salva**.

## Modifica del criterio cassetta postale di messaggistica unificata assegnato a un utente abilitato alla messaggistica unificata tramite Shell

Con questo esempio un utente abilitato alla messaggistica unificata denominato Tony Smith viene associato a un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Set-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy

