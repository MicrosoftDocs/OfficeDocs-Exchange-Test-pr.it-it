---
title: 'Proteggere i dati del modulo con documento fingerprinting: Exchange 2013 Help'
TOCTitle: Proteggere i dati del modulo con documento fingerprinting
ms:assetid: 110c839b-7693-42f6-aa5d-58ce64f4c357
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn635175(v=EXCHG.150)
ms:contentKeyID: 61202263
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Proteggere i dati del modulo con documento fingerprinting

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2014-09-11_

If your organization uses forms to collect sensitive information, users might try emailing those forms to outside contacts, which creates a security risk. Data loss prevention (DLP) in Exchange consente di proteggere le informazioni rilevandole nel [Creazione impronta digitale documenti](overview-of-document-fingerprinting-in-exchange.md). Per utilizzare l'impronta digitale del documento, basta semplicemente caricare un modulo vuoto, ad esempio un documento di proprietà intellettuale, un modulo governativo o un altro modulo standard usato nell'organizzazione. Quindi, aggiungere l'impronta digitale del documento risultante al criterio DLP o alla regola di trasporto. Ecco come fare.

> [!VIDEO https://www.microsoft.com/it-it/videoplayer/embed/0f803e16-397a-4b83-8a85-06cd4264aaca]

## Utilizzo di EAC per creare un'impronta digitale del documento

![Percorso per Creazione impronta digitale documenti in EAC evidenziato](images/Dn635175.e8562ea7-40ba-4feb-adde-2e81f029fcda(EXCHG.150).png "Percorso per Creazione impronta digitale documenti in EAC evidenziato")

1.  Nell'interfaccia di amministrazione di Exchange, andare a **Gestione conformità** \> **Prevenzione della perdita di dati**.

2.  Fare clic su **Gestione delle impronte digitali dei documenti**.

3.  Nella pagina sulle impronte digitali del documento, fare clic s **Nuova**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi") per creare una nuova impronta digitale del documento.

4.  Assegnare all'impronta digitale del documento un **Nome** e una **Descrizione**. Il nome scelto verrà visualizzato nell'elenco dei tipi di informazioni riservate

5.  Per caricare un modulo, fare clic su **Aggiungi**![Icona Aggiungi](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Icona Aggiungi").

6.  Scegliere un modulo e fare clic su **Apri**. (Assicurarsi che il file è caricare contiene testo, non è protetto da password e si trova in uno dei tipi di file supportati nelle regole di trasporto. Per un elenco di tipi di file supportati, vedere [Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/it-it/library/jj919236\(v=exchg.150\)). In caso contrario, verrà visualizzato un errore quando si tenta di creare l'impronta digitale.) Ripetere per tutti i file aggiuntivi che si desidera aggiungere all'elenco di documenti per questo impronta digitale del documento. È inoltre possibile aggiungere o rimuovere file da questa impronta digitale del documento in seguito se si desidera.

7.  Fare clic su **Salva**.

L'impronta digitale del documento è ora parte dei tipi di informazioni riservate ed è possibile aggiungere a un criterio DLP o aggiungerlo a una regola di trasporto tramite la condizione **il messaggio contiene informazioni riservate...**.

![Condizione "Applica questa regola se" evidenziata](images/Dn635175.9355a513-a790-48eb-a61b-575ba2ecdfa6(EXCHG.150).png "Condizione \"Applica questa regola se\" evidenziata")

Per ulteriori informazioni sull'aggiunta di regole a un criterio DLP, vedere la sezione su come modificare un criterio DLP di [Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md) e per ulteriori informazioni sulla modifica delle regole di trasporto, vedere [Integrazione di regole di informazioni sensibili con le regole di trasporto](https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/integrate-sensitive-information-rules). Se si desidera creare un nuovo criterio, vedere [Create a DLP policy from a template](how-to-new-dlp-data-loss-prevention-policy-template.md).

## Utilizzare Shell per creare un pacchetto di regole di classificazione in base all'impronta digitale del documento


> [!TIP]
> Anche se è possibile creare e modificare i pacchetti di regole di classificazione in Shell, è possibile che la creazione delle impronte digitali del documento è più semplice in EAC. È consigliabile che non vi è provare prima di tentare di questa procedura in Shell.



DLP usa i pacchetti di regole di classificazione per individuare il contenuto riservato nei messaggi. Per creare un pacchetto di regole di classificazione in base a un impronta digitale del documento, utilizzare i cmdlet **New-Fingerprint** e **New-DataClassification**. Poiché i risultati di **New-Fingerprint** non vengono archiviati al di fuori della regola di classificazione dei dati, eseguire sempre **New-Fingerprint** e **New-DataClassification** o **Set-DataClassification** nella stessa sessione di PowerShell. In questo esempio viene creata una nuova impronta digitale di documento in base al file C:\\Documenti\\Contoso Employee Template.docx. La nuova impronta digitale viene archiviata come variabile e potrà essere quindi utilizzata con il cmdlet **New-DataClassification** nella stessa sessione di PowerShell.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Employee Template.docx" -Encoding byte
    $Employee_Fingerprint = New-Fingerprint -FileData $Employee_Template -Description "Contoso Employee Template"

A questo punto, passiamo alla creazione di una nuova regola di classificazione dati denominata "Contoso Employee Confidential" che utilizza l'impronta digitale del documento del file C:\\Documenti\\Contoso Customer Information Form.docx.

    $Employee_Template = Get-Content "C:\My Documents\Contoso Customer Information Form.docx" -Encoding byte
    $Customer_Fingerprint = New-Fingerprint -FileData $Customer_Form -Description "Contoso Customer Information Form"
    New-DataClassification -Name "Contoso Customer Confidential" -Fingerprints $Customer_Fingerprint -Description "Message contains Contoso customer information." 

È ora possibile utilizzare il cmdlet **Get-DataClassification** per trovare tutti i pacchetti di regole di classificazione dei dati DLP e, in questo esempio, "Contoso Customer Confidential" fa parte dell'elenco dei pacchetti di regole di classificazione dei dati.

Infine, aggiungere il pacchetto di regole di classificazione dati "Contoso Customer Confidential" a un criterio DLP.

    New-TransportRule -Name "Notify :External Recipient Contoso confidential" -NotifySender NotifyOnly -Mode Enforce -SentToScope NotInOrganization -MessageContainsDataClassification @{Name=" Contoso Customer Confidential"}

L'agente DLP rileva ora i documenti che soddisfano l'impronta digitale del documento Contoso Customer Form.docx.

Per informazioni sulla sintassi e sui parametri, vedere [New-Fingerprint](https://technet.microsoft.com/it-it/library/dn584142\(v=exchg.150\)), [New-DataClassification](https://technet.microsoft.com/it-it/library/dn584139\(v=exchg.150\)), [Set-DataClassification](https://technet.microsoft.com/it-it/library/dn584141\(v=exchg.150\)) e [Get-DataClassification](https://technet.microsoft.com/it-it/library/jj215720\(v=exchg.150\)).

## Ulteriori informazioni

[Creazione impronta digitale documenti](overview-of-document-fingerprinting-in-exchange.md)

[Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md)

[Integrazione di regole di informazioni sensibili con le regole di trasporto](https://docs.microsoft.com/it-it/exchange/security-and-compliance/data-loss-prevention/integrate-sensitive-information-rules)

