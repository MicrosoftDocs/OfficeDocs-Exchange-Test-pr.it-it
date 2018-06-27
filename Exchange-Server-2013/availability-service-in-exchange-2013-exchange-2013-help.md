---
title: 'Servizio disponibilità in Exchange 2013: Exchange 2013 Help'
TOCTitle: Servizio disponibilità in Exchange 2013
ms:assetid: 9722dea2-2bf8-437c-85c0-3ab65b8a07b9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb232134(v=EXCHG.150)
ms:contentKeyID: 52063087
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Servizio disponibilità in Exchange 2013

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Il servizio Disponibilità di Exchange 2013 consente ai client Microsoft Outlook e Outlook Web App di accedere alle informazioni sulla disponibilità. Il servizio Disponibilità migliora l'utilizzo del calendario e delle riunioni da parte degli Information Worker, mettendo a disposizione informazioni sulla disponibilità affidabili, coerenti e aggiornate.

Outlook e Outlook Web App utilizzano il servizio Disponibilità per effettuare le attività seguenti:

  - Recupero di informazioni sulla disponibilità correnti per le cassette postali di Exchange 2013

  - Recupero di informazioni sulla disponibilità correnti da altre organizzazioni Exchange 2013

  - Recupero di informazioni sulla disponibilità pubblicate dalle cartelle pubbliche delle cassette postali sui server in cui sono in esecuzione versioni precedenti di Exchange

  - Visualizzazione degli orari lavorativi dei partecipanti

  - Visualizzazione dei suggerimenti sugli orari più adatti per le riunioni

**Sommario**

Overview of the Availability service

Information about away status

Availability service API

Availability service Network Load Balancing

Methods used to retrieve free/busy information

## Panoramica sul servizio Disponibilità

Il servizio disponibilità recupera informazioni sulla disponibilità direttamente dalla cassetta postale di destinazione per gli utenti in Exchange 2013, Exchange 2010 o Exchange 2007 e può essere configurato per recuperare le informazioni sulla disponibilità per gli utenti di versioni precedenti di Exchange. Le topologie che dispongono di cassette postali Exchange 2007, Exchange 2010 o Exchange 2013 in cui tutti i client eseguono Outlook 2007 o superiore, il servizio disponibilità viene utilizzato per recuperare le informazioni di disponibilità.

Outlook utilizza il servizio di individuazione automatica di Exchange per ottenere l'URL del servizio Disponibilità. Per ulteriori informazioni sul servizio di individuazione automatica, vedere [Servizio di individuazione automatica](autodiscover-service-for-exchange-2013.md).

È possibile utilizzare Exchange Management Shell per configurare il servizio Disponibilità. Non è possibile utilizzare l'interfaccia di amministrazione di Exchange Exchange per configurare il servizio Disponibilità.

## Informazioni sullo stato Non al computer

Il servizio Disponibilità offre anche l'accesso ai messaggi di risposta automatica che gli utenti inviano quando si trovano fuori sede per un determinato periodo di tempo.

Gli Information Worker utilizzano la funzionalità Risposte automatiche (conosciuta come Fuori sede) in Outlook e Outlook Web App per segnalare ad altri utenti che non potranno rispondere ai messaggi di posta elettronica. Questa funzionalità facilita l'impostazione e la gestione dei messaggi di risposta automatica sia per gli Information Worker che per gli amministratori.

## API del servizio Disponibilità

Il servizio Disponibilità fa parte dell'interfaccia di programmazione di Exchange 2013. Sarà disponibile come servizio Web per consentire agli sviluppatori di scrivere strumenti di terze parti a scopo di integrazione.

## Bilanciamento del carico di rete del servizio Disponibilità

L'utilizzo di Bilanciamento carico di rete (NLB) sui server Accesso client che eseguono il servizio Disponibilità può migliorare le prestazioni e l'affidabilità per gli utenti che si affidano alle informazioni sulla disponibilità. Outlook rileva l'URL del servizio Disponibilità utilizzando il servizio di individuazione automatica. Per utilizzare il bilanciamento del carico di rete con il servizio Disponibilità, è necessario modificare la configurazione.

L'URL interno viene utilizzato dalla Intranet e l'URL esterno da Internet. Se si desidera utilizzare lo stesso URL sia per il traffico interno che per il traffico esterno, assicurarsi che il DNS sia correttamente configurato per instradare il traffico interno direttamente all'URL interno. Inoltre, assicurarsi che l'URL sia accessibile sia internamente che esternamente. Per consentire il funzionamento del servizio di individuazione automatica e del servizio Disponibilità, è necessario configurare DNS in modo che mail.\<*nome dominio*\>.com e autodiscover.mail.\<*nome dominio*\>.com puntino all'IP virtuale (VIP) della soluzione di bilanciamento del carico, in cui \<*nome dominio*\> rappresenta il nome del dominio.


> [!NOTE]
> Per ulteriori informazioni, vedere <A href="https://go.microsoft.com/fwlink/p/?linkid=45959">Riferimento tecnico rete bilanciamento del carico</A> e <A href="https://go.microsoft.com/fwlink/p/?linkid=49315">Cluster di bilanciamento del carico di rete</A>. È inoltre possibile cercare siti Web del software di bilanciamento del carico di terze parti.



## Metodi utilizzati per il recupero delle informazioni sulla disponibilità

Nella seguente tabella vengono elencati i diversi metodi utilizzati per recuperare le informazioni sulla disponibilità in varie topologie a foresta singola.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Client</th>
<th>Recupero delle informazioni sulla disponibilità delle cassette postali in esecuzione</th>
<th>Cassetta postale di destinazione in esecuzione</th>
<th>Metodi di recupero disponibilità</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>Il servizio Disponibilità legge le informazioni sulla disponibilità dalla cassetta postale di destinazione.</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>Exchange 2010 o Exchange 2007</p></td>
<td><p>Il servizio Disponibilità legge le informazioni sulla disponibilità dalla cassetta postale di destinazione.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2010 o Exchange 2007</p></td>
<td><p>Exchange 2003</p></td>
<td><p>Il servizio Disponibilità stabilisce connessioni HTTP con la directory virtuale /public della cassetta postale Exchange 2003 .</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>Outlook Web App in Exchange 2010 o Outlook Web Access in Exchange 2007 chiama l'API del servizio disponibilità che legge le informazioni sulla disponibilità dalla cassetta postale di destinazione.</p></td>
</tr>
</tbody>
</table>

