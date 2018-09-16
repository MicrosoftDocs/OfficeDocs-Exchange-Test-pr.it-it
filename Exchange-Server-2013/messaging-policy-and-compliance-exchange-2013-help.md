---
title: 'Criteri di messaggistica e conformità: Exchange 2013 Help'
TOCTitle: Criteri di messaggistica e conformità
ms:assetid: 65f20a20-27a4-4f6e-9b27-f8705d65b8d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Aa998599(v=EXCHG.150)
ms:contentKeyID: 50480783
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criteri di messaggistica e conformità

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

La posta elettronica è diventata un mezzo di comunicazione affidabile e molto diffuso per gli Information Worker nelle organizzazioni di tutte le dimensioni. Gli archivi di messaggistica e le cassette postali sono diventati repository dei dati importanti. Per le organizzazioni è importante creare dei criteri di messaggistica che definiscono l'utilizzo corretto dei sistemi di messaggistica, forniscono linee guida per l'utilizzo dei criteri e, se necessario, dettagli sui tipi di comunicazione eventualmente non consentiti.

Le organizzazioni devono creare dei criteri anche per gestire il ciclo di vita dei messaggi di posta elettronica, per conservare i messaggi per il periodo di tempo necessario in base ai requisiti aziendali, legali e normativi a cui sono soggette, per mantenere i record dei messaggi per eventuali controversie e indagini e per essere in grado di trovare e fornire i record dei messaggi per soddisfare le richieste di eDiscovery.

L'organizzazione deve anche proteggersi dalla perdita di informazioni riservate quali proprietà intellettuali, segreti commerciali, piani aziendali e informazioni personali raccolte o gestite al suo interno.

## Criteri di messaggistica e conformità in Exchange 2013

Nella seguente tabella è fornita una panoramica sui criteri di messaggistica e sulle funzionalità di conformità in Microsoft Exchange Server 2013, inclusi i collegamenti agli argomenti con ulteriori informazioni su queste funzionalità e sulla loro gestione.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Funzionalità</th>
<th>Descrizione</th>
<th>Resources (Risorse)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gestione record di messaggistica</p></td>
<td><p>Per risultare conformi alle normative applicabili o soddisfare requisiti aziendali o legali, le organizzazioni includono i criteri del ciclo di vita per i messaggi di posta elettronica nell'ambito del criterio di messaggistica. Tra le domande frequenti a cui questi criteri devono fornire una risposta ci sono:</p>
<ul>
<li><p>Per quanto tempo è necessario conservare i messaggi?</p></li>
<li><p>Dove devono essere conservati i messaggi?</p></li>
<li><p>Tutti i messaggi devono essere conservati per lo stesso tempo?</p></li>
</ul>
<p>Exchange 2013 include le funzionalità di Gestione record di messaggistica che consentono di implementare i criteri del ciclo di vita per i messaggi di posta elettronica. È possibile utilizzare Gestione record di messaggistica per applicare a tutti i messaggi impostazioni di conservazione uniformi, per utilizzare i criteri di conservazione per applicare un'impostazione di conservazione di riferimento a una cassetta postale e facoltativamente per consentire agli utenti di classificare i messaggi in modo che possano essere conservati per un determinato periodo di tempo.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/messaging-records-management/messaging-records-management">Gestione record di messaggistica</a></p></td>
</tr>
<tr class="even">
<td><p>Archivio locale</p></td>
<td><p>L'<em>archiviazione in locale</em> consente di controllare i dati di messaggistica dell'organizzazione eliminando la necessità di utilizzare file di archivio personale (.pst) e permettendo agli utenti di archiviare i messaggi in una <em>cassetta postale di archiviazione</em> accessibile in Outlook 2010 e versioni successive e Outlook Web App.</p></td>
<td><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Archiviazione sul posto di Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Conservazione in locale</p></td>
<td><p>In presenza di un ragionevole rischio di controversia, le organizzazioni sono tenute a conservare le informazioni in forma elettronica, inclusi i messaggi pertinenti al caso. La conservazione in locale consente di cercare e conservare i messaggi che corrispondono ai parametri della query. I messaggi sono protetti da attività quali eliminazione, modifica e contraffazione e possono essere conservati illimitatamente o per un dato periodo di tempo.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-and-litigation-holds">Archiviazione sul posto e conservazione per controversia legale</a></p></td>
</tr>
<tr class="even">
<td><p>eDiscovery in locale</p></td>
<td><p>eDiscovery in locale consente di cercare i dati nelle cassette postali all'interno dell'organizzazione Exchange, visualizzare in anteprima i risultati della ricerca e copiarli in una cassetta postale di individuazione.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery">eDiscovery sul posto</a></p></td>
</tr>
<tr class="odd">
<td><p>Inserimento nel journal</p></td>
<td><p>La creazione del journal consente alle organizzazioni di soddisfare i requisiti di conformità legale, normativa e organizzativa registrando le comunicazioni di posta elettronica in entrata e in uscita. Quando si pianifica un sistema per garantire la conservazione e la conformità dei messaggi, è fondamentale avere ben chiaro il concetto di creazione di un journal e capire come adattarlo ai criteri di conformità dell'organizzazione e in che modo Exchange 2013 può essere utile per proteggere i messaggi inseriti nel journal.</p></td>
<td><p><a href="journaling-exchange-2013-help.md">Inserimento nel journal</a></p></td>
</tr>
<tr class="even">
<td><p>Transport Rules</p></td>
<td><p>Utilizzando le regole di trasporto, è possibile cercare specifiche condizioni nei messaggi che attraversano l'organizzazione ed eseguire determinate attività su di essi. Le regole di trasporto consentono di applicare i criteri di messaggistica ai messaggi di posta elettronica, di proteggere i messaggi e i sistemi di messaggistica e di evitare una perdita di informazioni.</p></td>
<td><p><a href="mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md">Regole del flusso di posta o di trasporto</a></p></td>
</tr>
<tr class="odd">
<td><p>Prevenzione della perdita di dati (DLP)</p></td>
<td><p>Le funzionalità di prevenzione della perdita di dati consentono di proteggere i dati riservati e di informare gli utenti su criteri e normative. La prevenzione della perdita di dati consente anche di evitare che gli utenti inviino inavvertitamente informazioni riservate a persone non autorizzate. Quando si configurano i criteri per la prevenzione della perdita di dati, è possibile identificare e proteggere i dati riservati analizzando il contenuto del sistema di messaggistica che include numerosi tipi di file associati. I modelli dei criteri per la prevenzione della perdita di dati forniti in Exchange 2013 si basano su standard normativi quali PII e PCI-DSS (Payment Card Industry Data Security Standard). La prevenzione della perdita di dati è flessibile e di conseguenza consente di includere altri criteri importanti per la propria organizzazione. Inoltre, la nuova funzionalità dei suggerimenti per i criteri permette di informare gli utenti di eventuali violazioni dei criteri prima dell'invio dei dati.</p></td>
<td><p><a href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention">Prevenzione della perdita di dati</a></p></td>
</tr>
<tr class="even">
<td><p>Information Rights Management (IRM)</p></td>
<td><p>Information Rights Management (IRM) offre una protezione online e offline permanente per i messaggi e gli allegati tramite Active Directory Rights Management Services (AD RMS).</p></td>
<td><p><a href="information-rights-management-exchange-2013-help.md">Information Rights Management</a></p></td>
</tr>
<tr class="odd">
<td><p>S/MIME</p></td>
<td><p>Estensioni S/MIME (Secure/Multipurpose Internet Mail Extensions) consente agli utenti che dispongono di cassette postali di Office 365 e Exchange 2013 e Exchange Online di proteggere le informazioni riservate inviando posta elettronica firmata e crittografata all'interno dell'organizzazione. Gli amministratori possono abilitare S/MIME per le cassette postali di Office 365 sincronizzando i certificati utente tra Office 365 e i loro server in locale quindi configurare Outlook Online per supportare S/MIME.</p></td>
<td><p><a href="s-mime-for-message-signing-and-encryption-exchange-2013-help.md">S/MIME per la crittografia e firma dei messaggi</a></p></td>
</tr>
<tr class="even">
<td><p>Registrazione di controllo delle cassette postali</p></td>
<td><p>Dal momento che le cassette postali possono contenere informazioni riservate sia a livello aziendale che di singolo utente, è fondamentale tenere traccia di chi accede alle cassette postali nell'organizzazione e che attività esegue su di esse. È soprattutto importante controllare gli accessi alle cassette postali eseguiti da utenti che non ne sono i legittimi proprietari (in questo caso si parla di utenti delegati). Utilizzando la registrazione di controllo delle cassette postali, è possibile registrare gli accessi effettuati dai proprietari delle cassette postali, dai delegati (inclusi gli amministratori con autorizzazioni di accesso completo) e dagli amministratori.</p></td>
<td><p><a href="mailbox-audit-logging-exchange-2013-help.md">Registrazione di controllo delle cassette postali</a></p>
<p><a href="https://docs.microsoft.com/it-it/exchange/security-and-compliance/exchange-auditing-reports/exchange-auditing-reports">Rapporti di controllo di Exchange</a></p></td>
</tr>
<tr class="odd">
<td><p>Registrazione controlli dell'amministratore</p></td>
<td><p>I registri di controllo dell'amministratore consentono di mantenere un registro delle modifiche apportate dagli amministratori al server Exchange, alla configurazione dell'organizzazione e ai destinatari di Exchange. Si potrebbe utilizzare la registrazione dei controlli dell'amministratore come parte del processo di controllo delle modifiche o per tenere traccia delle modifiche e dell'accesso alla configurazione e ai destinatari per scopi di conformità.</p></td>
<td><p><a href="administrator-audit-logging-exchange-2013-help.md">Registrazione controlli dell'amministratore</a></p></td>
</tr>
</tbody>
</table>

