---
title: 'Esportare i tipi di informazioni riservate DLP da Exchange 2013: Exchange 2013 Help'
TOCTitle: Esportare i tipi di informazioni riservate DLP di Exchange
ms:assetid: 8f02fbc2-dd1c-4276-be1a-517a43fe39b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn479225(v=EXCHG.150)
ms:contentKeyID: 59634578
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Esportare i tipi di informazioni riservate DLP da Exchange 2013

 

_**Si applica a:**Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:**2016-05-04_

È possibile visualizzare o modificare i dettagli relativi all'interno dei criteri DLP senza utilizzare i cmdlet Exchange Management ShellInterfaccia di amministrazione di Exchange (EAC) esportando i criteri, vengono salvati in un file XML e la modifica di file XML. In genere è necessario reimportare il file XML in Exchange. In questo modo, i criteri possono essere modificati indipendenti Exchange. Tuttavia, è necessario che soddisfino i requisiti di formato specifico, anche noto come XML schema per il funzionamento.

Per altre attività di gestione relative a DLP, vedere [Gestire i criteri DLP](manage-dlp-policies-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare

  - Tempo stimato per il completamento: 15 minuti

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Prevenzione della perdita di dati (DLP)" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata

L'interfaccia di amministrazione di Exchange non fornisce un modo per esportare i criteri DLP o modelli in un file esterno. Per eseguire questa attività, utilizzare Exchange Management Shell.

## Utilizzare Exchange Management Shell per esportare i tipi di informazioni riservate DLP

In questo esempio Esporta tutti i tipi di informazioni riservate DLP insieme ai relativi attributi in un file XML nel percorso C:\\My Documents\\exportedInformationTypes.xml. È consigliabile impostare una copia di backup dell'insieme di tipi di informazioni riservate DLP corrente. Per ottenere questo risultato, è per esportare e copiare immediatamente e rinominare lo stesso file XML.

1.  Aprire Exchange Management Shell.

2.  Tipo **Get-ClassificationRuleCollection**e tipi di informazioni riservate dell'organizzazione dovrebbero essere visualizzati sullo schermo. Se è stata creata qualsiasi tipo di informazioni riservate personale, si verrà visualizzato solo l'impostazione predefinita, insieme di tipi incorporati informazioni riservate, denominata "Pacchetto Microsoft Rule".

3.  Archiviare i tipi di informazioni riservate in una variabile digitando **$ruleCollections = Get-ClassificationRuleCollection**.

4.  Ora l'esecuzione di un file XML formattato con tutti i dati digitando **Set-Content - path "C:\\My Documents\\exportedRules.xml"-Encoding Byte-valore $ruleCollections.SerializedClassificationRuleCollection**..

È ora possibile modificare il file XML per modificare i criteri in base alle esigenze. Per informazioni su come personalizzare i tipi di informazioni riservate incorporati, vedere [Personalizzare i tipi di informazioni riservate DLP incorporati](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md). Per ulteriori informazioni su come importare i criteri in Exchange, vedere [Importare un modello di criteri DLP personalizzato da un file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md).

## Ulteriori informazioni

[Cosa cercare i tipi di informazioni riservate in Exchange](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[Personalizzare i tipi di informazioni riservate DLP incorporati](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)

[Importare un modello di criteri DLP personalizzato da un file](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

