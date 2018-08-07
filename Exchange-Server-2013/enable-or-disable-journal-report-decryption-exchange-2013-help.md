---
title: 'Attiva/disattiva decrittografia rapporti del Journal: Exchange 2013 Help'
TOCTitle: Attivare o disattivare la decrittografia dei rapporti del Journal
ms:assetid: 1dedbe73-2c1a-4b14-8799-5091aaec7965
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dd638092(v=EXCHG.150)
ms:contentKeyID: 50480179
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Attivare o disattivare la decrittografia dei rapporti del Journal

 

_**Si applica a:** Exchange Server 2013_

_**Ultima modifica dell'argomento:** 2016-12-09_

Decrittografia dei rapporti del journal abilitazione consente l'agente di Journaling collegare una copia di un messaggio protetto con RMS decrittografata al rapporto del journal. Prima di abilitare decrittografia dei rapporti del journal, è necessario aggiungere la cassetta postale di recapito federato per il gruppo di utenti con privilegi avanzati configurato sul server di [Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx) .

Per altre attività di gestione relative a Information Rights Management (IRM), vedere [Procedure di Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Che cosa è necessario sapere prima di iniziare?

  - Tempo stimato per il completamento: 1 minuto

  - Per eseguire queste procedure, è necessario disporre delle autorizzazioni appropriate. Per sapere quali autorizzazioni sono necessarie, vedere "Protezione dei diritti" nell'argomento [Criteri di messaggistica e autorizzazioni di conformità](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Ai membri del gruppo di utenti con privilegi avanzati viene concessa una licenza d'uso con diritti di proprietario quando richiedono una licenza dal cluster AD RMS. Ciò consente loro di decrittografare tutto il contenuto protetto con RMS creato dal cluster AD RMS.

  - Un cluster AD RMS deve essere installato nella foresta di Active Directory.

  - La cassetta postale di recapito federativo è stata aggiunta al gruppo di utenti con privilegi avanzati di AD RMS. Per ulteriori informazioni, vedere [Aggiungere la cassetta postale di federazione per il gruppo di utenti con privilegi avanzati di AD RMS](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

  - Non è possibile utilizzare Interfaccia di amministrazione di Exchange per abilitare la decrittografia del rapporto del journal. È necessario utilizzare la shell.

  - Per informazioni sui tasti di scelta rapida che è possibile utilizzare con le procedure in questo argomento, vedere [Tasti di scelta rapida nell'interfaccia di amministrazione di Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Problemi? È possibile richiedere supporto nei forum di Exchange. I forum sono disponibili sui seguenti siti: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Operazione desiderata?

## Abilitazione della decrittografia dei rapporti del journal tramite Shell

In questo esempio viene abilitata la decrittografia dei rapporti del journal per l'organizzazione di Exchange.

    Set-IRMConfiguration -JournalReportDecryptionEnabled $true

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Disabilitazione della decrittografia dei rapporti del journal tramite Shell

In questo esempio viene disabilitata la decrittografia dei rapporti del journal per l'organizzazione di Exchange.

    Set-IRMConfiguration -JournalReportDecryptionEnabled $false

Per informazioni dettagliate sulla sintassi e sui parametri, vedere [Set-IRMConfiguration](https://technet.microsoft.com/it-it/library/dd979792\(v=exchg.150\)).

## Come verificare se l'operazione ha avuto esito positivo?

Per verificare di aver abilitato o disabilitato la decrittografia del rapporto del journal, eseguire il cmdlet **Get-IRMConfiguration** e verificare il valore della proprietà *JournalDecryptionEnabled*.

Per un esempio di come controllare la configurazione IRM, vedere [Examples](https://technet.microsoft.com/it-it/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples) in **Get-IRMConfiguration**.

