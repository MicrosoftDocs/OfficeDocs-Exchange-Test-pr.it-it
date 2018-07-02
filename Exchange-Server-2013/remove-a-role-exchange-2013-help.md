---
title: 'Rimozione di un ruolo: Exchange 2013 Help'
TOCTitle: Rimozione di un ruolo
ms:assetid: 2fb6f453-f37a-4636-8353-3f9927f81298
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335178(v=EXCHG.150)
ms:contentKeyID: 50480261
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Rimozione di un ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

È possibile rimuovere dall'organizzazione i ruoli di gestione che non sono più necessari. Ma potranno essere rimossi solo quelli creati. I ruoli di gestione incorporati, infatti, non possono essere rimossi. Per ulteriori informazioni sui ruoli di gestione in Microsoft Exchange Server 2013, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Prima di rimuovere un ruolo di gestione, è necessario rimuovere tutte le assegnazioni ad esso associate. Per ulteriori informazioni sulla rimozione di un'assegnazione di ruolo, vedere [Rimozione di un ruolo da un utente o gruppo di protezione universale](remove-a-role-from-a-user-or-usg-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Rimozione di un ruolo di gestione senza ruoli figlio

Per rimuovere un ruolo senza ruoli figlio, utilizzare la seguente sintassi.

    Remove-ManagementRole <role name>

In questo esempio viene rimosso il ruolo di amministratore del server di Seattle.

    Remove-ManagementRole "Seattle Server Administrators"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-ManagementRole](https://technet.microsoft.com/it-it/library/dd351170\(v=exchg.150\)).

## Rimozione di un ruolo di gestione con ruoli figlio

Se a un ruolo che si desidera rimuovere sono associati dei ruoli figlio, è necessario eliminare anche questi. Se si tenta di rimuovere un ruolo a cui sono associati ruoli figlio senza utilizzare l'opzione *Recurse* verrà visualizzato un messaggio d'errore. Se, per rimuovere un ruolo, si utilizza l'opzione *Recurse*, verranno eliminati il ruolo specificato e tutti i ruoli figlio ad esso associati.


> [!WARNING]
> Se si utilizza l'opzione <EM>Recurse</EM>, tutti i ruoli figlio del ruolo specificato verranno rimossi assieme a questo. Prima di eseguire questo comando, accertarsi di verificare quali ruoli saranno rimossi.



Per avere la certezza che saranno rimossi soltanto i ruoli che si desidera effettivamente eliminare, assieme al comando utilizzare l'opzione *WhatIf*, in modo da verificare che l'operazione determini il risultato desiderato. Utilizzare la seguente sintassi.

    Remove-ManagementRole <role name> -Recurse -WhatIf

L'opzione *WhatIf* esegue il comando senza che avvengano modifiche e consente di visualizzare le informazioni sui ruoli che verrebbero rimossi. Per ulteriori informazioni sull'opzione *WhatIf*, vedere [Opzioni WhatIf, Confirm e ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md).

Appurato che saranno rimossi solo i ruoli desiderati, eseguire lo stesso comando senza l'opzione *WhatIf*. In questo esempio viene rimosso il ruolo di amministratore di Londra e tutti i relativi ruoli figlio.

    Remove-ManagementRole "London Administrators" -Recurse

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-ManagementRole](https://technet.microsoft.com/it-it/library/dd351170\(v=exchg.150\)).

## Rimozione di un ruolo di gestione senza ambito

Per rimuovere un ruolo senza ambito, è possibile utilizzare le procedure descritte precedentemente in Remove a management role with no child roles e Remove a management role with child roles. L'unica differenza è che, per rimuovere un ruolo senza ambito, quando si esegue il comando è necessario specificare l'opzione *UnScopedTopLevel*. In questo esempio viene rimosso un ruolo senza ambito con tutti i relativi ruoli figlio.

    Remove-ManagementRole "Custom IT Scripts" -Recurse -UnScopedTopLevel

Così come con gli altri ruoli, utilizzando l'opzione *WhatIf* sarà possibile verificare di rimuovere i ruoli corretti.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Remove-ManagementRole](https://technet.microsoft.com/it-it/library/dd351170\(v=exchg.150\)).

