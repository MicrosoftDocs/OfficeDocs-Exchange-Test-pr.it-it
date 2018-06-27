---
title: 'Criteri delle rubriche: Exchange 2013 Help'
TOCTitle: Criteri delle rubriche
ms:assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh529948(v=EXCHG.150)
ms:contentKeyID: 50481712
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criteri delle rubriche

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-12-09_

Informazioni su come è possibile segmentare l'elenco indirizzi globale in specifici gruppi per creare elenchi personalizzati in Outlook e Outlook Web App.

Segmentazione elenco indirizzi globale (noto anche come *elenco indirizzi globale separazione*) è il processo tramite cui gli amministratori possono segmentare utenti in popolazione specifici per fornire le visualizzazioni personalizzate dell'elenco indirizzi globale dell'organizzazione. Criteri delle rubriche (criteri della Rubrica) consentono agli utenti di segmento in specifici gruppi per fornire le visualizzazioni personalizzate dell'elenco indirizzi globale dell'organizzazione (GAL). Quando si crea un criterio della Rubrica, assegnare un elenco indirizzi globale, una rubrica offline (OAB), un elenco di sala e uno o più elenchi di indirizzi per il criterio. È quindi possibile assegnare il criterio della Rubrica per gli utenti delle cassette postali, fornire loro l'accesso a un elenco indirizzi globale personalizzato in Outlook e Outlook Web App. L'obiettivo è offrire un semplice meccanismo per eseguire la segmentazione degli elenchi indirizzi globali per le organizzazioni locali che richiedono più elenchi indirizzi globali. .


> [!NOTE]
> I criteri della rubrica hanno lo scopo di ottimizzare l'Elenco indirizzi globale e gli elenchi di indirizzi per i singoli gruppi di utenti, non di impedire agli utenti di vedersi a vicenda o di comunicare insieme ad altri utenti dell'organizzazione. I criteri della rubrica creano semplicemente una separazione virtuale degli utenti dalla prospettiva della directory, non una separazione legale.



**Sommario**

How ABPs work

ABP example

Entourage, Outlook for Mac, and ABPs

## Funzionamento dei criteri della rubrica

I criteri della rubrica includono gli elenchi seguenti:

  - Un Elenco indirizzi globale

  - Una Rubrica offline

  - Un elenco di sale (ai fini della prenotazione)

  - Uno o più elenchi di indirizzi

Nella figura seguente il criterio della rubrica A è costituito da un sottoinsieme dei vari oggetti di indirizzi presenti nell'organizzazione, mostrati nella parte inferiore della figura. L'ambito risultante del criterio della rubrica è uguale a quello dell'Elenco indirizzi globale incluso nel criterio, che in questo caso è GAL1. Quando un criterio della rubrica viene creato e assegnato a un utente, gli oggetti di indirizzi nel criterio della rubrica diventano l'ambito degli oggetti visualizzabili dall'utente.

![Panoramica dei criteri della rubrica](images/Hh529948.68084064-7319-431b-be3b-0cce761258b1(EXCHG.150).gif "Panoramica dei criteri della rubrica")

Per assegnare i criteri della rubrica ai singoli utenti delle cassette postali, è possibile utilizzare i metodi seguenti:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cassetta postale nuova o esistente</th>
<th>Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nuovo</p></td>
<td><p><a href="https://technet.microsoft.com/it-it/library/aa997663(v=exchg.150)">New-Mailbox</a>, cmdlet con il parametro <em>AddressBookPolicy</em></p></td>
</tr>
<tr class="even">
<td><p>Esistente</p></td>
<td><p><a href="https://technet.microsoft.com/it-it/library/bb123981(v=exchg.150)">Set-Mailbox</a>, cmdlet con il parametro <em>AddressBookPolicy</em></p>
<p></p></td>
</tr>
</tbody>
</table>


Criteri della Rubrica hanno effetto quando l'applicazione client di un utente si connette a un server Accesso Client di Exchange 2013. Se si modifica il criterio della Rubrica, ABP aggiornato non avranno effetto fino a quando l'utente riavvia o si riconnette il client o si riavvia il server Accesso Client RPC su server cassette postali Exchange 2013.

## Agente di routing di Address book criteri

In un'organizzazione di Exchange che non utilizza i criteri della Rubrica, le operazioni seguenti si verificano quando un messaggio di posta elettronica viene creato in Outlook o Outlook Web App e inviato a un altro destinatario nella propria organizzazione di Exchange:

1.  L'indirizzo di posta elettronica si risolve. Ad esempio, se si digita **kweku@contoso.com** nel campo **A**, l'indirizzo di posta elettronica SMTP si risolve nel nome visualizzato dell'utente **Kweku Ako-Adjei**.

2.  È possibile visualizzare la scheda contatto dell'altra persona. Una volta risolto il nome, è possibile fare doppio clic sul nome dell'utente per visualizzarne le informazioni di contatto quali ufficio e numero di telefono.

Se si utilizzano ABP e non si desidera che gli utenti di organizzazioni virtuali separate visualizzino reciprocamente informazioni potenzialmente private, è possibile attivare l'agente di routing dei criteri della rubrica. Tale agente è un agente di trasporto che controlla il modo in cui i destinatari si risolvono nell'organizzazione. Quando l'agente di routing dei criteri della rubrica viene installato e configurato, gli utenti assegnati a diversi elenchi di indirizzi globali vengono visualizzati come destinatari esterni nelle schede di contatto.

Per ulteriori informazioni su come attivare l'agente di Routing in Exchange Online, vedere [Attivare il criterio della Rubrica routing](https://technet.microsoft.com/it-it/library/jj891095\(v=exchg.150\)).

Per i dettagli sull'attivazione dell'agente di routing dei criteri della rubrica in Exchange Server, vedere [Installare e configurare l'agente di Address Book Policy Routing](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md).

## Esempio di criteri della rubrica

Nel diagramma che segue Fabrikam e Tailspin Toys condividono la stessa organizzazione Exchange e lo stesso CEO. Il CEO è l'unico dipendente comune a entrambe le società.

![Due società, un CEO](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "Due società, un CEO")

Questa configurazione contiene tre criteri della rubrica:

  - Uno contiene i dipendenti e il CEO di Fabrikam

  - Uno contiene i dipendenti e il CEO di Tailspin Toys

  - Uno contiene solo il CEO

I criteri della rubrica rispettano le seguenti regole:

  - Gli utenti in Tailspin Toys possono visualizzare solo i dipendenti e il CEO di Tailspin Toys quando cercano nell'Elenco indirizzi globale.

  - Gli utenti in Fabrikam possono visualizzare solo i dipendenti e il CEO di Fabrikam quando cercano nell'Elenco indirizzi globale.

  - Il CEO può visualizzare tutti i dipendenti di Fabrikam e di Tailspin Toys quando cerca nell'Elenco indirizzi globale.

  - Gli utenti che visualizzano i membri del gruppo del CEO possono visualizzare solo i gruppi che appartengono alla società dell'utente. Non visualizzeranno i gruppi presenti nell'altra società.

## Entourage, Outlook for Mac e criteri della rubrica

Criteri della Rubrica non funzioneranno per gli utenti di Entourage o Outlook per gli utenti Mac connessi alla rete aziendale. Quando all'interno della rete aziendale, Entourage e Outlook per i client Mac connettersi direttamente al server di catalogo globale e alla query Active Directory direttamente anziché utilizzare il server Accesso Client. Outlook per Mac 2011 client che si connettono da Internet, tuttavia, può utilizzare una rubrica Offline o servizi Web Exchange (EWS). Di conseguenza, questi client possono eseguire ricerche in elenco indirizzi globale basato su ABP. assegnati Per ulteriori informazioni sull'amministrazione di Outlook per Mac 2011, vedere Planning for Outlook per Mac 2011[](https://go.microsoft.com/fwlink/p/?linkid=231878)

## Ulteriori informazioni

[Scenario: Distribuzione di criteri della Rubrica](scenario-deploying-address-book-policies-exchange-2013-help.md)

[Indirizzo procedure relative al criterio della Rubrica](https://technet.microsoft.com/it-it/library/jj891096\(v=exchg.150\)) in Exchange Online

