---
title: 'Collaborazione: Exchange 2013 Help'
TOCTitle: Collaborazione
ms:assetid: f45c1be1-2a66-4610-a28d-4adc6d212769
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ218725(v=EXCHG.150)
ms:contentKeyID: 50482043
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Collaborazione

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

Exchange 2013 fornisce le funzionalità avanzate seguenti che possono facilitare la collaborazione tra gli utenti finali con la posta elettronica:

  - Cassette postali del sito

  - Cartelle pubbliche

  - Cassette postali condivise

  - Gruppi di distribuzione

Ogni funzionalità prevede un'esperienza utente e un set di caratteristiche diverse che devono essere utilizzati in base alle esigenze dell'utente e al tipo di organizzazione. Ad esempio, le cassette postali del sito forniscono una ricca gamma di funzionalità di collaborazione per la documentazione. Le cassette postali del sito si basano tuttavia su SharePoint Server 2013. Se non si pianifica pertanto di distribuire SharePoint, è necessario utilizzare le cartelle pubbliche per la condivisione dei documenti.

In questo argomento vengono confrontate le funzionalità di collaborazione per facilitare la scelta del tipo di funzionalità da offrire agli utenti.

## Cassette postali del sito

Dal punto di vista funzionale, una cassetta postale del sito è composta dall'appartenenza al sito di SharePoint 2013 (proprietari e membri), da un'archiviazione condivisa tramite una cassetta postale di Exchange 2013 per i messaggi di posta elettronica e un sito SharePoint 2013 per l'archiviazione e la condivisione. Le cassette postali del sito riuniscono fondamentalmente la posta elettronica di Exchange e i documenti di SharePoint. Per gli utenti, la cassetta postale del sito funge da cabinet di archiviazione centrale per il progetto, fornendo uno spazio in cui archiviare posta elettronica e documenti relativi a un progetto, accessibili e modificabili solo dai membri del sito. Inoltre, le cassette postali del sito hanno un ciclo di vita specifico e sono ottimizzate per essere utilizzate in progetti con date di inizio e fine determinate. Per implementare completamente le cassette postali del sito, gli utenti finali devono utilizzare Outlook 2013.

Per ulteriori informazioni, vedere [Cassette postali del sito](site-mailboxes-exchange-2013-help.md).

## Cartelle pubbliche

Le cartelle pubbliche sono progettate per l'accesso condiviso e offrono un metodo semplice ed efficace per raccogliere, organizzare e condividere le informazioni con altre persone del gruppo di lavoro o dell'organizzazione.

Le cartelle pubbliche organizzano il contenuto in base a una gerarchia diretta facile da sfogliare. Gli utenti scoprono contenuti interessanti e pertinenti esplorando gli opportuni rami della gerarchia. Gli utenti visualizzano sempre la gerarchia completa nella visualizzazione cartelle di Outlook. Le cartelle pubbliche rappresentano un'ottima tecnologia per l'archiviazione dei gruppi di distribuzione. Una cartella pubblica può essere abilitata alla posta elettronica e aggiunta come membro di un gruppo di distribuzione. La posta elettronica inviata al gruppo di distribuzione viene aggiunta automaticamente alla cartella pubblica per riferimenti futuri. Le cartelle pubbliche offrono anche una semplice condivisione dei documenti e non richiedono l'installazione di SharePoint Server 2013 nell'organizzazione. Infine gli utenti finali possono utilizzare le cartelle pubbliche con i client di Outlook supportati seguenti: Outlook 2007, Outlook 2010 e Outlook 2013.

Per ulteriori informazioni, vedere [Cartelle pubbliche](public-folders-exchange-2013-help.md).

## Cassette postali condivise

Una cassetta postale condivisa è una cassetta postale a cui possono accedere più utenti designati per leggere e inviare messaggi di posta elettronica e per condividere un calendario comune. Le cassette postali condivise possono fornire un indirizzo di posta elettronica generico (ad esempio, info@contoso.com o sales@contoso.com) che i clienti possono utilizzare per richiedere informazioni sulla società. Se a una cassetta postale condivisa viene assegnata l'autorizzazione "Invia come" quando un utente delegato risponde ai messaggi di posta elettronica, la risposta sembrerà provenire dalla cassetta postale (ad esempio, sales@contoso.com) e non dall'utente.

Per ulteriori informazioni, vedere [Cassette postali condivise](shared-mailboxes-exchange-2013-help.md).

## Gruppi

I gruppi, noti anche come gruppi di distribuzione, sono una raccolta di due o più destinatari presenti nella rubrica condivisa. Quando un messaggio di posta elettronica viene inviato a un gruppo, tale messaggio viene ricevuto da tutti i membri del gruppo. I gruppi di distribuzione possono essere organizzati in base a un determinato oggetto di discussione, ad esempio "Amanti dei cani" o in base a utenti che condividono una struttura di lavoro comune che richiede comunicazioni frequenti.

Per ulteriori informazioni, vedere [Destinatari](recipients-exchange-2013-help.md).

## Quale utilizzare?

Nella tabella seguente viene fornita una rassegna rapida di ogni singola funzionalità di collaborazione per agevolarne la scelta.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>Cassette postali del sito</th>
<th>Cartelle pubbliche</th>
<th>Cassette postali condivise</th>
<th>Gruppi</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Tipo di gruppo</strong></p></td>
<td><p>Gli utenti che collaborano come team a un progetto specifico con data di inizio e fine stabilite.</p></td>
<td><p>Con le dovute autorizzazioni, ciascun utente dell'organizzazione può accedere ed eseguire ricerche nelle cartelle pubbliche. Le cartelle pubbliche sono ideali per mantenere la cronologia o le conversazioni dei gruppi di distribuzione.</p></td>
<td><p>Delegati che lavorano a nome di un'identità virtuale e possono rispondere ai messaggi di posta elettronica come identità di cassetta postale condivisa. Esempio: support@tailspintoys.com</p></td>
<td><p>Gli utenti che devono inviare messaggi di posta elettronica a un gruppo di destinatari con interessi o caratteristiche comuni.</p></td>
</tr>
<tr class="even">
<td><p><strong>Dimensione ideale del gruppo</strong></p></td>
<td><p>Piccolo</p></td>
<td><p>Organizzazione di</p></td>
<td><p>Piccolo</p></td>
<td><p>Organizzazione di</p></td>
</tr>
<tr class="odd">
<td><p><strong>Accesso</strong></p></td>
<td><p>Membri e proprietari della cassetta postale del sito.</p></td>
<td><p>Accessibile da tutti gli utenti dell'organizzazione.</p></td>
<td><p>Agli utenti possono essere concesse le autorizzazioni di accesso completo e/o Invia come. Con le autorizzazioni di accesso completo, gli utenti possono anche aggiungere la cassetta postale condivisa al profilo di Outlook personale per accedere alla cassetta postale condivisa.</p></td>
<td><p>Per i gruppi di distribuzione, i membri devono essere aggiunti manualmente. Per i gruppi di distribuzione dinamici, i membri vengono aggiunti in base ai criteri di filtro.</p></td>
</tr>
<tr class="even">
<td><p><strong>Calendario condiviso?</strong></p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><strong>I messaggi arrivano nella cartella Posta in arrivo personale dell'utente?</strong></p></td>
<td><p>No, i messaggi di posta elettronica arrivano nella cassetta postale del sito.</p></td>
<td><p>No, i messaggi di posta elettronica arrivano nella cartella pubblica.</p></td>
<td><p>No, i messaggi di posta elettronica arrivano nella cartella Posta in arrivo della cassetta postale condivisa.</p></td>
<td><p>Sì. Sì, i messaggi di posta elettronica arrivano nella cartella Posta in arrivo di un membro del gruppo di distribuzione.</p></td>
</tr>
<tr class="even">
<td><p><strong>Client supportati</strong></p></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>SharePoint 2013</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
</tr>
</tbody>
</table>

