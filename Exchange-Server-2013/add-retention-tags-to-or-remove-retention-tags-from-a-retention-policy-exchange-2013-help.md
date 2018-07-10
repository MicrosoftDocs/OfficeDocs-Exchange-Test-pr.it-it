---
title: 'I tag di conservazione per aggiungere o rimuovere i tag di conservazione da un criterio di conservazione: Exchange 2013 Help'
TOCTitle: I tag di conservazione per aggiungere o rimuovere i tag di conservazione da un criterio di conservazione
ms:assetid: 3a5196ce-2764-453d-9bc1-5ec22d06b40d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd362328(v=EXCHG.150)
ms:contentKeyID: 50480442
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# I tag di conservazione per aggiungere o rimuovere i tag di conservazione da un criterio di conservazione

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-02_

È possibile aggiungere tag di conservazione a un criterio di conservazione quando il criterio viene creato o in un qualsiasi momento successivo. Per informazioni dettagliate su come creare un criterio di conservazione, incluso come aggiungere contemporaneamente tag di conservazione, vedere [Creare un criterio di conservazione](create-a-retention-policy-exchange-2013-help.md).

Un criterio di conservazione può contenere i seguenti tag di conservazione:

  - Uno o più tag dei criteri di conservazione (RPT) per cartelle predefinite supportate

  - Un tag dei criteri predefiniti (DPT) con l'azione **Sposta nell'archivio**

  - Un DPT con l'azione **Elimina e consenti ripristino** o **Elimina definitivamente**

  - Un DPT per messaggi vocali

  - Qualsiasi numero di tag personali

Per ulteriori informazioni sui tag di conservazione, vedere [Tag di conservazione e criteri di conservazione](retention-tags-and-retention-policies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - I tag di conservazione non vengono applicati a una cassetta postale fino a quando non sono collegati a un criterio di conservazione e l'Assistente cartelle gestite elaborata la cassetta postale. Per avviare l'Assistente cartelle gestite in modo che l'elaborazione di una cassetta postale, vedere [Configurazione dell'Assistente cartelle gestite](configure-the-managed-folder-assistant-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzare EAC per aggiungere o rimuovere i tag di conservazione

1.  Accedere a **Gestione conformità** \>**criteri di conservazione**.

2.  Nell'elenco, selezionare il criterio di conservazione a cui aggiungere i tag di conservazione, quindi fare clic su **Modifica**![Icona Modifica](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icona Modifica").

3.  In **Criteri di conservazione**, utilizzare le seguenti impostazioni:
    
      - **Aggiungi** ![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi")   Fare clic su questo pulsante per aggiungere un tag di conservazione al criterio.
    
      - **Rimuovi** ![Icona Rimuovi](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icona Rimuovi")   Selezionare un tag nell'elenco e fare clic su questo pulsante per rimuoverlo dal criterio.

## Utilizzo della Shell per aggiungere o rimuovere i tag di conservazione

In questo esempio, vengono aggiunti tag di conservazione VPs-Default, VPs-Inbox e VPs-DeletedItems al criterio di conservazione RetPolicy-VPs, a cui non è ancora associato alcun tag di conservazione.


> [!WARNING]
> Se il criterio dispone di tag di conservazione associati, tale comando sostituisce i tag esistenti.



    Set-RetentionPolicy -Identity "RetPolicy-VPs" -RetentionPolicyTagLinks "VPs-Default","VPs-Inbox","VPs-DeletedItems"

In questo esempio viene aggiunto il tag di conservazione VPs-DeletedItems al criterio di conservazione RetPolicy-VPs, a cui sono collegati altri tag di conservazione.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Add((Get-RetentionPolicyTag 'VPs-DeletedItems').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

In questo esempio, viene rimosso il tag di conservazione VPs-Inbox dal criterio di conservazione RetPolicy-VPs.

    $TagList = (Get-RetentionPolicy "RetPolicy-VPs").RetentionPolicyTagLinks
    $TagList.Remove((Get-RetentionPolicyTag 'VPs-Inbox').DistinguishedName)
    Set-RetentionPolicy "RetPolicy-VPs" -RetentionPolicyTagLinks $TagList

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-RetentionPolicy](https://technet.microsoft.com/it-it/library/dd335196\(v=exchg.150\)) e [Get-RetentionPolicy](https://technet.microsoft.com/it-it/library/dd298086\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo

Per controllare di aver correttamente aggiunto o rimosso un tag di conservazione da un criterio di conservazione, utilizzare il cmdlet [Get-RetentionPolicy](https://technet.microsoft.com/it-it/library/dd298086\(v=exchg.150\)) per verificare la proprietà *RetentionPolicyTagLinks*.

In questo esempio, il cmdlet **Get-RetentionPolicy** viene utilizzato per recuperare i tag di conservazione aggiunti al criterio predefinito di Gestione record di messaggistica e successivamente questi tag vengono inviati tramite pipeline al cmdlet **Format-Table** per visualizzare solo il nome della proprietà di ciascun tag.

    (Get-RetentionPolicy "Default MRM Policy").RetentionPolicyTagLinks | Format-Table name

