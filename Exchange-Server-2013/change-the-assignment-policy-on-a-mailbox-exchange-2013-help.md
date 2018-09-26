---
title: 'Modifica criterio assegnaz. cassetta postale: Exchange 2013 Help'
TOCTitle: Modificare il criterio di assegnazione di una cassetta postale
ms:assetid: 011690a5-233a-4c03-8842-92276f899a89
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638076(v=EXCHG.150)
ms:contentKeyID: 50479900
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modificare il criterio di assegnazione di una cassetta postale

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-08_

È possibile modificare il criterio di assegnazione del ruolo di gestione assegnato a una cassetta postale. Quando si modifica un criterio di assegnazione della cassetta postale, la modifica viene applicata non appena l'utente aggiorna la connessione, ad esempio, al successivo accesso alla cassetta postale oppure quando apre la pagina relativa alle opzioni della cassetta postale. Per ulteriori informazioni sui criteri di assegnazione in Microsoft Exchange Server 2013, vedere [Informazioni sui criteri di assegnazione di ruolo di gestione](understanding-management-role-assignment-policies-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle autorizzazioni, vedere [Autorizzazioni](permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gruppi di ruoli" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Utilizzo dell'interfaccia di amministrazione di Exchange per la modifica del criterio di assegnazione in una cassetta postale

1.  Nell'interfaccia di amministrazione di Exchange, accedere a **Destinatari** \> **Cassette postali**.

2.  Selezionare la cassetta postale dell'utente o della risorsa per la quale modificare il criterio di assegnazione e fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  Selezionare **Funzionalità della cassetta postale**.

4.  Nell'elenco **Criterio di assegnazione dei ruoli**, selezionare il criterio di assegnazione da assegnare alla cassetta postale e fare clic su **Salva**.

## Modifica del criterio di assegnazione per una cassetta postale tramite Shell

Per modificare il criterio di assegnazione associato a una cassetta postale, utilizzare la seguente sintassi.

```powershell
Set-Mailbox <mailbox alias or name> -RoleAssignmentPolicy <assignment policy>
```

In questo esempio viene impostato il criterio di assegnazione Unified Messaging Users per la cassetta postale Brian.

```powershell
Set-Mailbox Brian -RoleAssignmentPolicy "Unified Messaging Users"
```

## Modifica del criterio di assegnazione per un gruppo di cassette postali assegnate a uno specifico criterio tramite Shell


> [!NOTE]
> Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per modificare contemporaneamente il criterio di assegnazione su tutte le cassette postali di un gruppo.



In questa procedura viene eseguito il pipelining, il cmdlet **Where** e il parametro *WhatIf*. Per ulteriori informazioni su questi concetti, vedere i seguenti argomenti:

  - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))

  - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

  - [Opzioni WhatIf, Confirm e ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

Se si desidera modificare il criterio di assegnazione per un gruppo di cassette postali assegnate a uno specifico criterio, utilizzare la seguente sintassi.
```powershell
    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<assignment policy to find>" } | Set-Mailbox -RoleAssignmentPolicy <assignment policy to set>
```
In questo esempio vengono individuate tutte le cassette postali assegnate al criterio di assegnazione Redmond Users - No Voicemail e il criterio viene modificato in Redmond Users - Voicemail Enabled.
```powershell
    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled"
```

In questo esempio viene incluso il parametro *WhatIf* in modo da poter visualizzare tutte le cassette postali modificate senza apportare alcuna modifica.
```powershell
    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled" -WhatIf
```
Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)) o [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

