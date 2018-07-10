---
title: 'Configurare i cellulari per accedere alla posta elettronica: Exchange 2013 Help'
TOCTitle: Configurare i cellulari per accedere alla posta elettronica
ms:assetid: 8d6e2cea-265a-43d9-a074-076f35658436
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Bb123704(v=EXCHG.150)
ms:contentKeyID: 52057295
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurare i cellulari per accedere alla posta elettronica

 

_**Si applica a:** Exchange Online, Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2015-03-12_

È possibile configurare un telefono cellulare, ad esempio un Windows Phone, per utilizzare MicrosoftExchange ActiveSync. Questa procedura deve essere eseguita su ogni telefono cellulare dell'organizzazione.

## Prerequisiti

  - L'utente deve aver letto con attenzione la documentazione del produttore relativa al telefono cellulare che si desidera configurare.

  - Exchange ActiveSync è abilitato nell'organizzazione.


> [!NOTE]
> Per specifici del dispositivo informazioni su come configurare Microsoft posta elettronica basata su Exchange in un cellulare o tablet, vedere <A href="https://support.office.com/en-us/article/set-up-a-mobile-device-using-office-365-for-business-7dabb6cb-0046-40b6-81fe-767e0b1f014f">configurare un dispositivo mobile con Office 365 per aziende</A>.



## Configurazione di un telefono cellulare per l'utilizzo di Exchange ActiveSync

La maggior parte dei telefoni cellulari e dei dispositivi mobili è in grado di utilizzare l'individuazione automatica per configurare il client di posta elettronica per dispositivi mobili per utilizzare Exchange ActiveSync. Per configurare un account di posta elettronica sulla maggior parte dei cellulari, sarà necessario disporre di due informazioni.

  - L'indirizzo di posta elettronica dell'utente

  - La password dell'utente

Se il telefono cellulare è in grado di connettersi al server Exchange automaticamente tramite servizio di individuazione automatica, sarà necessario configurare manualmente il telefono cellulare. Indirizzo di posta elettronica dell'utente e password, nonché il nome del server di Exchange ActiveSync richiede l'installazione manuale. Nella maggior parte delle organizzazioni, il nome del server di Exchange ActiveSync è lo stesso nome del server Outlook Web App senza /owa, ad esempio mail.contoso.com.

## Sincronizzazione di Windows Phone

Se si configura un cellulare Windows Phone per la sincronizzazione con la cassetta postale di Exchange tramite Exchange ActiveSync, è supportato solo un sottoinsieme di impostazioni di criteri cassette postali per dispositivi mobili. Tali impostazioni dei criteri sono illustrati in dettaglio in [Supportato criteri cassetta postale di dispositivo mobile per Windows Phone e dispositivi](supported-mobile-device-mailbox-policies-for-windows-phones-and-devices-exchange-2013-help.md).

Se si configurano impostazioni di criteri di cassette postali per dispositivi mobili che non sono supportate dalla versione del Windows Phone in uso, sarà inoltre necessario impostare il criterio **AllowNonProvisionableDevices** su true oppure creare un altro criterio cassette postali per dispositivi mobili per cellulari Windows Phone.

