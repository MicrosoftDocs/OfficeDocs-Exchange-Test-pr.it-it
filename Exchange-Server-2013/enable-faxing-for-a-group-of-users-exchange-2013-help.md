---
title: 'Abilita fax per un gruppo di utenti: Exchange 2013 Help'
TOCTitle: Abilita fax per un gruppo di utenti
ms:assetid: b8d9f54d-ff06-4942-83e1-fc6c4ad02178
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423556(v=EXCHG.150)
ms:contentKeyID: 52057335
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilita fax per un gruppo di utenti

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2016-12-09_

È possibile abilitare i fax in ingresso per gli utenti collegati a un criterio cassetta postale di messaggistica unificata. Per impostazione predefinita, quando gli utenti vengono abilitati per la messaggistica unificata, non possono ricevere messaggi fax se prima non si specifica l'URI per il server partner fax, si distribuisce un server partner fax per l'organizzazione e si abilita la funzione fax in un criterio cassetta postale di messaggistica unificata. Se l'opzione per consentire i fax in ingresso è disabilitata nel dial plan di messaggistica unificata, gli utenti collegati al criterio cassetta postale di messaggistica unificata non potranno ricevere fax. Analogamente, se l'opzione per consentire i fax in ingresso è disabilitata per un singolo utente, tale utente non potrà ricevere fax.

Per ulteriori informazioni sui partner fax, vedere [Individuare Microsoft per i partner Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Per ulteriori attività di gestione relative all'invio e ricezione di fax, vedere [Fax procedure](faxing-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassetta postale di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Abilitazione dei fax in ingresso tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criterio cassetta postale di messaggistica unificata** \> **Generale**, selezionare la casella di controllo accanto a **Consenti fax in ingresso**.

4.  Fare clic su **Salva** per salvare le modifiche.

## Abilitazione dei fax in ingresso tramite Shell

In questo esempio agli utenti collegati al criterio cassetta posta di messaggistica unificata `MyUMMailboxPolicy` viene consentito l'uso dei fax in ingresso.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowFax $true

