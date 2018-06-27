---
title: 'Abilitare i formati comuni PIN per la segreteria telefonica: Exchange 2013 Help'
TOCTitle: Abilitare i formati comuni PIN per la segreteria telefonica
ms:assetid: 9940a8c2-f576-4089-ab96-8b318ad3da0f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ673546(v=EXCHG.150)
ms:contentKeyID: 50555639
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare i formati comuni PIN per la segreteria telefonica

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

È possibile abilitare o disabilitare i criteri PIN comuni della messaggistica unificata per gli utenti di Outlook Voice Access. Se si abilita o disabilita l'impostazione dei criteri comuni del PIN in un criterio cassetta postale di messaggistica unificata, tale impostazione verrà applicata a tutti gli utenti abilitati alla messaggistica unificata che sono associati al criterio cassetta postale di messaggistica unificata. Per impostazione predefinita, gli utenti abilitati alla messaggistica unificata non possono utilizzare i criteri comuni durante la creazione di un PIN.

È possibile configurare numerose diverse impostazioni relative al PIN su un criterio cassetta postale di messaggistica unificata. L'impostazione **Consenti modelli di PIN comuni** viene utilizzata per consentire o impedire l'utilizzo dei modelli di numero comuni nella creazione di un PIN. Per impostazione predefinita, questa impostazione è disabilitata e impedisce quindi agli utenti di utilizzare i seguenti criteri numero:

  - **Numeri sequenziali**   Si tratta di valori del PIN che includono solo numeri consecutivi. ad esempio, 1234 e 65432.

  - **Numeri che si ripetono**   Si tratta di valori del PIN che includono solo numeri che si ripetono. ad esempio 11111 e 22222.

  - **Suffisso dell'estensione della cassetta postale**   Si tratta di valori del PIN che includono il suffisso dell'estensione della cassetta postale di un utente. Ad esempio, se l'estensione della cassetta postale dell'utente è 36697, il PIN dell'utente non potrà essere 3669712.


> [!NOTE]
> Se l'impostazione <STRONG>Consenti modelli di PIN comuni</STRONG> è abilitata, verrà rifiutato solo il suffisso dell'estensione della cassetta postale.



Per altre attività relative alla protezione tramite PIN di Outlook Voice Access, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Per saperne di più

## Abilitazione dei modelli di PIN comuni tramite l'interfaccia di amministrazione di Exchange

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare e sulla barra degli strumenti fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, in **Criteri cassette postali di messaggistica unificata** selezionare il criterio cassetta postale di messaggistica unificata da gestire, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Criteri cassetta postale di messaggistica unificata**, in **Criteri PIN** selezionare la casella di controllo accanto a **Consenti modelli di PIN comuni**.

4.  Fare clic su **Salva**.

## Abilitazione dei modelli di PIN comuni tramite Shell

In questo esempio gli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy` vengono abilitati all'uso di PIN contenenti modelli comuni.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowCommonPatterns $true

