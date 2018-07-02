---
title: 'Visualizzazione voci di ruolo: Exchange 2013 Help'
TOCTitle: Visualizzazione voci di ruolo
ms:assetid: d9bb0d14-db59-456c-8f50-a8d7f7323df9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd351179(v=EXCHG.150)
ms:contentKeyID: 50481807
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualizzazione voci di ruolo

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-03_

Ogni voce di ruolo di gestione rappresenta un singolo cmdlet o script. I parametri inclusi in una voce di ruolo determinano i parametri del cmdlet o dello script a cui un utente può accedere.

L'identità delle voci di ruolo è costituita dal nome del ruolo di gestione a cui è associata la voce di ruolo e dal cmdlet o dallo script a cui la voce di ruolo fa riferimento. Per ulteriori informazioni sulle voci di ruolo in Microsoft Exchange Server 2013, vedere [Informazioni sui ruoli di gestione](understanding-management-roles-exchange-2013-help.md).

Per informazioni sulle altre attività di gestione relative alle voci di ruolo, vedere [Autorizzazioni avanzate](advanced-permissions-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Ruoli di gestione" nell'argomento [Autorizzazioni per la gestione del ruolo](role-management-permissions-exchange-2013-help.md).

  - Per eseguire queste procedure, è necessario utilizzare Shell.

  - In questo argomento vengono utilizzati il pipelining, il cmdlet **Format-List**, oggetti e proprietà. Per ulteriori informazioni su questi concetti, vedere i seguenti argomenti:
    
      - [Pipelining](https://technet.microsoft.com/it-it/library/aa998260\(v=exchg.150\))
    
      - [Utilizzo dell'output del comando](working-with-command-output-exchange-2013-help.md)
    
      - [Dati strutturati](https://technet.microsoft.com/it-it/library/aa996386\(v=exchg.150\))

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Visualizzazione di un elenco di voci di ruolo

Utilizzare il cmdlet **Get-ManagementRoleEntry** per recuperare un elenco di voci di ruolo. Quando si utilizza il cmdlet **Get-ManagementRoleEntry**, è necessario specificare un valore che contenga sia il nome del ruolo contenente le voci di ruolo da elencare sia il nome del cmdlet della voce di ruolo da elencare. Combinando il nome del ruolo e del cmdlet con il carattere jolly (\*) è possibile ottenere un elenco circoscritto o più ampio di voci di ruolo.

Per ulteriori informazioni sulla sintassi e sui parametri, vedere [Get-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd335210\(v=exchg.150\)).

## Visualizzazione di un elenco di tutte le voci di ruolo in un ruolo

Per visualizzare un elenco delle voci di ruolo in un ruolo specifico, utilizzare la seguente sintassi.

    Get-ManagementRoleEntry <role name>\*

Con questo esempio vengono recuperate tutte le voci di ruolo nel ruolo `Recipient Administrators`.

    Get-ManagementRole "Recipient Administrators\*"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd335210\(v=exchg.150\)).

## Visualizzazione di un elenco dei ruoli contenenti una specifica voce di ruolo

Per visualizzare un elenco di tutti i ruoli che contengono una voce di ruolo specifica, utilizzare la seguente sintassi.

    Get-ManagementRoleEntry *\<cmdlet name>

Con questo esempio vengono recuperati tutti i ruoli contenenti la voce di ruolo **Set-Mailbox**.

    Get-ManagementRoleEntry *\Set-Mailbox

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd335210\(v=exchg.150\)).

## Visualizzazione di un elenco mirato dei ruoli contenenti voci di ruolo simili

Per visualizzare un elenco dei ruoli mirati che contengono cmdlet con nomi simili, utilizzare la seguente sintassi.

    Get-ManagementRoleEntry *<partial role name>*\*<partial cmdlet name>*

Con questo esempio viene restituito un elenco delle voci di ruolo contenenti la stringa `Mailbox` e appartenenti a ruoli il cui nome contiene la stringa `Tier 1`.

    Get-ManagementRoleEntry "*Tier 1*\*Mailbox*"

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd335210\(v=exchg.150\)).

## Visualizzazione di una singola voce di ruolo

Per visualizzare i dettagli di una singola voce di ruolo, utilizzare la seguente sintassi.

    Get-ManagementRoleEntry <role name>\<cmdlet name> | Format-List

Con questo esempio vengono recuperati i dettagli della voce di ruolo **Set-Mailbox** nel ruolo `Recipient Administrators`.

    Get-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" | Format-List

Se la voce di ruolo visualizzata presenta un numero di parametri eccessivo per l'inserimento nell'elenco creato con il cmdlet **Format-List**, vedere "Visualizzazione dei parametri di una singola voce di ruolo" in questo argomento.

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd335210\(v=exchg.150\)).

## Visualizzazione dei parametri di una singola voce di ruolo

Alcune voci di ruolo contengono un numero di parametri eccessivo per la visualizzazione con pipelining dei risultati del cmdlet **Get-ManagementRoleEntry** nel cmdlet **Format-List**. Se è necessario visualizzare tutti i parametri di una voce di ruolo, è possibile accedere direttamente alla proprietà **Parameters** dell'oggetto voce di ruolo.

Per visualizzare i parametri memorizzati nella proprietà **Parameters** di un oggetto voce di ruolo, utilizzare la seguente sintassi.

    (Get-ManagementRoleEntry <role name>\<cmdlet name>).Parameters

Con questo esempio vengono recuperati i parametri della voce di ruolo **Set-Mailbox** nel ruolo Mail Recipients.

    (Get-ManagementRoleEntry "Mail Recipients\Set-Mailbox").Parameters

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Get-ManagementRoleEntry](https://technet.microsoft.com/it-it/library/dd335210\(v=exchg.150\)).

