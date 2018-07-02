---
title: 'Modelli di criteri DLP forniti di Exchange: Exchange 2013 Help'
TOCTitle: Modelli di criteri DLP forniti di Exchange
ms:assetid: 7e1917ab-1920-4a52-97d1-7dfe2add6198
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ150530(v=EXCHG.150)
ms:contentKeyID: 50479755
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Modelli di criteri DLP forniti di Exchange

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-09_

In Microsoft Exchange Server 2013 e Exchange Online, è possibile utilizzare modelli di criteri di prevenzione della perdita di dati (DLP) come punto di partenza per la costruzione di criteri DLP che consentono di soddisfare specifici criteri normativi o necessità aziendali. Per rispondere alle esigenze della propria organizzazione è possibile modificare i modelli.


> [!WARNING]
> È opportuno abilitare i criteri DLP in modalità di test prima di eseguirli nell'ambiente di produzione vero e proprio. Durante i test, si consiglia di configurare delle cassette postali campione e di inviare dei messaggi di prova che richiamino i criteri di test in modo da poterne verificare i risultati.<BR>L'utilizzo di questi criteri non assicura la conformità con qualsiasi normativa. Al termine del test, effettuare le necessarie modifiche di configurazione in Exchange in modo che la trasmissione delle informazioni sia conforme ai criteri dell'organizzazione. Ad esempio, potrebbe essere necessario configurare TLS con partner commerciali conosciuti e aggiungere regole di trasporto più restrittive, quali ad esempio aggiungere protezione dei diritti ai messaggi che contengono determinati tipi di dati.



## Modelli disponibili per DLP

Nella tabella seguente sono elencati i modelli di criteri DLP in Exchange. Per ulteriori informazioni relative alla personalizzazione di questi modelli per creare criteri DLP, vedere [Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Modello</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dati finanziari Australia</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute dati finanziari in Australia, incluso carte di credito e codici SWIFT.</p></td>
</tr>
<tr class="even">
<td><p>Australia Health Records Act (HRIP Act)</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come Health Records and Information Privacy (HRIP) in Australia, quali ad esempio il numero di tessera sanitaria e il codice fiscale.</p></td>
</tr>
<tr class="odd">
<td><p>Dati di identificazione personale (PII) in Australia</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni di identificazione personale (PII) in Australia, quali ad esempio il codice fiscale e il numero della patente di guida.</p></td>
</tr>
<tr class="even">
<td><p>Legge sulla privacy in Australia</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni soggette alla legge sulla privacy in Australia, quali ad esempio il numero della patente di guida e il numero di passaporto.</p></td>
</tr>
<tr class="odd">
<td><p>Dati finanziari Canada</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute dati finanziari in Canada, incluso il numero di conto bancario e carte di credito.</p></td>
</tr>
<tr class="even">
<td><p>Canada Health Information Act (HIA)</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da Canada Health Information Act (HIA) per Alberta, incluso dati quali ad esempio numero di passaporto e informazioni sanitarie.</p></td>
</tr>
<tr class="odd">
<td><p>Canada Personal Health Act (PHIPA) - Ontario</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da Canada Personal Health Information Protection Act (PHIPA) per Ontario, incluso dati quali ad esempio numero di passaporto e informazioni sanitarie.</p></td>
</tr>
<tr class="even">
<td><p>Canada Personal Health Information Act (PHIA) - Manitoba</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da Canada Personal Health Information Act (PHIA) per Manitoba, incluso dati quali ad esempio informazioni sanitarie.</p></td>
</tr>
<tr class="odd">
<td><p>Canada Personal Information Protection Act (PIPA)</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da Canada Personal Information Protection Act (PIPA) per British Columbia, incluso dati quali ad esempio numero di passaporto e informazioni sanitarie.</p></td>
</tr>
<tr class="even">
<td><p>Canada Personal Information Protection Act (PIPEDA)</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da Canada Personal Information Protection and Electronic Documents Act (PIPEDA), incluso dati quali ad esempio numero di passaporto e informazioni sanitarie.</p></td>
</tr>
<tr class="odd">
<td><p>Dati di identificazione personale (PII) in Canada</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni di identificazione personale (PII) in Canada, quali ad esempio il numero di tessera sanitaria e il numero di previdenza sociale.</p></td>
</tr>
<tr class="even">
<td><p>France Data Protection Act</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da Data Protection Act in Francia, quali ad esempio il numero di tessera sanitaria.</p></td>
</tr>
<tr class="odd">
<td><p>Dati finanziari Francia</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute dati finanziari in Francia, incluso il numero di conto bancario, carte di credito, numero di carta di debito.</p></td>
</tr>
<tr class="even">
<td><p>Dati di identificazione personale (PII) in Francia</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni di identificazione personale (PII) in Francia, quali ad esempio il numero di passaporto.</p></td>
</tr>
<tr class="odd">
<td><p>Dati finanziari Germania</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute dati finanziari in Germania quali ad esempio numero di carta di debito EU.</p></td>
</tr>
<tr class="even">
<td><p>Dati di identificazione personale (PII) in Germania</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni di identificazione personale (PII) in Germania, quali ad esempio il numero di passaporto.</p></td>
</tr>
<tr class="odd">
<td><p>Dati finanziari Israele</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute dati finanziari in Israele, incluso il numero di conto bancario e codice SWIFT.</p></td>
</tr>
<tr class="even">
<td><p>Dati di identificazione personale (PII) in Israele</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni di identificazione personale (PII) in Israele, quali ad esempio il numero di identità nazionale.</p></td>
</tr>
<tr class="odd">
<td><p>Tutela della Privacy in Israele</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni soggette alla legge sulla privacy in Israele, incluso informazioni relative a numero di conto bancario, o identificativo nazionale.</p></td>
</tr>
<tr class="even">
<td><p>Dati finanziari Giappone</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute dati finanziari in Giappone, incluso il numero di conto bancario, carte di credito, numero di carta di debito.</p></td>
</tr>
<tr class="odd">
<td><p>Dati di identificazione personale (PII) in Giappone</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni di identificazione personale (PII) in Giappone, quali ad esempio il numero di passaporto.</p></td>
</tr>
<tr class="even">
<td><p>Protezione dei dati personali in Giappone</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni soggette alla legge sulla protezione delle informazioni personali in Giappone, incluso i dati come il numero di registrazione residenti.</p></td>
</tr>
<tr class="odd">
<td><p>PCI Data Security Standard (PCI DSS)</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni soggette a PCI Data Security Standard (PCI DSS), incluso informazioni quali numero di carta di credito o di debito.</p></td>
</tr>
<tr class="even">
<td><p>Saudi Arabia - Anti-Cyber Crime Law</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni soggette alla legge Anti-Cyber Crime in Arabia Saudita, incluso numero di conto bancario internazionale e codice SWIFT.</p></td>
</tr>
<tr class="odd">
<td><p>Dati finanziari Arabia Saudita</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute dati finanziari in Arabia Saudita, incluso il numero di conto bancario internazionale e codice SWIFT.</p></td>
</tr>
<tr class="even">
<td><p>Dati di identificazione personale (PII) in Arabia Saudita</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni di identificazione personale (PII) in Arabia Saudita, quali ad esempio il numero di identità nazionale.</p></td>
</tr>
<tr class="odd">
<td><p>U.K. Access to Medical Reports Act</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni soggette alla legge United Kingdom Access to Medical Reports Act, inclusi i dati quali ad esempio numero di servizio sanitario nazionale.</p></td>
</tr>
<tr class="even">
<td><p>U.K. Data Protection Act</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni soggette alla legge United Kingdom Data Protection Act, inclusi i dati quali ad esempio numero di servizio assicurazione nazionale.</p></td>
</tr>
<tr class="odd">
<td><p>Dati finanziari Regno Unito</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute dati finanziari nel Regno Unito, incluso il numero di conto bancario, carte di credito, numero di carta di debito.</p></td>
</tr>
<tr class="even">
<td><p>U.K. Personal Information Online Code of Practice (PIOCP)</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da United Kingdom Personal Information Online Code of Practice per il Regno Unito, incluso dati quali ad esempio informazioni sanitarie.</p></td>
</tr>
<tr class="odd">
<td><p>Dati di identificazione personale (PII) Regno Unito</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni di identificazione personale (PII) nel Regno Unito, quali ad esempio il numero di passaporto.</p></td>
</tr>
<tr class="even">
<td><p>U.K. Privacy and Electronic Communications Regulations</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da United Kingdom Privacy and Electronic Communications Regulations, inclusi dati quali informazioni finanziarie.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. Federal Trade Commission (FTC) Consumer Rules</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da U.S. Federal Trade Commission (FTC) Consumer Rules, inclusi dati come numero di carta di credito.</p></td>
</tr>
<tr class="even">
<td><p>Dati finanziari USA</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute dati finanziari negli Stati Uniti, incluso il numero di conto bancario, carte di credito, numero di carta di debito.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. Gramm-Leach-Bliley Act (GLBA)</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da Gramm-Leach-Bliley Act (GLBA), incluso informazioni quali codice di previdenza sociale o numero di carta di credito.</p></td>
</tr>
<tr class="even">
<td><p>U.S. Health Insurance Act (HIPAA)</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da United States Health Insurance Portability and Accountability Act (HIPAA), incluso informazioni quali codice di previdenza sociale e informazioni sanitarie.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. Patriot Act</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da U.S. Patriot Act, incluso informazioni quali numero di carta di credito o codice fiscale.</p></td>
</tr>
<tr class="even">
<td><p>Dati di identificazione personale (PII) Stati Uniti</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come informazioni di identificazione personale (PII) negli Stati Uniti, quali ad esempio il codice di previdenza sociale o numero della patente di guida.</p></td>
</tr>
<tr class="odd">
<td><p>U.S. State Breach Notification Laws</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da U.S. State Breach Notification Laws, inclusi dati quali codici fiscali e numeri di carte di credito.</p></td>
</tr>
<tr class="even">
<td><p>U.S. State Social Security Number Confidentiality Laws</p></td>
<td><p>Aiuta a rilevare la presenza di informazioni comunemente ritenute come regolate da U.S. State Social Security Number Confidentiality Laws, incluso informazioni quali codice di previdenza sociale.</p></td>
</tr>
</tbody>
</table>


## Ulteriori informazioni

[Prevenzione della perdita di dati](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Create a DLP policy from a template](how-to-new-dlp-data-loss-prevention-policy-template.md)

[Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

