---
title: 'Metriche del gruppo e i suggerimenti messaggio: Exchange 2013 Help'
TOCTitle: Metriche del gruppo e i suggerimenti messaggio
ms:assetid: 74a55072-4ba9-45bb-a18f-41afbf3de30b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ674302(v=EXCHG.150)
ms:contentKeyID: 50480895
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Metriche del gruppo e i suggerimenti messaggio

 

_**Si applica a:**Exchange Server 2013_

_**Ultima modifica dell'argomento:**2012-10-16_

La metrica di gruppo è una raccolta dei seguenti dati relativi ai gruppi di distribuzione e ai gruppi di distribuzione dinamici nell'organizzazione:

  - Numero di membri

  - Numero di membri esterni all'organizzazione

I dati della metrica di gruppo vengono utilizzati per supportare i suggerimenti messaggio in Microsoft Exchange Server 2013. I avvisi messaggio sono messaggi informativi visualizzati per i mittenti durante la composizione dei messaggi. Per ulteriori informazioni sugli avvisi messaggio, incluso un elenco completo di quelli disponibili in Exchange 2013, vedere [MailTips](mailtips-exchange-2013-help.md).

I dati della metrica di gruppo vengono utilizzati nei seguenti avvisi:

  - **Pubblico esteso**   Questo suggerimento messaggio viene visualizzato quando un mittente aggiunge un gruppo di distribuzione il cui numero di membri è considerato come un pubblico esteso in base alla configurazione dell'organizzazione. Per impostazione predefinita, qualsiasi messaggio indirizzato a più di 25 destinatari viene considerato come un pubblico esteso.

  - **Destinatari esterni**   Questo suggerimento messaggio viene visualizzato quando un mittente aggiunge un gruppo di distribuzione i cui membri sono esterni all'organizzazione.

Gli avvisi vengono valutati ogni volta che un mittente aggiunge un destinatario a un messaggio. Per fornire questa informazione, Exchange calcola i dati della metrica di gruppo nell'ambito di un processo in background per il quale è possibile pianificare l'esecuzione al di fuori dell'orario di ufficio. Quando si valutano i destinatari per gli avvisi messaggio, Exchange legge i dati della metrica di gruppo.

## Generazione della metrica di gruppo

In Exchange 2013, i dati della metrica di gruppo sono archiviati negli attributi **msExchGroupMemberCount** e **msExchGroupExternalMemberCount** sull'oggetto gruppo in Active Directory. Anche i seguenti file nella cartella %ExchangeInstallPath%GroupMetrics sono associati alla metrica di gruppo:

  - **Cookie\_*\<nnnnnnnn\>*.dsc**   Questo file di testo contiene informazioni sul server Cassette postali configurato per generare i dati della metrica di gruppo e l'indicazione temporale dell'ultima operazione di generazione della metrica di gruppo completata correttamente. In questo modo, la metrica di gruppo può generare i dati per i gruppi modificati successivamente all'ultima operazione di generazione della metrica.

  - **ChangedGroups.txt**   Questo file contiene l'elenco dei gruppi aggiornati dall'ultima creazione dei dati della metrica di gruppo.

La generazione della metrica di gruppo è gestita da una cassetta postale di arbitraggio, chiamata anche cassetta postale dell'organizzazione. Quando il parametro *GMGen* in una cassetta postale di arbitraggio è impostato su `$true`, questa è la cassetta postale che genera i dati della metrica di gruppo.

Il server Cassette postali crea i dati della metrica di gruppo completi per tutti i gruppi di distribuzione e i gruppi di distribuzione dinamici al primo avvio dell'Assistente cassette postali per la metrica di gruppo e gli aggiornamenti incrementali per tutti i gruppi modificati dall'ultima generazione completa. Per impostazione predefinita, i dati della metrica di gruppo vengono generati quotidianamente, in un momento casuale della giornata quando il carico di lavoro del server Exchange non è eccessivo. Se il carico di lavoro è sempre notevole, è possibile che la generazione della metrica di gruppo venga ignorata.

Per configurare la generazione della metrica di gruppo, vedere [Configurare le metriche di gruppo](configure-group-metrics-exchange-2013-help.md).

