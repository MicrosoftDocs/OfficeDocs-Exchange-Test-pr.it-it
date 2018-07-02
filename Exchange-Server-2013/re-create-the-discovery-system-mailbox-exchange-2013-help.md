---
title: 'Re-create the Discovery system mailbox: Exchange 2013 Help'
TOCTitle: Re-create the Discovery system mailbox
ms:assetid: 5ae8426b-5661-4ecb-99c4-cdd342107fb1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg588318(v=EXCHG.150)
ms:contentKeyID: 50480745
ms.date: 01/31/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Re-create the Discovery system mailbox

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2018-01-17_

La funzionalità eDiscovery in locale utilizza una cassetta postale di sistema per archiviare i metadati delle ricerche di eDiscovery in locale. Il nome visualizzato di questa cassetta postale del sistema di individuazione è **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**. Poiché le cassette postali di sistema non sono visibili nell'interfaccia di amministrazione di Exchange o negli elenchi indirizzi di Exchange, è raro che vengano eliminate inavvertitamente.

Tuttavia, se la cassetta postale del sistema di individuazione viene accidentalmente eliminata, i responsabili dell'individuazione non saranno più in grado di eseguire ricerche eDiscovery in locale o gestire le ricerche esistenti. In questo caso, per abilitare la funzionalità eDiscovery, occorre creare di nuovo la cassetta postale del sistema di individuazione.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 10 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni di provisioning dei destinatari" nell'argomento [Autorizzazioni dei destinatari](recipients-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Utilizzo di Shell per creare di nuovo la cassetta postale del sistema Discovery

1.  Eliminare l'account utente SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9} da Active Directory, se esiste. Per impostazione predefinita, il programma di installazione di Exchange Server 2013 crea la cassetta postale nel contenitore Utenti in Active Directory. Per i dettagli su come eliminare un account utente da Active Directory, vedere [Eliminare un account utente](https://go.microsoft.com/fwlink/p/?linkid=215850).

2.  Utilizzare Shell per abilitare la cassetta postale del sistema di individuazione.
    

    > [!NOTE]
    > Non è possibile utilizzare l'interfaccia di amministrazione di Exchange per abilitare la cassetta postale del sistema di individuazione.<BR>Questo comando deve essere eseguito dalla stessa directory in cui è stato estratto il supporto di installazione di Exchange.

    
    Per ricreare la cassetta postale del sistema Discovery, eseguire il comando seguente:
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## Come verificare se l'operazione ha avuto esito positivo

Per verificare di aver correttamente ricreato la cassetta postale del sistema di individuazione, utilizzare il cmdlet **Get-Mailbox** con l'opzione *Arbitration* per visualizzare le cassette postali del sistema. Verificare i risultati del comando per controllare che la cassetta postale del sistema `SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}` sia stata ricreata.


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


