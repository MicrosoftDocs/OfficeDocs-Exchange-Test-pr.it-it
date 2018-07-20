---
title: 'Opzioni WhatIf, Confirm e ValidateOnly: Exchange 2013 Help'
TOCTitle: Opzioni WhatIf, Confirm e ValidateOnly
ms:assetid: a850eea7-431e-49c5-b877-1ebde2a2b48f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124088(v=EXCHG.150)
ms:contentKeyID: 50481364
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Opzioni WhatIf, Confirm e ValidateOnly

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-04_

Sia gli amministratori e gli autori di script esperti che gli amministratori che non conoscono Exchange e lo scripting possono trarre vantaggio dall'utilizzo delle opzioni *WhatIf*, *Confirm* e *ValidateOnly*. Questi parametri consentono di controllare la modalità di esecuzione dei comandi e indicano esattamente l'effetto di un comando prima che influisca effettivamente sui dati. Questa funzionalità è particolarmente importante quando si passa dall'ambiente di prova all'ambiente di produzione e quando si esegue il roll-out di nuovi script o comandi.

Le opzioni *WhatIf*, *Confirm* e *ValidateOnly* sono particolarmente utili quando sono associate ai comandi che modificano gli oggetti restituiti utilizzando un filtro o un comando **Get** in una pipeline. Questo argomento descrive i singoli parametri e fornisce un comando di esempio per ciascuno di essi.


> [!IMPORTANT]
> Per utilizzare le opzioni <EM>WhatIf</EM>, <EM>Confirm</EM> e <EM>ValidateOnly</EM> con i comandi in uno script, è necessario aggiungere l'opzione appropriata a ogni comando nello script e non sulla riga di comando che richiama lo script.




> [!NOTE]
> <EM>WhatIf</EM>, <EM>Confirm</EM> e <EM>ValidateOnly</EM> sono denominati parametri di opzione. Per ulteriori informazioni sui parametri opzionali, vedere <A href="https://technet.microsoft.com/it-it/library/bb124388(v=exchg.150)">Parametri</A>.



## Opzione WhatIf

L'opzione *WhatIf* consente l'esecuzione del comando a cui è applicato solo per visualizzare gli oggetti interessati dall'esecuzione del comando e le eventuali modifiche apportate a tali oggetti. Il parametro non modifica effettivamente alcun oggetto. Utilizzando l'opzione *WhatIf* è possibile vedere se le eventuali modifiche agli oggetti soddisfano le proprie aspettative, senza preoccuparsi di modificare gli oggetti.

Quando si esegue un comando insieme all'opzione *WhatIf*, inserire l'opzione *WhatIf* alla fine del comando, come nell'esempio seguente:

    New-AcceptedDomain -Name "Contoso Domain" -DomainName "contoso.com" -WhatIf 

Quando si esegue questo comando di esempio, Shell visualizza il testo seguente:

    What if: Creating Accepted Domain "Contoso Domain" with domain name "contoso.com".

## Opzione Confirm

L'opzione *Confirm* consente al comando a cui è applicato di interrompere l'elaborazione prima che vengano apportate eventuali modifiche. Il comando richiede infatti di confermare ogni azione prima di continuare. Quando si utilizza l'opzione *Confirm*, è possibile valutare ogni singola modifica per accertarsi che vengano modificati solo gli oggetti desiderati. Questa funzionalità è utile quando si apportano modifiche a più oggetti e si desidera avere un controllo preciso sul funzionamento di Shell. Prima che Shell modifichi ogni oggetto, viene visualizzato una richiesta di conferma.

Per impostazione predefinita, Shell applica automaticamente l'opzione *Confirm* ai cmdlet con i verbi seguenti:

  - **Clear**

  - **Disable**

  - **Dismount**

  - **Move**

  - **Remove**

  - **Stop**

  - **Suspend**

  - **Uninstall**

Quando viene eseguito un cmdlet con uno di questi verbi, Shell interrompe automaticamente il comando e attende la conferma prima di continuare l'elaborazione.

Quando si applica manualmente l'opzione *Confirm* a un comando, inserire l'opzione *Confirm* alla fine del comando, come nell'esempio seguente:

    Get-JournalRule | Enable-JournalRule -Confirm

Quando si esegue questo comando di esempio, Shell visualizza la seguente richiesta di conferma:

    Confirm
    Are you sure you want to perform this action?
    Enabling journal rule "Litigation Journal Rule".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
    (default is "Y"):

La richiesta di conferma consente di scegliere tra le seguenti possibilità:

  - **\[Y\] Yes**   Digitare **Y** affinché il comando continui l'operazione. L'operazione successiva presenterà un'altra richiesta di conferma. `[Y] Yes` è la scelta predefinita.

  - **\[A\] Yes to All**   Digitare **A** affinché il comando continui l'operazione in corso e tutte quelle successive. Non si riceveranno ulteriori richieste di conferma per la durata di questo comando.

  - **\[N\] No**   Digitare **N** affinché il comando ignori questa operazione e passi a quella successiva. L'operazione successiva presenterà un'altra richiesta di conferma.

  - **\[L\] No to All**   Digitare **L** affinché il comando ignori l'operazione in corso e tutte quelle successive.

  - **\[S\] Suspend**   Digitare **S** per mettere in pausa la pipeline corrente e tornare alla riga di comando. Digitare **Exit** per riprendere la pipeline.

  - **\[?\] Help**   Digitare **?** per visualizzare la guida alle richieste di conferma sulla riga di comando.

Per sostituire l'impostazione predefinita di Shell ed eliminare la richiesta di conferma per i cmdlet a cui è applicata automaticamente, è possibile includere l'opzione *Confirm* con il valore `$False`, come nell'esempio seguente:

    Get-JournalRule | Disable-JournalRule -Confirm:$False

In questo caso non saranno visualizzate richieste di conferma.


> [!WARNING]
> Il valore predefinito dell'opzione <EM>Confirm</EM> è <CODE>$True</CODE>. Per impostazione predefinita, Shell visualizza automaticamente la richiesta di conferma. Se si modifica questo impostazione predefinita, il comando eliminerà tutte le richieste di conferma per la sua durata. Il comando elaborerà tutti gli oggetti che soddisfano i criteri stabiliti per il comando senza richiedere alcuna conferma.



## Opzione ValidateOnly

L'opzione *ValidateOnly* consente al comando a cui è applicato di valutare tutte le condizioni e i requisiti necessari per eseguire l'operazione prima di apportare eventuali modifiche. L'opzione *ValidateOnly* è disponibile per i cmdlet la cui esecuzione potrebbe richiedere molto tempo, che hanno diverse dipendenze su più sistemi o che influiscono su dati critici, ad esempio le cassette postali.

Quando si applica l'opzione *ValidateOnly* a un comando, questo viene eseguito per l'intero processo. Il comando esegue ogni azione come se l'opzione *ValidateOnly* non fosse stata applicata, tuttavia non modifica alcun oggetto. Al termine dell'elaborazione, il comando visualizza un riepilogo con i risultati della convalida. Se la convalida indica che l'esecuzione del comando è stata completata correttamente, è possibile eseguire di nuovo il comando senza l'opzione *ValidateOnly*.

Quando si esegue un comando insieme all'opzione *ValidateOnly*, l'opzione *ValidateOnly* deve essere inserita alla fine del comando.

