---
title: 'Gestire i criteri di provisioning delle cassette postali del sito: Exchange 2013 Help'
TOCTitle: Gestire i criteri di provisioning delle cassette postali del sito
ms:assetid: 2f160d1a-a031-461f-8d29-c9cd49ca1645
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ710340(v=EXCHG.150)
ms:contentKeyID: 50480351
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gestire i criteri di provisioning delle cassette postali del sito

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-02-21_

I criteri di provisioning della cassetta postale del sito si applicano solamente ai messaggi di posta elettronica inviati e ricevuti dalla cassetta del sito e alla dimensione della cassetta del sito sul server Exchange.

Per ulteriori informazioni sulle cassette postali del sito, vedere [Cassette postali del sito](site-mailboxes-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Cassette postali del sito" nell'argomento [Autorizzazioni di condivisione e collaborazione](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - Sebbene sia possibile creare più criteri di provisioning delle cassette postali del sito, solo il criterio di provisioning predefinito verrà applicato a tutte le cassette postali del sito. Non è possibile applicare più criteri all'interno dell'organizzazione.

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per eseguire questa procedura. È necessario utilizzare la shell.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Creazione di un criterio di provisioning della cassetta postale del sito

In questo esempio viene creato il criterio di provisioning predefinito SM\_ProvisioningPolicy con le seguenti impostazioni:

  - La quota di avviso per le cassette postali del sito è 9 GB.

  - Le cassette postali del sito non possono ricevere messaggi se la dimensione raggiunge 10 GB.

  - La dimensione massima dei messaggi di posta elettronica che possono essere inviati alle cassette postali del sito è 50 MB.

<!-- end list -->

    New-SiteMailboxProvisioningPolicy -Name SM_ProvisioningPolicy -IsDefault -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB -MaxReceiveSize 50MB

## Visualizzazione delle impostazioni del criterio di provisioning di una cassetta postale del sito

In questo esempio vengono restituite informazioni dettagliate su tutti i criteri di provisioning delle cassette postali del sito.

    Get-SiteMailboxProvisioningPolicy | Format-List

In questo esempio vengono restituiti tutti i criteri dell'organizzazione, ma viene visualizzata esclusivamente l'informazione `IsDefault` che identifica il criterio predefinito.

    Get-SiteMailboxProvisioningPolicy | Format-List IsDefault

## Modifica del criterio di provisioning di una cassetta postale del sito

Con questo esempio viene modificato il criterio di provisioning delle cassette postali denominato Default per impostare su 25 MB la dimensione massima di messaggi di posta elettronica che possono essere ricevuti dalla cassetta postale del sito. (quando si installa Exchange, viene creato un criterio di provisioning denominato **Default**).

    Set-SiteMailboxProvisioningPolicy -Identity Default -MaxReceiveSize 25MB

Con questo esempio vengono modificate la quota di avviso in 9,5 GB e la quota di invio e ricezione non consentiti in 10 GB.

    Set-SiteMailboxProvisioningPolicy -Identity Default -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB

## Configurazione del prefisso del nome in una cassetta postale del sito

Per impostazione predefinita, quando viene creata una cassetta postale del sito, l'indirizzo di posta elettronica deve avere un prefisso. Il prefisso nell'indirizzo di posta elettronica consente di cercare e riconoscere le cassette postali del sito e di eseguire query. Se si desidera, è possibile disattivare il prefisso oppure modificarlo per il tenant in Office 365 o per ambienti con più foreste in una distribuzione locale. Con il comportamento predefinito del prefisso, se la cassetta postale del sito viene creata in Office 365, il prefisso predefinito sarà **SMO-**. In alternativa, se la cassetta postale del sito viene creata in una distribuzione locale, il prefisso sarà **SM-**. Il comportamento predefinito cambia a seconda delle sedi, in questo modo non si verificheranno conflitti se le cassette postali del sito vengono create in entrambe le posizioni e vengono sincronizzate tra sedi diverse.

In questo esempio viene disabilitato il prefisso del nome tramite l'impostazione del parametro *DefaultAliasPrefixEnabled* su $false.

    Set-SiteMailboxProvisioningPolicy -Identity Default -DefaultAliasPrefixEnabled $false -AliasPrefix $null

In questo esempio viene modificato il criterio di provisioning e viene impostato il *AliasPrefix* su FOREST01.


> [!NOTE]
> Per gli ambienti a più foreste, si consiglia di utilizzare un prefisso diverso per ogni foresta per evitare conflitti quando gli oggetti vengono sincronizzati tra di esse e nel caso in cui le cassette postali del sito siano state create con lo stesso nome in due o più foreste.



    Set-SiteMailboxProvisioningPolicy -Identity Default -AliasPrefix FOREST01 -DefaultAliasPrefixEnabled $false


> [!NOTE]
> Nel caso di una distribuzione ibrida in Exchange locale e in Office 365, tutte le cassette postali del sito basate sul cloud vengono create con il prefisso <STRONG>SMO-</STRONG>. I prefissi per Office 365 e per Exchange locale sono diversi, in questo modo non si verificheranno conflitti se le cassette postali del sito vengono create in entrambe le posizioni e vengono sincronizzate tra sedi diverse. Il parametro del prefisso relativo all'alias ha la precedenza sul parametro DefaultAliasPrefixEnabled; di conseguenza, se il parametro <EM>AliasPrefix</EM> viene impostato su una stringa valida e non nulla, ogni nuova cassetta postale del sito avrà quella stringa anteposta all'alias.



## Eliminazione di un criterio di provisioning della cassetta postale del sito

In questo esempio viene eliminato il criterio di provisioning predefinito della cassetta postale creato durante l'installazione di Exchange.

    Remove-SiteMailboxProvisioningPolicy -Identity Default


> [!IMPORTANT]
> Innanzitutto è necessario creare e specificare un altro criterio predefinito per poter poi rimuovere il criterio denominato <STRONG>Default</STRONG>.



## Ulteriori informazioni

Per ulteriori informazioni sulla sintassi e sui parametri, vedere:

[New-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/it-it/library/jj218647\(v=exchg.150\))

[Get-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/it-it/library/jj218617\(v=exchg.150\))

[Set-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/it-it/library/jj218624\(v=exchg.150\))

[Remove-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/it-it/library/jj218672\(v=exchg.150\))

