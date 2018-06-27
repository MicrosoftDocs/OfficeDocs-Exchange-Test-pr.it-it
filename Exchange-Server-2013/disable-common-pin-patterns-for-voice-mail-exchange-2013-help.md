---
title: 'Disabilitare i formati comuni PIN per la segreteria telefonica: Exchange 2013 Help'
TOCTitle: Disabilitare i formati comuni PIN per la segreteria telefonica
ms:assetid: eecc40ae-fac7-41e4-a1e1-16330f4462a3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125160(v=EXCHG.150)
ms:contentKeyID: 50555707
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disabilitare i formati comuni PIN per la segreteria telefonica

 

_**Si applica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2013-02-22_

È possibile abilitare o disabilitare i modelli comuni di PIN della messaggistica unificata per gli utenti di Outlook Voice Access. Se si abilita o disabilita l'impostazione dei criteri comuni del PIN in un criterio cassetta postale di messaggistica unificata, tale impostazione verrà applicata a tutti gli utenti abilitati alla messaggistica unificata che sono associati al criterio cassetta postale di messaggistica unificata. Per impostazione predefinita, gli utenti abilitati alla messaggistica unificata non possono utilizzare i criteri comuni durante la creazione di un PIN.

È possibile configurare numerose diverse impostazioni relative al PIN su un criterio cassetta postale di messaggistica unificata. L'impostazione **Consenti modelli di PIN comuni** viene utilizzata per consentire o impedire agli utenti l'utilizzo di modelli di criteri numero comuni quando creano un PIN. Per impostazione predefinita, questa impostazione è disabilitata e impedisce quindi agli utenti di utilizzare i seguenti criteri numero:

  - **Numeri sequenziali**   Si tratta di valori del PIN che includono solo numeri consecutivi. ad esempio, 1234 e 65432.

  - **Numeri che si ripetono**   Si tratta di valori del PIN che includono solo numeri che si ripetono. ad esempio 11111 e 22222.

  - **Suffisso dell'estensione della cassetta postale**   Si tratta di valori del PIN che includono il suffisso dell'estensione della cassetta postale di un utente. Ad esempio, se l'estensione della cassetta postale dell'utente è 36697, il PIN dell'utente non potrà essere 3669712.


> [!NOTE]
> Se l'impostazione <STRONG>Consenti modelli di PIN comuni</STRONG> è abilitata, verrà rifiutato solo il suffisso dell'estensione della cassetta postale.



Per ulteriori attività relative alla protezione del PIN di Outlook Voice Access, vedere [Procedure di protezione PIN](pin-security-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: Meno di 1 minuto.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Disabilitazione dei modelli di PIN comuni tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**. Nella visualizzazione elenco, selezionare il dial plan di messaggistica unificata che si desidera modificare e sulla barra degli strumenti fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

2.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera gestire, quindi sulla barra degli strumenti fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Dalla pagina **Criteri cassetta postale di messaggistica unificata**, sotto **Criteri PIN**, deselezionare la casella di controllo accanto a **Consenti modelli di PIN comuni**.

4.  Fare clic su **Salva**.

## Disabilitazione dei modelli di PIN comuni tramite Shell

Con questo esempio agli utenti associati al criterio cassetta postale di messaggistica unificata `MyUMMailboxPolicy` viene impedito l'uso di PIN contenenti criteri comuni.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowCommonPatterns $false

