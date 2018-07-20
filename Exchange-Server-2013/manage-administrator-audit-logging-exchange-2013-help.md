---
title: 'Amministratore di gestire la registrazione di controllo: Exchange 2013 Help'
TOCTitle: Amministratore di gestire la registrazione di controllo
ms:assetid: 15c284c0-b8e6-42ca-9913-7c59fdb6885d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335109(v=EXCHG.150)
ms:contentKeyID: 50555543
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Amministratore di gestire la registrazione di controllo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-05-17_

La registrazione controlli dell'amministratore in Microsoft Exchange Server 2013 consente di creare una voce di registro ogni volta che si esegue un cmdlet specificato. Le voci di registro forniscono informazioni sul cmdlet eseguito, sui parametri utilizzati, sull'utente che ha eseguito il cmdlet e sugli oggetti coinvolti. Per ulteriori informazioni sulla registrazione dei controlli dell'amministratore, vedere [Registrazione controlli dell'amministratore](administrator-audit-logging-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: meno di 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Registrazione di controllo dell'amministratore" nell'argomento [Autorizzazioni infrastruttura Exchange ed Exchange Management Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - La registrazione dei controlli dell'amministratore si basa sulla replica di Active Directory per replicare le impostazioni di configurazione specificate nei controller di dominio nell'organizzazione. In base alle impostazioni della replica, le modifiche apportate potrebbero non essere immediatamente applicate a tutti i server Exchange 2013 dell'organizzazione.

  - Le modifiche alla configurazione del registro di controllo vengono aggiornate ogni 60 minuti sui computer che hanno Shell aperta al momento delle modifiche alla configurazione. Se si desidera applicare immediatamente le modifiche, chiudere e aprire di nuovo Shell su ogni computer.

  - Potrebbe essere necessario aspettare fino a 15 minuti dopo l'esecuzione di un comando affinché venga visualizzato nei risultati di ricerca del registro di controllo. Questo perché le voci del registro di controllo devono essere indicizzate prima di poter essere ricercate. Se un comando non viene visualizzato nel registro di controllo dell'amministratore, attendere qualche minuto ed eseguire nuovamente la ricerca.

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Scelta dei cmdlet da sottoporre a controllo

Per impostazione predefinita, la registrazione controlli crea una voce di registro per ogni cmdlet eseguito. Se si abilita la registrazione controlli per la prima volta e si desidera che questa operazione venga eseguita, non è necessario modificare l'elenco di controllo dei cmdlet. Se sono stati specificati dei cmdlet ma si desidera controllare tutti i cmdlet, è possibile eseguire l'operazione specificando il carattere jolly asterisco (\*) con il parametro *AdminAuditLogCmdlets* del cmdlet **Set-AdminAuditLogConfig**, come mostrato nel comando seguente.

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets *

È possibile specificare quali cmdlet controllare fornendo un elenco di cmdlet utilizzando il parametro *AdminAuditLogCmdlets*. Quando viene fornito l'elenco dei cmdlet da controllare, è possibile specificare singoli cmdlet, cmdlet con caratteri jolly asterisco (\*) o entrambi. Ogni voce dell'elenco viene separata da una virgola. Sono validi i seguenti valori:

  - `New-Mailbox`

  - `*TransportRule`

  - `*Management*`

  - `Set-Transport*`

In questo esempio vengono controllati i cmdlet specificati nell'elenco precedente.

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets New-Mailbox, *TransportRule, *Management*, Set-Transport*

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-AdminAuditLogConfig](https://technet.microsoft.com/it-it/library/dd298169\(v=exchg.150\)).

## Scelta dei parametri da sottoporre a controllo

Per impostazione predefinita, la registrazione di controllo crea una voce di registro per ogni cmdlet eseguito, indipendentemente dai parametri specificati. Se si abilita la registrazione controlli per la prima volta e si desidera che questa operazione venga eseguita, non è necessario modificare l'elenco di controllo dei parametri. Se in precedenza sono stati specificati dei parametri ma ora si desidera controllare tutti i parametri, è possibile eseguire l'operazione specificando il carattere jolly asterisco (\*) con il parametro *AdminAuditLogParameters* del cmdlet **Set-AdminAuditLogConfig**, come mostrato nel comando seguente.

    Set-AdminAuditLogConfig -AdminAuditLogParameters *

È possibile specificare i parametri che si desidera controllare utilizzando il parametro *AdminAuditLogParameters*. Quando viene fornito l'elenco dei parametri da controllare, è possibile specificare singoli parametri, parametri con caratteri jolly asterisco(\*) o entrambi. Ogni voce dell'elenco viene separata da una virgola. Sono validi i seguenti valori:

  - `Database`

  - `*Address*`

  - `Custom*`

  - `*Region`


> [!NOTE]
> Per creare una voce di registro quando viene eseguito un comando, questo deve includere almeno un parametro o più parametri presenti in almeno un cmdlet o in più cmdlet specificati con il parametro <EM>AdminAuditLogCmdlets</EM>.



In questo esempio vengono controllati i parametri specificati nell'elenco precedente.

    Set-AdminAuditLogConfig -AdminAuditLogParameters Database, *Address*, Custom*, *Region

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-AdminAuditLogConfig](https://technet.microsoft.com/it-it/library/dd298169\(v=exchg.150\)).

## Determinazione del periodo di validità del registro di controllo

Il periodo di validità del registro di controllo determina per quanto tempo verranno conservate le voci del registro di controllo. Quando una voce di registro supera il periodo di validità, viene eliminata. Il valore predefinito è 90 giorni.

È possibile specificare il numero di giorni, ore, minuti e secondi in cui le voci del registro di controllo devono essere conservate. Per specificare un valore, utilizzare il formato gg.hh.mm:ss in cui si applica quanto segue:

  - **gg**   Numero di giorni in cui mantenere la voce del registro di controllo

  - **hh**   Numero di ore in cui mantenere la voce del registro di controllo

  - **mm**   Numero di minuti in cui mantenere la voce del registro di controllo

  - **ss**   Numero di secondi in cui mantenere la voce del registro di controllo


> [!WARNING]
> È possibile impostare il periodo di validità del registro di controllo su un valore inferiore al periodo di validità corrente. Se si esegue questa operazione, verrà eliminata ogni voce del registro di controllo la cui validità supera il nuovo limite.<BR>Se si imposta il periodo di validità su 0, Exchange elimina tutte le voci dal registro di controllo.<BR>Si consiglia di concedere le autorizzazioni per la configurazione del periodo di validità del registro di controllo solo agli utenti molto attendibili.



In questo esempio viene specificato un periodo di validità di due anni e sei mesi.

    Set-AdminAuditLogConfig -AdminAuditLogAgeLimit 913.00:00:00

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-AdminAuditLogConfig](https://technet.microsoft.com/it-it/library/dd298169\(v=exchg.150\)).

## Abilitazione o disabilitazione della registrazione dei cmdlet Test

I cmdlet che iniziano con il verbo **Test** non vengono registrati per impostazione predefinita. Questo perché i cmdlet **Test** possono generare una notevole quantità di dati in breve tempo. Abilitare la registrazione dei cmdlet **Test** solo per brevi periodi di tempo.

Questo comando consente di abilitare la registrazione dei cmdlet **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $True

Questo comando consente di disabilitare la registrazione dei cmdlet **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $False

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-AdminAuditLogConfig](https://technet.microsoft.com/it-it/library/dd298169\(v=exchg.150\)).

## Disabilitazione della registrazione di controllo dell'amministratore

Per disabilitare la registrazione di controllo dell'amministratore, utilizzare il seguente comando.

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $False

## Abilitare la registrazione di controllo dell'amministratore

Per abilitare la registrazione di controllo dell'amministratore, utilizzare il seguente comando.

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $True

## Visualizzazione delle impostazioni per la registrazione di controllo dell'amministratore

Per visualizzare le impostazioni per la registrazione di controllo dell'amministratore configurate per l'organizzazione, utilizzare il seguente comando.

    Get-AdminAuditLogConfig

