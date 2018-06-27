---
title: 'Cassette postali del sito: Exchange 2013 Help'
TOCTitle: Cassette postali del sito
ms:assetid: 2c4393f4-d274-4e6c-bd09-9577e68c5a33
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150499(v=EXCHG.150)
ms:contentKeyID: 50480310
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cassette postali del sito

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Generalmente i messaggi di posta elettronica e i documenti sono conservati in due repository univoci e separati. La maggior parte delle organizzazioni collabora utilizzando entrambi i supporti. La sfida è rappresentata dall'esigenza di accedere ai messaggi di posta elettronica e ai documenti utilizzando diversi client. Generalmente questa situazione implica una riduzione della produttività e un'interfaccia meno intuitiva.

La *cassetta postale del sito* è un nuovo concetto di Microsoft Exchange 2013 che tenta di risolvere questo problema. Le cassette postali dei sito migliorano la collaborazione e la produttività degli utenti consentendo loro di accedere a documenti di Microsoft SharePoint 2013 e messaggi di posta elettronica di Exchange utilizzando la stessa interfaccia client. Una cassetta postale del sito è composta dall'appartenenza al sito di SharePoint 2013 (proprietari e membri), da un archivio condiviso tramite una cassetta postale di Exchange 2013 per i messaggi di posta elettronica e un sito di SharePoint 2013 per i documenti e da un'interfaccia di gestione per i requisiti di provisioning e ciclo di vita.

Le cassette postali del sito richiedono l'integrazione e la configurazione di Exchange 2013 e SharePoint Server 2013. Per ulteriori informazioni su come configurare l'organizzazione Exchange 2013 per la collaborazione con l'organizzazione SharePoint Server 2013, vedere i seguenti argomenti:

  - [Configurare cassette postali del sito in SharePoint Server 2013](https://go.microsoft.com/fwlink/p/?linkid=258264).

  - [Integrazione con SharePoint e Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md)

Per ulteriori informazioni sulle funzionalità di collaborazione in Exchange Server 2013, vedere [Collaborazione](collaboration-exchange-2013-help.md).

**Sommario**

How do site mailboxes work?

Site mailbox provisioning policies

## Funzionamento delle cassette postali del sito

Quando il membro di un progetto archivia la posta o i documenti utilizzando la cassetta postale del sito, tutti gli altri membri del progetto possono accedere al contenuto. Le cassette postali del sito sono replicate in Outlook 2013 e offrono agli utenti facile accesso alla posta elettronica e ai documenti dei progetti che li interessano. Inoltre, è possibile accedere agli stessi contenuti direttamente dallo stesso sito SharePoint. Con le cassette postali del sito, il contenuto resta nell'area di appartenenza. Exchange memorizza la posta elettronica, fornendo agli utenti la stessa visualizzazione per le conversazioni tramite posta elettronica utilizzate ogni giorno per le loro cassette postali. Nel contempo, SharePoint archivia i documenti, visualizzando nella tabelle le informazioni su autori e versioni dei documenti. Exchange sincronizza una quantità sufficiente di metadati da SharePoint per creare la visualizzazione del documento in Outlook (ad esempio, nome del documento, data ultima modifica, ultimo autore modificatore, dimensioni).

![Diagramma di archiviazione e utilizzo delle cassette postali del sito](images/JJ150499.b98be571-d2e0-4ebd-9fe2-440a14e91e35(EXCHG.150).gif "Diagramma di archiviazione e utilizzo delle cassette postali del sito")

## Criteri di provisioning per le cassette postali del sito

La quota della cassetta postale del sito può essere impostata utilizzando i cmdlet **SiteMailboxProvisioningPolicy** in Exchange Management Shell. I criteri di provisioning della cassetta postale del sito si applicano solamente ai messaggi di posta elettronica inviati e ricevuti dalla cassetta del sito e alla dimensione della cassetta del sito sul server Exchange. Le impostazioni del repository dei documenti vengono configurate in SharePoint. Sebbene sia possibile creare più criteri di provisioning delle cassette postali del sito utilizzando il cmdlet **New-SiteMailboxProvisioningPolicy**, solo il criterio di provisioning predefinito verrà applicato a tutte le cassette postali del sito. Non è possibile applicare più criteri all'interno dell'organizzazione. I criteri di provisioning consentono di impostare le seguenti quote:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Quota</th>
<th>Descrizione</th>
<th>Impostazione predefinita</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IssueWarningQuota</p></td>
<td><p>Il parametro <em>IssueWarningQuota</em> consente di specificare la dimensione della cassetta postale che causa un messaggio di avviso</p></td>
<td><p>4,5 GB</p></td>
</tr>
<tr class="even">
<td><p>MaxReceiveSize</p></td>
<td><p>Il parametro <em>MaxReceiveSize</em> consente di specificare le dimensioni massime dei messaggi di posta elettronica che può ricevere la cassetta postale del sito.</p></td>
<td><p>36 MB</p></td>
</tr>
<tr class="odd">
<td><p>ProhibitSendReceiveQuota</p></td>
<td><p>Il parametro <em>ProhibitSendReceiveQuota</em> consente di specificare la dimensione raggiunta la quale la cassetta postale del sito non può più inviare o ricevere messaggi.</p></td>
<td><p>5 GB</p></td>
</tr>
</tbody>
</table>


Per ulteriori informazioni su come configurare i criteri di provisioning delle cassette postali del sito, vedere [Gestire i criteri di provisioning delle cassette postali del sito](manage-site-mailbox-provisioning-policies-exchange-2013-help.md).

Inizio pagina

## Conservazione e criterio del ciclo di vita

Il ciclo di vita di una cassetta postale del sito viene gestito tramite SharePoint. È infatti tramite SharePoint che è necessario eseguire tutte le attività legate alle cassette postali del sito, quali la creazione e la rimozione di tutte le cassette postali del sito. Inoltre, è possibile creare un criterio del ciclo di vita di SharePoint per gestire il ciclo di vita di una cassetta postale del sito. Ad esempio, è possibile creare un criterio del ciclo di vita in SharePoint che chiuda automaticamente tutte le cassette postali del sito dopo 6 mesi. Se l'utente dovesse aver bisogno di continuare a utilizzare la cassetta postale del sito, può riattivarla sempre tramite SharePoint. Si consiglia di utilizzare l'applicazione per il ciclo di vita. L'eliminazione manuale da Exchange delle cassette postali del sito attive porterà alla presenza di cassette postali del sito orfane. .

Quando l'applicazione del criterio del ciclo di vita in SharePoint chiude una cassetta postale, questa viene conservata per il periodo impostato nel criterio con stato Chiuso. La cassetta postale può essere riattivata da un utente finale o da un amministratore tramite SharePoint. Una volta terminato il periodo di conservazione, al nome della cassetta postale del sito di Exchange ospitata nel database delle cassette verrà anteposto **MDEL:** ad indicare che la cassetta è stata contrassegnata per l'eliminazione. Sarà necessario rimuovere manualmente queste cassette postali del sito dal database delle cassette postali per liberare lo spazio di archiviazione e l'alias. Se il criterio del ciclo di vita di SharePoint non è abilitato, non sarà possibile possibile individuare le cassette postali del sito contrassegnate per l'eliminazione. Fino a quando la cassetta postale del sito non viene rimossa da un amministratore, il suo contenuto è recuperabile.

Utilizzando il seguente comando è possibile cercare e rimuovere le cassette postali del sito contrassegnate per l'eliminazione.

    Get-Mailbox MDEL:* | ?{$_.RecipientTypeDetails -eq "TeamMailbox"} | Remove-Mailbox -Confirm:$false

Le cassette postali del sito non supportano la conservazione a livello di elemento. Per le cassette postali del sito la conservazione funziona solo a livello di progetto e quindi, quando la cassetta del sito viene eliminata, anche gli elementi conservati vengono eliminati.

## Conformità

Utilizzando la console di eDiscovery in SharePoint, le cassette postali del sito possono essere incluse nell'ambito della funzione di eDiscovery in locale ed è possibile cercare le parole chiave nelle cassette postali degli utenti o del sito. Inoltre, è possibile applicare a una cassetta postale del sito la conservazione a fini giudiziari. Per ulteriori informazioni, vedere [eDiscovery sul posto](in-place-ediscovery-exchange-2013-help.md).


> [!NOTE]
> Per inserire una cassetta postale del sito sulla conservazione a fini giudiziari in Office 365, deve essere assegnato una licenza Exchange Online (piano 2). Se una cassetta postale del sito viene assegnata una licenza Exchange Online (piano 1), è necessario assegnarlo una licenza di archiviazione separata Exchange Online per mettere in attesa.



Inizio pagina

## Backup e ripristino

La funzionalità Backup e ripristino per le cassette postali del sito di Exchange ospitate sul server Cassette postali utilizzerà lo stesso metodo di backup e ripristino utilizzato per tutte le cassette postali di Exchange. Per ulteriori informazioni, vedere [Gruppi di disponibilità dei database (DAG)](database-availability-groups-dags-exchange-2013-help.md).

Per i documenti di SharePoint, eseguire il backup e il ripristino nello stesso percorso. Se il contenuto di SharePoint viene ripristinato negli stessi URL, la cassetta postale del sito continuerà a funzionare senza che siano necessarie ulteriori operazioni di configurazione. Se il ripristino viene eseguito in un URL diverso, sarà necessario utilizzare il cmdlet **Set-SiteMailbox** per aggiornare la proprietà *SharePointURL*. Si consiglia di non ripristinare SharePoint in una nuova foresta.

