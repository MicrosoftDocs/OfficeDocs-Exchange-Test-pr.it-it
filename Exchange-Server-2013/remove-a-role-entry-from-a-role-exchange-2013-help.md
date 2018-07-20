---
title: 'Rimuovere una voce di ruolo da un ruolo: Exchange 2013 Help'
TOCTitle: Rimuovere una voce di ruolo da un ruolo
ms:assetid: 4736367a-750f-44d3-8a20-5149bd35e9ff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd297947(v=EXCHG.150)
ms:contentKeyID: 50480573
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimuovere una voce di ruolo da un ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Le voci di un ruolo di gestione determinano quali cmdlet e parametri sono disponibili in un ruolo di gestione. Eliminando le voci di ruolo o i parametri di una voce di ruolo è possibile limitare le operazioni che gli utenti assegnati al ruolo di gestione possono eseguire. Per ulteriori informazioni sulle voci del ruolo di gestione in Microsoft Exchange Server 2013, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Eliminazione di una singola voce di ruolo da un ruolo

Quando si elimina una voce di ruolo da un ruolo, gli utenti assegnati a quel ruolo non sono più in grado di accedere al cmdlet o allo script associato.

Utilizzare la seguente sintassi per rimuovere un'intera voce del ruolo di gestione da un ruolo.

    Remove-ManagementRoleEntry <management role>\<management role entry>

Con questo esempio viene rimosso il cmdlet **Enable-MailUser** dal ruolo Seattle Server Administrators.

    Remove-ManagementRoleEntry "Seattle Server Administrators\Enable-MailUser"

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Remove-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351187\(v=exchg.150\)).

## Eliminazione di più voci di ruolo da un ruolo

Quando si eliminao più voci di ruolo da un ruolo, gli utenti assegnati a quel ruolo non sono più in grado di accedere ai cmdlet o agli script associati.

Per eliminare più voci di ruolo da un ruolo è necessario recuperare l'elenco delle voci di ruolo da rimuovere utilizzando il cmdlet **Get-ManagementRoleEntry**. Successivamente, è necessario inviare l'output al cmdlet **Remove-ManagementRoleEntry**. È possibile utilizzare i caratteri jolly insieme al cmdlet **Get-ManagementRoleEntry** per trovare più voci di ruolo. È buona norma utilizzare l'opzione *WhatIf* per verificare che le voci di ruolo in fase di eliminazione siano quelle corrette. Utilizzare la seguente sintassi.

    Get-ManagementRoleEntry <management role>\<role entry with wildcard character> | Remove-ManagementRoleEntry -WhatIf

Con questo esempio vengono eliminate tutte le voci di ruolo contenenti la parola journal dal ruolo Seattle Server Administrators.

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry -WhatIf

Quando si esegue il comando con l'opzione *WhatIf*, il cmdlet restituisce un elenco di tutte le voci di ruolo da eliminare. Se l'elenco è corretto, eseguire di nuovo il comando senza l'opzione *WhatIf* per eliminare le voci di ruolo.

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd335210\(v=exchg.150\)) e [Remove-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351187\(v=exchg.150\)).

## Eliminazione dei parametri da una voce di ruolo in un ruolo

Se si eliminano i parametri da una voce di ruolo in un ruolo, i parametri non sono più a disposizione degli utenti assegnati al ruolo.

Utilizzare la seguente sintassi per eliminare i parametri da una voce di ruolo.

    Set-ManagementRoleEntry <management role>\<role entry> -Parameters <parameter 1>,<parameter 2...> -RemoveParameter

Con questo esempio vengono eliminati i parametri *MaxSafeSenders*, *MaxSendSize*, *SecondaryAddress* e *UseDatabaseQuotaDefaults* dalla voce di ruolo **Set-Mailbox** nel ruolo Seattle Server Administrators.

    Set-ManagementRoleEntry "Seattle Server Administrators\Set-Mailbox" -Parameters MaxSafeSenders,MaxSendSize,SecondaryAddress,UseDatabaseQuotaDefaults -RemoveParameter

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Set-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd351162\(v=exchg.150\)).

