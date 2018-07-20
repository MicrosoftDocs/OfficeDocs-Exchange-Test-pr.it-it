---
title: 'Impostare la lunghezza minima del PIN per la segreteria telefonica: Exchange 2013 Help'
TOCTitle: Impostare la lunghezza minima del PIN per la segreteria telefonica
ms:assetid: b2ecab54-42e6-45af-8322-615cc1f68dd9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124271(v=EXCHG.150)
ms:contentKeyID: 50555666
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impostare la lunghezza minima del PIN per la segreteria telefonica

 

_**Si applica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:** 2013-02-22_

È possibile configurare la lunghezza minima del PIN per gli utenti di Outlook Voice Access abilitati alla messaggistica unificata. Le impostazioni del PIN configurate su un criterio cassetta postale di messaggistica unificata vengono applicate a tutti gli utenti associati a tale criterio.

Outlook Voice Access è utilizzato dagli utenti abilitati alla messaggistica unificata per accedere alle proprie caselle vocali, alla posta elettronica, al calendario e alle informazioni personali sui contatti che si trovano nella propria cassetta postale. Tuttavia, per poter accedere alla propria cassetta postale, devono immettere un PIN per l'autenticazione dal sistema di caselle vocali.


> [!NOTE]
> Se si apporta una modifica al valore della lunghezza minima del PIN, agli utenti esistenti di Outlook Voice Access verrà richiesto di immettere un nuovo PIN contenente il nuovo numero minimo di cifre. Il valore predefinito è 6.



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

## Configurazione della lunghezza minima del PIN per Outlook Voice Access tramite EAC

1.  Nell'interfaccia di amministrazione di Exchange, navigare a **Messaggistica unificata** \> **Dial plan di messaggistica unificata**.

2.  Nella visualizzazione elenco, selezionare il dial plan che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Nella pagina **Dial plan di messaggistica unificata**, sotto **Criteri cassetta postale di messaggistica unificata**, selezionare il criterio cassetta postale di messaggistica unificata che si desidera modificare, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

4.  Fare clic su **Criteri PIN** e, accanto a **Lunghezza minima PIN**, immettere un valore compreso tra 4 e 24.

5.  Fare clic su **Salva**.

## Configurazione della lunghezza minima del PIN per Outlook Voice Access tramite Shell

Con questo esempio la lunghezza minima del PIN per gli utenti di Outlook Voice Access associati al criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy` viene impostata su 8 cifre.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MinPINLength 8

Con questo esempio la lunghezza minima del PIN viene impostata su 8 cifre, mentre il numero di tentativi di accesso non riusciti prima della reimpostazione del PIN dell'utente viene impostato su 3. Si applica agli utenti abilitati alla messaggistica unificata associati al criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MinPINLength 8

