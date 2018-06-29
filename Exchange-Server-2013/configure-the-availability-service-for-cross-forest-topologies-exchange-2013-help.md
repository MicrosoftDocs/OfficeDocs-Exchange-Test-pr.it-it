---
title: 'Configurare il servizio disponibilità per topologie con più foreste: Exchange 2013 Help'
TOCTitle: Configurare il servizio disponibilità per topologie con più foreste
ms:assetid: f1e7d407-f0d3-47a7-8cc3-03c5980445d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb125182(v=EXCHG.150)
ms:contentKeyID: 52063118
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare il servizio disponibilità per topologie con più foreste

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2014-10-22_

Il servizio Disponibilità migliora i dati sulla disponibilità degli Information Worker fornendo informazioni sicure, coerenti e aggiornate ai client che eseguono MicrosoftOutlook. Per impostazione predefinita, questo servizio è installato con Exchange Server 2013. Nelle topologie con più foreste in cui tutti i client connessi eseguono Outlook, il servizio Disponibilità è il solo metodo per recuperare i dati sulla disponibilità. È possibile utilizzare Shell per configurare il Servizio Disponibilità per topologie con più foreste.


> [!NOTE]
> Non è possibile utilizzare EAC per configurare il servizio Disponibilità per topologie con più foreste.



## Utilizzo del servizio Disponibilità nelle foreste trusted e non trusted

Il servizio Disponibilità può essere utilizzato nelle topologie con più foreste, sia nelle foreste attendibili sia in quelle non attendibili. I tipi disponibili di informazioni sulla disponibilità dipendono dall'uso di una foresta trusted o untrusted.

**Foreste trusted**   Nelle foreste trusted, è possibile configurare il servizio Disponibilità per recuperare informazioni sulla disponibilità in base ai singoli utenti. Se il Servizio Disponibilità è configurato per recuperare le informazioni sulla disponibilità in base ai singoli utenti, il servizio può effettuare richieste tra più foreste per conto di un particolare utente. In questo modo un utente in una foresta remota può recuperare informazioni sulla disponibilità dettagliate per un utente che non appartiene alla stessa foresta.

**Foreste non trusted**   Nelle foreste non trusted, è possibile configurare il servizio Disponibilità per recuperare informazioni sulla disponibilità solo in base all'intera organizzazione. Quando il Servizio Disponibilità effettua richieste sulla disponibilità tra più foreste a livello dell'organizzazione, le informazioni sulla disponibilità vengono restituite per ogni utente nell'organizzazione. Nelle foreste non trusted, non è possibile controllare il livello delle informazioni sulla disponibilità restituite in base ai singoli utenti.

## Configurazione di Windows per le topologie a più foreste

Per impostazione predefinita, in un elenco indirizzi globale (GAL, Global Address List) sono contenuti solo i destinatari di posta elettronica di un singolo insieme di strutture. In un ambiente tra foreste, si consiglia di utilizzare Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1) per assicurarsi che l'elenco indirizzi globale (GAL) di una determinata foresta contenga i destinatari di posta elettronica di altre foreste. ILM 2007 FP1 consente di creare utenti di posta elettronica che rappresentano destinatari di altre foreste, in modo che gli utenti siano in grado di visualizzarli nell'elenco indirizzi globale e utilizzarli per inviare messaggi. Ad esempio, gli utenti della foresta A vengono visualizzati come utenti di posta elettronica nella foresta B e viceversa. Gli utenti della foresta di destinazione possono inoltre selezionare l'utente di posta elettronica che rappresenta un destinatario in un'altra foresta e inviargli un messaggio.

Per abilitare la funzionalità di sincronizzazione degli elenchi indirizzi globali, è necessario creare agenti di gestione per l'importazione di utenti, contatti e gruppi abilitati all'utilizzo della posta da specifici servizi di Active Directory in una metadirectory centralizzata in cui gli oggetti abilitati all'utilizzo della posta sono rappresentati come utenti di posta elettronica, mentre i gruppi vengono rappresentati come contatti senza appartenenze associate. Gli agenti di gestione esportano quindi gli utenti di posta elettronica in un'unità organizzativa della foresta di destinazione specificata.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento di ciascuna procedura: 5 minuti.

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Autorizzazioni del servizio Disponibilità" nell'argomento [Autorizzazioni per client e dispositivi mobili](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Operazione desiderata

## Configurazione delle informazioni sulla disponibilità in base ai singoli utenti in una topologia con più foreste trusted tramite Shell

Con questo esempio il Servizio Disponibilità viene configurato per recuperare le informazioni sulla disponibilità in base ai singoli utenti su un server Cassette postali nella foresta di destinazione.

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedrights "ms-Exch-
    EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

Con questo esempio viene definito il metodo di accesso alle informazioni sulla disponibilità utilizzato dal Servizio Disponibilità sul server Cassette postali locale nella foresta di origine. Il server Cassette postali locale è configurato per accedere alle informazioni sulla disponibilità dalla foresta ContosoForest.com in base ai singoli utenti. In questo esempio viene utilizzato l'account di servizio per recuperare le informazioni sulla disponibilità.

    Add-AvailabilityAddressSpace -Forestname ContosoForest.com -AccessMethod PerUserFB -UseServiceAccount:$true


> [!NOTE]
> Per configurare la disponibilità per più foreste bidirezionali, ripetere questi passaggi nella foresta di destinazione.



Se si sceglie di configurare la disponibilità tra foreste con trust e di utilizzare un account di servizio (anziché specificare le credenziali a livello di organizzazione o in base ai singoli utenti), è necessario estendere le autorizzazioni come mostrato nell'esempio della sezione "Configurazione della disponibilità tra foreste trusted con un account di servizio tramite Shell". L'esecuzione della procedura nella foresta di destinazione consente ai server Cassette postali nella foresta di origine di serializzare il contesto utente originale.

## Configurazione della disponibilità tra foreste trusted con un account di servizio tramite Shell

Con questo esempio viene configurata la disponibilità tra foreste trusted con un account di servizio.

    Get-MailboxServer | Add-ADPermission -Accessrights Extendedright -Extendedright "ms-Exch-EPI-Token-Serialization" -User "<Remote Forest Domain>\Exchange servers"

Per ulteriori informazioni sulla sintassi e sui parametri, vedere gli argomenti seguenti:

  - [Get-MailboxServer](https://technet.microsoft.com/it-it/library/bb123539\(v=exchg.150\))

  - [Add-ADPermission](https://technet.microsoft.com/it-it/library/bb124403\(v=exchg.150\))

  - [Add-AvailabilityAddressSpace](https://technet.microsoft.com/it-it/library/bb124122\(v=exchg.150\))

  - [Set-AvailabilityConfig](https://technet.microsoft.com/it-it/library/bb124103\(v=exchg.150\))

## Configurazione delle informazioni sulla disponibilità a livello di organizzazione in una topologia con più foreste non trusted tramite Shell

Con questo esempio l'account a livello di organizzazione viene impostato sull'oggetto di configurazione della disponibilità per configurare il livello di accesso alle informazioni sulla disponibilità nella foresta di destinazione.

    Set-AvailabilityConfig -OrgWideAccount "Contoso.com\User"

Con questo esempio viene aggiunto l'oggetto di configurazione dello spazio di indirizzi Disponibilità per la foresta di origine.

    $a = Get-Credential (Enter the credentials for organization-wide user in Contoso.com domain)
    Add-AvailabilityAddressspace -Forestname Contoso.com -Accessmethod OrgWideFB -Credential:$a

