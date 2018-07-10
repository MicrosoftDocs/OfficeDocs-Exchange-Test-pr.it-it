---
title: 'Criteri cassetta postale di Outlook Web App: Exchange 2013 Help'
TOCTitle: Criteri cassetta postale di Outlook Web App
ms:assetid: 213b8b7a-1c29-49ee-8c98-d0364ddf4f9d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd335142(v=EXCHG.150)
ms:contentKeyID: 50480216
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Criteri cassetta postale di Outlook Web App

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2012-10-05_

Utilizzare i criteri cassetta postale di MicrosoftOutlook Web App per creare criteri a livello di organizzazione per la gestione dell'accesso alle funzionalità di Outlook Web App.

**Sommario**

Outlook Web App mailbox policies

Creating or deleting Outlook Web App mailbox policies

Configuring Outlook Web App mailbox policies

Applying Outlook Web App mailbox policies

## Criteri cassetta postale di Outlook Web App

In Exchange 2013, è possibile creare più criteri cassetta postale di Outlook Web App e applicarli alle singole cassette postali. Quando viene applicato un criterio cassetta postale di Outlook Web App a una cassetta postale, questo avrà la precedenza sulle impostazioni della directory virtuale.

È possibile gestire le funzionalità di Outlook Web App anche configurando le directory virtuali di Outlook Web App. Le impostazioni delle directory virtuali verranno utilizzate per tutte le cassette postali a cui non è applicato un criterio cassetta postale.

## Creazione o eliminazione dei criteri cassetta postale di Outlook Web App

Un criterio cassetta postale di Outlook Web App predefinito viene creato automaticamente quando si installa Exchange. Per impostazione predefinita, tutte le opzioni vengono abilitate nel criterio cassetta postale di Outlook Web App predefinito. È possibile creare tutti i criteri cassetta postale di Outlook Web App necessari a soddisfare le esigenze relative alla configurazione.


> [!NOTE]
> Il criterio cassetta postale di Outlook Web App predefinito non viene applicato automaticamente alle cassette postali.



Per informazioni su creazione e rimozione dei criteri cassetta postale, vedere [Creare un criterio cassetta postale di Outlook Web App](create-an-outlook-web-app-mailbox-policy-exchange-2013-help.md) e [Rimuovere un criterio cassetta postale di Outlook Web App da Exchange](remove-an-outlook-web-app-mailbox-policy-from-exchange-exchange-2013-help.md).

## Configurazione dei criteri cassetta postale di Outlook Web App

Per impostazione predefinita, tutte le opzioni del criterio cassetta postale di Outlook Web App predefinito sono abilitate. Per informazioni sulla configurazione dei criteri cassetta postale di Outlook Web App, vedere [Visualizzazione o configurazione delle proprietà dei criteri cassetta postale di Outlook Web App](view-or-configure-outlook-web-app-mailbox-policy-properties-exchange-2013-help.md).

## Applicazione dei criteri cassetta postale di Outlook Web App

È possibile applicare solo un criterio cassetta postale di Outlook Web App a una cassetta postale.

Se non vi è alcun criterio cassetta postale di Outlook Web App applicato a una cassetta postale, verranno applicate le impostazioni definite nella directory virtuale.

Un criterio cassetta postale di Outlook Web App può essere applicato a una cassetta postale utilizzando l'interfaccia di amministrazione di Exchange per modificare una cassetta postale esistente oppure utilizzando Shell e il cmdlet [Set-CASMailbox](https://technet.microsoft.com/it-it/library/bb125264\(v=exchg.150\)). Per ulteriori informazioni, vedere [Applicare o rimuovere un criterio cassetta postale di Outlook Web App in una cassetta postale](apply-or-remove-an-outlook-web-app-mailbox-policy-on-a-mailbox-exchange-2013-help.md).

