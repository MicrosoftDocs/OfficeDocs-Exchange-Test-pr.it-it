---
title: 'Visualizza un ruolo: Exchange 2013 Help'
TOCTitle: Visualizza un ruolo
ms:assetid: 1875b15f-22db-4ede-b310-ea894d6211c8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335117(v=EXCHG.150)
ms:contentKeyID: 50480128
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizza un ruolo

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-03_

I ruoli di gestione possono essere elencati in una varietà di modi, a seconda delle informazioni che si desidera. Ad esempio, è possibile scegliere di monitorare solo i ruoli specifici, i ruoli che contengono solo specifici cmdlet e parametri o visualizzare i dettagli di un ruolo specifico di gestione. Per ulteriori informazioni sui ruoli di gestione in Microsoft Exchange Server 2013, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Se si desidera visualizzare un elenco di tutte le voci in un ruolo di gestione, vedere [Visualizzazione voci di ruolo](view-role-entries-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative ai ruoli, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - Questo argomento utilizza il pipelining e i cmdlet **Format-List** e **Format-Table**. Per ulteriori informazioni su questi concetti, vedere i seguenti argomenti:
    
      - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))
    
      - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Visualizzazione di un ruolo di gestione specifico

È anche possibile visualizzare i dettagli di un ruolo specifico recuperandolo utilizzando il cmdlet **Get-ManagementRole** e eseguendo il piping dell'output al cmdlet **Format-List**.

Per visualizzare i dettagli di un ruolo specifico, utilizzare la seguente sintassi.

    Get-ManagementRole <role name> | Format-List

In questo esempio vengono recuperati i dettagli sul ruolo di gestione dei Destinatari posta elettronica.

    Get-ManagementRole "Mail Recipients" | Format-List

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRole](https://technet.microsoft.com/it-it/library/dd351125\(v=exchg.150\)).

## Elencare tutti i ruoli di gestione

È possibile visualizzare un elenco di tutti i ruoli di gestione nell'organizzazione non specificando i ruoli, quando si esegue il cmdlet **Get-ManagementRole**. Per impostazione predefinita, il nome e il tipo di ogni ruolo sono inclusi nei risultati.

In questo esempio viene restituito un elenco di tutti i ruoli nell'organizzazione.

    Get-ManagementRole

Per restituire un elenco delle proprietà specifiche per tutti i ruoli nell'organizzazione, è possibile eseguire il piping dei risultati del cmdlet **Format-Table** e specificare le proprietà che si desidera nell'elenco dei risultati. Utilizzare la seguente sintassi.

    Get-ManagementRole | Format-Table <property 1>, <property 2...>

In questo esempio viene restituito un elenco di tutti i ruoli nell'organizzazione e inclusa la proprietà **Name** e ogni proprietà con la parola **Implicit** all'inizio del nome della proprietà.

    Get-ManagementRole | Format-Table Name, Implicit*

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRole](https://technet.microsoft.com/it-it/library/dd351125\(v=exchg.150\)).

## Elenco dei ruoli di gestione che contengono un cmdlet specifico

È possibile ottenere un elenco dei ruoli che contengono un cmdlet che può essere specificato tramite il parametro *Cmdlet* sul cmdlet **Get-ManagementRole**.

Per restituire un elenco dei ruoli che contengono il cmdlet che può essere specificato, utilizzare la seguente sintassi.

    Get-ManagementRole -Cmdlet <cmdlet>

In questo esempio viene restituito un elenco di ruoli che contengono il cmdlet **New-Mailbox**.

    Get-ManagementRole -Cmdlet New-Mailbox

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRole](https://technet.microsoft.com/it-it/library/dd351125\(v=exchg.150\)).

## Elenco dei ruoli di gestione che contengono un parametro specifico

È possibile ottenere un elenco dei ruoli che contengono uno o più parametri che possono essere specificati tramite il parametro *CmdletParameters* sul cmdlet **Get-ManagementRole**. Vengono restituiti solo i ruoli che contengono tutti i parametri specificati.

Quando si utilizza il parametro *CmdletParameters*, è possibile scegliere di includere il parametro *Cmdlet*. Se si include il parametro *Cmdlet*, vengono restituiti solo i ruoli che contengono i parametri specificati nel cmdlet scelto. Se non viene incluso il parametro *Cmdlet*, vengono restituiti i ruoli che contengono i parametri specificati indipendentemente dal cmdlet.

Per restituire un elenco dei ruoli che contengono i parametri specificati, utilizzare la seguente sintassi.

    Get-ManagementRole [-Cmdlet <cmdlet>] -CmdletParameters <parameter 1>, <parameter 2...>

In questo esempio viene restituito un elenco di ruoli che contiene i parametri *Database* e *Server*, indipendentemente dai cmdlet esistenti.

    Get-ManagementRole -CmdletParameters Database, Server

In questo esempio viene restituito un elenco di ruoli in cui il parametro *EmailAddresses* esiste solo nel cmdlet **Set-Mailbox**.

    Get-ManagementRole -Cmdlet Set-Mailbox -CmdletParameters EmailAddresses

È possibile utilizzare anche il carattere jolly (\*) con il parametro *Cmdlet* o *CmdletParameters* per individuare nomi parziali di cmdlet o parametri.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRole](https://technet.microsoft.com/it-it/library/dd351125\(v=exchg.150\)).

## Elenco dei ruoli di gestione di un tipo di ruolo specifico

È possibile ottenere un elenco dei ruoli basato su un ruolo specifico tramite il parametro *RoleType* sul cmdlet **Get-ManagementRole**.

Per restituire un elenco dei ruoli che corrispondono al tipo di ruolo si specificato, utilizzare la seguente sintassi.

    Get-ManagementRole -RoleType <roletype>

In questo esempio viene restituito un elenco di ruoli basato sul tipo di ruolo `UmMailboxes`.

    Get-ManagementRole -RoleType UmMailboxes

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRole](https://technet.microsoft.com/it-it/library/dd351125\(v=exchg.150\)).

## Elenco dei ruoli figlio diretti di un ruolo padre

È possibile ottenere un elenco dei ruoli che sono figli diretti di un ruolo padre specificato tramite il parametro *GetChildren* sul cmdlet **Get-ManagementRole**. Solo ruoli che contengono il ruolo specificato come ruolo padre vengono restituiti.

Per restituire un elenco dei ruoli che sono figli diretti di un ruolo padre, utilizzare la seguente sintassi.

    Get-ManagementRole <parent role name> -GetChildren

In questo esempio viene restituito un elenco dei ruoli che sono figli diretti del ruolo Ripristino d'emergenza.

    Get-ManagementRole "Disaster Recovery" -GetChildren

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRole](https://technet.microsoft.com/it-it/library/dd351125\(v=exchg.150\)).

## Elenco di tutti i ruoli figlio al di sotto di un ruolo padre

È possibile ottenere un elenco di tutta la catena dei ruoli da quello padre fino all'ultimo figlio tramite il parametro *Recurse* sul cmdlet **Get-ManagementRole**. Il parametro *Recurse* fa sì che il cmdlet **Get-ManagementRole** attraversi tutte le relazioni padre/figlio fino a raggiungere l'ultimo ruolo figlio. Il ruolo padre è incluso nell'elenco che viene restituito.

In questo esempio viene restituito un elenco di tutti i ruoli figlio di un ruolo padre.

    Get-ManagementRole <parent role name> -Recurse

In questo esempio vengono restituiti tutti i ruoli figlio del ruolo Destinatari di posta.

    Get-ManagementRole "Mail Recipients" -Recurse

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRole](https://technet.microsoft.com/it-it/library/dd351125\(v=exchg.150\)).

