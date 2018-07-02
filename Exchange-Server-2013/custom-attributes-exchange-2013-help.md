---
title: 'Attributi personalizzati: Exchange 2013 Help'
TOCTitle: Attributi personalizzati
ms:assetid: 2b043878-0b34-4563-a9c2-28a9efa7447e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Ee423541(v=EXCHG.150)
ms:contentKeyID: 50480231
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attributi personalizzati

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-17_

Microsoft Exchange Server 2013 include 15 attributi di estensione. È possibile utilizzare questi attributi per aggiungere informazioni su un destinatario, come un ID dipendente, un'unità organizzativa (OU) o qualche altro valore personalizzato per il quale non esiste già un attribuito. Questi attributi personalizzati vengono etichettati in Active Directory come **ms-Exch-Extension-Attribute1** - **ms-Exch-Extension-Attribute15**. In Exchange Management Shell, i parametri corrispondenti sono compresi tra *CustomAttribute1* e *CustomAttribute15*. Questi attributi non vengono utilizzati da tutti i componenti di Exchange. Possono essere utilizzati per archiviare i dati di Active Directory senza dover estendere lo schema di Active Directory.

In Exchange Server 2003 e versioni precedenti, se si desiderava archiviare queste informazioni in Active Directory, si doveva creare un attributo estendendo lo schema di Active Directory. L'estensione dello schema richiede la pianificazione, il conseguimento degli identificatori di oggetto (OID) per i nuovi attributi e la verifica del processo di estensione in un ambiente di prova prima dell'implementazione in un ambiente di produzione. In Exchange 2013, le estensioni dello schema non possono essere utilizzate nei filtri destinatario utilizzati dagli elenchi indirizzi, dai criteri degli indirizzi di posta elettronica e dai gruppi di distribuzione dinamici.

**Sommario**

Advantages of custom attributes

Custom attributes examples

Custom attributes example with the ConditionalCustomAttributes parameter

Custom attribute example with ExtensionCustomAttributes parameter

## Vantaggi degli attributi personalizzati

Alcuni dei vantaggi derivanti dall'utilizzo degli attributi personalizzati:

  - Evitare l'estensione dello schema di Active Directory.

  - Gli attributi vengono creati dal programma di installazione di Exchange.

  - Per gestire gli attributi, è possibile utilizzare l'interfaccia di amministrazione di Exchange o Exchange Management Shell. Non è necessario creare i controlli personalizzati o scrivere gli script per compilare e visualizzare questi attributi.

  - Gli attributi indicano le proprietà valide per il filtro utilizzabili nel parametro *Filter* con i cmdlet dei destinatari, come **Get-Mailbox**. Possono essere utilizzati anche nell'interfaccia di amministrazione di Exchange e in Shell per creare filtri per i criteri degli indirizzi di posta elettronica, gli elenchi indirizzi e i gruppi di distribuzione dinamici.

## Attributi multivalore personalizzati

In Exchange 2010 Service Pack 2 (SP2), sono stati aggiunti cinque attributi multivalore personalizzati che consentono di archiviare ulteriori informazioni per i destinatari di posta nel caso che gli attributi personalizzati tradizionali non soddisfino le esigenze dell'utente. I parametri da *ExtensionCustomAttribute1* a *ExtensionCustomAttribute5* possono contenere fino a 1.300 valori. È possibile specificare più valori sotto forma di elenco delimitato da virgole. Questi nuovi parametri sono supportati dai seguenti cmdlet:

  - [Set-DistributionGroup](https://technet.microsoft.com/it-it/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/it-it/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/it-it/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/it-it/library/aa995950\(v=exchg.150\))

  - [Set-MailPublicFolder](https://technet.microsoft.com/it-it/library/bb123707\(v=exchg.150\))

  - [Set-RemoteMailbox](https://technet.microsoft.com/it-it/library/ff607302\(v=exchg.150\))

Per ulteriori informazioni sulle proprietà multivalore, vedere [Modifica delle proprietà multivalore](modifying-multivalued-properties-exchange-2013-help.md).

## Esempi di attributi personalizzati

In molte distribuzioni di Exchange, la creazione di un criterio degli indirizzi di posta elettronica per tutti i destinatari di un'unità organizzativa costituisce uno scenario comune. L'unità organizzativa non indica una proprietà valida per il filtro utilizzabile nel parametro *RecipientFilter* di un criterio degli indirizzi di posta elettronica o di un elenco indirizzi.


> [!NOTE]
> I gruppi di distribuzione dinamici dispongono di un altro parametro che è possibile utilizzare per limitarlo ai destinatari di un'unità organizzativa o un contenitore particolare.



Se i destinatari di tale unità organizzativa non condividono alcuna proprietà comune che è possibile filtrare, come il reparto o il percorso, è possibile compilare uno degli attributi personalizzati con un valore comune, come mostrato in questo esempio.

    Get-Mailbox -OrganizationalUnit Sales | Set-Mailbox CustomAttribute1 "SalesOU"

Ora è possibile creare un criterio degli indirizzi di posta elettronica per tutti i destinatari che dispongono della proprietà *CustomAttribute1* equivalente a SalesOU, come mostrato in questo esempio.

    New-EmailAddressPolicy -Name "Sales" -RecipientFilter { CustomAttribute1 -eq "SalesOU"} -EnabledEmailAddressTemplates "SMTP:%s%2g@sales.contoso.com"

## Esempio di attributo personalizzato con il parametro ConditionalCustomAttributes

Durante la creazione dei gruppi di distribuzione dinamici, dei criteri degli indirizzi di posta elettronica o degli elenchi indirizzi, non è necessario utilizzare il parametro *RecipeintFilter* per specificare gli attributi personalizzati. È invece possibile utilizzare i parametri da *ConditionalCustomAttribute1* a *ConditionalCustomAttribute15*.

In questo esempio viene creato un gruppo di distribuzione dinamico basato sui destinatari il cui parametro *CustomAttribute1* è impostato su SalesOU.

    New-DynamicDistributionGroup -Name "Sales Users and Contacts" -IncludedRecipients "MailboxUsers,MailContacts" -ConditionalCustomAttribute1 "SalesOU"


> [!NOTE]
> È necessario utilizzare il parametro <EM>IncludedRecipients</EM> se si utilizza un parametro <EM>Conditional</EM>. Inoltre, non è possibile utilizzare i parametri <EM>Conditional</EM> se si utilizza il parametro <EM>RecipientFilter</EM>. Se si desidera includere altri filtri per creare il gruppo di distribuzione dinamico, i criteri degli indirizzi di posta elettronica o gli elenchi indirizzi, è necessario utilizzare il parametro <EM>RecipientFilter</EM>.



## Esempio di attributo personalizzato utilizzando il parametro ExtensionCustomAttributes

In questo esempio, il parametro *ExtensionCustomAttribute1* della cassetta postale di Kweku verrà aggiornato a indicare che si è iscritto ai seguenti corsi: MATH307, ECON202, ENGL300.

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 MATH307,ECON202,ENGL300

Quindi, utilizzando il parametro *RecipientFilter* in cui *ExtensionCustomAttribute1* è uguale a MATH307, verrà creato un gruppo di distribuzione dinamico per tutti gli studenti iscritti a MATH307. Quando si utilizzano i parametri *ExtentionCustomAttributes*, è possibile utilizzare l'operatore `-eq` invece dell'operatore `-like`.

    New-DynamicDistributionGroup -Name Students_MATH307 -RecipientFilter {ExtensionCustomAttribute1 -eq "MATH307"}

In questo esempio, i valori dell'attributo *ExtensionCustomAttribute1* per Kweku vengono aggiornati a indicare che si è iscritto al corso ENGL210 e ha abbandonato il corso ECON202.

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 @{Add="ENGL210"; Remove="ECON202"}

