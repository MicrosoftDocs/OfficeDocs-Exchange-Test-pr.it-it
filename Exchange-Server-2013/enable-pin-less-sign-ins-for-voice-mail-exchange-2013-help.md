---
title: 'Abilitare gli accessi meno PIN per la segreteria telefonica: Exchange 2013 Help'
TOCTitle: Abilitare gli accessi meno PIN per la segreteria telefonica
ms:assetid: 54133753-317c-42ef-9b0d-ca9f2d2d6bd7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg602127(v=EXCHG.150)
ms:contentKeyID: 54652867
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare gli accessi meno PIN per la segreteria telefonica

 

_**Si applica a:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Ultima modifica dell'argomento:**2015-04-08_

È possibile impostare la Messaggistica unificata in modo che gli utenti possano accedere alla propria casella vocale senza l'utilizzo di un PIN. Per impostazione predefinita, agli utenti di Outlook Voice Access viene richiesto di immettere un PIN per accedere alla propria cassetta postale e di accedere alla posta vocale, alla posta elettronica, al calendario, ai contatti personali, alla directory e alle opzioni personali.


> [!WARNING]
> L'abilitazione degli accessi senza PIN per utenti singoli o gruppi di utenti abilitati alla posta vocale, comporta dei rischi per la sicurezza dell'organizzazione.



Per abilitare gli accessi senza PIN, è necessario impostare il parametro *AllowPinlessVoiceMailAccess* su `$true` nel criterio cassetta postale di messaggistica unificata e impostare il parametro *PinlessAccessToVoiceMailEnabled* su `$true` nella cassetta postale di messaggistica unificata. Per impostazione predefinita, entrambi i parametri sono impostati su `$false` e ciò fa sì che gli utenti di Outlook Voice Access debbano immettere il PIN per accedere alla loro casella vocale.

L'impostazione di entrambi i parametri su `$true` consente di abilitare gli accessi senza PIN alla posta vocale per un ampio gruppo di utenti associati ad una cassetta postale di messaggistica unificata e inoltre consente gli accessi senza PIN per una singola cassetta postale di messaggistica unificata o per un gruppo di cassette postali di messaggistica unificata. Anche se si abilitano gli accessi senza PIN per un gruppo di utenti abilitati alla messaggistica unificata o per un singolo utente abilitato alla messaggistica unificata, quando si accede alla posta elettronica, al calendario, ai contatti personali, alla directory o alle opzioni personali, verrà richiesto di immettere un PIN.

Per consentire gli accessi senza PIN alla posta vocale per un utente, è necessario che siano soddisfatte le seguenti condizioni:

  - È necessario aver eseguito il cmdlet seguente sul criterio cassetta postale di messaggistica unificata: `Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true`

  - È necessario aver eseguito il cmdlet seguente sulla cassetta postale dell'utente abilitato alla messaggistica unificata: `Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true`

  - L'utente abilitato alla messaggistica unificata è associato con lo stesso criterio cassetta postale di messaggistica unificata per il quale sono abilitati gli accessi senza PIN.

  - L'utente abilitato alla messaggistica unificata chiama Outlook Voice Access da un numero telefonico che è stato loro assegnato.

  - È possibile utilizzare solo Shell per eseguire questa procedura. Per sapere come aprire Exchange Management Shell nell'organizzazione Exchange locale, vedere [Aprire Shell.](https://technet.microsoft.com/it-it/library/dd638134\(v=exchg.150\)). Per informazioni su come usare Windows PowerShell per connettersi a Exchange Online, vedere [Connessione a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

Per altre attività relative ai criteri cassetta postale di messaggistica unificata, vedere [Procedure relative al criterio cassetta postale messaggistica unificata](um-mailbox-policy-procedures-exchange-2013-help.md).

Per ulteriori attività relative alle cassette postali di messaggistica unificata, vedere [Procedure utente abilitato alla posta vocale](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 3 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Criteri cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali di messaggistica unificata" nell'argomento [Autorizzazioni della messaggistica unificate](unified-messaging-permissions-exchange-2013-help.md).

  - È necessario confermare la creazione del dial plan di messaggistica unificata prima di eseguire le procedure. Per la procedura dettagliata, vedere [Creazione di un dial plan di messaggistica unificata](create-a-um-dial-plan-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che sia stato creato un criterio di cassetta postale di messaggistica unificata. Per la procedura dettagliata, vedere [Creazione di un criterio cassetta postale di messaggistica unificata](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Prima di eseguire queste procedure, verificare che l'utente o gli utenti siano abilitati alla messaggistica unificata e alla posta vocale. Per la procedura dettagliata, vedere [Consentire a un utente per la segreteria telefonica](enable-a-user-for-voice-mail-exchange-2013-help.md).

## Operazione desiderata

## Abilitazione dell'accesso senza PIN alla posta vocale per gli utenti abilitati alla messaggistica unificata su un criterio cassetta postale di messaggistica unificata tramite Shell

In questo esempio viene consentito l'accesso alla posta vocale senza PIN su un criterio cassetta postale di messaggistica unificata denominato `MyUMMailboxPolicy` per gli utenti associati al criterio cassetta postale che utilizzano Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true

## Abilitazione dell'accesso senza PIN alla posta vocale sulla cassetta postale dell'utente abilitato alla messaggistica unificata tramite Shell

In questo esempio viene consentito l'accesso alla posta vocale senza PIN per gli utenti che utilizzano Outlook per raggiungere la cassetta postale denominata `tonys@contoso.com`.

    Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true

