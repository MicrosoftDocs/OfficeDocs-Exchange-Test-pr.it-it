---
title: 'Disattiva/sospende gestione record di messaggistica: Exchange 2013 Help'
TOCTitle: Disattivare o sospendere la gestione dei record di messaggistica
ms:assetid: 631191aa-3bba-4ebf-a727-c48ed2ebe176
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998580(v=EXCHG.150)
ms:contentKeyID: 52063072
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Disattivare o sospendere la gestione dei record di messaggistica

 

_**Si applica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2013-02-14_

Per soddisfare i requisiti, aziendali o IT, potrebbe essere necessario disattivare o sospendere temporaneamente Gestione record di messaggistica per un singolo utente o per un server Cassette postali. Tra i motivi per cui potrebbe essere necessario disattivare o sospendere Gestione record di messaggistica, sono compresi:

  - Se l'utente della cassetta postale non si trova in ufficio o non può accedere alla posta elettronica, è possibile disabilitare temporaneamente Gestione record di messaggistica eseguendo il mantenimento della cassetta postale. Quando viene eseguito il mantenimento, la cassetta postale non verrà più elaborata dall'Assistente cartelle gestite. Quando l'utente della cassetta postale ritorna in ufficio o è in grado di accedere nuovamente alla cassetta postale, è possibile annullare il mantenimento della cassetta postale.

  - Se è necessario verificare o risolvere problemi relativi alle prestazioni, è possibile disattivare temporaneamente Gestione record di messaggistica sul server annullando la pianificazione per L'Assistente cartelle gestite.

  - Se è necessario rimuovere un tag di conservazione dalle cassette postali (con un criterio di conservazione in cui è applicato il tag), è possibile rimuovere il tag dal criterio.

  - Se non si desidera più applicare alla cassetta postale un criterio di conservazione o un criterio cassette postali della cartella gestita, è possibile rimuovere il criterio dalla cassetta postale.

  - Se l'organizzazione decide di non utilizzare le funzionalità di Gestione record di messaggistica, è possibile disattivare in modo definitivo Gestione record di messaggistica per l'intera organizzazione. È possibile distribuire Gestione record di messaggistica in un secondo momento, se necessario.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 1 minuto

  - Le procedure descritte in questo argomento richiedono autorizzazioni specifiche. Vedere ciascuna procedura per le informazioni sulle autorizzazioni necessarie.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Operazione desiderata

## Mantenimento delle cassette postali

È possibile eseguire il mantenimento delle cassette postali per disattivare temporaneamente Gestione record di messaggistica (ad esempio, quando gli utenti sono in ferie). L'operazione sospende l'elaborazione dei criteri di conservazione per la cassetta postale finché non viene disabilitato il mantenimento. Questa operazione è diversa dalla disposizione delle cassette postali nell'archiviazione sul posto o in conservazione per controversia legale.

Per ulteriori informazioni su come eseguire il mantenimento di una cassetta postale, vedere [Archiviazione sul posto una cassetta postale di conservazione](https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/mailbox-retention-hold).

Per ulteriori informazioni sull'archiviazione sul posto e sulla conservazione per controversia legale, vedere [Archiviazione sul posto e conservazione per controversia legale](https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-and-litigation-holds).

## Rimozione dei tag di conservazione dalle cassette postali

Per rimuovere un tag di conservazione da una cassetta postale, scollegare il tag dal criterio di conservazione. Quando si scollega un tag del criterio di conservazione per una cartella predefinita, il tag della cassetta postale predefinito viene applicato a tutti gli elementi della cartella. Quando si scollega un tag personale, non sarà più disponibile all'utente. I tag applicati ai messaggi esistenti continuano a essere elaborati a meno di rimuovere il tag dall'organizzazione di Exchange.

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

In questo esempio Shell consente di scollegare il tag di conservazione Delete - 3 Days dal criterio di conservazione Corp-Users.

    $tags = (Get-RetentionPolicy "Corp-Users").RetentionPolicyTagLinks
    $tags -= "Deleted Items - 3 Days"
    Set-RetentionPolicy "Corp-Users" -RetentionPolicyTagLinks $tags

Per informazioni dettagliate sulla sintassi e sul parametro, vedere [Get-RetentionPolicy](https://technet.microsoft.com/it-it/library/dd298086\(v=exchg.150\)) e [Set-RetentionPolicy](https://technet.microsoft.com/it-it/library/dd335196\(v=exchg.150\)).

## Rimozione dei criteri di conservazione dalle cassette postali

Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Applicazione criteri di conservazione" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

È possibile fare in modo che un criterio di conservazione non venga più applicato a una cassetta postale rimuovendo il criterio dalle proprietà dell'utente della cassetta postale.

In questo esempio Shell consente di rimuovere il criterio di conservazione dalla cassetta postale jpeoples.

```powershell
Set-Mailbox jpeoples -RetentionPolicy $null.
```

In questo esempio Shell consente di rimuovere il criterio di conservazione da tutte le cassette postali nell'organizzazione Exchange.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -ne $null} | Set-Mailbox -RetentionPolicy $null

In questo esempio Shell consente di rimuovere il criterio di conservazione Corp-Finance da tutti gli utenti della cassetta postale a cui è applicato il criterio.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -eq "Corp-Finance"} | Set-Mailbox -RetentionPolicy $null

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)) e [Get-Mailbox](https://technet.microsoft.com/it-it/library/bb123685\(v=exchg.150\)).

## Disattivazione definitiva di Gestione record di messaggistica per l'intera organizzazione

Per disattivare Gestione record di messaggistica per un'organizzazione, eliminare tutti i tag e i criteri di conservazione ad eccezione del criterio ArbitrationMailbox, creato dal programma di installazione di Exchange. Una volta completata l'operazione, i criteri di conservazione non vengono applicati.


> [!WARNING]
> I criteri di conservazione includono anche i tag Sposta in archivio che consentono di spostare i messaggi nella cassetta postale di archivio dell'utente. Se viene rimosso un criterio di conservazione che dispone di un tag Sposta in archivio, gli utenti con il criterio applicato non ricevono più i messaggi spostati nell'archivio dall'Assistente cartelle gestite.<BR>Per evitare questa eventualità, rimuovere esclusivamente i tag "Elimina e consenti ripristino" e "Elimina definitivamente" dall'organizzazione e mantenere i criteri con i tag Sposta in archivio applicati. In alternativa, per gli utenti che dispongono di un archivio abilitato, è possibile spostare manualmente gli elementi alla relativa cassetta postale di archivio tramite Outlook o Outlook Web App.<BR>Prima di rimuovere i tag e i criteri di conservazione, si consiglia di verificare le impostazioni dei tag da rimuovere. Non eliminare i tag con l'azione di conservazione Sposta in archivio.



Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Gestione record di messaggistica" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).


> [!NOTE]
> Includere il parametro <EM>WhatIf</EM> opzionale nei seguenti comandi per simulare l'azione intrapresa da un comando.



In questo esempio vengono rimossi tutti i tag di eliminazione da un'organizzazione di Exchange tranne il tag Non eliminare mai, utilizzato nel criterio ArbitrationMailbox e creato dal programma di installazione di Exchange.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -ne "MoveToArchive" -and $_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

In questo esempio vengono rimossi tutti i tag di conservazione tranne il tag Non eliminare mai.

    Get-RetentionPolicyTag | ? {$_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

Il comando consente di rimuovere il criterio di conservazione Corp-Users da un'organizzazione di Exchange.

```powershell
Remove-RetentionPolicy Corp-Users
```

Per ulteriori informazioni sulla sintassi e sui parametri, vedere i seguenti argomenti:

  - [Get-RetentionPolicyTag](https://technet.microsoft.com/it-it/library/dd298009\(v=exchg.150\))

  - [Remove-RetentionPolicyTag](https://technet.microsoft.com/it-it/library/dd335092\(v=exchg.150\))

  - [Remove-RetentionPolicy](https://technet.microsoft.com/it-it/library/dd297962\(v=exchg.150\))

