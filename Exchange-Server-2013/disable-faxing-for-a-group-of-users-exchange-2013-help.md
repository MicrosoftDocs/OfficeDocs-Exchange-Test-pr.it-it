---
title: 'Disabilitare la funzionalità fax per un gruppo di utenti: Exchange 2013 Help'
TOCTitle: Disabilitare la funzionalità fax per un gruppo di utenti
ms:assetid: 1c57c3ba-2b0e-43dd-9b28-43bada1592c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ650864(v=EXCHG.150)
ms:contentKeyID: 52057217
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare la funzionalità fax per un gruppo di utenti

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile disabilitare i fax in entrata per gli utenti associati a un criterio cassetta postale di messaggistica unificata. Per impostazione predefinita, quando si abilitano utenti alla messaggistica unificata, gli utenti non possono ricevere fax finché non viene specificato l'URI del server partner fax, distribuito il server partner fax per l'organizzazione e abilitato il fax su un criterio cassetta postale di messaggistica unificata. Se questa opzione viene disabilitata sul dial plan di messaggistica unificata, non sarà possibile la ricezione dei fax da parte degli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata. Allo stesso modo, se l'opzione per consentire a un singolo utente di ricevere i fax in entrata viene disabilitata, tale utente non potrà ricevere fax.

Per ulteriori informazioni sui partner fax, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Per altre attività di gestione relative ai fax, vedere [Fax procedure](faxing-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Disabilitazione dei fax in entrata tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio della cassetta postale di messaggistica unificata**, \> **Generale**, deselezionare la casella di controllo accanto a **Consenti fax in ingresso**.

4.  Fare clic su **Salva** per salvare le modifiche.

## Disabilitazione dei fax in entrata tramite Shell

Con questo esempio si impedisce agli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy` di utilizzare i fax in ingresso.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $false

