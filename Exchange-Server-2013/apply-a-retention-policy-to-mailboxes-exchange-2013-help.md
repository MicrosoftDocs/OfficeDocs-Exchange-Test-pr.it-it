---
title: 'Applicazione dei criteri di conservazione alle cassette postali: Exchange 2013 Help'
TOCTitle: Applicazione dei criteri di conservazione alle cassette postali
ms:assetid: 6ccc80db-d201-44f7-8d4b-473a89c14b2f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd298052(v=EXCHG.150)
ms:contentKeyID: 50480941
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Applicazione dei criteri di conservazione alle cassette postali

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-10-01_

È possibile utilizzare i criteri di conservazione per raggruppare uno o più tag di conservazione e applicarli alle cassette postali per imporre le impostazioni di conservazione dei messaggi. Una cassetta postale non può avere più di un criterio di conservazione.


> [!WARNING]
> La scadenza dei messaggi dipende dalle impostazioni definite nei tag di conservazione legati al criterio. Queste impostazioni comprendono azioni quali lo spostamento dei messaggi nell'archivio o la loro eliminazione definitiva. Prima di applicare un criterio di conservazione a una o più cassette postali, si consiglia di verificare il criterio e di esaminare ogni tag ad esso associato.



Per altre attività di gestione relative a Gestione record di messaggistica, vedere [Messaggistica Records Management Procedures](messaging-records-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Applicazione criteri di conservazione" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Utilizzo dell'interfaccia di amministrazione di Exchange per l'applicazione di un criterio di conservazione a una singola cassetta postale

1.  Accedere a **Destinatari** \> **Cassette postale**.

2.  Nell'elenco, selezionare la cassetta postale a cui applicare il criterio di conservazione, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Cassetta postale utente**, fare clic su **Funzionalità delle cassette postali**.

4.  Nell'elenco **Criterio di conservazione**, selezionare il criterio da applicare alla cassetta postale e fare clic su **Salva**.

## Utilizzo dell'interfaccia di amministrazione di Exchange per l'applicazione di un criterio di conservazione a più cassette postali

1.  Accedere a **Destinatari** \> **Cassette postale**.

2.  Nell'elenco, utilizzare il tasto Maiusc o Ctrl per selezionare più cassette postali.

3.  Nel riquadro dei dettagli, fare clic su **Altre opzioni**.

4.  In **Criterio di conservazione**, fare clic su **Aggiorna**.

5.  Nell'elenco **Assegna in blocco il criterio di conservazione**, selezionare il criterio di conservazione da applicare alle cassette postali e fare clic su **Salva**.

## Utilizzo di Shell per l'applicazione di un criterio di conservazione a una singola cassetta postale

In questo esempio viene applicato il criterio di conservazione RP-Finance alla cassetta postale di Cavaglieri.

    Set-Mailbox "Morris" -RetentionPolicy "RP-Finance"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Utilizzo di Shell per l'applicazione di un criterio di conservazione a più cassette postali

In questo esempio viene applicato il nuovo criterio di conservazione New-Retention-Policy a tutte le cassette postali che dispongono del precedente criterio Old-Retention-Policy.

    $OldPolicy={Get-RetentionPolicy "Old-Retention-Policy"}.distinguishedName
    Get-Mailbox -Filter {RetentionPolicy -eq $OldPolicy} -Resultsize Unlimited | Set-Mailbox -RetentionPolicy "New-Retention-Policy"

In questo esempio, il criterio di conservazione RetentionPolicy-Corp viene applicato a tutte le cassette postali nell'organizzazione Exchange.

    Get-Mailbox -ResultSize unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Corp"

In questo esempio, il criterio di conservazione RetentionPolicy-Finance viene applicato a tutte le cassette postali nell'unità organizzativa Finance.

    Get-Mailbox -OrganizationalUnit "Finance" -ResultSize Unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Finance"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) e [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver applicato il criterio di conservazione, eseguire il cmdlet [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) per recuperare il criterio di conservazione per la cassetta postale o le cassette postali.

In questo esempio viene recuperato il criterio di conservazione per la cassetta postale di Cavaglieri.

    Get-Mailbox Morris | Select RetentionPolicy

Questo comando consente di recuperare tutte le cassette postali a cui è stato applicato il criterio di conservazione RP-Finance.

    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionPolicy -eq "RP-Finance"} | Format-Table Name,RetentionPolicy -Auto

