---
title: 'Registri di verifica messaggi di ricerca: Exchange 2013 Help'
TOCTitle: Registri di verifica messaggi di ricerca
ms:assetid: e1678327-bcd5-42d4-a363-67f33067fe9a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb124926(v=EXCHG.150)
ms:contentKeyID: 51407435
ms.date: 01/04/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Registri di verifica messaggi di ricerca

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2013-02-25_

In Microsoft Exchange Server 2013, il registro di verifica messaggi è un record dettagliato di tutta l'attività relativa ai messaggi trasferiti al/dal servizio di trasporto sui server Cassette postali, alle/dalle cassette postali sui server Cassette postali e ai/dai server Trasporto Edge.

È possibile utilizzare il cmdlet **Get-MessageTrackingLog** in Exchange Management Shell per cercare le voci nel registro di verifica messaggi tramite specifici criteri di ricerca.

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 30 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Tracciabilità messaggi" nell'argomento [Autorizzazioni per il flusso di posta](mail-flow-permissions-exchange-2013-help.md).

  - La ricerca nei registri di verifica messaggi richiede che il servizio di ricerca nei registri di trasporto di Microsoft Exchange sia in esecuzione. Se si disabilita o si interrompe questo servizio, non è possibile effettuare ricerche nei registri di verifica messaggi o eseguire rapporti di recapito. L'arresto di questo servizio non influisce tuttavia sulle altre funzionalità di Exchange.

  - I nomi dei campi visualizzati nei risultati del cmdlet **Get-MessageTrackingLog** sono simili ai nomi dei campi effettivi utilizzati nei registri di verifica messaggi. Le differenze principali sono:
    
      - I trattini vengono rimossi dai nomi dei campi. Ad esempio, **internal-message-id** viene visualizzato come `InternalMessageId`.
    
      - Il campo **date-time** viene visualizzato come `Timestamp`.
    
      - Il campo **recipient-address** viene visualizzato come `Recipients`.
    
      - Il campo **sender-address** viene visualizzato come `Sender`.

  - Nel campo **date-time** del registro di verifica messaggi le informazioni vengono archiviate nel formato ora UTC (Coordinated Universal Time). Tuttavia, è opportuno immettere i criteri di ricerca di data e ora per i parametri *Start* o *End* nel formato di data e ora nazionale del computer utilizzato per eseguire la ricerca.

  - Non è possibile copiare i file di registro di verifica messaggi da un altro server Exchange ed eseguire quindi una ricerca utilizzando il cdmlet **Get-MessageTrackingLog**. Inoltre, se si salva manualmente un file di registro di verifica messaggi esistente, la modifica dell'indicatore di data e ora nel file interrompe la logica della query utilizzata da Exchange per effettuare le ricerche nei registri di verifica messaggi.

  - Il cmdlet Exchange 2013**Get-MessageTrackingLog** è in grado di cercare i registri di verifica messaggi sui server Exchange 2007 e Exchange 2010 nello stesso sito Active Directory.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

## Utilizzo di Shell per eseguire ricerche nei registri di verifica messaggi

Per cercare specifici eventi nelle voci dei registri di verifica messaggi, utilizzare la seguente sintassi.

    Get-MessageTrackingLog [-Server <ServerIdentity.] [-ResultSize <Integer> | Unlimited] [-Start <DateTime>] [-End <DateTime>] [-EventId <EventId>] [-InternalMessageId <InternalMessageId>] [-MessageId <MessageId>] [-MessageSubject <Subject>] [-Recipients <RecipientAddress1,RecipientAddress2...>] [-Reference <Reference>] [-Sender <SenderAddress>]

Per visualizzare le 1000 voci più recenti dei registri di verifica messaggi sul server, utilizzare il seguente comando:

    Get-MessageTrackingLog

In questo esempio vengono cercate nei registri di verifica messaggi sul server locale tutte le voci dal 28 marzo 2013 alle 8:00 al 28 marzo 2013 alle 17:00 per tutti gli eventi **FAIL** in cui il mittente del messaggio era pat@contoso.com.

    Get-MessageTrackingLog -ResultSize Unlimited -Start "3/28/2013 8:00AM" -End "3/28/2013 5:00PM" -EventId "Fail" -Sender "pat@contoso.com"

## Utilizzo di Shell per controllare l'output di una ricerca nei registri di verifica messaggi

Utilizzare la seguente sintassi.

    Get-MessageTrackingLog <SearchFilters> | <Format-Table | Format-List> [<FieldNames>] [<OutputFileOptions>]

In questo esempio viene eseguita la ricerca nei registri di verifica messaggi utilizzando i seguenti criteri di ricerca:

  - Restituire i risultati per i primi 1000 eventi di **invio**.

  - Visualizzare i risultati in formato elenco.

  - Visualizzare solo i nomi dei campi che iniziano con `Send` o `Recipient`.

  - Scrivere l'output in un nuovo file denominato `D:\Send Search.txt`.

<!-- end list -->

    Get-MessageTrackingLog -EventId Send | Format-List Send*,Recipient* > "D:\Send Search.txt"

## Utilizzo di Shell per cercare nei registri di verifica messaggi le voci dei messaggi su più server

In genere, il valore del campo di intestazione **MessageID:** resta costante mentre il messaggio viaggia nell'organizzazione Exchange. La proprietà è denominata **InternetMessageId** nelle utilità di visualizzazione delle code e **MessageId** nelle utilità di visualizzazione dei registri di verifica messaggi. Dopo aver determinato il valore di `MessageID:` di uno specifico messaggio, è possibile cercare le informazioni sul messaggio nei registri di verifica messaggi su ogni server Cassette postali dell'organizzazione Exchange.

Per cercare uno specifico messaggio in tutte le voci dei registri di verifica messaggi in tutti i server Cassette postali, utilizzare la seguente sintassi.

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId <MessageID> | Select-Object <CommaSeparatedFieldNames> | Sort-Object -Property <FieldName>

In questo esempio la ricerca nei registri di verifica messaggi viene eseguita su tutti i server Cassette postali di Exchange 2013 utilizzando i seguenti criteri di ricerca:

  - Trovare tutte le voci correlate a un messaggio con valore di **MessageID:**`<ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com>`. Tenere presente che è possibile omettere le parentesi angolari (`<``>`). In caso contrario, è necessario racchiudere l'intero valore di **MessageID:** tra virgolette.

  - Per ogni voce, visualizzare i campi **date-time**, **server-hostname**, **client-hostname**, **source**, **event-id** e **recipient-address**.

  - Ordinare i risultati per campo **date-time**.

<!-- end list -->

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com | Select-Object Timestamp,ServerHostname,ClientHostname,Source,EventId,Recipients | Sort-Object -Property Timestamp

## Utilizzo di EAC per eseguire ricerche nei registri di verifica messaggi

È possibile utilizzare la funzionalità Rapporti di recapito per gli amministratori nell'interfaccia di amministrazione di Exchange (EAC) per cercare nei registri di verifica messaggi le informazioni sui messaggi inviati o ricevuti da una specifica cassetta postale dell'organizzazione. Per ulteriori informazioni, vedere [Tenere traccia dei messaggi con i rapporti di recapito](track-messages-with-delivery-reports-exchange-2013-help.md).

