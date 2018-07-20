---
title: 'Abilitare o disabilitare il ripristino di un singolo elemento per una cassetta postale: Exchange 2013 Help'
TOCTitle: Abilitare o disabilitare il ripristino di un singolo elemento per una cassetta postale
ms:assetid: 2e7f1bcd-8395-45ad-86ce-22868bd46af0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee633460(v=EXCHG.150)
ms:contentKeyID: 54652837
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Abilitare o disabilitare il ripristino di un singolo elemento per una cassetta postale

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-13_

È possibile utilizzare la Shell per abilitare o disabilitare il ripristino di un singolo elemento in una cassetta postale. In Exchange Online, ripristino di singoli elementi è attivato per impostazione predefinita, quando viene creata una nuova cassetta postale. In Exchange 2013, ripristino di singoli elementi è disabilitato quando viene creata una cassetta postale. Se il ripristino di singoli elementi è attivato, i messaggi che vengono eliminati definitivamente (cancellati) dall'utente vengono mantenuti nella cartella elementi recuperabili della cassetta postale fino alla scadenza del periodo di mantenimento elementi eliminati. Ciò consente a un amministratore di recuperare i messaggi eliminati dall'utente prima della scadenza del periodo di mantenimento elementi eliminati. Inoltre, se un messaggio viene modificato da un utente o un processo, copie dell'elemento originale inoltre vengono mantenute quando ripristino di singoli elementi è attivato.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 2 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere Voce "Conservazione e requisiti di conformità legale" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md) .

  - È possibile utilizzare l'interfaccia di amministrazione di Exchange (EAC) per abilitare o disabilitare il ripristino di un singolo elemento.

  - In Exchange Online, il periodo di mantenimento elementi eliminati è impostato su 14 giorni, per impostazione predefinita. È possibile modificare questa impostazione per un massimo di 30 giorni. Per ulteriori informazioni, vedere [Vengono conservati gli elementi eliminato in modo permanente il tempo di modifica per una cassetta postale di Exchange Online](https://technet.microsoft.com/it-it/library/dn163584\(v=exchg.150\))

  - In Exchange 2013, la cassetta postale utilizza le impostazioni di mantenimento elementi eliminati del database delle cassette postali, per impostazione predefinita. Il periodo di mantenimento elementi eliminati per un database delle cassette postali è impostato su 14 giorni, ma ignorare l'impostazione predefinita è possibile configurare questa impostazione singoli per cassetta postale. Per ulteriori informazioni, vedere [Configurare il periodo di mantenimento degli elementi eliminati e delle quote di elementi ripristinabili](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Utilizzo della Shell per abilitare il ripristino di un singolo elemento

Questo esempio attiva il ripristino di singoli elementi della cassetta postale dell'aprile giudici.

    Set-Mailbox -Identity "April Summers" -SingleItemRecoveryEnabled $true

Questo esempio attiva il ripristino di singoli elementi della cassetta postale del Pilar Pinilla e imposta il numero di giorni per cui gli elementi eliminati viene mantenuto per 30 giorni.

    Set-Mailbox -Identity "Pilar Pinilla" -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

Questo esempio attiva il ripristino di un singolo elemento per tutte le cassette postali nell'organizzazione.

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true

Questo esempio viene attivato il ripristino di un singolo elemento per tutte le cassette postali dell'organizzazione e imposta il numero di giorni per cui gli elementi eliminati viene mantenuto per 30 giorni

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\)).

## Utilizzo della Shell per disabilitare il ripristino di un singolo elemento

Potrebbe essere necessario disattivare il ripristino di un singolo elemento per la cassetta postale dell'utente. Ad esempio, prima di poter utilizzare **Search-Mailbox –DeleteContent** per eliminare definitivamente il contenuto da una cassetta postale, è necessario disabilitare il ripristino di un singolo elemento. Per ulteriori informazioni, vedere [Ricerca ed eliminazione di messaggi - Guida di Amministrazione](search-for-and-delete-messages-admin-help-exchange-2013-help.md).

In questo esempio consente di disabilitare il ripristino di singoli elementi della cassetta postale di Ayla Kol.

    Set-Mailbox -Identity "Ayla Kol" -SingleItemRecoveryEnabled $false

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver abilitato il ripristino di singoli elementi di una cassetta postale e visualizzare il valore per quanto tempo verranno mantenuti gli elementi eliminati (in giorni), eseguire il comando seguente.

    Get-Mailbox <Name> | FL SingleItemRecoveryEnabled,RetainDeletedItemsFor

È possibile utilizzare lo stesso comando per verificare che il ripristino di singoli elementi è disabilitato per una cassetta postale.

## Ulteriori informazioni

  - Per ulteriori informazioni sul ripristino di un singolo elemento, vedere [Cartella Elementi ripristinabili](recoverable-items-folder-exchange-2013-help.md). Per recuperare i messaggi eliminati dall'utente prima del periodo di mantenimento elementi eliminati scade, vedere [Recuperare i messaggi eliminati nella cassetta postale dell'utente](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md).

  - Se una cassetta postale viene inserita nella conservazione In locale o conservazione per controversia legale, i messaggi nella cartella elementi recuperabili vengono mantenuti finché non scade la durata dell'attesa. Se la durata di attesa è illimitata, gli elementi vengono conservati fino alla rimozione o viene modificata la durata dell'attesa.

